**Versione:** 2.0
**Ultimo aggiornamento:** 2026-06-11

# Flow 7: Stato Cliente — Primo Cliente Assoluto

## Chi entra in questo flow

Persone che hanno effettuato il **primo ordine in assoluto** sul sito Paleocomplex (Has Placed Order = 1 over all time).

Il flow lavora sulla **relazione brand**, non sulla parte prodotto. L'educazione specifica sui prodotti (istruzioni, aspettative, social proof) è gestita dai **flow prodotto 09-22** che girano in parallelo, triggerati dai singoli SKU presenti nell'ordine.

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
- I flow prodotto (09-22) girano in parallelo, triggerati dagli SKU specifici dell'ordine
- I retention flow per prodotto partono dopo (timing Fulfilled Order specifici per prodotto)

## Mittenti

| # | Email | Mittente |
|---|-------|----------|
| 1 | Benvenuto | Lorenzo Zarone |
| 2 | Ottimizza | Lorenzo Zarone |

**Nota:** la richiesta recensione brand è stata spostata in un flow dedicato (**Flow 23 — Recensione Brand**, vedi `fase2/23-recensione-brand.md`). Triggerato su Fulfilled Order +32gg, gira in parallelo a questo flow per tutti i clienti (primi e ricorrenti). Vedi changelog per il motivo.

## Timeline

| # | Timing | Tema | Tipo |
|---|--------|------|------|
| 1 | +2h dal Placed | Benvenuto + cosa succede adesso | Statica |
| 2 | +12gg dal Placed | Ottimizza i risultati (5 abitudini complementari) | Statica |

**Incastro con flow prodotto** (esempio cliente nuovo che compra solo Paleocomplex, fulfilled scenario medio T+1gg):

```
T+2h    [07 Stato]      Benvenuto Lorenzo
T+1gg   [09 Paleo]      Istruzioni Paleocomplex
T+5gg   [09 Paleo]      Aspettative multivitaminico
T+12gg  [07 Stato]      Ottimizza abitudini
T+18gg  [09 Paleo]      Social proof Paleocomplex (Flaminia)
T+33gg  [23 Recensione] Richiesta recensione brand (Flaminia)
T+35gg  [WooCommerce]   Email automatica ⭐⭐⭐⭐⭐
```

Gap minimo tra invii ≥ 2 giorni. Sequenza alternata Lorenzo/Flaminia.

**Coordinamento con WooCommerce:**
- L'email di conferma ordine arriva da WooCommerce standard (riepilogo ordine, totale, dettaglio prodotti)
- L'email di richiesta recensione automatica di WooCommerce è schedulata a +34gg dal Completed (quando l'ordine viene spedito)
- Il **Flow 23** anticipa di 2 giorni questa email di sistema, triggerato su Fulfilled+32gg per avere gap esatto e indipendente dai tempi di spedizione

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

**Appena il tuo ordine partirà** ti spiego come assumere correttamente il prodotto: è la cosa più importante per partire bene.

**Nei giorni successivi** ti dico cosa aspettarti realisticamente dalle prime settimane di integrazione.

**Più avanti** ti darò qualche consiglio per amplificare i risultati senza spendere altro.

Niente promesse esagerate. Solo informazioni che la maggior parte dei brand di integratori non si prende il tempo di darti.

Per qualsiasi cosa scrivici dalla nostra **[pagina di supporto](https://paleocomplex.com/contatti/)**: rispondiamo sempre, di solito entro la giornata lavorativa.

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

Se nel frattempo hai domande, scrivici dalla nostra [pagina di supporto](https://paleocomplex.com/contatti/).

Un forte abbraccio
Lorenzo Zarone
Fondatore di Paleocomplex

---

## Note operative

### CTA per email
- Email 1: nessuna CTA esplicita, solo link a pagina di supporto in caso di problemi
- Email 2: 3 link inline a articoli blog (sonno, sole, alimentazione)

### Open loop tra email
- Email 1 → 2: "Più avanti ti darò consigli per amplificare i risultati"
- (La richiesta recensione brand è ora nel Flow 23 separato)

### Filtro accessori
Il flow NON parte se l'ordine contiene SOLO Lampada Apollo, occhiali blue blocker, libri.
Trigger filter: ordine deve contenere almeno 1 integratore.

### Rinforzo Lorenzo / Flaminia
- Lorenzo nelle email 1-2 (autorità, voce educativa)
- Flaminia nell'email 3 (umano, customer care, richiesta recensione)
- La firma standardizzata di Flaminia: "Flaminia · Customer Care Paleocomplex"

### Refactoring storico
Le email 2 (Istruzioni), 3 (Aspettative), 5 (Social proof) della versione precedente di questo flow sono state estratte e migrate nei **flow prodotto 09-22** (uno per SKU), per garantire che il cliente riceva l'educazione specifica del prodotto anche quando lo acquista come cliente ricorrente (es. primo cliente compra Youth, riceve Welcome + flow Youth; al secondo ordine compra Elisir, riceve Cliente Ricorrente + flow Elisir specifico).

### Decisione trigger / Fulfilled vs Placed (2026-06-11)
Analisi dati WooCommerce 90gg (1.265 ordini): tempo Placed→Fulfilled mediana 22h, P90 55h, P95 71h. Il 26% degli ordini ha fulfilled > 1.5gg (ordini weekend e venerdì sera). Per questo:
- Flow 07 (Primo Cliente) e 08 (Cliente Ricorrente): **trigger Placed Order** — intervengono subito per buyer's remorse, copy non parla del prodotto fisico
- Flow prodotto 09-22: **trigger Fulfilled Order** — parlano del prodotto in viaggio, sempre veri
- Flow 23 (Recensione Brand): **trigger Fulfilled Order +32gg** — gap esatto con email automatica WC (+34gg da Completed), indipendente dalla velocità di spedizione
- Copy email 1 modificato: rimosso "Domani ti spiego" (regge solo per il 60% degli ordini) → sostituito con "Appena il tuo ordine partirà ti spiego" (regge per tutti)

### Changelog
- **v2.0 (2026-06-11)**: rinumerazione globale (06 → 07 per evitare conflitto con 06-conversione di Fase 1). **Email 3 (Richiesta recensione brand) rimossa e migrata nel nuovo Flow 23 — Recensione Brand**, triggerato su Fulfilled+32gg invece che Placed+32gg. Motivazione: con Placed-based, il gap tra la nostra recensione e l'email WC (che parte da Completed+34gg) oscillava da 1 a 5 giorni a seconda della velocità di spedizione, rompendo il copy "tra poche ore riceverai un'email automatica". Con Fulfilled+32gg il gap è sempre esatto di 2 giorni.
- v1.1 (2026-06-11): fix copy email 1 Benvenuto. Rimosso il riferimento "Domani" alle istruzioni prodotto (non regge per il 26% degli ordini con fulfilled > 1.5gg). Sostituito con "Appena il tuo ordine partirà ti spiego..." per coerenza con trigger Fulfilled del flow prodotto.
- v1.0 (2026-05-13): refactor architetturale. Spogliato dei blocchi prodotto-specifici (email 2 istruzioni, email 3 aspettative, email 5 social proof) migrati nei flow prodotto. Cleanup nomenclatura.
- v0.9 (2026-05-11): versione precedente con 6 email + blocchi condizionali per prodotto. Archiviata.
