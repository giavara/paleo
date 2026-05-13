**Versione:** 1.0
**Ultimo aggiornamento:** 2026-05-13

# Flow 7: Stato Cliente — Cliente Ricorrente

## Chi entra in questo flow

Persone che hanno effettuato un **ordine successivo al primo** (Has Placed Order >= 2 over all time).

Il flow lavora sulla **relazione brand** (grazie, costanza, cross-sell). L'educazione specifica sui prodotti (istruzioni, aspettative, social proof) per **prodotti acquistati per la prima volta** è gestita dai **flow prodotto 08-21** che girano in parallelo: se il cliente ricorrente acquista un prodotto mai provato prima, riceve il flow prodotto specifico oltre a questo flow stato.

L'obiettivo del flow è:
- Validare il riacquisto e rinforzare la decisione di fedeltà
- Suggerire un prodotto complementare al loro acquisto (cross-sell intelligente con esclusione prodotti già posseduti)
- Mantenere il filo del rapporto umano con Flaminia

## Configurazione Klaviyo

**Trigger:** Placed Order

**Filtro principale:**
- Has Placed Order at least 2 times over all time (non è il primo acquisto)

**Filtro accessori (escludere chi compra SOLO accessori):**
- Items contains at least one supplement (Elisir, Revolution, Essentiel, Paleocomplex, Elisir Basic, Youth, Jeunesse, Hurricane, Armageddon, Artosan, Liverty, Testoplus, Renaissance, Vitamina D)
- Se l'ordine contiene SOLO accessori (Lampada Apollo, occhiali, libri), il flow NON parte

**Effetto su altri flow:**
- Il flow 06 (Primo Cliente Assoluto) NON parte (filtro Has Placed Order = 1)
- I flow prodotto 08-21 girano in parallelo per i prodotti dell'ordine acquistati per la prima volta in assoluto
- I retention flow per prodotto partono dopo (Fulfilled Order)

## Mittenti

| # | Email | Mittente |
|---|-------|----------|
| 1 | Grazie + costanza | Lorenzo Zarone |
| 2 | Cross-sell prodotto complementare | Flaminia (Customer Care) |

## Timeline

| # | Timing | Tema | Tipo |
|---|--------|------|------|
| 1 | +2h | Grazie per essere tornato + costanza | Statica |
| 2 | +3gg | Cross-sell prodotto complementare | 4 blocchi dinamici per famiglia + blocco sport trasversale, tutti con esclusione "già posseduto" |

**Coordinamento con altri flow:**
- L'email di conferma ordine arriva da WooCommerce standard
- La richiesta recensione automatica WooCommerce è a +34gg. Per i clienti ricorrenti probabilmente l'hanno già lasciata in passato — il sistema WC dovrebbe gestirlo nativamente
- Se il cliente acquista un prodotto mai provato, i flow prodotto specifici 08-21 girano in parallelo (es. cliente esistente compra Elisir per la prima volta: riceve questo flow + flow 10 Elisir specifico)

---

## EMAIL 1 — Grazie + costanza (+2 ore)

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

Hai appena fatto un nuovo ordine, e per me è il segnale più importante che possa ricevere come fondatore. Le recensioni a 5 stelle fanno piacere, ma è il riacquisto a dirmi davvero che il lavoro sta funzionando. Significa che ci hai dato fiducia di nuovo, che lo abbiamo confermato, e che ti sei trovato bene.

Sulla costanza ci ho costruito la mia filosofia di lavoro: gli integratori funzionano davvero solo se assunti con regolarità. I primi tre mesi sono la fase in cui il corpo ricostituisce le scorte. Dal quarto mese in poi cominciano a consolidarsi i benefici strutturali, quelli che non "senti" nel quotidiano ma che fanno la differenza negli anni a venire.

Continua così.

L'ordine ti è già stato confermato dal sistema (l'email con il riepilogo è arrivata). Lo prepariamo entro 24 ore lavorative e parte con corriere espresso, tracking incluso.

**Tra qualche giorno** Flaminia ti scriverà con un suggerimento concreto: un prodotto che, dato quello che hai nel tuo protocollo, potrebbe completarlo bene. Niente forzature, solo logica di combinazioni.

Per qualsiasi cosa scrivici a **ordini@paleocomplex.com**.

Un forte abbraccio
Lorenzo Zarone
Fondatore di Paleocomplex

