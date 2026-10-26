---
reviewDomain: requirements
reviewRound: 1
evidenceDigest: aa0a318cea0a6209d6d5c449caa8f41e6ddd44924a275289d37f245d5c23b7d0
evidenceRefs:
  - work
  - design-description
  - analysis:task-managment-backend-21c6dc4a
  - analysis:task-managment-frontend-8577187c
  - clarification:15ef4e45-31a4-4e93-8d66-63bdcdfe7969
  - clarification:9970c26d-d463-4f30-87b0-4449d9a5ea8a
  - clarification:250d30b1-5b0e-4478-8a06-ac8db516bc7f
  - clarification:4da29b06-1b37-43e7-a898-8e2d9eb5d71c
  - repositories
  - review:working-documents
blockedQuestionIds: []
reviewStatus: ready
---

# Analisi funzionale — TASK MANAGMENT - 3

## Documento, fonti e modifiche

Questa è l’Analisi Funzionale (AFU) del Work `0f6def3a-0a64-4361-87ee-654c2a109562`, per la review round 1. Le fonti funzionali principali sono `work` e `design-description`; le analisi `analysis:task-managment-frontend-8577187c` e `analysis:task-managment-backend-21c6dc4a` contribuiscono le conclusioni di feasibility. Le decisioni umane successive sono conservate con le rispettive identità: `clarification:15ef4e45-31a4-4e93-8d66-63bdcdfe7969`, `clarification:9970c26d-d463-4f30-87b0-4449d9a5ea8a`, `clarification:250d30b1-5b0e-4478-8a06-ac8db516bc7f` e `clarification:4da29b06-1b37-43e7-a898-8e2d9eb5d71c` (tutte accettate).

`review:working-documents` indicava che questo file AFU era mancante senza recovery. La review frontend disponibile nell’inventario è di un digest precedente; è stata riletta come supporto e aggiornata concettualmente con la quarta chiarificazione. La review backend non era presente nell’inventario; per lo stato dei repository si usano le due analisi repository indicizzate. Non è disponibile un AFU precedente da cui ereditare identità. Il registro provenance di questo documento contiene le origini elemento per elemento.

