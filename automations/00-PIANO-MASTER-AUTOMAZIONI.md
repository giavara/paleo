**Versione:** 2.0
**Ultimo aggiornamento:** 2026-04-07
**Status:** Architettura confermata — in fase di scrittura email

# Piano Master — Automazioni Email Klaviyo

## Obiettivo

Ricostruire da zero tutte le automazioni email di Paleocomplex per la migrazione da ActiveCampaign a Klaviyo. Strategia basata su:
- Dati performance delle vecchie 218 email (revenue €195K totale)
- Flow post-purchase personalizzati per prodotto acquistato
- Riduzione drastica del volume (da 218 a ~55 email + blocchi dinamici) con focus su ROI per invio
- Best practice Klaviyo (documentazione ufficiale + academy)

## Decisioni prese

1. **Authority + Post Purchase non si sovrappongono.** Chi compra entra SOLO nel Post Purchase. L'Authority Flow si sospende. Chi NON compra dopo il welcome entra nell'Authority completo.
2. **Acquisti multipli: contenuto dinamico, non flow separati.** Il Post Purchase e' un unico flow con blocchi dinamici Show/Hide per prodotto. Se uno compra Elisir + Jeunesse, vede le istruzioni di entrambi nella stessa email.
3. **Optin marketing nel post-purchase:** P.S. soft in email 2 e 3 solo per chi non ha optin. Non prioritario (99.9% ha gia' autorizzato).
4. **Email educative vecchie (157 email Automazione Italia + Finale):** NON migrate come automazione. Le migliori 15-20 diventano contenuto per newsletter settimanale (campaign). Tenute a lato per riuso.
5. **Cross-sell sport trasversale:** Hurricane e Armageddon proposti come blocco fisso in tutte le email di cross-sell ("Ti alleni? Scopri la linea sport").
6. **Retention/Cross-sell: flow separati per prodotto**, non un unico flow con condizionali. Ogni flow ha trigger, timing e contenuto specifico per prodotto. **Trigger: Fulfilled Order** (non Placed Order) — il cliente deve aver ricevuto il prodotto.
7. **Carrello abbandonato: conditional split nuovo vs. esistente** nella email 2. Nuovo cliente: risposta obiezioni + eventuale incentivo. Cliente esistente: tono diverso, no sconto. NO split per valore carrello (non serve per il nostro caso). Codici sconto univoci (non generici). Re-ingresso limitato a 1 volta ogni 7 giorni. Disabilitare email carrello nativo WooCommerce.
8. **Welcome series: email 4 a +7gg per chi non ha acquistato.** Dato Klaviyo: la maggior parte degli acquisti avviene entro 10 giorni. Email 4 = "ultima occasione" con tono lettera personale Lorenzo + reminder sconto BENVENUTO.
9. **Welcome da lead magnet specifico: contenuto e prodotti coerenti con il tema del lead magnet** (es. Welcome Kit Benessere = report anti-aging 40+ → prodotti citati: Elisir, Revolution, Essentiel, NO Paleocomplex base). **L'Authority parte DOPO il completamento della welcome** (sequenziale, NON in parallelo) per evitare sovrapposizioni e bombardamento. La storia di Lorenzo è nel welcome, l'Authority non la ripete.
10. **Win-back: doppio approccio.** (A) Flow basato su timing fisso: +85gg dall'ultimo ordine (ciclo medio Paleocomplex = 76gg). (B) Segmento Klaviyo Predictive Analytics per intercettare chi sta performando sotto la media indipendentemente dal timing. I due approcci sono complementari.
11. **Browse Abandonment: filtro prodotto gia' acquistato.** Se l'utente ha gia' comprato quel prodotto, il flow NON parte. L'email arriva solo a chi sta esplorando un prodotto che non ha ancora acquistato.
12. **Compleanno: parcheggiato.** Lo attiviamo appena abbiamo un sistema che raccoglie la data di nascita (campo nel checkout o form dedicato).

## Architettura dei flow

### FASE 1 — Flow critici per revenue

| # | Flow | File | Email | Trigger | Status |
|---|------|------|-------|---------|--------|
| 1 | Carrello abbandonato | `fase1/01-carrello-abbandonato.md` | 3 | Checkout started + non completato | Da scrivere |
| 2 | Welcome Kit Benessere | `fase1/02-welcome-kit-benessere.md` | 5 | Optin da popup/homepage/blog/landing social | In review |
| 3 | Welcome Unghie/Capelli | `fase1/03-welcome-unghie-capelli.md` | 6 | Optin da lead magnet unghie/capelli | In review |
| 4 | Authority Flow | `fase1/04-authority-flow.md` | 5 | DOPO completamento welcome (sequenziale) + non ha comprato | In review |
| 5 | Browse Abandonment | `fase1/05-browse-abandonment.md` | 2 (email 2 in draft) | Viewed Product + non ha comprato quel prodotto + non in altri flow + max 1 volta ogni 30gg | In review |
| 6 | Conversione | `fase1/06-conversione.md` | 10 | DOPO Authority + non ha comprato. 32 giorni. Sconto PRIMOPASSO nell'ultima email | In review |

### FASE 2 — Flow post-acquisto

| # | Flow | File | Email | Trigger | Status |
|---|------|------|-------|---------|--------|
| 6 | Post Purchase New Customer | `fase2/06-post-purchase-new.md` | 6 + blocchi dinamici | Primo ordine completato (Placed Order, has ordered = 1) | Da scrivere |
| 7 | Post Purchase Returning | `fase2/07-post-purchase-returning.md` | 2 | Ordine completato da cliente esistente (has ordered >= 2) | Da scrivere |

**Blocchi dinamici Post Purchase New (email 2, 3, 4, 5):**

| Categoria | File blocco | Prodotti coperti | Dettaglio |
|-----------|-------------|------------------|-----------|
| Multivitaminici | `fase2/blocchi/multi-elisir.md` | Elisir, Elisir Basic | Completo |
| Multivitaminici | `fase2/blocchi/multi-paleo.md` | Paleocomplex, Revolution | Completo |
| Collagene | `fase2/blocchi/collagene-youth.md` | Youth | Completo |
| Collagene | `fase2/blocchi/collagene-jeunesse.md` | Jeunesse | Completo |
| Generico | `fase2/blocchi/generico-altri.md` | Artosan, Liverty, Testoplus, Renaissance, Hurricane, Armageddon, Vitamina D | Blocco unico adattabile |

### FASE 3 — Flow di retention e lifecycle

| # | Flow | File | Email | Trigger | Timing cross-sell | Timing riacquisto | Status |
|---|------|------|-------|---------|-------------------|-------------------|--------|
| 8 | Retention Elisir/EB | `fase3/08-retention-elisir.md` | 3 | Fulfilled Order con Elisir o EB | gg 28 | gg 35 | Da scrivere |
| 9 | Retention Paleo/Rev | `fase3/09-retention-paleo.md` | 3 | Fulfilled Order con Paleo o Rev | gg 20 | gg 25 | Da scrivere |
| 10 | Retention Youth | `fase3/10-retention-youth.md` | 3 | Fulfilled Order con Youth | gg 20 | gg 25 | Da scrivere |
| 11 | Retention Jeunesse | `fase3/11-retention-jeunesse.md` | 3 | Fulfilled Order con Jeunesse | gg 35 | gg 45 | Da scrivere |
| 12 | Retention Sport | `fase3/12-retention-sport.md` | 3 | Fulfilled Order con Hurricane o Armageddon | gg 20 | gg 25 | Da scrivere |
| 13 | Retention Generico | `fase3/13-retention-generico.md` | 3 | Fulfilled Order con Artosan/Liverty/Testoplus/Renaissance/VitD | gg 45 | gg 55 | Da scrivere |
| 14 | Win-back (timing) | `fase3/14-winback.md` | 4 | Placed Order + nessun ordine da 85+ giorni | — | — | Da scrivere |
| 15 | Win-back (predictive) | `fase3/15-winback-predictive.md` | 2 | Klaviyo Predictive Analytics: churn risk alto | — | — | Da scrivere |
| 16 | Back in Stock | `fase3/16-back-in-stock.md` | 1 | Subscribed to Back In Stock + prodotto torna disponibile | — | — | Da scrivere |
| 17 | Sunset (pulizia lista) | `fase3/17-sunset.md` | 2 + azione soppressione | Segmento: iscritto 180+ gg, 0 aperture, 0 click, 0 ordini, 5+ email ricevute | — | — | Da scrivere |
| 18 | Programma Fedelta' | `fase3/18-programma-fedelta.md` | 4 | Raggiungimento livello Club/Silver/Gold/Elite | — | — | Da scrivere |

### FUTURO — Da attivare quando pronti

| # | Flow | Email | Prerequisito | Status |
|---|------|-------|-------------|--------|
| 19 | Compleanno | 1 | Sistema raccolta data di nascita (campo checkout o form) | Parcheggiato |

## Dettaglio flow con note tecniche Klaviyo

### Flow 1: Carrello Abbandonato

**Trigger:** Started Checkout
**Filtri:**
- Placed Order zero times since starting this flow
- Re-ingresso: max 1 volta ogni 7 giorni
- Disabilitare email carrello nativo WooCommerce per evitare duplicati

| # | Timing | Contenuto | Note Klaviyo |
|---|--------|-----------|-------------|
| 1 | +4h | Reminder soft + dynamic table block con prodotti nel carrello | Nessuno sconto. Tono rassicurante Lorenzo |
| 2 | +16h | **SPLIT nuovo vs. esistente** (Has Placed Order = 0 over all time). Nuovo: risposta obiezioni (contrassegno, rate, qualita'). Esistente: "conosci gia' la qualita'" + CTA diretto | Codici sconto univoci (se usati), solo per nuovi |
| 3 | +2gg | Social proof (recensioni reali) + ultima chance. Per nuovi: eventuale incentivo | Dynamic table block |

### Flow 2-3: Welcome Kit Benessere / Welcome Unghie-Capelli

**Trigger:** Added to List (lista specifica per optin source)
**Filtri:** non è già in questo flow
**Timing:** 5 email in 10 giorni (la maggior parte degli acquisti avviene entro 10 giorni)

**Welcome Kit Benessere (flow 2):**

| # | Timing | Contenuto |
|---|--------|-----------|
| 1 | Immediata | Delivery report 7 strategie + codice BENVENUTO €10 |
| 2 | +2gg | Perché un multivitaminico completo batte 10 separati |
| 3 | +4gg | Chi è Lorenzo + perché ha creato Paleocomplex |
| 4 | +7gg | Il prodotto giusto per te (Elisir/Revolution/Essentiel) + social proof reali |
| 5 | +10gg | **SOLO se non ha acquistato.** Ultima occasione BENVENUTO |

Prodotti citati coerenti col tema anti-aging/40+: Elisir, Revolution, Essentiel. NO Paleocomplex base.

**Welcome Unghie/Capelli (flow 3):**

| # | Timing | Contenuto |
|---|--------|-----------|
| 1 | Immediata | Delivery report unghie/capelli + codice BENVENUTO €10 |
| 2 | +2gg | Approfondimento: ruolo collagene per capelli/unghie/pelle |
| 3 | +4gg | Chi è Lorenzo + brand story (angolo beauty/salute) |
| 4 | +7gg | Il prodotto giusto per te (Youth/Jeunesse) + social proof |
| 5 | +10gg | **SOLO se non ha acquistato.** Ultima occasione BENVENUTO |

Prodotti citati coerenti col tema beauty: Youth, Jeunesse, multivitaminico come base.

**Uscita dal flow:**
- Se acquista durante la welcome → esce e entra in Post Purchase (flow 6)
- Se completa senza acquistare → entra in Authority Flow (flow 4)

**L'Authority parte DOPO il welcome (sequenziale, NON in parallelo).** La storia di Lorenzo è nel welcome (email 3), l'Authority non la ripete.

### Flow 4: Authority Flow

**Trigger:** Completamento welcome series + non ha acquistato
**Nota:** Parte DOPO il welcome (sequenziale). Non ripete la brand story di Lorenzo (già coperta nel welcome email 3). Focus su educazione prodotto/ingredienti.

| # | Timing | Contenuto |
|---|--------|-----------|
| 1 | +1gg dal completamento welcome | La filosofia Paleocomplex: "meno integratori, meglio dosati" |
| 2 | +3gg | I 3 errori che tutti fanno con gli integratori (dosaggi simbolici, forme non attive, combo sbagliate) |
| 3 | +5gg | Cosa rende unico un multivitaminico Paleo (forme attive, dosaggi reali, trasparenza etichetta) |
| 4 | +8gg | Social proof: 3 recensioni reali + risultati concreti |
| 5 | +11gg | "Quale integratore fa per te?" — mini-guida alla scelta con CTA |

### Flow 5: Browse Abandonment

**Trigger:** Viewed Product
**Filtri:**
- Placed Order zero times since starting this flow
- Started Checkout zero times since starting this flow
- Added to Cart zero times since starting this flow
- **Non ha gia' acquistato quel prodotto specifico** (Has Placed Order where Item = viewed product zero times over all time)
- Non e' stato in questo flow negli ultimi 30 giorni

| # | Timing | Contenuto |
|---|--------|-----------|
| 1 | +2h | "Hai dato un'occhiata a [prodotto]" — breve, informativo, 1 beneficio chiave. Tono suggestivo, NON aggressivo. Nessuno sconto |
| 2 | +1gg | Social proof specifico per quel prodotto (opzionale, valutare performance email 1 prima di attivare) |

### Flow 6: Post Purchase New Customer

**Trigger:** Placed Order (Has Placed Order = 1 over all time)
**Effetto:** Authority Flow si sospende per questo contatto

| # | Timing | Contenuto | Blocchi dinamici |
|---|--------|-----------|-----------------|
| 1 | +2h | Benvenuto + conferma + "hai fatto la scelta giusta" + info spedizione | Uguale per tutti |
| 2 | +1gg | Istruzioni assunzione specifiche per prodotto/i acquistato/i | Blocchi per: Elisir, Paleo, Youth, Jeunesse, generico |
| 3 | +7gg | Ottimizza risultati: abitudini complementari + combinazioni suggerite | Blocco combo dinamico |
| 4 | +21gg | Set aspettative: cosa aspettarti a questo punto del percorso | Blocco timeline dinamico per prodotto |
| 5 | +25gg | Social proof: recensioni specifiche per prodotto acquistato | Blocchi recensioni dinamici |
| 6 | +29gg | Richiesta recensione | Uguale per tutti |

### Flow 7: Post Purchase Returning

**Trigger:** Placed Order (Has Placed Order >= 2 over all time)

| # | Timing | Contenuto |
|---|--------|-----------|
| 1 | +2h | Grazie + conferma + "ottima scelta continuare" (validazione riacquisto) |
| 2 | +3gg | Cross-sell personalizzato basato su acquisto (vedi matrice cross-sell) + blocco sport |

### Flow 8-13: Retention (6 flow separati per prodotto)

**Trigger:** Fulfilled Order (contiene prodotto specifico)
**Filtro:** Non ha riacquistato lo stesso prodotto dall'inizio del flow

Struttura identica per tutti, cambiano timing e contenuto:

| # | Email | Contenuto |
|---|-------|-----------|
| 1 | Cross-sell day | "Hai provato [X], potresti essere interessato a [Y]" + perche' si combinano + blocco sport |
| 2 | Riacquisto day | "Il tuo [X] sta per finire" + reminder benefici + CTA riacquisto |
| 3 | +5gg se non riacquista | Ultimo reminder + eventuale incentivo soft |

**Timing per flow:**

| Flow | Prodotto | Cross-sell | Riacquisto | Reminder |
|------|----------|-----------|------------|---------|
| 8 | Elisir/EB | gg 28 | gg 35 | gg 40 |
| 9 | Paleo/Rev | gg 20 | gg 25 | gg 30 |
| 10 | Youth | gg 20 | gg 25 | gg 30 |
| 11 | Jeunesse | gg 35 | gg 45 | gg 50 |
| 12 | Sport | gg 20 | gg 25 | gg 30 |
| 13 | Generico | gg 45 | gg 55 | gg 60 |

### Flow 14: Win-back (timing fisso)

**Trigger:** Placed Order
**Filtro:** Placed Order zero times in last 85 days since starting this flow
**Delay iniziale:** 85 giorni (ciclo medio acquisto Paleocomplex = 76 giorni, margine +12%)

**Conditional split:** Ha aperto email almeno 1 volta negli ultimi 60 giorni

**Percorso engaged (apre email):**

| # | Timing | Contenuto |
|---|--------|-----------|
| 1 | +85gg | "Ci manchi" — reminder benefici + cosa succede quando si smette |
| 2 | +5gg | Offerta personalizzata (codice univoco) |

**Percorso disengaged (non apre email):**

| # | Timing | Contenuto |
|---|--------|-----------|
| 1 | +85gg | "Ci manchi" — reminder benefici + cosa succede quando si smette |
| 2 | +5gg | Social proof fresh + novita' prodotti |
| 3 | +10gg | Offerta personalizzata (codice univoco) |
| 4 | +20gg | Ultima email — "rispettiamo la tua scelta" + link per gestire preferenze |

### Flow 15: Win-back (Klaviyo Predictive)

**Trigger:** Segmento Klaviyo con Churn Risk = High (>66%)
**Nota:** Complementare al flow 14. Questo intercetta clienti a rischio PRIMA del timing fisso di 85 giorni, grazie alla predizione Klaviyo. Richiede almeno 500 clienti con ordini e 180 giorni di storico.

| # | Timing | Contenuto |
|---|--------|-----------|
| 1 | Immediata (al cambio di segmento) | Email personalizzata basata su ultimo acquisto + "torna a prenderti cura di te" |
| 2 | +7gg | Incentivo se non ha riacquistato |

**Filtro:** Escludi chi e' gia' nel flow 14 (win-back timing)

### Flow 16: Back in Stock

**Trigger:** Subscribed to Back In Stock + prodotto torna disponibile
**Smart Sending:** DISATTIVATO (tutti devono ricevere)
**Priorita' per:** Youth e Jeunesse (stock-out frequenti)

| # | Timing | Contenuto |
|---|--------|-----------|
| 1 | Automatica al restock | "[Prodotto] e' tornato disponibile — ma le scorte sono limitate" + CTA diretto all'acquisto |

**Prerequisito tecnico:** Aggiungere bottone "Avvisami quando torna" sulle pagine prodotto esaurite. Klaviyo lo gestisce nativamente con WooCommerce.

### Flow 17: Sunset (pulizia lista)

**Trigger:** Ingresso in segmento "Inattivi da sopprimere"
**Definizione segmento (best practice Klaviyo):**
- Puo' ricevere email marketing
- Creato almeno 180 giorni fa
- Ha ricevuto almeno 5 email nelle ultime 72 settimane
- 0 aperture email totali
- 0 click email totali
- 0 visite al sito
- 0 visualizzazioni prodotto
- 0 ordini effettuati

| # | Timing | Contenuto |
|---|--------|-----------|
| 1 | Immediata | "Ci manchi — vuoi continuare a ricevere i nostri contenuti?" — CTA per confermare interesse. Link gestione preferenze ben visibile |
| 2 | +3gg (se non apre/clicca) | "Ultima email — se non ci fai sapere, smetteremo di scriverti" — CTA per restare + link cancellazione |
| Azione | +3gg dopo email 2 | Aggiornamento proprieta' profilo → tag "Disimpegnato" → soppressione da invii futuri |

**Nota:** La soppressione va fatta manualmente prima di ogni campagna (creare segmento "Unengaged = true" e sopprimere). Automazione completa richiede webhook + API.

**DECISIONE APERTA:** Valutare se escludere dal sunset chi ha comprato almeno 1 volta. Esempio: un cliente con 2 ordini che non interagisce da 180+ giorni — lo sopprimiamo o lo teniamo? Opzioni:
- (A) Sopprimere tutti gli inattivi indipendentemente dagli acquisti (protegge deliverability al massimo)
- (B) Escludere chi ha comprato almeno 1 volta e mandarli invece nel win-back (non perdiamo clienti reali)
- (C) Split nel flow: chi ha comprato riceve un percorso diverso (es. "ci manchi, torna a trovarci" + incentivo forte) prima della soppressione
Da valutare prima di attivare il flow.

**Impatto:** Lista piu' pulita = open rate piu' alti su tutti i flow = migliore deliverability = piu' revenue.

### Flow 18: Programma Fedelta'

**Trigger:** Raggiungimento nuovo livello (proprieta' profilo aggiornata)

| Livello | Email | Contenuto |
|---------|-------|-----------|
| Club (500pt) | 1 | Congratulazioni + 5% sbloccato + prossimo traguardo Silver |
| Silver (1000pt) | 1 | 10% sbloccato + vantaggi + traguardo Gold |
| Gold (2000pt) | 1 | 15% sbloccato + "sei tra i nostri migliori clienti" |
| Elite (4000pt) | 1 | 20% + spedizione gratuita + trattamento VIP |

## Conteggio email totale

| Fase | Flow | Email |
|------|------|-------|
| Fase 1 | 6 flow (carrello, 2 welcome, authority, browse, conversione) | 34 email |
| Fase 2 | 2 flow + 5 blocchi dinamici | 8 email + 5 blocchi |
| Fase 3 | 11 flow (6 retention, 2 winback, back in stock, sunset, fedelta') | 29 email + 1 azione |
| **Totale** | **19 flow** | **~71 email + 5 blocchi dinamici** |

## Matrice cross-sell

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

## Note tecniche Klaviyo

### Funzionalita' da sfruttare
- **Dynamic table blocks:** prodotti nel carrello abbandonato (flow 1)
- **Show/Hide blocks:** contenuto condizionale per prodotto nel post-purchase (flow 6)
- **Codici sconto univoci:** per carrello e win-back (impediscono condivisione)
- **Smart Sending:** attivo su tutti i flow TRANNE Back in Stock (flow 16)
- **Predictive Analytics:** churn risk per win-back predictive (flow 15), expected next order date per ottimizzare retention
- **A/B test nativi:** testare subject line su ogni flow, UNA variabile alla volta, minimo 500 destinatari per variante
- **Back in Stock button:** widget nativo per WooCommerce sulle pagine prodotto esaurite
- **Product feeds:** raccomandazioni automatiche nei cross-sell

### Metriche da monitorare per flow
- **Click Rate** (metrica primaria — non influenzata da Apple Mail Privacy)
- Open Rate (secondaria, gonfiata da MPP)
- Conversion Rate (placed orders / recipients)
- Revenue per Recipient
- Unsubscribe Rate (alert se supera 0.5%)

### Prerequisiti tecnici
- [ ] Disabilitare email carrello abbandonato nativo WooCommerce
- [ ] Configurare widget Back in Stock sulle pagine prodotto
- [ ] Verificare piano Klaviyo per accesso a Predictive Analytics (richiede 500+ clienti, 180gg storico)
- [ ] Creare segmento Sunset con i criteri indicati
- [ ] Configurare proprieta' profilo "Unengaged" per la soppressione

## Regole di scrittura email

Riferimento: `context/email-rules.md`

Punti chiave per le automazioni:
- Tono Lorenzo: diretto, schietto, scientifico ma accessibile
- Claims prudenti: "supporta", "aiuta", "può contribuire"
- No emoji, no elenchi puntati nel corpo, no trattini lunghi
- Apertura "Ciao [NOME]" SENZA virgola (placeholder Klaviyo per il nome del contatto, se fallisce resta "Ciao" pulito) — a capo con maiuscola — chiusura con firma variabile per mittente (vedi tabella sotto)
- Ogni email: 3 varianti oggetto A/B + 3 varianti preview text
- Grassetti strategici, frasi brevi, paragrafi corti (mobile-first)
- MAI inventare dati, dosaggi, ingredienti — verificare sempre su schede prodotto e etichette
- Usare sempre accenti reali (è, à, ò, ù, é) — MAI apostrofo al posto dell'accento
- **Linguaggio gender-neutral:** evitare "Benvenuto/a". Usare forme neutre naturali ("Da oggi fai parte di...", "Ti diamo il benvenuto nel..."). Il codice sconto BENVENUTO e il sostantivo "benvenuto" restano invariati. Per il flow Unghie/Capelli la grafica sarà stilizzata al femminile, ma il copy resta neutro

### Mittenti per tipo di flow

| Mittente | Flow | Firma |
|----------|------|-------|
| **Lorenzo Zarone** | Welcome (tutte), Authority (tutte), Post Purchase educative (istruzioni, ottimizza, aspettative), Win-back, Email "ultima occasione" | Un forte abbraccio · Lorenzo Zarone · Fondatore di Paleocomplex |
| **Team Paleocomplex** | Carrello abbandonato, Browse abandonment, Back in stock, Programma fedeltà, Sunset, Post Purchase returning (cross-sell) | Team Paleocomplex |
| **[Nome CS reale]** (se disponibile, altrimenti Team) | Richiesta recensione | [Nome] · Team Paleocomplex |

### Open loop (cliffhanger) tra email

Tecnica: chiusura email N con promessa specifica e curiosa sulla N+1, apertura email N+1 con richiamo che chiude il loop.

**Obiettivi:**
- Aumentare l'open rate progressivo della sequenza
- Allenare il lettore a riconoscere e aprire il mittente Lorenzo
- Creare continuità narrativa tra le email

**Regola:** solo nei flow educativi/nurturing lunghi e solo dove c'è un contenuto forte da promettere. **Mai forzato in ogni email.**

| Flow | Open loop |
|------|-----------|
| Authority Flow (4) | SÌ — tutte le email (5/5), il flow più editoriale |
| Welcome Kit Benessere (2) | SÌ — solo 2-3 punti chiave |
| Welcome Unghie/Capelli (3) | SÌ — solo 2-3 punti chiave |
| Conversione (6) | SÌ — 3-4 punti strategici (cambio angolo, contenuti forti) |
| Carrello Abbandonato | NO — transazionale |
| Browse Abandonment | NO — touchpoint freddo |
| Post Purchase | NO (per ora) — valutare nei flow lunghi |
| Retention | NO |
| Win-back | NO |
| Back in Stock, Sunset, Fedeltà | NO — operativi |

## Fonti dati per la scrittura

- Schede prodotto: `context/products/[nome]-scheda-prodotto.md`
- Mappa scelta integratori: `context/products/mappa-scelta-integratori.md`
- FAQ ufficiali (dosaggi, combinazioni): `context/faq-sito.md`
- Etichette originali: `context/labels/`
- Recensioni reali: `context/2026 03 31 paleocoplex export-reviews.csv`
- Dati performance vecchie email: `input/paleo mappatura/`
- Esempi flow SP (riferimento strutturale): `input/paleo mappatura/esempi flow sp/`
- Analisi ex clienti (obiezioni per win-back): `context/analysis/analisi sondaggio ex clienti.md`

## Come usare questo documento

1. Prima di scrivere qualsiasi email, consultare questo piano per capire dove si inserisce
2. Ogni flow ha il suo file dedicato nella sottocartella della fase
3. Quando un flow e' completato, aggiornare lo Status nella tabella sopra
4. Se cambia l'architettura (aggiunta flow, modifica timing, nuova decisione) aggiornare QUESTO documento
5. Per trovare un'email specifica: flow file → numero email → contenuto completo
6. Per prerequisiti tecnici Klaviyo: vedi checklist nella sezione "Note tecniche Klaviyo"
