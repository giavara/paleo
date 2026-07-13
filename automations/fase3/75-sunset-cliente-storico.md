**Versione:** 1.0
**Ultimo aggiornamento:** 2026-06-18

# Flow 75: Sunset Cliente Storico

## Chi entra in questo flow

Clienti che **hanno comprato almeno una volta in passato** e sono **completamente scomparsi da 180 giorni**: nessun ordine, nessuna apertura email, nessun click. Sono ex-clienti dormienti.

L'obiettivo è **fare un ultimo tentativo di risveglio con toni caldi e long-term** e, se non funziona, **NON sopprimere hard** ma passare a frequenza ridotta. La logica: il cliente storico può tornare da solo tra 6-12 mesi (compleanno, cambio di vita, ricerca specifica), quindi mantenere il canale aperto vale la pena.

## Razionale architetturale

**Perché diverso dal Flow 74 Sunset Lead**: cliente storico ha investito soldi, tempo, fiducia. Toglierlo con "suppress + dimentica" è disrispettoso e strategicamente miope (i clienti storici possono tornare). Il flow è **soft e long-term**.

**Perché segmento comportamentale e non RFM "Inactive"**: RFM Inactive è calcolato su Recency/Frequency/Monetary insieme, non ha soglia esatta configurabile da noi. Segmento comportamentale ci dà controllo preciso su "180gg di silenzio totale" — soglia allineata al ciclo di vita reale del cliente Paleocomplex.

**Perché non usare sconto forte**: il cliente storico che non è tornato in 180gg dopo Flow 72 + Flow 73 + email winback probabilmente non ha bisogno solo di sconto. Ha bisogno di essere "ricontattato" con calore genuino. Uno sconto open-ended senza scadenza breve (per non forzare la mano) può aiutare.

## Configurazione Klaviyo

**Trigger:** **Ingresso in segmento** `Sunset Cliente Storico`

**Definizione del segmento (da creare in Lists & Segments → Create Segment):**

```
Nome: "Sunset Cliente Storico"
Definition (TUTTE le condizioni):
  Placed Order at least 1 time over all time
  AND Last placed order > 180 days ago
  AND Last opened email > 180 days ago (OR never opened in last 180gg)
  AND Last clicked email > 180 days ago (OR never clicked in last 180gg)
```

