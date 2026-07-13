**Versione:** 2.0
**Ultimo aggiornamento:** 2026-06-18

# Flow 78: Cross-Sell Data-Driven (Catalog Insights)

## Chi entra in questo flow

Clienti ricorrenti (Lifetime Orders ≥ 2) al raggiungimento della loro **Best Cross-Sell Date** calcolata da Klaviyo Catalog Insights basandosi su pattern product-level.

L'obiettivo è **suggerire il prodotto giusto al momento giusto** basandosi su cosa **acquistano tipicamente i clienti simili nel loro secondo/terzo ordine successivo**, non su regole hard-coded.

## Razionale architetturale

**Questo è l'UNICO punto di cross-sell automatico del sistema** (decisione Andrea 2026-06-18): la vecchia email 2 cross-sell del Flow 22 Cliente Ricorrente è stata rimossa (il 22 è ora un semplice grazie). Il Flow 78 esegue cross-sell **QUANDO Klaviyo dice che è il momento giusto**, che può essere T+30, T+45, o T+70gg dopo l'ultimo ordine a seconda del pattern del cliente.

**Perché usare Catalog Insights e non Predictive Analytics standard**: Klaviyo documenta esplicitamente:
> *"Best cross-sell date is based on product-level purchase data, taking into consideration multiple items in someone's last order and identifying sequential patterns. Expected date of next order does not take product-level data into account."*

Cioè Best Cross-Sell Date è **più preciso** perché sa QUALE prodotto ha comprato, non solo QUANDO ha comprato l'ultima volta.

**Perché nella Fase 3 solo con trial Marketing Analytics**: Catalog Insights è disponibile solo col piano Marketing Analytics avanzato. Andrea ha trial 30gg da 2026-06-18. Se il ROI a fine trial giustifica, il flow resta attivo con piano permanente.

## Configurazione Klaviyo

**Trigger:** Date property trigger: **`Best Cross-Sell Date`**

**Timing config nel trigger**:
- **Send on the date** (non "before the date") — Klaviyo Academy raccomanda esplicitamente di NON usare "before" perché la data è già il momento ottimale calcolato dall'AI
- **Ora di invio**: 10:00 (mattina in cui il target apre di più) o customizzabile
- **Giorni**: tutti i giorni (nessuna limitazione)

**Trigger frequency:** **`never`** (CRITICO — senza questa impostazione il flow rispedirebbe ogni ricalcolo settimanale)

