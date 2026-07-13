**Versione:** 1.0
**Ultimo aggiornamento:** 2026-06-18

# Flow 74: Sunset Lead (Iscritti mai-clienti)

## Chi entra in questo flow

Iscritti alla newsletter **da oltre 180 giorni** che **non hanno mai acquistato** e sono completamente disingaggiati (nessuna apertura né click nelle ultime 90gg).

L'obiettivo è **pulire la lista** di contatti che non sono e non saranno mai clienti, per proteggere deliverability, aumentare open rate reali su chi resta, e ridurre costi email. Chi non risponde a questo flow viene soppressa dalle broadcast future.

## Razionale architetturale

**Perché serve un Sunset**: Klaviyo raccomanda esplicitamente di pulire la lista periodicamente. Gli iscritti disingaggiati abbassano la reputazione del dominio mittente, causano più email in spam per TUTTI gli iscritti, e occupano quota nel piano Klaviyo. Meglio 5.000 iscritti attivi che 15.000 con 10.000 fantasmi.

**Perché "Lead" e non "Cliente Storico"**: distinguere è importante perché i due profili hanno valore diverso. Il cliente storico (Flow 75) merita nurturing soft, il lead mai-cliente (Flow 74) è puro peso morto se non risponde.

**Perché 180gg**: soglia standard Klaviyo per re-engagement. Sotto è prematuro, sopra è inutile.

## Configurazione Klaviyo

**Trigger:** **Ingresso in segmento** `Sunset Lead` (segmento da creare in Klaviyo)

**Definizione del segmento (da creare in Lists & Segments → Create Segment):**

```
Nome: "Sunset Lead"
Definition (TUTTE le condizioni):
  Subscribed to email > over 180 days ago
  AND Placed Order zero times over all time
  AND Last opened email > 90 days ago (OR never opened)
  AND Last clicked email > 90 days ago (OR never clicked)
```

**Trigger filter:** nessuno (il segmento già filtra tutto)

**Smart Sending:** OFF (queste sono email importanti di ultima chance)

**Re-entry:** non applicabile (dopo suppress il profilo esce dal segmento)

## Trigger — Machine Learning?

❌ **NO**. Segmento puramente comportamentale, calcolato da Klaviyo con logica if/then su proprietà standard. Nessun ML coinvolto.

## Struttura email

**2 email + 1 azione automatica**:

| # | Timing | Mittente | Tema |
|---|--------|----------|------|
| 1 | T+0 dall'ingresso | Lorenzo Zarone | "Mi senti ancora?" — richiesta esplicita di conferma interesse |
| 2 | +7gg dopo Email 1 | Lorenzo Zarone | "Ultima nota. Rispetto la tua scelta" — link gestione preferenze |
| Azione | +3gg dopo Email 2 senza engagement | (sistema) | Tag `Unengaged` + Suppress da broadcast future |

## Coordinamento con altri flow

Nessun sormonto: chi è in Flow 74 non ha mai acquistato (Placed Order = 0), quindi non può essere in Flow 71/72/73/75 (che richiedono almeno 1 ordine). Standalone.

---

## EMAIL 1 — Lorenzo (immediate dall'ingresso)

**Mittente:** Lorenzo Zarone
**Tipo:** Statica

### Oggetto (3 varianti A/B)

- A: Ancora interessato? Domanda seria
- B: Ci sei? Un check onesto
- C: Prima che ti tolga dalla lista, un pensiero

### Preview text (3 varianti)

- A: Da 6 mesi non apri le nostre email. Legittimo, ma…
- B: Ci sei un motivo per cui sei ancora iscritto?
- C: 30 secondi per decidere.

### Corpo email

Ciao [NOME]

Sono Lorenzo, fondatore di Paleocomplex. Ti scrivo direttamente perché il nostro sistema mi segnala che sei iscritto alla newsletter da oltre 6 mesi ma non stai leggendo quello che ti mandiamo.

Ci sono due possibilità.

**La prima**: le nostre email finiscono in spam o in una cartella secondaria e non le vedi. In quel caso, se ci tieni a continuare a ricevere i nostri contenuti (integrazione, nutrizione, ricerca scientifica), aggiungi il nostro indirizzo alla tua rubrica o alla lista dei contatti prioritari. Poi resta qui, ti scriverò di nuovo.

**La seconda**: hai perso interesse, la tua vita è cambiata, o semplicemente non è più un topic per te in questo momento. Va bene assolutamente. Non è un giudizio, e non c'è nulla di male.

Quello che ti chiedo è di scegliere. Se resti interessato, **clicca qui e conferma che vuoi restare**:

