**Versione:** 2.0
**Ultimo aggiornamento:** 2026-07-14

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

**3 email + 1 azione automatica** (v2.0, decisione Andrea 2026-07-14: lo sconto entra anche qui come ultima carta — chi non ha mai comprato potrebbe avere avuto il prezzo come freno, e visto che sta uscendo dalla lista, ogni conversione è guadagno puro):

| # | Timing | Mittente | Tema | Sconto |
|---|--------|----------|------|--------|
| 1 | T+0 dall'ingresso | Lorenzo Zarone | "Mi senti ancora?" — conferma interesse | NO |
| 2 | +7gg dopo Email 1 | Lorenzo Zarone | Ultima occasione + **20% univoco** ("se il freno era il prezzo") | **20%** |
| 3 | +7gg dopo Email 2 | Flaminia | Reminder codice + invito gentile a scegliere (resta o disiscriviti) | reminder 20% |
| Azione | +3gg dopo Email 3 | (sistema) | Suppress SOLO chi ha zero aperture e zero click su tutte e 3 le email | — |

**Logica engagement (il "segnale di interesse" che chiedeva Andrea)**: chi apre o clicca anche solo una delle 3 email dimostra interesse residuo → NON viene soppresso, resta in lista normale. Chi non interagisce con nessuna delle 3 → tag `Unengaged` + suppression. Il click sul codice sconto è il segnale più forte (per quello lo sconto sta in email 2 E 3: fa anche da test di interesse).

## Coordinamento con altri flow

Nessun sormonto: chi è in Flow 74 non ha mai acquistato (Placed Order = 0), quindi non può essere in Flow 71/72/73/75 (che richiedono almeno 1 ordine). Standalone.

---

## EMAIL 1 — Lorenzo (immediate dall'ingresso)

**Mittente:** Lorenzo Zarone
**Tipo:** Statica

### Oggetto (3 varianti A/B)

- A: Ti interessa ancora? Domanda seria
- B: Ci sei? Un check onesto
- C: Prima che ti tolga dalla lista, un pensiero

### Preview text (3 varianti)

- A: Da 6 mesi non apri le nostre email. Legittimo, ma…
- B: C'è un motivo per cui ricevi ancora le nostre email?
- C: 30 secondi per decidere.

### Corpo email

Ciao [NOME]

Sono Lorenzo, fondatore di Paleocomplex. Ti scrivo direttamente perché la tua iscrizione alla newsletter risale a oltre 6 mesi fa, ma non stai leggendo quello che ti mandiamo.

Ci sono due possibilità.

**La prima**: le nostre email finiscono in spam o in una cartella secondaria e non le vedi. In quel caso, se ci tieni a continuare a ricevere i nostri contenuti (integrazione, nutrizione, ricerca scientifica), aggiungi il nostro indirizzo alla tua rubrica o alla lista dei contatti prioritari. Poi resta qui, ti scriverò di nuovo.

**La seconda**: hai perso interesse, la tua vita è cambiata, o semplicemente non è più un argomento che ti interessa in questo momento. Va bene assolutamente. Non è un giudizio, e non c'è nulla di male.

Quello che ti chiedo è di scegliere. Se vuoi restare, **clicca qui e confermalo**:

