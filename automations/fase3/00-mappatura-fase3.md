**Versione:** 2.0
**Ultimo aggiornamento:** 2026-07-14

# Mappatura Fase 3 — Retention, Winback, Lifecycle

Documento di riferimento per l'architettura completa Fase 3 di Paleocomplex. Include: tabella flow con trigger, uso di Machine Learning / Predictive Analytics Klaviyo, sequenza logica cliente attraverso i flow, sormonti tra flow e come li risolviamo, cosa Klaviyo calcola in automatico vs cosa impostiamo noi.

## Tabella architetturale Fase 3

| # | Flow | Trigger tecnico Klaviyo | Machine Learning? | Cosa fa | Priorità |
|---|------|-------------------------|-------------------|---------|----------|
| **71** | First-Order Reorder | `Placed Order` + filter `Customer's Lifetime Number of Orders = 1` + conditional split famiglia SKU | ❌ NO — timing fisso per famiglia pack | Reorder primo cliente (rete di sicurezza pre-Predictive) | **ALTA** |
| **72** | AI Repeat Purchase | Date property trigger: `Expected Date of Next Order` | ✅ **SÌ — Predictive Analytics** calcola ENO personalizzata per cliente | Reorder ricorrente al momento personalizzato | **ALTA** |
| | └ Conditional Split | `Predicted CLV ≥ 150€` (media reale calcolata 22/7 su 2.895 clienti) | ✅ **SÌ — Predictive Analytics** calcola CLV atteso 365gg | Above/Below split per modulare il copy (nessuno sconto in questo flow) | |
| **73** | RFM Winback | Ingresso segmento `Current RFM group ∈ [At Risk, Needs Attention]` | ✅ **SÌ — RFM Automation** classifica i clienti in 6 gruppi ogni notte | Riattivazione clienti a rischio churn | **MEDIA** |
| | └ Conditional Split | `Historic CLV > 450€` (mediana reale calcolata 22/7) | ❌ NO — dato storico | Distinguere top spender persi da clienti medi (split 50/50) | |
| **74** | Sunset Lead | Ingresso segmento comportamentale (`Subscribed > 180gg` + `Placed Order = 0` + `Last Open > 90gg` + `Last Click > 90gg`) | ❌ NO — segmento comportamentale semplice | Igiene lista: sopprimere iscritti mai-clienti mai-attivi | BASSA |
| **75** | Sunset Cliente Storico | Ingresso segmento (`Placed Order ≥ 1` + `Last Placed > 180gg` + `Last Open > 180gg`) | ❌ NO — segmento comportamentale | Nurturing soft per cliente vero che è scomparso (no suppress hard) | BASSA |
| **76** | Back in Stock | `Subscribed to Back in Stock` + prodotto restock | ❌ NO — trigger event-based nativo Klaviyo/WooCommerce | Notifica quando prodotto torna disponibile | BASSA |
| **78** | Cross-Sell Data-Driven | Date property trigger: `Best Cross-Sell Date` | ✅ **SÌ — Catalog Insights** (Marketing Analytics avanzato) calcola data ottimale product-level | Cross-sell mirato al momento giusto — **UNICO punto di cross-sell del sistema** | **MEDIA** (dopo trial 30gg) |
| | └ Content dinamico | Blocco `Next Best Product` | ✅ **SÌ — Catalog Insights** suggerisce prodotto ottimale per profilo | Suggerisce automaticamente il prodotto giusto per ogni cliente | |
| ~~77~~ | Programma Fedeltà | (sospeso — plugin loyalty non collegato a Klaviyo) | - | - | - |

**Nota architetturale sul cross-sell (2026-06-18):** con l'introduzione del Flow 78, la vecchia email 2 cross-sell del **Flow 22 Cliente Ricorrente** (Fase 2) è stata rimossa: il 22 è ora un semplice grazie post-acquisto (1 email Lorenzo +2h). Il cross-sell automatico vive SOLO nel Flow 78. Questo elimina alla radice il rischio di suggerimenti duplicati e sposta la scelta di prodotto/timing dall'hard-coding all'AI di Klaviyo.

**Legenda ML/Predictive:**
- ✅ **SÌ**: Klaviyo calcola automaticamente il trigger/valore usando Machine Learning o Analytics avanzato
- ❌ **NO**: trigger/valore comportamentale o event-based, impostabile senza AI

