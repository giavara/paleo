**Versione:** 3.0
**Ultimo aggiornamento:** 2026-06-18

# Flow 71: First-Order Reorder Reminder

## Chi entra in questo flow

Clienti al **primo ordine in assoluto** (`Customer's Lifetime Number of Orders = 1`), per ricordare il riacquisto al momento giusto in base alla durata pack del prodotto principale ordinato.

Il flow gira **in parallelo** ai flow Fase 2 post-acquisto (21 Primo Cliente, 24-37 Flow prodotto, 23 Recensione Brand) e coordina i suoi timing per non sovrapporsi.

L'obiettivo è **portare il primo cliente al secondo acquisto** prima che Klaviyo Predictive (Flow 72) abbia abbastanza dati per intervenire. Il primo riacquisto è il momento di churn più alto.

## Razionale architetturale

**Perché un flow timing-based e non Predictive**: Klaviyo Predictive Analytics richiede 3+ ordini per dare previsioni personalizzate affidabili (con 1-2 ordini restituisce la mediana store, meno utile). Per il primo cliente bisogna usare time delay fissi basati sulla durata reale del pack, come Klaviyo stessa raccomanda per cataloghi con cicli ben definiti (fonte: help.klaviyo.com/360020919731).

**Perché 3 rami semplificati** (non 14, non 6): Andrea ha scelto di accorpare per blocchi di durata approssimata (~30gg / ~60gg / Vit D). Manutenzione 5-6× più semplice rispetto al granulare per ogni durata reale. Compromesso accettato: alcune email arrivano qualche giorno prima/dopo il punto ottimale.

## Configurazione Klaviyo

**Trigger:** Fulfilled Order (Order Completed in WooCommerce)

**Trigger filter (entrambe le condizioni):**
1. `Customer's Lifetime Number of Orders equals 1` — solo primo ordine assoluto
2. `Items contains at least one supplement` (esclude ordini accessori-only)

**Filtro accessori:**
- L'ordine deve contenere almeno un SKU della linea integratori
- Se l'ordine contiene SOLO accessori (Lampada Apollo, occhiali, libri), il flow NON parte

**Smart Sending:** OFF

**Re-entry:** Non applicabile (filtro Lifetime Orders = 1 lo previene)

**Flow filter trasversale ad ogni email:**
- `Placed Order zero times since starting this flow with Items contains [SKU famiglia del trigger]` — il cliente esce subito appena ricompra

## Conditional Split: 3 rami per durata pack (semplificato)

Lo split valuta `event.Items.0.SKU` e dirotta su uno dei 3 rami.

| Ramo | Durata approssimata | SKU inclusi | Email 1 | Email 2 |
|------|---------------------|-------------|---------|---------|
| **A** ~30gg | paleocomplex, paleocomplex-revo, elisir, elisir-basic, youth, testo-plus, renaissance, hurricane, armageddon (**9 SKU**) | ~30gg | T+25 Flaminia | T+30 Lorenzo |
| **B** ~60gg | jeunesse, essentiel, liverty, artosan (**4 SKU**) | ~60gg | T+50 Flaminia | T+58 Lorenzo |
| **C** Vit D | vitamina-d | 150gg | T+120 Lorenzo unica | — |

### Compromessi accettati con questa semplificazione

| SKU | Durata reale pack | Ramo | Reminder Email 1 arriva | Risultato |
|-----|-------------------|------|-------------------------|-----------|
| Paleocomplex, Revolution, Youth, Testoplus, Renaissance | 30gg | A | T+25 | 5gg prima fine pack ✅ |
| Elisir, Elisir Basic | 40gg | A | T+25 | ~15gg prima fine pack ⚠️ (sensibilizza in anticipo) |
| Hurricane, Armageddon | ~30 dosi variabile | A | T+25 | dipende da frequenza allenamenti |
| Jeunesse | 50gg | B | T+50 | ~stesso giorno fine pack ✅ |
| Essentiel | 60gg | B | T+50 | 10gg prima fine pack ✅ |
| Liverty, Artosan | 60gg (mantenimento) | B | T+50 | 10gg prima fine pack ✅ |
| Vitamina D | 150gg | C | T+120 | 30gg prima fine flaconcino ✅ |

