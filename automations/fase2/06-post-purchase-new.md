**Versione:** 0.9
**Ultimo aggiornamento:** 2026-05-11


# Flow 6: Post Purchase — Nuovo Cliente

## Chi entra in questo flow

Persone che hanno effettuato il **primo ordine** sul sito Paleocomplex (Has Placed Order = 1 over all time).

L'obiettivo del flow è:
- Validare la scelta e abbattere il buyer's remorse
- Accompagnare nei primi 30 giorni con istruzioni, aspettative, ottimizzazione
- Generare social proof tramite richiesta recensione
- Creare la base per un cliente fidelizzato

## Configurazione Klaviyo

**Trigger:** Placed Order
**Filtro principale:**
- Has Placed Order equals 1 over all time (primo acquisto in assoluto)

**Filtro accessori (escludere chi compra SOLO accessori):**
- Items contains at least one supplement (Elisir, Revolution, Essentiel, Paleocomplex, Elisir Basic, Youth, Jeunesse, Hurricane, Armageddon, Artosan, Liverty, Testoplus, Renaissance, Vitamina D)
- Se l'ordine contiene SOLO accessori (Lampada Apollo, occhiali, libri), il flow NON parte
- TODO Fase 2bis: valutare un Post Purchase Accessori dedicato (non urgente, raro che un nuovo cliente compri solo accessori)

**Effetto su altri flow:**
- L'Authority Flow si sospende per questo contatto (chi compra esce dall'Authority)
- I retention flow per prodotto partono dopo (timing Fulfilled Order specifici per prodotto)

## Mittenti

| # | Email | Mittente |
|---|-------|----------|
| 1 | Benvenuto | Lorenzo Zarone |
| 2 | Istruzioni | Lorenzo Zarone |
| 3 | Aspettative | Lorenzo Zarone |
| 4 | Ottimizza | Lorenzo Zarone |
| 5 | Social proof + check-in | Flaminia (Customer Care) |
| 6 | Richiesta recensione | Flaminia (Customer Care) |

## Timeline

| # | Timing | Tema | Tipo |
|---|--------|------|------|
| 1 | +2h | Benvenuto + cosa succede adesso | Statica |
| 2 | +1gg | Istruzioni assunzione | 6 blocchi dinamici |
| 3 | +5gg | Aspettative + cosa farà il prodotto | 4 blocchi dinamici |
| 4 | +12gg | Ottimizza i risultati (5 abitudini complementari) | Statica |
| 5 | +18gg | Social proof + check-in | 4 blocchi dinamici |
| 6 | +32gg | Richiesta recensione (anticipa la mail di sistema a +34gg) | Statica |

**Sovrapposizioni con retention flow verificate:** PP email 5 (gg 18) gap 2gg da retention 30gg cross-sell (gg 20). PP email 6 (gg 32) gap 2gg da retention 30gg reminder (gg 30) e gap 4gg da retention 40gg cross-sell (gg 28). Tutti i gap superiori a 2 giorni.

**Coordinamento con WooCommerce:**
- L'email di conferma ordine arriva da WooCommerce standard (riepilogo ordine, totale, dettaglio prodotti)
- L'email di richiesta recensione automatica di WooCommerce è schedulata a +34gg dall'ordine (oggetto: "⭐⭐⭐⭐⭐ Quante stelle daresti a Paleocomplex?")
- La nostra email 6 di richiesta recensione (+32gg) anticipa di 2 giorni questa email di sistema, preparando il cliente

---

## EMAIL 1 — Benvenuto (+2 ore)

**Mittente:** Lorenzo Zarone
**Tipo:** Statica (uguale per tutti)

### Oggetto (3 varianti A/B)

- A: Benvenuto. Ecco cosa succede adesso.
- B: Hai fatto la scelta giusta
- C: Ti aspettano alcune cose importanti

### Preview text (3 varianti)

- A: Le prossime settimane non saranno come le altre.
- B: L'ordine è confermato. Adesso arriva la parte interessante.
- C: Le mie prossime email valgono la pena di essere aperte.

### Corpo email

Ciao [NOME]

Ti do il mio benvenuto.

Hai appena scelto un integratore con una formulazione diversa dalla maggior parte di quelli che troveresti in farmacia o al supermercato. La scelta che hai fatto si vede nei dosaggi, nelle forme degli ingredienti e nella trasparenza dell'etichetta. Da qui in avanti la palla passa a noi.

Info sulla consegna del tuo ordine 📦
L'ordine ti è già stato confermato dal sistema (se non è arrivata l'email con il riepilogo contattaci)
Sarà spedito entro 24h lavorative e riceverai un’email con il tracking appena il pacco partirà.
Solitamente la consegna avviene in 24/48h (usiamo corriere espresso nella maggior parte delle spedizioni, con tracking e assicurazione).



Nelle prossime settimane però ti scriverò io, di persona. Non sono email di vendita, sono email pensate per aiutarti a tirare fuori il massimo da quello che hai comprato.

**Domani** ti spiego come assumere correttamente il prodotto: è la cosa più importante per partire bene.

**Tra qualche giorno** ti dico cosa aspettarti realisticamente dalle prime settimane di integrazione.

**Più avanti** ti darò qualche consiglio per amplificare i risultati senza spendere altro.

Niente promesse esagerate. Solo informazioni che la maggior parte dei brand di integratori non si prende il tempo di darti.

Per qualsiasi cosa scrivici a **ordini@paleocomplex.com**: rispondiamo sempre, di solito entro la giornata lavorativa.

A domani.

Un forte abbraccio
Lorenzo Zarone
Fondatore di Paleocomplex

---

## EMAIL 2 — Istruzioni assunzione (+1 giorno)

**Mittente:** Lorenzo Zarone
**Tipo:** Tronco comune + 14 blocchi dinamici (uno per ogni prodotto). Ogni cliente vede solo i blocchi dei prodotti effettivamente acquistati. Le sezioni "comuni" (modalità multivitaminico, nota krill, timing collagene) sono testualmente identiche tra i blocchi che le condividono.

### Oggetto (3 varianti A/B)

- A: Il tuo prodotto è in viaggio. Ecco come usarlo bene.
- B: Le istruzioni per partire con il piede giusto
- C: Cinque minuti per fare le cose nel modo corretto

### Preview text (3 varianti)

- A: La cosa più importante è iniziare bene. Te lo spiego in pratica.
- B: Dosaggi, orari, errori da evitare.
- C: Non è complicato. Ma c'è un modo giusto.

