# Guida ai prompt

Questo file elenca i messaggi che l'utente può inviare a Claude per avviare
le azioni principali del progetto. Ogni prompt attiva un processo specifico
definito nei file di documentazione.

---

## Inizializzazione del progetto

**Quando usarlo**: la prima volta che si apre una sessione su un progetto
appena clonato da questo template.

**Prompt di esempio**:

```
iniziamo
partiamo
voglio creare un'app
ho clonato il template, da dove si comincia?
```

**Cosa succede**: Claude controlla il git log. Se non trova il commit di
inizializzazione, chiede all'utente di descrivere liberamente il progetto,
poi fa domande mirate per colmare le lacune, compila tutti i file di
documentazione, aspetta l'approvazione e crea il branch `develop`.

**Processo completo**: `CLAUDE.md` → sezione "Inizializzazione del progetto"

---

## Nuova iterazione

**Quando usarlo**: ogni volta che si vuole aggiungere una funzionalità
o avviare un nuovo ciclo di sviluppo.

**Prompt di esempio**:

```
inizia iterazione 3
nuova iterazione
voglio implementare la schermata di ricerca
partiamo con la gestione dei preferiti
aggiungiamo il login
```

**Cosa succede**: Claude raccoglie e chiarisce i requisiti, crea il branch
di iterazione da `develop`, redige il file `docs/iterations/it-XX.md` e
aspetta l'approvazione prima di scrivere qualsiasi codice. Alla fine esegue
il merge su `develop` con `--no-ff`.

**Processo completo**: `docs/iteration-workflow.md`

---

## Rilascio su main

**Quando usarlo**: quando il progetto ha raggiunto uno stato stabile e
consegnabile (MVP completato, milestone raggiunta, versione da consegnare).

**Prompt di esempio**:

```
siamo pronti per il rilascio
facciamo il merge su main
tagghiamo la versione 1.0
```

**Cosa succede**: Claude esegue il merge di `develop` su `main` con `--no-ff`
e crea un tag di versione.

```
git checkout main
git merge --no-ff develop -m "release: [descrizione]"
git tag v[X.Y.Z]
```

---

## Domande e chiarimenti (uso libero)

Per qualsiasi altra richiesta che non rientra nei processi sopra — spiegazioni
sul codice, revisioni, analisi, domande sull'architettura — non è necessario
un prompt specifico. Scrivere liberamente e Claude risponderà seguendo le
regole operative definite in `CLAUDE.md`.

Esempi:

```
spiegami come funziona il service X
c'è un modo migliore per gestire questa logica?
cosa potremmo fare per risolvere questo bug?
rivedi il codice dell'iterazione 3
```