## Mittenti per ramo

| Ramo | Email 1 | Email 2 |
|------|---------|---------|
| A ~30gg | Flaminia | Lorenzo |
| B ~60gg | Flaminia | Lorenzo |
| C Vit D | (singola Lorenzo) | — |

**Pattern**: Email 1 sempre Flaminia (soft, umana, anticipa la fine del pack). Email 2 sempre Lorenzo (più diretta, push al riacquisto con autorevolezza). Eccezione Vit D: singola email diretta Lorenzo.

**Niente sconti in nessuna email.** Lo sconto vive solo nei Flow 72 (Below-CLV) e 73 (At Risk Winback). Coerente con la filosofia "selective discounting" del playbook Klaviyo.

## Coordinamento con flow Fase 2 (esempio Ramo A)

```
T+2h    Placed     [21]  Benvenuto Lorenzo
T+0     Fulfilled  [24]  Istruzioni prodotto Lorenzo
T+4     Fulfilled  [24]  Aspettative Lorenzo
T+11    Fulfilled  [21]  Ottimizza abitudini Lorenzo
T+17    Fulfilled  [24]  Social proof Flaminia
T+25    Fulfilled  [71]  Email 1 Reorder Flaminia ⭐ NUOVO
T+30    Fulfilled  [71]  Email 2 Reorder Lorenzo ⭐ NUOVO
T+32    Fulfilled  [23]  Anticipo recensione Flaminia
T+34    Fulfilled  [WC]  Email automatica ⭐⭐⭐⭐⭐
```

Gap minimo 2gg tra Email 2 (Lorenzo) e Recensione brand (Flaminia). Pulito.

Per Ramo B (~60gg) e Ramo C (Vit D, T+120): timing distanti, nessun conflitto.

---

## RAMO A — Pack ~30 giorni (9 SKU)

Copre tutti i prodotti con pack che si esauriscono in circa un mese (multivit base, collagene Youth, prodotti specifici a dosaggio acuto, sport).

### Email 1 — Flaminia (+25 giorni dal Fulfilled)

**Mittente:** Flaminia (Customer Care)
**Tipo:** Statica con dynamic content sul `event.Items.0.product_name`

#### Oggetto (3 varianti A/B)

- A: Tra qualche giorno finirai il tuo {{ event.Items.0.product_name }}
- B: Una piccola nota sul tuo pack
- C: Volevo dirti una cosa importante

#### Preview text (3 varianti)

- A: La costanza è tutto. Te lo ricordo io.
- B: Per non interrompere il percorso che hai iniziato.
- C: Sto pensando a te in queste settimane.

#### Corpo email

Ciao [NOME]

Sono Flaminia. Ti scrivo perché ho fatto due conti: il tuo {{ event.Items.0.product_name }} sta arrivando alla fine.

Sei al giorno 25 dalla spedizione e il tuo pack si sta avvicinando alla fine.

Ti scrivo adesso, non quando sarà finito, perché ho imparato una cosa lavorando con i nostri clienti: **il vero risultato sta nella costanza**. Le interruzioni, anche brevi, rallentano il percorso che hai costruito nel primo mese.

E il primo mese è importante. È la fase in cui il corpo comincia a rispondere davvero al supporto che gli stai dando, qualunque sia il prodotto che hai scelto. Saltarlo significa ricominciare da capo.

Se hai dubbi su come va, su quale dosaggio scegliere, o vuoi parlarne direttamente con Lorenzo, **rispondi pure a questa email**. Leggo io e ti rispondo personalmente.