## Strategia sconti del ciclo retention (decisa 2026-07-14)

Principio: **lo sconto cresce con la distanza del cliente, mai con la vicinanza**. Si sconta dove c'è incrementalità vera (cliente che non comprerebbe senza), mai dove l'acquisto avverrebbe comunque.

| Flow | Momento cliente | Sconto | Codice | Tipo |
|------|-----------------|--------|--------|------|
| 71 First-Order Reorder | Primo riacquisto in finestra naturale | **0%** | — | Mai educare il nuovo cliente allo sconto |
| 72 AI Repeat Purchase | Riordino alla data prevista (picco propensione) | **0%** al lancio | — | Opzione test 10€ dopo 60-90gg di dati se conversion Below debole |
| 73 RFM Winback Standard | At Risk, HCLV ≤450€ | **10%** | univoco `RP10-xxx` (14gg) | Primo sconto del ciclo: c'è segnale reale di allontanamento |
| 73 RFM Winback High | At Risk, HCLV >450€ | **15%** solo Email 3 | univoco `WB15-xxx` (14gg) | Prima brand reintroduction, sconto come ultima leva |
| 74 Sunset Lead | Mai cliente, in uscita dalla lista | **20%** Email 2+3 | univoco `SL20-xxx` (14gg) | Baseline ~zero: ogni conversione è guadagno puro. Il click fa anche da test interesse |
| 75 Sunset Cliente Storico | Ex cliente dormiente 180gg | **20%** open-ended | statico `BENTORNATO20` (1 uso/cliente) | Carta finale senza pressione temporale |
| 78 Cross-Sell Data-Driven | Cliente attivo, prova prodotto NUOVO | **10€ fissi** | univoco `NP10-xxx` (14gg) | Incrementalità vera: barriera della prima prova. Vale su tutto il catalogo |

**Codici univoci Klaviyo per WooCommerce**: supporto nativo confermato (help.klaviyo.com/hc/en-us/articles/22168739689627). Coupon master in WooCommerce (usage limit 1+1) + collegamento in Klaviyo Content → Coupons → WooCommerce tab con prefix. Klaviyo genera e assegna i codici per profilo con scadenza relativa alla ricezione.

**Setup scadenza (fatto e verificato, Andrea 2026-07-14)**: tutti i coupon univoci scadono a **15 giorni alle 00:00 (mezzanotte, verificato)** dall'assegnazione → il cliente ha 14 giorni pieni, e il copy dice con precisione "scade a mezzanotte del 14° giorno". Le email successive dello stesso flow citano i giorni residui esatti (73 Standard E2 a +10gg → "scade tra 4 giorni"; 74 E3 a +7gg → "scade tra 7 giorni").

**BENTORNATO20 (fatto)**: creato come coupon statico normale in WooCommerce, 20%, **1 uso per cliente, senza scadenza** — coerente col design open-ended del Flow 75.

✅ Setup coupon completato. Prossimi passi operativi: creazione segmenti Klaviyo (definizioni in questo documento) e montaggio flow: 71 → 73 → 74 → 75 → 76 subito; 72 e 78 montati ma in draft finché Predictive/Catalog Insights non hanno 60-90gg di dati.

## Cosa Klaviyo calcola in automatico vs cosa impostiamo noi

### Klaviyo calcola in automatico (con Marketing Analytics attivo)

1. **Expected Date of Next Order** (per profilo, aggiornato settimanale)
   - Usato in: Flow 72
   - Requisiti: 500+ clienti, 180gg storico, 3+ ordini per cliente
2. **Predicted CLV** (per profilo, aggiornato settimanale)
   - Usato in: Flow 72 (conditional split)
3. **Churn Risk** (per profilo, valore 0-1, esportabile via CSV o attivabile in segment builder via support)
   - Non usato direttamente (proxy: RFM At Risk)
4. **RFM Customer Groups** (per profilo, aggiornato notturno)
   - Assegna ogni profilo a: Champions, Loyal, Recent Customer, Needs Attention, At Risk, Inactive
   - Usato in: Flow 73, Flow 75 (proxy)
5. **Best Cross-Sell Date** (per profilo, aggiornato quotidiano)
   - Usato in: Flow 78 (nuovo)
   - Basato su product-level patterns
6. **Next Best Product** (per profilo, aggiornato a ogni ordine)
   - Usato in: Flow 78 (contenuto dinamico)
