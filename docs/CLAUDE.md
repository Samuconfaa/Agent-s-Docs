# CLAUDE.md

## Inizializzazione del progetto

<!-- ATTENZIONE: questa sezione è temporanea. Va eliminata completamente
     da questo file al termine del Passo D, prima del commit iniziale. -->

Quando l'utente clona questo template e scrive un messaggio del tipo:

- "iniziamo"
- "voglio creare un'app"
- "partiamo"
- "ho clonato il template, da dove si comincia?"
- qualsiasi messaggio che segnala l'avvio di un nuovo progetto

…seguire **nell'ordine** i passi A, B, C e D senza saltarne nessuno.

### Passo A — Raccolta delle informazioni

Inviare all'utente **in un unico messaggio** le seguenti domande.
Non procedere prima di aver ricevuto le risposte a tutte.

1. Come si chiama il progetto e cosa fa, in una frase?
2. Chi lo usa e in quale contesto d'uso?
3. Quali sono le 3–5 funzionalità principali che deve avere?
4. Ci sono funzionalità secondarie o opzionali?
5. Quale linguaggio e framework vuoi usare?
6. L'app si appoggia ad API esterne? Se sì, quali conosci già?
7. Quali vincoli ci sono? (tempo disponibile, piattaforma target, complessità massima, ecc.)
8. È un progetto didattico, un prototipo o qualcosa destinato a essere usato in produzione?

Se le risposte sono vaghe, incomplete o contraddittorie, fare domande di chiarimento
prima di procedere al Passo B. Non compilare i file con informazioni incerte.

### Passo B — Compilazione dei file

Con le risposte ricevute, compilare nell'ordine:

1. `docs/spec.md` — sostituire tutti i placeholder con le informazioni del progetto
2. `docs/architecture.md` — compilare le scelte di pattern, layer e tecnologie
3. `docs/plan.md` — definire le iterazioni in base alle funzionalità dichiarate
4. `docs/api-notes.md` — compilare solo se sono presenti API esterne già note;
   altrimenti eliminare il file
5. Questo file (`CLAUDE.md`) — compilare le sezioni "Contesto del progetto"
   e "Scelte tecniche" con i dati reali del progetto

Regole per la compilazione:
- Sostituire ogni placeholder (`[...]`) con i dati reali.
- Rimuovere tutti i commenti HTML `<!-- -->` dei template.
- Adattare gli esempi al progetto reale, non lasciarli come riferimento generico.
- Se una sezione non è applicabile al progetto, eliminarla.

### Passo C — Approvazione

Mostrare all'utente un riepilogo dei file compilati e chiedere conferma esplicita.
Se l'utente richiede correzioni, applicarle e ripresentare il riepilogo.
Non procedere al Passo D senza approvazione esplicita.

### Passo D — Setup git e pulizia

Una volta che l'utente approva i file:

1. Creare il branch `develop`:
   ```
   git branch develop
   ```
2. Eliminare **questa intera sezione** `## Inizializzazione del progetto`
   da questo file. Il progetto è configurato e la sezione non serve più.
3. Committare la configurazione iniziale:
   ```
   git add .
   git commit -m "chore: configure project from template"
   ```

---

## Contesto del progetto

<!-- Compilare questa sezione durante l'inizializzazione (Passo B).
     Descrivere cosa fa l'app e l'obiettivo principale di sviluppo.
     Non descrivere la tecnologia qui: quella va in "Scelte tecniche". -->

[Descrivere in 2-3 righe cosa fa l'applicazione e il suo obiettivo principale.
Indicare se si tratta di un progetto didattico, di produzione, di prototipo, ecc.]

**Documentazione di riferimento**:
- Specifica completa: `docs/spec.md`
- Piano di lavoro e iterazioni: `docs/plan.md`
- Architettura e pattern: `docs/architecture.md`
- Note sulle API esterne: `docs/api-notes.md`
- Log delle iterazioni: `docs/iterations/` — il file `docs/iterations/README.md` contiene il template da seguire per ogni nuova iterazione
- **Workflow iterazioni: `docs/iteration-workflow.md` — da seguire obbligatoriamente ogni volta che l'utente richiede una nuova iterazione**