**[Sì, voglio continuare a ricevere contenuti Paleocomplex](https://paleocomplex.com)**

Se invece hai deciso che non fa per te, non fare niente. Tra qualche giorno ti scriverò un'ultima email e poi non ti disturberò più.

Ci mancherai, ma non voglio essere invadente. La cosa più importante per un progetto come il nostro è avere iscritti che vogliono davvero essere qui.

Un forte abbraccio
Lorenzo Zarone
Fondatore di Paleocomplex

---

## EMAIL 2 — Lorenzo (+7gg dopo Email 1) — Ultima occasione + 20%

**Mittente:** Lorenzo Zarone
**Tipo:** Statica con codice sconto univoco

### Oggetto (3 varianti A/B)

- A: Prima di salutarci: un regalo, se ti va
- B: Il 20% che non ti ho mai dato
- C: Se il freno era il prezzo, adesso non lo è più

### Preview text (3 varianti)

- A: Un codice personale del 20%, valido 14 giorni.
- B: L'ultima proposta che ti faccio, poi decidi tu.
- C: Mai comprato da noi? Questo è il momento migliore.

### Corpo email

Ciao [NOME]

Sono Lorenzo di nuovo. Una settimana fa ti ho chiesto se volessi continuare a ricevere le nostre email. Non ho ricevuto segnali, e va bene.

Prima di chiudere questo ciclo, però, voglio farti una proposta concreta.

In tutti questi mesi ti abbiamo mandato contenuti su salute e integrazione, ma non hai mai provato i nostri prodotti. Ci può stare: magari non era il momento, magari avevi dubbi, magari il prezzo ti sembrava alto per un prodotto che non conosci.

Se il freno era il prezzo, questo è il momento di provarci: ti lascio un codice personale del **20% di sconto** sul tuo primo ordine, su qualsiasi prodotto del catalogo.

**Codice personale: {{ unique_coupon_code_sunset }}**
**Validità**: 14 giorni. Scade a mezzanotte del 14° giorno, e non torna.

**[Scegli il tuo primo prodotto](https://paleocomplex.com/negozio/)**

Se non sai da dove partire, la nostra **[guida alla scelta](https://paleocomplex.com/guida-scelta/)** ti orienta in base a età e obiettivi.

E se invece il tema non ti interessa più, nessun problema: te lo dico nella prossima email, l'ultima, come uscire in un click.

Un forte abbraccio
Lorenzo Zarone
Fondatore di Paleocomplex

---

## EMAIL 3 — Flaminia (+7gg dopo Email 2, ultima)

**Mittente:** Flaminia (Customer Care)
**Tipo:** Statica con reminder codice + link disiscrizione esplicito

### Oggetto (3 varianti A/B)

- A: L'ultima email che ricevi da noi (decidi tu)
- B: Il tuo codice del 20% sta per scadere
- C: Restare o uscire: un click e scegli

### Preview text (3 varianti)

- A: Nessun rancore, qualunque cosa scegli.
- B: Il tuo 20% scade tra una settimana.
- C: Dopo questa email, silenzio. A meno che tu non scelga di restare.

### Corpo email

Ciao [NOME]

Sono Flaminia, mi occupo dei clienti di Paleocomplex. Chiudo io questo ciclo di email.

Le cose stanno così: Lorenzo ti ha scritto due volte nelle ultime settimane. Se non c'è stato nessun segnale da parte tua, dopo questa email il nostro sistema smetterà di scriverti. Niente più newsletter, niente più aggiornamenti.

Prima di salutarci, due cose veloci.

**La prima**: il tuo codice personale del **20%** ({{ unique_coupon_code_sunset }}) scade tra 7 giorni, a mezzanotte. Se hai anche solo una curiosità da provare, queste sono le condizioni migliori che vedrai mai.

**[Vai al negozio](https://paleocomplex.com/negozio/)**

**La seconda**: se invece preferisci semplicemente non ricevere più le nostre email, puoi **[disiscriverti qui](https://paleocomplex.com)** in un click, senza rancore. Oppure non fare niente: ci penserà il nostro sistema, con la stessa gentilezza.

Se un giorno vorrai tornare, ti basterà iscriverti di nuovo dal sito.

Grazie del tempo che ci hai dedicato.

Flaminia
Customer Care Paleocomplex

---

## AZIONE AUTOMATICA — Suppress + Tag (solo zero-engagement)

**Timing:** +3 giorni dopo Email 3

**Conditional split PRIMA dell'azione:**
```
Opened email at least once since starting this flow
OR Clicked email at least once since starting this flow?
  ├── SÌ (segnale di interesse) → EXIT senza suppression. Il profilo resta in lista normale.
  └── NO (zero engagement su 3 email) →
        1. Update Profile: tag "Unengaged - Sunset Lead [DATA]"
        2. Suppress Profile da email marketing
```

**Nota**: la suppression NON cancella il profilo. Se un giorno si iscrive di nuovo o compra, viene automaticamente riabilitato.

## Note operative

### Sconto 20% univoco — perché adesso sì (v2.0)

Decisione Andrea 2026-07-14. Il ragionamento è cambiato rispetto alla v1: questo lead ha già ignorato BENVENUTO e PRIMOPASSO durante il nurturing, vero — ma sta USCENDO dalla lista. La baseline di conversione è ~zero, quindi qualunque ordine generato dal 20% è guadagno puro, e il margine lo consente. In più il click sul codice è il miglior test di interesse residuo: alimenta la logica engagement che decide chi sopprimere.

**Setup codice**: coupon master `SUNSET20` in WooCommerce (20%, usage limit 1+1), collegato a Klaviyo Coupons con prefix `SL20-`. Klaviyo genera il codice univoco per profilo con validità 14gg. Stessa procedura documentata nel Flow 73.

### Mittenti: Lorenzo apre e propone, Flaminia chiude

Su un tema "delicato" come "ti sto togliendo dalla lista", la voce del fondatore è più credibile e onesta (Email 1 e 2, inclusa la proposta del 20%). La chiusura operativa (reminder codice + disiscrizione esplicita) passa a Flaminia: è customer care puro, e il cambio di voce segnala al lettore che il ciclo si sta davvero chiudendo.

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
Email 1 Lorenzo (mi senti ancora? — no sconto)
    │
    ▼ wait 7 days
[Filter: Placed Order zero times since starting flow]
    ▼
Email 2 Lorenzo (ultima occasione + 20% univoco SL20-xxx)
    │
    ▼ wait 7 days
[Filter: Placed Order zero times since starting flow]
    ▼
Email 3 Flaminia (reminder codice + resta/disiscriviti)
    │
    ▼ wait 3 days
[Conditional split: Opened OR Clicked at least once in this flow?]
    ├── SÌ → EXIT (resta in lista)
    └── NO → Tag "Unengaged" + Suppress
```

### Status
Bozza v1.0 — pronto per montaggio Klaviyo. Da attivare con calma monitorando l'impatto.

### Changelog
- **v2.0 (2026-07-14)**: lo sconto entra nel Sunset Lead (decisione Andrea). Struttura da 2 a 3 email: E1 conferma interesse (invariata), E2 Lorenzo con **20% univoco** ("se il freno era il prezzo"), E3 Flaminia con reminder codice + scelta esplicita resta/disiscriviti. Suppression SOLO per chi ha zero aperture e zero click su tutte e 3 le email (il click sul codice è il test di interesse). Codice univoco Klaviyo con prefix SL20-, master WooCommerce SUNSET20.
- **v1.1 (2026-06-18)**: fix da verifica content-verifier. Anglicismi rimossi (topic, "È OK"), grammatica preview ("Ci sei un motivo"), gender-neutral (oggetto "Ancora interessato?", "sei iscritto", "Se resti interessato"), preview "Nessuna manipolazione" sostituito con formulazione positiva.
- v1.0 (2026-06-18): prima stesura. Segmento comportamentale (iscritti mai-clienti + 180gg + no engagement 90gg). 2 email Lorenzo + suppress automatico. Nessuno sconto (lead che non ha convertito in 180gg non è recuperabile con sconto).
