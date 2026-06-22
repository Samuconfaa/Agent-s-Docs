# Piano di lavoro

## Titolo del progetto

[Nome dell'applicazione]

---

## Obiettivo del piano

<!-- Questo documento traduce la specifica (spec.md) in un piano
     di lavoro concreto: iterazioni sequenziali, ciascuna con obiettivo
     verificabile, file coinvolti e criteri di completamento.
     Il piano non è immutabile: va aggiornato se le priorità cambiano,
     ma ogni cambiamento deve essere documentato e motivato. -->

Trasformare le funzionalità descritte in `spec.md` in un insieme di iterazioni
incrementali, ognuna consegnabile e verificabile in modo autonomo.

---

## Architettura prevista

<!-- Sintetizzare le scelte architetturali. Il dettaglio sta in architecture.md.
     Qui indicare solo le scelte che influenzano la struttura delle iterazioni. -->

- **Pattern**: [es. MVVM / Clean Architecture / MVC]
- **Navigazione**: [es. gerarchica / a tab / a menu laterale / mista]
- **Layer principali**: Presentazione → ViewModel/Controller → Servizi → Repository → Dati
- **Persistenza locale**: [es. SQLite / key-value store / file]
- **Comunicazione remota**: [es. HTTP client asincrono / GraphQL / WebSocket]
- **Iniezione dipendenze**: [es. contenitore DI built-in / manuale / framework specifico]

---

## Struttura prevista delle cartelle

<!-- Adattare alla struttura reale del progetto.
     Ogni cartella deve avere uno scopo non ambiguo.
     Non creare cartelle vuote "per il futuro". -->

```
ProjectRoot/
├── .git/
├── .gitignore
├── src/
│   ├── api/          ← backend / API REST o GraphQL
│   ├── web/          ← frontend / sito web
│   ├── mobile/       ← app mobile
│   ├── worker/       ← processi in background, job, queue
│   └── shared/       ← codice condiviso tra più servizi
│       (creare solo le cartelle effettivamente necessarie)
├── docs/
│   ├── spec.md
│   ├── plan.md               ← questo file
│   ├── architecture.md
│   ├── api-notes.md
│   ├── test-matrix.md
│   └── iterations/
│       ├── it-01.md
│       └── ...
└── README.md
```

---

## Dipendenze previste

<!-- Elencare SOLO le dipendenze già decise, con la motivazione.
     Non aggiungere dipendenze "nel caso servano".
     Ogni dipendenza è un impegno di manutenzione a lungo termine. -->

| Dipendenza | Versione | Scopo | Obbligatoria / Opzionale | Motivazione |
|-----------|---------|-------|--------------------------|-------------|
| [nome libreria] | [>=X.Y] | [cosa fa] | Obbligatoria | [perché non si usa un'alternativa built-in] |
| [nome libreria] | [>=X.Y] | [cosa fa] | Opzionale | [quando viene aggiunta e perché] |

### Regole per le dipendenze

- Nessuna dipendenza viene aggiunta senza discussione esplicita e motivazione documentata.
- Preferire sempre ciò che è già disponibile nel linguaggio o nel framework base.
- Valutare: maturità, manutenzione attiva, licenza, dimensione del pacchetto.
- Documentare le dipendenze rimosse con la motivazione.

---

## Strategia di versioning e branch

<!-- Definire la strategia git prima di iniziare il lavoro.
     Una strategia non documentata porta a branch orfani e merge caotici. -->

### Nomenclatura dei branch

- `main` — codice stabile, sempre compilabile e testato
- `dev` — integrazione tra le iterazioni (opzionale se team singolo)
- `iter/XX-nome-feature` — un branch per ogni iterazione
- `fix/nome-bug` — hotfix su problemi critici

### Commit semantici (obbligatori)

| Prefisso | Quando usarlo |
|----------|--------------|
| `feat:` | Nuova funzionalità aggiunta |
| `fix:` | Correzione di un bug |
| `refactor:` | Modifica che non aggiunge funzionalità né corregge bug |
| `docs:` | Aggiornamento documentazione |
| `test:` | Aggiunta o modifica di test |
| `chore:` | Aggiornamento dipendenze, configurazione CI, ecc. |
| `style:` | Formattazione, spaziatura (nessuna logica cambiata) |

### Regola di merge

- Un branch di iterazione viene unito a `main` solo dopo che tutti i criteri
  della Definition of Done sono soddisfatti.
- Nessun merge con conflitti non risolti o test falliti.

---

## Iterazioni previste

<!-- Ogni iterazione deve:
     - avere un obiettivo singolo e verificabile
     - essere completabile in una sessione di lavoro ragionevole
     - produrre un artefatto funzionante (anche se parziale)
     - non dipendere da iterazioni non ancora completate
     
     Non pianificare troppe iterazioni in anticipo: le ultime saranno spesso riviste. -->

### Iterazione 1 — Setup e struttura base

- **Obiettivo**: creare il progetto, configurare la struttura di cartelle, inizializzare git
- **Branch**: `iter/01-setup`
- **File da creare**: [elenco file iniziali]
- **File da modificare**: nessuno (nuovo progetto)
- **Risultato verificabile**: il progetto si compila e si avvia senza errori
- **Dipendenze**: nessuna

### Iterazione 2 — Navigazione e schermata principale

- **Obiettivo**: implementare la struttura di navigazione e la prima schermata funzionante
- **Branch**: `iter/02-navigazione`
- **File da creare**: [elenco]
- **File da modificare**: [elenco]
- **Risultato verificabile**: l'utente può navigare tra le sezioni principali
- **Dipendenze**: Iterazione 1

### Iterazione 3 — Integrazione API e primo dato reale

- **Obiettivo**: implementare il servizio di comunicazione remota e visualizzare dati reali
- **Branch**: `iter/03-api`
- **File da creare**: [elenco]
- **File da modificare**: [elenco]
- **Risultato verificabile**: i dati reali sono visibili nella schermata principale
- **Dipendenze**: Iterazione 2

### Iterazione 4 — Dettaglio e navigazione avanzata

- **Obiettivo**: implementare la schermata di dettaglio con navigazione e passaggio parametri
- **Branch**: `iter/04-dettaglio`
- **File da creare**: [elenco]
- **File da modificare**: [elenco]
- **Risultato verificabile**: cliccando un elemento si apre il dettaglio con dati corretti
- **Dipendenze**: Iterazione 3

### Iterazione 5 — Persistenza locale

- **Obiettivo**: salvare e recuperare dati in locale in modo persistente
- **Branch**: `iter/05-persistenza`
- **File da creare**: [elenco]
- **File da modificare**: [elenco]
- **Risultato verificabile**: i dati salvati sopravvivono alla chiusura dell'app
- **Dipendenze**: Iterazione 4

### Iterazione 6 — Gestione errori, stati UI, rifinitura

- **Obiettivo**: gestire tutti gli stati UI (loading, errore, empty) e rifinire l'esperienza utente
- **Branch**: `iter/06-ux-errors`
- **File da creare**: nessuno previsto
- **File da modificare**: tutti i ViewModel e le View esistenti
- **Risultato verificabile**: l'app non crasha né rimane bloccata in nessuno scenario
  documentato nella spec
- **Dipendenze**: Iterazioni 3, 4, 5

*(Aggiungere iterazioni per le funzionalità opzionali solo dopo il completamento del MVP)*

---

## Rischi tecnici

<!-- Identificare i rischi prima di iniziare, non durante lo sviluppo.
     Aggiornare questa tabella man mano che i rischi si materializzano o si chiudono. -->

| ID  | Rischio | Probabilità | Impatto | Mitigazione | Stato |
|-----|---------|------------|---------|-------------|-------|
| RT1 | API esterna non disponibile per i test | Media | Alto | Preparare dati mock da usare offline | Aperto |
| RT2 | Struttura JSON diversa dalla documentazione | Media | Alto | Validare con client HTTP prima dell'integrazione | Aperto |
| RT3 | Rate limit troppo restrittivo | Alta | Medio | Implementare cache, limitare chiamate durante sviluppo | Aperto |
| RT4 | Scope creep non controllato | Alta | Alto | Bloccare spec prima di iniziare, non aggiungere feature non pianificate | Aperto |
| RT5 | Tempi insufficienti per la rifinitura | Alta | Medio | Definire MVP non negoziabile, iterazione 6 è la safety net | Aperto |
| RT6 | Dipendenze esterne aggiuntive introdotte senza valutazione | Media | Basso | Revisione esplicita a ogni iterazione | Aperto |

---

## Strategia di testing

<!-- Documentare l'approccio al testing prima di scrivere il codice.
     Senza una strategia esplicita, il testing viene sempre rimandato. -->

### Test manuali (obbligatori per ogni iterazione)

- Eseguire ogni caso documentato in `docs/test-matrix.md` dopo ogni iterazione.
- Testare sia su emulatore/simulatore che su dispositivo fisico (se applicabile).
- Documentare l'esito di ogni test in `docs/iterations/it-XX.md`.

### Test automatici (raccomandati)

- Test unitari per: servizi, repository, logica di business, parsing dati.
- Test di integrazione per: operazioni di persistenza locale, chiamate API mockate.
- Non è richiesto il 100% di coverage, ma la logica critica deve avere almeno un test.

### Criteri di accettazione dei test

Un'iterazione non è completa se:
- almeno un test del caso limite documentato in spec.md fallisce;
- si è verificato un crash non intercettato durante i test manuali;
- uno stato UI (loading / errore / empty / dati) non viene mostrato correttamente.

---

## Strategia di documentazione

<!-- La documentazione non è opzionale. Documentare dopo ogni iterazione
     costa poco; recuperarla alla fine costa molto. -->

Dopo ogni iterazione aggiornare **obbligatoriamente**:

- `docs/iterations/it-XX.md` — log dell'iterazione (sempre)
- `docs/test-matrix.md` — se sono stati aggiunti o modificati test
- `docs/api-notes.md` — se è stata integrata o modificata una API
- `docs/architecture.md` — se è stata presa una decisione architetturale rilevante
- `docs/spec.md` — solo se lo scope è cambiato (con motivazione esplicita)

---

## Definition of Done

<!-- Questi criteri si applicano a ogni singola iterazione.
     Un'iterazione non completata secondo questi criteri non viene
     considerata chiusa, anche se il codice è presente. -->

Un'iterazione si considera **completata** quando:

- [ ] Il codice compila senza errori e senza warning non giustificati
- [ ] La funzionalità è testata su emulatore/dispositivo fisico (se applicabile)
- [ ] Tutti i casi limite della funzionalità sono stati verificati
- [ ] I tre stati UI (loading, errore, empty) sono gestiti dove applicabile
- [ ] Nessuna credenziale o dato sensibile è presente nel codice committato
- [ ] Il codice è stato letto e compreso dall'autore dopo la scrittura
- [ ] Il file `docs/iterations/it-XX.md` è aggiornato
- [ ] Il branch è stato unito a `main` con un commit semantico corretto
- [ ] Nessuna funzionalità esistente è stata rotta (regressione verificata manualmente)
