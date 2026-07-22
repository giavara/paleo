**Versione:** 1.4
**Ultimo aggiornamento:** 2026-07-17
**Status:** ✅ **LIVE** — flow Klaviyo `SuFKGT` attivo dal 2026-07-17

# Flow 7: Welcome Lead Magnet D3+K2

## Chi entra in questo flow

Contatti che scaricano il lead magnet **"D3 + K2: Smontiamo il Mito delle Assunzioni Separate"** (report PDF, 16 pagine) tramite le campagne social.

**Fonte prevista:** landing page sponsorizzata sui social (Meta) con form di download del report. Traffico prevalentemente freddo, non conosce ancora il brand. Livello di consapevolezza: medio. Sono persone che si informano, hanno un dubbio specifico ("D3 e K2 vanno prese separate o insieme?") e cercano una risposta basata su dati. Target ampio per età, taglio scientifico e razionale.

**Leva psicologica (da target-personas.md):** questo lead magnet colpisce in pieno la **paura #5 del target — "e se stessi facendo tutto nel modo sbagliato?"** (bombardato da consigli contraddittori) e la **soluzione fallita #3** ("uno dice che la vitamina D è tossica, l'altro che dovrei prenderne il triplo"). Il gancio emotivo delle email è la fine di quella confusione. La leva secondaria è la **soluzione fallita #1** (troppi prodotti separati, "ricordarmi troppe cose, questo lontano dai pasti"): la promessa di semplificazione, un solo gesto al posto di dieci pillole e mille allarmi.

**Cosa ricevono:**
- Il report gratuito **"D3 + K2: Smontiamo il Mito delle Assunzioni Separate"**
- Lo sconto di **10 euro sul primo acquisto** (codice BENVENUTO)
- 2 email in 2 giorni, poi passaggio all'Authority Flow

**Tema dominante del report:** sinergia D3 + K2, i cofattori della vitamina D, l'errore di distanziare le vitamine liposolubili. I prodotti citati devono essere coerenti: i multivitaminici che contengono D3 + K2 MK-7 + cofattori nella stessa formula (Paleocomplex, Revolution, Elisir). NON spingere la Vitamina D in gocce da sola, che è D3 senza K2: contraddirebbe il messaggio del report.

## Configurazione Klaviyo (MONTATO — stato reale)

| Cosa | Valore |
|------|--------|
| **Flow ID** | `SuFKGT` — status **live** (attivato da Andrea il 2026-07-17) |
| **Nome** | `07-welcome-d3-k2` |
| **Trigger** | Segmento `UadnPz` = "lm vitamina d3+k2 social" (membro lista `VQBSLm` + `InstagramKeyword` contiene `reportd`) |
| **Filtro di uscita** | `Placed Order` (`Yx2zYn`) count = 0, timeframe `flow-start` |
| **Reentry** | `{duration: 0, unit: alltime}` — una volta sola per profilo |
| **Email 1** | action `112093206`, template `TE6AAK`, immediata |
| **Email 2** | action `112093210`, template `XeWmBH`, dopo delay 2 giorni (tz profilo) |
| **Mittente** | Lorenzo Zarone `<info@paleocomplex.com>` (entrambe) |
| **Smart Sending** | OFF su entrambe (vedi nota) |

Template sciolti creati come intermedi (Klaviyo poi li clona nel flow, quindi sono ridondanti): `VREKQc`, `RDMWcB`. Eliminabili.

**Uscita dal flow:**
- Se il contatto acquista durante il flow → il filtro `flow-start` lo fa uscire subito, non riceve l'email 2. Entra nel **Post Purchase** (flow 21 Primo Cliente / 22 Ricorrente + eventuale flow prodotto)
- Se completa il flow senza acquistare → entra nell'**Authority Flow (flow 4)**

**Due scelte prese in fase di montaggio (deviano dalla spec v1.0):**
1. **Filtro a livello di flow invece del conditional-split.** La spec prevedeva uno split prima dell'email 2. Ho usato il `profile_filter` di flow (`Placed Order = 0 since flow-start`), che è il pattern già usato da `01 carrello abbandonato`, `04-authority` e `06-conversione`. Klaviyo lo valuta a ogni step: stesso risultato, meno nodi, coerente con gli altri flow.
2. **Smart Sending OFF** (la spec diceva ON). Su un'email di delivery lo Smart Sending può **sopprimere la consegna del report** se il contatto ha ricevuto un'altra email di recente: promessa tradita. Il `02-welcome-kit-benessere` ha Smart Sending OFF su tutte le email, stessa logica.

