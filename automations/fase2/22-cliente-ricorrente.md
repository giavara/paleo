**Versione:** 2.0
**Ultimo aggiornamento:** 2026-06-18

# Flow 22: Stato Cliente — Cliente Ricorrente

## Chi entra in questo flow

Persone che hanno effettuato un **ordine successivo al primo** (Has Placed Order >= 2 over all time).

Il flow lavora sulla **relazione brand**: un semplice grazie che valida il riacquisto e rinforza la costanza. L'educazione specifica sui prodotti (istruzioni, aspettative, social proof) per **prodotti acquistati per la prima volta** è gestita dai **flow prodotto 24-37** che girano in parallelo. Il **cross-sell è gestito dal Flow 78 Cross-Sell Data-Driven** (Catalog Insights), che sceglie prodotto e momento con l'AI di Klaviyo invece che con regole fisse.

L'obiettivo del flow è:
- Validare il riacquisto e rinforzare la decisione di fedeltà
- Rinforzare il messaggio della costanza (filosofia Lorenzo)

## Configurazione Klaviyo

**Trigger:** Placed Order

**Filtro principale:**
- Has Placed Order at least 2 times over all time (non è il primo acquisto)

**Filtro accessori (escludere chi compra SOLO accessori):**
- Items contains at least one supplement (Elisir, Revolution, Essentiel, Paleocomplex, Elisir Basic, Youth, Jeunesse, Hurricane, Armageddon, Artosan, Liverty, Testoplus, Renaissance, Vitamina D)
- Se l'ordine contiene SOLO accessori (Lampada Apollo, occhiali, libri), il flow NON parte

**Smart Sending:** OFF

**Re-entry:** Allow re-entry a ogni ordine (è un grazie transazionale, giusto che arrivi ogni volta)

**Effetto su altri flow:**
- Il flow 21 (Primo Cliente Assoluto) NON parte (filtro Has Placed Order = 1)
- I flow prodotto 24-37 girano in parallelo per i prodotti dell'ordine acquistati per la prima volta in assoluto
- Il Flow 78 Cross-Sell Data-Driven gira in parallelo e suggerisce il prodotto complementare alla Best Cross-Sell Date calcolata dall'AI
- Il Flow 23 Recensione Brand parte a Fulfilled+32gg

## Mittenti

| # | Email | Mittente |
|---|-------|----------|
| 1 | Grazie + costanza | Lorenzo Zarone |

## Timeline

| # | Timing (T+X dal trigger) | Delay Klaviyo | Tema | Tipo |
|---|--------------------------|---------------|------|------|
| 1 | +2h dal Placed | 2 hours from trigger | Grazie per essere tornato + costanza | Statica |

**Coordinamento con altri flow:**
- L'email di conferma ordine arriva da WooCommerce standard
- La richiesta recensione automatica WooCommerce è a +34gg dal Completed
- Se il cliente acquista un prodotto mai provato, i flow prodotto specifici 24-37 girano in parallelo (es. cliente esistente compra Elisir per la prima volta: riceve questo flow + flow 26 Elisir specifico)
- Il cross-sell arriva via Flow 78 alla Best Cross-Sell Date del cliente (tipicamente T+30-90gg, calcolata dall'AI di Klaviyo)

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

Per qualsiasi cosa scrivici dalla nostra **[pagina di supporto](https://paleocomplex.com/contatti/)**.

Un forte abbraccio
Lorenzo Zarone
Fondatore di Paleocomplex

---

## Schema del flow

```
[Placed Order, Has Placed Order >= 2 over all time, ordine NON solo accessori]
    │
    │  In parallelo: se ordine contiene prodotti mai acquistati prima → trigger Flow 24-37 specifico
    │  In parallelo: Flow 78 Cross-Sell Data-Driven alla Best Cross-Sell Date (AI)
    │  In parallelo: Flow 23 Recensione Brand a Fulfilled+32gg
    ▼  (+2 ore)
EMAIL 1 — Grazie + costanza (Lorenzo, statica)
    │
    ▼
Fine flow
```

---

## Note operative

### Dove è finito il cross-sell

Fino alla v1.2 questo flow conteneva una seconda email di cross-sell (Flaminia, +7gg) con 4 blocchi dinamici per famiglia + esclusione "già posseduto". **Rimossa nella v2.0**: il cross-sell è ora gestito dal **Flow 78 Cross-Sell Data-Driven**, che usa Catalog Insights di Klaviyo (Best Cross-Sell Date + Next Best Product) per scegliere il prodotto e il momento con l'AI invece che con la matrice hard-coded.

Vantaggi del passaggio:
- Il suggerimento arriva al momento in cui i clienti simili effettivamente aggiungono quel prodotto (pattern reali, non regole fisse)
- Zero manutenzione della matrice cross-sell (l'AI si aggiorna da sola coi dati)
- Nessun rischio di suggerire un prodotto già posseduto (Next Best Product lo esclude nativamente)
- Un solo punto di cross-sell = zero rischio di email duplicate

Il copy della vecchia email 2 (blocchi famiglia + sport trasversale) resta recuperabile nella history git del file, se mai servisse per una campagna broadcast.

### Niente sconto

Nessun codice sconto in questo flow. Il cliente ricorrente è già fedele, lo sconto svaluta il prezzo pieno che ha appena pagato. Lo sconto vive nei flow di retention/winback (72 Below-CLV, 73 At Risk).

### Changelog
- **v2.0 (2026-06-18)**: rimossa Email 2 Cross-sell (Flaminia +7gg con blocchi dinamici). Il cross-sell migra al Flow 78 Cross-Sell Data-Driven basato su Catalog Insights (decisione Andrea 2026-06-18, dopo attivazione trial Marketing Analytics). Il flow diventa un semplice grazie: 1 email Lorenzo +2h. Rimosso open loop "Flaminia ti scriverà" dall'email 1. Aggiunta timeline con dual notation delay Klaviyo.
- v1.2 (2026-06-11): spostato cross-sell email 2 da T+5gg a T+7gg dal Placed (fix conflitto timing con Aspettative dei flow prodotto).
- v1.1 (2026-06-11): spostato cross-sell email 2 da T+3gg a T+5gg dal Placed (fix iniziale conflitto con Istruzioni prodotto).
- v1.0 (2026-05-13): refactor architetturale. Email 1 riscritta generica. Email 2 cross-sell con conditional esclusione "già posseduto". Renamed da "Post Purchase Cliente Ricorrente" a "Cliente Ricorrente".
- v0.1 (2026-05-11): bozza iniziale.
