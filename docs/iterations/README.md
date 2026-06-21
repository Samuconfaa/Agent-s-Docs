# Iterazione XX — [Titolo sintetico della feature]

<!-- Il titolo deve essere la descrizione in 3-5 parole della funzionalità implementata.
     Esempi corretti: "Integrazione API ricerca", "Persistenza preferiti locale", "Gestione errori UI"
     Esempi errati: "Feature nuova", "Modifiche varie", "Iterazione 5" -->

---

## Metadati

| Campo | Valore |
|-------|--------|
| **Numero iterazione** | XX |
| **Branch** | `iter/XX-[nome-feature]` |
| **Data inizio** | [GG/MM/AAAA] |
| **Data completamento** | [GG/MM/AAAA] |
| **Dipende da** | Iterazione [YY] — [titolo] (o "Nessuna") |
| **Stato** | In corso / Completata / Parziale / Sospesa |

---

## Obiettivo

<!-- Una sola frase che descrive il risultato atteso in modo verificabile.
     Un obiettivo è verificabile se si può rispondere con "sì" o "no" alla domanda
     "questo obiettivo è stato raggiunto?".
     
     Corretto: "L'utente può cercare contenuti tramite la barra di ricerca e
                visualizzare i risultati in una lista scrollabile."
     Errato: "Implementare la ricerca." -->

[Descrizione precisa e verificabile del risultato atteso da questa iterazione]

---

## Piano

### File da creare

<!-- Elencare ogni file con il percorso relativo alla root del progetto.
     Se il file non è ancora definito, indicarlo con [DA DEFINIRE]. -->

- `src/[Componente]/[File].[ext]` — [descrizione dello scopo]
- `src/[Componente]/[File].[ext]` — [descrizione dello scopo]

### File da modificare

- `src/[Percorso]/[File].[ext]` — [descrizione della modifica prevista]
- `src/[Percorso]/[File].[ext]` — [descrizione della modifica prevista]

### Dipendenze tecniche

<!-- Elencare ogni componente già esistente da cui questa iterazione dipende.
     Una dipendenza non dichiarata è un rischio nascosto. -->

- [Componente o service già implementato su cui si basa questa iterazione]
- [Eventuale API o libreria esterna usata per la prima volta]

### Rischi specifici di questa iterazione

<!-- Rischi diversi da quelli generali già in plan.md.
     Indicare solo i rischi concreti e pertinenti a questo specifico lavoro. -->

- [Rischio 1: cosa potrebbe andare storto e perché]
- [Rischio 2: ...]

---

## Prompt principali utilizzati

<!-- Tracciare i prompt significativi inviati all'AI durante questa iterazione.
     Questo log è utile per comprendere le decisioni prese e riprodurre il lavoro.
     Non serve copiare il testo integrale: un riassunto di 1-2 righe è sufficiente.
     Includere i prompt di correzione e follow-up, non solo quelli iniziali. -->

1. "[Descrivere la richiesta principale fatta all'AI]"
2. "[Descrivere eventuali richieste di correzione o chiarimento]"
3. "[Descrivere altri prompt significativi]"

---

## Implementazione

### File creati

<!-- Elencare i file effettivamente creati durante questa iterazione.
     Confrontare con il piano: se ci sono differenze, documentarle. -->

- `src/[Percorso]/[File].[ext]` — [creato come da piano / aggiunto per necessità X]

### File modificati

<!-- Per ogni file modificato, indicare brevemente cosa è cambiato
     e perché, se non ovvio. -->

- `src/[Percorso]/[File].[ext]` — [tipo di modifica: aggiunto metodo X / modificato comportamento Y]

### File eliminati

<!-- Se è stato eliminato del codice esistente, documentarlo con la motivazione. -->

