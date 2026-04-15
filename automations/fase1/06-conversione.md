**Versione:** 1.1
**Ultimo aggiornamento:** 2026-04-10
**Status:** Bozza v1 — in attesa review Andrea

# Flow 6: Conversione

## Chi entra in questo flow

Persone che hanno completato Welcome + Authority **senza acquistare**. Sono in lista da circa 26 giorni.

Conoscono già:
- Chi è Lorenzo e la storia del brand (welcome email 3)
- Perché i dosaggi simbolici non funzionano (welcome email 2)
- I prodotti principali e i prezzi (welcome email 4-5)
- Le carenze nutrizionali, la vitamina D e i cofattori, la metilazione (authority)

**Perché non hanno comprato (ipotesi basate su dati sondaggio ex-clienti):**
- Non ancora convinti della qualità/efficacia (servono più prove)
- Il prezzo li frena (serve più percezione di valore)
- Non sentono urgenza (serve far percepire il costo dell'inazione)
- Si fidano ma rimandano (serve un trigger per agire)

**Obiettivo del flow:** portare alla prima conversione in 32 giorni, toccando i pilastri: scienza, filosofia, sicurezza, brand, authority, social proof, stile di vita, obiezione prezzo.

**Dopo questo flow:** chi non ha comprato entra nel nurturing broadcast (newsletter settimanale).

**Timeline totale percorso automatico:** Welcome (12gg) + Authority (14gg) + Conversione (32gg) = **~58 giorni**

## Struttura email

Ogni email è pensata per blocchi (per il layout HTML futuro):

```
[BLOCCO CORPO] — contenuto principale
[BLOCCO PRODOTTO] — opzionale, prodotto con immagine + breve testo (quando rilevante)
[BLOCCO REVIEW] — 1-2 recensioni reali tematicamente legate al contenuto sopra
[P.S.] — CTA morbida verso guida-scelta
```

## Configurazione Klaviyo

**Trigger:** Completamento Authority Flow (flow 4) + non ha acquistato
**Mittente:** Lorenzo Zarone (tutte le email)
**Filtri profilo:**
- Has Placed Order zero times over all time
- Has completed Authority flow

**Uscita dal flow:**
- Se acquista durante il flow → esce e entra nel Post Purchase New Customer
- Se completa senza acquistare → entra nel nurturing newsletter (campaign settimanali)

**Sconto finale:** codice PRIMOPASSO (€10 + spedizione gratuita, solo primo ordine). Diverso dal BENVENUTO per coerenza: il BENVENUTO è "andato", questo è un nuovo incentivo per chi ha dimostrato interesse restando in lista 58 giorni.

---

## EMAIL 1 — Omega 3: perché in polvere e non in capsule (+2 giorni)

### Oggetto (3 varianti A/B)

- A: Omega 3 in polvere? Sì, e ti spiego perché
- B: Il problema delle capsule di omega 3 che nessuno ti dice
- C: Perché abbiamo messo gli omega 3 in polvere (non siamo pazzi)

### Preview text (3 varianti)

- A: Krill vs olio di pesce: non è la stessa cosa.
- B: La forma conta più della quantità.
- C: Biodisponibilità, rancidità e sinergia: i 3 motivi.

### Corpo email

Ciao [NOME]

Se hai mai preso omega 3, probabilmente erano capsule di olio di pesce. È la forma più diffusa. Ma non è la migliore.

Il primo problema è la biodisponibilità. Gli omega 3 da olio di pesce sono in forma trigliceride. Quelli da krill sono in forma fosfolipidica: la stessa forma in cui si trovano nelle membrane cellulari del tuo corpo. Il risultato? Il krill viene assorbito in modo più efficiente, a parità di dosaggio.

Il secondo problema è la rancidità. L'olio chiuso in una capsula è esposto all'ossidazione nel tempo. Un omega 3 ossidato non solo è inutile, ma può essere dannoso. Con la polvere questo problema non esiste.

Il terzo problema è la sinergia. Una capsula di omega 3 è un prodotto singolo. Io sono e sarò per sempre per la sinergia: non amo i prodotti singoli, li trovo obsoleti. Gli omega 3 lavorano meglio quando sono affiancati da vitamina E (che li protegge dall'ossidazione), vitamina D, magnesio e zinco. Prenderli separati significa sperare che tutto funzioni insieme. Prenderli nella stessa formula significa averne la certezza.

Per questo nei nostri multivitaminici trovi omega 3 da krill in polvere, insieme a tutti i cofattori che ne massimizzano l'efficacia.

**[BLOCCO REVIEW]**

**"Eccezionale! Sono già al sesto mese di assunzione. Pratico ciclismo almeno tre volte la settimana e Paleocomplex mi fa sentire sempre energico e con una grande vitalità. Anche il sapore è piacevole e gli omega 3 presenti risultano ben digeribili."** Cristina

**"Già dopo 3 settimane, miglioramenti visibili sulla mia condizione generale di salute. Ho più energia, dormo meglio."** Raimondo B.

Un forte abbraccio
Lorenzo Zarone
Fondatore di Paleocomplex

P.S. Se vuoi capire quale dei nostri multivitaminici è il più adatto a te: **[Vai alla guida alla scelta](https://paleocomplex.com/guida-scelta)**

---

## EMAIL 2 — Storie di scettici convertiti (+5 giorni)

### Oggetto (3 varianti A/B)

- A: "Ero scettica. Mi sono dovuta ricredere."
- B: 3 persone che non ci credevano (e cosa è successo)
- C: Le storie che ci emozionano di più

### Preview text (3 varianti)

- A: Esperienze reali di chi ha provato con zero aspettative.
- B: Scettici, titubanti, delusi da altri prodotti. Poi hanno provato.
- C: Non le abbiamo scritte noi. Le hanno scritte loro.

### Corpo email

Ciao [NOME]

Non ti chiedo di fidarti delle mie parole. Ti chiedo di leggere quelle di chi era scettico quanto te, se non di più.

**Ramy** aveva provato di tutto e non credeva in un unico integratore:

"Inizialmente ero parecchio titubante sull'efficacia di un unico integratore che raggruppasse praticamente tutti gli elementi di cui necessito. Ad oggi, dopo circa due settimane, posso parlare con un minimo di cognizione di causa. Sento già una maggiore concentrazione, meno irritabilità, più energie. Ma più di tutto la soddisfazione la riscontro sulla mia capacità di affrontare il problema stress con l'apporto nutrizionale a 360 gradi."

**Michela** convive con la fibromialgia e aveva già provato diversi integratori senza risultati:

"Ero molto scettica, in quanto già assumevo diversi integratori e non avevo riscontrato nessun beneficio. Ogni notte venivo svegliata da dei dolori allucinanti alle gambe. Dopo 4 mesi di integrazione, i miei dolori sono fortemente diminuiti, soprattutto quelli notturni. Chi avesse dei dubbi nell'acquistarlo, vi dico semplicemente di provarlo."

**Alessandra** non ci credeva e ha coinvolto anche sua madre:

"Mi è stato consigliato da un'amica e scetticamente ho iniziato ad usarlo. Già dopo una decina di giorni ho iniziato ad avere più energia e voglia di fare. La vitamina D solitamente la assumevo tramite il D-base, ma avendola a zero non riuscivo mai ad averla alta. Ora con un'unica soluzione ho risolto."

Queste sono persone reali. Non le abbiamo selezionate perché dicono cose belle. Le abbiamo selezionate perché partivano esattamente da dove sei tu adesso.

**Nella prossima email** voglio fare una cosa diversa. Smettere per un attimo di parlarti di integratori e dirti le 5 cose che puoi fare da oggi, senza comprare nulla, per stare meglio. Perché l'integrazione funziona solo se le basi sono in ordine. E le basi sono più semplici di quanto pensi.

Un forte abbraccio
Lorenzo Zarone
Fondatore di Paleocomplex

P.S. Se sei pronto a provare anche tu: **[Vai alla guida alla scelta](https://paleocomplex.com/guida-scelta)**

---

## EMAIL 3 — Alimentazione e stile di vita: cosa puoi fare da subito (+9 giorni)

### Oggetto (3 varianti A/B)

- A: 5 cose che puoi fare oggi per stare meglio (senza comprare nulla)
- B: Prima degli integratori, parti da qui
- C: La base che nessun integratore può sostituire

### Preview text (3 varianti)

- A: Alimentazione, sonno, sole: i fondamentali.
- B: L'integrazione funziona solo se il resto è a posto.
- C: Consigli pratici che non ti costano nulla.

### Corpo email

Ciao [NOME]

Oggi non ti parlo di integratori. Ti parlo di quello che viene prima.

L'integrazione funziona solo se hai le basi in ordine. Nessun multivitaminico al mondo può compensare un'alimentazione sbagliata, un sonno insufficiente e una vita sedentaria.

Ecco 5 cose concrete che puoi fare da subito.

**Mangia più pesce azzurro.** Sardine, sgombro, acciughe, aringhe. Sono la fonte naturale più ricca di omega 3 EPA e DHA. Due porzioni a settimana fanno già la differenza per il rapporto omega-6/omega-3.

**Esponiti al sole quando puoi.** Da aprile a settembre, 15-20 minuti al giorno con braccia e gambe scoperte. Il tuo corpo produce circa 15.000 UI di vitamina D in quel tempo. Nessun integratore può replicare questo effetto.

**Dormi 7-8 ore.** Il sonno è il momento in cui il corpo ripara, rigenera e consolida. Senza sonno sufficiente, anche la migliore integrazione rende la metà.

**Muoviti ogni giorno.** Non serve andare in palestra. Una camminata di 30 minuti è sufficiente per migliorare la sensibilità insulinica, ridurre l'infiammazione e supportare la detossificazione.

**Riduci gli alimenti ultra-processati.** Ogni alimento processato che elimini è un passo verso un intestino più sano e un assorbimento migliore di tutti i nutrienti, sia dal cibo che dagli integratori.

Se fai queste 5 cose, sei già avanti rispetto al 90% delle persone. L'integrazione è il passo successivo: colma le carenze che l'alimentazione da sola non riesce a coprire.

**[BLOCCO REVIEW]**

**"Un solo barattolo al posto dei 10 che dovevo usare in precedenza."** Stefano F.

**"Prima di Paleocomplex ero costretta ad assumere troppe pastiglie ogni giorno. Paleocomplex è arrivato al momento giusto: comodissimo, e con Paleocomplex ho risparmiato parecchio sul budget mensile destinato all'integrazione."** Paola

Un forte abbraccio
Lorenzo Zarone
Fondatore di Paleocomplex

P.S. Se le basi sono in ordine e vuoi fare il passo successivo: **[Vai alla guida alla scelta](https://paleocomplex.com/guida-scelta)**

---

## EMAIL 4 — Vitamina K2 e salute cardiovascolare (+13 giorni)

### Oggetto (3 varianti A/B)

- A: Vitamina K2: la vitamina che protegge le tue arterie
- B: Placche alle carotidi? Il ruolo della K2 che nessuno ti spiega
- C: Il calcio nelle ossa, non nelle arterie: come fa la K2

### Preview text (3 varianti)

- A: Il calcio può finire nel posto sbagliato. La K2 lo dirige.
- B: Perché ogni volta che leggo "la K2 non serve" mi sanguinano gli occhi.
- C: La vitamina più sottovalutata per la salute cardiovascolare.

### Corpo email

Ciao [NOME]

C'è una vitamina di cui quasi nessuno parla, ma che può fare la differenza tra il calcio che finisce nelle tue ossa e il calcio che finisce nelle tue arterie.

La vitamina K2 nella forma MK-7.

Funziona così. La vitamina D aumenta l'assorbimento del calcio dall'intestino. Ottimo. Ma una volta nel sangue, quel calcio deve andare nel posto giusto: le ossa. Se non c'è abbastanza K2, il calcio può depositarsi nelle arterie, nei reni, nelle articolazioni. Invece di rafforzare le ossa, calcifica i tessuti molli.

La K2 attiva due proteine fondamentali. La prima, l'osteocalcina, lega il calcio alle ossa. La seconda, la MGP (matrix gla protein), lo rimuove dalle arterie. Senza K2, entrambe restano inattive.

Ogni volta che leggo qualcuno scrivere "fino a 10.000 unità di vitamina D la K2 non serve" mi sanguinano gli occhi. È il contrario: è proprio la carenza di K2 che può portare ai cosiddetti "sintomi di tossicità della vitamina D" e alla calcificazione arteriosa.

Il rapporto ottimale? 100 mcg di K2 MK-7 ogni 1.000 UI di vitamina D. Se prendi 5.000 UI di D3, ti servono 500 mcg di K2. Se ne prendi 10.000, te ne servono 1.000 mcg. Quanti integratori di vitamina D sul mercato includono la K2 a questi dosaggi? Quasi nessuno.

**[BLOCCO REVIEW]**

**"A 70 anni ho riscontrato un oggettivo aumento delle energie e una generale sensazione di benessere. Vitamina D sempre sui 60 ng."** Federico

**"Mio padre ha 93 anni. Da quando ha cominciato ad assumere Paleocomplex Revolution è rinato. È tornato a deambulare benissimo, non accusa disturbi e gli è tornato l'appetito."** Eleonora M.

**Tra qualche giorno** torno sulla vitamina D, ma da un angolo che probabilmente non hai mai considerato: la stagionalità. Ti dirò esattamente quando fare le analisi (sono due momenti dell'anno specifici), quando esporti al sole serve davvero, e perché chi ti consiglia di prendere il sole a novembre ti sta dicendo una cosa che la fisica smentisce.

Un forte abbraccio
Lorenzo Zarone
Fondatore di Paleocomplex

P.S. Nei nostri multivitaminici il rapporto K2/D3 è fisso a 1:10. Quando aumenti la dose, tutti i cofattori scalano proporzionalmente. **[Scopri come sono formulati](https://paleocomplex.com/guida-scelta)**

---

## EMAIL 5 — Vitamina D: l'angolo stagionale (+16 giorni)

### Oggetto (3 varianti A/B)

- A: L'"inverno della vitamina D": cosa succede al tuo corpo da ottobre a marzo
- B: Quando fare le analisi della vitamina D (e cosa devi sapere)
- C: Se qualcuno ti dice di prendere il sole a novembre, cambia consiglio

### Preview text (3 varianti)

- A: Da ottobre a marzo il tuo corpo non produce vitamina D. Ecco cosa fare.
- B: I 2 momenti dell'anno in cui controllare i tuoi livelli.
- C: Il sole, le stagioni e l'integrazione: guida pratica.

### Corpo email

Ciao [NOME]

Ti avevo già parlato della vitamina D e dei suoi cofattori. Oggi voglio darti un'informazione pratica che cambia tutto: **quando** integrarla e **quanto**.

La produzione cutanea di vitamina D dipende dall'angolo di incidenza dei raggi UVB. In Italia, da ottobre a marzo (al Nord) e da ottobre a febbraio (al Centro-Sud), il sole è troppo basso per stimolare la produzione. Se qualcuno ti consiglia di prendere il sole a novembre, anche nelle ore centrali, mi dispiace: non produrrai neanche una nanoparticella di vitamina D.

Questo periodo si chiama "inverno della vitamina D". Per 4-6 mesi all'anno il tuo corpo non ne produce e i livelli calano progressivamente.

Da aprile a settembre invece il sole è il tuo migliore alleato. Esponiti il più possibile: 15-20 minuti al giorno con pelle scoperta sono sufficienti. Il tuo corpo in quel tempo produce circa 15.000 UI di D3. Ma anche in estate, quasi nessuno riesce a stare al sole abbastanza. Una piccola integrazione di 2.000-2.500 UI al giorno resta utile.

**Quando fare le analisi?** Due volte all'anno.

**Fine marzo:** dopo l'inverno, quando i livelli sono al minimo. Se sei sotto 30 ng/ml, hai una carenza.

**Fine settembre:** dopo l'estate, quando i livelli sono al massimo. Se neanche dopo mesi di sole arrivi a 40-60 ng/ml, c'è un problema di assorbimento o di integrazione insufficiente.

Il valore ottimale è tra 40 e 60 ng/ml. Non amo i mega dosaggi: se non conosci i tuoi livelli, parti con 5.000 UI al giorno, controlla dopo 3 mesi e aggiusta. Se non basta, sali a 10.000.

**[BLOCCO REVIEW]**

**"Dopo solo tre mesi la mia vitamina D da 39 è andata a 70. Cosa che non è successa prendendo il D-base gocce."** Cliente verificato

**"I miei livelli di vitamina D sono saliti in poco tempo da 19 a 60."** Massimo C.

**Tra qualche giorno** affronto l'obiezione che ricevo più spesso: "i tuoi prodotti costano troppo." Lo capisco, è la reazione più comune. Ma voglio capovolgere il ragionamento e farti vedere un calcolo che nessuno fa, ma che dovresti fare. Spoiler: non è il tuo integratore che costa troppo. È il modo in cui stai integrando adesso.

Un forte abbraccio
Lorenzo Zarone
Fondatore di Paleocomplex

P.S. I nostri multivitaminici contengono D3 da 2.000 a 10.000 UI (modulabile con la dose) insieme a K2, magnesio, zinco e tutti i cofattori: **[Scopri quale fa per te](https://paleocomplex.com/guida-scelta)**

---

## EMAIL 6 — "Costa troppo?" Il vero costo dell'integrazione (+19 giorni)

### Oggetto (3 varianti A/B)

- A: "Costa troppo." (Capovolgiamo il ragionamento)
- B: Quanto spendi davvero in integratori ogni mese?
- C: €3,47 al giorno. Meno di una colazione al bar.

### Preview text (3 varianti)

- A: Il costo di Paleocomplex vs il costo di fare male.
- B: Fai due conti e poi decidi.
- C: Il confronto che nessuno fa (ma che dovresti fare).

### Corpo email

Ciao [NOME]

Eccoci al ragionamento che ti avevo promesso. Capisco perfettamente se pensi che i nostri prodotti costino tanto. È la reazione più comune. Oggi voglio fare un ragionamento onesto sui numeri.

**Il costo di comprare singolarmente.** Prendere separatamente gli stessi ingredienti di Elisir (40 nutrienti) nelle stesse forme e dosaggi costerebbe tra **€302 e €460 per 40 giorni**. Elisir costa €139. Non è un risparmio inventato: puoi verificarlo confrontando le etichette prodotto per prodotto.

**Il costo al giorno.** Elisir costa €3,47 al giorno. Essentiel costa €2,15. Paleocomplex base costa €2,23. Meno di una colazione al bar con cappuccino e cornetto.

**Il costo di NON integrare bene.** Questo è il calcolo che nessuno fa. Quanto costano 5 integratori separati con dosaggi simbolici che non fanno nulla? Non zero: costano i soldi che hai speso più il tempo che hai perso senza risultati. Quante persone spendono €30-50 al mese in prodotti da farmacia con il "100% del VNR" e dopo un anno non hanno notato nessuna differenza?

Non ti sto dicendo che devi comprare da noi. Ti sto dicendo che se scegli di integrare, fallo bene. Confronta le etichette. Guarda le forme. Guarda i dosaggi. Poi decidi.

**[BLOCCO PRODOTTO: Elisir — 40 nutrienti, €3,47/giorno, 40 giorni]**

**[BLOCCO PRODOTTO: Essentiel — 34 nutrienti, €2,15/giorno, 60 giorni]**

**[BLOCCO REVIEW]**

**"Ogni volta che vedrai o sentirai parlare di integratori sentirai la piena soddisfazione di essere già al vertice. E vista la qualità e la comodità d'uso, il costo è davvero esiguo."** Matteo

**"Con Paleocomplex ho risparmiato parecchio sul budget mensile destinato all'integrazione. Lo consiglio a tutti."** Paola

Un forte abbraccio
Lorenzo Zarone
Fondatore di Paleocomplex

P.S. Se vuoi confrontare i nostri prodotti e capire quale si adatta al tuo budget: **[Vai alla guida alla scelta](https://paleocomplex.com/guida-scelta)**

---

## EMAIL 7 — Per quanto tempo integrare? (+22 giorni)

### Oggetto (3 varianti A/B)

- A: "Provo un mese e vedo." (L'errore più comune)
- B: Per quanto tempo bisogna integrare?
- C: Perché un mese non basta (ma non devi prendere integratori per sempre)

### Preview text (3 varianti)

- A: Il tempo minimo per vedere risultati reali.
- B: Ciclizzazione, costanza e il falso mito del "mese di prova".
- C: La risposta onesta alla domanda che ci fate più spesso.

### Corpo email

Ciao [NOME]

"Provo un mese e vedo come va."

È la frase che sento più spesso. Ed è l'errore più comune.

Non perché un mese sia poco. Ma perché i nutrienti non funzionano come i farmaci. Non c'è un effetto immediato on/off. C'è un processo: il tuo corpo deve riempire le riserve, riparare i tessuti, ristabilire equilibri che magari sono compromessi da anni.

Molte persone sentono più energia già nelle prime 2 settimane. Alcune dopo pochi giorni. Ma i risultati strutturali (analisi del sangue, densità ossea, qualità del sonno profondo, elasticità della pelle) richiedono **almeno 2-3 mesi di uso continuativo**.

L'approccio che consiglio è semplice: 3 mesi di integrazione costante, poi una pausa facoltativa di 15-20 giorni. Poi riparti. La base (un multivitaminico) ha senso prenderla tutto l'anno, perché le carenze non vanno in vacanza.

Non è un trucco per venderti più prodotto. È biochimica: le vitamine liposolubili (A, D, E, K) si accumulano nel tempo, i livelli nel sangue salgono gradualmente, e gli effetti a cascata su ossa, sistema immunitario e funzione cellulare si consolidano dopo mesi, non dopo giorni.

**[BLOCCO REVIEW]**

**"Lo uso ormai da un anno. Io, mio marito e i miei figli. Mai un raffreddore. I miei figli sono stati gli unici a scuola a non fare neanche un giorno di assenza nell'anno scolastico precedente. L'intento era prenderlo a cicli, ma appena lo smettiamo ci manca talmente che lo ricompriamo subito."** Justine

**"Lo uso ormai come routine quotidiana da molto tempo e trovo grande beneficio."** Ornella

Un forte abbraccio
Lorenzo Zarone
Fondatore di Paleocomplex

P.S. Se vuoi iniziare con il piede giusto: **[Vai alla guida alla scelta](https://paleocomplex.com/guida-scelta)**

---

## EMAIL 8 — Risultati misurabili: analisi del sangue (+25 giorni)

### Oggetto (3 varianti A/B)

- A: Da 17 a 60. Da 39 a 70. I numeri parlano.
- B: Le analisi del sangue prima e dopo Paleocomplex
- C: Non devi crederci. Devi misurarlo.

### Preview text (3 varianti)

- A: Risultati reali, misurabili, verificabili.
- B: Vitamina D, ferro, energia: cosa dicono le analisi.
- C: Le prove che non servono parole per spiegare.

### Corpo email

Ciao [NOME]

Oggi lascio parlare i numeri. Nessuna opinione, nessuna promessa. Solo risultati misurabili da analisi del sangue, condivisi spontaneamente dai nostri clienti.

**Massimo C.** (psicologo, fisioterapista, erborista, laureato in scienze motorie):

"Ho comprato il Paleocomplex dopo aver osservato per un certo periodo il suo produttore Lorenzo Zarone, data la mia disillusione sui tanti improvvisati pseudospecialisti degli integratori. E subito ho notato la sua competenza. Il prodotto si è dimostrato in linea con la mia impressione iniziale: completo, mi ha fornito energia sia nella vita che negli allenamenti, scomparsa di dolori articolari e di una noiosissima dermatite seborroica. **I miei livelli di vitamina D sono saliti in poco tempo da 19 a 60.**"

**Nello P.** (classe 1963):

"Dopo 3 mesi di integrazione, una sensazione di benessere in tutte le attività sportive e non. **La vitamina D da 17 a 35** purtroppo senza sole. Ma il risultato che mi ha sorpreso di più è l'effetto sulla pelle in tutte le parti del corpo, e non sono giovanissimo."

**Cliente verificato:**

"Dopo solo tre mesi **la mia vitamina D da 39 è andata a 70**. Cosa che non è successa prendendo il D-base gocce. Questo integratore lo consiglio a tutti."

**Alessandra G.:**

"La vitamina D solitamente la assumevo tramite il D-base, ma avendola a zero non riuscivo mai ad averla alta. Ora con un'unica soluzione ho risolto."

Questi risultati non li abbiamo creati noi. Li hanno misurati i laboratori di analisi e li hanno condivisi le persone. Se vuoi verificare anche tu, fai le analisi della 25(OH)D prima di iniziare e ripetile dopo 3 mesi.

Un forte abbraccio
Lorenzo Zarone
Fondatore di Paleocomplex

P.S. Se i numeri ti hanno convinto più delle parole: **[Vai alla guida alla scelta](https://paleocomplex.com/guida-scelta)**

---

## EMAIL 9 — Il magnesio: 300 reazioni e nessuno te lo dice (+28 giorni)

### Oggetto (3 varianti A/B)

- A: Il magnesio che non ti salva solo dai crampi
- B: 300 reazioni enzimatiche dipendono da un minerale che ti manca
- C: Crampi, insonnia, irritabilità: e se fosse solo magnesio?

### Preview text (3 varianti)

- A: Il minerale più carente e più sottovalutato.
- B: Non tutti i magnesio sono uguali. Le forme contano.
- C: Perché il magnesio da farmacia potrebbe non funzionare.

### Corpo email

Ciao [NOME]

Il magnesio è coinvolto in oltre 300 reazioni enzimatiche nel tuo corpo. Eppure è uno dei minerali più carenti nella popolazione occidentale.

I sintomi di carenza sono così comuni che li consideriamo normali: crampi muscolari, difficoltà ad addormentarsi, irritabilità, stanchezza inspiegabile, mal di testa. Se hai uno o più di questi sintomi in modo ricorrente, prima di cercare cause complesse vale la pena escludere la più semplice.

Ma c'è un problema: non tutti i magnesio sono uguali.

Il magnesio ossido (quello che trovi nella maggior parte degli integratori da farmacia) ha una biodisponibilità molto bassa. Il tuo corpo ne assorbe una piccola parte, e il resto finisce nell'intestino con effetto lassativo. Non è un caso se tante persone dicono "il magnesio mi dà problemi intestinali": stanno prendendo la forma sbagliata.

Le forme che funzionano davvero sono il **magnesio citrato** (ottima biodisponibilità, ben tollerato), il **magnesio bisglicinato** (chelato con glicina, eccellente per il sonno) e il **magnesio taurinato** (combinato con taurina, ottimo per il cuore e il sistema nervoso).

Nei nostri multivitaminici usiamo magnesio citrato o bisglicinato, a seconda della formulazione. Entrambe sono forme ad alta biodisponibilità, ben tollerate a livello intestinale.

Il magnesio è anche un cofattore essenziale della vitamina D: senza di lui, la D3 non si attiva. Se integri vitamina D senza magnesio, stai facendo solo metà del lavoro.

**[BLOCCO REVIEW]**

**"Ho iniziato con Paleocomplex e ho notato subito miglioramenti: risolto problemi di crampi durante gli allenamenti. Ho raggiunto una qualità del sonno come mai prima. Un sonno profondo e senza interruzioni."** Iuri B.

**"Il primo e importante miglioramento, non correlato o richiesto: il miglioramento del sonno. Cosa che mi tormentava da anni."** Carli

**Tra qualche giorno** ti scrivo l'ultima email di questo percorso. Sono quasi due mesi che ti scrivo. Per chi è arrivato fin qui ho preparato qualcosa di speciale: un regalo concreto, diverso da tutto quello che ti ho proposto finora. Non aprirla solo se non sei interessato a fare il primo passo davvero.

Un forte abbraccio
Lorenzo Zarone
Fondatore di Paleocomplex

P.S. Se il magnesio è uno dei nutrienti che ti mancano, nei nostri multivitaminici è in forma citrato insieme a tutti gli altri cofattori: **[Scopri quale fa per te](https://paleocomplex.com/guida-scelta)**

---

## EMAIL 10 — L'unica cosa che ti chiedo (+32 giorni)

### Oggetto (3 varianti A/B)

- A: L'ultima cosa che ti chiedo (con un regalo)
- B: 58 giorni di contenuti. Ora tocca a te.
- C: Un regalo per chi è arrivato fin qui

### Preview text (3 varianti)

- A: €10 di sconto + spedizione gratuita sul tuo primo ordine.
- B: Questo è il momento giusto per provare.
- C: Un codice speciale per chi ha avuto la pazienza di leggere.

### Corpo email

Ciao [NOME]

Sono quasi due mesi che ti scrivo.

Ti ho parlato delle carenze nutrizionali che quasi tutti hanno senza saperlo. Della vitamina D e dei suoi cofattori. Della metilazione e delle forme vitaminiche. Degli omega 3 e della K2. Del magnesio. Ti ho mostrato analisi del sangue, recensioni di scettici convertiti e consigli pratici su alimentazione e stile di vita.

Non ti ho mai chiesto di comprare a tutti i costi. Non lo faccio neanche adesso.

Ma se sei arrivato a leggere questa email, significa che qualcosa di quello che ti ho raccontato ti ha interessato. E allora voglio farti un regalo.

Ho creato un codice speciale per chi, come te, ha avuto la pazienza di seguire questo percorso:

**Codice: PRIMOPASSO**
**€10 di sconto + spedizione gratuita sul tuo primo ordine.**

Non è il solito sconto. È un invito a fare il primo passo con zero rischi. Non ti è piaciuto? Non riordinare. Ma almeno avrai provato sulla tua pelle (e nelle tue analisi del sangue) cosa significa integrare con dosaggi reali.

Se non sai quale prodotto scegliere: **[CTA: Vai alla guida alla scelta](https://paleocomplex.com/guida-scelta)**

Oppure vai direttamente allo store: **[CTA: Usa il codice PRIMOPASSO](https://paleocomplex.com)**

**[BLOCCO PRODOTTO: Elisir — 40 nutrienti, €3,47/giorno]**

**[BLOCCO PRODOTTO: Essentiel — 34 nutrienti, €2,15/giorno]**

**[BLOCCO PRODOTTO: Revolution — 26 nutrienti, €3,97/giorno]**

**[BLOCCO REVIEW: Le 3 più forti]**

**"Sono invalido per una patologia metabolica. Sono padre single di una bambina di 9 anni. Mi ero dovuto rivolgere ad un aiuto esterno per portarla a scuola. Da 3 settimane assumo Paleocomplex Revolution e oggi ho ricominciato a riaccompagnare mia figlia a scuola. La strada è ancora lunga, ma Paleocomplex Revolution è stato davvero una rivelazione e l'inizio della mia rivoluzione."** Giulio

**"Soffro di stanchezza cronica da 16 anni. Per 16 anni la mia vita è stata un inferno. Dopo 2 mesi ho ripreso a dormire, capelli e unghie più forti, migliorata anche la stanchezza cronica. So che il mio percorso è ancora lungo, ma ora so che sono sulla strada giusta."** Raffaella

**"Sono uno psicologo, fisioterapista, erborista, laureato in scienze motorie. Molto attento alla salute vera e non come persuasione commerciale. Ho subito notato la competenza di Lorenzo. Il prodotto mi ha fornito energia, scomparsa di dolori articolari, e i miei livelli di vitamina D sono saliti da 19 a 60."** Massimo C.

Dopo questa email continuerai a ricevere la nostra newsletter con contenuti di valore. Ma il codice PRIMOPASSO non durerà per sempre.

Un forte abbraccio
Lorenzo Zarone
Fondatore di Paleocomplex

---

## Schema del flow

```
[Completamento Authority, senza acquisto — ~giorno 26]
    │
    ▼  (+2gg = ~g28)
EMAIL 1 — Omega 3: krill, polvere, sinergia
    │
    ▼  (+5gg = ~g31)
EMAIL 2 — Storie di scettici convertiti (social proof dedicata)
    │
    ▼  (+9gg = ~g35)
EMAIL 3 — Alimentazione e stile di vita (zero pitch)
    │
    ▼  (+13gg = ~g39)
EMAIL 4 — Vitamina K2 e salute cardiovascolare
    │
    ▼  (+16gg = ~g42)
EMAIL 5 — Vitamina D: angolo stagionale (diverso da Authority)
    │
    ▼  (+19gg = ~g45)
EMAIL 6 — "Costa troppo?" (obiezione prezzo)
    │
    ▼  (+22gg = ~g48)
EMAIL 7 — Per quanto tempo integrare? (costanza)
    │
    ▼  (+25gg = ~g51)
EMAIL 8 — Risultati misurabili: analisi del sangue (social proof dati)
    │
    ▼  (+28gg = ~g54)
EMAIL 9 — Magnesio: 300 reazioni, forme, sonno
    │
    ▼  (+32gg = ~g58)
EMAIL 10 — "L'unica cosa che ti chiedo" + codice PRIMOPASSO (€10 + spedizione gratis)
    │
    ▼
Fine Conversione → nurturing via newsletter (campaign settimanali)
```

**Se il contatto acquista in qualsiasi momento → esce e entra nel Post Purchase.**

---

## Note

### Codice sconto PRIMOPASSO
- **Valore:** €10 + spedizione gratuita
- **Validità:** solo primo ordine
- **Diverso da BENVENUTO:** il BENVENUTO è "andato" (detto esplicitamente nel welcome). PRIMOPASSO è un nuovo codice per chi ha dimostrato interesse restando 58 giorni in lista.
- **Da creare su WooCommerce** prima dell'attivazione del flow.
- **Non cumulabile** con PROMO3/PROMO6.

### Recensioni utilizzate (tutte verificate dal CSV)
- **Email 1:** Cristina (ciclismo, energia, 6 mesi), Raimondo B. (3 settimane, miglioramenti)
- **Email 2:** Ramy (scettica, stress, 2 settimane), Michela (fibromialgia, scettica, 4 mesi), Alessandra G. (scettica, vitamina D)
- **Email 3:** Stefano F. (semplificazione), Paola (risparmio budget)
- **Email 4:** Federico (70 anni, energia, D a 60), Eleonora M. (padre 93 anni)
- **Email 5:** Cliente verificato (D da 39 a 70), Massimo C. (D da 19 a 60)
- **Email 6:** Matteo (vertice integrazione), Paola (risparmio)
- **Email 7:** Justine (1 anno, famiglia, figli mai malati), Ornella (routine quotidiana)
- **Email 8:** Massimo C. (professionista sanitario), Nello P. (classe 1963), Alessandra G.
- **Email 9:** Iuri B. (crampi risolti, sonno profondo), Carli (sonno migliorato)
- **Email 10:** Giulio (padre single, invalido), Raffaella (stanchezza cronica 16 anni), Massimo C. (professionista)

### Topic basati su dati performance storici
- Omega 3: €1.503 revenue media
- K2 cardiovascolare: €878 revenue, 4.66% click (il più alto)
- Vitamina D stagionale: angolo diverso da Authority (cofattori)
- Integrazione durata: €1.083 revenue media
- Magnesio: €930 revenue media
- Prezzo: obiezione #1 dal sondaggio ex-clienti (41%)