**[AFU-REQ-001](#provenance-AFU-REQ-001)** — Il prodotto consente agli studenti di seguire attività formative, consegnare il lavoro e comunicare con i mentor; i mentor verificano le consegne degli studenti loro assegnati. [Fonte: `work`, `description > OBIETTIVO E REQUISITI`]

## Obiettivi e ambito

**[AFU-REQ-002](#provenance-AFU-REQ-002)** — L’esperienza comprende dashboard/home, elenco e dettaglio attività, elenco mentor, messaggi, notifiche e impostazioni rappresentati dal Figma, con riferimento visivo per desktop e mobile. Le principali composizioni sono barra di navigazione laterale e aree affiancate su desktop, navigazione compatta e contenuti impilati su mobile. [Fonti: `work`, `description > Ambito`; `design-description`, §§466–472]

Il Work richiede la pianificazione delle modifiche necessarie, usando il testo come autorità per le regole di business e il Figma come riferimento per schermate e controlli. Non sono richieste API o scelte di stack. I repository forniti sono evidenza dello stato attuale, non fonti di nuovi requisiti. Le varianti con nomi, date e numeri diversi nei render sono contenuti d’esempio, non valori di prodotto (`design-description`, §§472, 484).

Non è definito un ruolo amministrativo né un flusso per creare o assegnare i mentor. L’assegnazione è una relazione necessaria per autorizzare le attività di revisione, ma le fonti non richiedono un’interfaccia d’amministrazione. Le icone telefono/video nel design non costituiscono da sole un requisito d’integrazione telefonica o video.

## Attori, ruoli e permessi

**[AFU-RULE-001](#provenance-AFU-RULE-001)** — Uno studente può consultare solo le proprie attività e conversazioni. La stessa restrizione vale per un accesso diretto a una risorsa e non dipende dal fatto che l’interfaccia nasconda o mostri un collegamento. [Fonte: `work`, `Regole di business > 1. Visibilità e permessi`]

**[AFU-RULE-002](#provenance-AFU-RULE-002)** — Un mentor può consultare solo gli studenti assegnati e le relative attività. Solo il mentor assegnato può valutare la consegna di quell’attività. La directory mentor non concede accesso alle attività degli altri studenti. Il controllo Follow/Followed non conferisce permessi né modifica l’assegnazione: oltre allo stato visibile, il suo effetto non è specificato e non va usato per ampliare l’accesso. [Fonti: `work`, `Regole di business > 1. Visibilità e permessi`; `design-description`, §§237–249, 480]

La distinzione degli attori è necessaria anche nel dettaglio: lo studente vede la propria consegna; il mentor assegnato vede e valuta la consegna dello studente assegnato. La vista condivisa dell’attività non rende intercambiabili le rispettive autorizzazioni (`clarification:15ef4e45-31a4-4e93-8d66-63bdcdfe7969`).

## Entità, dati e stati

**[AFU-RULE-003](#provenance-AFU-RULE-003)** — Un’attività può trovarsi in uno dei cinque stati: da iniziare, in corso, in revisione, da correggere o completata. Lo studente può iniziarla e inviarla in revisione; il mentor assegnato può completarla o richiedere correzioni. Una richiesta di correzione contiene una motivazione. Un’attività completata non è più modificabile dallo studente. [Fonte: `work`, `Regole di business > 2. Ciclo di vita delle attività`]

**[AFU-RULE-004](#provenance-AFU-RULE-004)** — Ogni invio accettato crea una nuova versione della consegna; le versioni precedenti restano consultabili. La puntualità è riferita alla versione al momento dell’invio: un invio tardivo è ammesso e deve essere indicato come tardivo, senza che una successiva valutazione ne cambi la puntualità. La valutazione è riferita a una versione precisa; valutare una versione superata non completa né modifica implicitamente una versione più recente. [Fonti: `work`, `Regole di business > 3. Consegne e scadenze`; `clarification:15ef4e45-31a4-4e93-8d66-63bdcdfe7969`]

**[AFU-RULE-005](#provenance-AFU-RULE-005)** — Per ciascun invio di consegna sono ammessi al massimo 5 file, con massimo 10 MiB per file e 25 MiB complessivi. I formati accettati sono PDF, DOCX, PPTX, XLSX, TXT, PNG e JPEG. Un file non supportato o oltre i limiti, oppure un caricamento annullato o interrotto, rifiuta l’intero invio: non crea una versione nuova, non altera quelle precedenti, mostra allo studente il motivo e consente di correggere e riprovare. Questi limiti si riferiscono agli invii di attività e non estendono implicitamente la semantica degli allegati dei messaggi. [Origine: `clarification:9970c26d-d463-4f30-87b0-4449d9a5ea8a`]

**[AFU-RULE-006](#provenance-AFU-RULE-006)** — Le notifiche in-app hanno uno stato di lettura proprio, separato dallo stato letto/non letto delle conversazioni. L’azione di lettura di un elemento cambia solo lo stato di quella notifica; leggere una conversazione cambia solo il suo stato. [Fonti: `work`, regola sullo stato di lettura notifiche/conversazioni; `clarification:250d30b1-5b0e-4478-8a06-ac8db516bc7f`]

**[AFU-RULE-007](#provenance-AFU-RULE-007)** — Le quattro preferenze Message, Task Update, Task Deadline e Mentor Help controllano solo l’invio email per categoria. Le notifiche in-app restano attive e disponibili nell’inbox, senza opt-out in-app per categoria; disattivare un’email non disattiva la corrispondente notifica in-app. [Fonti: `work`, regola sulle preferenze email e notifiche in-app; `clarification:4da29b06-1b37-43e7-a898-8e2d9eb5d71c`]

**[AFU-RULE-008](#provenance-AFU-RULE-008)** — Dashboard e riepiloghi rispettano la visibilità dell’attore: aggregati e attività elencate devono riferirsi al medesimo insieme autorizzato; un’attività in revisione non è completata e il completamento è conteggiato solo nello stato completata. [Fonti: `work`, regole di visibilità e ciclo di vita; `analysis:task-managment-backend-21c6dc4a`, §23; `analysis:task-managment-frontend-8577187c`, §24]

**[AFU-RULE-009](#provenance-AFU-RULE-009)** — Le conversazioni e i messaggi sono accessibili soltanto ai partecipanti autorizzati. Il design mostra ricerca, elenco contatti, anteprime e messaggi testuali/immagine; questi contenuti di esempio non attribuiscono un accesso ulteriore né definiscono una politica di consegna file per la messaggistica. [Fonti: `work`, `Regole di business > 1. Visibilità e permessi`; `design-description`, §§251–270]

L’entità di preferenza generale mostrata dal design comprende lingua, fuso orario e formato 12/24 ore. I valori disponibili e le regole di salvataggio non sono definiti dalle fonti e non modificano le regole di attività o autorizzazione (`design-description`, §§272–284, 367–375).

## Processi e funzionalità

### Consultare la dashboard e le attività

Lo studente consulta le proprie attività; il mentor consulta quelle degli studenti assegnati. Ricerca, categorie, ordinamento e navigazione non ampliano l’insieme autorizzato. La dashboard può mostrare attività, scadenze, calendario, mentor e riepiloghi coerenti con quel medesimo insieme; i numeri/date d’esempio non sono valori da copiare. Il conteggio “completate” usa lo stato completata, non in revisione (**[AFU-RULE-001](#provenance-AFU-RULE-001)**, **[AFU-RULE-002](#provenance-AFU-RULE-002)**, **[AFU-RULE-008](#provenance-AFU-RULE-008)**; `design-description`, §§195–221, 300–318, 479).

### Iniziare, inviare e correggere una consegna

Lo studente apre il dettaglio della propria attività e può iniziarla. Seleziona file conformi ai limiti di **[AFU-RULE-005](#provenance-AFU-RULE-005)** e invia la consegna per la revisione. Un invio accettato crea una versione, che mostra il proprio stato e la propria puntualità; se è tardivo resta accettato ma viene contrassegnato. Invio in revisione non equivale a completamento (**[AFU-RULE-003](#provenance-AFU-RULE-003)**, **[AFU-RULE-004](#provenance-AFU-RULE-004)**).

Se un formato non è ammesso, un limite è superato o il caricamento viene annullato/interrotto, l’intera operazione è rifiutata: nessuna versione nuova, nessuna modifica delle precedenti, motivo visibile e retry possibile. Lo stato visibile non deve suggerire che la consegna sia riuscita (**[AFU-RULE-005](#provenance-AFU-RULE-005)**).

### Valutare una consegna

Il mentor assegnato seleziona la versione da valutare. Può completare l’attività oppure chiedere correzioni inserendo una motivazione. Se la versione è superata, il sistema rende esplicito l’esito e non presenta la valutazione come completamento di una versione più recente. Quando l’attività è completata, lo studente la vede come non modificabile (**[AFU-RULE-002](#provenance-AFU-RULE-002)**, **[AFU-RULE-003](#provenance-AFU-RULE-003)**, **[AFU-RULE-004](#provenance-AFU-RULE-004)**).

### Comunicare e leggere le notifiche

I partecipanti autorizzati trovano una conversazione, consultano lo storico e possono comporre/inviare un messaggio; la vista può mostrare allegati immagine come nel design. Il design presenta anche simboli rosso/blu di lettura nella lista, ma non ne specifica la legenda: non devono confondere lo stato della conversazione con quello della notifica (**[AFU-RULE-001](#provenance-AFU-RULE-001)**, **[AFU-RULE-009](#provenance-AFU-RULE-009)**; `design-description`, §§251–270, 481).

La campanella apre un elenco in-app. Il badge mostra il numero delle notifiche non lette; ciascuna notifica offre l’azione esplicita «Segna come letta». Usarla aggiorna solo la notifica selezionata; leggere una conversazione aggiorna solo lo stato della conversazione. Pagina, pannello o altra disposizione responsive possono seguire il design (**[AFU-RULE-006](#provenance-AFU-RULE-006)**; `clarification:250d30b1-5b0e-4478-8a06-ac8db516bc7f`).

**[AFU-AC-001](#provenance-AFU-AC-001)** — Per gli eventi di invio, richiesta di correzioni e completamento, i destinatari coinvolti ricevono la notifica in-app richiesta dal Work. Le preferenze email determinano soltanto se viene inviata anche l’email corrispondente. Un eventuale errore del canale email non deve presentare come fallita né annullare un invio o una valutazione già accettati. [Fonti: `work`, regole su notifiche ed email; `analysis:task-managment-backend-21c6dc4a`, §24; `analysis:task-managment-frontend-8577187c`, §§27, 36]

### Modificare le preferenze

**[AFU-AC-002](#provenance-AFU-AC-002)** — Nella sezione Notification, ciascuno dei quattro toggle salva la preferenza email della propria categoria. Dopo la disattivazione di una categoria, le relative email non vengono inviate, mentre le notifiche in-app restano nell’inbox e seguono il proprio stato di lettura. Etichettare la sezione/toggle come preferenza email chiarisce il canale; non si aggiungono opt-out in-app per categoria (**[AFU-RULE-007](#provenance-AFU-RULE-007)**; `design-description`, §§286–298).

Le impostazioni generali mostrano lingua, fuso orario, formato orario e Salva modifiche. La schermata visualizza i campi ma non prescrive opzioni, valori predefiniti o dettagli di conferma/errore del salvataggio (`design-description`, §§272–284, 367–375).

## Schermate e interazioni

| Schermata / contesto | Informazioni e controlli | Comportamento richiesto |
| --- | --- | --- |
| Dashboard, desktop e mobile | Attività in corso, riepiloghi, grafico, mentor, scadenze/calendario e accesso al dettaglio (`design-description`, §§195–207, 300–308). | Dati limitati all’attore; non trattare esempi numerici/date come valori prescritti (**[AFU-RULE-001](#provenance-AFU-RULE-001)**, **[AFU-RULE-008](#provenance-AFU-RULE-008)**). |
| Elenco attività | Ricerca, categoria, ordinamento e schede attività (`design-description`, §§209–221, 310–318). | Filtri e navigazione non ampliano l’insieme autorizzato (**[AFU-RULE-001](#provenance-AFU-RULE-001)**). |
| Dettaglio attività | Contenuti/criteri, dettagli assegnazione, area upload e azione generica Submit (`design-description`, §§223–235, 320–332, 409–420). | Presentare flussi separati per studente e mentor assegnato, con consegna/versioni, stato, azioni e feedback espliciti descritti in **[AFU-AC-003](#provenance-AFU-AC-003)** e **[AFU-AC-004](#provenance-AFU-AC-004)**. |
| Directory mentor | Ricerca, categorie, ordinamento, card, Follow/Followed (`design-description`, §§237–249, 334–346). | La directory non attribuisce accesso alle attività di altri studenti (**[AFU-RULE-002](#provenance-AFU-RULE-002)**). |
| Messaggi e conversazione | Contatti, anteprime, marker di lettura, storico testuale/immagine, composer e allegato (`design-description`, §§251–270, 348–365). | Consultazione per partecipanti; non confondere marker di conversazione e stato notifica (**[AFU-RULE-001](#provenance-AFU-RULE-001)**, **[AFU-RULE-006](#provenance-AFU-RULE-006)**, **[AFU-RULE-009](#provenance-AFU-RULE-009)**). |
| Inbox notifiche | Campanella e badge nel dashboard; elenco con stato per singolo elemento e azione esplicita di lettura, definita dalla chiarificazione accettata. | Badge uguale al numero di notifiche non lette; marcare una notifica non modifica lo stato della conversazione e viceversa (**[AFU-RULE-006](#provenance-AFU-RULE-006)**). Posizione responsive flessibile. |
| Impostazioni notifiche | Message, Task Update, Task Deadline, Mentor Help e Salva modifiche (`design-description`, §§286–298). | Quattro toggle solo email; notifiche in-app sempre attive e leggibili nell’inbox (**[AFU-RULE-007](#provenance-AFU-RULE-007)**, **[AFU-AC-002](#provenance-AFU-AC-002)**). |
| Impostazioni generali | Lingua, fuso orario, scelta 12/24 ore e Salva modifiche (`design-description`, §§272–284, 367–375). | Controlli responsive presenti; opzioni specifiche e dettagli di salvataggio non sono definiti dalle fonti. |

**[AFU-AC-003](#provenance-AFU-AC-003)** — In desktop e mobile, lo studente visualizza solo la propria consegna, la cronologia delle versioni e lo stato; il mentor assegnato seleziona la versione da valutare e può completare o chiedere correzioni con motivazione. Lo studente vede feedback di invio riuscito/fallito, ritardo, versione superata e attività completata/non modificabile. [Origine: `clarification:15ef4e45-31a4-4e93-8d66-63bdcdfe7969`]

**[AFU-AC-004](#provenance-AFU-AC-004)** — Per un invio valido si crea una nuova versione. Per formato non ammesso, limite superato, annullamento o interruzione non si crea alcuna versione e le precedenti restano inalterate; lo studente vede il motivo e può correggere e riprovare. [Origine: `clarification:9970c26d-d463-4f30-87b0-4449d9a5ea8a`]

**[AFU-AC-005](#provenance-AFU-AC-005)** — La campanella apre l’elenco in-app; il badge conta le notifiche non lette. «Segna come letta» modifica soltanto la notifica selezionata; la lettura di una conversazione modifica soltanto lo stato della conversazione. La disposizione dell’elenco è adattabile a desktop/mobile. [Origine: `clarification:250d30b1-5b0e-4478-8a06-ac8db516bc7f`]

## Input, output e integrazioni

L’input file degli invii di attività è circoscritto da **[AFU-RULE-005](#provenance-AFU-RULE-005)**. L’output dello studente è una nuova versione accettata con file e puntualità; l’output del mentor è una decisione riferita a una versione. Le conseguenze di invio rifiutato e ripristino sono definite da **[AFU-AC-004](#provenance-AFU-AC-004)**. Il design mostra allegati immagine nella messaggistica, ma il Work e le chiarificazioni non estendono a questi la policy di upload delle consegne; non si deducono formati o limiti aggiuntivi per i messaggi dai soli esempi visivi (`design-description`, §§254, 268).

Le notifiche in-app vengono rese nell’inbox e includono un conteggio non letto; l’email è un canale separato, regolato dai quattro toggle. Gli eventi e la separazione dei canali sono descritti in **[AFU-AC-001](#provenance-AFU-AC-001)** e **[AFU-AC-002](#provenance-AFU-AC-002)**. Non è richiesta un’integrazione esterna specifica da Work. I controlli telefono/video nel design non costituiscono un impegno a integrare servizi di chiamata. Nessuna API viene definita in questa AFU.

## Vincoli, fattibilità e questioni aperte

Il vincolo funzionale principale è l’autorizzazione per ruolo anche sugli accessi diretti (**[AFU-RULE-001](#provenance-AFU-RULE-001)**, **[AFU-RULE-002](#provenance-AFU-RULE-002)**). I limiti degli upload di consegna e il rifiuto senza mutazione sono umanamente approvati (**[AFU-RULE-005](#provenance-AFU-RULE-005)**). Inbox e stati letti indipendenti sono approvati (**[AFU-RULE-006](#provenance-AFU-RULE-006)**); i toggle email-only e l’assenza di opt-out in-app per categoria sono approvati (**[AFU-RULE-007](#provenance-AFU-RULE-007)**). Non rimangono blocker materiali noti; `blockedQuestionIds` è vuoto.

Feasibility verificata in sola lettura:

- Il frontend `https://github.com/demeedogg/task-managment-frontend`, branch `main`, commit `5ef7900b2fbc037b03f50c58a6fdba9d8ee9c7bd`, contiene solo `README.md`; non sono verificabili UI, sessione, responsive, integrazioni o test (`analysis:task-managment-frontend-8577187c`, §§7–18; `repositories`). È necessaria una prima implementazione dell’app frontend.
- Il backend `https://github.com/demeedogg/task-managment-backend`, branch `main`, commit `4985e4cfb8d0135b7aecf7b1b6e7412d1e443396`, contiene solo `README.md`; non sono verificabili autenticazione, autorizzazione, persistenza, versioni, upload, notifiche o test (`analysis:task-managment-backend-21c6dc4a`, §§7–15; `repositories`). È necessaria una prima implementazione backend; nessuna migrazione o compatibilità esistente è accertabile.
- Le conclusioni backend/front-end sono coerenti sulle regole di ruolo, versioni, scadenze, stati, notifiche e parità desktop/mobile (`analysis:task-managment-backend-21c6dc4a`, §§19–25; `analysis:task-managment-frontend-8577187c`, §§32–36). I comportamenti target sono formulati nel presente contratto, ma la fattibilità end-to-end resta ipotetica finché il codice non esiste. Non sono stati eseguiti build, test, applicazioni, container o integrazioni di rete; i repository non sono stati modificati.

Questioni non bloccanti: i valori di esempio nei render non fissano metriche/dati di produzione; opzioni dei filtri, valori di lingua/fuso orario e layout preciso dell’inbox possono essere definiti mantenendo le regole di accesso e di lettura. Il significato di Follow oltre allo stato presentato non è definito e non modifica l’assegnazione o i permessi. Il comportamento dei controlli telefono/video non stabilisce un’integrazione esterna.

<!-- sdlc-decision-provenance:v1
{
  "schemaVersion": 1,
  "reviewRound": 1,
  "evidenceDigest": "aa0a318cea0a6209d6d5c449caa8f41e6ddd44924a275289d37f245d5c23b7d0",
  "entries": [
    {
      "subjectId": "AFU-REQ-001",
      "subjectKind": "requirement",
      "supersedes": [],
      "origins": [
        {
          "kind": "explicit_source",
          "sources": [
            {
              "evidenceRef": "work",
              "locator": "description \u003e OBIETTIVO E REQUISITI: prodotto e obiettivo studenti/mentor"
            }
          ]
        }
      ]
    },
    {
      "subjectId": "AFU-REQ-002",
      "subjectKind": "requirement",
      "supersedes": [],
      "origins": [
        {
          "kind": "explicit_source",
          "sources": [
            {
              "evidenceRef": "work",
              "locator": "description \u003e Ambito: dashboard, attività, mentor, messaggi, notifiche e impostazioni; riferimento Figma desktop/mobile"
            },
            {
              "evidenceRef": "design-description",
              "locator": "§§466–472: pattern condivisi desktop/mobile e famiglie di schermate"
            }
          ]
        }
      ]
    },
    {
      "subjectId": "AFU-RULE-001",
      "subjectKind": "rule",
      "supersedes": [],
      "origins": [
        {
          "kind": "explicit_source",
          "sources": [
            {
              "evidenceRef": "work",
              "locator": "description \u003e Regole di business \u003e 1. Visibilità e permessi: studente, conversazioni proprie e accesso diretto"
            }
          ]
        }
      ]
    },
    {
      "subjectId": "AFU-RULE-002",
      "subjectKind": "rule",
      "supersedes": [],
      "origins": [
        {
          "kind": "explicit_source",
          "sources": [
            {
              "evidenceRef": "work",
              "locator": "description \u003e Regole di business \u003e 1. Visibilità e permessi: mentor assegnato; directory non autorizza accesso alle attività di altri studenti"
            }
          ]
        },
        {
          "kind": "agent_decision",
          "sources": [
            {
              "evidenceRef": "work",
              "locator": "description \u003e Regole di business \u003e 1. Visibilità e permessi: accesso alle attività limitato all’assegnazione"
            },
            {
              "evidenceRef": "design-description",
              "locator": "§§237–249, 334–346, 480: Follow/Followed visibile, semantica dell’assegnazione non mostrata"
            }
          ],
          "decisionType": "deduction",
          "rationale": "Non attribuire al controllo Follow un cambio di assegnazione o permessi non stabilito dalle fonti; i diritti di revisione restano legati all’assegnazione esplicita, preservando il confine autorizzativo del Work.",
          "specialists": [
            "requirements",
            "frontend"
          ]
        }
      ]
    },
    {
      "subjectId": "AFU-RULE-003",
      "subjectKind": "rule",
      "supersedes": [],
      "origins": [
        {
          "kind": "explicit_source",
          "sources": [
            {
              "evidenceRef": "work",
              "locator": "description \u003e Regole di business \u003e 2. Ciclo di vita delle attività: cinque stati, transizioni consentite, motivazione correzioni e blocco dopo completamento"
            }
          ]
        }
      ]
    },
    {
      "subjectId": "AFU-RULE-004",
      "subjectKind": "rule",
      "supersedes": [],
      "origins": [
        {
          "kind": "explicit_source",
          "sources": [
            {
              "evidenceRef": "work",
              "locator": "description \u003e Regole di business \u003e 3. Consegne e scadenze: versioni della consegna e puntualità al momento dell’invio"
            }
          ]
        },
        {
          "kind": "human_clarification",
          "sources": [
            {
              "evidenceRef": "clarification:15ef4e45-31a4-4e93-8d66-63bdcdfe7969",
              "locator": "accepted decision: mentor selects a specific submission version; stale-version and late outcomes are visible"
            }
          ],
          "interactionId": "15ef4e45-31a4-4e93-8d66-63bdcdfe7969",
          "question": "Confermi che il dettaglio attività debba distinguere i flussi di studente e mentor e che i frame Figma vadano integrati, per desktop e mobile, con le azioni e i feedback mancanti? In particolare, lo studente dovrebbe vedere la propria consegna, le sue versioni e il relativo stato; solo il mentor assegnato dovrebbe poter selezionare una versione da valutare, completare l’attività o richiedere correzioni con motivazione. I frame dovrebbero inoltre mostrare gli esiti necessari, inclusi invio riuscito o fallito, ritardo, versione superata e attività completata/non modificabile. Se questa rappresentazione non è quella desiderata, indica quale schermata o flusso deve rappresentare le azioni del mentor e gli esiti della consegna.",
          "answer": "confermo\n"
        }
      ]
    },
    {
      "subjectId": "AFU-RULE-005",
      "subjectKind": "rule",
      "supersedes": [],
      "origins": [
        {
          "kind": "human_clarification",
          "sources": [
            {
              "evidenceRef": "clarification:9970c26d-d463-4f30-87b0-4449d9a5ea8a",
              "locator": "accepted decision on submission file count, size, allowed formats, rejection, preservation and retry"
            }
          ],
          "interactionId": "9970c26d-d463-4f30-87b0-4449d9a5ea8a",
          "question": "Quali limiti devono applicarsi ai file caricati per le consegne: numero massimo di file, dimensione massima per file e complessiva, e formati ammessi? Se un file è non supportato, supera un limite o il caricamento viene annullato o interrotto, confermi che l’invio debba essere rifiutato senza creare una nuova versione, lasciando inalterate quelle precedenti e mostrando allo studente il motivo così che possa correggere e riprovare?",
          "answer": "la tua assunzione va bene\n"
        }
      ]
    },
    {
      "subjectId": "AFU-RULE-006",
      "subjectKind": "rule",
      "supersedes": [],
      "origins": [
        {
          "kind": "explicit_source",
          "sources": [
            {
              "evidenceRef": "work",
              "locator": "description \u003e Regole di business: stato letto delle notifiche distinto dallo stato letto delle conversazioni"
            }
          ]
        },
        {
          "kind": "human_clarification",
          "sources": [
            {
              "evidenceRef": "clarification:250d30b1-5b0e-4478-8a06-ac8db516bc7f",
              "locator": "accepted notification inbox, unread badge, explicit per-item read action and independent conversation state"
            }
          ],
          "interactionId": "250d30b1-5b0e-4478-8a06-ac8db516bc7f",
          "question": "Confermi che la campanella apra un elenco in-app di notifiche individuali, che il badge mostri quante sono non lette e che ogni notifica abbia un’azione esplicita «Segna come letta»? L’azione dovrebbe aggiornare solo lo stato di quella notifica; leggere una conversazione dovrebbe aggiornare solo lo stato della conversazione. La disposizione dell’elenco — pagina, pannello o altro — può seguire il design desktop e mobile.",
          "answer": "confermo\n"
        }
      ]
    },
    {
      "subjectId": "AFU-RULE-007",
      "subjectKind": "rule",
      "supersedes": [],
      "origins": [
        {
          "kind": "explicit_source",
          "sources": [
            {
              "evidenceRef": "work",
              "locator": "description \u003e Regole di business: disattivazione email non disattiva notifica in-app"
            }
          ]
        },
        {
          "kind": "human_clarification",
          "sources": [
            {
              "evidenceRef": "clarification:4da29b06-1b37-43e7-a898-8e2d9eb5d71c",
              "locator": "accepted decision that four category toggles are email-only; in-app notifications stay on with no in-app category opt-outs"
            }
          ],
          "interactionId": "4da29b06-1b37-43e7-a898-8e2d9eb5d71c",
          "question": "Confermi che i quattro interruttori «Message», «Task Update», «Task Deadline» e «Mentor Help» regolino solo le email per categoria, mentre le notifiche in-app restano attive nell’inbox approvato? Oppure vuoi anche preferenze separate per disattivare categorie di notifiche in-app? In entrambi i casi, disattivare un’email non deve disattivare la notifica in-app corrispondente.",
          "answer": "La tua assunzione va bene"
        }
      ]
    },
    {
      "subjectId": "AFU-RULE-008",
      "subjectKind": "rule",
      "supersedes": [],
      "origins": [
        {
          "kind": "agent_decision",
          "sources": [
            {
              "evidenceRef": "work",
              "locator": "description \u003e Regole di business \u003e 1. Visibilità e permessi and 2. Ciclo di vita: aggregates must respect caller visibility and completed is a distinct state"
            },
            {
              "evidenceRef": "analysis:task-managment-backend-21c6dc4a",
              "locator": "§23: derive dashboard aggregates from caller-visible activities and count completed activities only"
            },
            {
              "evidenceRef": "analysis:task-managment-frontend-8577187c",
              "locator": "§24: align dashboard/list scope and count only completed state"
            }
          ],
          "decisionType": "deduction",
          "rationale": "Deriving aggregates from the same authorized activity set as the corresponding list preserves the explicit access boundary; counting only the completed state preserves the five distinct lifecycle states and avoids conflating in-review with completion.",
          "specialists": [
            "requirements",
            "frontend",
            "backend"
          ]
        }
      ]
    },
    {
      "subjectId": "AFU-RULE-009",
      "subjectKind": "rule",
      "supersedes": [],
      "origins": [
        {
          "kind": "explicit_source",
          "sources": [
            {
              "evidenceRef": "work",
              "locator": "description \u003e Obiettivo: communicate with mentors; Regole di business \u003e 1. Visibilità e permessi: own/participant conversations only"
            },
            {
              "evidenceRef": "design-description",
              "locator": "§§251–270: conversation list, messages, attachments and composer"
            }
          ]
        }
      ]
    },
    {
      "subjectId": "AFU-AC-001",
      "subjectKind": "acceptance",
      "supersedes": [],
      "origins": [
        {
          "kind": "explicit_source",
          "sources": [
            {
              "evidenceRef": "work",
              "locator": "description \u003e Regole di business: notifications for submission, correction and completion events; email preferences separate from in-app notifications"
            }
          ]
        },
        {
          "kind": "agent_decision",
          "sources": [
            {
              "evidenceRef": "work",
              "locator": "description \u003e Regole di business: submission and review outcomes are distinct from notification email preference"
            },
            {
              "evidenceRef": "analysis:task-managment-backend-21c6dc4a",
              "locator": "§24: email delivery failure must not roll back submission or review"
            }
          ],
          "decisionType": "deduction",
          "rationale": "A delivery failure in the optional email channel is not the outcome of the already accepted submission or review action; reporting that core action as failed would misstate its persisted product result.",
          "specialists": [
            "requirements",
            "backend"
          ]
        }
      ]
    },
    {
      "subjectId": "AFU-AC-002",
      "subjectKind": "acceptance",
      "supersedes": [],
      "origins": [
        {
          "kind": "human_clarification",
          "sources": [
            {
              "evidenceRef": "clarification:4da29b06-1b37-43e7-a898-8e2d9eb5d71c",
              "locator": "accepted email-only semantics for Message, Task Update, Task Deadline and Mentor Help toggles"
            }
          ],
          "interactionId": "4da29b06-1b37-43e7-a898-8e2d9eb5d71c",
          "question": "Confermi che i quattro interruttori «Message», «Task Update», «Task Deadline» e «Mentor Help» regolino solo le email per categoria, mentre le notifiche in-app restano attive nell’inbox approvato? Oppure vuoi anche preferenze separate per disattivare categorie di notifiche in-app? In entrambi i casi, disattivare un’email non deve disattivare la notifica in-app corrispondente.",
          "answer": "La tua assunzione va bene"
        }
      ]
    },
    {
      "subjectId": "AFU-AC-003",
      "subjectKind": "acceptance",
      "supersedes": [],
      "origins": [
        {
          "kind": "human_clarification",
          "sources": [
            {
              "evidenceRef": "clarification:15ef4e45-31a4-4e93-8d66-63bdcdfe7969",
              "locator": "accepted role-specific student/assigned-mentor detail actions and desktop/mobile submission/review feedback"
            }
          ],
          "interactionId": "15ef4e45-31a4-4e93-8d66-63bdcdfe7969",
          "question": "Confermi che il dettaglio attività debba distinguere i flussi di studente e mentor e che i frame Figma vadano integrati, per desktop e mobile, con le azioni e i feedback mancanti? In particolare, lo studente dovrebbe vedere la propria consegna, le sue versioni e il relativo stato; solo il mentor assegnato dovrebbe poter selezionare una versione da valutare, completare l’attività o richiedere correzioni con motivazione. I frame dovrebbero inoltre mostrare gli esiti necessari, inclusi invio riuscito o fallito, ritardo, versione superata e attività completata/non modificabile. Se questa rappresentazione non è quella desiderata, indica quale schermata o flusso deve rappresentare le azioni del mentor e gli esiti della consegna.",
          "answer": "confermo\n"
        }
      ]
    },
    {
      "subjectId": "AFU-AC-004",
      "subjectKind": "acceptance",
      "supersedes": [],
      "origins": [
        {
          "kind": "human_clarification",
          "sources": [
            {
              "evidenceRef": "clarification:9970c26d-d463-4f30-87b0-4449d9a5ea8a",
              "locator": "accepted invalid/over-limit/cancelled/interrupted upload behavior and retry"
            }
          ],
          "interactionId": "9970c26d-d463-4f30-87b0-4449d9a5ea8a",
          "question": "Quali limiti devono applicarsi ai file caricati per le consegne: numero massimo di file, dimensione massima per file e complessiva, e formati ammessi? Se un file è non supportato, supera un limite o il caricamento viene annullato o interrotto, confermi che l’invio debba essere rifiutato senza creare una nuova versione, lasciando inalterate quelle precedenti e mostrando allo studente il motivo così che possa correggere e riprovare?",
          "answer": "la tua assunzione va bene\n"
        }
      ]
    },
    {
      "subjectId": "AFU-AC-005",
      "subjectKind": "acceptance",
      "supersedes": [],
      "origins": [
        {
          "kind": "human_clarification",
          "sources": [
            {
              "evidenceRef": "clarification:250d30b1-5b0e-4478-8a06-ac8db516bc7f",
              "locator": "accepted inbox, unread badge, explicit per-notification read action, independent conversation state, flexible placement"
            }
          ],
          "interactionId": "250d30b1-5b0e-4478-8a06-ac8db516bc7f",
          "question": "Confermi che la campanella apra un elenco in-app di notifiche individuali, che il badge mostri quante sono non lette e che ogni notifica abbia un’azione esplicita «Segna come letta»? L’azione dovrebbe aggiornare solo lo stato di quella notifica; leggere una conversazione dovrebbe aggiornare solo lo stato della conversazione. La disposizione dell’elenco — pagina, pannello o altro — può seguire il design desktop e mobile.",
          "answer": "confermo\n"
        }
      ]
    }
  ]
}
-->