7. **Products Bought in Same Cart / Next Order** (dashboard)
   - Usato per: strategie di bundle, insight generali (non trigger di flow)

### Noi impostiamo manualmente

1. **Segmenti comportamentali** (Flow 74 Sunset Lead, Flow 75 Sunset Cliente Storico)
2. **Filtri di esclusione reciproca tra flow** (vedi sezione Sormonti)
3. **Soglia Predicted CLV** per il conditional split del Flow 72: **150€** (media reale 22/7; ricalcolare ogni 3-6 mesi via API)
4. **Timing fissi** del Flow 71 (per famiglia pack)
5. **Copy delle email**, oggetti, dynamic content variables
6. **Sconti e codici coupon**

---

## Sequenza logica del cliente attraverso i flow

Un cliente attraversa i flow in una precisa sequenza temporale. Ogni flow ha uno "stato cliente" preciso in cui si applica:

```
CLIENTE NUOVO
  ↓ compra 1° ordine
[Fase 2: 21 Primo Cliente + 24-37 prodotto + 23 Recensione]
  ↓ ~T+25gg-30gg dopo il primo ordine
[71 First-Order Reorder] — timing fisso famiglia pack
  ↓ SE cliente riordina → esce e diventa "Cliente Ricorrente"

CLIENTE RICORRENTE (Lifetime Orders ≥ 2)
  ↓ Klaviyo calcola Expected Date of Next Order
[72 AI Repeat Purchase] — al momento di ENO personalizzata
  ↓ SE cliente ordina → esce
  ↓ SE cliente ignora → passa nella fase successiva
  
  Contemporaneamente, quando Klaviyo lo determina:
[78 Cross-Sell Data-Driven] — al Best Cross-Sell Date del cliente
  ↓ Suggerisce prodotto complementare (Next Best Product)

CLIENTE CHE SI SCOSTA (~30-60gg dopo ENO senza ordinare)
  ↓ RFM classifica il profilo come "Needs Attention" o "At Risk"
[73 RFM Winback] — trigger su segmento RFM
  ↓ SE cliente riordina → esce, torna a Cliente Ricorrente
  ↓ SE ignora → RFM lo classifica "Inactive" dopo altri gg

CLIENTE INATTIVO (180gg+ senza ordine + no engagement)
  ↓ Segmento cattura la condizione
[75 Sunset Cliente Storico] — nurturing soft senza suppress hard
  ↓ SE risponde/riacquista → esce
  ↓ SE non risponde → resta in newsletter frequenza ridotta

CLIENTE ISCRITTO MAI ATTIVO (180gg+ iscritto + 0 ordini + 0 engagement)
  ↓
[74 Sunset Lead] — 2 email + suppress hard
```

## Sormonti tra flow — analisi e risoluzione

Ci sono **4 punti di sormonto reali** che dobbiamo gestire con filtri di esclusione precisi.

### Sormonto 1 — Flow 72 (AI Repeat Purchase) vs Flow 73 (RFM Winback)

**Dove**: cliente non riordina dopo la sua ENO, riceve Flow 72 Below CLV (fino a 3 email in 17gg con sconto). Se ancora non ordina, RFM lo classifica "Needs Attention" o "At Risk" (~15-30gg dopo). Il Flow 73 si triggera all'ingresso in questo segmento.

**Rischio**: cliente riceve nell'arco di 30-45gg il Flow 72 completo + Flow 73 completo = 3+3 = 6 email di winback con doppio sconto. Troppo aggressivo.

**Soluzione**: Flow 73 ha filtro di ingresso `NOT currently in Flow 72 AND has not received Flow 72 last email in last 30 days`. Cioè aspettiamo che il Flow 72 sia finito da almeno 30gg prima di far partire il 73.

### Sormonto 2 — Flow 73 (RFM Winback) vs Flow 75 (Sunset Cliente Storico)

**Dove**: cliente At Risk riceve Flow 73, non ordina, dopo altri 60-90gg diventa Inactive/scomparso. Segmento Flow 75 lo cattura (180gg totali).

**Rischio**: cliente riceve Flow 73 (3 email con sconto) + Flow 75 (2 email soft). Non è terribile, ma è ridondante se si sovrappongono.

**Soluzione**: Flow 75 ha filtro `NOT currently in Flow 73 AND has not received Flow 73 last email in last 60 days`. Serve gap ampio per aspettare che il Flow 73 abbia dato modo di rispondere.

