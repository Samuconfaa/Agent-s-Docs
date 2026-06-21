# Workflow per ogni iterazione

Questo file descrive il processo obbligatorio da seguire ogni volta che l'utente
vuole implementare una nuova iterazione. I passi sono sequenziali: nessun passo
può essere saltato senza motivazione esplicita documentata nel file di iterazione.

---

## Passo 1 — Raccolta dei requisiti

Chiedere all'utente cosa vuole implementare in questa iterazione.

Prima di procedere, verificare che siano chiari tutti questi punti:

- **Obiettivo**: cosa deve fare la funzionalità, dal punto di vista dell'utente
- **Scope**: cosa è incluso e cosa non lo è in questa iterazione
- **Dipendenze**: si appoggia a codice già esistente? Quale?
- **Casi limite**: come si comporta in caso di input vuoto, errore, assenza di dati?
- **Criteri di verifica**: come si controlla che funzioni correttamente?

Se uno di questi punti non è chiaro, fare domande specifiche all'utente prima di
procedere. Non iniziare l'implementazione con requisiti ambigui.

---

## Passo 2 — Creazione del branch

Creare un branch dedicato che parte da `develop` aggiornato:

```
git checkout develop
git pull
git checkout -b iter/XX-nome-feature
```

Il nome del branch deve rispecchiare la funzionalità, non il numero progressivo:
`iter/03-api-ricerca` è corretto, `iter/03-feature` non lo è.

---

## Passo 3 — Creazione del file di iterazione

Creare il file `docs/iterations/it-XX.md` copiando la struttura da
`docs/iterations/README.md` e compilando:

- i metadati (numero, branch, data inizio, dipendenze)
- l'obiettivo verificabile
- il piano (file da creare, file da modificare, rischi)

**Attendere l'approvazione esplicita dell'utente** prima di procedere al passo 4.

Se l'utente richiede modifiche al piano, aggiornarle nel file e ripresentarlo.
Non procedere con il codice finché il piano non è approvato.

---

## Passo 4 — Implementazione

Effettuare tutte le modifiche al codice descritte nel piano approvato.

Regole durante l'implementazione:

- Implementare esattamente ciò che è stato approvato, nulla di più.
- Se durante il lavoro emerge la necessità di una modifica non pianificata,
  segnalarla all'utente e attendere conferma prima di procedere.
- Aggiornare il file `it-XX.md` con i file effettivamente creati o modificati
  (potrebbero differire dal piano).
- Documentare nel file di iterazione le decisioni prese durante l'implementazione.

---

## Passo 5 — Verifica e commit

Al termine del codice, indicare all'utente esattamente come verificare
che la funzionalità funzioni:

- quali azioni compiere nell'app (percorso preciso, non generico)
- quali risultati attendersi per ogni azione
- quali casi limite testare e come

I casi da verificare sono quelli documentati in `docs/test-matrix.md` per questa
funzionalità. Se non sono ancora presenti, aggiungerli alla matrice prima di
procedere con i test.

Includere sempre almeno:

- il caso normale (happy path)
- il caso con input vuoto o assente
- il caso con errore di rete o dato non disponibile

Una volta che l'utente conferma il funzionamento, eseguire il commit:

```
git add [file specifici, mai git add .]
git commit -m "<tipo>(<scope>): <descrizione>"
```

### Verifica delle regressioni

Prima di procedere, eseguire tutti i test contrassegnati come `TC-REG-*` in
`docs/test-matrix.md` e aggiornarne l'esito. Indicare all'utente quali aree
testare in base alle modifiche apportate.

---

## Passo 6 — Gestione degli errori (ricorsivo)

Se durante la verifica qualcosa non funziona:

1. Identificare la causa del problema.
2. Documentare nel file `it-XX.md`, sezione "Problemi riscontrati":
   - descrizione del problema
   - causa identificata
   - impatto
3. Applicare la correzione.
4. Documentare la correzione nel file `it-XX.md`, sezione "Correzioni effettuate".
5. Tornare al **Passo 5** e ripetere la verifica completa.

Ripetere finché tutti i test, incluse le regressioni, producono l'esito atteso.
Non procedere al Passo 7 finché ci sono problemi aperti.

---

## Passo 7 — Definition of Done

Prima del merge, verificare che ogni punto della checklist sia soddisfatto:

- [ ] Il codice compila senza errori e senza warning non giustificati
- [ ] La funzionalità è testata su dispositivo o emulatore reale
- [ ] I casi limite sono stati verificati manualmente
- [ ] I tre stati UI (loading / errore / empty) sono gestiti dove applicabile
- [ ] Nessuna credenziale o dato sensibile è presente nel codice committato
- [ ] Il codice è stato letto e compreso dopo la generazione
- [ ] Nessuna regressione nelle funzionalità esistenti
- [ ] Il file `it-XX.md` riporta tutti i problemi e le correzioni avvenute

Se anche un solo punto non è soddisfatto, tornare al Passo 6 prima di procedere.

---

## Passo 8 — Merge su develop

Quando la Definition of Done è completamente soddisfatta:

```
git checkout develop
git merge --no-ff iter/XX-nome-feature
git branch -d iter/XX-nome-feature
```

Il flag `--no-ff` è obbligatorio: garantisce che i commit dell'iterazione restino
raggruppati nel log di `develop` come unità distinta.

---

## Passo 9 — Chiusura dell'iterazione

Completare il file `docs/iterations/it-XX.md`:

- compilare la sezione "Commit creati" con gli hash e i messaggi
- impostare la data di completamento nei metadati
- compilare la sezione "Esito" con: Completato / Parziale / Sospesa

Aggiornare gli altri file di documentazione coinvolti:

- `docs/test-matrix.md` — aggiungere i nuovi casi di test alla sezione della funzionalità e aggiornare lo storico degli esiti
- `docs/changelog.md` — aggiungere le modifiche rilevanti nella sezione [Non rilasciato]
- `docs/architecture.md` — se è stata presa una decisione architetturale rilevante
- `docs/api-notes.md` — se è stata integrata o modificata una API esterna
- `docs/spec.md` — solo se lo scope è cambiato (con motivazione esplicita)
- `docs/plan.md` — se il piano delle iterazioni successive è stato rivisto

Eseguire il commit di documentazione sul branch `develop`:

```
git add docs/
git commit -m "docs: aggiornata documentazione iterazione XX"
```

---

## Al momento del rilascio su main

Quando si promuove `develop` su `main`, aggiornare `docs/changelog.md`:

1. Rinominare la sezione `[Non rilasciato]` con il numero di versione e la data:
   ```
   ## [1.0.0] — AAAA-MM-GG
   ```
2. Aggiungere una nuova sezione `[Non rilasciato]` vuota in cima.
3. Committare su `develop` prima del merge:
   ```
   git add docs/changelog.md
   git commit -m "docs: release changelog v1.0.0"
   ```
