**Versione:** 2.3
**Ultimo aggiornamento:** 2026-04-15
**Status:** Bozza v2 — in attesa review Andrea

# Flow 2: Welcome Kit Benessere

## Chi entra in questo flow

Tutti i nuovi contatti che si iscrivono alla lista tramite il **Welcome Kit del Benessere**, da qualsiasi fonte:

**Con sconto promesso (popup/blog/homepage):**
- Popup sul sito (compare su tutte le pagine)
- Form alla fine di ogni post del blog
- Form nella homepage

**Senza sconto promesso (landing social):**
- Landing page sponsorizzata sui social: `paleocomplex.com/7-strategie-scientifiche-dopo-40anni/`

In entrambi i casi ricevono lo stesso flow. Lo sconto BENVENUTO viene presentato come "regalo di benvenuto", così funziona sia per chi se lo aspettava sia per chi lo scopre come sorpresa.

**Cosa ricevono:**
- Il report gratuito **"Le 7 Strategie Scientifiche per corpo forte, mente lucida e più energia dopo i 40 anni"**
- Lo sconto di **€10 sul primo acquisto** (codice BENVENUTO)
- 5 email di nurturing in 10 giorni

**Chi sono queste persone:**
Persone 40+ interessate a salute, longevità, energia e integrazione. Molti arrivano da ads social, non conoscono ancora il brand. Il livello di consapevolezza è basso-medio: sanno di voler "stare meglio" ma non sanno ancora perché Paleocomplex è diverso.

**Tema dominante del report:** anti-aging, energia mitocondriale, protezione DNA, ritmo circadiano. I prodotti citati in questo flow devono essere coerenti con questo tema (Elisir, Revolution, Essentiel, Renaissance — NO Paleocomplex base che è per under 40).

## Configurazione Klaviyo

**Trigger:** Added to List (lista "Welcome Kit Benessere")
**Mittente:** Lorenzo Zarone (tutte le email del flow)
**Filtri profilo:**
- Has not been in this flow before

**Uscita dal flow:**
- Se il contatto effettua un acquisto durante il flow → esce e entra nel **Post Purchase New Customer (flow 6)**
- Se completa il flow senza acquistare → entra nell'**Authority Flow (flow 4)**

**Relazione con Authority Flow:**
Authority parte DOPO il completamento di questo welcome (sequenziale, NON in parallelo). Questo evita sovrapposizioni e bombardamento. La storia di Lorenzo è in questo flow (email 3), quindi l'Authority non la ripete.

**Note tecniche:**
- Codice BENVENUTO: €10 fissi, solo primo acquisto, valido su tutti i prodotti
- Il report va consegnato come link diretto al PDF (o link alla pagina di download)
- Taggare la provenienza del contatto (popup vs social) come proprietà profilo per analytics

---

## EMAIL 1 — Delivery report + sconto benvenuto (immediata)

### Oggetto (3 varianti A/B)

- A: Ecco il tuo report + un regalo di benvenuto
- B: Le 7 strategie scientifiche sono pronte per te
- C: Il tuo percorso verso più energia inizia qui

### Preview text (3 varianti)

- A: Scarica il report e scopri il tuo regalo di €10.
- B: 47 studi, 7 strategie, 1 protocollo da 30 giorni.
- C: Il report che hai richiesto è pronto.

### Corpo email

Ciao [NOME]

Da oggi fai parte del mondo Paleocomplex.

Ecco il report che hai richiesto: **"Le 7 Strategie Scientifiche per corpo forte, mente lucida e più energia dopo i 40 anni."**

**[CTA: Scarica il tuo report gratuito]**
(link al PDF)

All'interno troverai un protocollo di 30 giorni basato su 47 studi scientifici, con strategie concrete su energia mitocondriale, infiammazione silente, protezione del DNA e ritmo circadiano. Non è il solito elenco generico di consigli: è un piano d'azione con routine mattutina e serale.

Come regalo di benvenuto, ho anche un **codice sconto di €10 sul tuo primo acquisto**: **BENVENUTO**.

Il codice è valido su tutti i prodotti dello store, senza limiti di spesa.