### Sormonto 3 — Flow 71 (First-Order Reorder) vs Flow 72 (AI Repeat Purchase)

**Dove**: cliente al primo ordine riceve Flow 71 (2 email a T+25/T+30). Se non riordina, passa a "Lifetime Orders = 1" ancora (perché non ha fatto 2° ordine). Klaviyo Predictive con 1 ordine solo usa la mediana store per ENO (meno affidabile) e potrebbe triggerare Flow 72 sullo stesso cliente.

**Rischio**: cliente riceve 2 email Flow 71 + Flow 72 subito dopo = 4-5 email in 60gg tutte di reorder push.

**Soluzione**: Flow 72 ha filtro `Lifetime Number of Orders ≥ 2` (già presente) + `Has not received Flow 71 in last 365 days`. Il primo filtro basta in teoria, ma il secondo è cintura di sicurezza per casi edge.

### Sormonto 4 — Flow 73 (RFM At Risk) vs RFM "Inactive" nel tempo

**Dove**: RFM classifica come "At Risk" un cliente e triggeriamo il Flow 73. Poi lo stesso cliente diventa "Inactive" dopo settimane (RFM lo riclassifica automaticamente). Se avessimo un Flow triggerato su "Inactive", scatterebbe di nuovo.

**Rischio**: doppio winback sullo stesso cliente.

**Soluzione**: **non abbiamo un flow trigger separato su "Inactive"** (proprio per evitare questo). Il "cliente veramente perso" finisce nel **Flow 75 Sunset Cliente Storico** (segmento comportamentale, non RFM) con filtro NOT in Flow 73.

## Filtri di esclusione riepilogati (da configurare in Klaviyo)

| Flow | Filtri di esclusione da mettere |
|------|--------------------------------|
| 71 | `Lifetime Orders = 1` (già natura del trigger) |
| 72 | `Lifetime Orders ≥ 2` + `Has not received Flow 71 email in last 365 days` |
| 73 | `NOT currently in Flow 72` + `Has not received Flow 72 last email in last 30 days` |
| 74 | Solo comportamentale (iscritti mai clienti — non sovrappone con nessuno) |
| 75 | `NOT currently in Flow 73` + `Has not received Flow 73 last email in last 60 days` + `Placed Order at least 1 time` |
| 76 | Nessuno (event-based standalone) |
| 78 | `NOT currently in Flow 72` (opzionale: evita doppio push nel medesimo istante) |

## Come Klaviyo classifica i clienti nei 6 gruppi RFM

Per capire meglio come vengono usati Flow 73 e Flow 75, ecco la definizione dei gruppi RFM (calcolo automatico Klaviyo):

| Gruppo RFM | Chi include | Cosa facciamo |
|------------|-------------|---------------|
| **Champions** | Alto Recency + Alta Frequency + Alta Monetary | Nessun flow winback — sono top clienti, li lasciamo tranquilli (eventualmente Flow 72 Above CLV) |
| **Loyal** | Alta F + Alta M ma R più basso | Idem, Flow 72 Above CLV se rilevante |
| **Recent Customer** | Alto R ma bassa F/M | Cliente nuovo, ancora in Flow 71 o post-purchase |
| **Needs Attention** | Media R + Media F + Media M — "sta rallentando" | **Flow 73** — intervento precoce |
| **At Risk** | Bassa R + storia F/M significativa | **Flow 73** — intervento urgente |
| **Inactive** | Bassa R + bassa F + bassa M — scomparso | **Flow 75** (via segmento comportamentale, non RFM diretto) o **Flow 74** se mai comprato |

**Nota**: Klaviyo aggiorna questi gruppi ogni notte. Un cliente può muoversi da un gruppo all'altro nel tempo automaticamente.

## Configurazione Segmenti da creare in Klaviyo

Da fare manualmente in Lists & Segments → Create Segment:

### Segmento "At Risk Winback" (per Flow 73)

```
Definition:
  Properties about someone > Predictive Analytics > Current RFM group is At Risk
  OR
  Properties about someone > Predictive Analytics > Current RFM group is Needs Attention
```

### Segmento "Sunset Lead" (per Flow 74)

```
Definition:
  Subscribed to email > over 180 days ago
  AND Placed Order zero times over all time
  AND Last opened > 90 days ago
  AND Last clicked > 90 days ago
```