Tra qualche giorno Lorenzo ti scriverà con il link diretto per riordinare senza fatica. Nel frattempo, se vuoi anticipare, puoi farlo direttamente dal **[nostro sito](https://paleocomplex.com)**.

A presto
Flaminia
Customer Care Paleocomplex

---

### Email 2 — Lorenzo (+30 giorni dal Fulfilled, 5gg dopo Email 1)

**Mittente:** Lorenzo Zarone

#### Oggetto (3 varianti A/B)

- A: Il tuo {{ event.Items.0.product_name }} è finito (o quasi)
- B: Non lasciare un buco nel tuo percorso
- C: Da qui in poi è solo costanza

#### Preview text (3 varianti)

- A: 30 secondi per riordinare e continuare.
- B: La cosa più importante è non saltare.
- C: La differenza tra chi vede risultati e chi no.

#### Corpo email

Ciao [NOME]

Sono Lorenzo. Flaminia mi ha detto che ti ha scritto qualche giorno fa. Ti scrivo io adesso perché è il momento giusto.

A questo punto il tuo {{ event.Items.0.product_name }} è finito, o stai per finirlo. Ho due cose da dirti.

**La prima**: hai fatto bene a iniziare. Il primo mese di integrazione vera non è semplice. Ti dà il tempo di capire come reagisce il tuo corpo, di abituarti al sapore o alla modalità d'uso, di vedere i primi segnali. Arrivare fin qui è già un risultato.

**La seconda**: adesso viene la parte che separa chi vede davvero la differenza da chi no. È la **costanza**.

Te lo dico in modo diretto perché è quello che dico a chiunque mi scriva: gli integratori veri non funzionano come un farmaco che provi per 30 giorni e poi giudichi. Funzionano come un investimento sul tempo. Tre mesi continuativi è il minimo per giudicare onestamente. Dal quarto mese in poi cominciano a consolidarsi i benefici strutturali, quelli che fanno la differenza negli anni.

Se hai dubbi sul dosaggio, sul prodotto giusto per te, o vuoi confrontarti con noi su qualcosa, **rispondi a questa email**: la leggiamo io e il mio team, e ti rispondiamo.

Se invece sei convinto e vuoi continuare:

**[Riordina il tuo {{ event.Items.0.product_name }}](https://paleocomplex.com/prodotto/{{ event.Items.0.product_slug }})**

Spedizione veloce come sempre, 24-48h con corriere espresso.

Un forte abbraccio
Lorenzo Zarone
Fondatore di Paleocomplex

---

## RAMO B — Pack ~60 giorni (4 SKU)

Copre i prodotti con pack a durata doppia (Jeunesse collagene grass-fed, Essentiel multivit no-krill, Liverty supporto epatico mantenimento, Artosan articolazioni mantenimento).

### Email 1 — Flaminia (+50 giorni dal Fulfilled)

**Mittente:** Flaminia (Customer Care)

#### Oggetto (3 varianti A/B)

- A: A che punto siamo con il tuo {{ event.Items.0.product_name }}?
- B: Sono passate quasi 8 settimane
- C: Volevo sentire come va

#### Preview text (3 varianti)

- A: Il pack sta arrivando alla fine, ti scrivo per ricordarti.
- B: Due mesi di percorso. Adesso siamo al momento giusto.
- C: La cosa più importante adesso è non interrompere.

#### Corpo email

Ciao [NOME]

Sono Flaminia. Ti scrivo perché sei al giorno 50 dalla spedizione del tuo {{ event.Items.0.product_name }}.

Il pack che hai ordinato si sta avvicinando alla fine.

Volevo scriverti adesso, e non alla fine, perché su questi prodotti la costanza vale ancora di più. Lavorano su strutture che richiedono settimane di lavoro continuo per consolidare i risultati (collagene, supporto epatico, articolazioni, sistema nutritivo profondo a seconda di quello che hai scelto).

Le pause lunghe rallentano il consolidamento dei risultati su cui hai già lavorato.

A questo punto del percorso può essere che tu abbia notato i primi cambiamenti (pelle più compatta, articolazioni migliorate, energia più costante a seconda del prodotto), oppure che stia ancora aspettando. In entrambi i casi: continua.

Se hai dubbi o vuoi confrontarti con noi, **rispondi a questa email**. Leggo io e ti rispondo personalmente.

Tra qualche giorno Lorenzo ti scriverà con il link per riordinare.

A presto
Flaminia
Customer Care Paleocomplex

---

### Email 2 — Lorenzo (+58 giorni dal Fulfilled, 8gg dopo Email 1)

**Mittente:** Lorenzo Zarone

#### Oggetto (3 varianti A/B)

- A: Il tuo {{ event.Items.0.product_name }} è finito
- B: Due mesi di percorso. Adesso la scelta è tua.
- C: Continuare o smettere: perché conta

#### Preview text (3 varianti)

- A: Il momento in cui la maggior parte molla. Non sei tu, vero?
- B: Il vero risultato sta in cosa fai adesso.
- C: 30 secondi per riordinare e continuare.

#### Corpo email

Ciao [NOME]

Sono Lorenzo. Il tuo primo pack di {{ event.Items.0.product_name }} è agli sgoccioli. Te lo dico onestamente: adesso viene il bivio.

Su prodotti come questo, che lavorano su rigenerazione strutturale, supporto profondo a organi o sistemi specifici, la maggior parte delle persone abbandona dopo i primi 60 giorni perché "non ha ancora visto la differenza". È un errore di tempistica.

I primi due mesi servono per costruire le basi. Ed è di solito dal terzo mese che i benefici cominciano a consolidarsi e a farsi notare. Chi smette ora ha messo le basi senza godersi la casa che ha costruito.

Te lo dico perché ci ho visto troppi clienti smettere a metà strada e poi ricominciare da capo sei mesi dopo. Non è efficiente, e soprattutto, hai investito tempo che ora rischi di buttare via.

Se vuoi confrontarti su come prosegui (dosaggio, eventuali combinazioni, dubbi sul prodotto), **rispondi a questa email**.

Se invece sei convinto e vuoi continuare:

**[Riordina il tuo {{ event.Items.0.product_name }}](https://paleocomplex.com/prodotto/{{ event.Items.0.product_slug }})**

Un forte abbraccio
Lorenzo Zarone
Fondatore di Paleocomplex

---

## RAMO C — Vitamina D (singola email a T+120)

Solo per la Vitamina D in gocce, durata pack 150 giorni circa (5 mesi a 4 gocce/giorno).

### Email unica — Lorenzo (+120 giorni dal Fulfilled)

**Mittente:** Lorenzo Zarone

#### Oggetto (3 varianti A/B)

- A: La tua Vitamina D sta finendo
- B: 4 mesi di Vitamina D. Adesso un controllo.
- C: Tre cose veloci sulla tua integrazione

#### Preview text (3 varianti)

- A: È il momento di valutare i livelli e riordinare.
- B: Se hai fatto le analisi, mi fa piacere saperlo.
- C: La vitamina D è uno dei pochi integratori misurabili davvero.

#### Corpo email

Ciao [NOME]

Sono Lorenzo. Sei al giorno 120 dalla spedizione della tua Vitamina D in gocce.

Il flaconcino dovrebbe essere a circa l'80% di utilizzo. Hai ancora qualche settimana di prodotto, ma è il momento giusto per due cose: il controllo dei valori e il pensiero al riordino.

Ti scrivo per tre motivi:

**1. Se non l'hai ancora fatto, fai le analisi della 25(OH)D adesso.** È il momento giusto: dopo 4 mesi di supplementazione i valori si sono stabilizzati. Hai un quadro reale di come la tua dose sta funzionando. Il range ottimale è 40-60 ng/ml.

**2. Se hai fatto le analisi, mi farebbe piacere conoscere i tuoi valori prima/dopo.** Rispondi pure a questa email con i numeri (anche solo "ero a X, adesso sono a Y"). Sono i dati che ci aiutano a costruire un quadro reale.

**3. Per il riacquisto**, la Vitamina D è una supplementazione di lungo periodo, specialmente da ottobre a marzo quando in Italia il sole non basta. Se vuoi assicurarti di avere il flaconcino di scorta:

**[Riordina la tua Vitamina D in gocce](https://paleocomplex.com/prodotto/vitamina-d/)**

Una nota: se le analisi dovessero dirti che sei in carenza marcata, scrivimi prima di riordinare. Possiamo ragionare insieme sul dosaggio.

Un forte abbraccio
Lorenzo Zarone
Fondatore di Paleocomplex

---

## Note operative

### Dynamic content e variabili Klaviyo

Tutto il copy usa `{{ event.Items.0.product_name }}` per riferirsi al prodotto del primo ordine, e `{{ event.Items.0.product_slug }}` per costruire il link al prodotto. Questo funziona perché il flow è triggered su Fulfilled Order, quindi le proprietà dell'evento sono direttamente disponibili.

Nei rami che includono prodotti diversi, la variabile si compila automaticamente con il nome specifico. Una sola email per ramo gestisce tutti gli SKU senza riscrittura.

**Verifica setup Klaviyo:** confermare che WooCommerce passi correttamente `product_name` e un `product_slug` (o sostituibile con `product_url` o `product_id`) negli items dell'evento Placed Order.

### Filtro Flow Filter durante il flow

Su ogni time delay deve essere impostato il filtro:

```
Placed Order zero times since starting this flow 
  where Items contains [trigger_SKU]
```

Cioè: se il cliente ha già riordinato lo stesso SKU del trigger, esce automaticamente. Pattern Klaviyo ufficiale.

### Niente sconto in nessuna email

Decisione strategica:
- Il primo cliente non va abituato allo sconto. Se diamo sconto al primo reorder, il cliente impara che basta aspettare per avere il prezzo migliore
- Lo sconto vive in Flow 72 (Below-CLV branch) per chi è ricorrente ma sotto-media + Flow 73 (Churn Risk Winback)
- Il framing nelle email è sulla **costanza** e sul **valore del percorso**, non sul prezzo

### Cosa NON c'è e perché

- **No check-in puramente emotivo**: già coperto da Flaminia in Fase 2 Email 3 Social proof a T+17 dal Fulfilled
- **No cross-sell**: già coperto da Flow 22 (Cliente Ricorrente Cross-sell) quando il cliente farà il 2° ordine
- **No richiesta recensione**: già coperto da Flow 23 a T+32 dal Fulfilled

### Schema flow Klaviyo

```
[Fulfilled Order]
    │
    ▼
[Trigger Filter]
  - Customer's Lifetime Number of Orders = 1
  - Items contains supplement
    │
    ▼
[Conditional Split su event.Items.0.SKU]
    │
    ├── Ramo A (~30gg, 9 SKU)
    │     ▼ wait 25 days
    │     [Filter: Placed Order zero times with same SKU since flow start]
    │     ▼
    │     Email 1 Flaminia
    │     ▼ wait 5 days → Email 2 Lorenzo
    │
    ├── Ramo B (~60gg, 4 SKU)
    │     ▼ wait 50 days → Email 1 Flaminia → wait 8 days → Email 2 Lorenzo
    │
    └── Ramo C (Vit D)
          ▼ wait 120 days → Email unica Lorenzo
```

### Smart Sending OFF
Email retention sono email importanti. Lo Smart Sending serve su broadcast/newsletter per evitare burst. Qui no.

### Coordinamento WooCommerce metric mapping
Verificare in Klaviyo Account Settings → Integrations → WooCommerce → Metric Mapping che gli SKU vengano passati correttamente nel campo `Items.SKU` dell'evento Placed Order. Se i SKU non sono mappati bene, il Conditional Split non funziona.

### Status
**MONTATO COME DRAFT IN KLAVIYO via API il 2026-06-18.** Flow ID `Xi3wcm`, status `draft` (inerte, nessuno entra finche' non viene attivato a mano nel builder). 5 template HTML creati via API (ID: A1 VS2Uev, A2 TszY7p, B1 WqqGvJ, B2 TmWHKZ, C1 QWvMCT). Da rivedere e rifinire nel builder prima di attivare.

#### Differenze tra il design su carta e quanto montato via API
1. **Split prodotto:** il `multi-branch-split` su SKU NON e' creabile via Create Flow API (bug lato Klaviyo, ritorna 500). Sostituito con **3 conditional-split annidati** che instradano per `ProductName` (lista nomi prodotto per ramo, non SKU). Ramo A se ProductName in [9 nomi], altrimenti check Ramo B [4 nomi], altrimenti Ramo C [Vitamina D], altrimenti esce (accessori/bundle/libri).
2. **Filtro primo ordine + uscita al riacquisto:** invece del flow-filter per-delay "Placed Order zero times same SKU", si usa un unico `profile_filter` di flusso **"Placed Order count == 1 (alltime)"**, applicato a ogni azione. Fa entrambe le cose: entra solo al primo ordine assoluto, ed esce automaticamente appena il cliente fa il 2o ordine (count diventa 2). Piu' semplice e robusto; esce su QUALSIASI riacquisto, non solo lo stesso SKU.
3. **Variabile dynamic content:** il copy usava `{{ event.Items.0.product_name }}` / `product_slug`, che **non esistono** nello schema reale degli eventi Paleo. Variabile corretta verificata sugli eventi reali: **`{{ event.ProductNames.0 }}`** (lista piatta top-level). Il `product_slug` per il deep-link al prodotto non ha equivalente piatto (lo SKU/URL sta annidato in `$extra.Items[]`): nei template il CTA "Riordina" punta a `https://paleocomplex.com` (homepage) — da sostituire nel builder con deep-link o blocco prodotto dinamico.

#### Cosa resta da fare a mano nel builder (Andrea)
- **Mittenti:** l'API ha forzato il sender di default dell'account ("Paleocomplex") su tutte le email. Impostare **Flaminia** (Email 1 di ogni ramo) e **Lorenzo Zarone** (Email 2 + Vit D) come from name/email reali.
- **A/B subject + preview:** montata solo la **variante A**. Aggiungere varianti B/C (gia' scritte sopra) come A/B test nel builder.
- **Deep-link riordino:** sostituire l'href homepage con il link prodotto / blocco dinamico.
- **Verificare il routing prodotto:** confermare che il filtro `profile-metric` su property `ProductName` matchi correttamente i nomi (i 3 conditional-split).
- **Prerequisito SKU/metric mapping:** non bloccante per questo design (si instrada su ProductName, gia' presente negli eventi), ma resta da disabilitare le email carrello native WooCommerce ecc. come da memoria.

### Changelog
- **v3.0 (2026-06-18)**: fix da verifica content-verifier (report 4 agenti + review Andrea). (1) Range 25(OH)D corretto da 50-80 a **40-60 ng/ml** (scheda prodotto, citazione Lorenzo). (2) Rimossi i claim di durata pack falsi per parte del ramo ("circa un mese" non regge per Elisir/EB 40gg; "circa due mesi" non regge per Jeunesse 50gg) → claim neutro "si sta avvicinando alla fine". (3) Ammorbiditi claim scientifici esagerati (interruzione 1 settimana, 15 giorni = settimane indietro, "saturare il sistema"). (4) Fix grammatica ("sta per finirlo") e gender-neutral ("Sei arrivato" ecc.). (5) "Leggo io personalmente" → "la leggiamo io e il mio team" (Lorenzo).
- **v2.2 (2026-06-18)**: montato come Draft in Klaviyo via Create Flow API (flow ID `Xi3wcm`). Documentate le 3 differenze design-vs-implementazione (split su ProductName via conditional-split annidati invece di multi-branch su SKU; filtro primo-ordine via profile_filter Placed Order=1; variabile reale `event.ProductNames.0`) e i to-do manuali nel builder (mittenti, A/B, deep-link).
- **v2.1 (2026-06-18)**: semplificazione drastica della ramificazione su decisione di Andrea. Da 6 rami granulari a **3 rami per blocchi di durata approssimata**:
  - Ramo A ~30gg: 9 SKU (Paleo/Rev/Elisir/EB/Youth/Testoplus/Renaissance/Hurricane/Armageddon)
  - Ramo B ~60gg: 4 SKU (Jeunesse/Essentiel/Liverty/Artosan)
  - Ramo C: Vit D dedicato (T+120)
  - Compromessi accettati: Elisir/EB ricevono reminder ~15gg in anticipo (sensibilizzazione, ok); Jeunesse ~stesso giorno fine pack (ottimo).
  - Copy email riformulato in modo generico (rimossi riferimenti specifici a "vitamine B", "magnesio", "collagene") usando il dynamic content `{{ event.Items.0.product_name }}` per nominare il prodotto. Una sola email per ramo gestisce 9 o 4 SKU diversi.
- v2.0 (2026-06-18): refactor con 6 rami su durate pack reali verificate sulle schede prodotto. Superato dalla v2.1.
- v1.x (2026-06-18): prime stesure con 5 rami per "famiglia merceologica". Errore di base sulle durate pack — verificato successivamente.