- `src/[Percorso]/[File].[ext]` — [motivazione dell'eliminazione]

### Dipendenze aggiunte

<!-- Se questa iterazione ha introdotto nuove dipendenze esterne, documentarle.
     Se non sono state aggiunte, lasciare "Nessuna". -->

- [Nome dipendenza] v[X.Y.Z] — [motivazione] — (già approvata in plan.md / aggiunta per necessità X)

---

## Revisione del codice generato

### Codice accettato senza modifiche

<!-- Indicare le parti generate dall'AI e accettate così come prodotte.
     Essere specifici: non "tutto il ViewModel" ma "il metodo LoadDataAsync e le proprietà
     IsBusy, HasData, ErrorMessage". -->

- [Componente o metodo specifico] — accettato perché [corretto / ben strutturato / nessuna modifica necessaria]

### Codice modificato manualmente

<!-- Indicare cosa è stato cambiato rispetto all'output dell'AI e perché.
     Questo è il punto più critico del log: rivela dove l'AI ha sbagliato
     o dove il contesto non era sufficiente. -->

- [Componente o metodo] — modificato perché [il codice generato faceva X invece di Y /
  non rispettava il pattern adottato / la logica era scorretta in caso Z]

### Codice scritto interamente manualmente

<!-- Indicare le parti non generate dall'AI, con la motivazione. -->

- [Componente o logica] — scritto manualmente perché [troppo specifico / l'AI non aveva
  contesto sufficiente / il risultato generato era inutilizzabile]

---

## Test eseguiti

<!-- Copiare gli ID dei test da docs/test-matrix.md per questa funzionalità.
     Se mancano, aggiungerli prima alla matrice e poi riportarli qui.
     Usare tre stati: ✅ superato / ❌ fallito / ⏭ saltato (con motivazione)
     Non marcare un test come superato senza averlo effettivamente eseguito.
     Aggiornare l'esito anche in docs/test-matrix.md al termine. -->

### Funzionalità principali

- [ ] **[TC-FX-01]** [Descrizione del test] → [esito e note]
- [ ] **[TC-FX-02]** [Descrizione del test] → [esito e note]
- [ ] **[TC-FX-03]** [Descrizione del test] → [esito e note]

### Casi limite

- [ ] **[TC-CL-01]** Input vuoto / null → [comportamento osservato]
- [ ] **[TC-CL-02]** Nessuna connessione di rete → [comportamento osservato]
- [ ] **[TC-CL-03]** Risposta API con errore → [comportamento osservato]
- [ ] **[TC-CL-04]** Risposta API con lista vuota → [comportamento osservato]
- [ ] **[TC-CL-05]** [Caso limite specifico di questa iterazione] → [esito]

### Regressioni verificate

<!-- Eseguire tutti i TC-REG-* presenti in docs/test-matrix.md e aggiornarne l'esito. -->

- [ ] [Funzionalità esistente 1] — funziona ancora correttamente
- [ ] [Funzionalità esistente 2] — funziona ancora correttamente

---

## Problemi riscontrati

<!-- Documentare ogni problema incontrato, anche quelli risolti durante l'iterazione.
     Questa sezione è memoria storica: non omettere i problemi "minori". -->

### [Problema 1 — Titolo sintetico]

- **Descrizione**: [cosa è successo esattamente]
- **Causa**: [perché è successo]
- **Impatto**: [quanto ha bloccato il lavoro]
- **Stato**: [Risolto in questa iterazione / Rimandato a iterazione XX / Accettato]

### [Problema 2 — Titolo sintetico]

- **Descrizione**: [...]
- **Causa**: [...]
- **Impatto**: [...]
- **Stato**: [...]

---

## Correzioni effettuate

<!-- Per ogni correzione significativa descrivere cosa è stato cambiato e perché.
     Non limitarsi a "fixato bug": spiegare la causa e la soluzione. -->

### [Correzione 1 — Titolo sintetico]

- **Problema**: [descrizione del problema originale]
- **Soluzione**: [cosa è stato modificato nel codice]
- **Verifica**: [come è stato confermato che la correzione funziona]

---

## Decisioni prese durante l'iterazione

<!-- Documentare le scelte non ovvie fatte durante l'implementazione.
     Le decisioni non documentate si dimenticano e vengono riprese da capo in futuro. -->

| Decisione | Alternativa considerata | Motivazione della scelta |
|-----------|------------------------|--------------------------|
| [es. Usare cache in memoria invece di persistenza] | [Cache su disco] | [Semplicità, dati non critici] |
| [...] | [...] | [...] |

---

## Commit creati

<!-- Elencare i commit significativi con hash abbreviato e messaggio.
     Questo facilita il debugging e la revisione storica. -->

| Hash | Messaggio del commit |
|------|---------------------|
| `[abc1234]` | `feat: [descrizione feature principale]` |
| `[def5678]` | `fix: [descrizione correzione]` |
| `[ghi9012]` | `docs: aggiornata documentazione iterazione XX` |

---

## Definition of Done — checklist

<!-- Questa checklist deve essere completata prima di chiudere l'iterazione.
     Nessun punto può essere saltato senza motivazione esplicita. -->

- [ ] Il codice compila senza errori
- [ ] Il codice compila senza warning non giustificati
- [ ] La funzionalità è testata su dispositivo fisico o emulatore
- [ ] Tutti i test elencati nella sezione "Test eseguiti" hanno esito positivo
- [ ] I tre stati UI (loading / errore / empty) sono gestiti dove applicabile
- [ ] Nessuna credenziale o dato sensibile è presente nel codice committato
- [ ] Il codice è stato letto e compreso dopo la scrittura (non solo generato)
- [ ] Le funzionalità delle iterazioni precedenti non sono state rotte
- [ ] Il branch è stato unito a `main` con commit semantico corretto
- [ ] Questo file `it-XX.md` è completo e aggiornato

---

## Esito

<!-- Scegliere uno tra: Completato / Parziale / Sospesa
     Se parziale o sospesa, indicare esattamente cosa manca e dove è tracciato. -->

**[Completato / Parziale / Sospesa]**

Se parziale o sospesa:

- **Cosa manca**: [descrizione precisa]
- **Dove è tracciato**: [Iterazione XX / Issue #N / TODO in file X:riga Y]
- **Motivazione**: [perché non è stato completato in questa iterazione]
