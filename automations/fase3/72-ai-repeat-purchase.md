**Versione:** 2.0
**Ultimo aggiornamento:** 2026-06-18

# Flow 72: AI Repeat Purchase Flow (Predictive-powered)

## Chi entra in questo flow

Clienti **ricorrenti con storia sufficiente** (`Customer's Lifetime Number of Orders ≥ 2`) per cui Klaviyo Predictive Analytics calcola previsioni personalizzate affidabili. Il flow si triggera quando viene raggiunta la `Expected Date of Next Order` calcolata da Klaviyo sul pattern d'acquisto storico del cliente.

L'obiettivo è **accompagnare il cliente al riacquisto naturale** sfruttando il momento di massima propensione previsto dall'AI. Per i clienti **above-average CLV** la spinta è premium/community-building (no sconto). Per i clienti **below-average CLV** la spinta include incentivo (sconto modulato).

Implementa il **template ufficiale Klaviyo Academy** "Increase CLV with a refined AI repeat purchase flow" (corso "Use predictive analytics to retain more customers"), adattato alla realtà Paleocomplex (no sistema loyalty connesso, no programma referral).

## Razionale architetturale

**Perché serve un secondo flow oltre al 71**: il Flow 71 First-Order Reorder è timing-fisso e copre solo i primi clienti. Per i clienti ricorrenti, Klaviyo Predictive sa quando ognuno fa il prossimo ordine (calibrato sul SUO pattern personale, non sulla mediana store). Sfruttare questa precisione = email arrivano al momento ottimale, con conversion rate più alto.

**Perché conditional split su Predicted CLV**: Klaviyo Academy raccomanda esplicitamente di non trattare tutti i clienti ricorrenti allo stesso modo. Cliente high-CLV è probabilmente già loyal: lo sconto lo svaluta e brucia margine. Cliente low-CLV ha bisogno di incentivo per crescere. Split = ROI massimizzato.

**Quando attivare il flow**: 60-90 giorni dopo go-live Klaviyo, quando Predictive ha abbastanza dati per calcolare ENO e Predicted CLV affidabili. Prima è prematuro (mediana store, non personalizzata).

**Soglia Predicted CLV**: da calcolare media del segmento `Has placed 1+ orders` esportando CSV (Manage segment → Export to CSV → media colonna `predicted_clv`). Per partire, soglia stimata **200€**. Da ricalibrare con dati reali.

## Configurazione Klaviyo

**Trigger:** `Expected Date of Next Order` (date property)

**Trigger frequency:** **`never`** (CRITICO: senza questa impostazione il flow rispedirebbe in loop ogni ricalcolo della data — fonte: Klaviyo Academy)