### Corpo email

**Tronco comune — apertura**

Ciao [NOME]

Te l'avevo detto: oggi le istruzioni.

Il tuo ordine è in viaggio (se non l'ha già consegnato il corriere mentre leggi). Prima che lo apri voglio assicurarmi che parti con il piede giusto. Gli integratori funzionano se assunti bene. È un dettaglio che può fare la differenza tra "non sento niente" e "sento la differenza dopo qualche settimana".

Qui sotto trovi le istruzioni precise per quello che hai ordinato.

---

### Sotto-blocchi comuni (riusati nei blocchi prodotto)

Questi paragrafi compaiono **testualmente identici** in tutti i blocchi che li condividono. Non riformulare. Se serve modificarli, cambiarli in tutti i blocchi che li usano.

**[COMUNE-MULTI] Modalità multivitaminici** (Paleocomplex, Revolution, Elisir, Elisir Basic, Essentiel):
> Sciogli la polvere in un bicchiere di acqua fresca o a temperatura ambiente. Mai calda: le vitamine idrosolubili e altri ingredienti si ossidano. Bevi dopo colazione o dopo pranzo, mai a stomaco vuoto: le vitamine liposolubili A, D, E, K hanno bisogno dei grassi del pasto per essere assorbite meglio.

**[COMUNE-KRILL] Nota krill** (Paleocomplex, Revolution, Elisir, Elisir Basic):
> Il prodotto contiene Omega-3 da krill. Può capitare di percepire un leggero odore di pesce all'apertura del barattolo. È normale, sciogliendolo in acqua diventa impercettibile.

**[COMUNE-COLLAGENE] Timing collagene** (Youth, Jeunesse):
> Si prende preferibilmente dopo cena, idealmente 1-1,5 ore prima di andare a dormire. La glicina (un terzo del collagene) favorisce il rilassamento e supporta la qualità del sonno profondo: è proprio nel sonno profondo che il corpo costruisce nuovo collagene.
> 
> Il collagene richiede costanza. I primi risultati sulla pelle si vedono dopo 2-3 settimane, su unghie e capelli serve un mese o più. Datti almeno 3 mesi continuativi per giudicare l'efficacia.


---

### Blocchi prodotto (uno per ogni SKU)

I 14 blocchi sotto sono separati. Show condition: Items contains "[Nome prodotto]". Ogni blocco è auto-contenuto al singolare e non inizia con il nome del prodotto.

---

**[BLOCCO 1 — PALEOCOMPLEX]**
*Show condition: Items contains "Paleocomplex" AND NOT "Revolution"*

Il tuo Paleocomplex è un multivitaminico in polvere a dose modulabile. Il misurino ha tacche a 2, 3 e 5 ml. La dose consigliata per adulti è di 2 misurini al giorno, riempiti fino alla tacca 5 (10 ml totali). Puoi modulare la quantità in base alle tue esigenze: ogni nutriente scala proporzionalmente alla dose. Per la vitamina D, ad esempio: 2 ml = 2.000 UI, 5 ml = 5.000 UI, 10 ml (2 misurini) = 10.000 UI.

Se hai dubbi su quale dose è adatta a te, scrivici a ordini@paleocomplex.com.

[COMUNE-MULTI]

[COMUNE-KRILL]

---

**[BLOCCO 2 — PALEOCOMPLEX REVOLUTION]**
*Show condition: Items contains "Revolution"*

Il tuo Paleocomplex Revolution è un multivitaminico in polvere a dose modulabile, con antiossidanti avanzati rispetto al Paleocomplex base (glutatione liposomiale, ubiquinolo, astaxantina, vitamina C liposomiale). Il misurino ha tacche a 2, 3 e 5 ml. La dose consigliata per adulti è di 2 misurini al giorno, riempiti fino alla tacca 5 (10 ml totali). Puoi modulare la quantità in base alle tue esigenze: ogni nutriente scala proporzionalmente alla dose. Per la vitamina D, ad esempio: 2 ml = 2.000 UI, 5 ml = 5.000 UI, 10 ml (2 misurini) = 10.000 UI.

Se hai dubbi su quale dose è adatta a te, scrivici a ordini@paleocomplex.com.

[COMUNE-MULTI]

[COMUNE-KRILL]

---

**[BLOCCO 3 — ELISIR]**
*Show condition: Items contains "Elisir" AND NOT "Elisir Basic"*

Il tuo Elisir è il nostro multivitaminico più completo: 40 nutrienti in un solo misurino al giorno. È in polvere, assumi 1 misurino colmo (circa 5 g) sciolto in un bicchiere di acqua.

[COMUNE-MULTI]

[COMUNE-KRILL]

---

**[BLOCCO 4 — ELISIR BASIC]**
*Show condition: Items contains "Elisir Basic"*

Il tuo Elisir Basic è un multivitaminico in polvere, assumi 1 misurino colmo (circa 5 g) al giorno sciolto in un bicchiere di acqua.

A differenza degli altri multivitaminici della linea, Elisir Basic non contiene vitamina D ed ha un dosaggio ridotto di vitamina K2 (50 mcg). È una scelta intenzionale, pensata per due tipi di persone: chi assume la vitamina D separatamente con dosaggi personalizzati (su prescrizione medica o per esposizione al sole ogni giorno) e chi assume farmaci anticoagulanti coumarinici per cui il dosaggio di K2 più basso è compatibile.

[COMUNE-MULTI]

[COMUNE-KRILL]

---

**[BLOCCO 5 — ESSENTIEL]**
*Show condition: Items contains "Essentiel"*

Il tuo Essentiel è un multivitaminico in polvere, assumi 1 misurino colmo (circa 5 g) al giorno sciolto in un bicchiere di acqua.

A differenza degli altri nostri multivitaminici, Essentiel non contiene krill: è pensato per chi è allergico ai crostacei o semplicemente preferisce un prodotto senza derivati marini. In più contiene citicolina e acetil-carnitina, due nutrienti specifici per la funzione cognitiva e l'energia mentale.

[COMUNE-MULTI]

---

**[BLOCCO 6 — YOUTH]**
*Show condition: Items contains "Youth" AND NOT "Jeunesse"*

Il tuo Youth è un integratore di collagene in polvere ad alto dosaggio: 2 misurini colmi al giorno (circa 10 g totali) sciolti in 250 ml di acqua fresca o a temperatura ambiente.

[COMUNE-COLLAGENE]

Una nota importante: la glucosamina presente in Youth deriva da crostacei. Se sei allergico ai crostacei, puoi sostituirlo con Jeunesse (glucosamina di origine vegetale).

---

**[BLOCCO 7 — JEUNESSE]**
*Show condition: Items contains "Jeunesse"*

Il tuo Jeunesse è un integratore di collagene grass-fed in polvere, formula premium: assumi 1 misurino colmo al giorno (circa 15g), sciolto in 250 ml di acqua fresca o a temperatura ambiente.

[COMUNE-COLLAGENE]



---

**[BLOCCO 8 — HURRICANE]**
*Show condition: Items contains "Hurricane"*

Il tuo Hurricane è un pre-allenamento. Si usa solo nei giorni in cui ti alleni: sciogli un misurino colmo (circa 15 g) in 300 ml di acqua e bevilo 30-45 minuti prima della sessione.

Se sei sensibile alla caffeina, ricorda che Hurricane contiene Guaranà titolato: l'apporto di caffeina è basso ma presente. Meglio non assumerlo nelle ore serali per non disturbare il sonno.

Se hai anche Armageddon nell'ordine, puoi miscelarli: 30-40 minuti prima dell'allenamento bevi Hurricane + Armageddon insieme. È un pre-workout completo (energia + protezione muscolare).

---

**[BLOCCO 9 — ARMAGEDDON]**
*Show condition: Items contains "Armageddon"*

Il tuo Armageddon è una formula di aminoacidi essenziali. Il dosaggio si calcola sul peso corporeo: regola semplice, 1 grammo di prodotto per ogni 10 kg di peso. Per semplificare, e per assumere una dose realmente efficace, l'assunzione consigliata è di 2 misurini  (circa 10 g).

Sul timing hai flessibilità: puoi prenderlo prima dell'allenamento (per energia e protezione muscolare), durante (per coprire sessioni lunghe), o dopo (per il recupero). Per sport di endurance come tennis o corsa, l'ideale è bere il prodotto 10-15 minuti prima e continuare fino a 30 minuti dopo l'inizio della sessione.

Nei giorni di riposo puoi assumerlo al mattino se vuoi mantenere l'apporto aminoacidico costante. È particolarmente utile per chi ha più di 40 anni e si allena con i pesi (supporto anti-sarcopenia) o per chi segue una dieta ipoproteica.

Se hai anche Hurricane nell'ordine, puoi miscelarli prima dell'allenamento.

---

**[BLOCCO 10 — ARTOSAN]**
*Show condition: Items contains "Artosan"*

Il tuo Artosan è un integratore in capsule per il supporto articolare. Dose standard: 1 capsula al giorno ai pasti principali. È la dose di mantenimento e prevenzione.

In presenza di dolore articolare attivo puoi aumentare gradualmente: 1 capsula in più al giorno fino a quando il dolore si attenua, distribuendo le capsule nella giornata (colazione, pranzo, cena). Massimo 3-4 capsule al giorno. Quando il dolore passa, mantieni il dosaggio per un periodo e poi scendi gradualmente fino a 1 capsula al giorno.

Una nota importante: Artosan può essere assunto insieme ai comuni antinfiammatori (FANS come ibuprofene, ketoprofene): non c'è alcuna interazione. Se invece assumi anticoagulanti, confrontati prima con il tuo medico.

---

**[BLOCCO 11 — LIVERTY]**
*Show condition: Items contains "Liverty"*

Il tuo Liverty è un integratore in capsule per il supporto della funzione epatica: 1 capsula al giorno dopo un pasto. In presenza di patologie specifiche puoi salire a 2 capsule, ma solo in accordo con il medico.

Puoi assumerlo in continuo oppure ciclicamente: la modalità consigliata da Lorenzo è 1 confezione (60 giorni) seguita da una pausa di 2-3 mesi, per un totale di 2-4 confezioni l'anno. È particolarmente indicato per chi consuma alcol regolarmente o assume farmaci che impegnano il fegato (statine, paracetamolo cronico).

Se hai calcoli biliari o patologie epatiche, parlane con il tuo medico prima di iniziare: la curcumina stimola la secrezione biliare.

---

**[BLOCCO 12 — TESTOPLUS]**
*Show condition: Items contains "Testoplus"*

Il tuo Testoplus è un integratore in capsule per il supporto ormonale. Dose standard per uomini: da 4 a 6 capsule al giorno. Si parte con 2 dopo colazione e 2 dopo pranzo; se serve si aggiungono 2 dopo cena.

In casi specifici (sovrappeso/obesi con aromatasi elevata) si può arrivare fino a 8 capsule per un breve periodo, distribuendole nella giornata (colazione, pranzo, spuntino, cena), poi scalare gradualmente a 6 e poi a 4. Ma è una scelta da prendere con il proprio medico.

Per le donne in menopausa o con calo della libido, il dosaggio è ridotto a 2-4 capsule al giorno.

Avvertenza importante: non usare in presenza di disfunzioni della tiroide e non combinare con farmaci anticoagulanti o antiaggreganti piastrinici senza il parere del medico (per la presenza di Ginkgo Biloba).

---

**[BLOCCO 13 — RENAISSANCE]**
*Show condition: Items contains "Renaissance"*

Il tuo Renaissance è un integratore anti-aging cellulare in capsule. Dose standard: 4 capsule al giorno, preferibilmente al mattino dopo un pasto (mai a stomaco vuoto).

Puoi assumerlo in continuo (la scelta più semplice), oppure ciclicamente con pause di 10 giorni dopo ogni ciclo di 30 giorni di assunzione.

Avvertenza importante: non superare la dose consigliata (contiene EGCG da tè verde) e non combinare con altri prodotti contenenti tè verde. Se assumi farmaci ipoglicemizzanti, confrontati con il tuo medico. La berberina può influenzare la glicemia.

---

**[BLOCCO 14 — VITAMINA D IN GOCCE]**
*Show condition: Items contains "Vitamina D"*

La tua Vitamina D in gocce è formulata in olio MCT (un grasso): può essere assunta anche a stomaco vuoto, non richiede il pasto.

Dose standard: 4 gocce al giorno a colazione, equivalenti a circa 2.000 UI. Ogni goccia contiene circa 500 UI. Il dosaggio può essere modulato in base ai tuoi livelli ematici:

- 1-2 gocce al giorno: dose minima di mantenimento
- 4 gocce: dose standard per la maggior parte degli adulti
- 8 gocce: protocollo intensivo per carenze marcate (consultare il medico)

Se non conosci i tuoi livelli di vitamina D, parti con 4 gocce al giorno per 3 mesi e poi fai un controllo della 25(OH)D. In base al risultato puoi regolare il dosaggio.

---

**Tronco comune — chiusura**

Se hai dubbi specifici sul dosaggio o vuoi adattare l'assunzione a una tua condizione (gravidanza, allattamento, patologie, farmaci), scrivici a **ordini@paleocomplex.com**. Per qualunque altra domanda sui prodotti, la pagina **[FAQ del sito](https://paleocomplex.com/faq/)** copre quasi tutti i casi.

**Tra qualche giorno** ti dico cosa aspettarti realisticamente dall'integrazione. Spoiler: non è quello che ti dicono le pubblicità.

Un forte abbraccio
Lorenzo Zarone
Fondatore di Paleocomplex

---

DA CAPIRE SE METTERE:
**P.S. SOLO per chi non ha accettato marketing al checkout:**

*P.S. Questa è un'email di servizio sul tuo ordine. Attualmente non hai dato il consenso alle comunicazioni marketing. Se ti fa piacere ricevere consigli pratici e contenuti utili su integrazione e salute, puoi iscriverti alla nostra newsletter [link]: solo cose utili, mai spam.*

---

## EMAIL 3 — Aspettative + cosa farà il prodotto (+5 giorni)

**Mittente:** Lorenzo Zarone
**Tipo:** Tronco comune + 9 blocchi dinamici (Show/Hide su Items dell'ordine). Le aspettative dei prodotti sport e specifici sono troppo diverse per essere accorpate.

### Oggetto (3 varianti A/B)

- A: Cosa aspettarti realisticamente nelle prossime settimane
- B: Gli integratori non funzionano come dicono le pubblicità
- C: I tempi veri dell'integrazione (senza esagerazioni)

### Preview text (3 varianti)

- A: Ti spiego cosa è normale aspettarsi e cosa no.
- B: Niente promesse miracolose. Solo onestà.
- C: La costanza è tutto. Te lo spiego con esempi concreti.

### Corpo email

**Tronco comune — apertura**

Ciao [NOME]

A questo punto hai (spero) iniziato il tuo prodotto da qualche giorno. È il momento giusto per parlarti di una cosa importante: cosa aspettarti realisticamente.

Ti chiedo cinque minuti perché questo è il punto in cui la maggior parte delle persone si scoraggia. Iniziano un integratore, dopo 7-10 giorni "non sentono niente" e mollano. È un errore. Ma è anche colpa di come il marketing comunica gli integratori, promettendo risultati immediati quando i meccanismi biologici hanno tempi diversi.

Ti spiego come funzionano davvero le cose, partendo da una premessa onesta: ogni corpo è diverso. Lo stato di partenza, l'assorbimento individuale, lo stile di vita, l'età, eventuali patologie, tutto influisce sui tempi. Quelli che leggi sotto sono i tempi medi, basati su quello che ci raccontano migliaia di clienti.

---

**[BLOCCO 1 — MULTIVITAMINICI]**
*Show condition: Items contains "Paleocomplex" OR "Revolution" OR "Elisir" OR "Elisir Basic" OR "Essentiel"*

**Cosa aspettarti dal tuo multivitaminico**

Prime 2 settimane: i primi segnali sono sottili ma reali. Il magnesio può migliorare la qualità del sonno e ridurre i crampi notturni già nei primi giorni. Le vitamine B attivate iniziano a sostenere il metabolismo energetico. Chi aveva carenze importanti può notare una maggiore stabilità dell'umore. È la fase in cui il corpo ricostituisce le scorte di micronutrienti.

Dopo 1 mese: i risultati diventano tangibili. L'energia è più costante, meno crolli pomeridiani, meno bisogno di stimolanti. Unghie e capelli iniziano a mostrare miglioramento (biotina, zinco, selenio). Chi fa attività fisica nota un recupero migliore.

Dopo 2-3 mesi: è il momento in cui controllare le analisi del sangue ha senso. Vitamina D, ferritina, omocisteina sono i parametri più sensibili (la vitamina D richiede 8-12 settimane per stabilizzarsi). La pelle è più luminosa. Il sistema immunitario è più reattivo. Chi smette nota subito: "mi manca qualcosa".

Uso continuativo (6+ mesi): i benefici strutturali e preventivi si consolidano. Salute cardiovascolare, densità ossea, protezione cellulare. Sono benefici che non "senti" nel quotidiano ma che fanno una differenza enorme negli anni a venire.

---

**[BLOCCO 2 — COLLAGENE]**
*Show condition: Items contains "Youth" OR "Jeunesse"*

**Cosa aspettarti dal collagene**

Prime 2 settimane: la pelle inizia ad assorbire i peptidi di collagene. Alcuni clienti riportano "pelle più morbida" già dopo 10 giorni, ma, sono sincero, è presto per risultati visibili. Il miglioramento del sonno (grazie alla glicina) può essere percepibile già nei primi giorni.

Dopo 1 mese: i risultati diventano tangibili. Le articolazioni migliorano, meno dolore e più mobilità. Le unghie sono più forti e crescono in fretta, i capelli cadono meno. La pelle inizia a mostrare un miglioramento nella compattezza e luminosità. L'acido ialuronico ha iniziato a idratare i tessuti dall'interno.

Dopo 2-3 mesi: la differenza è evidente. La pelle è più compatta, più elastica, più luminosa. I capelli sono più spessi e forti. Le articolazioni hanno recuperato mobilità. Chi smette dopo 3 mesi nota un peggioramento graduale.

Uso continuativo (6+ mesi): la cartilagine si rigenera progressivamente. La pelle mantiene la compattezza. È il punto in cui il collagene diventa parte della routine quotidiana.

---

**[BLOCCO 3 — HURRICANE]**
*Show condition: Items contains "Hurricane"*

**Cosa aspettarti da Hurricane**

Hurricane è diverso dagli altri integratori: non aspettare "settimane per vedere risultati". L'effetto è immediato e legato all'allenamento.

15-20 minuti dopo averlo bevuto: il guaranà e la sinefrina iniziano ad agire. Senti più energia e concentrazione, la citrullina e l'arginina iniziano la vasodilatazione (pump muscolare).

Durante l'allenamento: la creatina alimenta gli sforzi esplosivi, la beta-alanina tampona l'acidosi muscolare (meno bruciore), il magnesio previene i crampi.

Dopo 4-6 settimane di uso costante: la creatina raggiunge la saturazione completa nei muscoli. Tieni presente che assumendo Hurricane solo nei giorni di allenamento (3-4 volte a settimana) la saturazione richiede qualche settimana in più rispetto a un uso quotidiano. È il punto in cui inizi a notare miglioramenti più stabili nella forza e nella resistenza, non solo durante il singolo allenamento.

---

**[BLOCCO 4 — ARMAGEDDON]**
*Show condition: Items contains "Armageddon"*

**Cosa aspettarti da Armageddon**

Armageddon è una formula di aminoacidi essenziali: il suo effetto è legato al recupero e alla protezione muscolare, non a "sensazioni" durante l'allenamento.

Subito: durante o dopo l'allenamento gli aminoacidi entrano in circolo rapidamente. La leucina attiva i meccanismi di sintesi proteica, il triptofano (precursore di serotonina e melatonina) supporta umore e qualità del sonno, due fattori chiave per il recupero.

Dopo 2-4 settimane: noti un recupero più rapido tra una sessione e l'altra, meno indolenzimento muscolare il giorno dopo, meno catabolismo nelle sessioni lunghe (utile per sport di endurance come tennis o corsa).

Uso continuativo: se hai più di 40 anni e ti alleni con i pesi, Armageddon è un alleato contro la sarcopenia. Se segui una dieta ipoproteica o vegetariana, ti aiuta a colmare il gap aminoacidico essenziale.

---

**[BLOCCO 5 — ARTOSAN]**
*Show condition: Items contains "Artosan"*

**Cosa aspettarti da Artosan**

Artosan ha tempi più rapidi degli altri integratori, perché la curcumina liposomiale ha un effetto anti-infiammatorio relativamente veloce.

Primi 4-7 giorni: chi ha infiammazione acuta può notare un miglioramento rapido. Il dolore articolare attivo si attenua, la mobilità migliora. È la fase in cui Artosan dà i risultati più visibili.

Dopo 2-4 settimane: l'effetto anti-infiammatorio si consolida. Il dolore cronico si attenua, la boswellia e l'artiglio del diavolo raggiungono la massima efficacia con l'uso continuativo.

Dopo 1-3 mesi: i benefici strutturali iniziano a emergere. Il silicio dal bamboo e l'MSM supportano la riparazione dei tessuti. Chi affianca Artosan a Youth o Jeunesse nota un miglioramento superiore alla somma dei due.

Uso continuativo: mantenimento della protezione anti-infiammatoria e prevenzione del peggioramento.

---

**[BLOCCO 6 — LIVERTY]**
*Show condition: Items contains "Liverty"*

**Cosa aspettarti da Liverty**

Prime 2 settimane: miglioramento della digestione grazie a cardo mariano e zenzero. Meno pesantezza dopo i pasti, meno gonfiore. Il NAC inizia a ripristinare i livelli di glutatione epatico.

Dopo 1 mese: la funzione epatica migliora in modo tangibile. Più energia (un fegato efficiente significa un metabolismo più efficiente). La pelle può migliorare, perché il fegato gestisce l'eliminazione delle tossine che spesso si manifestano sulla cute.

Dopo 2-3 mesi: i benefici si consolidano. Chi fa analisi può notare miglioramenti nei valori epatici (transaminasi) e lipidici (colesterolo, trigliceridi). Chi assume farmaci cronicamente riferisce di tollerarli meglio.

Uso continuativo: protezione epatica costante. Particolarmente utile per chi vive in città, consuma alcol anche moderatamente, assume farmaci o ha una dieta non perfetta.

---

**[BLOCCO 7 — TESTOPLUS]**
*Show condition: Items contains "Testoplus"*

**Cosa aspettarti da Testoplus**

Prime 2 settimane: l'ashwagandha inizia a ridurre il cortisolo, con miglioramento del sonno e della gestione dello stress. La maca può dare un boost energetico percepibile. I tonici (muira, damiana) iniziano a lavorare sulla libido.

Dopo 1 mese: l'energia è più costante. La libido migliora. La forza in palestra aumenta. L'umore è più stabile. Il tribolo e la forskolina hanno avuto tempo di supportare la produzione di testosterone.

Dopo 2-3 mesi: i benefici si consolidano. Chi fa analisi può notare un miglioramento dei livelli di testosterone totale e libero. La composizione corporea migliora (meno grasso viscerale, più massa magra).

Uso continuativo: il supporto ormonale è un percorso continuo, non un ciclo unico. Chi smette nota un calo graduale.

---

**[BLOCCO 8 — RENAISSANCE]**
*Show condition: Items contains "Renaissance"*

**Cosa aspettarti da Renaissance**

Renaissance lavora su meccanismi cellulari profondi (anti-aging, senolitici, NAD+, telomeri). Per natura i tempi sono più lunghi di un multivitaminico.

Prime 2 settimane: gli effetti della berberina sulla glicemia possono essere percepibili (più stabilità energetica dopo i pasti). L'effetto tonico del tè verde EGCG si sente subito. La nicotinammide riboside inizia a ripristinare i livelli di NAD+.

Dopo 1 mese: l'energia migliora, non in modo esplosivo ma come una costanza nuova. La stabilità glicemica è evidente. I senolitici hanno iniziato il lavoro di pulizia cellulare.

Dopo 2-3 mesi: è il periodo minimo consigliato per valutare i risultati. L'autofagia (spermidina) ha avuto tempo di fare pulizia profonda. Chi fa analisi può notare miglioramenti nei marker infiammatori e nel profilo lipidico.

Uso continuativo (6+ mesi): i benefici strutturali si accumulano. Renaissance è un investimento sulla qualità della vita futura: i benefici più profondi non si "sentono" oggi ma si vedranno negli anni a venire nella differenza tra chi ha fatto prevenzione cellulare e chi no.

---

**[BLOCCO 9 — VITAMINA D IN GOCCE]**
*Show condition: Items contains "Vitamina D"*

**Cosa aspettarti dalla Vitamina D in gocce**

Dopo 2-4 settimane: i livelli ematici di 25(OH)D iniziano a salire. Effetti percepibili su umore ed energia, se la carenza era significativa.

Dopo 2-3 mesi: i livelli si stabilizzano. Il sistema immunitario è più reattivo. Le ossa beneficiano dell'aumentato assorbimento di calcio. Il miglioramento è documentabile con un'analisi del sangue (25(OH)D).

Uso continuativo: la vitamina D è una supplementazione che ha senso a vita per chi vive in Italia, specialmente da ottobre a marzo quando il sole non basta a stimolare la produzione cutanea. Mantenere il 25(OH)D tra 50 e 80 ng/ml richiede integrazione costante: controlla i livelli a fine marzo e fine settembre per regolare il dosaggio.

---

**Tronco comune — chiusura**

Una cosa che voglio chiarire: l'integrazione non è una pillola che provi per giudicarla. È un investimento sul tempo. La differenza tra chi vede risultati e chi no è quasi sempre la costanza. **Tre mesi continuativi** è il minimo per giudicare onestamente. Otto-dieci settimane invece sono il punto in cui la maggior parte delle persone abbandona, prima di vedere il vero beneficio.

Se sei a 5 giorni dall'inizio e "non senti niente", è perfettamente normale. Continua. Tra qualche settimana riparliamo.

**Più avanti** ti darò qualche consiglio pratico per amplificare i risultati senza spendere altro. Niente integratori in più, solo abitudini che fanno la differenza.

Un forte abbraccio
Lorenzo Zarone
Fondatore di Paleocomplex

---

**P.S. SOLO per chi non ha accettato marketing al checkout:**

*P.S. Questa è un'email di servizio sul tuo ordine. Se vuoi continuare a ricevere contenuti come questo, puoi iscriverti alla nostra newsletter [link]. Niente spam, solo cose utili.*

---

## EMAIL 4 — Ottimizza i risultati (+12 giorni)

**Mittente:** Lorenzo Zarone
**Tipo:** Statica (uguale per tutti)

### Oggetto (3 varianti A/B)

- A: Come tirare fuori il massimo da qualunque integratore
- B: 5 abitudini che amplificano i tuoi risultati
- C: Il segreto è quello che fai intorno all'integratore

### Preview text (3 varianti)

- A: Niente di esoterico. Solo le 5 cose che funzionano davvero.
- B: L'integratore amplifica. Non sostituisce.
- C: Cinque abitudini che cambiano davvero la qualità della vita.

### Corpo email

Ciao [NOME]

Sei a metà del primo mese. Probabilmente stai iniziando a notare qualcosa, o stai aspettando che succeda. In entrambi i casi, oggi voglio darti qualcosa di gratuito.

Ci sono cinque abitudini che amplificano l'effetto di qualunque integratore tu prenda. Non solo quello che hai comprato da noi: qualunque. La verità è che gli integratori non sostituiscono uno stile di vita scarso, lo amplificano dove è già buono.

**Idratazione.** Almeno 1,5-2 litri di acqua al giorno (di più se ti alleni o fa caldo). Senza acqua sufficiente, le vitamine idrosolubili che assumi vengono eliminate prima che il corpo le utilizzi a pieno.

**Sonno.** Sette-otto ore regolari. Il sonno è il momento in cui il corpo ripara, rigenera e consolida. Tutti i nutrienti che assumi durante il giorno vengono utilizzati molto meglio se dormi bene. Se vuoi approfondire, sul nostro blog c'è una **[guida completa al sonno basata su evidenze scientifiche](https://paleocomplex.com/limportanza-della-dieta-e-degli-integratori-per-un-sonno-perfetto-suggerimenti-basati-su-evidenze-scientifiche/)** che spiega ritmo circadiano, luce blu, alimentazione e integrazione.

**Sole.** Da aprile a settembre esponiti almeno 15-20 minuti al giorno con braccia e gambe scoperte. La vitamina D che produci col sole è perfettamente regolata dal tuo corpo, cosa che nessun integratore può replicare. Su **[come esporsi correttamente al sole in base alla zona d'Italia](https://paleocomplex.com/sole-vitamina-d/)** trovi una guida pratica con tabelle per fototipo e latitudine.

**Movimento.** Non serve la palestra. Una camminata di 30 minuti al giorno migliora sensibilità insulinica, infiammazione, sonno, umore e assorbimento dei nutrienti. Qualsiasi forma di esercizio va bene, l'importante è inserirlo all'interno della propria routine e mantenerlo nel tempo. È il consiglio più sottovalutato di tutti.

**Alimentazione.** Riduci gli alimenti ultra-processati. Più cibo intero (verdure, frutta, pesce, uova, legumi), meno cibo da pacchetto. Non serve essere fanatici: anche solo passare dal 70% al 50% di processati nella tua dieta cambia molto. Per capire cosa privilegiare e cosa evitare, c'è una guida sull'**[alimentazione antinfiammatoria](https://paleocomplex.com/alimentazione-antinfiammatoria-e-quali-cibi-consumare/)** sul blog.

Se fai queste cinque cose, il tuo integratore lavora al massimo del suo potenziale. Se non le fai, anche il miglior integratore del mondo rende la metà.

**Tra qualche giorno** ti scrivo per sapere come stai andando. Se nel frattempo hai domande, scrivici a info@paleocomplex.com.

Un forte abbraccio
Lorenzo Zarone
Fondatore di Paleocomplex

---

## EMAIL 5 — Social proof + check-in (+18 giorni)

**Mittente:** Flaminia (Customer Care)
**Tipo:** Tronco comune + 9 blocchi dinamici (Show/Hide su Items dell'ordine). Tutte le recensioni sono verificate dal CSV `context/2026 03 31 paleocoplex export-reviews.csv`. Per Testoplus e Renaissance non ci sono recensioni utilizzabili (solo recensioni generiche tipo "ottimo prodotto"), quindi i blocchi specifici contengono un check-in onesto senza testimonianze.

### Oggetto (3 varianti A/B)

- A: Come sta andando?
- B: Sono passate quasi tre settimane
- C: Volevo sentirti

### Preview text (3 varianti)

- A: Sono Flaminia, faccio parte del team di Lorenzo. Mi farebbe piacere sapere come va.
- B: Una piccola pausa dalla teoria. Oggi qualche storia vera.
- C: Ho raccolto qualche esperienza che potrebbe interessarti.

### Corpo email

**Tronco comune — apertura**

Ciao [NOME]

Ti scrivo io questa volta. Sono Flaminia e mi occupo del rapporto con i clienti di Paleocomplex. Lorenzo si occupa della parte tecnica e scientifica, io invece sono il punto di contatto umano: rispondo a chi ci scrive, ascolto i feedback, raccolgo storie. Ed è proprio per questo che oggi voglio scriverti.

Sono passate circa 2-3 settimane da quando hai iniziato il tuo prodotto. È un momento interessante: alcune persone iniziano a notare qualcosa, altre sono ancora nella fase di pazienza che ti aveva descritto Lorenzo. In entrambi i casi può essere utile leggere le esperienze di chi è passato dallo stesso punto in cui sei tu adesso.

Ti lascio qualche storia vera. Sono tutte recensioni di clienti verificati, ognuna con la sua tempistica e il suo modo di raccontare.

---

**[BLOCCO 1 — MULTIVITAMINICI]**
*Show condition: Items contains "Paleocomplex" OR "Revolution" OR "Elisir" OR "Elisir Basic" OR "Essentiel"*

**Storie con i nostri multivitaminici**

*"Il Paleocomplex Revolution è il prodotto che da quando l'ho acquistato per la prima volta a Ottobre 2024, mi ha cambiato totalmente la vita, dato che mi permette di avere molta più energia. Lungo la giornata riesco a portare a termine molte più cose con maggiore facilità, praticamente mi dà molta più forza di vivere la mia vita con maggiore intensità."*
**Mario Ricci** (Paleocomplex Revolution)

*"Un equilibrato apporto di vitamine che migliora lo stato generale di salute, rinforza il metabolismo e dà una sensazione generale di benessere ed energia. Ho 68 anni e non prendo altro se non integratori omeopatici di supporto."*
**Flavio** (Elisir Basic)

*"Sono uno psicologo, fisioterapista, erborista, laureato in scienze motorie. Molto attento alla salute vera e non come persuasione commerciale. Il prodotto mi ha fornito energia sia nella vita che negli allenamenti, una scomparsa di dolori articolari e di una noiosissima dermatite seborroica. In più i miei livelli di vitamina D sono saliti in poco tempo da 19 a 60."*
**Massimo Camelo** (Paleocomplex)

I risultati sono personali, dipendono dalle condizioni di partenza e dallo stile di vita. Se col solo multivitaminico non raggiungi livelli ottimali di vitamina D (sopra i 40 ng/ml), il consiglio non è raddoppiare la dose del multivitaminico ma aggiungere le **[gocce di Vitamina D](https://paleocomplex.com/prodotto/vitamina-d/)**: 4 gocce al giorno coprono la maggior parte dei casi.

---

**[BLOCCO 2 — COLLAGENE]**
*Show condition: Items contains "Youth" OR "Jeunesse"*

**Storie con il collagene**

*"Dopo soli 10 giorni di assunzione la mia pelle è diventata più morbida e liscia, i capelli più corposi e robusti. Un integratore davvero favoloso. Consigliatissimo."*
**Manuela** (Youth)

*"Promuovo questo prodotto come uno dei migliori in assoluto. Pelle in assoluto migliorata, ho 40 anni e vi assicuro che neanche a 20 l'avevo così elastica e bella. Capelli folti e lucenti e ottimo risultato anche alle ciglia. Fantastico prodotto, non credo proprio di mollarlo mai."*
**Alice B.** (Jeunesse)

*"Non ne posso fare a meno, ottimo prodotto. Unghie durissime, capelli più folti."*
**Anna** (Jeunesse)

I risultati arrivano con la costanza. Per il collagene **3 mesi continuativi** sono il minimo per giudicare onestamente.

---

**[BLOCCO 3 — HURRICANE]**
*Show condition: Items contains "Hurricane"*

**Storie con Hurricane**

*"Preso per preparare la traversata dello Stretto di Messina a nuoto, abbinato ad Armageddon, sto notando minor affaticamento post allenamento e pronto per le sessioni successive. Consigliatissimo."*
**Raffaele C.**

*"Veramente ti dà una carica nello stesso momento. Si abbassa anche la pressione, che io l'avevo alta. Favoloso, bravo Lorenzo."*
**Donato I.**

---

**[BLOCCO 4 — ARMAGEDDON]**
*Show condition: Items contains "Armageddon"*

**Storie con Armageddon**

*"Ottimo prodotto. Facile da assumere. La mia resistenza durante gli allenamenti è migliorata, e anche la massa magra. Consiglio vivamente questi aminoacidi a chiunque cerchi di migliorare le proprie prestazioni sportive o semplicemente di sostenere il proprio benessere generale."*
**Mariella C.**

*"A differenza di integratori di altre marche che ho provato, questo è il migliore sia come gusto che come qualità della polvere. Si scioglie bene in acqua e non mi disturba a livello gastrointestinale. Top."*
**Laura C.**

*"Una spinta psicofisica per chi si sottopone ad allenamenti importanti. La formulazione è molto bilanciata per non incorrere in carenze di aminoacidi essenziali."*
**Marco B.**

---

**[BLOCCO 5 — ARTOSAN]**
*Show condition: Items contains "Artosan"*

**Storie con Artosan**

*"Perfetto. Preso una capsula al giorno, dopo quattro giorni sono tornato a camminare normalmente, dolore quasi sparito completamente, ginocchio nella norma."*
**Gian Filippo R.**

*"Ottimo prodotto, sono migliorati i dolori al mio ginocchio, assumendo insieme anche Youth."*
**Anna**

*"Ho risolto un problema infiammatorio."*
**Mirella F.**

---

**[BLOCCO 6 — LIVERTY]**
*Show condition: Items contains "Liverty"*

**Storie con Liverty**

*"Che dire... mi si è abbassato il colesterolo, che avevo molto, troppo alto. Fantastico."*
**Daniela M.**

*"Da quando lo prendo la mia digestione è ottima."*
**Gianfranco**

---

**[BLOCCO 7 — TESTOPLUS]**
*Show condition: Items contains "Testoplus"*

**Storie con Testoplus**

Su Testoplus le recensioni pubbliche sono ancora poche perché è un prodotto entrato più di recente nel nostro catalogo. Ma uno dei messaggi più importanti che Lorenzo ha ricevuto è proprio una testimonianza concreta con i numeri delle analisi del sangue:

*"Ti mando il valore del testosterone prima dell'utilizzo del Testoplus e dopo 2 mesi di integrazione: livelli di testosterone passati da 5,34 a 644."*
**Messaggio di un cliente dopo 2 mesi**. Una trasformazione incredibile ma ci tengo a precisare che ogni risultato è soggettivo.

È esattamente il tipo di feedback che ci interessa: documentato, misurabile, onesto. Se nelle prossime settimane noti cambiamenti (energia, libido, recupero, o se fai analisi ormonali), **rispondi pure a questa email** raccontandomi com'è andata: per me è prezioso sentire la tua esperienza diretta.

---

**[BLOCCO 8 — RENAISSANCE]**
*Show condition: Items contains "Renaissance"*

**Storie con Renaissance**

Renaissance è un integratore particolare: non è un multivitaminico, è un prodotto avanzato per la longevità cellulare. Lavora su meccanismi profondi come senolitici, autofagia, NAD+ e supporto telomerico. Per natura i benefici più importanti non si "sentono" nel breve termine: si vedono nel lungo periodo, sulla qualità dell'invecchiamento.

Le prime recensioni che riceviamo riflettono proprio questo:

*"Ottimo integratore, ricco di ingredienti. Completi."*
**Sandra S.**

*"Qualità ed efficacia."*
**Cliente verificato**

Sono testimonianze brevi e generali: è il tipo di feedback che ci si aspetta da un prodotto i cui effetti più profondi (markers infiammatori, profilo lipidico, autofagia) sono documentabili nel medio-lungo periodo. Se nei prossimi mesi farai analisi e noti cambiamenti misurabili, **rispondi pure a questa email** raccontandomi i numeri: per noi è il modo migliore di costruire social proof su un prodotto con benefici a lungo termine.

---

**[BLOCCO 9 — VITAMINA D IN GOCCE]**
*Show condition: Items contains "Vitamina D"*

**Storie con la Vitamina D**

*"Ne prendo sempre 4 gocce al mattino e i risultati si vedono, specialmente con la mia patologia di artrite reumatoide."*
**Stefano O.**

*"Ho piena fiducia nei prodotti proposti da Paleocomplex, non ho bisogno di essere convinta sull'assunzione della Vitamina D in gocce. Consigliata a tutti."*
**Cinzia G.**

I risultati sono personali. La Vitamina D è uno dei pochi integratori i cui effetti si possono misurare oggettivamente con un'analisi del sangue (25(OH)D): per capire se il dosaggio è quello giusto per te, controlla i livelli dopo 3 mesi e regola di conseguenza.

---

**Tronco comune — chiusura**

Una cosa importante: queste sono storie di persone reali, ma non sono "garanzie". Ogni corpo risponde a tempi suoi. Se a questo punto non stai notando ancora cambiamenti, non significa che il prodotto non stia funzionando: significa solo che il tuo corpo ha bisogno di più tempo per riempire le riserve. Continua.

E se invece hai già notato qualcosa, mi farebbe davvero piacere saperlo. **Rispondi pure a questa email** raccontandomi com'è andata: per me è il modo migliore di lavorare, sapendo cosa cambia davvero nella vita delle persone che ci scelgono.


Flaminia
Customer Care Paleocomplex

---

## EMAIL 6 — Richiesta recensione (+32 giorni)

**Mittente:** Flaminia (Customer Care)
**Tipo:** Statica (uguale per tutti)

### Oggetto (3 varianti A/B)

- A: Tra poco riceverai una mia richiesta. Te la anticipo.
- B: Una cosa veloce, se hai 2 minuti
- C: Il tuo parere mi farebbe davvero piacere

### Preview text (3 varianti)

- A: Il tuo voto vale più di mille slogan.
- B: Riceverai un'email con oggetto "⭐⭐⭐⭐⭐ Quante stelle daresti a Paleocomplex?"
- C: Bastano pochi minuti per condividere la tua esperienza.

### Corpo email

Ciao [NOME]

Ti scrivo io questa volta. Sono Flaminia e mi occupo del rapporto con i clienti di Paleocomplex.

Sono passate circa quattro settimane da quando hai ricevuto il tuo ordine. Hai avuto il tempo di provare il prodotto, di capire se ti trovi bene con il sapore o la praticità d'uso, e magari di iniziare a notare qualche cambiamento.

Ho una piccola richiesta da farti.

Tra poche ore riceverai un'email automatica dal nostro sistema con oggetto **"⭐⭐⭐⭐⭐ Quante stelle daresti a Paleocomplex?"**. È un invito ufficiale a lasciare una recensione sul prodotto che hai comprato.

Per noi le recensioni dei clienti contano davvero. Più di qualunque pubblicità che potremmo fare. Il mondo degli integratori è pieno di promesse vuote e prodotti che non mantengono quello che dichiarano. Le recensioni reali sono l'unico modo che hanno le persone serie di capire chi vale la pena ascoltare.

Non serve scrivere un trattato. Bastano un voto e qualche parola su quello che hai notato. Anche solo "energia più stabile durante la giornata" o "pelle più morbida dopo tre settimane" è prezioso. E se hai trovato qualcosa che non ti convince, dillo: i feedback meno entusiastici sono quelli che ci aiutano a migliorare.

Se non trovi l'email tra qualche ora controlla in spam o posta indesiderata.

Grazie davvero per la fiducia che ci hai dato finora.

Flaminia
Customer Care Paleocomplex

---

## Note operative trasversali

### Disclaimer marketing optin
Per i contatti che NON hanno espresso consenso al marketing al momento dell'acquisto, aggiungere un P.S. soft nelle email 2 e 3 con invito all'iscrizione. Non prioritario (99,9% dei nuovi clienti ha già autorizzato).

### CTA per email
- Email 1: nessuna CTA esplicita, solo info@ in caso di problemi
- Email 2: link interno a guida assunzione + info@ per dubbi (da definire nei blocchi)
- Email 3: nessuna CTA forte (è educativa); rimando a scheda prodotto solo per "Specifici"
- Email 4: 3 link inline a articoli blog (sonno, sole, alimentazione)
- Email 5: invito a rispondere alla mail (no link esterni); eventuale link a gocce Vitamina D nel disclaimer
- Email 6: nessuna CTA (l'azione è sulla mail di sistema successiva)

### Open loop tra email
- Email 1 → 2: "Domani ti spiego come assumere correttamente il prodotto"
- Email 2 → 3: "Tra qualche giorno ti dico cosa aspettarti dalle prime settimane"
- Email 3 → 4: "Più avanti ti darò consigli per amplificare i risultati"
- Email 4 → 5: "Tra qualche giorno ti scrivo per sapere come stai andando"
- Email 5 → 6: nessun open loop (la 6 è transazionale)

### Filtro accessori
Il flow NON parte se l'ordine contiene SOLO Lampada Apollo, occhiali blue blocker, libri.
Trigger filter: ordine deve contenere almeno 1 integratore.

### Rinforzo Lorenzo / Flaminia
- Lorenzo nelle email 1-4 (autorità, voce educativa)
- Flaminia nelle email 5-6 (umano, customer care)
- La firma standardizzata di Flaminia: "Flaminia · Customer Care Paleocomplex"