**Handoff Authority (da configurare):** l'Authority (flow 4) oggi parte dal completamento di Welcome Kit Benessere o Welcome Unghie/Capelli. Aggiungere **questo flow come terza sorgente di trigger** dell'Authority, così i lead D3+K2 non convertiti proseguono nel nurturing lungo. Coerente con la decisione #9 del piano master (welcome specifico → Authority sequenziale, non in parallelo).

**Note tecniche:**
- Codice BENVENUTO: 10 euro fissi, solo primo acquisto, valido su tutti i prodotti
- Il report va consegnato come link diretto al PDF
- Taggare la provenienza (lead magnet D3+K2) come proprietà profilo per analytics
- Smart Sending: ON

---

## EMAIL 1 — Delivery report + benvenuto (immediata)

**Timing:** invio immediato (T+0 dal trigger).

### Oggetto (3 varianti A/B)

- A: Ecco il tuo report su D3 e K2 (e un regalo di benvenuto)
- B: D3 e K2: la risposta chiara che cercavi
- C: Il report che hai richiesto è pronto

### Preview text (3 varianti)

- A: Scarica il report e scopri il tuo sconto di benvenuto.
- B: Basta consigli contraddittori: qui parlano le evidenze cliniche.
- C: Più un regalo di 10 euro sul primo acquisto.

### Corpo email

Ciao [NOME]

Da oggi fai parte del mondo Paleocomplex.

Ecco il report che hai richiesto: **"D3 + K2: Smontiamo il Mito delle Assunzioni Separate."**

**[CTA: Scarica il tuo report gratuito]**
(link al PDF)

Se hai cercato informazioni sulla vitamina D, sai già quanto è facile perdersi. Un sito dice una cosa, un altro l'esatto contrario. Chi ti dice di distanziare D3 e K2 di ore, chi di prenderle insieme. E alla fine il dubbio resta: sto facendo la cosa giusta, o sto sbagliando senza saperlo?

Questo report mette ordine. È un'indagine basata su biologia cellulare, falsi miti del web ed evidenze cliniche umane. In sintesi: la regola di assumerle a distanza di ore è una forzatura nata online, non supportata dalla ricerca. D3 e K2 non competono e non c'è motivo di distanziarle: agiscono su recettori diversi. E i grandi trial clinici sull'uomo che le combinano mostrano un beneficio maggiore, non minore.