**Trigger filter (flow filter applicato all'ingresso):**
1. `Customer's Lifetime Number of Orders is at least 2`
2. `Placed Order zero times since starting this flow` (esce subito se ricompra)
3. `Has not received Flow 71 First-Order Reorder Reminder in last 365 days` (evita doppio reminder a chi è uscito dal 71 senza riacquistare ed è ora al 2° ordine)

**Smart Sending:** OFF

**Re-entry:** Allow re-entry, waiting period **365 days** (massima dilazione, evita stress della soglia ENO ricalcolata)

## Conditional Split: Predicted CLV

Subito dopo il trigger, lo split valuta `Predictive analytics about someone > Predicted CLV is at least [SOGLIA]`.

| Ramo | Condizione | Cliente | Numero email | Sconto |
|------|------------|---------|--------------|--------|
| **YES — Above CLV** | Predicted CLV ≥ soglia (~200€) | Top spender / loyal | **2 email** | NO (community-building) |
| **NO — Below CLV** | Predicted CLV < soglia | Cliente da coltivare | **3 email** | SÌ (10% → 15%) |

### Razionale dei due rami

**Above CLV (Cliente Top)**: già spende sopra la media. Non va incentivato col prezzo ma valorizzato. Klaviyo Academy raccomanda: early access, premium suggestions, richiesta testimonial, invito a programmi di status. Nel nostro caso (no loyalty connesso, no referral), gli incentivi non-monetari sono:
- Early access alla prossima formula/lancio
- Bundle premium curato da Lorenzo
- Richiesta testimonial pubblico (riconoscimento)
- Dialogo personale con Lorenzo (rispondi a questa email)

**Below CLV (Cliente da Coltivare)**: ha potenziale ma non è ancora top. L'incentivo monetario è giustificato per spingerlo verso lo step successivo. 10% sull'email 1, escalation a 15% sull'email 3 finale.

## Mittenti per ramo

| Ramo | Email | Mittente |
|------|-------|----------|
| Above CLV | Email 1 (immediate) | Lorenzo Zarone |
| Above CLV | Email 2 (+7gg) | Lorenzo Zarone |
| Below CLV | Email 1 (immediate) | Flaminia (Customer Care) |
| Below CLV | Email 2 (+7gg) | Flaminia (Customer Care) |
| Below CLV | Email 3 (+10gg, ultima) | Lorenzo Zarone |

**Pattern**:
- Above CLV: Lorenzo coerente per tutto il ramo (autorità, riconoscimento, voice del fondatore al cliente top)
- Below CLV: Flaminia per le prime due (warmer, customer care attento), Lorenzo nell'ultima (autorità che chiude il loop con sconto più alto, ultimo push)

## Coordinamento con altri flow

```
[Cliente ha già fatto 2+ ordini]
    │
    ▼
Klaviyo calcola Expected Date of Next Order (ENO)
    │
    ▼
Trigger Flow 72 alla data ENO
    │
    ├── Above CLV (no sconto) — 2 email distribuite in 7gg
    │
    └── Below CLV (sconto) — 3 email distribuite in 17gg

Filtri di esclusione:
- Se cliente ricompra: esce subito dal flow (filter Placed Order zero times)
- Se cliente passa in At Risk RFM: non viene mandato nel Flow 73 (filter NOT in Flow 72)
- Se cliente è Lifetime Orders = 1: non entra (filter ≥ 2)
```

**Filtro reciproco Flow 73**: il Flow 73 (At Risk Winback) ha filtro `NOT currently in Flow 72`. Se il cliente non risponde al Flow 72 e finisce in At Risk RFM, il Flow 73 parte solo DOPO che il 72 è terminato.

---

## RAMO ABOVE CLV — Cliente Top (predicted CLV ≥ soglia)

### Email 1 — Lorenzo (immediate dal trigger)

**Mittente:** Lorenzo Zarone
**Tipo:** Statica

#### Oggetto (3 varianti A/B)

- A: Volevo dirti una cosa, da fondatore a cliente storico
- B: Sei una delle persone che mi aiutano a crescere
- C: Un pensiero per te

#### Preview text (3 varianti)

- A: Niente vendite. Solo un riconoscimento.
- B: Sei tra le persone che fanno la differenza per noi.
- C: Tra qualche giorno ti scrivo qualcosa di concreto.

#### Corpo email

Ciao [NOME]

Sono Lorenzo. Ti scrivo per una cosa diversa dal solito.

Ho fatto due conti sui clienti che, da quando ho fondato Paleocomplex, hanno scelto di continuare con noi nel tempo. Sei tra questi.

Non sono numeri buttati lì: tu hai investito sulla tua salute con noi più di quanto faccia la maggior parte dei nostri clienti. Te lo dico perché lo voglio riconoscere esplicitamente. Spesso si parla solo di acquisizione e si dimentica chi è già qui da tempo. Io non voglio fare questo errore.

Ti scrivo per due motivi.

**Primo**, voglio chiederti un favore. Se hai esperienza concreta con i nostri prodotti, un cambiamento misurabile, un risultato che ti ha sorpreso, **rispondi pure a questa email** e raccontamelo. Le testimonianze dei clienti come te valgono per noi più di qualunque pubblicità. E mi farebbe davvero piacere sapere come sta andando.

**Secondo**, da qui in poi voglio che tu sappia delle cose prima degli altri. Nei prossimi mesi usciranno delle novità (alcuni prodotti sono in fase finale di sviluppo, su altri stiamo lavorando). Sarai tra le prime persone a saperlo.

Tra qualche giorno ti scrivo con qualcosa di più concreto: un suggerimento di prodotti che potrebbero completare bene il tuo protocollo, dato quello che usi già.

Grazie per la fiducia.

Un forte abbraccio
Lorenzo Zarone
Fondatore di Paleocomplex

---

### Email 2 — Lorenzo (+7gg dopo Email 1)

**Mittente:** Lorenzo Zarone
**Tipo:** Statica + dynamic content per protocollo cliente

#### Oggetto (3 varianti A/B)

- A: Il prossimo passo del tuo protocollo
- B: Un suggerimento che faccio raramente
- C: Quello che potrebbe portarti al livello successivo

#### Preview text (3 varianti)

- A: Niente sconto. Solo logica di sinergie.
- B: Per chi ha già fatto i primi 6-12 mesi seri.
- C: Cosa abbinare a quello che usi già.

#### Corpo email

Ciao [NOME]

Eccoci. Come ti dicevo nell'altra email, voglio dirti una cosa concreta.

Hai costruito una base seria con il tuo protocollo di integrazione. A questo punto, se vuoi andare a un livello superiore, ci sono due strade che vedo per chi è già rodato come te.

**La prima: anti-aging cellulare profondo (Renaissance)**

Se non lo stai già usando, Renaissance lavora su meccanismi che nessun multivitaminico copre: senolitici (eliminazione cellule vecchie), NAD+ (energia mitocondriale), autofagia, supporto telomeri. Non è un sostituto del tuo prodotto, è un'aggiunta complementare per chi ha già le basi solide. Puoi notare miglioramenti nei marker infiammatori e nel profilo lipidico, misurabili nelle analisi.

**[Scopri Renaissance](https://paleocomplex.com/prodotto/renaissance/)**

**La seconda: sport e longevità funzionale (Hurricane + Armageddon)**

Se ti alleni seriamente o vuoi mantenere la massa magra negli anni (specialmente da 40+ in su), il combo Hurricane + Armageddon è quello che consiglio. Pre-workout completo + aminoacidi essenziali. Lavorano in sinergia.

**[Scopri la linea sport](https://paleocomplex.com/categoria-prodotto/sport/)**

Una nota: **non c'è nessuno sconto in questa email**. Non lo trovi qua perché non lo voglio dare. Quando proporrò una cosa a un cliente come te, voglio che sia perché la sceglie consapevolmente, non perché ha visto un codice.

Se vuoi confrontarti su quale di queste due strade ha più senso per te, o se hai dubbi su come incastrarle con quello che usi già, **rispondi a questa email**. Te lo dico io personalmente.

Un forte abbraccio
Lorenzo Zarone
Fondatore di Paleocomplex

---

## RAMO BELOW CLV — Cliente da Coltivare (predicted CLV < soglia)

### Email 1 — Flaminia (immediate dal trigger) — Reorder reminder + sconto soft

**Mittente:** Flaminia (Customer Care)
**Tipo:** Statica

#### Oggetto (3 varianti A/B)

- A: Stavo pensando a te. Ti scrivo io.
- B: La costanza è quello che conta. Te lo ricordo.
- C: Una nota veloce, e un piccolo aiuto

#### Preview text (3 varianti)

- A: Il momento giusto per continuare il percorso.
- B: Sappiamo che vuoi continuare, ti facciamo un regalo.
- C: 10% di sconto se vuoi continuare adesso.

#### Corpo email

Ciao [NOME]

Sono Flaminia. Ti scrivo perché, di solito, a questo punto del percorso il prodotto sta per finire. E non vorrei che ti trovassi con un buco proprio adesso.

So che con noi hai fatto già più di un ordine: significa che il percorso sta funzionando e che la costanza per te non è una novità. Non sto qui a ripetertelo, lo sai meglio di me.

Però lo so anche un'altra cosa: a volte tra un ordine e l'altro passa qualche giorno di troppo, e quei pochi giorni di interruzione sono uno spreco rispetto al lavoro che stai facendo.

Per non lasciarti questo dubbio, ti faccio un piccolo regalo. Se vuoi riordinare adesso senza interruzione, usa il codice **CONTINUA10K7** per avere il **10% di sconto** sul tuo prossimo ordine.

Valido per 14 giorni. Spedizione veloce come sempre.

**[Riordina sul nostro sito](https://paleocomplex.com)**

Se hai dubbi sul prodotto, su un eventuale cambio o vuoi parlarne, **rispondi pure a questa email**. Leggo io.

A presto
Flaminia
Customer Care Paleocomplex

---

### Email 2 — Flaminia (+7gg dopo Email 1) — Social proof + bundle

**Mittente:** Flaminia (Customer Care)
**Tipo:** Statica

#### Oggetto (3 varianti A/B)

- A: Cosa ci raccontano i clienti che ce l'hanno fatta
- B: Storie vere di chi ha continuato il percorso
- C: Una settimana fa ti ho scritto. Eccomi di nuovo.

#### Preview text (3 varianti)

- A: Tre storie di clienti che hanno tenuto duro.
- B: La differenza tra il 1° mese e il 4°.
- C: Il codice CONTINUA10K7 è ancora valido.

#### Corpo email

Ciao [NOME]

Sono Flaminia di nuovo. Una settimana fa ti ho scritto per il riacquisto. So che non l'hai ancora fatto e non voglio mettere pressione. Voglio raccontarti qualcosa.

Negli ultimi mesi ho letto centinaia di recensioni dei nostri clienti. Tre storie sul valore della costanza mi sono rimaste in mente, e oggi le condivido con te.

*"Ottimo prodotto che ormai uso da anni. Aiuta molto nei periodi di stanchezza e stress. Ho sentito la differenza in un periodo di sospensione che ho fatto e devo dire che ora, assumendolo di nuovo, mi sento in buona energia e mai stanca."*
**Ornella B.**

*"Non ho trovato immediato beneficio, ma alla terza confezione non credo sia un caso che i dolori siano quasi scomparsi e la stanchezza attenuata. Mi sento di consigliarlo, e ovviamente continuo a monitorare."*
**Alessia D.**

*"L'ho utilizzato con costanza e ho visto risultati concreti, soprattutto in termini di vitalità e concentrazione."*
**Paola L.**

Il messaggio comune: i risultati arrivano a chi non interrompe. E chi ha provato a sospendere, come Ornella, ha sentito la differenza.

Il codice **CONTINUA10K7** (10% di sconto) è ancora valido per qualche giorno, se vuoi continuare adesso.

**[Riordina sul nostro sito](https://paleocomplex.com)**

A presto
Flaminia
Customer Care Paleocomplex

---

### Email 3 — Lorenzo (+10gg dopo Email 2, = T+17 dal trigger) — Ultima chance, sconto più alto

**Mittente:** Lorenzo Zarone
**Tipo:** Statica

#### Oggetto (3 varianti A/B)

- A: L'ultima cosa che ti chiedo su questo
- B: Per riprendere il tuo percorso, il mio ultimo aiuto
- C: Una decisione, e poi ti lascio in pace

#### Preview text (3 varianti)

- A: 15% di sconto con un codice personale. Poi mi fermo.
- B: Te lo dico io: continua, o decidi di smettere. Non c'è terzo.
- C: Il momento di chiudere questo loop.

#### Corpo email

Ciao [NOME]

Sono Lorenzo. Te lo dico onestamente: è passato più o meno il tempo in cui di solito si arriva al riordino, e il tuo non è arrivato. Flaminia ti ha scritto due volte nelle ultime settimane. Nessun riordino ancora.

Ho due ipotesi.

**La prima**: hai deciso che non fa per te. Va bene anche questo, nessun problema. Se è questo il caso, **rispondi pure a questa email** e dimmelo. Mi farebbe piacere sapere che cosa non ha funzionato: il prodotto, il prezzo, il timing, il sapore, qualsiasi cosa. Vorrei migliorare il servizio per chi viene dopo di te.

**La seconda**: vuoi continuare ma stai aspettando il momento giusto, o un piccolo aiuto economico.

Se sei nel secondo caso, ti do un ultimo aiuto. Codice **{{ unique_coupon_code }}** che ti dà il **15% di sconto** sul tuo prossimo ordine. È un codice personale, generato per te: vale 14 giorni dalla ricezione di questa email, poi scade.

**[Riordina con il tuo codice](https://paleocomplex.com)**

Dopo questa email, per le prossime settimane non riceverai altri promemoria di riordino da parte mia. Tornerai nella nostra newsletter: contenuti su salute e integrazione, e ogni tanto le nostre novità.

Spero di rivederti.

Un forte abbraccio
Lorenzo Zarone
Fondatore di Paleocomplex

---

## Note operative

### Soglia Predicted CLV — come calcolarla

Una volta che Klaviyo ha 60-90gg di dati post go-live:

1. Crea segmento `Has placed at least 1 order`
2. Manage segment → Export to CSV
3. Apri in Excel/Numbers
4. Calcola **media** della colonna `predicted_clv`
5. Usa questo numero nel conditional split

Per partire (e per inserire una soglia temporanea): **200€**. Da ricalibrare con dati reali quando disponibili.

### Codice univoco — perché

Klaviyo permette di generare codici univoci (uno per profilo), con validità limitata nel tempo. Va configurato nell'app coupon di WooCommerce e collegato a Klaviyo via integrazione standard. **Importante**: codice univoco impedisce che venga condiviso pubblicamente (es. screenshot su forum). Nel Flow 72 Email 3 Below CLV uso `{{ unique_coupon_code }}` come placeholder per il codice generato.

Per Email 1 Below CLV uso `CONTINUA10K7` (10%): codice statico ma con nome alfanumerico che comunica temporaneità (decisione Andrea 2026-06-18). Validità dichiarata 14 giorni — configurare in WooCommerce con scadenza assoluta rinnovata periodicamente, oppure limite 1 uso per cliente. La sequenza è coerente: Email 1 (T+0, codice 14gg) → Email 2 (T+7, codice ancora valido per 7gg) → Email 3 (T+17, il CONTINUA10K7 è scaduto, arriva il codice personale 15%).

### Dynamic content prodotto

Le email di questo flow NON usano `{{ event.Items.0.product_name }}` perché il trigger è una data property (`Expected Date of Next Order`), non un Placed Order. Klaviyo non espone nativamente "last ordered SKU" come profile property.

**Opzione futura**: popolare una profile property `last_ordered_sku` con un flow ausiliario `Placed Order → Update Profile Property → last_ordered_sku = event.Items.0.SKU`. Questo permetterà di usare `{{ person.last_ordered_sku }}` nel copy. Per ora le email restano generiche ("il tuo percorso", "il tuo prodotto") con CTA verso paleocomplex.com.

### Smart Sending OFF

Coerente con Flow 71. Email retention sono email importanti, no frequency cap.

### Trigger frequency "never" — CRITICO

Klaviyo Academy esplicita: senza `frequency = never` il flow rispedirebbe ogni volta che Klaviyo ricalcola la data ENO (settimanalmente). Questo causerebbe loop infiniti e unsubscribe massivi. **Verificare sempre** che questa impostazione sia attiva.

### Filtro reciproco con Flow 73

Quando configureremo il Flow 73 (At Risk Winback), il suo trigger filter includerà `NOT currently in Flow 72`. Così evitiamo che cliente che ha appena ricevuto la Email 3 Below CLV Lorenzo (con 15% codice) riceva anche subito una Email 1 Flow 73 con altro sconto. Sequenza: Flow 72 → eventualmente Flow 73 dopo che il 72 è terminato (entrata in At Risk segment richiede tempo).

### Schema flow Klaviyo

```
[Expected Date of Next Order]  ← Klaviyo Predictive
    │
    ▼
[Trigger Filter]
  - Lifetime Number of Orders ≥ 2
  - Placed Order zero times since starting flow
  - Has not received Flow 71 in last 365 days
    │
    ▼
[Conditional Split: Predicted CLV ≥ soglia]
    │
    ├── YES (Above CLV)
    │     ▼ immediate
    │     Email 1 Lorenzo (riconoscimento, no sconto)
    │     ▼ wait 7 days [filter: Placed Order zero times]
    │     ▼
    │     Email 2 Lorenzo (suggerimento Renaissance/Sport, no sconto)
    │
    └── NO (Below CLV)
          ▼ immediate
          Email 1 Flaminia (reorder + CONTINUA10K7 10%)
          ▼ wait 7 days [filter]
          ▼
          Email 2 Flaminia (social proof + reminder codice)
          ▼ wait 10 days [filter]
          ▼
          Email 3 Lorenzo (ultima chance + {{ unique_coupon_code }} 15%)
```

### Quando attivare il Flow 72

**Non subito**. Attendi 60-90gg dopo go-live Klaviyo + Flow 71 attivo. Klaviyo ha bisogno di:
- 500+ clienti che hanno fatto un ordine
- 180gg di storico ordini
- Ordini nei 30gg recenti
- Clienti con 3+ ordini per le previsioni personalizzate

Tu hai già tutti questi prerequisiti come dati totali, ma Klaviyo deve avere visto **gli stessi dati DENTRO Klaviyo** per 60-90gg per calcolare Predicted CLV affidabile.

### Status
Bozza v1.0 — pronto per montaggio Klaviyo, ma DA ATTIVARE solo dopo 60-90gg post-migrazione.

### Changelog
- **v2.0 (2026-06-18)**: fix da verifica content-verifier + decisioni Andrea. (1) **Le 3 testimonianze inventate della Email 2 Below sono state sostituite con recensioni REALI dal CSV** (Ornella B. su sospensione/ripresa, Alessia D. su terza confezione, Paola L. su costanza) e rimossa la nota interna "(dal CSV recensioni)". (2) Codice CONTINUA10 → **CONTINUA10K7**, validità 14gg (matematica sequenza ora coerente: E2 a +7gg trova codice ancora valido, E3 a +17gg lo trova scaduto e porta il 15% personale). (3) Rimossa la frase falsa "niente promo periodiche, niente codici riutilizzabili" → "è un codice personale". (4) Promessa di silenzio resa veritiera ("per le prossime settimane... da parte mia"). (5) Rimossi i riferimenti creepy a Klaviyo/predizione data ordine. (6) Fix persona Flaminia ("Ti ho fatto scrivere" → "Flaminia ti ha scritto"). (7) Claim Renaissance prudente ("puoi notare"). (8) Early access ammorbidito ("sarai tra le prime persone a saperlo"). (9) Gender-neutral.
- v1.0 (2026-06-18): prima stesura. Architettura template Klaviyo Academy: trigger Expected Date of Next Order + conditional split Predicted CLV. Above CLV: 2 email Lorenzo, no sconto, focus riconoscimento/community. Below CLV: 3 email Flaminia+Lorenzo, escalation sconto 10%→15%. Coordinamento con Flow 71 (esclusione 365gg) e Flow 73 (esclusione reciproca).
- v1.0 (2026-06-18): prima stesura. Architettura template Klaviyo Academy: trigger Expected Date of Next Order + conditional split Predicted CLV. Above CLV: 2 email Lorenzo, no sconto, focus riconoscimento/community. Below CLV: 3 email Flaminia+Lorenzo, escalation sconto 10%→15%. Coordinamento con Flow 71 (esclusione 365gg) e Flow 73 (esclusione reciproca).
