# IA Project Template

Template di documentazione per progetti software sviluppati con assistenza AI.

## A cosa serve

Fornisce un insieme di linee guida e file strutturati da copiare all'inizio di ogni
nuovo progetto. L'obiettivo è guidare l'agente AI verso uno sviluppo controllato,
iterativo e documentato, indipendentemente dal linguaggio o dal framework scelto.

## Contenuto

| File | Scopo |
|------|-------|
| `CLAUDE.md` | Regole operative per l'AI: comportamento, stile, git, workflow |
| `docs/spec.md` | Template per la specifica del progetto |
| `docs/plan.md` | Template per il piano di lavoro e le iterazioni |
| `docs/architecture.md` | Template per le decisioni architetturali |
| `docs/api-notes.md` | Template per documentare le API esterne integrate |
| `docs/iteration-workflow.md` | Processo passo-passo da seguire per ogni iterazione |
| `docs/iterations/README.md` | Template per il log di ogni singola iterazione |

## Come si usa

1. Copiare l'intera cartella come base del nuovo progetto.
2. Compilare `CLAUDE.md` con il contesto e le scelte tecniche del progetto.
3. Compilare `docs/spec.md` con i requisiti prima di scrivere codice.
4. Compilare `docs/plan.md` con le iterazioni previste.
5. Per ogni iterazione, seguire il processo in `docs/iteration-workflow.md`
   e creare un file `docs/iterations/it-XX.md` a partire dal template in
   `docs/iterations/README.md`.
