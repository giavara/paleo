**Versione:** 0.1
**Ultimo aggiornamento:** 2026-05-11
**Status:** Bozza v1 — in attesa review Andrea, poi review Lorenzo

# Flow 7: Post Purchase — Cliente Ricorrente

## Chi entra in questo flow

Persone che hanno effettuato un **ordine successivo al primo** (Has Placed Order >= 2 over all time).

Sono clienti già fidelizzati: conoscono il brand, sanno come usare i prodotti, hanno già completato (o stanno completando) il Post Purchase Nuovo Cliente in passato. Per loro un flow lungo di onboarding sarebbe ridondante.

L'obiettivo di questo flow è:
- Validare il riacquisto e rinforzare la decisione di fedeltà
- Suggerire un prodotto complementare al loro acquisto (cross-sell intelligente)
- Mantenere il filo del rapporto umano con Flaminia

## Configurazione Klaviyo

**Trigger:** Placed Order
**Filtro principale:**
- Has Placed Order at least 2 times over all time (non è il primo acquisto)

**Filtro accessori (escludere chi compra SOLO accessori):**
- Items contains at least one supplement (Elisir, Revolution, Essentiel, Paleocomplex, Elisir Basic, Youth, Jeunesse, Hurricane, Armageddon, Artosan, Liverty, Testoplus, Renaissance, Vitamina D)
- Se l'ordine contiene SOLO accessori (Lampada Apollo, occhiali, libri), il flow NON parte

**Effetto su altri flow:**
- Il Post Purchase Nuovo Cliente NON parte (perché il filtro è "Has Placed Order = 1 over all time")
- I retention flow per prodotto partono dopo (Fulfilled Order)

## Mittenti

| # | Email | Mittente |
|---|-------|----------|
| 1 | Grazie + validazione | Lorenzo Zarone |
| 2 | Cross-sell prodotto complementare | Flaminia (Customer Care) |

## Timeline

| # | Timing | Tema | Tipo |
|---|--------|------|------|
| 1 | +2h | Grazie per essere tornato + costanza è tutto | Statica |
| 2 | +3gg | Cross-sell prodotto complementare | 4 blocchi dinamici per famiglia + blocco sport trasversale |

**Coordinamento con altri flow:**
- L'email di conferma ordine arriva da WooCommerce standard
- La richiesta recensione automatica WooCommerce è a +34gg (oggetto: "⭐⭐⭐⭐⭐ Quante stelle daresti a Paleocomplex?"). Per i clienti ricorrenti probabilmente l'hanno già lasciata in passato — il sistema WC dovrebbe gestirlo nativamente

---

## EMAIL 1 — Grazie + validazione riacquisto (+2 ore)

**Mittente:** Lorenzo Zarone
**Tipo:** Statica (uguale per tutti)

### Oggetto (3 varianti A/B)

- A: Grazie per essere tornato
- B: Una conferma che vale più di mille parole
- C: La costanza è quello che fa la differenza

### Preview text (3 varianti)

- A: Hai appena fatto la cosa più importante.
- B: Il riacquisto è il vero indicatore.
- C: Una nota veloce, solo per ringraziarti.

### Corpo email

Ciao [NOME]

Ti scrivo solo per dirti grazie.

Hai appena fatto un nuovo ordine, e per me è il segnale più importante che possa ricevere come fondatore. Le recensioni a 5 stelle fanno piacere, ma sono il riacquisto a dirmi davvero che un prodotto funziona. Significa che il primo ciclo ti è stato utile, che hai notato la differenza, e che hai deciso di continuare.

Sulla costanza ci ho costruito la mia filosofia di lavoro: gli integratori funzionano davvero solo se assunti con regolarità. I primi tre mesi sono la fase in cui il corpo ricostituisce le scorte. Dal quarto mese in poi cominciano a consolidarsi i benefici strutturali, quelli che non "senti" nel quotidiano ma che fanno la differenza negli anni.

Tu sei già in quella fase. Continua.

L'ordine ti è già stato confermato dal sistema (l'email con il riepilogo è arrivata). Lo prepariamo entro 24 ore lavorative e parte con corriere espresso, tracking incluso.

**Tra qualche giorno** Flaminia ti scriverà con un suggerimento concreto: un prodotto che, dato quello che usi già, potrebbe completare bene il tuo protocollo. Niente forzature, solo logica di combinazioni.

Per qualsiasi cosa scrivici a **ordini@paleocomplex.com**.

Un forte abbraccio
Lorenzo Zarone
Fondatore di Paleocomplex

---

## EMAIL 2 — Cross-sell prodotto complementare (+3 giorni)