---

## Scelte tecniche

<!-- Elencare le scelte tecnologiche già decise per questo progetto.
     Non includere tecnologie "possibili": solo quelle effettivamente adottate.
     Ogni voce non ovvia deve avere una motivazione. -->

- **Linguaggio**: [es. Kotlin / Swift / Dart / TypeScript / C#]
- **Framework / piattaforma**: [es. React Native / Flutter / .NET MAUI / Jetpack Compose]
- **Pattern architetturale**: [es. MVVM / Clean Architecture / MVC]
- **Navigazione**: [es. Stack-based / Tab-based / Declarative Shell]
- **Persistenza locale**: [es. SQLite / Room / CoreData / Preferences]
- **Comunicazione remota**: [es. HTTP client asincrono / GraphQL client]
- **Parsing dati**: [es. libreria built-in / libreria specifica]
- **Gestione dello stato / MVVM toolkit**: [es. built-in / libreria specifica]
- **Iniezione delle dipendenze**: [es. built-in / libreria specifica / manuale]

---

## Regole operative

<!-- Queste regole si applicano a ogni interazione con l'AI durante lo sviluppo.
     Sono non negoziabili: se una regola deve essere derogata, va documentata
     la motivazione nel log dell'iterazione corrente. -->

### Nuova iterazione

Quando l'utente scrive un messaggio del tipo:

- "inizia iterazione X"
- "nuova iterazione"
- "voglio implementare [funzionalità]"
- "partiamo con [funzionalità]"
- qualsiasi richiesta di aggiungere una nuova funzionalità al progetto

…seguire **obbligatoriamente e nell'ordine** tutti i passi descritti in
`docs/iteration-workflow.md`. Non saltare né riordinare i passi senza
motivazione esplicita.

### Prima di qualsiasi modifica

- **Proporre sempre un piano** prima di modifiche che toccano più di un file.
  Il piano deve elencare: file coinvolti, rischi, dipendenze, test suggeriti.
- **Leggere il codice esistente** prima di scrivere nuovo codice.
  Non assumere la struttura: verificarla.
- **Limitare ogni iterazione a una sola feature ben definita.**
  Se una richiesta tocca più aree, suddividerla in iterazioni separate.

### Durante l'implementazione

- **Non introdurre dipendenze esterne** senza motivazione esplicita e approvazione.
  Preferire sempre ciò che è già disponibile nel linguaggio o nel framework.
- **Non spostare logica nella View o nel code-behind** se può stare in un
  ViewModel, Controller o Service.
- **Non rimuovere codice esistente** senza spiegare perché.
  Se il codice è obsoleto, indicarlo e attendere conferma.
- **Non generare blocchi di codice non richiesti.**
  Implementare solo ciò che è stato esplicitamente richiesto nell'iterazione corrente.
- **Gestire sempre i tre stati UI**: loading, errore, empty.
  Uno stato non gestito è un bug, non un'omissione accettabile.
- **Non silenziare mai gli errori.** Ogni eccezione deve essere intercettata,
  loggata e comunicata all'utente in modo appropriato.
- **Evitare duplicazioni.** Prima di scrivere qualcosa di nuovo, verificare
  se esiste già nel codebase.

### Nomenclatura e stile

- Usare le convenzioni di nomenclatura standard del linguaggio scelto in modo coerente.
- Nomi descrittivi e non ambigui: un nome che richiede un commento per essere capito
  è un nome da cambiare.
- Componenti piccoli con responsabilità singola e delimitata.
- Metodi asincroni dove l'operazione può bloccare il thread principale.
- Commenti solo quando il PERCHÉ non è deducibile dal codice.
  Non commentare ciò che il codice dice già.

### Gestione del versioning con Git

#### Branch

**Struttura dei branch permanenti**:

| Branch | Scopo | Chi ci scrive |
|--------|-------|--------------|
| `main` | Versione ufficiale rilasciata. Ogni commit su `main` rappresenta una release stabile consegnabile. | Solo merge da `develop` a milestone raggiunte |
| `develop` | Integrazione continua del lavoro. Contiene tutte le iterazioni completate. | Solo merge da branch di iterazione |

**Setup iniziale del progetto** (eseguire una sola volta):

```
git init
git commit --allow-empty -m "chore: init repository"
git branch develop
```

Da questo momento `main` e `develop` esistono entrambi. Tutto il lavoro ordinario avviene su `develop` e i suoi branch figli.

**Ciclo di vita di ogni iterazione**:

```
# 1. Partire sempre da develop aggiornato
git checkout develop
git pull

# 2. Creare il branch dell'iterazione
git checkout -b iter/XX-nome-feature

# 3. Lavorare e committare sul branch
# ... commit semantici ...

# 4. A iterazione completata, mergiare su develop
git checkout develop
git merge --no-ff iter/XX-nome-feature
git branch -d iter/XX-nome-feature
```

**Promozione a main** (solo a milestone o rilascio):

```
git checkout main
git merge --no-ff develop -m "release: [descrizione della versione]"
git tag v[X.Y.Z]
```

**Regole obbligatorie**:

- Non si lavora mai direttamente su `main` o `develop`.
- I branch di iterazione nascono sempre da `develop`, mai da `main` o da altri branch di iterazione.
- Il flag `--no-ff` è obbligatorio in ogni merge: preserva la storia dell'iterazione come gruppo di commit distinto nel log.
- `main` riceve commit solo quando il progetto raggiunge uno stato consegnabile (MVP completato, versione stabile, consegna finale).
- Non si crea un branch da un altro branch di iterazione, salvo necessità esplicitamente documentata.

#### Commit semantici

Il messaggio di ogni commit segue il formato **Conventional Commits**:

```
<tipo>[scope opzionale]: <descrizione in minuscolo, imperativa, max 72 caratteri>

[corpo opzionale: spiega il PERCHÉ, non il cosa — massimo 3 righe]

[footer opzionale: BREAKING CHANGE: ... oppure Closes #N]
```

**Tipi obbligatori**:

| Tipo | Quando usarlo |
|------|--------------|
| `feat` | Aggiunge una nuova funzionalità visibile all'utente |
| `fix` | Corregge un bug |
| `refactor` | Modifica il codice senza aggiungere funzionalità né correggere bug |
| `docs` | Aggiorna solo documentazione (md, commenti, README) |
| `test` | Aggiunge o modifica test |
| `chore` | Aggiorna dipendenze, configurazione, script di build, CI |
| `style` | Formattazione, spaziatura, ordine import — nessuna logica cambiata |
| `perf` | Migliora le prestazioni senza cambiare il comportamento |
| `revert` | Annulla un commit precedente |

**Regole sul messaggio**:

- La descrizione è in minuscolo e all'imperativo: `add search screen`, non `Added search screen`.
- Nessun punto finale nella riga del titolo.
- Lo scope è opzionale ma utile per progetti grandi: `feat(search): add pagination`.
- Il corpo del commit spiega il PERCHÉ della modifica, non il cosa (il cosa è nel diff).
- Un commit = una modifica logica coerente. Non mescolare fix e refactor nello stesso commit.

**Esempi corretti**:

```
feat(search): add text input with debounce
fix(api): handle null field in search response
refactor(viewmodel): extract loading state into base class
docs: update iteration 03 log
chore: update dependency X to version Y
test(repository): add unit test for empty response case
```

**Esempi errati**:

```
fix stuff                        ← nessun tipo, nessun contesto
WIP                              ← non committare lavoro non funzionante
aggiornamenti vari               ← troppo vago
Fixed the bug that caused crash  ← maiuscola iniziale, passato, punto implicito
feat: added new feature.         ← passato e punto finale
```

**Regola sull'autore dei commit**:

I commit non devono includere co-autori automatici (es. `Co-authored-by: Claude`
o simili). Ogni commit deve risultare firmato solo dall'autore umano del progetto.
Non aggiungere footer di attribuzione all'AI in nessun commit.

---

## Formato di risposta atteso

<!-- L'AI deve strutturare le risposte in questo formato per ogni richiesta significativa.
     Una risposta che salta questi punti è incompleta. -->

Per ogni richiesta che implica una modifica al codice, restituire nell'ordine:

1. **Piano breve** — elenco dei file da creare o modificare, con il motivo
2. **Implementazione** — il codice richiesto, nulla di più
3. **Rischi e dipendenze** — cosa potrebbe andare storto, su cosa dipende
4. **Test manuali suggeriti** — almeno 3 casi da verificare, inclusi casi limite

Per richieste di spiegazione o analisi: risposta diretta senza struttura rigida.

---

## Policy di documentazione

<!-- La documentazione deve essere aggiornata durante l'iterazione, non dopo.
     Documentare "dopo" porta a documentazione incompleta o mai aggiornata. -->

Dopo ogni iterazione significativa, aggiornare **obbligatoriamente**:

- `docs/iterations/it-XX.md` — sempre, per ogni iterazione (copiare la struttura da `docs/iterations/README.md`)
- `docs/test-matrix.md` — se sono stati aggiunti o modificati test
- `docs/api-notes.md` — se è stata integrata o modificata una API esterna
- `docs/architecture.md` — se è stata presa una decisione architetturale rilevante
- `docs/spec.md` — solo se lo scope è cambiato (con motivazione esplicita)
- `docs/plan.md` — se il piano delle iterazioni è stato revisionato

---

## Coding style

- Componenti piccoli con responsabilità unica e delimitata.
- Servizi / Repository separati dalla logica di presentazione.
- ViewModel (o equivalente) con proprietà di stato esplicite:
  almeno `IsBusy`, `ErrorMessage`, `HasData`, `IsEmpty`.
- Metodi asincroni per qualsiasi operazione che accede a rete, disco o risorse di sistema.
- Gestione degli errori non silenziosa: ogni `catch` fa almeno una cosa utile.
- Commenti solo quando il motivo non è deducibile dal codice.
  Mai commenti che ripetono ciò che il codice dice.

---

## Anti-pattern vietati

- Logica di business o chiamate di rete nella View o nel code-behind.
- Mix di strategie di navigazione diverse senza motivazione documentata.
- Nomi di classi, proprietà o variabili incoerenti tra loro.
- Dipendenze esterne aggiunte senza discussione e documentazione.
- Refactoring ampi in un'unica iterazione insieme a nuove feature.
- Codice che l'autore non riesce a spiegare dopo averlo scritto.
- Catch vuoti o che restituiscono `null` senza gestire l'errore.
- Stato UI implicito (derivato da condizioni multiple invece che da proprietà esplicite).
- TODO nel codice committato senza riferimento a un'issue o iterazione specifica.

---

## Definition of Done (per ogni iterazione)

Un'iterazione è completa solo quando tutte queste condizioni sono vere:

- [ ] Il codice compila senza errori e senza warning non giustificati
- [ ] La funzionalità è testata su dispositivo o emulatore reale
- [ ] I casi limite della funzionalità sono stati verificati manualmente
- [ ] I tre stati UI (loading / errore / empty) sono gestiti dove applicabile
- [ ] Nessuna credenziale o dato sensibile è nel codice committato
- [ ] Il codice è stato letto e compreso dopo la generazione
- [ ] Nessuna regressione nelle funzionalità esistenti
- [ ] Il branch è unito a `main` con commit semantico corretto
- [ ] `docs/iterations/it-XX.md` è compilato e aggiornato