---

## EMAIL 2 — Cross-sell prodotto complementare (+3 giorni)

**Mittente:** Flaminia (Customer Care)
**Tipo:** Tronco comune + 4 blocchi dinamici per famiglia (sui prodotti DELL'ORDINE CORRENTE) + blocco sport trasversale. **Ogni suggerimento all'interno dei blocchi ha conditional di esclusione "già posseduto"** (vedi sotto).

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

*Sotto-blocco Youth (mostrato solo se cliente non ha mai acquistato Youth in passato — condition: Customer has not Placed Order with item SKU `youth`):*
> [**Youth**](https://paleocomplex.com/prodotto/youth/) — 6 g di collagene bovino al giorno, con acido ialuronico, glucosamina e i cofattori per la sintesi del collagene. È il punto di partenza.

*Sotto-blocco Jeunesse (mostrato solo se cliente non ha mai acquistato Jeunesse — condition: SKU `jeunesse` non in storico):*
> [**Jeunesse**](https://paleocomplex.com/prodotto/jeunesse/) — 12 g di collagene bovino grass-fed al giorno, più antiossidanti cutanei avanzati (astaxantina, corteccia di pino, centella asiatica). È la versione potenziata, con focus anti-aging.

*Sotto-blocco Renaissance (mostrato solo se cliente non ha mai acquistato Renaissance — condition: SKU `renaissance` non in storico):*
> Se vuoi un protocollo anti-aging completo, c'è anche [**Renaissance**](https://paleocomplex.com/prodotto/renaissance/), 13 nutraceutici per la longevità cellulare. Da abbinare al multivitaminico, lavora su senolitici, NAD+, autofagia.

*Se tutti i sotto-blocchi sopra sono nascosti (cliente ha già tutto), il BLOCCO 1 NON si mostra affatto e si passa al blocco successivo o trasversale.*

---

**[BLOCCO 2 — HAI ACQUISTATO COLLAGENE (Youth o Jeunesse)]**
*Show condition: Items contains "Youth" OR "Jeunesse"*

**Il complemento naturale: la base multivitaminica**

Il collagene da solo è ottimo per pelle, capelli e unghie. Ma per amplificarne l'efficacia ti serve una base solida di vitamine e minerali: senza vitamina C, zinco e biotina (i cofattori della sintesi del collagene) il tuo corpo non può costruire collagene nuovo in modo efficiente.

*Sotto-blocco Elisir (mostrato solo se cliente non ha mai acquistato Elisir — condition: SKU `elisir` non in storico):*
> [**Elisir**](https://paleocomplex.com/prodotto/elisir/) — il più completo della linea, 40 nutrienti in un misurino al giorno. Include omega 3 da krill, antiossidanti avanzati, vitamine attivate.

*Sotto-blocco Essentiel (mostrato solo se cliente non ha mai acquistato Essentiel — condition: SKU `essentiel` non in storico):*
> [**Essentiel**](https://paleocomplex.com/prodotto/essentiel/) — 34 nutrienti, senza krill, con focus cognitivo (citicolina, acetil-carnitina). Per chi è allergico ai crostacei o cerca un prodotto più orientato alla funzione cognitiva.

*Sotto-blocco Renaissance (mostrato solo se cliente non ha mai acquistato Renaissance — condition: SKU `renaissance` non in storico):*
> Per chi vuole spingere l'anti-aging cellulare, [**Renaissance**](https://paleocomplex.com/prodotto/renaissance/) è il livello successivo: lavora sui meccanismi di longevità più profondi.

*Se cliente ha già acquistato Paleocomplex o Revolution (multivitaminici della casa) ma non Elisir/Essentiel, mostriamo comunque Elisir/Essentiel come "upgrade" naturale ma con framing diverso.* TODO setup Klaviyo: definire show/hide preciso del framing.

---

**[BLOCCO 3 — HAI ACQUISTATO UN PRODOTTO SPORT (Hurricane o Armageddon)]**
*Show condition: Items contains "Hurricane" OR "Armageddon"*

**Il complemento naturale: l'altro prodotto sport + la base multivitaminica**

I prodotti sport lavorano sulla performance e sul recupero. Se non hai già una base multivitaminica, il consiglio è abbinarne una: l'allenamento intenso aumenta lo stress ossidativo e la richiesta di micronutrienti.

*Sotto-blocco "se manca Armageddon" (mostrato solo se ordine contiene Hurricane AND cliente non ha mai acquistato Armageddon — condition: SKU `armageddon` non in storico):*
> Se usi Hurricane, l'abbinamento naturale è [**Armageddon**](https://paleocomplex.com/prodotto/armageddon/): aminoacidi essenziali per il recupero e la protezione muscolare. La miscela Hurricane + Armageddon pre-workout è il protocollo che ti consigliamo per allenamenti intensi.

*Sotto-blocco "se manca Hurricane" (mostrato solo se ordine contiene Armageddon AND cliente non ha mai acquistato Hurricane — condition: SKU `hurricane` non in storico):*
> Se usi Armageddon, [**Hurricane**](https://paleocomplex.com/prodotto/hurricane/) è il pre-workout che lavora in sinergia: creatina, beta-alanina, citrullina per esplosività e pump muscolare.

*Sotto-blocco multivitaminico per sportivi (mostrato solo se cliente non ha mai acquistato Revolution né Elisir — condition: SKU `paleocomplex-revo` non in storico AND SKU `elisir` non in storico):*
> Per la base multivitaminica, se ti alleni intensamente ti consigliamo [**Revolution**](https://paleocomplex.com/prodotto/paleocomplex-revolution/) (antiossidanti avanzati per chi mette sotto stress il corpo) o [**Elisir**](https://paleocomplex.com/prodotto/elisir/) (più completo in assoluto).

---

**[BLOCCO 4 — HAI ACQUISTATO UN PRODOTTO SPECIFICO (Artosan, Liverty, Testoplus, Renaissance, Vit D)]**
*Show condition: Items contains "Artosan" OR "Liverty" OR "Testoplus" OR "Renaissance" OR "Vitamina D"*

**Il complemento naturale: la base multivitaminica**

I prodotti specifici lavorano su una funzione precisa (articolazioni, fegato, ormoni, anti-aging, vitamina D). Sono ottimi quando hai un obiettivo mirato, ma danno il meglio quando appoggiati a una base di micronutrienti completa.

*Sotto-blocchi multivitaminici (ognuno mostrato solo se cliente non ha già quel SKU in storico):*

> Se non usi già un multivitaminico:
>
> [**Elisir**](https://paleocomplex.com/prodotto/elisir/) — il più completo, 40 nutrienti tra cui omega 3 da krill, antiossidanti avanzati, vitamine attivate. *[mostra se SKU `elisir` non in storico]*
>
> [**Essentiel**](https://paleocomplex.com/prodotto/essentiel/) — 34 nutrienti senza krill, ottimo rapporto qualità-prezzo, focus cognitivo. *[mostra se SKU `essentiel` non in storico]*

Su [**guida-scelta**](https://paleocomplex.com/guida-scelta) trovi un orientamento rapido per scegliere quello giusto per te in base ad età e obiettivi.

---

**[BLOCCO TRASVERSALE — SPORT]**
*Show condition: Items NOT contains "Hurricane" AND NOT contains "Armageddon" (cioè: si mostra a chi NON ha acquistato prodotti sport nell'ordine corrente). Inoltre ognuno dei sotto-blocchi è condizionato su "non ha mai acquistato il prodotto in passato".*

**Se ti alleni: scopri la linea sport**

Una nota a parte: se ti alleni regolarmente (palestra, corsa, ciclismo, sport di endurance), la nostra linea sport potrebbe completare bene il tuo protocollo.

*Sotto-blocco Hurricane (mostrato solo se cliente non ha mai acquistato Hurricane — condition: SKU `hurricane` non in storico):*
> [**Hurricane**](https://paleocomplex.com/prodotto/hurricane/) — pre-workout completo, creatina + beta-alanina + citrullina, da bere 30-45 minuti prima dell'allenamento.

*Sotto-blocco Armageddon (mostrato solo se cliente non ha mai acquistato Armageddon — condition: SKU `armageddon` non in storico):*
> [**Armageddon**](https://paleocomplex.com/prodotto/armageddon/) — aminoacidi essenziali, per il recupero e la protezione muscolare durante e dopo l'allenamento. Utile anche per chi ha più di 40 anni come supporto anti-sarcopenia.

*Se entrambi i sotto-blocchi sono nascosti (cliente ha già Hurricane + Armageddon in storico), il BLOCCO TRASVERSALE non si mostra.*

---

**Tronco comune — chiusura**

Una cosa importante: nessuno di questi suggerimenti è una "vendita forzata". Sono solo le combinazioni più sensate basate su quello che usi già. Se non ti interessano, ignora pure l'email.

Se invece vuoi un parere personalizzato sul tuo caso specifico, **rispondi pure a questa email** raccontandomi i tuoi obiettivi: ti aiuto a costruire il protocollo giusto.

A presto
Flaminia
Customer Care Paleocomplex

---

## Edge case: cliente con storico completo

Se un cliente ha già acquistato in passato TUTTI i prodotti suggeribili (caso raro, ma esiste), tutti i sotto-blocchi della email 2 risultano nascosti e il cliente vedrebbe solo il tronco comune + niente blocchi. Per evitare un'email vuota, va inserito un **fallback content block** che si mostra quando nessun altro blocco è visibile:

> *Hai già un protocollo completo con la nostra linea. Continua così.*
>
> *Se vuoi un confronto su come ottimizzare i dosaggi, le combinazioni o le pause cicliche, **rispondi pure a questa email**: te lo costruiamo insieme.*

**TODO setup Klaviyo:** implementare il fallback come ultimo blocco con condizione "tutti gli altri blocchi sono hidden".

---

## Schema del flow

```
[Placed Order, Has Placed Order >= 2 over all time, ordine NON solo accessori]
    │
    │  In parallelo: se ordine contiene prodotti mai acquistati prima → trigger Flow 08-21 specifico
    ▼  (+2 ore)
EMAIL 1 — Grazie + costanza (Lorenzo, statica)
    │
    ▼  (+3 giorni)
EMAIL 2 — Cross-sell complementare (Flaminia, blocchi dinamici con esclusione "già posseduto")
    │
    ▼
Fine flow → entra in Retention specifico per il prodotto acquistato (gg 20-55)
```

---

## Note operative

### Logica esclusione "già posseduto"

Tutti i sotto-blocchi cross-sell hanno una condition aggiuntiva: il prodotto viene proposto **solo se il cliente non lo ha mai acquistato in passato**. Implementazione Klaviyo: usare "Placed Order metric → Item SKU equals X has happened zero times over all time" come show condition di ogni sotto-blocco.

Questa logica risolve il problema di proporre prodotti che il cliente ha già nel protocollo (es. cliente ha Paleocomplex + Youth e ricompra Paleocomplex → senza esclusione gli proporremmo Youth che già ha; con esclusione, il blocco Youth si nasconde e mostriamo solo Renaissance/Jeunesse).

### Niente sconto

Decisione confermata: nessun codice sconto in questo flow. Il cliente ricorrente è già fedele, lo sconto svaluta il prezzo pieno che ha appena pagato. Lo sconto resta per il win-back (flow 24-25, quando il cliente non torna da 85+ giorni).

### Link prodotti

Tutti i prodotti citati nei blocchi sono linkati alla pagina prodotto del sito. La guida alla scelta è linkata come fallback per chi vuole orientarsi.

### Coerenza con la matrice cross-sell del piano master

I suggerimenti seguono la matrice del piano master (sezione "Matrice cross-sell"):
- Multivitaminico → Collagene primario, Renaissance secondario, Sport trasversale
- Collagene Youth/Jeunesse → Multivitaminico se non l'ha + Renaissance + Sport trasversale
- Sport → L'altro prodotto sport + Multivitaminico
- Specifici → Multivitaminico come base

### Changelog
- v1.0 (2026-05-13): refactor architetturale. Email 1 riscritta in modo generico (no più "il primo ciclo ti è stato utile" che presupponeva ricompra dello stesso prodotto). Email 2 cross-sell: aggiunti conditional di esclusione "già posseduto" su ogni sotto-blocco prodotto (risolve il problema di proporre prodotti che il cliente ha già nel protocollo). Aggiunto fallback content block per edge case "cliente con storico completo". Aggiunto riferimento ai flow prodotto 08-21 che girano in parallelo per prodotti acquistati per la prima volta. Renamed da "Post Purchase Cliente Ricorrente" a "Cliente Ricorrente" per coerenza con nuovo schema.
- v0.1 (2026-05-11): bozza iniziale.
