**Versione:** 1.0
**Ultimo aggiornamento:** 2026-05-13

# Flow 6: Stato Cliente — Primo Cliente Assoluto

## Chi entra in questo flow

Persone che hanno effettuato il **primo ordine in assoluto** sul sito Paleocomplex (Has Placed Order = 1 over all time).

Il flow lavora sulla **relazione brand**, non sulla parte prodotto. L'educazione specifica sui prodotti (istruzioni, aspettative, social proof) è gestita dai **flow prodotto 08-21** che girano in parallelo, triggerati dai singoli SKU presenti nell'ordine.

L'obiettivo del flow è:
- Validare la scelta e abbattere il buyer's remorse subito dopo l'ordine
- Costruire la voce di Lorenzo come autorità di brand
- Dare valore con consigli trasversali su abitudini complementari
- Generare social proof tramite richiesta recensione

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
- I flow prodotto (08-21) girano in parallelo, triggerati dagli SKU specifici dell'ordine
- I retention flow per prodotto partono dopo (timing Fulfilled Order specifici per prodotto)

## Mittenti

| # | Email | Mittente |
|---|-------|----------|
| 1 | Benvenuto | Lorenzo Zarone |
| 2 | Ottimizza | Lorenzo Zarone |
| 3 | Richiesta recensione | Flaminia (Customer Care) |

## Timeline

| # | Timing | Tema | Tipo |
|---|--------|------|------|
| 1 | +2h | Benvenuto + cosa succede adesso | Statica |
| 2 | +12gg | Ottimizza i risultati (5 abitudini complementari) | Statica |
| 3 | +32gg | Richiesta recensione (anticipa la mail di sistema a +34gg) | Statica |

**Incastro con flow prodotto** (esempio cliente nuovo che compra solo Paleocomplex):

```
T+2h    [06 Stato]   Benvenuto Lorenzo
T+1gg   [08 Paleo]   Istruzioni Paleocomplex
T+5gg   [08 Paleo]   Aspettative multivitaminico
T+12gg  [06 Stato]   Ottimizza abitudini
T+18gg  [08 Paleo]   Social proof Paleocomplex (Flaminia)
T+32gg  [06 Stato]   Recensione brand (Flaminia)
```

Gap minimo tra invii ≥ 2 giorni. Sequenza alternata Lorenzo/Flaminia.

**Coordinamento con WooCommerce:**
- L'email di conferma ordine arriva da WooCommerce standard (riepilogo ordine, totale, dettaglio prodotti)
- L'email di richiesta recensione automatica di WooCommerce è schedulata a +34gg dall'ordine (oggetto: "⭐⭐⭐⭐⭐ Quante stelle daresti a Paleocomplex?")
- La nostra email 3 di richiesta recensione (+32gg) anticipa di 2 giorni questa email di sistema, preparando il cliente

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

**Info sulla consegna del tuo ordine 📦**

L'ordine ti è già stato confermato dal sistema (se non è arrivata l'email con il riepilogo contattaci).
Sarà spedito entro 24h lavorative e riceverai un'email con il tracking appena il pacco partirà.
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

## EMAIL 2 — Ottimizza i risultati (+12 giorni)

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

Se nel frattempo hai domande, scrivici a info@paleocomplex.com.

Un forte abbraccio
Lorenzo Zarone
Fondatore di Paleocomplex

---

## EMAIL 3 — Richiesta recensione (+32 giorni)

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

## Note operative

### CTA per email
- Email 1: nessuna CTA esplicita, solo ordini@ in caso di problemi
- Email 2: 3 link inline a articoli blog (sonno, sole, alimentazione)
- Email 3: nessuna CTA (l'azione è sulla mail di sistema successiva)

### Open loop tra email
- Email 1 → 2: "Più avanti ti darò consigli per amplificare i risultati"
- Email 2 → 3: nessun open loop diretto (email 3 ha topic completamente diverso, transazionale)

### Filtro accessori
Il flow NON parte se l'ordine contiene SOLO Lampada Apollo, occhiali blue blocker, libri.
Trigger filter: ordine deve contenere almeno 1 integratore.

### Rinforzo Lorenzo / Flaminia
- Lorenzo nelle email 1-2 (autorità, voce educativa)
- Flaminia nell'email 3 (umano, customer care, richiesta recensione)
- La firma standardizzata di Flaminia: "Flaminia · Customer Care Paleocomplex"

### Refactoring storico
Le email 2 (Istruzioni), 3 (Aspettative), 5 (Social proof) della versione precedente di questo flow sono state estratte e migrate nei **flow prodotto 08-21** (uno per SKU), per garantire che il cliente riceva l'educazione specifica del prodotto anche quando lo acquista come cliente ricorrente (es. primo cliente compra Youth, riceve Welcome + flow Youth; al secondo ordine compra Elisir, riceve Cliente Ricorrente + flow Elisir specifico).

### Changelog
- v1.0 (2026-05-13): refactor architetturale. Spogliato dei blocchi prodotto-specifici (email 2 istruzioni, email 3 aspettative, email 5 social proof) migrati nei flow prodotto 08-21. Il flow ora gestisce solo lo stato cliente "primo ordine in assoluto" (benvenuto + ottimizza abitudini + richiesta recensione brand). Cleanup nomenclatura: rinominato da "Post Purchase Nuovo Cliente" a "Primo Cliente Assoluto" per chiarire il ruolo nel nuovo schema.
- v0.9 (2026-05-11): versione precedente con 6 email + blocchi condizionali per prodotto. Archiviata.