**[Sì, voglio continuare a ricevere contenuti Paleocomplex](https://paleocomplex.com)**

Se invece hai deciso che non fa per te, non fare niente. Tra qualche giorno ti scriverò un'ultima email e poi non ti disturberò più.

Ci mancherai, ma non voglio essere invadente. La cosa più importante per un progetto come il nostro è avere iscritti che vogliono davvero essere qui.

Un forte abbraccio
Lorenzo Zarone
Fondatore di Paleocomplex

---

## EMAIL 2 — Lorenzo (+7gg dopo Email 1, ultima)

**Mittente:** Lorenzo Zarone
**Tipo:** Statica con link gestione preferenze

### Oggetto (3 varianti A/B)

- A: L'ultima email che ricevi da noi (probabilmente)
- B: Silenzio. Rispetto anche questo.
- C: Se ci sei, batti un colpo

### Preview text (3 varianti)

- A: Nessuna manipolazione. Solo una decisione da prendere.
- B: Dopo di questa, ti tolgo dalla lista.
- C: Un click per continuare, niente per uscire.

### Corpo email

Ciao [NOME]

Sono Lorenzo di nuovo. Una settimana fa ti ho scritto per chiederti se volessi continuare a ricevere le nostre email. Non ho ricevuto risposta.

È OK. Rispetto anche il silenzio.

Ma prima di toglierti dalla lista automaticamente (cosa che farò tra qualche giorno), voglio darti un'ultima occasione onesta.

Se vuoi continuare, ti basta cliccare qui:

**[Voglio restare: riattiva la mia iscrizione](https://paleocomplex.com)**

Se non fai niente, tra qualche giorno il nostro sistema smetterà di scriverti. Non riceverai più email da Paleocomplex, né newsletter né promo.

Nessun risentimento da parte mia. Le liste devono restare pulite, e chi non è più interessato è giusto che non riceva contenuti che non legge.

Se un giorno vorrai tornare, ti basterà iscriverti di nuovo dal sito. Ti accoglieremo con la stessa serietà.

Grazie del tempo.

Un forte abbraccio
Lorenzo Zarone
Fondatore di Paleocomplex

---

## AZIONE AUTOMATICA — Suppress + Tag

**Timing:** +3 giorni dopo Email 2, se il profilo non ha né aperto né cliccato né riattivato

**Azione Klaviyo:**
1. **Update Profile**: aggiungi tag `Unengaged - Sunset Lead 2026-06-XX` (con data del sunset)
2. **Suppress Profile**: sopprimi da email marketing

Questa azione è configurabile in Klaviyo via "Update Profile Property" step + "Suppress" action nel flow builder.

**Nota**: la suppression NON cancella il profilo. Se un giorno il cliente si iscrive di nuovo o compra, viene automaticamente riabilitato.

---

## Note operative

### Nessun sconto in questo flow

Un lead che non ha mai comprato e non risponde da 180gg non è un cliente da recuperare con lo sconto. Se non ha convertito con 6 mesi di welcome + newsletter + autority flow, non lo farà con -10%. Meglio sopprimere e concentrarci sui contatti attivi.

### Perché Lorenzo mittente per entrambe

Su un tema "delicato" come "ti sto togliendo dalla lista", la voce del fondatore è più credibile e onesta di un "team". Lorenzo che dice "va bene, rispetto" ha peso. Team Paleocomplex che dice lo stesso suona come automation cinico.

### Impatto atteso

Su un database tipico di ecommerce, il segmento Sunset Lead raccoglie 10-25% degli iscritti. Se dopo il flow ne recuperi il 3-5%, hai già vinto. Il resto è pulizia sana.

### Metriche da monitorare

- **Reactivation rate**: quanti hanno cliccato "voglio restare" (target: 3-5%)
- **Delta open rate sulla lista attiva** dopo la suppression (dovrebbe salire di 2-4 punti percentuali)
- **Delta unsubscribe rate**: non deve salire

### Schema flow Klaviyo

```
[Segmento Sunset Lead → Trigger su ingresso]
    │
    ▼ immediate
Email 1 Lorenzo (mi senti ancora?)
    │
    ▼ wait 7 days
[Filter: Opened or Clicked in last 7 days? YES → EXIT, NO → continua]
    │
    ▼
Email 2 Lorenzo (ultima nota)
    │
    ▼ wait 3 days
[Filter: Opened or Clicked in last 3 days? YES → EXIT]
    │
    ▼
Update Profile Property: tag "Unengaged - Sunset Lead [DATA]"
    │
    ▼
Suppress Profile (from broadcast + flow)
```

### Status
Bozza v1.0 — pronto per montaggio Klaviyo. Da attivare con calma monitorando l'impatto.

### Changelog
- v1.0 (2026-06-18): prima stesura. Segmento comportamentale (iscritti mai-clienti + 180gg + no engagement 90gg). 2 email Lorenzo + suppress automatico. Nessuno sconto (lead che non ha convertito in 180gg non è recuperabile con sconto).
