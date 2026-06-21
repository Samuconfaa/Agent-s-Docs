# Architettura del progetto

## Obiettivo di questo documento

Descrivere l'organizzazione tecnica dell'applicazione: i layer che la compongono,
le responsabilità di ciascuno, le regole di dipendenza tra di essi e il flusso
dei dati tra i componenti.

Questo documento deve essere aggiornato ogni volta che una decisione architetturale
cambia. Un'architettura documentata solo all'inizio e non aggiornata è fuorviante.

---

## Principi architetturali adottati

<!-- Indicare i principi che guidano tutte le decisioni tecniche.
     Questi principi devono essere sufficientemente concreti da poter
     risolvere ambiguità quando sorge una scelta di design. -->

1. **Separazione delle responsabilità**: ogni componente ha un solo motivo per cambiare.
2. **Dipendenze verso l'interno**: i layer esterni dipendono da quelli interni, mai il contrario.
3. **Testabilità**: la logica di business deve poter essere verificata in isolamento.
4. **Esplicitezza degli stati**: ogni stato visibile dell'applicazione deve essere
   rappresentato da una proprietà esplicita, non derivato implicitamente.
5. **Nessun errore silenzioso**: ogni eccezione viene intercettata, loggata e comunicata.
6. **Immutabilità dei dati dove possibile**: i modelli di dati non vengono modificati
   in-place; si creano nuove istanze con i valori aggiornati.

---

## Pattern architetturale

<!-- Descrivere il pattern principale adottato e la motivazione.
     Indicare chiaramente cosa rientra in ogni layer e cosa NON vi rientra.
     Includere le regole di dipendenza tra i layer. -->

### [Nome del pattern, es. MVVM / Clean Architecture / MVC / MVP]

[Descrizione sintetica del pattern e del perché è stato scelto per questo progetto]

### Regole di dipendenza tra layer (obbligatorie)

```
[Layer Presentazione]
       ↓ dipende da
[Layer Logica / ViewModel / Controller]
       ↓ dipende da
[Layer Servizi / Use Case]
       ↓ dipende da
[Layer Dati / Repository / API]
```

- Il layer presentazione NON contiene logica di business.
- Il layer logica NON conosce i dettagli dell'interfaccia grafica.
- Il layer servizi NON conosce il framework UI.
- Il layer dati NON contiene logica di business.
- Le interfacce/contratti sono definiti dal layer che li usa, non da chi li implementa.

---

## Componenti principali

<!-- Per ogni componente descrivere: cosa fa, cosa NON deve fare,
     e come comunica con gli altri componenti.
     La colonna "NON deve" è importante quanto "Responsabilità". -->

| Componente | Responsabilità | NON deve | Comunica con |
|-----------|---------------|----------|--------------|
| **Presentazione** (View / Screen / Page) | Layout, binding dati, feedback visivo, intercettare input utente | Contenere logica, fare chiamate di rete, accedere direttamente ai dati | ViewModel / Controller |
| **ViewModel / Controller** | Stato della UI, comandi, orchestrazione delle operazioni, trasformazione dati per la vista | Conoscere dettagli del framework UI, accedere direttamente alla rete o al DB | Servizi, Modelli |
| **Servizi** | Operazioni di dominio, chiamate API, accesso alla persistenza locale, regole di business | Conoscere il framework UI, dipendere dal layer presentazione | Repository, API client, Storage |
| **Repository / Data source** | Accesso ai dati (remoti o locali), cache, serializzazione | Contenere logica di business, conoscere la UI | API esterne, Storage locale |
| **Modelli / DTO** | Strutture dati pure, senza logica o dipendenze | Dipendere da altri layer, contenere logica | Tutti i layer (passati come dati) |
| **Utilità / Helper** | Funzioni condivise senza stato (formattazione, validazione, conversione) | Dipendere da layer specifici, contenere stato | Chiamati dove necessario |

---

## Struttura delle cartelle

<!-- Definire la struttura di directory che riflette l'architettura.
     La struttura deve essere leggibile da uno sviluppatore nuovo al progetto.
     Ogni cartella deve avere uno scopo non ambiguo.
     Se una cartella contiene solo un file, probabilmente non serve. -->

```
ProjectRoot/
├── src/
│   └── [NomeProgetto]/
│       ├── Models/           ← Strutture dati pure (entità di dominio)
│       ├── DTOs/             ← Oggetti di trasferimento dati (risposta API, storage)
│       ├── Services/
│       │   ├── Interfaces/   ← Contratti dei servizi (interfacce/protocolli)
│       │   └── Impl/         ← Implementazioni concrete
│       ├── Repositories/
│       │   ├── Interfaces/
│       │   └── Impl/
│       ├── ViewModels/       ← (o Controllers, Presenters, a seconda del pattern)
│       ├── Views/            ← (o Screens, Pages, Components)
│       ├── Helpers/          ← Utilità condivise senza stato
│       └── Config/           ← Costanti, configurazione, DI setup
├── tests/
│   ├── Unit/
│   └── Integration/
├── docs/
└── [file di configurazione del progetto]
```

