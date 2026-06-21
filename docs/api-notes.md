# Note sulle API esterne

<!-- Questo documento va compilato per ogni API esterna integrata nel progetto.
     Documentare le API durante l'integrazione, non dopo: i dettagli si dimenticano.
     Ogni sezione contrassegnata con [DA COMPILARE] è obbligatoria prima
     di considerare l'integrazione completa. -->

---

## API: [Nome dell'API]

### Informazioni generali

| Campo | Valore |
|-------|--------|
| Nome ufficiale | [Nome completo del servizio] |
| URL base | `https://[dominio-api]/[versione]/` |
| Documentazione ufficiale | [URL della documentazione] |
| Versione API usata | [es. v1, v2, 2024-01] |
| Tipo di API | [REST / GraphQL / gRPC / WebSocket] |
| Formato risposta | [JSON / XML / protobuf] |

---

### Autenticazione

<!-- Documentare il meccanismo di autenticazione in modo preciso.
     Indicare dove va posizionato il token/chiave nella richiesta. -->

- **Tipo**: [Nessuna / API Key / Bearer Token / OAuth2 / Basic Auth]
- **Posizione**: [Header `Authorization: Bearer {token}` / Header `X-Api-Key: {key}` / Query param `?api_key={key}`]
- **Scadenza token**: [Non scade / Scade ogni X ore / Refresh token disponibile]
- **Come ottenere le credenziali**: [URL della dashboard / procedura di registrazione]
- **Dove sono salvate nel progetto**: [variabile d'ambiente / file escluso da git — mai nel codice]

**Regola obbligatoria**: nessuna credenziale deve apparire nel codice sorgente o nei
file committati. Usare variabili d'ambiente o file locali esclusi da `.gitignore`.

---

### Endpoint utilizzati

<!-- Documentare solo gli endpoint effettivamente usati nel progetto.
     Per ogni endpoint: metodo, path, scopo, parametri, risposta attesa. -->

#### [GET / POST / ...] `[/path/endpoint]` — [Scopo sintetico]

**Parametri richiesta**:

| Nome | In | Tipo | Obbligatorio | Descrizione |
|------|----|------|:------------:|-------------|
| `[nome]` | [query / path / body / header] | [string / int / bool] | Sì / No | [cosa rappresenta] |
| `[nome]` | [...] | [...] | [...] | [...] |

**Esempio di richiesta**:
```http
GET /[path]?param1=valore&param2=valore
Authorization: Bearer {token}
```

**Risposta di successo** (`200 OK`):
```json
{
  "[campo]": "[tipo e descrizione]",
  "[lista]": [
    {
      "[campo]": "[tipo]",
      "[campo]": "[tipo]"
    }
  ],
  "[paginazione]": {
    "[page]": 1,
    "[total]": 42
  }
}
```

**Campi della risposta usati nel progetto**:

| Campo | Tipo | Usato per | Obbligatorio nella risposta |
|-------|------|-----------|:--------------------------:|
| `[campo]` | string | [es. titolo da mostrare in lista] | Sì |
| `[campo]` | string | [es. URL immagine] | No (può essere null) |

**Risposte di errore note**:

| Codice | Condizione | Gestione implementata |
|--------|-----------|----------------------|
| 400 | Parametro mancante o non valido | Mostrare messaggio errore, non riprovare |
| 401 | Token mancante o non valido | Richiedere nuova autenticazione |
| 404 | Risorsa non trovata | Mostrare stato "non trovato" |
| 429 | Rate limit superato | Attendere X secondi, poi riprovare |
| 500 | Errore server | Messaggio generico + pulsante riprova |

---

*(Ripetere la sezione endpoint per ogni endpoint integrato)*

---

### Limiti e vincoli

<!-- I limiti non documentati diventano bug in produzione.
     Documentare ogni limite noto, anche se non ancora raggiunto. -->

| Limite | Valore | Conseguenza se superato | Strategia adottata |
|--------|--------|------------------------|-------------------|
| Rate limit | [X req/min o req/giorno] | Risposta 429 | [Cache locale, delay tra chiamate] |
| Dimensione risposta | [max N elementi per pagina] | Risposta troncata | [Paginazione implementata] |
| Quota giornaliera | [X chiamate/giorno] | Blocco accesso | [Mock per sviluppo, chiamate limitate] |
| Timeout risposta | [X secondi attesi] | Connessione lasciata aperta | [Timeout configurato lato client] |
| Dimensione payload | [max X KB] | Errore 413 | [Limitare dimensione input] |

---

### Gestione della paginazione

<!-- Se l'API supporta la paginazione, documentare esattamente il meccanismo.
     Una paginazione non documentata porta a risultati incompleti silenziosamente. -->

- **Supportata**: [Sì / No]
- **Meccanismo**: [offset+limit / page+size / cursor / token di continuazione]
- **Parametri richiesta**: `[page=N]` + `[size=N]` (o equivalente)
- **Informazioni di paginazione nella risposta**: `[total_results]`, `[page]`, `[total_pages]`
- **Comportamento al termine dei risultati**: [lista vuota / campo `has_more: false` / altro]
- **Implementazione nell'app**: [infinite scroll / load more button / navigazione pagine]

---

### Comportamento in caso di errori di rete

<!-- Documentare la strategia di retry adottata.
     Una strategia di retry non documentata porta a comportamenti inconsistenti. -->

| Scenario | Comportamento adottato |
|----------|----------------------|
| Nessuna connessione | Mostrare errore immediato, non tentare retry |
| Timeout (> X secondi) | Mostrare errore, offrire pulsante "Riprova" |
| Errore 5xx | Retry automatico dopo [X] secondi, massimo [N] tentativi |
| Errore 429 | Attendere [X] secondi (come da header `Retry-After`), poi riprovare |
| Errore 4xx (escluso 429) | Nessun retry, mostrare errore specifico |

---

### Dati mock per sviluppo offline

<!-- I dati mock devono rispecchiare esattamente la struttura della risposta reale.
     Un mock che non corrisponde alla struttura reale nasconde i bug di parsing. -->

- **Percorso file mock**: `[path relativo nella cartella del progetto]`
- **Struttura**: identica alla risposta API reale (verificata su [data])
- **Come attivare il mock**: [variabile d'ambiente / flag di build / commento nel codice]
- **Casi coperti dal mock**:
  - [ ] Risposta con dati normali (lista piena)
  - [ ] Risposta con lista vuota
  - [ ] Risposta con dati parziali (campi opzionali assenti)
  - [ ] Risposta di errore (es. 404, 500)

---

### Problemi riscontrati

<!-- Documentare ogni problema incontrato durante l'integrazione,
     anche quelli risolti. Questa sezione è memoria storica del progetto. -->

#### [Data] — [Titolo breve del problema]

- **Descrizione**: [cosa è successo]
- **Causa**: [perché è successo]
- **Soluzione / workaround**: [come è stato risolto]
- **Impatto**: [quanto ha ritardato lo sviluppo o influenzato il comportamento]

---

### Changelog dell'integrazione

<!-- Tracciare le modifiche significative all'integrazione con questa API. -->

| Data | Modifica | Motivazione |
|------|---------|-------------|
| [GG/MM/AAAA] | Prima integrazione | Implementazione Iterazione 3 |
| [GG/MM/AAAA] | [Aggiunto endpoint X] | [Funzionalità Y richiesta da spec] |
| [GG/MM/AAAA] | [Modificato parsing campo Z] | [Struttura risposta diversa da attesa] |

---

## Linee guida generali per l'integrazione di API

<!-- Queste regole si applicano a qualsiasi API integrata nel progetto. -->

### Prima dell'integrazione

1. Leggere la documentazione ufficiale completa, non solo gli esempi.
2. Testare ogni endpoint con un client HTTP (es. Postman, curl, Insomnia) prima di scrivere codice.
3. Verificare che la struttura della risposta corrisponda a quanto documentato.
4. Controllare i limiti di rate e quota e confrontarli con l'uso previsto.
5. Documentare l'autenticazione in questo file prima di procedere.

### Durante l'integrazione

1. Creare il DTO di risposta a partire da una risposta reale, non dalla documentazione.
2. Rendere opzionali tutti i campi che potrebbero essere assenti nella risposta reale.
3. Gestire esplicitamente ogni codice di errore HTTP documentato.
4. Configurare un timeout lato client (mai lasciare la connessione aperta indefinitamente).
5. Non loggare mai il contenuto completo delle risposte se contiene dati sensibili.

### Dopo l'integrazione

1. Aggiornare questo file con i problemi riscontrati e le soluzioni adottate.
2. Verificare il comportamento con rete assente, timeout e risposte di errore.
3. Creare dati mock che coprono almeno i casi: lista piena, lista vuota, errore.
4. Documentare la struttura dei dati mock in questo file.
