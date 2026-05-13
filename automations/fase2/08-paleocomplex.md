**Versione:** 0.2
**Ultimo aggiornamento:** 2026-05-13

# Flow 8: Prodotto — Paleocomplex

## Chi entra in questo flow

Persone che hanno acquistato **Paleocomplex** (base, non Revolution) **per la prima volta in assoluto**, indipendentemente dal fatto che sia il primo ordine o un riacquisto. Lo scopo del flow è dare istruzioni, aspettative e social proof specifici del prodotto.

Il flow gira **in parallelo** ai flow di stato cliente (06 Primo Cliente Assoluto / 07 Cliente Ricorrente), che si occupano della relazione brand. Qui parla solo il prodotto.

L'obiettivo del flow è:
- Garantire che il cliente assuma il prodotto correttamente (dosaggio, timing, modalità)
- Calibrare le aspettative sui tempi di risposta (anti buyer's remorse)
- Generare social proof con recensioni verificate di chi ha usato il prodotto
- Costruire la base per un cliente che ricomprerà

## Configurazione Klaviyo

**Trigger:** Placed Order

**Filtro trigger (entrambe le condizioni):**
1. **Items in this event SKU equals** `paleocomplex` (SKU prodotto base, distinto da Revolution e altri)
2. **Placed Order metric** → has happened **zero times** where Item SKU equals `paleocomplex` **over all time before this event**

In pratica: il flow parte se nell'ordine corrente c'è il SKU `paleocomplex` e nessun ordine precedente conteneva quel SKU. Se il cliente ricompra Paleocomplex base, il flow NON riparte (perché già completato in passato).

**Nota tecnica:** trigger basato sullo SKU (non sul match di stringa nel nome prodotto) → evita ambiguità con prodotti che hanno "Paleocomplex" nel nome (es. Paleocomplex Revolution). Stesso pattern verrà applicato a tutti i 14 flow prodotto.

**Effetto su altri flow:**
- Gira in parallelo a 06 Primo Cliente Assoluto (se è il primo ordine in assoluto) o a 07 Cliente Ricorrente (se è ordine ≥ 2)
- Non interferisce con i retention flow per prodotto (timing più avanti)

## Mittenti

| # | Email | Mittente |
|---|-------|----------|
| 1 | Istruzioni | Lorenzo Zarone |
| 2 | Aspettative | Lorenzo Zarone |
| 3 | Social proof + check-in | Flaminia (Customer Care) |

## Timeline

| # | Timing | Tema | Tipo |
|---|--------|------|------|
| 1 | +1gg | Istruzioni assunzione Paleocomplex | Statica |
| 2 | +5gg | Aspettative multivitaminico | Statica |
| 3 | +18gg | Social proof multivitaminici + check-in | Statica |

**Incastro con flow stato cliente** (esempio cliente nuovo, primo ordine in assoluto, che compra solo Paleocomplex):

```
T+2h    [06 Stato]   Benvenuto Lorenzo
T+1gg   [08 Paleo]   Istruzioni Paleocomplex
T+5gg   [08 Paleo]   Aspettative multivitaminico
T+12gg  [06 Stato]   Ottimizza abitudini
T+18gg  [08 Paleo]   Social proof multivitaminici (Flaminia)
T+32gg  [06 Stato]   Recensione brand (Flaminia)
```

Gap minimo tra invii ≥ 2 giorni. Sequenza pulita Lorenzo/Flaminia.

---

## EMAIL 1 — Istruzioni assunzione (+1 giorno)

**Mittente:** Lorenzo Zarone
**Tipo:** Statica

### Oggetto (3 varianti A/B)

- A: Il tuo Paleocomplex è in viaggio. Ecco come usarlo bene.
- B: Le istruzioni per partire con il piede giusto con Paleocomplex
- C: Cinque minuti per fare le cose nel modo corretto

### Preview text (3 varianti)

- A: La cosa più importante è iniziare bene. Te lo spiego in pratica.
- B: Dosaggi, orari, errori da evitare.
- C: Non è complicato. Ma c'è un modo giusto.

### Corpo email

Ciao [NOME]

Il tuo Paleocomplex è in viaggio (se non te l'ha già consegnato il corriere mentre leggi). Prima che lo apri voglio assicurarmi che parti con il piede giusto. Gli integratori funzionano se assunti bene. È un dettaglio che può fare la differenza tra "non sento niente" e "sento la differenza dopo qualche settimana".

**Dosaggio e modalità**

Il tuo Paleocomplex è un multivitaminico in polvere a dose modulabile. Il misurino ha tacche a 2, 3 e 5 ml. La dose consigliata per adulti è di 2 misurini al giorno, riempiti fino alla tacca 5 (10 ml totali). Puoi modulare la quantità in base alle tue esigenze: ogni nutriente scala proporzionalmente alla dose. Per la vitamina D, ad esempio: 2 ml = 2.000 UI, 5 ml = 5.000 UI, 10 ml (2 misurini) = 10.000 UI.

Se hai dubbi su quale dose è adatta a te, scrivici a **ordini@paleocomplex.com**.

**Come prenderlo**

Sciogli la polvere in un bicchiere di acqua fresca o a temperatura ambiente. Mai calda: le vitamine idrosolubili e altri ingredienti si ossidano. Bevi dopo colazione o dopo pranzo, mai a stomaco vuoto: le vitamine liposolubili A, D, E, K hanno bisogno dei grassi del pasto per essere assorbite meglio.

**Una nota sull'odore**

Il prodotto contiene Omega-3 da krill. Può capitare di percepire un leggero odore di pesce all'apertura del barattolo. È normale, sciogliendolo in acqua diventa impercettibile.

**Per dubbi specifici**

Se hai dubbi sul dosaggio o vuoi adattare l'assunzione a una tua condizione (gravidanza, allattamento, patologie, farmaci), scrivici a **ordini@paleocomplex.com**. Per qualunque altra domanda sui prodotti, la pagina **[FAQ del sito](https://paleocomplex.com/faq/)** copre quasi tutti i casi.

**Tra qualche giorno** ti dico cosa aspettarti realisticamente dalle prime settimane di integrazione. Spoiler: non è quello che ti dicono le pubblicità.

Un forte abbraccio
Lorenzo Zarone
Fondatore di Paleocomplex

---

## EMAIL 2 — Aspettative (+5 giorni)

**Mittente:** Lorenzo Zarone
**Tipo:** Statica

### Oggetto (3 varianti A/B)

- A: Cosa aspettarti realisticamente dal tuo Paleocomplex
- B: Gli integratori non funzionano come dicono le pubblicità
- C: I tempi veri dell'integrazione (senza esagerazioni)

### Preview text (3 varianti)

- A: Ti spiego cosa è normale aspettarsi e cosa no.
- B: Niente promesse miracolose. Solo onestà.
- C: La costanza è tutto. Te lo spiego con esempi concreti.

### Corpo email

Ciao [NOME]

A questo punto hai (spero) iniziato il tuo Paleocomplex da qualche giorno. È il momento giusto per parlarti di una cosa importante: cosa aspettarti realisticamente.

Ti chiedo cinque minuti perché questo è il punto in cui la maggior parte delle persone si scoraggia. Iniziano un integratore, dopo 7-10 giorni "non sentono niente" e mollano. È un errore. Ma è anche colpa di come il marketing comunica gli integratori, promettendo risultati immediati quando i meccanismi biologici hanno tempi diversi.

Ti spiego come funzionano davvero le cose, partendo da una premessa onesta: ogni corpo è diverso. Lo stato di partenza, l'assorbimento individuale, lo stile di vita, l'età, eventuali patologie, tutto influisce sui tempi. Quelli che leggi sotto sono i tempi medi, basati su quello che ci raccontano migliaia di clienti.

**Prime 2 settimane**

I primi segnali sono sottili ma reali. Il magnesio può migliorare la qualità del sonno e ridurre i crampi notturni già nei primi giorni. Le vitamine B attivate iniziano a sostenere il metabolismo energetico. Chi aveva carenze importanti può notare una maggiore stabilità dell'umore. È la fase in cui il corpo ricostituisce le scorte di micronutrienti.

**Dopo 1 mese**

I risultati diventano tangibili. L'energia è più costante, meno crolli pomeridiani, meno bisogno di stimolanti. Unghie e capelli iniziano a mostrare miglioramento (biotina, zinco, selenio). Chi fa attività fisica nota un recupero migliore.

**Dopo 2-3 mesi**

È il momento in cui controllare le analisi del sangue ha senso. Vitamina D, ferritina, omocisteina sono i parametri più sensibili (la vitamina D richiede 8-12 settimane per stabilizzarsi). La pelle è più luminosa. Il sistema immunitario è più reattivo. Chi smette nota subito: "mi manca qualcosa".

**Uso continuativo (6+ mesi)**

I benefici strutturali e preventivi si consolidano. Salute cardiovascolare, densità ossea, protezione cellulare. Sono benefici che non "senti" nel quotidiano ma che fanno una differenza enorme negli anni a venire.

**La verità che pochi dicono**

L'integrazione non è una pillola che provi per giudicarla. È un investimento sul tempo. La differenza tra chi vede risultati e chi no è quasi sempre la costanza. **Tre mesi continuativi** è il minimo per giudicare onestamente. Otto-dieci settimane invece sono il punto in cui la maggior parte delle persone abbandona, prima di vedere il vero beneficio.

Se sei a 5 giorni dall'inizio e "non senti niente", è perfettamente normale. Continua. Tra qualche settimana riparliamo.

**Più avanti** Flaminia, una persona del nostro team, ti scriverà per sentire come stai andando. Nel frattempo, se hai domande, scrivici a **ordini@paleocomplex.com**.

Un forte abbraccio
Lorenzo Zarone
Fondatore di Paleocomplex

---

## EMAIL 3 — Social proof + check-in (+18 giorni)

**Mittente:** Flaminia (Customer Care)
**Tipo:** Statica

Recensioni verificate dal CSV `context/20260511 paleocomplex export-reviews.csv` — filtro `product_sku = paleocomplex` (193 recensioni 5 stelle disponibili). Selezionate 3 top per varietà territoriale: vitamina D misurabile + multi-benefit + professionista (Camelo), vitamina D misurabile + costanza 3 mesi + pelle + target 50+ (Pennello), sport + 6 mesi + immune/rinite (Cristina).

### Oggetto (3 varianti A/B)

- A: Come sta andando con il Paleocomplex?
- B: Sono passate quasi tre settimane
- C: Volevo sentirti

### Preview text (3 varianti)

- A: Sono Flaminia, faccio parte del team di Lorenzo. Mi farebbe piacere sapere come va.
- B: Una piccola pausa dalla teoria. Oggi qualche storia vera.
- C: Ho raccolto qualche esperienza che potrebbe interessarti.

### Corpo email

Ciao [NOME]

Ti scrivo io questa volta. Sono Flaminia e mi occupo del rapporto con i clienti di Paleocomplex. Lorenzo si occupa della parte tecnica e scientifica, io invece sono il punto di contatto umano: rispondo a chi ci scrive, ascolto i feedback, raccolgo storie. Ed è proprio per questo che oggi voglio scriverti.

Sono passate circa 2-3 settimane da quando hai iniziato il tuo Paleocomplex. È un momento interessante: alcune persone iniziano a notare qualcosa, altre sono ancora nella fase di pazienza che ti aveva descritto Lorenzo. In entrambi i casi può essere utile leggere le esperienze di chi è passato dallo stesso punto in cui sei tu adesso.

Ti lascio qualche storia vera. Sono tutte recensioni di clienti verificati, ognuna con la sua tempistica e il suo modo di raccontare.

*"Sono uno psicologo, fisioterapista, erborista, laureato in scienze motorie. Molto attento alla salute vera e non come persuasione commerciale. Il prodotto mi ha fornito energia sia nella vita che negli allenamenti, una scomparsa di dolori articolari e di una noiosissima dermatite seborroica. In più i miei livelli di vitamina D sono saliti in poco tempo da 19 a 60."*
**Massimo Camelo**

*"Dopo 3 mesi di integrazione una sensazione di benessere in tutte le attività svolte, sportive e non. La vitamina D da 17 a 35 purtroppo senza sole. Ma il risultato che mi ha sorpreso di più è l'effetto positivo che ho riscontrato sulla pelle in tutte le parti del corpo, e non sono giovanissimo (classe 1963). Consiglio a tutti questo integratore veramente completo."*
**Nello Pennello**

*"Sono già al sesto mese di assunzione e devo confermare le straordinarie proprietà del prodotto. Pratico ciclismo almeno tre volte la settimana e Paleocomplex mi fa sentire sempre energico e con una grande vitalità. Solitamente nel periodo tra maggio e giugno soffrivo di rinite allergica in maniera insopportabile e invece quest'anno solo piccoli fastidi. Promosso a pieni voti."*
**Cristina**

I risultati sono personali, dipendono dalle condizioni di partenza e dallo stile di vita. Se col solo Paleocomplex non raggiungi livelli ottimali di vitamina D (sopra i 40 ng/ml), il consiglio non è raddoppiare la dose ma aggiungere le **[gocce di Vitamina D](https://paleocomplex.com/prodotto/vitamina-d/)**: 4 gocce al giorno coprono la maggior parte dei casi.

**Una cosa importante**: queste sono storie di persone reali, ma non sono "garanzie". Ogni corpo risponde a tempi suoi. Se a questo punto non stai notando ancora cambiamenti, non significa che il prodotto non stia funzionando: significa solo che il tuo corpo ha bisogno di più tempo per riempire le riserve. Continua.

E se invece hai già notato qualcosa, mi farebbe davvero piacere saperlo. **Rispondi pure a questa email** raccontandomi com'è andata: per me è il modo migliore di lavorare, sapendo cosa cambia davvero nella vita delle persone che ci scelgono.

Flaminia
Customer Care Paleocomplex

---

## Note operative

### CTA per email
- Email 1: nessuna CTA esplicita (solo ordini@paleocomplex.com per dubbi) + link inline a FAQ
- Email 2: nessuna CTA esplicita (solo ordini@paleocomplex.com)
- Email 3: invito a rispondere alla mail + link inline a Vitamina D in gocce per chi non raggiunge livelli ottimali

### Open loop interni al flow
- Email 1 → 2: "Tra qualche giorno ti dico cosa aspettarti realisticamente"
- Email 2 → 3: "Più avanti Flaminia ti scriverà per sentire come stai andando"

### Coordinamento con flow paralleli
- Se cliente è nuovo (primo ordine), riceve in parallelo flow 06 (benvenuto Lorenzo +2h, ottimizza +12gg, recensione +32gg)
- Se cliente è ricorrente (ordine ≥ 2, primo acquisto Paleocomplex), riceve in parallelo flow 07 (grazie Lorenzo +2h, cross-sell Flaminia +3gg)
- Email 3 di questo flow (Flaminia, +18gg) si distanzia di 14 giorni dall'email cross-sell del flow 07: gap sufficiente per non sovrapporsi
- Email 3 di questo flow (+18gg) si distanzia di 14 giorni dall'email recensione del flow 06 (+32gg): gap sufficiente

### Status
Bozza v0.2 — in attesa review Andrea. Una volta validato, lo userò come template per i flow 09-21 (gli altri 13 prodotti).

### Changelog
- v0.2 (2026-05-13): trigger basato su SKU `paleocomplex` invece di match stringa + 3 recensioni Paleocomplex puro selezionate dal CSV (Camelo, Pennello, Cristina) invece di recensioni famiglia multivit.
- v0.1 (2026-05-13): bozza iniziale, estratta dai blocchi del flow 06 (istruzioni Paleocomplex + aspettative multivit + social proof multivit).