**Mittente:** Flaminia (Customer Care)
**Tipo:** Tronco comune + 4 blocchi dinamici per famiglia (sui prodotti DELL'ORDINE CORRENTE) + blocco sport trasversale fisso

### Oggetto (3 varianti A/B)

- A: Una cosa che potrebbe completare bene il tuo protocollo
- B: Un suggerimento, se ti va
- C: Cosa funziona bene con quello che usi già

### Preview text (3 varianti)

- A: Nessuna pressione. Solo logica di combinazioni.
- B: Il prodotto che spesso accompagna il tuo.
- C: Una piccola idea da Flaminia.

### Corpo email

**Tronco comune — apertura**

Ciao [NOME]

Sono Flaminia. Lorenzo mi ha lasciato il testimone su questa email, come sempre quando si tratta di parlare con i nostri clienti più affezionati.

Visto che sei tornato, voglio darti un suggerimento concreto basato su quello che hai acquistato: un prodotto che spesso accompagna bene il tuo nei protocolli più completi. Non è una vendita forzata: è quello che ci raccontano i clienti che combinano più prodotti, e quello che Lorenzo consiglia nella sua guida ai protocolli.

Qui sotto trovi il suggerimento più adatto al tuo ordine.

---

**[BLOCCO 1 — HAI ACQUISTATO UN MULTIVITAMINICO]**
*Show condition: Items contains "Paleocomplex" OR "Revolution" OR "Elisir" OR "Elisir Basic" OR "Essentiel"*

**Il complemento naturale: collagene per pelle, capelli, unghie**

Il multivitaminico copre le basi vitaminiche e minerali. Per andare oltre, il passo successivo più consigliato è il collagene: lavora su pelle, unghie, capelli e articolazioni, dimensioni che il multivitaminico tocca solo marginalmente.

Hai due opzioni a seconda del livello:

[**Youth**](https://paleocomplex.com/prodotto/youth/) — 6 g di collagene bovino al giorno, con acido ialuronico, glucosamina e i cofattori per la sintesi del collagene. È il punto di partenza.

[**Jeunesse**](https://paleocomplex.com/prodotto/jeunesse/) — 12 g di collagene bovino grass-fed al giorno, più antiossidanti cutanei avanzati (astaxantina, corteccia di pino, centella asiatica). È la versione potenziata, con focus anti-aging.

Se vuoi un protocollo anti-aging completo, c'è anche [**Renaissance**](https://paleocomplex.com/prodotto/renaissance/), 13 nutraceutici per la longevità cellulare. Da abbinare al multivitaminico, lavora su senolitici, NAD+, autofagia.

---

**[BLOCCO 2 — HAI ACQUISTATO COLLAGENE (Youth o Jeunesse)]**
*Show condition: Items contains "Youth" OR "Jeunesse"*

**Il complemento naturale: la base multivitaminica**

Il collagene da solo è ottimo per pelle, capelli e unghie. Ma per amplificarne l'efficacia ti serve una base solida di vitamine e minerali: senza vitamina C, zinco e biotina (i cofattori della sintesi del collagene) il tuo corpo non può costruire collagene nuovo in modo efficiente.

Se non ne usi già uno, il nostro consiglio è abbinarlo a un multivitaminico:

[**Elisir**](https://paleocomplex.com/prodotto/elisir/) — il più completo della linea, 40 nutrienti in un misurino al giorno. Include omega 3 da krill, antiossidanti avanzati, vitamine attivate.

[**Essentiel**](https://paleocomplex.com/prodotto/essentiel/) — 34 nutrienti, senza krill, con focus cognitivo (citicolina, acetil-carnitina). Per chi è allergico ai crostacei o cerca un prodotto più orientato alla funzione cognitiva.

Per chi vuole spingere l'anti-aging cellulare, [**Renaissance**](https://paleocomplex.com/prodotto/renaissance/) è il livello successivo: lavora sui meccanismi di longevità più profondi (senolitici, NAD+, autofagia).

---

**[BLOCCO 3 — HAI ACQUISTATO UN PRODOTTO SPORT (Hurricane o Armageddon)]**
*Show condition: Items contains "Hurricane" OR "Armageddon"*

**Il complemento naturale: l'altro prodotto sport + la base multivitaminica**

I prodotti sport lavorano sulla performance e sul recupero. Se non hai già una base multivitaminica, il consiglio è abbinarne una: l'allenamento intenso aumenta lo stress ossidativo e la richiesta di micronutrienti.

Se usi già Hurricane, l'abbinamento naturale è [**Armageddon**](https://paleocomplex.com/prodotto/armageddon/): aminoacidi essenziali per il recupero e la protezione muscolare. La miscela Hurricane + Armageddon pre-workout è il protocollo che ti consigliamo per allenamenti intensi.

Se usi già Armageddon, [**Hurricane**](https://paleocomplex.com/prodotto/hurricane/) è il pre-workout che lavora in sinergia: creatina, beta-alanina, citrullina per esplosività e pump muscolare.

Per la base multivitaminica, se ti alleni intensamente ti consigliamo [**Revolution**](https://paleocomplex.com/prodotto/paleocomplex-revolution/) (antiossidanti avanzati per chi mette sotto stress il corpo) o [**Elisir**](https://paleocomplex.com/prodotto/elisir/) (più completo in assoluto).

---

**[BLOCCO 4 — HAI ACQUISTATO UN PRODOTTO SPECIFICO (Artosan, Liverty, Testoplus, Renaissance, Vit D)]**
*Show condition: Items contains "Artosan" OR "Liverty" OR "Testoplus" OR "Renaissance" OR "Vitamina D"*

**Il complemento naturale: la base multivitaminica**

I prodotti specifici lavorano su una funzione precisa (articolazioni, fegato, ormoni, anti-aging, vitamina D). Sono ottimi quando hai un obiettivo mirato, ma danno il meglio quando appoggiati a una base di micronutrienti completa.

Se non usi già un multivitaminico:

[**Elisir**](https://paleocomplex.com/prodotto/elisir/) — il più completo, 40 nutrienti tra cui omega 3 da krill, antiossidanti avanzati, vitamine attivate.

[**Essentiel**](https://paleocomplex.com/prodotto/essentiel/) — 34 nutrienti senza krill, ottimo rapporto qualità-prezzo, focus cognitivo.

Su [**guida-scelta**](https://paleocomplex.com/guida-scelta) trovi un orientamento rapido per scegliere quello giusto per te in base ad età e obiettivi.

---

**[BLOCCO TRASVERSALE — SPORT]**
*Show condition: Items NOT contains "Hurricane" AND NOT contains "Armageddon" (cioè: si mostra a chi NON ha già comprato prodotti sport in questo ordine)*

**Se ti alleni: scopri la linea sport**

Una nota a parte: se ti alleni regolarmente (palestra, corsa, ciclismo, sport di endurance), la nostra linea sport potrebbe completare bene il tuo protocollo.

[**Hurricane**](https://paleocomplex.com/prodotto/hurricane/) — pre-workout completo, creatina + beta-alanina + citrullina, da bere 30-45 minuti prima dell'allenamento.

[**Armageddon**](https://paleocomplex.com/prodotto/armageddon/) — aminoacidi essenziali, per il recupero e la protezione muscolare durante e dopo l'allenamento. Utile anche per chi ha più di 40 anni come supporto anti-sarcopenia.

---

**Tronco comune — chiusura**

Una cosa importante: nessuno di questi suggerimenti è una "vendita forzata". Sono solo le combinazioni più sensate basate su quello che usi già. Se non ti interessano, ignora pure l'email.

Se invece vuoi un parere personalizzato sul tuo caso specifico, **rispondi pure a questa email** raccontandomi i tuoi obiettivi: ti aiuto a costruire il protocollo giusto.

A presto
Flaminia
Customer Care Paleocomplex

---

## Schema del flow

```
[Placed Order, Has Placed Order >= 2 over all time, ordine NON solo accessori]
    │
    ▼  (+2 ore)
EMAIL 1 — Grazie + validazione riacquisto (Lorenzo, statica)
    │
    ▼  (+3 giorni)
EMAIL 2 — Cross-sell complementare (Flaminia, 4 blocchi dinamici + sport trasversale)
    │
    ▼
Fine flow → entra in Retention specifico per il prodotto acquistato (gg 20-55 a seconda del prodotto)
```

---

## Note operative

### Filtri Klaviyo avanzati (da valutare in seconda battuta)

Per ottimizzare il cross-sell, si possono aggiungere filtri "Has Ever Purchased" sui prodotti suggeriti, in modo da NON proporre a un cliente un prodotto che ha già comprato in passato. Esempi:

- Se hai comprato Elisir e in passato hai già comprato anche Youth, il blocco multivitaminico potrebbe spingere su Renaissance invece che su Youth/Jeunesse
- Se hai già comprato Hurricane in passato, il blocco sport trasversale potrebbe spingere solo su Armageddon

Questi filtri rendono il cross-sell più intelligente ma aumentano la complessità di gestione. Per la v1 del flow, partiamo con i blocchi semplici basati sui prodotti dell'ordine corrente. Quando avremo dati di engagement sul flow, valuteremo se vale la pena complicare la logica.

### Niente sconto

Decisione confermata: nessun codice sconto in questo flow. Il cliente ricorrente è già fedele, lo sconto svaluta il prezzo pieno che ha appena pagato. Lo sconto resta per il win-back (flow 15-16, quando il cliente non torna da 85+ giorni).

### Link prodotti

Tutti i prodotti citati nei blocchi sono linkati alla pagina prodotto del sito. La guida alla scelta è linkata come fallback per chi vuole orientarsi.

### Coerenza con la matrice cross-sell del piano master

I suggerimenti seguono la matrice del piano master (sezione "Matrice cross-sell"):
- Multivitaminico → Collagene primario, Renaissance secondario, Sport trasversale
- Collagene Youth/Jeunesse → Multivitaminico se non l'ha + Renaissance + Sport trasversale
- Sport → L'altro prodotto sport + Multivitaminico
- Specifici → Multivitaminico come base
