**Versione:** 3.0
**Ultimo aggiornamento:** 2026-07-14

# Flow 73: RFM Winback

## Chi entra in questo flow

Clienti che Klaviyo classifica come **"At Risk"** o **"Needs Attention"** nel sistema RFM Customer Groups (aggiornato automaticamente ogni notte). Sono clienti che avevano un pattern di acquisto e ora stanno rallentando o hanno smesso di ordinare.

L'obiettivo è **recuperarli prima che diventino Inactive** (dove il recupero sarebbe molto più difficile).

## Razionale architetturale

**Perché RFM e non solo Predictive Churn Risk**: Klaviyo raccomanda RFM come metodo nativo per identificare clienti a rischio (fonte: klaviyo.com Marketing Analytics course). RFM è disponibile automaticamente nel segment builder col piano Marketing Analytics attivo, senza esportazioni CSV. Refresh notturno automatico.

**Perché "At Risk" + "Needs Attention" insieme**: intercettiamo il cliente **prima** che il churn sia consolidato. "Needs Attention" è il segnale precoce (rallentamento), "At Risk" è il segnale conclamato. Meglio agire su entrambi.

**Perché conditional split su Historic CLV (non Predicted CLV)**: Klaviyo Academy raccomanda esplicitamente HCLV per i winback, perché "il Predicted CLV di un cliente At Risk ha bias verso lo zero" (il modello prevede che non spenderà più). HCLV invece è il dato storico oggettivo di quanto ha già speso — sta a noi capire se vale la pena spendere per recuperarlo.

## Configurazione Klaviyo

**Trigger:** **Ingresso in segmento** `At Risk Winback` (segmento da creare in Klaviyo)

**Definizione del segmento (da creare in Lists & Segments → Create Segment):**

```
Nome: "At Risk Winback"
Definition:
  Properties about someone > Predictive Analytics > Current RFM group is At Risk
  OR
  Properties about someone > Predictive Analytics > Current RFM group is Needs Attention
```