---

## Iniezione delle dipendenze

<!-- Descrivere come vengono risolte le dipendenze tra i componenti.
     Specificare: dove vengono registrate, come vengono iniettate, chi le crea.
     Un sistema di DI non documentato porta a dipendenze occulte. -->

### Regole

- Tutte le dipendenze devono essere dichiarate esplicitamente nel costruttore
  (o tramite il meccanismo di DI del framework scelto).
- Nessun componente deve creare direttamente le proprie dipendenze con `new`
  se queste dipendenze hanno effetti collaterali o richiedono configurazione.
- I servizi che accedono a risorse condivise (rete, database) devono essere
  registrati come singleton o con ciclo di vita esplicito.
- I ViewModel devono ricevere i servizi tramite iniezione, non cercarli attivamente.

### Registrazione

[Descrivere dove e come vengono registrati i servizi nell'applicazione,
es. file di bootstrap, contenitore DI, factory manuale]

---

## Flusso dati tipico

<!-- Descrivere il percorso che compie un'azione dell'utente
     dalla View fino alla risposta finale.
     Questo schema deve essere applicato coerentemente in tutta l'app. -->

### Operazione di lettura (es. caricamento lista)

```
Utente
  → [View] intercetta evento (tap, scroll, init)
  → [ViewModel] imposta IsBusy = true, chiama ServiceAsync()
  → [Service] chiama Repository.GetAsync()
  → [Repository] effettua richiesta remota o legge da cache
  → [Repository] deserializza risposta in DTO
  → [Service] converte DTO in Model, applica logica di dominio
  → [ViewModel] riceve Model, aggiorna proprietà osservabili
  → [ViewModel] imposta IsBusy = false, HasData = true
  → [View] aggiorna automaticamente la visualizzazione tramite binding
```

### Operazione di scrittura (es. salvataggio)

```
Utente
  → [View] intercetta azione (tap su "Salva")
  → [ViewModel] valida input, chiama SaveAsync(model)
  → [Service] applica logica pre-salvataggio (es. deduplicazione)
  → [Repository] persiste il dato nello storage locale
  → [Service] restituisce esito (successo / errore)
  → [ViewModel] aggiorna stato (messaggio conferma o ErrorMessage)
  → [View] mostra feedback all'utente
```

---

## Gestione degli stati UI

<!-- Ogni schermata che carica dati deve gestire esplicitamente tutti gli stati.
     Stato non esplicito = stato non testabile = bug nascosti. -->

### Proprietà obbligatorie in ogni ViewModel con dati asincroni

| Proprietà | Tipo | Valore iniziale | Descrizione |
|-----------|------|----------------|-------------|
| `IsBusy` | bool | false | Operazione asincrona in corso |
| `ErrorMessage` | string | "" | Messaggio di errore (vuoto = nessun errore) |
| `HasError` | bool | false | Derivato da ErrorMessage, per binding visibile |
| `HasData` | bool | false | Dati presenti e visualizzabili |
| `IsEmpty` | bool | false | Richiesta completata con risultato vuoto |

### Regola di mutua esclusività degli stati

In ogni momento deve essere vero uno e uno solo tra:

- `IsBusy = true` (caricamento in corso)
- `HasError = true` (errore, nessun dato)
- `IsEmpty = true` (nessun risultato, operazione OK)
- `HasData = true` (dati presenti)

### Comportamento della View per ogni stato

| Stato | Elemento visivo atteso |
|-------|----------------------|
| `IsBusy` | Indicatore di caricamento visibile, contenuto nascosto o bloccato |
| `HasError` | Messaggio di errore visibile + pulsante "Riprova" |
| `IsEmpty` | Messaggio "Nessun risultato" appropriato al contesto |
| `HasData` | Contenuto principale visibile, nessun indicatore di stato |

---

## Gestione degli errori

<!-- La gestione degli errori deve essere uniforme in tutta l'app.
     Documentare qui le convenzioni adottate, non lasciarle implicite. -->

### Gerarchia di gestione

1. **Repository / Data source**: cattura errori di rete, I/O, parsing.
   Li converte in eccezioni di dominio o risultati tipizzati (es. `Result<T>`).
2. **Service**: cattura eccezioni dal repository, applica logica di fallback
   (es. dati cached), ri-lancia solo se il fallback non è possibile.
3. **ViewModel**: cattura tutte le eccezioni nei blocchi `try/catch`,
   imposta `ErrorMessage`, imposta `IsBusy = false`.
   Non propaga mai eccezioni verso la View.
4. **View**: non cattura mai eccezioni. Risponde solo ai cambiamenti di stato del ViewModel.

### Categorie di errori e messaggi

