**Versione:** 1.4
**Ultimo aggiornamento:** 2026-04-15
**Status:** Bozza v1 — in attesa review Andrea

# Flow 1: Carrello Abbandonato

## Configurazione Klaviyo

**Trigger:** Started Checkout
**Mittente:** Team Paleocomplex (tutte le email del flow)
**Filtri profilo:**
- Placed Order zero times since starting this flow
- Has not been in this flow in the last 7 days

**Note tecniche:**
- Usare Dynamic Table Block per mostrare i prodotti nel carrello
- Disabilitare email carrello abbandonato nativo di WooCommerce
- Codici sconto univoci (se usati in email 3 per nuovi clienti)
- CTA verso homepage (non checkout diretto) per compatibilità contrassegno

---

## EMAIL 1 — Reminder soft (+4 ore)

### Oggetto (3 varianti A/B)

- A: Il tuo carrello ti aspetta
- B: Hai lasciato qualcosa in sospeso
- C: Stavi per fare una scelta importante

### Preview text (3 varianti)

- A: I prodotti che hai scelto sono ancora disponibili.
- B: Completa il tuo ordine prima che le scorte cambino.
- C: Bastano pochi click per completare il tuo ordine.

### Corpo email

Ciao [NOME]

Abbiamo notato che hai aggiunto dei prodotti al carrello ma non hai completato l'ordine.

Capita. Magari ti hanno interrotto, o volevi pensarci ancora un momento.

Nessun problema.

**[DYNAMIC TABLE BLOCK — prodotti nel carrello]**

Vogliamo solo ricordarti che dietro ogni nostro integratore ci sono mesi di studio, formulazioni ad alto dosaggio con forme attive e una trasparenza totale sull'etichetta. Non troverai mai dosaggi simbolici nei nostri prodotti, solo quantità che possono fare davvero la differenza.

