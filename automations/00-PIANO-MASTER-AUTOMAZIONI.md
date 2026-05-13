**Versione:** 3.0
**Ultimo aggiornamento:** 2026-05-13
**Status:** Fase 1 review Lorenzo completata. Fase 2 refactor architetturale completato (06 Primo Cliente + 07 Cliente Ricorrente + 14 flow prodotto 08-21). In attesa review Lorenzo Fase 2.

# Piano Master — Automazioni Email Klaviyo

## Obiettivo

Ricostruire da zero tutte le automazioni email di Paleocomplex per la migrazione da ActiveCampaign a Klaviyo. Strategia basata su:
- Dati performance delle vecchie 218 email (revenue €195K totale)
- Flow stato cliente + flow prodotto paralleli (architettura modulare)
- Riduzione drastica del volume per CLIENTE (non per flow) con focus su ROI per invio
- Best practice Klaviyo (documentazione ufficiale + academy)

## Decisioni prese

1. **Authority + Post Purchase non si sovrappongono.** Chi compra entra SOLO nel Post Purchase. L'Authority Flow si sospende. Chi NON compra dopo il welcome entra nell'Authority completo.
2. **Architettura post-purchase a due binari paralleli** (refactor maggio 2026):
   - **Flow stato cliente** (06 Primo Cliente Assoluto, 07 Cliente Ricorrente): parlano della relazione brand, mai del prodotto specifico
   - **Flow prodotto** (08-21, uno per SKU): trigger basato sull'acquisto di un prodotto MAI acquistato prima. Contengono istruzioni + aspettative + social proof specifici del prodotto.
   - I due binari girano in parallelo, i timing non si sovrappongono.
   - Vantaggio: un cliente esistente che compra Elisir per la prima volta riceve sia il flow Cliente Ricorrente sia il flow prodotto Elisir (educazione specifica). Architettura modulare, manutenzione pulita.