**Trigger filter (flow filter al momento dell'ingresso):**
1. `NOT currently in Flow 73 RFM Winback`
2. `Has not received Flow 73 last email in last 60 days` (aspetta che il 73 sia finito ed esaurito)
3. `Placed Order zero times since starting this flow`

**Smart Sending:** OFF (email importanti long-term)

**Re-entry:** Allow re-entry, waiting period **365 days** (evita di riscattare il flow ogni volta che il cliente esce brevemente dal segmento)

## Trigger — Machine Learning?

❌ **NO**. Segmento comportamentale con soglie esatte. Zero ML.

## Struttura email

**2 email + azione di frequenza ridotta** (non suppress hard):

| # | Timing | Mittente | Tema |
|---|--------|----------|------|
| 1 | T+0 dall'ingresso | Lorenzo Zarone | Ti vogliamo ancora + niente fretta + sconto open-ended 20% |
| 2 | +14gg dopo Email 1 | Flaminia (Customer Care) | "Se preferisci silenzio lo rispetto" + link gestione preferenze (no suppress hard) |
| Azione | +30gg dopo Email 2 senza engagement | (sistema) | Tag `Unengaged Storico` + riduzione frequenza a 1 newsletter/mese (NON suppression totale) |

## Coordinamento con altri flow

Vedi `00-mappatura-fase3.md` sezione Sormonti. Sintesi:
- Aspetta 60gg dalla fine del Flow 73 prima di scattare (perché sono state già mandate 2-3 email winback)
- Nessun conflitto con Flow 71/72 (che richiedono ordini recenti)
- Coordinato con Flow 74 Sunset Lead (segmenti mutuamente esclusivi: 74 richiede 0 ordini, 75 richiede ≥1)

---

## EMAIL 1 — Lorenzo (immediate dall'ingresso)

**Mittente:** Lorenzo Zarone
**Tipo:** Statica con codice sconto open-ended

### Oggetto (3 varianti A/B)

- A: Ci sei stato con noi. Volevo dirti solo una cosa.
- B: Niente fretta. Solo un pensiero da fondatore.
- C: Ti ricordo, ma senza pressione

### Preview text (3 varianti)

- A: Se un giorno vuoi tornare, ti aspetto qui.
- B: 20% aperto. Nessuna scadenza forzata.
- C: Niente automation cinico. Solo umanità.

### Corpo email

Ciao [NOME]

Sono Lorenzo. Ti scrivo da fondatore di Paleocomplex.

Ho controllato: hai fatto ordini con noi in passato. Poi c'è stato un silenzio lungo, di mesi. Il nostro sistema ti aveva segnalato "a rischio" tempo fa e ti abbiamo scritto per riprenderti. Non ha funzionato. Fair enough.

Ti scrivo adesso in modo diverso.

Non ti chiedo di ricomprare. Non ti offro uno sconto a tempo che scade tra 3 giorni e ti mette pressione. Ti dico una cosa sola: **se un giorno vorrai tornare, siamo qui**. Non tra 3 mesi, non tra 6, non tra 2 anni. Il pomodoro maturo si raccoglie quando è il momento.

Se e quando vorrai tornare, ti lascio un codice **aperto senza scadenza**: **BENTORNATO20**, il 20% sul tuo prossimo ordine, quando vorrai riprendere. Nessun trucco.

**[Vai al negozio](https://paleocomplex.com/negozio/)**

E se hai voglia di raccontarmi cosa è successo (un cambiamento di vita, un problema con i nostri prodotti, un cambio nelle tue priorità), **rispondi a questa email**. Leggo io, personalmente. Mi aiuta a capire meglio come lavorare.

Un forte abbraccio
Lorenzo Zarone
Fondatore di Paleocomplex

---

## EMAIL 2 — Flaminia (+14gg dopo Email 1)

**Mittente:** Flaminia (Customer Care)
**Tipo:** Statica con link gestione preferenze

### Oggetto (3 varianti A/B)

- A: Un ultimo pensiero, poi ti lascio scegliere
- B: Se preferisci silenzio, dimmelo
- C: Ci sei? Come stai?

### Preview text (3 varianti)

- A: Nessuna suppression forzata. Solo trasparenza.
- B: Puoi scegliere la frequenza che ti fa più comodo.
- C: Rispetto anche il non risposta.

### Corpo email

Ciao [NOME]

Sono Flaminia di Paleocomplex. Lorenzo ti ha scritto un paio di settimane fa. Ti scrivo io adesso con un ultimo pensiero, poi lascio decidere a te.

Se in queste settimane hai riflettuto e vuoi continuare a sentirci, ma con meno frequenza (per esempio, una sola newsletter al mese invece che una alla settimana), puoi impostarlo dalle preferenze:

**[Gestisci le tue preferenze](https://paleocomplex.com)**

Se preferisci silenzio totale, puoi anche scegliere di non ricevere più le nostre email. Nessun risentimento: è la tua scelta e la rispettiamo.

Se non fai niente, il nostro sistema per rispetto verso di te ridurrà automaticamente la frequenza delle email che ti mandiamo (una al mese al massimo, e solo contenuto di valore, mai push commerciale automatico).

Continuo a lasciarti il codice **BENTORNATO20** (20% di sconto sul prossimo ordine, senza scadenza) se un giorno vorrai tornare a trovarci.

Ti auguro il meglio, davvero.

Flaminia
Customer Care Paleocomplex

---

## AZIONE AUTOMATICA — Tag + Frequency Reduction

**Timing:** +30 giorni dopo Email 2, se il profilo non ha né aperto né cliccato né riattivato

**Azione Klaviyo:**
1. **Update Profile Property**: `frequency_preference = monthly` (o profile property custom `unengaged_storico = true`)
2. **NON suppression totale** — il profilo resta attivo ma esclude da broadcast frequenti
3. **Include solo in newsletter mensile** con contenuto forte, no push commerciale

### Differenza chiave con Flow 74 Sunset Lead

Il Flow 74 (mai-clienti) fa **suppress totale**: elimina dalle broadcast. Il Flow 75 (clienti storici) fa **frequenza ridotta**: mantiene canale attivo con 1 email/mese.

Motivo: i dati mostrano che il 5-8% dei clienti "storici dormienti" torna spontaneamente entro 12 mesi (compleanno, cambio abitudini, ricerca specifica). Se li abbiamo cancellati, li perdiamo. Se li teniamo con frequency ridotta, siamo lì quando tornano.

---

## Note operative

### Codice BENTORNATO20 senza scadenza — perché

**Contro-intuitivo ma efficace**: uno sconto senza scadenza forzata rimuove la "pressione" che tipicamente fa scattare la resistenza del cliente. Il cliente storico che è stato via 180gg non torna per una scadenza artificiale di 7 giorni. Torna quando è pronto. Il codice open-ended dice: "ti aspettiamo, senza fretta".

**Nota operativa**: BENTORNATO20 è statico, riutilizzabile. Configurare in WooCommerce app coupon come codice utente-specifico (uno per email) tramite Yith Coupon Email o simile, oppure come codice globale con limit 1 uso per cliente. Klaviyo non è coinvolto nell'univocità (a differenza del Flow 73 High CLV Email 3).

### Perché Lorenzo Email 1 + Flaminia Email 2

Lorenzo apre con il pensiero da fondatore (calore, autorità). Flaminia chiude con l'operativo (gestione preferenze, umanità del customer care). Coppia collaudata già usata negli altri flow.

### Come segmentare la newsletter mensile "frequenza ridotta"

Andrea deve creare in Klaviyo:
1. Segmento "Newsletter Frequenza Ridotta": `frequency_preference = monthly` OR `unengaged_storico = true`
2. Escludere questo segmento dalle campaign broadcast normali (settimanali)
3. Includerlo in una campaign dedicata mensile con contenuto "best-of"

### Sormonto con Flow 73 RFM Winback

Cliente esce dal Flow 73 senza riordinare, RFM lo classifica "Inactive" dopo altre settimane. Segmento Flow 75 lo cattura (180gg totali). Filtro reciproco: Flow 75 richiede `Has not received Flow 73 last email in last 60 days`. Cioè aspettiamo 2 mesi che il Flow 73 abbia dato modo di rispondere.

### Metriche da monitorare

- **Reactivation rate**: quanti hanno cliccato "voglio restare" o hanno riacquistato (target: 5-10%)
- **Utilizzo BENTORNATO20**: quanti codice riscattati in 6-12 mesi post-flow (target: 3-5%)
- **Complaint rate su newsletter mensile ridotta**: deve essere < 0.1%

### Schema flow Klaviyo

```
[Segmento Sunset Cliente Storico → Trigger su ingresso]
    │
    ▼
[Trigger Filter]
  - Placed Order ≥ 1 over all time (implicito nel segmento)
  - NOT currently in Flow 73
  - Has not received Flow 73 last email in last 60 days
  - Placed Order zero times since starting flow
    │
    ▼ immediate
Email 1 Lorenzo (BENTORNATO20 open-ended, no fretta)
    │
    ▼ wait 14 days [filter: no order since]
    ▼
Email 2 Flaminia (gestione preferenze, no suppression hard)
    │
    ▼ wait 30 days [filter: no engagement in 30 days]
    ▼
Update Profile Property: frequency_preference = monthly + tag "Unengaged Storico [DATA]"
    │
    ▼
(Non suppress. Il profilo continua a ricevere newsletter mensile ridotta)
```

### Status
Bozza v1.0 — pronto per montaggio Klaviyo. Da attivare in parallelo con Flow 74 ma monitorando che i filtri di esclusione con Flow 73 funzionino.

### Changelog
- v1.0 (2026-06-18): prima stesura. Segmento comportamentale (1+ ordini + 180gg inattivo totale). 2 email caldre Lorenzo + Flaminia + azione di frequency reduction (NON suppression hard). Sconto BENTORNATO20 open-ended senza scadenza. Coordinamento con Flow 73 (60gg gap). Filosofia long-term retention diversa dal Flow 74 Lead.