Se hai dubbi su quale prodotto sia il più adatto a te, abbiamo preparato una guida che ti aiuta a scegliere in base alla tua età e ai tuoi obiettivi. **[CTA: Scopri la guida alla scelta](https://paleocomplex.com/guida-scelta)**

Il tuo carrello è ancora pronto.

**[CTA: Completa il tuo ordine]**
(link a homepage / carrello)

Team Paleocomplex

---

## EMAIL 2 — Gestione obiezioni (+16 ore)

### Split condizionale

**PRIMA dello split:** Delay 16 ore
**SPLIT:** Has Placed Order = 0 over all time?
- **SÌ (nuovo cliente)** → Variante A (risposta obiezioni completa)
- **NO (cliente esistente)** → Variante B (breve, diretto)

---

### Variante A — Nuovo cliente

#### Oggetto (3 varianti A/B)

- A: Qualche dubbio? Ecco le risposte
- B: Le domande che ci fanno più spesso
- C: Ecco cosa devi sapere prima di ordinare

#### Preview text (3 varianti)

- A: Pagamento, spedizione, qualità: risposte chiare.
- B: Tutto quello che devi sapere su Paleocomplex.
- C: Le risposte alle domande più comuni dei nuovi clienti.

#### Corpo email

Ciao [NOME]

Spesso chi arriva per la prima volta sul nostro store ha delle domande. È comprensibile: non siamo il solito brand di integratori da supermercato, e i nostri prodotti hanno un livello di complessità che merita qualche spiegazione.

Ecco le risposte alle domande più frequenti.

**"Perché costa così tanto?"**

Perché non troverai mai il "100% del VNR (Valori Nutrizionali di Riferimento)" nei nostri prodotti. Quel 100% è il minimo per non avere carenze, non il dosaggio per stare davvero bene. Noi usiamo forme attive (vitamine B metilate, ubiquinolo, R-lipoico) a dosaggi che molti medici funzionali prescrivono singolarmente. Per darti un'idea: la vitamina B12 in Elisir è a **80 volte la dose che trovi al supermercato**, nella forma metilata più biodisponibile. Nei multivitaminici da banco trovi il 100% nella forma più economica.

Facciamo due conti: Elisir, il nostro multivitaminico più completo con 40 nutrienti, costa **€3,47 al giorno**. Meno di una colazione al bar. Se comprassi gli stessi ingredienti separatamente nelle stesse forme e dosaggi, spenderesti **tra €302 e €460 per 40 giorni** invece di €139.

**"La spedizione è veloce?"**

Ordini effettuati entro le 14:00 vengono spediti in giornata. Corriere espresso tracciato, consegna in 24-48 ore lavorative.

**"Come posso pagare?"**

Carta di credito, PayPal (anche a rate senza costi aggiuntivi), e contrassegno (supplemento di €7, serve un account registrato).

**"Non so quale prodotto scegliere."**

Abbiamo preparato una guida che ti aiuta a trovare il prodotto giusto in base alla tua età, ai tuoi obiettivi e al tuo budget. **[CTA: Vai alla guida alla scelta](https://paleocomplex.com/guida-scelta)**

Se preferisci un consiglio personalizzato, scrivici a **info@paleocomplex.com** e ti rispondiamo personalmente.

**[DYNAMIC TABLE BLOCK — prodotti nel carrello]**

**[CTA: Torna al tuo carrello]**

Team Paleocomplex

---

### Variante B — Cliente esistente

#### Oggetto (3 varianti A/B)

- A: Hai lasciato qualcosa nel carrello
- B: Il tuo ordine è ancora in sospeso
- C: Ci rivediamo?

#### Preview text (3 varianti)

- A: I tuoi prodotti ti aspettano.
- B: Completa l'ordine e non interrompere il tuo percorso.
- C: Bastano pochi click.

#### Corpo email

Ciao [NOME]

Il tuo carrello è ancora lì.

Tu conosci già la qualità dei nostri prodotti. Sai cosa aspettarti. E sai che la costanza è la chiave per ottenere il massimo dai tuoi integratori.

**[DYNAMIC TABLE BLOCK — prodotti nel carrello]**

Non lasciare che una pausa diventi un'interruzione.

**[CTA: Completa il tuo ordine]**

Team Paleocomplex

---

## EMAIL 3 — Social proof + ultima chance (+2 giorni)

### Oggetto (3 varianti A/B)

- A: Cosa dicono chi li usa ogni giorno
- B: Questo è quello che succede quando inizi
- C: Il tuo carrello scade presto

### Preview text (3 varianti)

- A: Le esperienze di chi ha fatto la tua stessa scelta.
- B: Migliaia di persone hanno già scelto Paleocomplex.
- C: I prodotti che hai scelto sono ancora disponibili, ma non per sempre.

### Corpo email

Ciao [NOME]

Prima di lasciar scadere il tuo carrello, vogliamo condividere con te alcune esperienze di persone che hanno fatto la stessa scelta che stavi per fare tu.

**"Mi ha cambiato totalmente la vita. Lungo la giornata riesco a portare a termine molte più cose con maggiore facilità. Mi dà molta più forza di vivere la mia vita con maggiore intensità."** Mario R.

**"Sono entusiasta di aver comprato questo integratore unico, contiene tutto quanto prendevo prima. Avere una confezione unica è molto vantaggioso rispetto a decine di confezioni. Mi dà molta buona energia e dormo anche meglio la notte!"** Anna M.

**"Ero scettica perché pensavo fosse uno dei tanti integratori sul mercato. Mi sono dovuta ricredere: da quando lo assumo la mia pelle è meno secca. Lo ricompro senza remore."** Franca

Sono recensioni reali di clienti verificati. Non promettiamo miracoli, ma possiamo prometterti ingredienti di altissima qualità, dosaggi reali e trasparenza totale.

**[DYNAMIC TABLE BLOCK — prodotti nel carrello]**

Il tuo carrello non resterà attivo per sempre. Se quei prodotti ti interessavano, questo è il momento giusto per completare l'ordine.

**[CTA: Completa il tuo ordine]**

Team Paleocomplex

---

## Note per la scrittura delle email successive

### Obiezioni principali emerse dal sondaggio ex-clienti (da usare come riferimento)
1. **Prezzo/sostenibilità nel tempo** (41%) — Le persone riconoscono la qualità ma il budget è limitato. Risposta: costo/giorno, confronto con singoli integratori, programma fedeltà
2. **Pagamento** (9%) — Contrassegno, problemi checkout. Risposta: confermare opzioni pagamento
3. **Confusione prodotti** (11%) — Non sanno cosa scegliere. Risposta: offrire consulenza personalizzata via email
4. **Formato/gusto** (6%) — Polvere non piace a tutti. NON affrontare nell'email carrello (non è il momento)
5. **Troppe email** (4%) — NON aumentare la pressione oltre 3 email

### Recensioni utilizzate (email 3)
Tutte verificate dal file `context/2026 03 31 paleocoplex export-reviews.csv`:
- Mario Ricci, Revolution, 5 stelle (energia, produttività quotidiana)
- Anna Marin, Essentiel, 5 stelle (semplificazione, energia, sonno)
- Franca, Revolution, 5 stelle (scettica convertita, pelle migliorata)
Nota: i nomi dei prodotti non compaiono nel testo email perché non sappiamo cosa ha nel carrello.
