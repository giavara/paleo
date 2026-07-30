**Versione:** 1.0
**Ultimo aggiornamento:** 2026-07-28
**Status:** ✅ COMPLETATA — ActiveCampaign spento a fine giugno 2026. Documento di archivio.

# Migrazione ActiveCampaign → Klaviyo (archivio)

Piano tecnico e decisioni della migrazione, conclusa. Tenuto come backup: le regole di warmup e i costi servono se un domani si rifà una migrazione o si rinegozia il piano.

Roadmap operativa originale: `project/migrazione-klaviyo-roadmap.md` v2.0.

---

## Le fasi, come sono andate

| # | Fase | Esito |
|---|---|---|
| 0 | Setup tecnico | fatto |
| 1 | Costruzione automazioni Fase 1 su Klaviyo | fatto |
| 2 | Import 20K contatti attivi da AC + warmup dominio | fatto |
| 3 | Switch delle porte d'ingresso (form, popup, lead magnet) da AC a Klaviyo | fatto |
| 4 | Import 30K inattivi + re-engagement | giugno |
| 5 | Spegnimento ActiveCampaign | fine giugno |

---

## Regole di warmup del dominio

Da riusare se si dovesse ripetere l'operazione su un altro account o dominio.

- ⚠️ **Disattivare i flow prima di ogni import bulk.** L'import triggera i flow attivi.
- **Warmup manuale obbligatorio**, per segmenti crescenti: 30gg → 60gg → 90gg → 120gg → 180gg.
- L'open rate deve restare **sopra il 20%**, e sopra il **30%** nelle prime due settimane. Se scende, si torna indietro di un segmento.
- **Attivazione dei flow durante il warmup**: Welcome e Carrello dopo 2 settimane, Browse Abandonment dopo 30-60 giorni, Winback **solo a warmup completato**.
- I contatti inattivi si importano **dopo** il warmup, mai durante.
- Il CSV va **rigenerato il giorno stesso dell'import** (export fresco).

---

## Costi Klaviyo

| Voce | Costo |
|---|---|
| Email, fascia 20-25K contatti | $400/mese |
| Marketing Analytics (predictive, RFM, cross-sell) | +$120/mese |
| **Totale** | **$520/mese** |
| WhatsApp | non quotato, implementazione futura |

Il modulo Marketing Analytics è quello che alimenta i flow 72, 73 e 78 della Fase 3. Trial partito il 18/6.

---

## Risposte utili dalla call con Klaviyo (16 aprile 2026, Matteo Bassani)

- **Soft opt-in italiano**: a nostra discrezione. I clienti WooCommerce senza consenso esplicito restano profili attivi e raggiungibili per email legate al prodotto.
- **Warmup**: manuale, minimo 2-4 settimane. Klaviyo monitora e avvisa se l'audience è troppo grande.
- **Predictive analytics**: richiede il modulo Marketing Analytics. Gli ordini storici importati da WooCommerce contano ai fini del calcolo.
- **Onboarding**: programma Jump Start (webinar + task sheet + sessione 1-to-1 a 30 giorni).
- **Instagram DM automation**: Klaviyo ha acquisito un tool simile a ManyChat, potrebbe sostituirlo.
- **Customer Hub / Loyalty per WooCommerce**: rimasto in sospeso, Matteo doveva confermare.
