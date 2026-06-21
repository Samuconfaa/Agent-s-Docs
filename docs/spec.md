# Specifica del progetto

## Titolo del progetto

<!-- Scegliere un nome sintetico, significativo e non generico.
     Il titolo deve rispecchiare lo scopo principale dell'applicazione. -->

[Nome dell'applicazione]

---

## Descrizione sintetica

<!-- Massimo 3-4 righe. Rispondere a: cosa fa l'app, per chi, quale valore offre.
     Non descrivere la tecnologia, descrivere il prodotto. -->

[Cosa fa l'app e quale problema risolve, in linguaggio orientato all'utente]

---

## Utente target

<!-- Essere specifici. "Tutti" non è un utente target accettabile.
     Indicare almeno: fascia d'età approssimativa, contesto d'uso, livello di
     alfabetizzazione digitale, frequenza d'uso prevista. -->

- **Chi**: [tipologia di utente, es. studenti universitari, professionisti freelance]
- **Contesto d'uso**: [dove e quando usa l'app, es. in mobilità, a casa, al lavoro]
- **Obiettivo principale**: [cosa vuole ottenere con una singola sessione d'uso]
- **Livello tecnico**: [principiante / intermedio / avanzato]
- **Frequenza d'uso prevista**: [giornaliera / settimanale / occasionale]

---

## Problema affrontato

<!-- Descrivere il bisogno concreto, non la soluzione.
     Rispondere alla domanda: "Perché un utente userebbe questa app invece di
     fare la stessa cosa in modo diverso?"
     Includere il contesto attuale (come si risolve il problema oggi) e
     perché quella soluzione è insufficiente. -->

[Descrizione del problema reale dell'utente e del perché le soluzioni attuali sono inadeguate]

---

## Obiettivi del progetto

<!-- Gli obiettivi devono essere misurabili o almeno verificabili.
     Distinguere tra obiettivi del prodotto (cosa deve fare l'app)
     e obiettivi didattici/tecnici (cosa si vuole imparare o dimostrare). -->

### Obiettivi di prodotto

- **O1**: [Obiettivo verificabile — descrivere il risultato, non il mezzo]
- **O2**: [...]
- **O3**: [...]

### Obiettivi tecnici o didattici (se applicabile)

- **OT1**: [es. applicare il pattern di separazione tra logica e presentazione]
- **OT2**: [...]

---

## Funzionalità obbligatorie

<!-- Per ogni funzionalità indicare:
     - cosa fa (dal punto di vista dell'utente, non dell'implementazione)
     - perché è obbligatoria (collega a un obiettivo)
     - input e output attesi in modo sintetico
     Non usare termini tecnici in questa sezione. -->

| ID  | Funzionalità | Collegata a | Input richiesto | Output atteso |
|-----|-------------|-------------|-----------------|---------------|
| F1  | [Ricerca contenuti] | O1 | [testo inserito dall'utente] | [lista risultati] |
| F2  | [Visualizzazione risultati] | O1 | [selezione dalla lista] | [schermata dettaglio] |
| F3  | [Salvataggio locale] | O2 | [azione dell'utente] | [dato persistito] |
| F4  | [Gestione stati UI] | OT1 | [operazione asincrona] | [feedback visivo] |

---

## Funzionalità opzionali

<!-- Da implementare solo se le funzionalità obbligatorie sono complete e stabili.
     Indicare la priorità (alta/media/bassa) e i prerequisiti. -->

| ID   | Funzionalità | Priorità | Prerequisito |
|------|-------------|---------|--------------|
| FO1  | [Filtri avanzati] | Media | F1 completata |
| FO2  | [Cronologia ricerche] | Bassa | F1 completata |
| FO3  | [Modalità offline / cache] | Alta | F3 completata |
| FO4  | [Condivisione contenuti] | Bassa | F2 completata |
| FO5  | [Personalizzazione visiva] | Bassa | nessuno |

---

## Requisiti non funzionali

<!-- Questi requisiti non descrivono cosa fa l'app ma come si comporta.
     Devono essere verificabili. Evitare affermazioni vaghe come "deve essere veloce". -->

### Prestazioni

- Il tempo di risposta dell'interfaccia a qualsiasi azione dell'utente deve essere
  inferiore a 100ms (escluso il caricamento dati remoti).
- Le operazioni di rete non devono mai bloccare il thread principale.
- Il caricamento iniziale dell'app deve avvenire entro 3 secondi su hardware target.

### Affidabilità

- Qualsiasi errore (rete, parsing, persistenza) deve essere intercettato
  e comunicato all'utente in linguaggio comprensibile.
- Nessun crash silenzioso: ogni eccezione non gestita deve essere tracciata.
- In caso di errore, i dati già caricati devono rimanere visibili se disponibili.

### Usabilità

- L'interfaccia deve essere utilizzabile con una sola mano (se app mobile).
- I testi devono essere leggibili senza zoom su dispositivi di dimensione target.
- Ogni azione dell'utente deve produrre un feedback visivo immediato.
- Gli errori devono essere accompagnati da un'azione correttiva suggerita.

### Manutenibilità

- Il codice deve essere leggibile e comprensibile da chi lo ha scritto dopo 30 giorni.
- Ogni componente deve avere responsabilità unica e delimitata.
- Nessun blocco di logica deve essere duplicato in più punti.

### Sicurezza

- Nessuna credenziale (chiavi API, password) deve essere inclusa nel codice sorgente.
- Tutti gli input dell'utente devono essere validati prima dell'uso.
- I dati locali sensibili devono essere protetti con le API di sistema appropriate.

### Compatibilità

- [Specificare le versioni del sistema operativo target]
- [Specificare le dimensioni schermo target]
- [Specificare eventuali dipendenze hardware: fotocamera, GPS, ecc.]

---

## Schermate principali

<!-- Elencare ogni schermata prevista. Per ciascuna indicare:
     scopo, dati mostrati, azioni disponibili.
     Non descrivere l'aspetto visivo in questa sezione.
     Se la schermata non è ancora definita, segnarlo esplicitamente. -->

| Schermata | Scopo | Dati mostrati | Azioni possibili |
|-----------|-------|---------------|-----------------|
| [Home] | [pagina di ingresso] | [contenuti iniziali] | [navigare, cercare] |
| [Ricerca] | [trovare contenuti] | [lista risultati, contatore] | [filtrare, selezionare] |
| [Dettaglio] | [informazioni complete] | [dati estesi dell'elemento] | [salvare, condividere] |
| [Preferiti] | [contenuti salvati] | [lista elementi salvati] | [rimuovere, aprire] |
| [Impostazioni] | [configurazione] | [preferenze attuali] | [modificare, ripristinare] |

---

## Flussi di navigazione

<!-- Descrivere esplicitamente come l'utente si muove tra le schermate.
     Indicare: punto di ingresso principale, percorsi critici, come si torna indietro.
     Un flusso di navigazione ambiguo è fonte di bug e UX scadente. -->

### Struttura principale

[Descrivere se la navigazione è a tab, a menu laterale, gerarchica o mista]

### Percorso principale (happy path)

[Schermata A] → [azione utente] → [Schermata B] → [azione utente] → [risultato]

### Navigazione verso schermate di dettaglio

[Descrivere come vengono passati i dati tra schermate, es. identificativo,
oggetto completo, parametri di query]

### Gestione del tasto/gesto "indietro"

[Descrivere il comportamento atteso in ogni punto della navigazione]

---

## Integrazioni esterne

<!-- Elencare ogni dipendenza da sistemi esterni (API, servizi, SDK).
     Per ciascuna indicare il livello di criticità: se indisponibile, l'app
     funziona parzialmente o non funziona affatto? -->

| Integrazione | Scopo | Criticità | Alternativa se non disponibile |
|-------------|-------|-----------|-------------------------------|
| [Nome API] | [cosa fornisce] | Alta / Media / Bassa | [mock locale / funzione degradata] |

---

## Dati locali

<!-- Elencare ogni tipo di dato che l'app salva localmente.
     Per ciascuno indicare: cosa è, perché viene salvato, per quanto tempo
     e cosa succede se viene perso. -->

| Dato | Scopo | Durata prevista | Impatto se perso |
|------|-------|----------------|-----------------|
| [Preferiti] | [accesso rapido] | [permanente] | [l'utente li perde, recuperabili] |
| [Impostazioni] | [personalizzazione] | [permanente] | [ripristino valori default] |
| [Cache dati] | [uso offline] | [limitata, es. 24h] | [necessaria riconnessione] |
| [Cronologia] | [accesso recente] | [limitata, es. 30 elementi] | [nessun impatto critico] |

---

## Permessi richiesti

<!-- Elencare solo i permessi strettamente necessari.
     Per ciascuno indicare il motivo specifico e cosa succede se negato.
     Un permesso senza motivazione chiara è un permesso da rimuovere. -->

| Permesso | Motivazione | Comportamento se negato |
|---------|-------------|------------------------|
| [Accesso rete] | [chiamate API] | [app non funzionante senza connessione] |
| [Fotocamera] | [solo se usata] | [funzione X non disponibile] |
| [Posizione] | [solo se usata] | [funzione Y disabilitata] |

---

## Vincoli di progetto

<!-- Vincoli reali che influenzano le decisioni tecniche e di scope.
     Un vincolo non dichiarato diventa un rischio nascosto. -->

- **Tempo disponibile**: [X settimane / ore]
- **Complessità massima**: [descrivere i limiti accettati, es. no backend custom, no autenticazione utente]
- **Risorse esterne**: [budget API, licenze, account di test]
- **Limitazioni del team**: [numero di sviluppatori, competenze disponibili]
- **Limitazioni tecniche**: [es. no accesso a certi servizi, politiche aziendali]

---

## Criteri di accettazione

<!-- Per ogni funzionalità obbligatoria definire un test in forma BDD (Dato/Quando/Allora).
     I criteri di accettazione sono la definizione formale del "fatto".
     Senza criteri espliciti non è possibile verificare il completamento. -->

### F1 — [Nome funzionalità]

- **Dato** che [stato iniziale del sistema]
- **Quando** [azione specifica dell'utente]
- **Allora** [risultato verificabile e preciso]

### F2 — [Nome funzionalità]

- **Dato** che [...]
- **Quando** [...]
- **Allora** [...]

*(Ripetere per ogni funzionalità obbligatoria)*

---

## Casi limite da gestire obbligatoriamente

<!-- Questi scenari devono essere testati esplicitamente, non ignorati.
     Se un caso limite non viene gestito, deve essere documentato come
     comportamento noto e accettato, non come omissione. -->

### Input

- [ ] Campo di ricerca vuoto o con soli spazi
- [ ] Input con caratteri speciali o molto lungo (>500 caratteri)
- [ ] Stessa operazione eseguita più volte rapidamente (double-tap, doppio invio)

### Rete

- [ ] Nessuna connessione al momento della richiesta
- [ ] Connessione presente ma molto lenta (timeout)
- [ ] Risposta API con codice di errore HTTP (4xx, 5xx)
- [ ] Risposta API con JSON malformato o struttura inattesa
- [ ] Perdita di connessione durante una richiesta in corso

### Dati locali

- [ ] Storage locale pieno
- [ ] Tentativo di salvare un elemento già presente
- [ ] Tentativo di eliminare un elemento non esistente
- [ ] Corruzione del database locale (primo avvio dopo aggiornamento)

### Stato dell'app

- [ ] Ritorno in foreground dopo lunga inattività
- [ ] Interruzione da chiamata o notifica di sistema durante un'operazione
- [ ] Rotazione schermo durante un caricamento in corso

---

## Rischi principali

<!-- Identificare i rischi prima di iniziare, non durante lo sviluppo.
     Per ciascuno indicare probabilità, impatto e strategia di mitigazione. -->

| ID  | Rischio | Prob. | Impatto | Mitigazione |
|-----|---------|-------|---------|-------------|
| R1  | [API non disponibile durante lo sviluppo] | Media | Alto | [Preparare dati mock locali] |
| R2  | [Rate limit troppo restrittivo per i test] | Alta | Medio | [Implementare cache, limitare chiamate] |
| R3  | [Struttura JSON diversa dalla documentazione] | Media | Alto | [Validare con strumenti prima dell'integrazione] |
| R4  | [Scope creep: aggiunta di funzionalità non pianificate] | Alta | Alto | [Bloccare le modifiche allo scope dopo la specifica] |
| R5  | [Tempi insufficienti per rifinitura] | Alta | Medio | [Definire MVP minimo non negoziabile] |

---

## Versione MVP

<!-- Descrivere con precisione il sottoinsieme minimo che costituisce
     una consegna accettabile. Il MVP non è "l'app incompleta",
     è l'app completa con scope ridotto.
     Deve essere funzionante, stabile e senza stati non gestiti. -->

L'applicazione è considerata consegnabile quando:

1. [Funzionalità F1] funziona correttamente su hardware target
2. [Funzionalità F2] funziona correttamente su hardware target
3. [Funzionalità F3] funziona correttamente su hardware target
4. Tutti i casi limite delle funzionalità MVP sono gestiti
5. Nessun crash riproducibile è presente
6. La documentazione minima è aggiornata

Le funzionalità opzionali [FO1, FO2, ...] possono essere assenti nel MVP.
