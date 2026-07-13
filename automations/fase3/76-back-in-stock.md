**Versione:** 1.1
**Ultimo aggiornamento:** 2026-06-18

# Flow 76: Back in Stock

## Chi entra in questo flow

Chiunque si sia **iscritto a "Notify me when available"** per un prodotto esaurito. Quando il prodotto torna disponibile (restock in WooCommerce), Klaviyo invia una notifica immediata.

L'obiettivo è **massimizzare la conversione dell'esaurimento**: chi ha aspettato l'esaurimento vale come lead qualificato. La finestra di conversione post-restock è breve (24-48h), quindi tempistica cruciale.

## Razionale architetturale

**Perché serve**: senza questo flow, chi si iscrive per essere avvisato aspetta silenzio. Molti dimenticano, altri comprano dal competitor. Con la notifica automatica, catturi la maggioranza in 24h.

**Perché standalone (nessun conditional split)**: la logica è semplicissima. Non serve segmentare, non serve conditional. Klaviyo Academy raccomanda: **una email diretta con CTA forte**.

**Perché priorità BASSA nella Fase 3**: prerequisito tecnico serve un widget "Notify me" sul frontend + integrazione back-in-stock in Klaviyo. Setup ~30 minuti ma va fatto correttamente.

## Configurazione Klaviyo

**Trigger:** `Subscribed to Back In Stock` (metric event nativo Klaviyo)

**Come si integra tecnicamente**:
1. Aggiungere widget "Notify me when available" sulle pagine prodotto esaurite di paleocomplex.com. Klaviyo offre un widget nativo per WooCommerce (Klaviyo Onsite Forms).
2. Configurare il widget per inviare a Klaviyo l'evento `Subscribed to Back In Stock` con proprietà `product_id` e `variant_id`.
3. Configurare Klaviyo per tracciare quando lo stock del `product_id` torna disponibile (via webhook WooCommerce standard).

**Trigger filter:** nessuno

**Smart Sending:** **OFF** — questa è la classica email dove NON vuoi Smart Sending. Se il cliente ha ricevuto altre email nelle 24h passate, deve comunque ricevere questa (è la ragione per cui si è iscritto).

**Re-entry:** Allow re-entry sempre (chi si iscrive di nuovo dopo un altro esaurimento riceve di nuovo)

## Trigger — Machine Learning?

❌ **NO**. Event-based trigger nativo. Klaviyo intercetta il ritorno stock e triggera il flow. Nessun ML.

## Struttura email

**1 sola email, immediata dal trigger.**

| # | Timing | Mittente | Tema |
|---|--------|----------|------|
| 1 | Immediate | Flaminia (Customer Care) | "Il tuo prodotto è tornato disponibile!" — CTA diretto al prodotto |

## Coordinamento con altri flow

Nessun sormonto significativo. La email di back-in-stock è transazionale al 100% (il cliente l'ha esplicitamente richiesta), quindi ha priorità assoluta anche se il cliente è in altri flow. Klaviyo la gestisce naturalmente.

---

## EMAIL 1 — Flaminia (immediate dal trigger)

**Mittente:** Flaminia (Customer Care)
**Tipo:** Statica con dynamic content sul prodotto

### Oggetto (3 varianti A/B)

- A: Il tuo {{ event.product_name }} è di nuovo disponibile
- B: È tornato: {{ event.product_name }} di nuovo disponibile
- C: Come promesso: {{ event.product_name }} è di nuovo qui

### Preview text (3 varianti)

- A: Le scorte sono limitate. Ordina prima che finisca di nuovo.
- B: Ti avevamo detto che ti avremmo avvisato. Eccoci.
- C: Corri: è appena tornato disponibile.

### Corpo email

Ciao [NOME]

Sono Flaminia. Ottime notizie: **{{ event.product_name }}** è tornato disponibile sul nostro sito.

Ti scrivo subito perché avevi chiesto di ricevere l'avviso appena fosse tornato.

**[Vai al prodotto e ordina](https://paleocomplex.com/prodotto/{{ event.product_slug }})**

Una nota pratica: sui prodotti più richiesti, le scorte del primo rientro a volte finiscono in fretta. Se hai deciso di ordinarlo, meglio non aspettare troppo.

Spedizione veloce come sempre: 24-48h con corriere espresso.

Se hai domande sul prodotto, sul dosaggio, o su come integrarlo con quello che usi già, **rispondi a questa email**. Leggo io e ti rispondo.

A presto
Flaminia
Customer Care Paleocomplex

---

## Note operative

### Prerequisito tecnico: widget "Notify me"

Va installato **prima** di attivare il flow. Klaviyo offre widget nativi per WooCommerce (documenti nella loro Help > Onsite forms > Back in stock). Setup step-by-step:

1. Klaviyo Account → Signup Forms → Create form → tipo "Back in stock"
2. Configurare il form con branding Paleocomplex (font, colori, wording "Avvisami quando torna disponibile")
3. Embeddare il form nella pagina prodotto WooCommerce quando `stock_status = outofstock`
4. Verificare che il form invii evento `Subscribed to Back In Stock` con `product_id`, `product_name`, `product_slug`

### Nessun conditional split, nessuna serie

**Non aggiungere email 2/3**. Se il cliente non compra entro 24-48h dopo la notifica di restock, non serve inseguirlo con altre email — il prodotto potrebbe essere già di nuovo esaurito, o la finestra di interesse è passata. Meglio pulito e semplice.

### Smart Sending OFF — motivo strategico

Se un cliente ha ricevuto altre email nelle 24h passate (es. una newsletter), Smart Sending le sopprimerebbe. Ma la back-in-stock è la ragione per cui si è iscritto — deve arrivare. **Sempre OFF su questo flow**.

### Metriche da monitorare

- **Open rate**: dovrebbe essere altissimo (60-80%) — self-selected audience
- **Click-through rate**: 40-60% — interesse altissimo
- **Conversion rate**: 15-30% — molto sopra la media broadcast
- **Time-to-conversion**: mediana ≤ 24h (per capire se serve un follow-up)

### Coordinamento con Andrea per stock management

Andrea gestisce lo stock manualmente/via WooCommerce. Quando riordina prodotti esauriti:
- Aggiornare `stock_status` in WooCommerce → Klaviyo intercetta e triggera il flow
- Verificare che le webhook siano attive tra WooCommerce e Klaviyo (integrazione standard)

### Priorità di attivazione

**BASSA** ma **facile**: setup rapido, ROI immediato. Andrea può attivarlo in ogni momento post-migrazione Klaviyo, appena installato il widget "Notify me" sul frontend.

### Schema flow Klaviyo

```
[Subscribed to Back In Stock event → Trigger]
    │
    ▼ immediate
Email 1 Flaminia (prodotto disponibile, CTA diretto)
    │
    ▼
Fine flow
```

### Status
Bozza v1.0 — pronto per montaggio Klaviyo. Prerequisito: installare widget "Notify me" sulle pagine prodotto esaurite.

### Changelog
- **v1.1 (2026-06-18)**: fix da verifica content-verifier. Rimossa emoji 🎉 dall'oggetto A, oggetto B riformulato (via "Bentornato" gendered e "in stock" anglicismo), "ti eri iscritto" → "avevi chiesto di ricevere l'avviso" (neutro), claim scarsità ammorbidito ("le scorte del primo rientro a volte finiscono in fretta").
- v1.0 (2026-06-18): prima stesura. 1 email immediata Flaminia con dynamic content sul prodotto. Smart Sending OFF (trasazionale). Nessun sormonto con altri flow.
