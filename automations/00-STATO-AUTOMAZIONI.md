**Versione:** 1.0
**Ultimo aggiornamento:** 2026-07-27

# Stato e convenzioni — Automazioni Klaviyo

Documento di lavoro del sotto-progetto automazioni: dove siamo col montaggio e le convenzioni di copy che valgono solo per i flow.

**Non duplica niente.** Per il resto:

| Cosa cerchi | Dove |
|---|---|
| Architettura completa, tutte le fasi | [00-PIANO-MASTER-AUTOMAZIONI](00-PIANO-MASTER-AUTOMAZIONI.md) [[00-PIANO-MASTER-AUTOMAZIONI]] |
| Fase 3: trigger, ML, sormonti, filtri, strategia sconti | [fase3/00-mappatura-fase3](fase3/00-mappatura-fase3.md) [[00-mappatura-fase3]] |
| Come si monta un flow via API | `skills/montaggio-flow-klaviyo/SKILL.md` [[montaggio-flow-klaviyo]] |
| Convenzioni di scrittura valide su tutti i canali | `context/stile-contenuti.md` [[stile-contenuti]] |
| Chi firma cosa | [strategia-mittenti-email](strategia-mittenti-email.md) [[strategia-mittenti-email]] |

---

## Stato al 22 luglio 2026

### Fase 1 (01-07) — LIVE
Carrello abbandonato, Welcome ×2, Authority, Browse abandonment, Conversione, Welcome D3+K2.

- **Authority** `YimR66`: bug del segmento di handoff risolto il 17/7. Il nuovo welcome richiede la property `flow-XX-completed` più un OR nel segmento `Sjna4H`.
- **07 Welcome D3+K2** `SuFKGT`: creato via API, è il più recente della fase.

### Fase 2 (21-37) — MONTATA
- **21** Primo Cliente
- **22** Cliente Ricorrente, v2.0: solo ringraziamento, il cross-sell è stato tolto e spostato nel flow 78
- **23** Recensione Brand, parte a Fulfilled + 32 giorni
- **24-37** flow prodotto, trigger Fulfilled Order

### Fase 3 (71-78) — montaggio aperto dal 22/7

| Flow | Stato |
|---|---|
| **71** First-Order Reorder | ✅ **LIVE dal 22/7**, flow `UrwVp4` |
| 73 RFM Winback | pronto per il montaggio |
| 74 Sunset Lead | pronto per il montaggio |
| 75 Sunset Cliente Storico | pronto per il montaggio |
| 76 Back in Stock | pronto per il montaggio |
| 72 AI Repeat Purchase | in attesa di 60-90 giorni di dati |
| 78 Cross-Sell Data-Driven | in attesa di 60-90 giorni di dati |
| **77 Fedeltà** | ⏸ **SOSPESO** |

**Note sul 71**, che è l'unico già in produzione:
- Copy v4.3. La v4.1 ha introdotto i 3 rami con email **identiche**: cambiano solo le durate (T+25/30, T+50/58, T+120)
- I draft precedenti sono stati eliminati
- Restano da rifinire **a mano nel builder**: A/B sugli oggetti e deep-link di riordino
- ⚠️ **Da quando è live: mai ricreare il flow.** Solo builder o PATCH — i flow non si modificano via API, si ricreano, e ricrearne uno attivo significa perdere i dati

---

## Convenzioni copy specifiche dei flow

Queste valgono **in aggiunta** a `context/stile-contenuti.md`, che copre le convenzioni generali.

### Contatti (regola dal 22/7)

Per il supporto, sempre il link alla **[pagina di supporto](https://paleocomplex.com/contatti/)**.

- ❌ mai "rispondi a questa email" come canale di supporto — ammesso solo per raccogliere feedback o testimonianze
- ❌ mai "parla direttamente con Lorenzo"
- ✅ sempre al plurale: *"leggiamo sempre e ti rispondiamo"*

**Perché:** il supporto non è Lorenzo, e le risposte via reply si perdono. La pagina è tracciabile e ha una persona dietro.

### Recensioni

Nelle email si citano **solo recensioni reali**, prese dal file `context/20260511 paleocomplex export-reviews.csv`. Mai inventarne, mai parafrasarne una fino a cambiarne il senso.

### Chiusura delle email di riordino

Il blocco risparmio in fondo contiene, in quest'ordine:

1. Spedizione 24-48h
2. Metodi di pagamento: carta, PayPal, contrassegno
3. `PROMO3` 10% / `PROMO6` 15% (condizioni in `context/promo-rules.md`)
4. Programma fedeltà
5. Link a https://paleocomplex.com/promozioni/

### Coupon univoci

I coupon univoci generati da Klaviyo verso WooCommerce li crea Andrea, con **scadenza 15 giorni alle 00:00**. Quindi nel copy si scrive *"scade a mezzanotte del 14° giorno"*, e le email successive citano i giorni residui esatti.

---

## Storico utile

- **Mittenti**: Lorenzo per educativo e brand, Flaminia per il customer care. "Team Paleocomplex" è stato eliminato. Dettaglio in [strategia-mittenti-email](strategia-mittenti-email.md) [[strategia-mittenti-email]]
- **Codici**: `BENVENUTO` (€10, welcome), `PRIMOPASSO` (€10 + spedizione gratis, email 10 del flow conversione)
- **Trial Klaviyo Marketing Analytics** attivo dal 18/6 (RFM + Catalog Insights + Predictive). A fine trial valutare il rinnovo sui KPI indicati nella mappatura fase 3
- **Condivisione con Lorenzo**: repo GitHub `giavara/paleo` (push via clone in `/tmp`), pubblicato su GitHub Pages. Due pagine collegate, sorgente nel vault, si itera sui file e si ripusha (mai `_v2`):
  - overview 3 fasi → `presentazione-lorenzo-automazioni.html` v7.0
  - pagina dedicata Fase 3 → `presentazione-fase3.html` v1.0
