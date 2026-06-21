# Matrice dei test

Questo file raccoglie tutti i casi di test manuali del progetto, organizzati
per area funzionale. Va aggiornato ogni volta che viene aggiunta o modificata
una funzionalità.

I test qui documentati sono il riferimento per la verifica al termine di ogni
iterazione e per il controllo delle regressioni nelle iterazioni successive.

---

## Convenzioni

**ID test**: `TC-[AREA]-[numero]`
- `TC-F1-01` = primo test della funzionalità F1
- `TC-CL-01` = primo test di un caso limite (cross-feature)
- `TC-REG-01` = test di regressione

**Esito**:
- ✅ Superato
- ❌ Fallito
- ⏭ Saltato (motivare)
- 🔄 Da eseguire

---

## [Area: F1 — Nome funzionalità]

<!-- Creare una sezione per ogni funzionalità obbligatoria.
     Copiare il blocco e rinominare l'area.
     Aggiungere righe alla tabella per ogni nuovo caso di test. -->

| ID | Descrizione | Precondizioni | Passi | Risultato atteso | Esito | Note |
|----|-------------|--------------|-------|-----------------|-------|------|
| TC-F1-01 | [Caso normale / happy path] | [stato iniziale] | [1. azione 2. azione] | [cosa deve succedere] | 🔄 | |
| TC-F1-02 | [Variante o caso alternativo] | [stato iniziale] | [passi] | [risultato atteso] | 🔄 | |

---

## [Area: F2 — Nome funzionalità]

| ID | Descrizione | Precondizioni | Passi | Risultato atteso | Esito | Note |
|----|-------------|--------------|-------|-----------------|-------|------|
| TC-F2-01 | [Caso normale] | [stato iniziale] | [passi] | [risultato atteso] | 🔄 | |

---

## Casi limite (cross-feature)

<!-- Scenari che coinvolgono più funzionalità o che testano i confini del sistema.
     Questi test vanno eseguiti dopo ogni iterazione, non solo quella di riferimento. -->

| ID | Descrizione | Area coinvolta | Passi | Risultato atteso | Esito | Note |
|----|-------------|---------------|-------|-----------------|-------|------|
| TC-CL-01 | Input vuoto o con soli spazi | [F1, F2] | [passi] | [messaggio di errore / blocco] | 🔄 | |
| TC-CL-02 | Nessuna connessione di rete | [F1, F3] | [disabilitare rete, eseguire azione] | [errore visibile, nessun crash] | 🔄 | |
| TC-CL-03 | Risposta API con errore (5xx) | [F1] | [simulare errore, eseguire azione] | [messaggio errore, pulsante riprova] | 🔄 | |
| TC-CL-04 | Risposta API con lista vuota | [F1, F2] | [ricerca senza risultati] | [stato empty visibile] | 🔄 | |
| TC-CL-05 | Stessa azione eseguita più volte rapidamente | [F1] | [tap ripetuto su azione] | [nessun comportamento duplicato] | 🔄 | |
| TC-CL-06 | Ritorno in foreground dopo lunga inattività | [tutti] | [mettere in background, attendere, riaprire] | [stato coerente, nessun crash] | 🔄 | |

---

## Test di regressione

<!-- Questo elenco cresce ad ogni iterazione.
     Dopo ogni iterazione, eseguire tutti i test di regressione per verificare
     che le funzionalità precedenti non siano state rotte.
     Aggiungere una riga per ogni funzionalità completata nelle iterazioni passate. -->

| ID | Funzionalità verificata | Introdotta in | Esito ultimo controllo | Data | Note |
|----|------------------------|--------------|----------------------|------|------|
| TC-REG-01 | [es. La schermata principale si carica] | it-01 | 🔄 | | |
| TC-REG-02 | [es. La ricerca restituisce risultati] | it-03 | 🔄 | | |

---

## Storico degli esiti per iterazione

<!-- Tracciare quale iterazione ha eseguito quali test, con l'esito complessivo.
     Questo permette di vedere a colpo d'occhio quando un test ha iniziato a fallire. -->

| Iterazione | Test eseguiti | Superati | Falliti | Saltati | Note |
|-----------|--------------|---------|---------|---------|------|
| it-01 | | | | | |
| it-02 | | | | | |
| it-03 | | | | | |
