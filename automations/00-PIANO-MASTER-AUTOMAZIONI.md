**Versione:** 6.1
**Ultimo aggiornamento:** 2026-07-13
**Status:** Fase 1 in produzione. Fase 2 montata su Klaviyo (giugno 2026). Fase 3 scritta completa (7 flow, architettura Predictive/RFM/Catalog Insights) — in review Andrea, poi montaggio. Trial Klaviyo Marketing Analytics attivo dal 2026-06-18 (30gg).

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
   - **Flow stato cliente** (21 Primo Cliente Assoluto, 22 Cliente Ricorrente): parlano della relazione brand, mai del prodotto specifico
   - **Flow prodotto** (24-37, uno per SKU): trigger basato sull'acquisto di un prodotto MAI acquistato prima. Contengono istruzioni + aspettative + social proof specifici del prodotto.
   - I due binari girano in parallelo, i timing non si sovrappongono.
   - Vantaggio: un cliente esistente che compra Elisir per la prima volta riceve sia il flow Cliente Ricorrente sia il flow prodotto Elisir (educazione specifica). Architettura modulare, manutenzione pulita.
3. **Optin marketing nel post-purchase:** P.S. soft in email 2 e 3 solo per chi non ha optin. Non prioritario (99.9% ha gia' autorizzato).
4. **Email educative vecchie (157 email Automazione Italia + Finale):** NON migrate come automazione. Le migliori 15-20 diventano contenuto per newsletter settimanale (campaign). Tenute a lato per riuso.
5. **Cross-sell (rivisto giugno 2026): SOLO data-driven.** Unico punto di cross-sell automatico = Flow 78 (Best Cross-Sell Date + Next Best Product, Catalog Insights). La vecchia email 2 del Flow 22 con blocchi famiglia + sport trasversale è stata rimossa (Flow 22 v2.0 = solo grazie).
6. **Retention (rivisto giugno 2026, trial Marketing Analytics):** NIENTE flow retention separati per prodotto. Architettura a 2 livelli: Flow 71 First-Order Reorder (timing fisso per famiglia pack, solo primi clienti) + Flow 72 AI Repeat Purchase (Expected Date of Next Order di Klaviyo Predictive, clienti ricorrenti). Dettaglio completo in `fase3/00-mappatura-fase3.md`.
7. **Carrello abbandonato: conditional split nuovo vs. esistente** nella email 2. Nuovo cliente: risposta obiezioni + eventuale incentivo. Cliente esistente: tono diverso, no sconto. NO split per valore carrello. Codici sconto univoci. Re-ingresso limitato a 1 volta ogni 7 giorni. Disabilitare email carrello nativo WooCommerce.
8. **Welcome series: email 4 a +7gg per chi non ha acquistato.** Dato Klaviyo: la maggior parte degli acquisti avviene entro 10 giorni. Email 4 = "ultima occasione" con tono lettera personale Lorenzo + reminder sconto BENVENUTO.
9. **Welcome da lead magnet specifico: contenuto e prodotti coerenti con il tema del lead magnet**. **L'Authority parte DOPO il completamento della welcome** (sequenziale, NON in parallelo). La storia di Lorenzo è nel welcome, l'Authority non la ripete.
10. **Win-back (rivisto giugno 2026): RFM-driven.** Flow 73 triggerato dall'ingresso nel segmento RFM `At Risk / Needs Attention` (classificazione automatica notturna Klaviyo), con conditional split su Historic CLV (>300€ = 3 email brand-first, ≤300€ = 2 email con sconto diretto). Sostituisce il vecchio doppio approccio timing-fisso + churn-risk.
11. **Browse Abandonment: filtro prodotto gia' acquistato.** Se l'utente ha gia' comprato quel prodotto, il flow NON parte.
12. **Compleanno: parcheggiato.** Lo attiviamo appena abbiamo un sistema che raccoglie la data di nascita.
13. **VNR vs RDA:** Alla prima menzione di VNR nelle email, scrivere per esteso "Valore Nutritivo di Riferimento". Aggiungere il concetto: gli altri integratori si basano sul VNR (minimo per non ammalarsi nel breve termine), i nostri danno il 100% dell'RDA (apporto massimo giornaliero). Applicare a: Authority, Conversione, Welcome Series dove si citano dosaggi.
14. **Blog: "centinaia" non "decine":** Quasi 300 articoli. Applicare a: Authority flow.
15. **Disclaimer recensioni:** "I risultati sono personali" dopo le recensioni. Per recensioni che citano vitamina D: aggiungere consiglio di integrare con gocce di Vitamina D. Applicare a: Conversione (email con social proof), flow prodotto 24-37 (email social proof).
16. **Trigger flow prodotto: basato su SKU** (refactor maggio 2026). Ogni flow prodotto (24-37) ha trigger `Placed Order` + filter `Item SKU equals X` + filter `Has not placed order with SKU X over all time before this event`. Trigger SKU-based (non match stringa) per evitare ambiguità tra prodotti con nome simile.
17. **Esclusione "già posseduto" nel cross-sell:** gestita nativamente dal blocco `Next Best Product` di Klaviyo (Flow 78), che non suggerisce mai prodotti già acquistati dal profilo. (La vecchia implementazione manuale con conditional blocks nel Flow 22 è stata rimossa.)

## Architettura dei flow

### FASE 1 — Flow critici per revenue (6 flow, 35 email)

| # | Flow | File | Email | Trigger | Status |
|---|------|------|-------|---------|--------|
| 1 | Carrello abbandonato | `fase1/01-carrello-abbandonato.md` | 3 | Checkout started + non completato | Review Lorenzo OK 16/04 — applicare correzioni #13-15 poi chiudere |
| 2 | Welcome Kit Benessere | `fase1/02-welcome-kit-benessere.md` | 5 | Optin da popup/homepage/blog/landing social | Review Lorenzo OK 16/04 |
| 3 | Welcome Unghie/Capelli | `fase1/03-welcome-unghie-capelli.md` | 6 | Optin da lead magnet unghie/capelli | Review Lorenzo OK 16/04 |
| 4 | Authority Flow | `fase1/04-authority-flow.md` | 6 | Segmento `Sjna4H` "welcome completato" = OR delle property `flow-02/03/07-...-completed` | ✅ LIVE `YimR66` — v3.2 17/7: **risolto bug** (entrava solo il flow 02; 03 e 07 esclusi) |
| 5 | Browse Abandonment | `fase1/05-browse-abandonment.md` | 2 | Viewed Product + non ha comprato + max 1 volta ogni 30gg | Review Lorenzo OK 16/04 |
| 6 | Conversione | `fase1/06-conversione.md` | 10 | DOPO Authority + non ha comprato. 32 giorni. Sconto PRIMOPASSO nell'ultima email | Review Lorenzo OK 16/04 |
| 7 | Welcome Lead Magnet D3+K2 | `fase1/07-welcome-d3-k2.md` | 2 | Segmento `UadnPz` "lm vitamina d3+k2 social" | ✅ **LIVE** 2026-07-17 — flow `SuFKGT` (creato via API) |

### FASE 2 — Flow post-acquisto (17 flow, slot 21-37, buffer 38-70)

**Architettura a due binari paralleli:**

#### Binario A — Flow stato cliente + universale (3 flow, 5 email)

| # | Flow | File | Email | Trigger | Status |
|---|------|------|-------|---------|--------|
| 21 | Primo Cliente Assoluto | `fase2/21-primo-cliente.md` | 2 | Placed Order + Has Placed Order = 1 over all time | v2.0 2026-06-11 |
| 22 | Cliente Ricorrente | `fase2/22-cliente-ricorrente.md` | 1 | Placed Order + Has Placed Order >= 2 over all time | v2.0 2026-06-18 — solo grazie, cross-sell migrato al Flow 78 |
| 23 | Recensione Brand | `fase2/23-recensione-brand.md` | 1 | Fulfilled Order +32gg | v1.0 2026-06-11 |

Contenuto:
- **21 Primo Cliente**: Benvenuto Lorenzo (+2h dal Placed) → Ottimizza abitudini Lorenzo (+12gg dal Placed)
- **22 Cliente Ricorrente**: Grazie + costanza Lorenzo (+2h dal Placed). Nient'altro: il cross-sell è gestito dal Flow 78 Cross-Sell Data-Driven (Catalog Insights)
- **23 Recensione Brand**: Anticipo richiesta recensione Flaminia (+32gg dal Fulfilled, universale per primi e ricorrenti, anticipa di 2gg l'email automatica WC)

#### Binario B — Flow prodotto (14 flow, 42 email)

Ogni flow è triggerato dall'acquisto di uno specifico SKU **per la prima volta in assoluto**. Gira in parallelo ai flow stato cliente.

| # | Flow | File | SKU | Email | Status |
|---|------|------|-----|-------|--------|
| 24 | Paleocomplex | `fase2/24-paleocomplex.md` | `paleocomplex` | 3 | v0.2 — review Andrea OK |
| 25 | Paleocomplex Revolution | `fase2/25-paleocomplex-revolution.md` | `paleocomplex-revo` | 3 | v0.1 — in attesa review |
| 26 | Elisir | `fase2/26-elisir.md` | `elisir` | 3 | v0.1 |
| 27 | Elisir Basic | `fase2/27-elisir-basic.md` | `elisir-basic` | 3 | v0.1 |
| 28 | Essentiel | `fase2/28-essentiel.md` | `essentiel` | 3 | v0.1 |
| 29 | Youth | `fase2/29-youth.md` | `youth` | 3 | v0.1 |
| 30 | Jeunesse | `fase2/30-jeunesse.md` | `jeunesse` | 3 | v0.1 |
| 31 | Hurricane | `fase2/31-hurricane.md` | `hurricane` | 3 | v0.1 |
| 32 | Armageddon | `fase2/32-armageddon.md` | `armageddon` | 3 | v0.1 |
| 33 | Artosan | `fase2/33-artosan.md` | `artosan` | 3 | v0.1 |
| 34 | Liverty | `fase2/34-liverty.md` | `liverty` | 3 | v0.1 |
| 35 | Testoplus | `fase2/35-testoplus.md` | `testo-plus` | 3 | v0.1 |
| 36 | Renaissance | `fase2/36-renaissance.md` | `renaissance` | 3 | v0.1 |
| 37 | Vitamina D | `fase2/37-vitamina-d.md` | `vitamina-d` | 3 | v0.1 |

Struttura standard di ogni flow prodotto:
- Email 1 (+1gg, Lorenzo): Istruzioni assunzione specifiche del prodotto
- Email 2 (+5gg, Lorenzo): Aspettative + tempi di risposta del prodotto
- Email 3 (+18gg, Flaminia): Social proof con recensioni verificate + check-in

**Notazione dei tempi.** Klaviyo ragiona con delay incrementali tra step, non con orari assoluti dal trigger. Dove serve montare a mano nel builder, indicare accanto al `T+X` anche il delay dall'email precedente (es. `T+18gg` → `13 days from email 2`), così il numero si copia senza fare la sottrazione.

**Esempio di incastro timing** (cliente nuovo che compra Paleocomplex):

```
T+2h    [06 Stato]   Benvenuto Lorenzo
T+1gg   [08 Paleo]   Istruzioni Paleocomplex
T+5gg   [24 Paleo]      Aspettative multivitaminico
T+12gg  [21 Stato]      Ottimizza abitudini
T+18gg  [24 Paleo]      Social proof Paleocomplex (Flaminia)
T+33gg  [23 Recensione] Anticipo recensione (Flaminia, +32gg dal Fulfilled)
T+35gg  [WooCommerce]   Email automatica ⭐⭐⭐⭐⭐
```

Gap minimo tra invii ≥ 2 giorni. Sequenza alternata Lorenzo/Flaminia. NB: T+33gg dal Placed è una stima — il flow 23 parte da Fulfilled+32gg, quindi il T effettivo varia col tempo di spedizione.

**Esempio cliente ricorrente che compra Elisir per la prima volta** (al suo 3° ordine):

```
T+2h      [22 Stato]      Grazie + costanza Lorenzo
T+1gg     [26 Elisir]     Istruzioni Elisir
T+5gg     [26 Elisir]     Aspettative multivitaminico
T+18gg    [26 Elisir]     Social proof Elisir (Flaminia)
T+33gg    [23 Recensione] Anticipo recensione (Flaminia)
T+35gg    [WooCommerce]   Email automatica ⭐⭐⭐⭐⭐
T+30-90gg [78 Cross-sell] Suggerimento AI Next Best Product (Lorenzo) — alla Best Cross-Sell Date del cliente
```

### FASE 3 — Retention, Winback, Lifecycle (7 flow attivi + 1 sospeso, slot 71-78, buffer 79+)

**Architettura rivista giugno 2026** dopo attivazione trial Klaviyo Marketing Analytics (RFM + Catalog Insights + Predictive). Dettaglio completo, sormonti e filtri di esclusione in **`fase3/00-mappatura-fase3.md`** (documento di riferimento).

| # | Flow | File | Email | Trigger | ML Klaviyo? | Status |
|---|------|------|-------|---------|-------------|--------|
| 71 | First-Order Reorder | `fase3/71-first-order-reorder.md` | 5 (3 rami: ~30gg / ~60gg / VitD) | Fulfilled Order + Lifetime Orders = 1 + split famiglia pack | ❌ timing fisso | v2.2 — scritto |
| 72 | AI Repeat Purchase | `fase3/72-ai-repeat-purchase.md` | 5 (2 Above CLV + 3 Below CLV) | Expected Date of Next Order + split Predicted CLV | ✅ Predictive ×2 | v1.0 — scritto, ATTIVARE dopo 60-90gg dati |
| 73 | RFM Winback | `fase3/73-rfm-winback.md` | 5 (3 High CLV + 2 Standard) | Segmento RFM At Risk/Needs Attention + split Historic CLV | ✅ RFM | v1.0 — scritto |
| 74 | Sunset Lead | `fase3/74-sunset-lead.md` | 2 + suppress | Segmento comportamentale (180gg iscritto, 0 ordini, 0 engagement) | ❌ | v1.0 — scritto |
| 75 | Sunset Cliente Storico | `fase3/75-sunset-cliente-storico.md` | 2 + frequency reduction | Segmento comportamentale (1+ ordini, 180gg inattivo) | ❌ | v1.0 — scritto |
| 76 | Back in Stock | `fase3/76-back-in-stock.md` | 1 | Subscribed to Back In Stock + restock | ❌ event nativo | v1.0 — scritto, richiede widget "Notify me" |
| ~~77~~ | Programma Fedeltà | — | — | (sospeso: plugin loyalty non collegato a Klaviyo) | — | SOSPESO |
| 78 | Cross-Sell Data-Driven | `fase3/78-cross-sell-data-driven.md` | 1 | Best Cross-Sell Date + blocco Next Best Product | ✅ Catalog Insights ×2 | v1.1 — scritto, richiede Marketing Analytics |

**Punti chiave dell'architettura Fase 3:**
- **Sconti solo dove servono** (selective discounting Klaviyo): Flow 72 Below-CLV (10%→15%), Flow 73 (10% o 15% univoco per HCLV alto), Flow 75 (BENTORNATO20 open-ended). MAI sconto in Flow 71 (primo riacquisto), 72 Above-CLV, 76, 78.
- **Flow 78 = unico punto di cross-sell automatico** del sistema (la vecchia email cross-sell del Flow 22 è stata rimossa).
- **Sormonti gestiti con filtri di esclusione**: 72↔73 (gap 30gg), 73↔75 (gap 60gg), 71↔72 (Lifetime Orders + esclusione 365gg), 72↔78 (esclusione reciproca). Tabella completa in `fase3/00-mappatura-fase3.md`.
- **Smart Sending OFF su tutti i flow Fase 3** (email importanti, non broadcast).

### FUTURO — Da attivare quando pronti

| # | Flow | Email | Prerequisito | Status |
|---|------|-------|-------------|--------|
| 50 | Compleanno | 1 | Sistema raccolta data di nascita (campo checkout o form) | Parcheggiato |

## Conteggio totale

| Fase | Flow | Email |
|------|------|-------|
| Fase 1 | 6 flow | 35 email |
| Fase 2 stato cliente + recensione | 3 flow (21, 22, 23) | 4 email |
| Fase 2 prodotto | 14 flow (24-37) | 42 email |
| Fase 3 | 7 flow attivi (71-76, 78) + 1 sospeso (77) | 19 email + 2 azioni |
| **Totale** | **30 flow attivi** | **~100 email** |

**Nota volume per cliente medio**: il numero email totali è alto, ma ogni cliente riceve solo una frazione (dipende dai prodotti acquistati). Un nuovo cliente che compra 1 prodotto riceve circa 6 email nel primo mese (3 stato + 3 prodotto). Un cliente con 3 prodotti diversi nello stesso ordine ne riceve circa 12 in 32 giorni (3 stato + 3×3 prodotto), distribuiti senza sovrapposizioni.

## Matrice cross-sell

(Riferimento per il flow 22 Cliente Ricorrente)

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

Nel flow 22, ogni suggerimento è condizionato su "il cliente non ha già acquistato quel prodotto" (logica esclusione "già posseduto").

## Note tecniche Klaviyo

### Funzionalità da sfruttare
- **Dynamic table blocks:** prodotti nel carrello abbandonato (flow 1)
- **Show/Hide blocks:** sotto-blocchi condizionali nel flow 22 cross-sell
- **Trigger SKU-based:** per i 14 flow prodotto (24-37) — `Item SKU equals X` + `zero times before`
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
- [ ] Testare logica trigger "Has not placed order with SKU X over all time before" su Klaviyo per flow prodotto 24-37

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
| **Lorenzo Zarone** | Welcome (tutte), Authority (tutte), Conversione, Flow prodotto 24-37 (email 1 e 2), Flow 21 (entrambe), Flow 22 (grazie), Flow 71 email 2 + VitD, Flow 72 Above-CLV (tutte) + Below-CLV email 3, Flow 73 (High CLV email 1-2, Standard email 2), Flow 74 (entrambe), Flow 75 email 1, Flow 78 | Un forte abbraccio · Lorenzo Zarone · Fondatore di Paleocomplex |
| **Flaminia (Customer Care)** | Tutto il resto: Carrello abbandonato, Browse abandonment, Flow prodotto 24-37 email 3 social proof, Flow 23 Recensione Brand, Flow 71 email 1, Flow 72 Below-CLV email 1-2, Flow 73 (High CLV email 3, Standard email 1), Flow 75 email 2, Back in stock | Flaminia · Customer Care Paleocomplex |

**Nota**: rimosso il mittente "Team Paleocomplex" — sterile e impersonale. Flaminia diventa il volto unico del customer care per tutte le comunicazioni non-Lorenzo. Lorenzo resta la voce del fondatore per le comunicazioni educative/brand. Due voci sole, complementari e riconoscibili.

### Open loop (cliffhanger) tra email

Tecnica: chiusura email N con promessa specifica e curiosa sulla N+1.

| Flow | Open loop |
|------|-----------|
| Authority Flow (4) | SÌ — tutte le email (6/6) |
| Welcome Kit Benessere (2) | SÌ — solo 2-3 punti chiave |
| Welcome Unghie/Capelli (3) | SÌ — solo 2-3 punti chiave |
| Conversione (6) | SÌ — 3-4 punti strategici |
| Flow prodotto 24-37 | SÌ — open loop interno (email 1→2 e 2→3) |
| Flow stato cliente 21-22 | NO (eccetto email 1 → "Flaminia ti scriverà tra qualche giorno") |
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
5. Per i flow prodotto: il template è il flow 24 (Paleocomplex), validato con Andrea. Variazioni nei singoli flow per dosaggi/recensioni/aspettative specifiche del prodotto
6. Per prerequisiti tecnici Klaviyo: vedi checklist nella sezione "Note tecniche Klaviyo"

## Changelog

- **v6.1 (2026-07-13)**: aggiunto flow 7 Welcome Lead Magnet D3+K2 (`fase1/07-welcome-d3-k2.md`), welcome snello a 2 email (delivery report + benvenuto → bridge report/prodotto + urgency) da lead magnet report "D3 + K2: Smontiamo il Mito delle Assunzioni Separate", ingresso da landing social. Confluisce nell'Authority (flow 4) per i non convertiti: aggiungere come terza sorgente di trigger dell'Authority.
- **v6.0 (2026-06-18)**: architettura Fase 3 definitiva basata su Klaviyo Marketing Analytics (trial 30gg attivo). Eliminati gli 11 flow retention/winback pianificati (6 retention per prodotto + 2 winback + back in stock + sunset + fedeltà) e sostituiti con 7 flow: 71 First-Order Reorder (timing fisso 3 rami famiglia pack), 72 AI Repeat Purchase (Expected Date of Next Order + split Predicted CLV), 73 RFM Winback (segmento At Risk/Needs Attention + split Historic CLV), 74 Sunset Lead (suppress), 75 Sunset Cliente Storico (frequency reduction, no suppress), 76 Back in Stock, 78 Cross-Sell Data-Driven (Best Cross-Sell Date + Next Best Product). Flow 77 Fedeltà sospeso (plugin non collegato). **Flow 22 Cliente Ricorrente ridotto a semplice grazie (v2.0)**: cross-sell rimosso e centralizzato nel Flow 78. Documento di riferimento sormonti/segmenti: `fase3/00-mappatura-fase3.md`.
- v5.0 (2026-06-11): rinumerazione definitiva a decine (Fase 1: 01-20, Fase 2: 21-70, Fase 3: 71+). Nuovo flow 23 Recensione Brand su Fulfilled+32gg. Fix timing cross-flow su dati fulfillment reali.
- **v3.0 (2026-05-13)**: refactor architetturale Fase 2 maggiore. Il flow monolitico "Post Purchase New Customer" con 14 blocchi condizionali è stato smontato e ricomposto in 16 flow paralleli: 2 stato cliente (21 Primo Cliente, 22 Cliente Ricorrente) + 14 flow prodotto (24-37, uno per SKU). Motivazione: il vecchio schema non garantiva educazione specifica al cliente ricorrente che acquistava un prodotto mai provato (es. cliente compra Youth, poi Elisir: con vecchio schema, niente istruzioni Elisir). Nuovo schema risolve il buco architetturale, manutenzione più pulita, trigger SKU-based (zero ambiguità). Cross-sell flow 22: aggiunta logica esclusione "già posseduto" (Andrea, maggio 2026). Numerazione Fase 3 shiftata a 71-81.
- v2.2 (2026-04-22): Authority v3.0 con email 2 VNR vs apporto massimo legale.
- v2.1 (2026-04-16): Feedback Lorenzo Fase 1 review (correzioni VNR, blog "centinaia", disclaimer recensioni).
- v2.0 (2026-04): Fase 1 completata e in review Lorenzo.
- v1.0 (2026-03): Prima versione del piano master.
