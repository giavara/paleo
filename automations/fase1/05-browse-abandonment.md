**Versione:** 1.0
**Ultimo aggiornamento:** 2026-04-08
**Status:** Bozza v1 — in attesa review Andrea

# Flow 5: Browse Abandonment

## Chi entra in questo flow

Persone che hanno **visitato una pagina prodotto** sul sito ma NON hanno aggiunto al carrello, NON hanno iniziato il checkout e NON hanno acquistato.

**Chi sono in pratica:**
- Visitatori con cookie Klaviyo che esplorano per la prima volta (da ads, blog, SEO)
- Contatti in lista che hanno finito i flow automatici (welcome + authority) e tornano a curiosare
- Clienti esistenti che esplorano un prodotto che non hanno ancora comprato

**Chi NON entra (filtri di esclusione):**
- Chi è attualmente in un altro flow attivo (Welcome, Authority, Carrello Abbandonato)
- Chi ha già comprato quel prodotto specifico
- Chi è già stato in questo flow negli ultimi 30 giorni
- Chi ha aggiunto al carrello o iniziato il checkout (va nel Carrello Abbandonato)

**Logica di incastro con gli altri flow:**
Il Browse Abandonment è il touchpoint più leggero di tutto il sistema. Non deve mai sovrapporsi ai flow educativi o di vendita. Parte solo quando il contatto non è in nessun altro percorso automatico. In pratica serve per riattivare l'interesse di chi ha finito tutti i flow e torna a esplorare senza agire.

## Configurazione Klaviyo

**Trigger:** Viewed Product
**Mittente:** Team Paleocomplex (tutte le email)
**Filtri profilo:**
- Placed Order zero times since starting this flow (per quel prodotto specifico)
- Started Checkout zero times since starting this flow
- Added to Cart zero times since starting this flow
- **Has Placed Order where Item = viewed product zero times over all time** (non ha già comprato quel prodotto)
- **Has not been in this flow in the last 30 days** (filtro frequenza)
- **Non è attualmente in:** Welcome Kit Benessere (flow 2), Welcome Unghie/Capelli (flow 3), Authority Flow (flow 4), Carrello Abbandonato (flow 1)

**Note tecniche:**
- Usare proprietà dell'evento per mostrare il prodotto visualizzato: {{ event.Name }}, {{ event.Price }}, {{ event.URL }}, {{ event.ImageURL }}
- Nessuno sconto
- Email cortissime, tono leggero
- Email 2 in draft: attivare solo dopo aver valutato le performance della email 1

---

## EMAIL 1 — Touchpoint leggero (+2 ore)

### Oggetto (3 varianti A/B)

- A: Stavi guardando qualcosa?
- B: {{ event.Name }}: ecco cosa devi sapere
- C: Hai dato un'occhiata ai nostri prodotti

### Preview text (3 varianti)

- A: Il prodotto che hai visto è ancora disponibile.
- B: Un dettaglio che forse ti è sfuggito.
- C: Ecco un motivo in più per darci un'occhiata.

### Corpo email

Ciao [NOME]

Abbiamo notato che hai visitato la pagina di **{{ event.Name }}**.

**[BLOCCO PRODOTTO DINAMICO: immagine, nome, prezzo, link]**

Ogni nostro prodotto è formulato con dosaggi reali e ingredienti in forme biodisponibili. Se vuoi capire perché {{ event.Name }} è diverso da quello che trovi in farmacia o al supermercato, dai un'occhiata all'etichetta completa sulla pagina prodotto.

**[CTA: Scopri {{ event.Name }}]({{ event.URL }})**

Se non sai quale prodotto è il più adatto a te, abbiamo una guida rapida che ti aiuta a orientarti.

**[CTA: Vai alla guida alla scelta](https://paleocomplex.com/guida-scelta)**

Team Paleocomplex

---

## EMAIL 2 — Social proof specifico (+1 giorno) [IN DRAFT — attivare dopo valutazione performance email 1]

### Oggetto (3 varianti A/B)

- A: Cosa dicono chi usa {{ event.Name }}
- B: {{ event.Name }}: le esperienze di chi lo usa
- C: Hai ancora dubbi su {{ event.Name }}?

### Preview text (3 varianti)

- A: Le recensioni di chi ha fatto la tua stessa scelta.
- B: Esperienze reali da clienti verificati.
- C: A volte basta leggere chi ci è già passato.

### Corpo email

Ciao [NOME]

Ieri hai dato un'occhiata a **{{ event.Name }}** e magari stai ancora valutando.

Ecco cosa dicono alcune persone che lo usano:

**[BLOCCO RECENSIONI DINAMICO: 2-3 recensioni filtrate per prodotto visualizzato]**

Se hai domande, scrivici a **info@paleocomplex.com**. Ti rispondiamo personalmente.

**[CTA: Scopri {{ event.Name }}]({{ event.URL }})**

Team Paleocomplex

---

## Schema del flow

```
[Viewed Product + nessun altro flow attivo + non ha comprato quel prodotto + non in flow da 30gg]
    │
    ▼  (+2 ore)
EMAIL 1 — "Stavi guardando [prodotto]" + beneficio chiave + CTA
    │
    ├── Se acquista → esce
    ├── Se aggiunge al carrello → esce (entra nel Carrello Abbandonato)
    │
    ▼  (+1 giorno) [IN DRAFT]
EMAIL 2 — Social proof specifico per prodotto
    │
    ▼
Fine flow
```

---

## Note

### Perché il filtro 30 giorni
Se un contatto naviga 5 prodotti diversi in una settimana, senza filtro riceverebbe 5 email di browse abandonment. Con il filtro 30 giorni riceve la prima e poi basta. È il default consigliato da Klaviyo.

### Perché email 2 in draft
Per un touchpoint così leggero (l'utente ha solo guardato, intento basso), 1 email potrebbe bastare. Attiviamo la seconda solo se i dati mostrano che:
- L'email 1 ha un buon open rate (>30%) ma basso click rate (<2%): significa che il messaggio arriva ma non convince → la email 2 con social proof può aiutare
- Se l'email 1 ha già un buon click rate (>3%), la email 2 probabilmente non serve

### Perché NON parte durante altri flow
Se un contatto è nel Welcome e clicca un link → visita una pagina prodotto → NON deve ricevere il browse abandonment. Sta già ricevendo un percorso strutturato. Il browse sarebbe rumore in più. Il filtro "non è attualmente in flow 1, 2, 3, 4" evita questo problema.

### Blocco recensioni dinamico (email 2)
Su Klaviyo si può creare un blocco di recensioni filtrate per prodotto usando i Review Feeds o un custom block con logica condizionale. In alternativa, creare blocchi statici per i 5-6 prodotti principali (Elisir, Revolution, Essentiel, Youth, Jeunesse, Paleocomplex) e mostrare il blocco corretto con Show/Hide basato su {{ event.Name }}.

### Prodotti senza recensioni
Per prodotti con poche/nessuna recensione (Artosan, Liverty, Testoplus, accessori), l'email 2 non ha senso. Valutare se escludere questi prodotti dal flow oppure mostrare un messaggio generico al posto delle recensioni.