**Trigger filter (flow filter all'ingresso):**
1. `Customer's Lifetime Number of Orders is at least 2`
2. `Placed Order zero times since starting this flow` (esce se ricompra)
3. `NOT currently in Flow 72 AI Repeat Purchase` (evita doppio push nello stesso periodo)

**Smart Sending:** OFF (email di valore, no cap frequency)

**Re-entry:** Allow re-entry, waiting period **180 days** (evita doppie cross-sell nella stessa finestra ~6 mesi)

## Trigger — Machine Learning?

✅ **SÌ, DUE volte**:
1. **`Best Cross-Sell Date`** è calcolato da Catalog Insights AI su pattern product-level di clienti che hanno comprato lo stesso prodotto
2. **`Next Best Product`** (contenuto dinamico dell'email) è determinato da AI Klaviyo su base profilo — suggerisce il prodotto migliore per QUESTO specifico cliente sulla base del suo ultimo acquisto

Doppio ML: uno per il timing, uno per il contenuto.

## Struttura email

**1 email singola con contenuto dinamico**. Il flow è volutamente snello perché il valore è nella precisione dell'AI, non nella lunghezza della sequenza.

| # | Timing | Mittente | Tema |
|---|--------|----------|------|
| 1 | Immediate dal trigger (10:00 AM) | Lorenzo Zarone | "Un suggerimento data-driven per il tuo protocollo" con `Next Best Product` block |

**Rationale per 1 sola email**: se il cliente non risponde al momento ottimale calcolato dall'AI, insistere con follow-up secondari è controproducente. Il valore del data-driven cross-sell è "sparare al momento giusto", non "sparare tante volte".

## Coordinamento con altri flow

- **Flow 22 Cliente Ricorrente** (post-purchase +2h): semplice grazie Lorenzo, nessun cross-sell (rimosso in v2.0 del flow 22)
- **Flow 72 AI Repeat Purchase**: agisce quando Klaviyo dice "sta per finire il suo prodotto" (ENO)
- **Flow 78 Cross-Sell Data-Driven** (questo): agisce quando Klaviyo dice "è il momento ottimale per suggerire un NUOVO prodotto complementare"

I tre lavorano insieme su temi diversi:
- 22 = grazie post-acquisto (relazione brand)
- 72 = reorder dello stesso prodotto
- 78 = cross-sell ottimale nel tempo (data-driven) — UNICO punto di cross-sell

**Filtro reciproco Flow 78 vs Flow 72**: `NOT currently in Flow 72`. Se il cliente è in Flow 72 (sta ricevendo reminder di reorder), non gli spariamo anche il cross-sell contemporaneamente. Aspettiamo che il 72 finisca (max 17gg).

---

## EMAIL 1 — Lorenzo (immediate dal trigger)

**Mittente:** Lorenzo Zarone
**Tipo:** Statica con blocco `Next Best Product` (dinamico Catalog Insights)

### Oggetto (3 varianti A/B)

- A: Un suggerimento per il tuo protocollo, basato sui dati
- B: Il prossimo passo naturale per te
- C: I clienti come te tipicamente aggiungono questo

### Preview text (3 varianti)

- A: C'è una combinazione che voglio suggerirti. Ti spiego perché adesso.
- B: Un prodotto che completa bene quello che usi già.
- C: Un suggerimento basato sui dati. Te lo spiego.

### Corpo email

Ciao [NOME]

Sono Lorenzo. Ti scrivo con un suggerimento un po' diverso dal solito.

Guardando i percorsi dei nostri clienti ho notato una cosa: **chi ha comprato quello che usi tu, a un certo punto aggiunge tipicamente un prodotto preciso al proprio protocollo**. E quel punto, per la maggior parte, è più o meno questo momento del percorso.

Non è una promozione. È un'osservazione che viene dai dati di migliaia di ordini, e credo valga la pena condividerla con te.

**Il prodotto suggerito per te:**

{% if person.next_best_product %}
### {{ person.next_best_product.name }}

![{{ person.next_best_product.name }}]({{ person.next_best_product.image_url }})

{{ person.next_best_product.description | truncatewords: 50 }}

**[Scopri {{ person.next_best_product.name }}]({{ person.next_best_product.url }})**

{% else %}
<!-- SETUP KLAVIYO: questo ramo NON deve mai arrivare al cliente. Configurare: (a) fallback reale con blocco "i più scelti dai nostri clienti", oppure (b) conditional split prima dell'email che fa uscire dal flow i profili senza next_best_product. -->
{% endif %}

---

**Perché te lo suggerisco adesso**: perché è questo il momento in cui, tipicamente, i benefici della combinazione si consolidano meglio. Prima sarebbe stato prematuro, dopo sarebbe un'occasione persa.

**Nota importante**: non è uno sconto e non è una promo a tempo. È solo un suggerimento basato su quello che vedo nei percorsi dei nostri clienti.

Se vuoi vedere il prodotto, approfondire, o rispondere a questa email per confrontarti su come integrarlo, **decidi tu**. Se non ti interessa, ignora pure: non insisterò con altre email su questo suggerimento.

Un forte abbraccio
Lorenzo Zarone
Fondatore di Paleocomplex

---

## Note operative

### Prerequisiti tecnici

Prima di attivare questo flow:
1. **Marketing Analytics attivo** — verificato durante il trial 30gg
2. **Catalogo prodotti sincronizzato** con Klaviyo (Catalog → Products) — Andrea deve verificare
3. **Revenue metric mapped** su evento `Placed Order` — Andrea deve verificare
4. **48h di processing** dopo attivazione Catalog Insights per calcolo iniziale
5. **`Best Cross-Sell Date`** compare come profile property nei profili clienti
6. **Blocco `Next Best Product`** disponibile nel template editor Klaviyo

### Blocco Next Best Product — come funziona

Klaviyo espone `Next Best Product` come blocco custom nel template email editor. Il blocco:
- Prende come input il profilo (automatico)
- Cerca la property `next_best_product` calcolata da AI
- Renderizza automaticamente immagine + nome + descrizione + link del prodotto

**Non serve scrivere codice**: si trascina il blocco nel template e Klaviyo fa il resto. Il fallback (se AI non ha suggerimento) è configurabile (es. "prodotti popolari" o "top venduti").

### Frequency "never" — motivo

Klaviyo Academy: senza `frequency = never` il flow rispedirebbe ogni volta che Klaviyo ricalcola Best Cross-Sell Date. Questo causerebbe email ripetute e unsubscribe. **Verificare sempre** che l'impostazione sia attiva.

### Perché una sola email

Klaviyo Academy: il cross-sell data-driven ha valore massimo AL MOMENTO ottimale calcolato dall'AI. Se il cliente non converte quel giorno, non c'è ragione di forzarlo con follow-up nei giorni successivi — il "momento migliore" è già passato. Meglio aspettare la prossima Best Cross-Sell Date (che Klaviyo ricalcolerà a un nuovo ordine).

### Metriche di successo del trial

A fine trial 30gg, per decidere se rinnovare piano Marketing Analytics:

- **Revenue attribuito al Flow 78** vs. costo del piano
- **Conversion rate**: target > 5% (molto sopra newsletter broadcast)
- **AOV** dei ricorrenti che hanno risposto al Flow 78 (dovrebbe salire — perché comprano prodotto extra)
- **Overlap con Flow 72**: quanti clienti hanno risposto a Flow 78 quando avevano già risposto a Flow 72 (Reorder)? Se alto overlap, il valore aggiunto è basso.

### Sormonto con Flow 22 Cliente Ricorrente — RISOLTO

Il sormonto è stato eliminato alla radice: la vecchia email 2 cross-sell del Flow 22 è stata **rimossa** (Flow 22 v2.0, decisione Andrea 2026-06-18). Il Flow 78 è ora l'unico punto di cross-sell automatico del sistema. Nessun rischio di suggerimenti duplicati.

### Schema flow Klaviyo

```
[Best Cross-Sell Date (per profilo) → Trigger]
    │
    ▼
[Trigger Filter]
  - Lifetime Number of Orders ≥ 2
  - Placed Order zero times since starting flow
  - NOT currently in Flow 72
    │
    ▼ immediate (10:00 AM)
Email 1 Lorenzo con blocco Next Best Product
    │
    ▼
Fine flow (re-entry consentito dopo 180gg)
```

### Status
Bozza v1.0 — richiede Marketing Analytics attivo per Catalog Insights. Da attivare in coda al Flow 72 (60-90gg dopo go-live) per dare tempo a Klaviyo di popolare `Best Cross-Sell Date` per la coorte clienti.

### Changelog
- **v2.0 (2026-06-18)**: fix da verifica content-verifier + decisione Andrea ("una cosa specifica su di te" assolutamente da togliere). Riscritta l'apertura dell'email: rimossi tutti i riferimenti a tool/AI/Klaviyo e alla segnalazione individuale → framing sul comportamento tipico dei clienti simili ("chi ha comprato quello che usi tu, a un certo punto aggiunge tipicamente..."). Rimossi anglicismi (data-driven, reminder). Promessa "non ti scriverò più" resa compatibile col re-entry 180gg. Ramo {% else %} del template trasformato in istruzione di setup esplicita (mai testo segnaposto al cliente).
- **v1.1 (2026-06-18)**: il Flow 78 diventa l'UNICO punto di cross-sell automatico. Rimossa la vecchia email 2 cross-sell del Flow 22 (che ora è un semplice grazie). Sormonto 22/78 risolto alla radice. Fix em-dash nei corpi email (regola skill paleo-email).
- v1.0 (2026-06-18): prima stesura. Trigger Best Cross-Sell Date (Catalog Insights). Content dinamico Next Best Product block. 1 email singola Lorenzo. ROI da valutare a fine trial 30gg per decidere upgrade piano Marketing Analytics permanente.
