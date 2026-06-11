**Versione:** 1.0
**Ultimo aggiornamento:** 2026-06-11

# Flow 23: Recensione Brand

## Chi entra in questo flow

Tutti i clienti che hanno ricevuto fisicamente il prodotto (ordine passato a Completed in WooCommerce), indipendentemente dal fatto che sia il primo ordine o un riacquisto.

Il flow gira **in parallelo** ai flow stato cliente (07 Primo Cliente / 08 Cliente Ricorrente) e ai flow prodotto (09-22). È un flow universale post-acquisto che anticipa di 2 giorni la richiesta recensione automatica di WooCommerce.

L'obiettivo è preparare il cliente alla recensione, abbassare la friction e migliorare il response rate dell'email di sistema WooCommerce che arriva subito dopo.

## Configurazione Klaviyo

**Trigger:** Fulfilled Order (Order Completed in WooCommerce)

**Delay dal trigger:** 32 giorni

**Filtro principale:**
- Items contains at least one supplement (escludiamo accessori-only, vedi nota sotto)

**Filtro accessori:**
- Items contains almeno 1 SKU della linea integratori (Elisir, Revolution, Essentiel, Paleocomplex, Elisir Basic, Youth, Jeunesse, Hurricane, Armageddon, Artosan, Liverty, Testoplus, Renaissance, Vitamina D)
- Se l'ordine contiene SOLO accessori (Lampada Apollo, occhiali, libri), il flow NON parte (l'email WC automatica continuerà a partire comunque per quei prodotti)

**Effetto su altri flow:**
- Non interferisce con flow 07/08 (stato cliente) né con 09-22 (prodotto): timing distante
- L'email WC automatica con oggetto "⭐⭐⭐⭐⭐ Quante stelle daresti a Paleocomplex?" parte a +34gg dal Completed → questo flow la anticipa di esattamente 2 giorni

## Mittenti

| # | Email | Mittente |
|---|-------|----------|
| 1 | Anticipo richiesta recensione | Flaminia (Customer Care) |

## Timeline

| # | Timing (dal Fulfilled) | Delay Klaviyo | Tema | Tipo |
|---|------------------------|---------------|------|------|
| 1 | +32gg | 32 days from trigger | Anticipa email WC ⭐⭐⭐⭐⭐ | Statica |

**Coordinamento WooCommerce:**

```
Fulfilled+0    → Ordine spedito (status WC = completed)
Fulfilled+2gg  → Tipicamente consegnato fisicamente al cliente
Fulfilled+32gg → [23] Nostra anticipazione recensione (questa email)
Fulfilled+34gg → [WC] Email automatica WooCommerce "⭐⭐⭐⭐⭐"
```

Il gap di 2 giorni è esatto perché entrambi gli eventi partono dal Completed.

---

## EMAIL 1 — Anticipo richiesta recensione (+32 giorni dal Fulfilled)

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

**Tra due giorni** riceverai un'email automatica dal nostro sistema con oggetto **"⭐⭐⭐⭐⭐ Quante stelle daresti a Paleocomplex?"**. È un invito ufficiale a lasciare una recensione sul prodotto che hai comprato.

Per noi le recensioni dei clienti contano davvero. Più di qualunque pubblicità che potremmo fare. Il mondo degli integratori è pieno di promesse vuote e prodotti che non mantengono quello che dichiarano. Le recensioni reali sono l'unico modo che hanno le persone serie di capire chi vale la pena ascoltare.

Non serve scrivere un trattato. Bastano un voto e qualche parola su quello che hai notato. Anche solo "energia più stabile durante la giornata" o "pelle più morbida dopo tre settimane" è prezioso. E se hai trovato qualcosa che non ti convince, dillo: i feedback meno entusiastici sono quelli che ci aiutano a migliorare.

Se non trovi l'email tra un paio di giorni controlla in spam o posta indesiderata.

Grazie davvero per la fiducia che ci hai dato finora.

Flaminia
Customer Care Paleocomplex

---

## Note operative

### Perché un flow dedicato e non email 3 del flow 07
Inizialmente la richiesta recensione era email 3 del flow 06 (poi 07 dopo rinumerazione), triggerata su Placed Order +32gg. Problema: l'email WC automatica parte da Completed +34gg, non da Placed. Quindi il gap tra le due variava da 1 a 5 giorni (per ordini weekend con fulfilled lento). Il copy "Tra poche ore riceverai..." rompeva su una parte degli ordini.

Spostando il trigger a Fulfilled +32gg, il gap è sempre esatto di 2 giorni. Copy "Tra due giorni riceverai" sempre vero.

In più questo flow vale sia per primi clienti che per ricorrenti (entrambi possono ricevere richiesta recensione per ogni ordine), quindi è universale → ha senso staccato dai flow stato cliente che invece sono divisi tra primo/ricorrente.

### Filtri Klaviyo aggiuntivi da valutare in seconda battuta
- Escludere clienti che hanno già lasciato recensione negli ultimi 90 giorni (per evitare di chiedere recensione a ogni riacquisto). Da decidere se vogliamo una recensione per ogni ordine o solo periodicamente.
- Smart Sending: attivo (rispetta limite frequenza per profilo).

### Schema flow

```
[Order Completed = Fulfilled in WC + contiene almeno 1 integratore]
    │
    ▼  (+32 giorni)
EMAIL 1 — Anticipo richiesta recensione (Flaminia, statica)
    │
    ▼  (+2 giorni reali)
Email automatica WooCommerce "⭐⭐⭐⭐⭐ Quante stelle daresti a Paleocomplex?"
```

### Mittente
Flaminia, coerente con le altre comunicazioni Customer Care del piano (vedi piano master, sezione mittenti).

### Status
Bozza v1.0 — pronto per montaggio Klaviyo. Copy migrato dal vecchio Flow 06 email 3 con piccoli adattamenti ("Tra poche ore" → "Tra due giorni" coerente con il delay esatto).