3. **Optin marketing nel post-purchase:** P.S. soft in email 2 e 3 solo per chi non ha optin. Non prioritario (99.9% ha gia' autorizzato).
4. **Email educative vecchie (157 email Automazione Italia + Finale):** NON migrate come automazione. Le migliori 15-20 diventano contenuto per newsletter settimanale (campaign). Tenute a lato per riuso.
5. **Cross-sell sport trasversale:** Hurricane e Armageddon proposti come blocco trasversale nell'email 2 del flow Cliente Ricorrente.
6. **Retention/Cross-sell: flow separati per prodotto**, non un unico flow con condizionali. Ogni flow ha trigger, timing e contenuto specifico per prodotto. **Trigger: Fulfilled Order** (non Placed Order) — il cliente deve aver ricevuto il prodotto.
7. **Carrello abbandonato: conditional split nuovo vs. esistente** nella email 2. Nuovo cliente: risposta obiezioni + eventuale incentivo. Cliente esistente: tono diverso, no sconto. NO split per valore carrello. Codici sconto univoci. Re-ingresso limitato a 1 volta ogni 7 giorni. Disabilitare email carrello nativo WooCommerce.
8. **Welcome series: email 4 a +7gg per chi non ha acquistato.** Dato Klaviyo: la maggior parte degli acquisti avviene entro 10 giorni. Email 4 = "ultima occasione" con tono lettera personale Lorenzo + reminder sconto BENVENUTO.
9. **Welcome da lead magnet specifico: contenuto e prodotti coerenti con il tema del lead magnet**. **L'Authority parte DOPO il completamento della welcome** (sequenziale, NON in parallelo). La storia di Lorenzo è nel welcome, l'Authority non la ripete.
10. **Win-back: doppio approccio.** (A) Flow basato su timing fisso: +85gg dall'ultimo ordine (ciclo medio Paleocomplex = 76gg). (B) Segmento Klaviyo Predictive Analytics per intercettare chi sta performando sotto la media indipendentemente dal timing.
11. **Browse Abandonment: filtro prodotto gia' acquistato.** Se l'utente ha gia' comprato quel prodotto, il flow NON parte.
12. **Compleanno: parcheggiato.** Lo attiviamo appena abbiamo un sistema che raccoglie la data di nascita.
13. **VNR vs RDA:** Alla prima menzione di VNR nelle email, scrivere per esteso "Valore Nutritivo di Riferimento". Aggiungere il concetto: gli altri integratori si basano sul VNR (minimo per non ammalarsi nel breve termine), i nostri danno il 100% dell'RDA (apporto massimo giornaliero). Applicare a: Authority, Conversione, Welcome Series dove si citano dosaggi.
14. **Blog: "centinaia" non "decine":** Quasi 300 articoli. Applicare a: Authority flow.
15. **Disclaimer recensioni:** "I risultati sono personali" dopo le recensioni. Per recensioni che citano vitamina D: aggiungere consiglio di integrare con gocce di Vitamina D. Applicare a: Conversione (email con social proof), flow prodotto 08-21 (email social proof).
16. **Trigger flow prodotto: basato su SKU** (refactor maggio 2026). Ogni flow prodotto (08-21) ha trigger `Placed Order` + filter `Item SKU equals X` + filter `Has not placed order with SKU X over all time before this event`. Trigger SKU-based (non match stringa) per evitare ambiguità tra prodotti con nome simile.
17. **Cliente Ricorrente cross-sell: esclusione "già posseduto":** ogni sotto-blocco di suggerimento nell'email 2 del flow 07 è condizionato su "Customer has not placed order with item SKU X over all time" → non proponiamo prodotti che il cliente ha già nel protocollo.

## Architettura dei flow

### FASE 1 — Flow critici per revenue (6 flow, 35 email)

| # | Flow | File | Email | Trigger | Status |
|---|------|------|-------|---------|--------|
| 1 | Carrello abbandonato | `fase1/01-carrello-abbandonato.md` | 3 | Checkout started + non completato | Review Lorenzo OK 16/04 — applicare correzioni #13-15 poi chiudere |
| 2 | Welcome Kit Benessere | `fase1/02-welcome-kit-benessere.md` | 5 | Optin da popup/homepage/blog/landing social | Review Lorenzo OK 16/04 |
| 3 | Welcome Unghie/Capelli | `fase1/03-welcome-unghie-capelli.md` | 6 | Optin da lead magnet unghie/capelli | Review Lorenzo OK 16/04 |
| 4 | Authority Flow | `fase1/04-authority-flow.md` | 6 | DOPO completamento welcome (sequenziale) + non ha comprato | v3.0 — email 2 VNR vs apporto massimo legale |
| 5 | Browse Abandonment | `fase1/05-browse-abandonment.md` | 2 | Viewed Product + non ha comprato + max 1 volta ogni 30gg | Review Lorenzo OK 16/04 |
| 6 | Conversione | `fase1/06-conversione.md` | 10 | DOPO Authority + non ha comprato. 32 giorni. Sconto PRIMOPASSO nell'ultima email | Review Lorenzo OK 16/04 |

### FASE 2 — Flow post-acquisto (16 flow)

**Architettura a due binari paralleli:**

#### Binario A — Flow stato cliente (2 flow, 8 email)

| # | Flow | File | Email | Trigger | Status |
|---|------|------|-------|---------|--------|
| 6 | Primo Cliente Assoluto | `fase2/06-primo-cliente.md` | 3 | Placed Order + Has Placed Order = 1 over all time | v1.0 2026-05-13 — In attesa review Lorenzo |
| 7 | Cliente Ricorrente | `fase2/07-cliente-ricorrente.md` | 2 | Placed Order + Has Placed Order >= 2 over all time | v1.0 2026-05-13 — In attesa review Lorenzo |

Contenuto:
- **06 Primo Cliente**: Benvenuto Lorenzo (+2h) → Ottimizza abitudini Lorenzo (+12gg) → Richiesta recensione Flaminia (+32gg)
- **07 Cliente Ricorrente**: Grazie + costanza Lorenzo (+2h) → Cross-sell Flaminia (+3gg, blocchi dinamici con esclusione "già posseduto")

#### Binario B — Flow prodotto (14 flow, 42 email)

Ogni flow è triggerato dall'acquisto di uno specifico SKU **per la prima volta in assoluto**. Gira in parallelo ai flow stato cliente.

| # | Flow | File | SKU | Email | Status |
|---|------|------|-----|-------|--------|
| 8 | Paleocomplex | `fase2/08-paleocomplex.md` | `paleocomplex` | 3 | v0.2 — review Andrea OK |
| 9 | Paleocomplex Revolution | `fase2/09-paleocomplex-revolution.md` | `paleocomplex-revo` | 3 | v0.1 — in attesa review |
| 10 | Elisir | `fase2/10-elisir.md` | `elisir` | 3 | v0.1 |
| 11 | Elisir Basic | `fase2/11-elisir-basic.md` | `elisir-basic` | 3 | v0.1 |
| 12 | Essentiel | `fase2/12-essentiel.md` | `essentiel` | 3 | v0.1 |
| 13 | Youth | `fase2/13-youth.md` | `youth` | 3 | v0.1 |
| 14 | Jeunesse | `fase2/14-jeunesse.md` | `jeunesse` | 3 | v0.1 |
| 15 | Hurricane | `fase2/15-hurricane.md` | `hurricane` | 3 | v0.1 |
| 16 | Armageddon | `fase2/16-armageddon.md` | `armageddon` | 3 | v0.1 |
| 17 | Artosan | `fase2/17-artosan.md` | `artosan` | 3 | v0.1 |
| 18 | Liverty | `fase2/18-liverty.md` | `liverty` | 3 | v0.1 |
| 19 | Testoplus | `fase2/19-testoplus.md` | `testo-plus` | 3 | v0.1 |
| 20 | Renaissance | `fase2/20-renaissance.md` | `renaissance` | 3 | v0.1 |
| 21 | Vitamina D | `fase2/21-vitamina-d.md` | `vitamina-d` | 3 | v0.1 |

Struttura standard di ogni flow prodotto:
- Email 1 (+1gg, Lorenzo): Istruzioni assunzione specifiche del prodotto
- Email 2 (+5gg, Lorenzo): Aspettative + tempi di risposta del prodotto
- Email 3 (+18gg, Flaminia): Social proof con recensioni verificate + check-in

**Esempio di incastro timing** (cliente nuovo che compra Paleocomplex):

```
T+2h    [06 Stato]   Benvenuto Lorenzo
T+1gg   [08 Paleo]   Istruzioni Paleocomplex
T+5gg   [08 Paleo]   Aspettative multivitaminico
T+12gg  [06 Stato]   Ottimizza abitudini
T+18gg  [08 Paleo]   Social proof Paleocomplex (Flaminia)
T+32gg  [06 Stato]   Recensione brand (Flaminia)
```

Gap minimo tra invii ≥ 2 giorni. Sequenza alternata Lorenzo/Flaminia.

**Esempio cliente ricorrente che compra Elisir per la prima volta** (al suo 3° ordine):

```
T+2h    [07 Stato]   Grazie + costanza Lorenzo
T+1gg   [10 Elisir]  Istruzioni Elisir
T+3gg   [07 Stato]   Cross-sell Flaminia (esclude prodotti già posseduti)
T+5gg   [10 Elisir]  Aspettative multivitaminico
T+18gg  [10 Elisir]  Social proof Elisir (Flaminia)
```

### FASE 3 — Flow di retention e lifecycle (11 flow, ~29 email + 1 azione)

| # | Flow | File | Email | Trigger | Timing cross-sell | Timing riacquisto | Status |
|---|------|------|-------|---------|-------------------|-------------------|--------|
| 22 | Retention Elisir/EB | `fase3/22-retention-elisir.md` | 3 | Fulfilled Order con Elisir o EB | gg 28 | gg 35 | Da scrivere |
| 23 | Retention Paleo/Rev | `fase3/23-retention-paleo.md` | 3 | Fulfilled Order con Paleo o Rev | gg 20 | gg 25 | Da scrivere |
| 24 | Retention Youth | `fase3/24-retention-youth.md` | 3 | Fulfilled Order con Youth | gg 20 | gg 25 | Da scrivere |
| 25 | Retention Jeunesse | `fase3/25-retention-jeunesse.md` | 3 | Fulfilled Order con Jeunesse | gg 35 | gg 45 | Da scrivere |
| 26 | Retention Sport | `fase3/26-retention-sport.md` | 3 | Fulfilled Order con Hurricane o Armageddon | gg 20 | gg 25 | Da scrivere |
| 27 | Retention Generico | `fase3/27-retention-generico.md` | 3 | Fulfilled Order con Artosan/Liverty/Testoplus/Renaissance/VitD | gg 45 | gg 55 | Da scrivere |
| 28 | Win-back (timing) | `fase3/28-winback.md` | 4 | Nessun ordine da 85+ giorni | — | — | Da scrivere |
| 29 | Win-back (predictive) | `fase3/29-winback-predictive.md` | 2 | Klaviyo Predictive: churn risk alto | — | — | Da scrivere |
| 30 | Back in Stock | `fase3/30-back-in-stock.md` | 1 | Subscribed to Back In Stock + prodotto torna disponibile | — | — | Da scrivere |
| 31 | Sunset (pulizia lista) | `fase3/31-sunset.md` | 2 + azione | Segmento: iscritto 180+ gg, 0 aperture/click/ordini, 5+ email | — | — | Da scrivere |
| 32 | Programma Fedeltà | `fase3/32-programma-fedelta.md` | 4 | Raggiungimento livello Club/Silver/Gold/Elite | — | — | Da scrivere |

### FUTURO — Da attivare quando pronti

| # | Flow | Email | Prerequisito | Status |
|---|------|-------|-------------|--------|
| 33 | Compleanno | 1 | Sistema raccolta data di nascita (campo checkout o form) | Parcheggiato |

## Conteggio totale

| Fase | Flow | Email |
|------|------|-------|
| Fase 1 | 6 flow | 35 email |
| Fase 2 stato cliente | 2 flow | 8 email |
| Fase 2 prodotto | 14 flow | 42 email |
| Fase 3 | 11 flow | ~29 email + 1 azione |
| **Totale** | **33 flow** | **~114 email** |

**Nota volume per cliente medio**: il numero email totali è alto, ma ogni cliente riceve solo una frazione (dipende dai prodotti acquistati). Un nuovo cliente che compra 1 prodotto riceve circa 6 email nel primo mese (3 stato + 3 prodotto). Un cliente con 3 prodotti diversi nello stesso ordine ne riceve circa 12 in 32 giorni (3 stato + 3×3 prodotto), distribuiti senza sovrapposizioni.

## Matrice cross-sell

(Riferimento per il flow 07 Cliente Ricorrente)

| Ha comprato | Cross-sell primario | Cross-sell sport |
|-------------|--------------------|--------------------|
| Elisir / Elisir Basic | Jeunesse o Renaissance | Hurricane + Armageddon |
| Paleocomplex | Revolution (upgrade) o Youth | Hurricane + Armageddon |
| Revolution | Elisir (upgrade) o Renaissance | Hurricane + Armageddon |
| Essentiel | Youth o Liverty | Hurricane + Armageddon |
| Youth | Jeunesse (upgrade) + multivitaminico se manca | Armageddon (anti-sarcopenia) |
| Jeunesse | Renaissance (anti-aging completo) + multivitaminico | Hurricane + Armageddon |
| Hurricane | Armageddon + multivitaminico | — |
| Armageddon | Hurricane + multivitaminico | — |
| Artosan/Liverty/Testoplus/Renaissance/VitD | Multivitaminico come base | Hurricane + Armageddon |

Nel flow 07, ogni suggerimento è condizionato su "il cliente non ha già acquistato quel prodotto" (logica esclusione "già posseduto").

## Note tecniche Klaviyo

### Funzionalità da sfruttare
- **Dynamic table blocks:** prodotti nel carrello abbandonato (flow 1)
- **Show/Hide blocks:** sotto-blocchi condizionali nel flow 07 cross-sell
- **Trigger SKU-based:** per i 14 flow prodotto (08-21) — `Item SKU equals X` + `zero times before`
- **Codici sconto univoci:** per carrello e win-back (impediscono condivisione)
- **Smart Sending:** attivo su tutti i flow TRANNE Back in Stock
- **Predictive Analytics:** churn risk per win-back predictive (29), expected next order date per retention
- **A/B test nativi:** testare subject line su ogni flow, UNA variabile alla volta, minimo 500 destinatari per variante
- **Back in Stock button:** widget nativo per WooCommerce sulle pagine prodotto esaurite

### Metriche da monitorare per flow
- **Click Rate** (metrica primaria — non influenzata da Apple Mail Privacy)
- Open Rate (secondaria, gonfiata da MPP)
- Conversion Rate (placed orders / recipients)
- Revenue per Recipient
- Unsubscribe Rate (alert se supera 0.5%)

### Prerequisiti tecnici
- [ ] Disabilitare email carrello abbandonato nativo WooCommerce
- [ ] Configurare widget Back in Stock sulle pagine prodotto
- [ ] Verificare piano Klaviyo per accesso a Predictive Analytics
- [ ] Creare segmento Sunset con i criteri indicati
- [ ] Configurare proprietà profilo "Unengaged" per la soppressione
- [ ] Validare SKU esatti in WooCommerce (lista in tabella Fase 2B sopra)
- [ ] Testare logica trigger "Has not placed order with SKU X over all time before" su Klaviyo per flow prodotto 08-21

## Regole di scrittura email

Riferimento: `context/email-rules.md`

Punti chiave:
- Tono Lorenzo: diretto, schietto, scientifico ma accessibile
- Claims prudenti: "supporta", "aiuta", "può contribuire"
- No emoji, no elenchi puntati nel corpo, no trattini lunghi
- Apertura "Ciao [NOME]" SENZA virgola (placeholder Klaviyo) — a capo con maiuscola
- Ogni email: 3 varianti oggetto A/B + 3 varianti preview text
- Grassetti strategici, frasi brevi, paragrafi corti (mobile-first)
- MAI inventare dati, dosaggi, ingredienti — verificare SEMPRE su schede prodotto e etichette
- **Conteggio nutrienti:** mai usare "più" prima del numero totale. Usare "con", "tra cui" o ":"
- **Verifica obbligatoria:** ogni claim su ingredienti, dosaggi, forme vitaminiche e conteggi va incrociato con `context/products/[nome]-scheda-prodotto.md` prima di scrivere
- Usare sempre accenti reali (è, à, ò, ù, é) — MAI apostrofo al posto dell'accento
- **Linguaggio gender-neutral:** evitare "Benvenuto/a". Usare forme neutre

### Mittenti per tipo di flow

| Mittente | Flow | Firma |
|----------|------|-------|
| **Lorenzo Zarone** | Welcome (tutte), Authority (tutte), Conversione, Flow prodotto 08-21 (email 1 e 2), Flow stato cliente 06-07 (email 1 e 2 primo cliente, email 1 ricorrente), Win-back, Email "ultima occasione" | Un forte abbraccio · Lorenzo Zarone · Fondatore di Paleocomplex |
| **Flaminia (Customer Care)** | Flow prodotto 08-21 email 3 social proof, Flow stato cliente 06 email 3 recensione + 07 email 2 cross-sell | Flaminia · Customer Care Paleocomplex |
| **Team Paleocomplex** | Carrello abbandonato, Browse abandonment, Back in stock, Programma fedeltà, Sunset | Team Paleocomplex |

### Open loop (cliffhanger) tra email

Tecnica: chiusura email N con promessa specifica e curiosa sulla N+1.

| Flow | Open loop |
|------|-----------|
| Authority Flow (4) | SÌ — tutte le email (6/6) |
| Welcome Kit Benessere (2) | SÌ — solo 2-3 punti chiave |
| Welcome Unghie/Capelli (3) | SÌ — solo 2-3 punti chiave |
| Conversione (6) | SÌ — 3-4 punti strategici |
| Flow prodotto 08-21 | SÌ — open loop interno (email 1→2 e 2→3) |
| Flow stato cliente 06-07 | NO (eccetto email 1 → "Flaminia ti scriverà tra qualche giorno") |
| Carrello, Browse, Retention, Win-back, Back in Stock | NO |

## Fonti dati per la scrittura

- Schede prodotto: `context/products/[nome]-scheda-prodotto.md`
- Mappa scelta integratori: `context/products/mappa-scelta-integratori.md`
- FAQ ufficiali: `context/faq-sito.md`
- Etichette originali: `context/labels/`
- Recensioni reali: `context/20260511 paleocomplex export-reviews.csv` (aggiornato maggio 2026, 418 recensioni)
- Dati performance vecchie email: `input/paleo mappatura/`
- Analisi ex clienti: `context/analysis/analisi sondaggio ex clienti.md`

## Come usare questo documento

1. Prima di scrivere qualsiasi email, consultare questo piano per capire dove si inserisce
2. Ogni flow ha il suo file dedicato nella sottocartella della fase
3. Quando un flow è completato, aggiornare lo Status nella tabella sopra
4. Se cambia l'architettura aggiornare QUESTO documento
5. Per i flow prodotto: il template è il flow 08 (Paleocomplex), validato con Andrea. Variazioni nei singoli flow per dosaggi/recensioni/aspettative specifiche del prodotto
6. Per prerequisiti tecnici Klaviyo: vedi checklist nella sezione "Note tecniche Klaviyo"

## Changelog

- **v3.0 (2026-05-13)**: refactor architetturale Fase 2 maggiore. Il flow monolitico "Post Purchase New Customer" con 14 blocchi condizionali è stato smontato e ricomposto in 16 flow paralleli: 2 stato cliente (06 Primo Cliente, 07 Cliente Ricorrente) + 14 flow prodotto (08-21, uno per SKU). Motivazione: il vecchio schema non garantiva educazione specifica al cliente ricorrente che acquistava un prodotto mai provato (es. cliente compra Youth, poi Elisir: con vecchio schema, niente istruzioni Elisir). Nuovo schema risolve il buco architetturale, manutenzione più pulita, trigger SKU-based (zero ambiguità). Cross-sell flow 07: aggiunta logica esclusione "già posseduto" (Andrea, maggio 2026). Numerazione Fase 3 shiftata a 22-32.
- v2.2 (2026-04-22): Authority v3.0 con email 2 VNR vs apporto massimo legale.
- v2.1 (2026-04-16): Feedback Lorenzo Fase 1 review (correzioni VNR, blog "centinaia", disclaimer recensioni).
- v2.0 (2026-04): Fase 1 completata e in review Lorenzo.
- v1.0 (2026-03): Prima versione del piano master.