| Categoria | Causa | Messaggio utente | Azione suggerita |
|-----------|-------|-----------------|-----------------|
| Rete assente | Nessuna connessione | "Nessuna connessione disponibile" | Pulsante "Riprova" |
| Timeout | Risposta troppo lenta | "La richiesta ha impiegato troppo tempo" | Pulsante "Riprova" |
| Errore server (5xx) | Problema lato API | "Servizio temporaneamente non disponibile" | Riprova più tardi |
| Errore client (4xx) | Richiesta non valida | "Richiesta non valida" (dettaglio in log) | Nessuna azione utente |
| Parsing fallito | Struttura dati inattesa | "Dati ricevuti non validi" | Pulsante "Riprova" |
| Storage pieno | Spazio disco esaurito | "Spazio insufficiente sul dispositivo" | Indicare dove liberare spazio |

### Regole obbligatorie

- Ogni blocco `catch` deve fare almeno una di queste tre cose:
  (1) gestire l'errore in modo definitivo, (2) loggarlo, (3) propagarlo verso l'alto.
- Un `catch` vuoto o con solo `return null` è un anti-pattern vietato.
- Il messaggio mostrato all'utente non deve mai contenere stack trace o tecnicismi.
- Il log interno deve contenere informazioni sufficienti per il debug (tipo eccezione,
  contesto, parametri rilevanti).

---

## Persistenza locale

<!-- Descrivere quali dati vengono salvati localmente, con quale tecnologia
     e con quale ciclo di vita. -->

| Dato | Tecnologia scelta | Motivazione | Ciclo di vita |
|------|------------------|-------------|--------------|
| [Preferiti utente] | [SQLite / file / key-value store] | [struttura relazionale / semplicità] | [permanente fino a cancellazione esplicita] |
| [Impostazioni] | [key-value store] | [coppie chiave-valore semplici] | [permanente] |
| [Cache dati remoti] | [SQLite / file / memoria] | [riuso tra sessioni / velocità] | [TTL: X ore, invalidata a logout] |
| [Sessione utente] | [storage sicuro di sistema] | [dati sensibili] | [fino al logout] |

### Regole per la persistenza

- Nessun accesso diretto allo storage dalla View o dal ViewModel.
  Tutto passa attraverso il Repository o il Service.
- La struttura dello storage deve essere versionate: ogni modifica
  alla struttura dati locale deve includere una migrazione.
- I dati in cache devono avere un timestamp di creazione e una logica
  di invalidazione esplicita.

---

## Sicurezza

<!-- Queste regole non sono opzionali. Documentarle qui rende esplicito
     cosa deve essere verificato prima di ogni rilascio. -->

### Credenziali e segreti

- **Nessuna chiave API, password o token** deve apparire nel codice sorgente
  o nei file committati nel repository.
- Le credenziali per l'ambiente di sviluppo vengono gestite tramite
  variabili d'ambiente o file locali esclusi dal controllo versione.
- Le credenziali per la produzione vengono gestite tramite
  [specificare: CI/CD secrets, vault, ecc.].

### Validazione degli input

- Ogni dato proveniente dall'utente deve essere validato prima dell'uso,
  al massimo al livello del ViewModel o del Service.
- La lunghezza massima degli input deve essere limitata sia lato UI che lato logica.
- I dati ricevuti da API esterne non devono essere considerati affidabili:
  validare struttura e tipi prima dell'uso.

### Dati locali sensibili

- Dati considerati sensibili (token, dati personali) devono essere salvati
  tramite lo storage protetto del sistema operativo, non in plain text.
- Definire esplicitamente quali dati sono "sensibili" nel contesto di questo progetto:
  [elencare qui i dati sensibili specifici]

---

## Estendibilità

<!-- Descrivere le decisioni architetturali che facilitano l'aggiunta di funzionalità
     future, senza però progettare per requisiti non esistenti. -->

L'architettura adottata consente di:

- Aggiungere nuove schermate senza modificare quelle esistenti (se la navigazione è dichiarativa).
- Sostituire l'implementazione di un servizio con un mock per i test (tramite interfacce).
- Aggiungere nuovi provider di dati (es. seconda API, database diverso) senza
  toccare la logica di presentazione.
- Modificare la tecnologia di persistenza locale cambiando solo il Repository concreto.

**Non progettare per requisiti non presenti nella specifica.**
L'estendibilità deriva dall'architettura pulita, non dall'aggiunta di astrazioni preventive.

---

## Decisioni architetturali rilevanti

<!-- Tracciare le decisioni importanti con la loro motivazione.
     Questo aiuta a capire perché il codice è fatto in un certo modo
     e a non tornare indietro su scelte già valutate. -->

| Data | Decisione | Motivazione | Alternative considerate |
|------|-----------|-------------|------------------------|
| [GG/MM/AAAA] | [es. Uso di pattern Result<T> invece di eccezioni] | [es. evitare eccezioni per flussi normali] | [throw/catch puro] |
| [GG/MM/AAAA] | [...] | [...] | [...] |
