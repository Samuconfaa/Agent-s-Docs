# IA Project Template

Template di documentazione e workflow per progetti software sviluppati con
assistenza AI (Claude Code).

Clonando questa repo si ottiene una struttura pronta all'uso: documentazione
preimpostata, regole operative per l'AI, un processo di inizializzazione
guidato e un workflow iterativo standardizzato.

---

## Come funziona

### 1. Clona e apri con Claude Code

```
git clone <url-repo> nome-progetto
cd nome-progetto
```

Apri la cartella con Claude Code. Il file `CLAUDE.md` alla root viene letto
automaticamente dall'agente ad ogni sessione.

### 2. Inizializzazione automatica

La prima cosa che Claude fa ad ogni sessione è controllare il git log:

```
git log --oneline
```

Se non trova il commit `chore: configure project from template`, sa che il
progetto non è ancora stato configurato e avvia il processo di setup.

**Scrivi semplicemente**:

```
iniziamo
```

Claude chiederà prima di tutto di descrivere il progetto liberamente.
Sulla base della descrizione farà domande mirate solo su ciò che non è chiaro,
poi compilerà automaticamente tutti i file di documentazione (`spec.md`,
`architecture.md`, `plan.md`, ecc.) e aspetterà la tua approvazione prima
di confermare.

Al termine crea il branch `develop` ed esegue il commit di configurazione.
Alla sessione successiva Claude troverà quel commit nel git log, eliminerà
automaticamente la sezione di inizializzazione da `CLAUDE.md` e la committa.
Da quel momento il file è pulito e il check non viene più eseguito.

### 3. Sviluppo iterativo

Ogni funzionalità viene sviluppata in un'iterazione separata. Per avviarne una:

```
voglio implementare [funzionalità]
```

Claude segue il processo definito in `docs/iteration-workflow.md`:

1. Chiarisce i requisiti con domande mirate
2. Crea un branch `iter/XX-nome-feature` da `develop`
3. Redige il file `docs/iterations/it-XX.md` e aspetta approvazione
4. Implementa il codice
5. Guida l'utente nella verifica e nei test
6. Risolve eventuali problemi documentandoli nel file di iterazione
7. Verifica la Definition of Done
8. Fa il merge su `develop` con `--no-ff`
9. Chiude il file di iterazione e aggiorna la documentazione

### 4. Rilascio

Quando il progetto raggiunge uno stato stabile:

```
siamo pronti per il rilascio
```

Claude esegue il merge di `develop` su `main` e crea un tag di versione.

---

## Struttura del progetto

```
/
├── CLAUDE.md                    ← letto automaticamente da Claude Code
├── README.md                    ← questo file
└── docs/
    ├── spec.md                  ← specifica del progetto
    ├── plan.md                  ← piano di lavoro e iterazioni previste
    ├── architecture.md          ← decisioni architetturali
    ├── api-notes.md             ← documentazione API esterne
    ├── iteration-workflow.md    ← processo passo-passo per ogni iterazione
    ├── prompt-guide.md          ← prompt disponibili e cosa attivano
    ├── test-matrix.md           ← tutti i casi di test manuali del progetto
    ├── changelog.md             ← registro delle versioni rilasciate
    └── iterations/
        ├── README.md            ← template per i log di iterazione
        ├── it-01.md             ← log iterazione 1 (creato durante lo sviluppo)
        └── ...
```

---

## Strategia git

| Branch | Scopo |
|--------|-------|
| `main` | Versioni ufficiali rilasciate — tocca solo a milestone |
| `develop` | Integrazione di tutte le iterazioni completate |
| `iter/XX-nome` | Un branch per iterazione, nasce da `develop` e vi torna |

---

## File di riferimento rapido

| Vuoi... | Leggi... |
|---------|---------|
| Sapere quali prompt usare | `docs/prompt-guide.md` |
| Capire il processo di ogni iterazione | `docs/iteration-workflow.md` |
| Vedere il template per un log di iterazione | `docs/iterations/README.md` |
| Capire le regole operative dell'AI | `CLAUDE.md` |
| Vedere cosa è cambiato tra le versioni | `docs/changelog.md` |
| Consultare i casi di test del progetto | `docs/test-matrix.md` |