Come regalo di benvenuto ho anche un codice sconto di **10 euro sul tuo primo acquisto**: **BENVENUTO** (ti basta inserirlo nel campo "Codice coupon" durante l'acquisto).

È valido su tutti i prodotti dello store, senza limiti di spesa.

**[CTA: Vai allo store e usa il tuo sconto](https://paleocomplex.com)**

Tra un paio di giorni ti spiego una cosa che quasi nessun brand di integratori dice ad alta voce: perché la vitamina D presa da sola, senza i suoi cofattori, è quasi sempre uno spreco. E come smettere di complicarti la vita per sempre.

Un forte abbraccio
Lorenzo Zarone
Fondatore di Paleocomplex

---

## EMAIL 2 — Cosa significa il report per la tua integrazione (+2 giorni)

**Timing:** T+2 giorni dal trigger (delay incrementale: +2 giorni dall'email 1).

### Condizione

Gestita dal **filtro di flow** (`Placed Order = 0 since flow-start`), non da uno split: chi acquista esce dal flow e non riceve questa email.

### Oggetto (3 varianti A/B)

- A: Perché la vitamina D da sola è quasi sempre uno spreco
- B: Stanco di consigli contraddittori sulla vitamina D?
- C: D3 e K2: la fine delle mille regole

### Preview text (3 varianti)

- A: La D senza i suoi cofattori non può funzionare come dovrebbe.
- B: Un solo gesto al posto di dieci pillole e mille allarmi.
- C: Il tuo sconto di benvenuto è ancora attivo.

### Corpo email

Ciao [NOME]

Eccomi con quello che ti avevo promesso.

Quante volte hai letto un esperto dire una cosa e il giorno dopo un altro l'opposto? Sulla vitamina D succede a tutti. Chi la chiama tossica, chi dice di triplicare la dose, chi ti impone di distanziare D3 e K2 di ore, con la sveglia del telefono per non sbagliare.

Il report che hai scaricato chiude il discorso. D3 e K2 non competono, lavorano in coppia. La D3 promuove l'assorbimento del calcio e stimola le proteine giuste (osteocalcina e MGP). La K2 le attiva e dirige quel calcio dove serve: dentro le ossa, fuori dalle arterie. Senza K2, il lavoro della D resta a metà.

Ma c'è un passaggio in più che il web dimentica quasi sempre.

La vitamina D non ha bisogno solo della K2. Ha bisogno anche di magnesio, che la attiva, e poi di boro, zinco e vitamina A. Presa da sola e senza questi cofattori, la vitamina D rende molto meno di quello che potrebbe. E alle dosi più alte rischia persino di dirigere il calcio dove non serve.

Per questo io la penso da sempre allo stesso modo: non separare ciò che la natura ha messo insieme.

Ed è il criterio con cui sono formulati i nostri multivitaminici. Non trovi la D3 da una parte e la K2 dall'altra. Le trovi nella stessa formula, insieme a magnesio, boro, zinco e vitamina A. Tutto quello che serve alla vitamina D per lavorare come deve, già dosato nel modo giusto. Un solo gesto al giorno, preferibilmente durante un pasto, perché D3 e K2 sono entrambe liposolubili. Niente più allarmi sul telefono, niente più dieci prodotti separati da incastrare.

È esattamente il punto del report: la scienza premia la sinergia, non la separazione.

Se vuoi capire quale dei nostri multivitaminici è più adatto a te, abbiamo una guida che ti orienta in due minuti.

**[CTA: Vai alla guida alla scelta](https://paleocomplex.com/guida-scelta/)**

E ricorda che hai ancora il tuo sconto di benvenuto: **codice BENVENUTO**, 10 euro sul primo acquisto, valido su tutti i prodotti. Non resterà attivo per sempre.

**[CTA: Usa il codice BENVENUTO](https://paleocomplex.com)**

Un forte abbraccio
Lorenzo Zarone
Fondatore di Paleocomplex

---

## Schema del flow

```
[Optin da landing social — download report D3+K2]
    │
    ▼
EMAIL 1 (immediata, T+0) — Delivery report + BENVENUTO 10 euro
    │
    ├── Se acquista → esce → Post Purchase (flow 21/22 + prodotto)
    │
    ▼  (T+2 giorni · +2gg dall'email 1)
SPLIT: Ha acquistato dall'inizio del flow?
    ├── SI → Fine (è nel Post Purchase)
    │
    └── NO ↓
         EMAIL 2 — Il report applicato: D3+K2+cofattori nella stessa formula + reminder BENVENUTO
              │
              ▼
         Fine welcome → Entra in Authority Flow (flow 4)
```

**Timeline totale dal primo contatto:**
- Welcome D3+K2: 2 giorni
- Authority: 14 giorni (a seguire, per chi non compra)

---

## Note

### Angolo persona (revisione v1.1)
Le due email sono state riscritte partendo da `context/target-personas.md`. Il gancio non è più solo scientifico ma emotivo:
- **Email 1** apre sulla paura #5 ("sto sbagliando senza saperlo") e sul caos di consigli contraddittori. Il report è la risposta chiara che chiude il dubbio.
- **Email 2** apre sulla soluzione fallita #3 (esperti che dicono tutto e il contrario), risolve con la scienza, poi chiude sulla soluzione fallita #1 (troppi prodotti separati, allarmi sul telefono) con la promessa di semplificazione: un solo gesto. Coerente con i messaggi chiave brand ("stop alle mille pillole, inizia a semplificare").

### Perché solo 2 email (scelta deliberata)
Flow di delivery volutamente snello. La delivery + sconto immediato (email 1) è il momento a più alta conversione (dato Kit Benessere: email 1 = il singolo invio più redditizio del sistema). L'email 2 fa da ponte report→prodotto per chi non ha ancora comprato e chiude con l'urgency. Il nurturing lungo NON vive qui: vive nell'Authority Flow, in cui questo welcome confluisce. Così non si duplica contenuto e il volume per contatto resta basso.

Se in test la conversione fosse debole, la leva più ovvia è una terza email di sola urgency ("il tuo sconto sta per scadere") a T+4/5, prima del passaggio all'Authority. Da valutare sui dati, non a priori.

### Logica prodotto
Il report conclude che D3 e K2 vanno assunte insieme. Il gancio naturale sono i multivitaminici che già contengono **D3 + K2 MK-7 + magnesio + boro + zinco + vitamina A nella stessa formula** (Paleocomplex, Revolution, Elisir). Verificato su schede prodotto (sinergia "asse osseo-cardiovascolare", identica nei tre multivitaminici).

**Da NON spingere:** la Vitamina D in gocce da sola (è D3 senza K2). Spingerla contraddirebbe il messaggio del report. Semmai è un add-on per chi ha già un multivitaminico con K2 e vuole alzare la D, ma non è l'offerta di questo flow.

### Codice sconto
Default: **BENVENUTO** (10 euro, primo acquisto, tutti i prodotti), coerente con il sistema welcome esistente. In alternativa, per tracciare separatamente le conversioni di QUESTO funnel, Andrea può creare un codice dedicato su WooCommerce (es. D3K2) con le stesse regole e sostituirlo in entrambe le email.

### Claims prudenti
Il meccanismo D3/K2 (K2 attiva osteocalcina e MGP, dirige il calcio nelle ossa e fuori dalle arterie; la D senza K2 rischia la calcificazione) è presentato come contenuto del report e coerente con schede prodotto e Authority flow email 3. Mantenuto il "rischia di" per il claim sul calcio. Nessun claim medico sui prodotti.

### Link/asset da verificare prima della pubblicazione
- Link diretto al PDF del report → `https://paleocomplex.com/wp-content/uploads/2026/07/Report-d3-k2-assunzioni-separate_PALEOCOMPLEX.pdf` (attivo)
- `https://paleocomplex.com/guida-scelta/` → pagina online
- Codice BENVENUTO (o codice dedicato) attivo e configurato su WooCommerce
- Lista/form Klaviyo di ingresso creata e collegata alla landing social
- Authority Flow (flow 4): aggiungere questo welcome come sorgente di trigger

### Changelog
- **v1.4 (2026-07-17)**: flow **attivato da Andrea** (`SuFKGT` status `live`). Il flow vuoto `ShSeZw` è stato cancellato. Restano aperti: trigger Authority, etichetta campo coupon, fallback nome nel template R4zvd6 (vedi `tasks.md`).
- **v1.3 (2026-07-17)**: **montato su Klaviyo**. Creati 2 template HTML dal design `R4zvd6` (riusata la logica della skill `montaggio-email-klaviyo`, fermandosi prima della parte campagna) e creato il flow `SuFKGT` via `POST /api/flows` con definition completa (trigger segmento `UadnPz` + email 1 + delay 2gg + email 2). Il flow vuoto `ShSeZw` creato da Andrea è da archiviare: l'API Klaviyo non permette di aggiungere azioni a un flow esistente, solo di crearne uno nuovo con la definition completa. Deviazioni dalla spec documentate sopra (filtro di flow invece di split; Smart Sending OFF).
- **v1.2 (2026-07-14)**: applicati fix da content-verifier (skill, 3 dimensioni, 0 errori critici). Email 1: riformulato il claim sui trial distinguendo "non competono / recettori diversi" da "beneficio maggiore sull'osso" (evitato l'overstatement "insieme vengono assorbite" sul timing). Email 2: tolto "in gocce ad alto dosaggio" (impreciso: le gocce Paleo sono 2.000 UI standard) e ancorato il rischio calcio a "alle dosi più alte". Mantenuto "spreco" in Email 1 (scelta Andrea: voce Lorenzo, coerente con report + Authority). Aperti: campo checkout "Codice coupon" vs "Codice Promozionale" (incoerenza promo-rules vs welcome-kit, da allineare sul sito live su tutti i flow); fallback token first_name Klaviyo.
- **v1.1 (2026-07-14)**: revisione persona-driven (letto `target-personas.md` + `brand-database.md`). Riscritti gli attacchi di entrambe le email sugli angoli emotivi del target (paura "sto sbagliando", consigli contraddittori, semplificazione "un solo gesto"). Corretti tutti gli accenti da forma-apostrofo ad accenti reali nei corpi email (regola accenti-reali). Nuovi oggetti/preview coerenti con l'angolo.
- **v1.0 (2026-07-13)**: prima stesura. Welcome 2 email da lead magnet D3+K2 (delivery + benvenuto → bridge report/prodotto + urgency), split acquisto prima dell'email 2, handoff ad Authority per i non convertiti.