**[CTA: Vai allo store e usa il tuo sconto](https://paleocomplex.com)**

**Tra un paio di giorni** ti voglio raccontare una cosa che la maggior parte dei brand di integratori non vuole farti sapere: perché prendere 10 prodotti separati è quasi sempre uno spreco di soldi. E come fare a capire se quello che hai nel cassetto sta davvero funzionando o no.

Un forte abbraccio
Lorenzo Zarone
Fondatore di Paleocomplex

---

## EMAIL 2 — Perché un multivitaminico completo batte 10 separati (+2 giorni)

### Oggetto (3 varianti A/B)

- A: Il problema degli integratori che nessuno ti dice
- B: Perché prendere 10 integratori separati non funziona
- C: La differenza tra integrare e integrare bene

### Preview text (3 varianti)

- A: La maggior parte delle persone sta buttando soldi.
- B: Più prodotti non significa più risultati.
- C: Quello che i brand di integratori non vogliono che tu sappia.

### Corpo email

Ciao [NOME]

Eccomi con quello che ti avevo promesso. Ti faccio una domanda diretta: quanti integratori hai nel cassetto in questo momento?

Se la risposta è "più di tre", probabilmente stai facendo quello che fanno quasi tutti. Un integratore per la vitamina D, uno per il magnesio, uno per gli omega-3, uno per le vitamine B, uno per gli antiossidanti. Cinque prodotti diversi, cinque etichette da leggere, cinque aziende diverse con standard diversi.

Il problema non è la buona intenzione. Il problema è che **la maggior parte di questi prodotti ha dosaggi simbolici**.

Ti faccio un esempio concreto. Prendi un multivitaminico da supermercato e guarda l'etichetta. Troverai scritto "Vitamina B12: 2,5 mcg (100% VNR)". Quel 100% è il **minimo per non avere carenze**. Non è il dosaggio per stare bene davvero.

In Elisir, il nostro multivitaminico più completo, la B12 è a **200 mcg nella forma metilata** (8000% del VNR). La forma metilata è quella che il tuo corpo può usare direttamente, senza doverla convertire. E lo stesso vale per ogni singolo ingrediente: forme attive, dosaggi reali, nessun riempitivo.

Il risultato? **Un solo prodotto al giorno che sostituisce 15-20 integratori separati.** E che costa meno della somma dei singoli: Elisir costa €3,47 al giorno. Gli stessi ingredienti comprati separatamente nelle stesse forme costerebbero tra €302 e €460 per 40 giorni.

E non solo. Anche con mezzo misurino, Elisir sarebbe comunque di gran lunga superiore a qualsiasi multivitaminico da banco. A metà dose avresti ancora la B12 a 100 mcg (40 volte la dose che trovi al supermercato), la vitamina C a 250 mg in forma liposomiale, e tutti gli antiossidanti che nei prodotti da banco semplicemente non esistono. Per 80 giorni, con una spesa di poco più di un euro e mezzo al giorno.

Non ti chiedo di credermi sulla parola. Ti chiedo di confrontare le etichette.

**[CTA: Scopri i nostri multivitaminici](https://paleocomplex.com/guida-scelta)**

Ricorda che hai ancora il tuo sconto di benvenuto: **codice BENVENUTO** per €10 sul primo acquisto.

Un forte abbraccio
Lorenzo Zarone
Fondatore di Paleocomplex

---

## EMAIL 3 — Chi è Lorenzo + perché Paleocomplex esiste (+4 giorni)

### Oggetto (3 varianti A/B)

- A: Perché ho creato Paleocomplex
- B: La storia dietro ai nostri integratori
- C: Tutto è iniziato da una frustrazione

### Preview text (3 varianti)

- A: Non è nato come business. È nato come necessità.
- B: La mia storia con gli integratori è iniziata come la tua.
- C: C'era un problema che nessuno risolveva.

### Corpo email

Ciao [NOME]

Mi chiamo Lorenzo Zarone. Sono laureato in Scienze Motorie con specializzazione in Nutrizione e Nutraceutica, e sono il fondatore di Paleocomplex.

Ti racconto in breve perché questo brand esiste.

Anni fa, studiando nutrizione e integrazione, mi sono reso conto di una cosa che mi ha frustrato profondamente: **la maggior parte degli integratori sul mercato non funziona**. Dosaggi ridicoli, forme economiche che il corpo fatica ad assorbire, etichette che sembrano impressionanti ma che nascondono il nulla.

Ho provato a cercare un multivitaminico che avesse tutto quello che serviva: dosaggi terapeutici reali, vitamine in forma attivata, minerali biodisponibili, antiossidanti di ultima generazione. Non esisteva.

Così l'ho creato.

**Paleocomplex è nato dalla volontà di avere un solo prodotto che facesse davvero la differenza.** Non un compromesso. Non un "meglio di niente". Un integratore che potessi consigliare a mia madre, ai miei amici, ai miei clienti, sapendo esattamente cosa c'è dentro e perché.

Oggi siamo il brand di integratori con le formulazioni più complete e trasparenti sul mercato italiano. Ogni ingrediente ha una ragione precisa. Ogni dosaggio è studiato per avere un effetto reale. E l'etichetta ti dice tutto, senza nascondere nulla.

Non vendo integratori. **Vendo la possibilità di semplificare la tua integrazione senza compromessi sulla qualità.**

Se vuoi saperne di più, sul nostro sito trovi tutto: ingredienti, dosaggi, spiegazioni, confronti. Trasparenza totale.

**[CTA: Scopri i nostri prodotti](https://paleocomplex.com)**

**Tra qualche giorno** voglio mostrarti tre prodotti specifici, scelti tra tutti quelli che abbiamo creato, e dirti onestamente quale fa per te in base alla tua situazione. Ti racconterò anche cosa dicono le persone che li usano da mesi.

Un forte abbraccio
Lorenzo Zarone
Fondatore di Paleocomplex

---

## EMAIL 4 — Il prodotto giusto per te + social proof (+7 giorni)

### Oggetto (3 varianti A/B)

- A: Quale integratore è il più adatto a te?
- B: Energia, lucidità, protezione: ecco da dove partire
- C: Cosa scegliere dopo i 40 anni (la risposta è più semplice di quanto pensi)

### Preview text (3 varianti)

- A: Tre prodotti, tre esigenze diverse. Ecco come orientarti.
- B: La guida rapida per chi vuole iniziare con il piede giusto.
- C: Ecco cosa usano le persone come te.

### Corpo email

Ciao [NOME]

Eccomi con i tre prodotti che ti avevo promesso. Nel report che hai scaricato si parla di energia mitocondriale, infiammazione silente, protezione del DNA e stress ossidativo. Sono tutti meccanismi che si accelerano dopo i 40 anni.

La buona notizia è che puoi agire concretamente su ognuno di essi. E non servono 15 integratori diversi.

**Ecco le tre opzioni più adatte a te.**

**Elisir:** il più completo in assoluto. 40 nutrienti in un misurino al giorno: Omega-3 da Krill, glutatione liposomiale, quercetina fitosomiale, ubiquinolo, trans-resveratrolo, vitamine attivate. È la risposta diretta a tutte le 7 strategie del report. **€3,47/giorno per 40 giorni.**

**Revolution:** antiossidanti avanzati (glutatione liposomiale, ubiquinolo, astaxantina, vitamina C liposomiale) per chi vuole una protezione forte senza il costo massimo. 26 nutrienti, ideale per chi ha superato i 40. **€3,97/giorno per 30 giorni.**

**Essentiel:** 34 nutrienti con un focus sulla mente. Tra questi, citicolina e acetil-carnitina per lucidità mentale e funzione cognitiva. Zero crostacei. Il miglior rapporto qualità/prezzo della gamma. **€2,15/giorno per 60 giorni.**

Il multivitaminico è il punto di partenza. Ma se vuoi andare ancora più a fondo sulle strategie anti-aging del report, ci sono due prodotti specifici che completano il protocollo:

**Renaissance:** 13 nutraceutici mirati alla protezione cellulare e alla longevità. Contiene NR (Nicotinammide Riboside, precursore del NAD+), ubiquinolo, trans-resveratrolo e quercetina fitosomiale. È il complemento ideale al multivitaminico per chi prende sul serio la strategia anti-aging. **€89 per 30 giorni.**

**Jeunesse:** 12g di collagene bovino grass-fed al giorno, acido ialuronico e antiossidanti per pelle, capelli e articolazioni. Quando parliamo di "ricostruzione del collagene" nel report, questo è lo strumento. **€99 per 50 giorni.**

Non sai da dove partire? **[CTA: Vai alla guida alla scelta](https://paleocomplex.com/guida-scelta)**

Ecco cosa dicono alcune delle persone che hanno già fatto questa scelta:

**"Il meglio del meglio. Integrazione completa che tiene conto di ogni aspetto fondamentale: supporto nutrizionale, di energia, anti-età, antiossidante, mitocondriale, al sistema immunitario. Credo che al mondo non esista niente di meglio nel mondo dei nutraceutici."** Matteo A., Elisir

**"È da poco tempo che io e mia moglie assumiamo questo integratore ma i risultati sono stati veloci ad arrivare, la stanchezza è scomparsa, l'intestino lavora meglio, la pelle è più tonica. Siamo rimasti stupefatti."** Fabrizio G., Essentiel

**"Mi ha cambiato totalmente la vita. Lungo la giornata riesco a portare a termine molte più cose con maggiore facilità. Mi dà molta più forza di vivere la mia vita con maggiore intensità."** Mario R., Revolution

Il codice **BENVENUTO** è ancora attivo: **€10 di sconto sul primo acquisto**.

**[CTA: Scegli il tuo integratore](https://paleocomplex.com)**

Un forte abbraccio
Lorenzo Zarone
Fondatore di Paleocomplex

---

## EMAIL 5 — Ultima occasione (solo per chi NON ha acquistato) (+10 giorni)

### Condizione

**Split PRIMA dell'email:** Has Placed Order at least 1 time since starting this flow?
- **SÌ** → Esce dal flow (è già nel Post Purchase)
- **NO** → Riceve questa email

### Oggetto (3 varianti A/B)

- A: Il tuo sconto di €10 sta per scadere
- B: Un'ultima cosa prima di salutarti
- C: Non vorrei che te ne pentissi

### Preview text (3 varianti)

- A: Il codice BENVENUTO è ancora attivo, ma non per molto.
- B: Questa è l'ultima email sul tuo sconto di benvenuto.
- C: Ti avevo promesso di non essere insistente. Infatti questa è l'ultima.

### Corpo email

Ciao [NOME]

Questa è l'ultima volta che ti parlo del tuo sconto di benvenuto.

Nei giorni scorsi ti ho raccontato perché ho creato Paleocomplex, cosa ci rende diversi e perché un multivitaminico completo è meglio di dieci integratori separati.

Adesso la scelta è tua.

Il codice **BENVENUTO** ti dà ancora **€10 di sconto sul primo acquisto**, valido su qualsiasi prodotto. Ma non resterà attivo per sempre.

Se non sai da dove partire, il mio consiglio è semplice:

**Vuoi un multivitaminico completo per la tua età?** Abbiamo preparato una guida che ti aiuta a trovare quello giusto in 2 minuti, in base alla tua situazione e ai tuoi obiettivi.

**[CTA: Vai alla guida alla scelta](https://paleocomplex.com/guida-scelta)**

**Vuoi lavorare su pelle, capelli e articolazioni?** [Youth](https://paleocomplex.com/prodotto/youth/) e [Jeunesse](https://paleocomplex.com/prodotto/jeunesse/) sono i nostri integratori di collagene ad alto dosaggio, progettati per essere affiancati al multivitaminico.

**Vuoi un protocollo anti-aging completo?** La combinazione più potente è multivitaminico + [Renaissance](https://paleocomplex.com/prodotto/renaissance/) (13 nutraceutici mirati alla protezione cellulare e alla longevità).

**[CTA: Usa il codice BENVENUTO](https://paleocomplex.com)**

Dopo questa email continuerai a ricevere contenuti di valore sulla salute e sull'integrazione. Niente spam, solo cose utili. Ma lo sconto di benvenuto non tornerà.

Un forte abbraccio
Lorenzo Zarone
Fondatore di Paleocomplex

---

## Schema del flow

```
[Optin da popup / blog / homepage / landing social]
    │
    ▼
EMAIL 1 (immediata) — Delivery report + BENVENUTO €10
    │
    ├── Se acquista → esce → Post Purchase New (flow 6)
    │
    ▼  (+2 giorni)
EMAIL 2 — Perché un multivitaminico completo batte 10 separati
    │
    ├── Se acquista → esce → Post Purchase New (flow 6)
    │
    ▼  (+4 giorni)
EMAIL 3 — Chi è Lorenzo + perché Paleocomplex esiste
    │
    ├── Se acquista → esce → Post Purchase New (flow 6)
    │
    ▼  (+7 giorni)
EMAIL 4 — Il prodotto giusto per te (Elisir/Revolution/Essentiel) + social proof
    │
    ├── Se acquista → esce → Post Purchase New (flow 6)
    │
    ▼  (+10 giorni)
SPLIT: Ha acquistato?
    ├── SÌ → Fine (è nel Post Purchase)
    │
    └── NO ↓
         EMAIL 5 — Ultima occasione + reminder BENVENUTO
              │
              ▼
         Fine welcome → Entra in Authority Flow (flow 4)
```

---

## Note

### Dati performance vecchio flow Welcome 10€
- 2 email, revenue totale €24.770 (il flow più redditizio in assoluto)
- Email 1: 60.8% open, 23.7% click, €11.79 per invio
- Kit Benessere (delivery report): 48.9% open, 22.3% click

### Recensioni utilizzate (email 4)
Tutte verificate dal file `context/2026 03 31 paleocoplex export-reviews.csv`:
- Matteo Anceschi → Elisir, 5 stelle (energia, anti-aging, completezza)
- Fabrizio Gragnani → Essentiel, 5 stelle (stanchezza, pelle, coppia 40+)
- Mario Ricci → Revolution, 5 stelle (energia, produttività quotidiana)

### Link da verificare prima della pubblicazione
- Link al PDF del report "7 Strategie Scientifiche" → verificare URL attivo
- `paleocomplex.com/guida-scelta` → pagina da creare (vedi task-operativo)
- Codice BENVENUTO → verificare che sia attivo e configurato correttamente su WooCommerce

### Confronto prezzi ingredienti (email 2)
Il dato €302-460 per 40 giorni proviene dalla scheda prodotto Elisir (`context/products/elisir-scheda-prodotto.md`, sezione 1.3 USP). Verificare periodicamente se il dato è ancora valido.