### Segmento "Sunset Customer" (per Flow 75)

```
Definition:
  Placed Order at least 1 time over all time
  AND Last placed order > 180 days ago
  AND Last opened > 180 days ago
  AND Last clicked > 180 days ago
```

### Segmento "Above Average CLV" (per campagne dedicate — NON richiesto dal Flow 72)

```
Definition:
  Properties about someone > Predictive Analytics > Predicted CLV is at least 150
```

**Soglia: 150€** (media reale calcolata 22/7 su 2.895 clienti ricorrenti — stessa soglia dello split del Flow 72, tenerle allineate ai ricalcoli periodici).

**Chiarimento sul ruolo (22/7)**: il Flow 72 NON usa questo segmento — il conditional split dentro il flow valuta direttamente la property `Predicted CLV is at least 150` (più pulito, sempre aggiornato, nessuna dipendenza). Il segmento serve per le **campagne manuali ai VIP**: in particolare per mantenere la promessa dell'email Above ("sarai tra le prime persone a saperlo") — a ogni lancio nuovo prodotto, mandare una campagna a questo segmento 48-72h prima dell'annuncio pubblico.

## Requisiti operativi da verificare

- [x] **Marketing Analytics attivato** — trial 30gg avviato (Andrea, 2026-06-18)
- [x] **Integrazione WooCommerce** attiva e funzionante — già verificato
- [x] **Catalogo prodotti sincronizzato** con Klaviyo — da verificare
- [ ] **Revenue metric mapped** su evento "Placed Order" — da verificare
- [x] **500+ clienti storici + 180gg storico + 3+ ordini per almeno alcuni clienti** — Andrea conferma OK
- [x] **Aspettare 48h** dopo attivazione Catalog Insights per il processing dei report

## Cosa ci porta il trial Marketing Analytics (riepilogo)

| Feature | Senza trial | Con trial |
|---------|-------------|-----------|
| Expected Date of Next Order | ✅ già disponibile | ✅ |
| Predicted CLV | ✅ già disponibile | ✅ |
| Churn Risk (segment builder) | ⚠️ solo via CSV | ✅ nativamente segmentabile |
| **RFM Customer Groups** | ❌ non disponibile | ✅ **NUOVO** |
| **Catalog Insights + Next Best Product + Best Cross-Sell Date** | ❌ non disponibile | ✅ **NUOVO** |
| **Products Bought Same Cart / Next Order dashboard** | ❌ non disponibile | ✅ **NUOVO** |

Il trial di 30gg serve per capire se il piano permanente (costo tipicamente 100-200 €/mese in più) è ripagato dal revenue attribuito ai flow 72, 73 e 78.

## Come misuriamo il valore del trial (KPI a 30gg)

Metriche da guardare a fine trial per decidere se sottoscrivere il piano permanente:

1. **Revenue attribuito al Flow 72** (Predictive-triggered) vs stima di quello che avremmo ottenuto senza Predictive
2. **Revenue attribuito al Flow 78** (Catalog Insights) — è "nuovo" incremento, non replica di flow esistenti
3. **Conversion rate del Flow 78 Cross-Sell** — se > 5% è ottimo
4. **RFM shift**: quanti clienti At Risk sono tornati Loyal grazie al Flow 73

## Changelog
- **v2.0 (2026-07-14)**: aggiunta la sezione "Strategia sconti del ciclo retention" (decisioni Andrea): 72 no-sconto al lancio con opzione 10€ post-dati, 73 primo punto sconto (10%/15% univoci), 74 sunset lead con 20% univoco (E2+E3) e suppression solo zero-engagement, 75 BENTORNATO20 confermato, 78 con 10€ fissi per la prova prodotto. Tutti i codici univoci Klaviyo (WooCommerce nativo) tranne BENTORNATO20.
- **v1.1 (2026-06-18)**: Flow 78 dichiarato UNICO punto di cross-sell del sistema. Rimossa la vecchia email 2 cross-sell del Flow 22 Cliente Ricorrente (ora semplice grazie, v2.0). Sormonto 22/78 eliminato alla radice.
- v1.0 (2026-06-18): prima stesura completa. Include tabella architetturale, sequenza logica cliente, 4 sormonti analizzati, filtri di esclusione, definizione segmenti da creare in Klaviyo, requisiti operativi, KPI trial.