**Trigger filter (flow filter al momento dell'ingresso):**
1. `Placed Order at least 1 time over all time` (solo clienti veri, no lead)
2. `NOT currently in Flow 72 AI Repeat Purchase`
3. `Has not received Flow 72 last email in last 30 days` (aspetta che il 72 sia finito e passato del tempo per non stressare)
4. `Placed Order zero times since starting this flow` (esce se ricompra)

**Smart Sending:** OFF

**Re-entry:** Allow re-entry, waiting period **90 days** (evita spam se il cliente oscilla tra At Risk e Needs Attention nelle settimane)

## Trigger — Machine Learning?

✅ **SÌ, parzialmente**. RFM Customer Groups è calcolato automaticamente da Klaviyo con algoritmo statistico proprietario (non deep AI, ma comunque automation avanzata). Il trigger `Current RFM group = At Risk / Needs Attention` viene aggiornato notturno per ogni profilo.

Il conditional split su Historic CLV è invece un dato storico oggettivo, non ML.

## Conditional Split: Historic CLV

Subito dopo l'ingresso nel flow, valutare `Historic CLV`:

| Ramo | Condizione | Cliente | Email | Sconto |
|------|------------|---------|-------|--------|
| **HIGH** | Historic CLV > 300€ | Top spender persi (valgono molto) | **3 email** | Sconto graduale (15% finale) |
| **STANDARD** | Historic CLV ≤ 300€ | Clienti medi persi | **2 email** | Sconto 10% (codice univoco) |

### Razionale dei rami

**High CLV persi**: hanno speso molto storicamente. Valgono l'investimento di 3 email + sconto più alto (15%) + reso facile. Klaviyo Academy: "Reintroduce brand" prima, poi "Highlight new releases", poi sconto forte.

**Standard**: 2 email dirette, 10% sconto. Se non funziona in 2 email non insistiamo di più — passano poi al Flow 75 Sunset Cliente Storico se restano inattivi.

## Mittenti per ramo

| Ramo | Email | Mittente |
|------|-------|----------|
| High CLV | Email 1 (T+0) | Lorenzo Zarone |
| High CLV | Email 2 (+7gg) | Lorenzo Zarone |
| High CLV | Email 3 (+7gg, ultima) | Flaminia (Customer Care) |
| Standard | Email 1 (T+0) | Flaminia (Customer Care) |
| Standard | Email 2 (+10gg, ultima) | Lorenzo Zarone |

## Coordinamento con altri flow

Vedi documento `00-mappatura-fase3.md` sezione Sormonti. Sintesi:
- Aspetta 30gg dalla fine del Flow 72 prima di scattare
- Cliente che riordina esce automaticamente (flow filter)
- Se non risponde, dopo altri 60gg può entrare in Flow 75 Sunset Cliente Storico

---

## RAMO HIGH CLV — Cliente storico persi (Historic CLV > 300€)

### Email 1 — Lorenzo (immediate dal trigger)

**Mittente:** Lorenzo Zarone
**Tipo:** Statica

#### Oggetto (3 varianti A/B)

- A: Volevo scriverti io di persona
- B: Sono passati troppi mesi senza sentirti
- C: Prima di chiudere il cerchio, un pensiero

#### Preview text (3 varianti)

- A: Niente sconti, niente offerte. Solo un pensiero.
- B: Nel silenzio ho fatto due conti. E volevo dirti una cosa.
- C: Da fondatore a cliente storico che sta scomparendo.

#### Corpo email

Ciao [NOME]

Sono Lorenzo. Ti scrivo io perché quando un cliente storico come te si allontana, io lo noto.

Ho controllato: hai fatto diversi ordini con noi nel tempo, poi c'è stato un silenzio. Non so cosa sia successo, e non voglio riempirti la casella di email di recupero automatiche.

Voglio solo dirti tre cose, poi ti lascio in pace se preferisci.

**Uno**: qualunque sia il motivo per cui hai smesso (prezzo, dubbi sul prodotto, cambiamento nella tua vita, o semplicemente perché è passato il tempo), mi farebbe piacere saperlo. Le mail come questa ci permettono di capire dove miglioriamo. **Rispondi pure a questa email**: la leggiamo io e il mio team, e ti rispondiamo. Anche solo una riga.

**Due**: da quando hai smesso di ordinare abbiamo continuato a lavorare. Sono usciti nuovi prodotti, alcuni sono in cantiere. La gamma è cresciuta. Se vuoi vedere cosa è cambiato senza pressione, ti lascio il link al **[nostro catalogo](https://paleocomplex.com/negozio/)**.

**Tre**: nel prossimo mese riceverai da noi altre due email. Poi ridurremo drasticamente la frequenza, se non risponderai. Nessuna insistenza, niente email a raffica.

Un forte abbraccio
Lorenzo Zarone
Fondatore di Paleocomplex

---

### Email 2 — Lorenzo (+7gg dopo Email 1)

**Mittente:** Lorenzo Zarone
**Tipo:** Statica con dynamic content sui nuovi prodotti

#### Oggetto (3 varianti A/B)

- A: Le cose nuove nate mentre non c'eri
- B: Ti aggiorno su cosa è cambiato
- C: Dietro le quinte di questo silenzio

#### Preview text (3 varianti)

- A: 4 novità che potrebbero interessarti.
- B: Il mio catalogo è cambiato. Ecco come.
- C: Niente vendita. Solo aggiornamento.

#### Corpo email

Ciao [NOME]

Sono Lorenzo di nuovo. Come promesso, oggi ti aggiorno su cosa è cambiato mentre eri via. Nessuna proposta commerciale, solo un aggiornamento.

**Renaissance**: se non l'hai mai provato, è il nostro anti-aging cellulare avanzato. 13 nutraceutici che lavorano su meccanismi profondi (senolitici, NAD+, autofagia). È il prodotto più clinicamente sofisticato che ho formulato.

**Essentiel**: multivitaminico senza krill (per chi è allergico) con focus cognitivo. 34 nutrienti tra cui citicolina e acetil-carnitina. Formato 60gg, molto più conveniente.

**Jeunesse**: se conoscevi Youth, Jeunesse è il fratello maggiore. 12g di collagene grass-fed + antiossidanti cutanei avanzati (astaxantina, pino corteccia).

**E non è finita**: sto lavorando su nuove formule. Non prometto date, ma se ti fa piacere sapere quando saranno pronte, resta con noi in newsletter.

Se vuoi guardare senza fretta:
**[Vai al catalogo aggiornato](https://paleocomplex.com/negozio/)**

Se vuoi confrontarti su cosa potrebbe avere senso per te oggi (magari le tue esigenze sono cambiate rispetto all'inizio), **rispondi a questa email**: la leggiamo io e il mio team.

La prossima settimana Flaminia ti scriverà con un'ultima cosa, poi ti lascio scegliere.

Un forte abbraccio
Lorenzo Zarone
Fondatore di Paleocomplex

---

### Email 3 — Flaminia (+7gg dopo Email 2, ultima)

**Mittente:** Flaminia (Customer Care)
**Tipo:** Statica con codice sconto univoco

#### Oggetto (3 varianti A/B)

- A: L'ultima email di questo ciclo
- B: Un'ultima cosa per te da parte nostra
- C: 15% e reso facile, se ti serve una spinta

#### Preview text (3 varianti)

- A: Codice personale valido 14 giorni. E reso facile.
- B: Se il prezzo era il freno, adesso non lo è più.
- C: La nostra ultima proposta, senza altre insistenze.

#### Corpo email

Ciao [NOME]

Sono Flaminia. Lorenzo ti ha scritto due volte nelle ultime settimane. Prendo io il testimone per l'ultima email di questo ciclo.

Se dopo queste settimane non hai ancora riordinato, ho un'ipotesi: forse hai valutato ma il prezzo pieno ti frena. Capita a molti clienti storici, non c'è nulla di male ad ammetterlo.

Ti do un ultimo aiuto concreto:

**Codice personale per te**: **{{ unique_coupon_code }}**
**Sconto**: 15% sul tuo prossimo ordine
**Validità**: 14 giorni. Scade a mezzanotte del 14° giorno.
**Bonus**: reso facile se il prodotto non ti convince. Basta un'email e organizziamo tutto.

Non ci sono trucchi. Se vuoi riprendere, questo è il momento.

**[Riordina con il tuo codice](https://paleocomplex.com/negozio/)**

Se invece hai deciso che non fa più per te, va bene lo stesso. Per i prossimi mesi non riceverai altri promemoria automatici da parte nostra. Resterai nella nostra newsletter, con i contenuti di sempre e ogni tanto le nostre novità.

Grazie per il tempo che ci hai dedicato negli anni.

Flaminia
Customer Care Paleocomplex

---

## RAMO STANDARD — Historic CLV ≤ 300€

### Email 1 — Flaminia (immediate dal trigger)

**Mittente:** Flaminia (Customer Care)
**Tipo:** Statica

#### Oggetto (3 varianti A/B)

- A: Ci sei ancora? Volevo sentirti
- B: Un promemoria da parte nostra, senza pressione
- C: Volevo scriverti una cosa

#### Preview text (3 varianti)

- A: 10% di sconto se vuoi riprendere il percorso.
- B: Nessuna offerta. Solo una domanda.
- C: Sono passati mesi. Come va?

#### Corpo email

Ciao [NOME]

Sono Flaminia di Paleocomplex. Ti scrivo perché ho notato che è passato del tempo dal tuo ultimo ordine con noi.

Non ti sto inseguendo. Ti scrivo perché voglio farti una domanda semplice: **come va?** Hai continuato l'integrazione con qualcos'altro, hai fatto una pausa, hai cambiato prodotto?

Se vuoi rispondermi con una riga sola, sarei felice di leggerla. Aiuta noi a capire dove miglioriamo e dà a te la possibilità di dirci se qualcosa non ha funzionato.

Nel frattempo, se sei nella posizione di voler riprendere il percorso, ti lascio un piccolo aiuto:

**Codice personale: {{ unique_coupon_code_riprendi }}** (10% di sconto sul tuo prossimo ordine)
**Validità**: 14 giorni. Scade a mezzanotte del 14° giorno, poi non funziona più

**[Riprendi il percorso](https://paleocomplex.com/negozio/)**

Se non è il momento giusto, va bene. Ti scriveremo un'ultima email tra qualche giorno, poi ti lasciamo decidere.

A presto
Flaminia
Customer Care Paleocomplex

---

### Email 2 — Lorenzo (+10gg dopo Email 1, ultima)

**Mittente:** Lorenzo Zarone
**Tipo:** Statica

#### Oggetto (3 varianti A/B)

- A: Ultima nota da parte mia
- B: Prima che chiudiamo qui
- C: Se hai due minuti: quello che voglio dirti io

#### Preview text (3 varianti)

- A: Nessuna manipolazione. Solo trasparenza.
- B: Poi lascio decidere a te.
- C: Da fondatore, senza filtri.

#### Corpo email

Ciao [NOME]

Sono Lorenzo. Flaminia ti ha scritto qualche giorno fa. Prendo io il testimone per l'ultima email di questo ciclo automatico.

Ti dico onestamente cosa succede da qui in poi.

Se non riordini o non rispondi, per un lungo periodo non riceverai promemoria di riacquisto. Continuerai a ricevere la nostra newsletter (contenuti su salute, alimentazione e integrazione, e ogni tanto le nostre offerte), che puoi disattivare quando vuoi.

Il tuo codice personale del 10% scade tra 4 giorni, a mezzanotte. Se vuoi tornare, questo è il momento.

Voglio dirti una cosa da fondatore: la costanza è quello che ho sempre predicato ai nostri clienti. Non ti sto chiedendo di riordinare per farmi un favore. Ti sto chiedendo di riflettere se il tuo percorso di salute vale il piccolo sforzo di riprendere in mano l'integrazione. Se sì, siamo qui. Se no, va bene lo stesso: l'integrazione non è per tutti.

**[Vai al negozio](https://paleocomplex.com/negozio/)**

Se vuoi confrontarti prima di decidere, **rispondi a questa email**: la leggiamo io e il mio team.

Un forte abbraccio
Lorenzo Zarone
Fondatore di Paleocomplex

---

## Note operative

### Codici sconto

**Entrambi i rami usano codici UNIVOCI generati da Klaviyo** (decisione Andrea 2026-07-14 — supporto WooCommerce nativo confermato):

- **{{ unique_coupon_code_riprendi }}** (10%, univoco, 14gg): Email 1 Standard
- **{{ unique_coupon_code }}** (15%, univoco, 14gg): Email 3 High CLV

**Setup Klaviyo unique coupons per WooCommerce** (guida: help.klaviyo.com/hc/en-us/articles/22168739689627):
1. In WooCommerce: Marketing → Coupons → crea 2 coupon "master": `RIPRENDI10` (10%) e `WINBACK15` (15%), entrambi con **Usage limit: 1 per coupon + 1 per user** e scadenza relativa gestita da Klaviyo
2. In Klaviyo: Content → Coupons → tab WooCommerce Coupons → Create WooCommerce Coupon → collega i master
3. Imposta un **prefix** riconoscibile (es. `RP10-` e `WB15-`): Klaviyo genera codici tipo `RP10-H3SHFR7KGS`, uno per profilo
4. Imposta il batch minimo di codici da tenere pronti (Klaviyo li rigenera in automatico)
5. Nelle email, inserisci il tag coupon dal template editor (blocco Coupon) — il codice si compila per profilo

Vantaggi: scadenza reale per-destinatario (14gg dalla ricezione), zero condivisione sui forum, zero manutenzione manuale.

Configurare codici univoci in WooCommerce app coupon (Yith Coupon Email o simile) collegati a Klaviyo via integrazione standard.

### Perché no sconto nella Email 1/2 High CLV

Klaviyo Academy raccomanda per top clienti persi di **partire con brand reintroduction e news**, NON con sconto. Lo sconto arriva solo nell'ultima email (Email 3) come "cintura di sicurezza" per chi era frenato dal prezzo. Prima di quello, il messaggio è: "ci sei mancato, ecco cosa è cambiato, senza pressione".

### Reso facile solo in High CLV Email 3

Ridurre il rischio percepito del cliente storico che teme di "sbagliare a riordinare". NOTA (Andrea 2026-06-18): il reso è possibile ma le spese di spedizione del reso sono a carico del cliente — per questo il copy dice "reso facile" SENZA promettere "senza spese". Per clienti standard non menziono reso.

### Soglia HCLV 300€

Stima iniziale. Ricalibrare a metà trial guardando la distribuzione HCLV nel segmento "1+ ordini". Se la mediana HCLV è ~150€, magari 300€ è troppo alto e va abbassato. Se la mediana è 400€, 300€ è troppo basso.

### Filtri di esclusione riepilogo

Cliente entra solo se:
- Ha fatto almeno 1 ordine (no lead puri)
- NON è attualmente nel Flow 72
- Non ha ricevuto l'ultima email del Flow 72 negli ultimi 30gg
- Non ha ordinato dall'inizio di questo flow

### Schema flow Klaviyo

```
[Segmento At Risk Winback → Trigger su ingresso]
    │
    ▼
[Trigger Filter]
  - Placed Order ≥ 1 over all time
  - NOT currently in Flow 72
  - Has not received Flow 72 last email in last 30 days
  - Placed Order zero times since starting this flow
    │
    ▼
[Conditional Split: Historic CLV > 300€]
    │
    ├── YES (High CLV)
    │     ▼ immediate
    │     Email 1 Lorenzo (brand reintroduction, no sconto)
    │     ▼ wait 7 days [filter: no order since]
    │     ▼
    │     Email 2 Lorenzo (highlight new releases, no sconto)
    │     ▼ wait 7 days [filter]
    │     ▼
    │     Email 3 Flaminia (15% univoco + reso facile)
    │
    └── NO (Standard)
          ▼ immediate
          Email 1 Flaminia (RIPRENDI10X9 10%)
          ▼ wait 10 days [filter]
          ▼
          Email 2 Lorenzo (ultima trasparenza, codice ancora valido)
```

### Sormonto Flow 73 vs Flow 75 Sunset Cliente Storico

Cliente che finisce il Flow 73 senza riordinare entra automaticamente in "Inactive" secondo RFM dopo altre 30-60gg. Ma abbiamo deciso che **Flow 75 usa un segmento comportamentale** (Last Placed > 180gg + Last Open > 180gg) NON il gruppo RFM Inactive, per due motivi:
1. Il gruppo RFM Inactive è calcolato in base ai pattern F/R/M, non ci controlliamo la soglia
2. Il segmento comportamentale con 180gg dà tempo al Flow 73 di finire ed esaurire l'effetto

Filtro extra su Flow 75: `NOT received Flow 73 last email in last 60 days`. Così Flow 75 parte solo dopo che Flow 73 ha avuto tempo di esaurirsi.

### Status
Bozza v1.0 — pronto per montaggio Klaviyo. Richiede Marketing Analytics attivo per RFM.

### Changelog
- **v3.0 (2026-07-14)**: codici sconto UNIVOCI Klaviyo su entrambi i rami (RIPRENDI10X9 statico eliminato). Supporto WooCommerce nativo verificato; setup documentato nelle note operative. Il Flow 73 è ora il PRIMO punto sconto dell'intero ciclo retention (il 72 è diventato no-sconto): scala 10% Standard / 15% High CLV coerente e crescente.
- **v2.0 (2026-06-18)**: fix da verifica content-verifier + decisioni Andrea. (1) Reso: il copy non promette più "senza spese" (le spese di reso sono a carico del cliente) → "reso facile... organizziamo tutto". (2) Codice RIPRENDI10 → **RIPRENDI10X9** (alfanumerico, validità 14gg). (3) Promesse di silenzio rese veritiere ("per i prossimi mesi..."), tolto "(davvero)" dall'oggetto. (4) Anglicismi rimossi (pitch, automation). (5) Fix sintassi ("Bastano un'email"). (6) "Ti scriverò altre due email" → "riceverai da noi" (la terza è di Flaminia). (7) Pipeline resa vaga ("nuove formule"). (8) "Leggo io" → "la leggiamo io e il mio team". (9) Newsletter descritta onestamente (include offerte).
- v1.0 (2026-06-18): prima stesura. Trigger RFM (At Risk + Needs Attention), conditional split Historic CLV (300€ soglia). Ramo High CLV con brand reintroduction + news + sconto finale univoco 15% + reso facile. Ramo Standard con 10% + trasparenza finale. Filtri di esclusione con Flow 72 (30gg gap) e coordinamento con Flow 75 (60gg gap).
- v1.0 (2026-06-18): prima stesura. Trigger RFM (At Risk + Needs Attention), conditional split Historic CLV (300€ soglia). Ramo High CLV con brand reintroduction + news + sconto finale univoco 15% + reso facile. Ramo Standard con 10% RIPRENDI10 + trasparenza finale. Filtri di esclusione con Flow 72 (30gg gap) e coordinamento con Flow 75 (60gg gap).
