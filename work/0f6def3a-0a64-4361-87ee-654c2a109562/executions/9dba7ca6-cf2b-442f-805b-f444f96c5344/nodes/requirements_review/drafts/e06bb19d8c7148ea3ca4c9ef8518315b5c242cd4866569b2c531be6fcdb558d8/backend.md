---
reviewDomain: backend
reviewRound: 1
evidenceDigest: aa0a318cea0a6209d6d5c449caa8f41e6ddd44924a275289d37f245d5c23b7d0
evidenceRefs:
  - work
  - analysis:task-managment-backend-21c6dc4a
  - analysis:task-managment-frontend-8577187c
  - clarification:15ef4e45-31a4-4e93-8d66-63bdcdfe7969
  - clarification:9970c26d-d463-4f30-87b0-4449d9a5ea8a
  - clarification:250d30b1-5b0e-4478-8a06-ac8db516bc7f
  - clarification:4da29b06-1b37-43e7-a898-8e2d9eb5d71c
  - design-description
  - repositories
  - review:working-documents
blockedQuestionIds: []
reviewStatus: ready
---

# Analisi backend — TASK MANAGMENT - 3

## Ambito, fonti e stato attuale

Questa analisi precisa gli esiti osservabili e i vincoli lato backend per il prodotto richiesto; non definisce API o scelte tecnologiche. Il Work richiede un’app in cui gli studenti seguono e consegnano attività formative e comunicano con i mentor, che verificano le consegne degli studenti assegnati (`work`, descrizione → «OBIETTIVO E REQUISITI»). Le regole testuali del Work prevalgono per le regole di business; i render Figma documentano i controlli visibili e, dove mancanti, le clarification accettate completano i comportamenti richiesti.

I repository sono evidenza dello stato corrente, non dell’obiettivo. Il backend `https://github.com/demeedogg/task-managment-backend.git`, `main@4985e4cfb8d0135b7aecf7b1b6e7412d1e443396`, contiene solo `README.md`; non vi sono codice, configurazione, modello dati, autorizzazioni o integrazioni verificabili (`analysis:task-managment-backend-21c6dc4a`, «Evidence examined» e «Findings», righe 3–15; pin in `repositories`, righe 9–12). Anche il frontend `https://github.com/demeedogg/task-managment-frontend.git`, `main@5ef7900b2fbc037b03f50c58a6fdba9d8ee9c7bd`, contiene solo `README.md` e non ha schermate o integrazioni verificabili (`analysis:task-managment-frontend-8577187c`, righe 5–18; pin in `repositories`, righe 2–6). Di conseguenza non è possibile confermare comportamenti già implementati né verificare la fattibilità rispetto a componenti o configurazioni esistenti.

## Identità, visibilità e autorizzazioni

- Lo studente accede alle proprie attività, consegne, versioni e conversazioni. Il mentor accede agli studenti assegnati e alle relative attività. Questi limiti valgono anche quando si accede direttamente a una risorsa; la consultazione dell’elenco mentor non autorizza l’accesso al lavoro di studenti non assegnati (`work`, descrizione → regola di business 1).
- Solo il mentor assegnato può esaminare e valutare la consegna di quello studente. La directory mostra controlli Follow/Followed, ma non ne specifica l’effetto (`design-description`, render desktop `render-web---mentors-36-5489`, righe 237–242; mobile `render-mobile---mentors-36-6747`, righe 244–249). In ogni caso, il solo accesso alla directory o un follow non conferisce permessi sulle attività non assegnate, in coerenza con il limite esplicito del Work.
- Le conversazioni sono visibili solo ai partecipanti; le restrizioni per ruolo e assegnazione devono restare valide anche per accessi diretti. La necessità di accesso per partecipanti è inoltre registrata nelle analisi di repository (`analysis:task-managment-backend-21c6dc4a`, righe 19 e 24; `analysis:task-managment-frontend-8577187c`, righe 27 e 32).

**Esito verificabile:** uno studente non ottiene dati di un altro studente cambiando la risorsa consultata; un mentor non assegnato non può leggere né valutare consegne; aprire una conversazione non autorizzata non espone contenuti. L’interfaccia responsive non sostituisce queste autorizzazioni.

## Attività, consegne e transizioni

- Le attività hanno gli stati «da iniziare», «in corso», «in revisione», «da correggere» e «completata». Lo studente può iniziare e inviare in revisione; solo il mentor assegnato può completare o chiedere correzioni, con motivazione obbligatoria. Dopo il completamento lo studente non può più modificare l’attività (`work`, descrizione → regole di business 2–3).
- Ogni invio accettato crea una nuova versione consultabile dallo studente; il mentor assegnato seleziona la versione da valutare. La valutazione si riferisce alla versione selezionata e non deve apparire come esito della versione corrente se quella valutata è superata. Il feedback per versione superata, attività completata e invio riuscito o fallito è stato confermato per entrambi i ruoli e formati (`clarification:15ef4e45-31a4-4e93-8d66-63bdcdfe7969`, domanda e risposta accettata, righe 7–10).
- Una consegna tardiva è ammessa ma contrassegnata come tardiva; la puntualità si determina all’invio e non cambia in base al momento della revisione (`work`, descrizione → regola di business 3; `analysis:task-managment-backend-21c6dc4a`, righe 20–22).

**Criteri osservabili:** lo studente vede stato e cronologia delle proprie versioni; il mentor assegnato può valutare una versione specifica e, in caso di correzioni, deve fornire una motivazione; un esito su una versione superata non completa silenziosamente quella corrente; un’attività completata non è modificabile dallo studente. Gli esiti e le azioni sono coerenti su desktop e mobile (`clarification:15ef4e45-31a4-4e93-8d66-63bdcdfe7969`, righe 7–10; i render di dettaglio iniziali non mostravano questi stati: `design-description`, righe 223–235).

## Vincoli upload, fallimento e recupero

La zona di caricamento e il pulsante Submit compaiono nei dettagli desktop e mobile, ma i render originari non mostravano vincoli o feedback (`design-description`, `render-web---detail-task-39-1865`, righe 226–228; `render-mobile---detail-task-84-2102`, righe 233–235). La clarification accettata definisce i limiti e il recupero: al massimo **5 file**, **10 MiB per file** e **25 MiB complessivi**; formati ammessi **PDF, DOCX, PPTX, XLSX, TXT, PNG e JPEG**. Un file non supportato, oltre limite, o un caricamento annullato o interrotto rifiuta l’invio senza creare una nuova versione, lascia inalterate quelle precedenti, spiega il motivo allo studente e consente la correzione e il nuovo tentativo (`clarification:9970c26d-d463-4f30-87b0-4449d9a5ea8a`, domanda e risposta accettata, righe 7–10; i limiti sono l’assunzione accettata nel contesto della clarification).

**Criteri osservabili:** i limiti sono rispettati; una consegna incompleta o non valida non diventa una versione; la cronologia preesistente resta accessibile; lo studente riceve una spiegazione e può correggere e riprovare. Una versione nasce solo da un invio completo e accettato. Questi limiti rendono verificabile il profilo di input e risolvono la decisione di prodotto precedentemente aperta.

## Dashboard, conversazioni e notifiche

- Dashboard e liste riflettono solo le attività visibili al chiamante. I conteggi di completamento includono solo attività completate e devono essere coerenti con gli stessi filtri e intervalli temporali delle liste corrispondenti (`work`, descrizione → requisiti dashboard; `analysis:task-managment-backend-21c6dc4a`, riga 23). I valori esemplificativi dei render non definiscono metriche di business (`design-description`, render desktop e mobile dashboard, righe 195–207).
- Una conversazione e il suo stato di lettura sono separati dalle notifiche. La clarification accettata stabilisce che la campanella apre un elenco in-app, il badge conta le notifiche non lette e ogni elemento ha un’azione esplicita «Segna come letta». Tale azione aggiorna solo quella notifica; leggere una conversazione aggiorna solo lo stato della conversazione. La disposizione dell’elenco può seguire il design responsive (`clarification:250d30b1-5b0e-4478-8a06-ac8db516bc7f`, domanda e risposta accettata, righe 7–10). Questo completa la lacuna dei render che mostravano badge e indicatori di conversazione senza un inbox o stati di lettura definiti (`design-description`, §«Open questions», riga 481).
- I quattro interruttori «Message», «Task Update», «Task Deadline» e «Mentor Help» regolano solo le email per categoria. Le notifiche in-app restano attive nell’inbox approvato; non sono previste preferenze di opt-out in-app per categoria. Disabilitare email non sopprime la notifica in-app corrispondente (`clarification:4da29b06-1b37-43e7-a898-8e2d9eb5d71c`, domanda e risposta accettata, righe 7–10). I render mostrano i quattro interruttori ma non ne identificano il canale (`design-description`, render desktop `render-web---settings---notification-58-2195`, righe 286–291; render mobile `render-mobile---settings---notification-58-2279`, righe 293–298). La clarification risolve questa ambiguità di canale.
- Gli eventi rilevanti di invio, richiesta di correzioni e completamento notificano i destinatari coinvolti. Un errore di consegna email non annulla né trasforma in fallimento un invio o una valutazione già salvati; le notifiche in-app non dipendono dalle preferenze email (`work`, descrizione → regole su notifiche e preferenze; `analysis:task-managment-backend-21c6dc4a`, riga 24; conferma cross-domain in `analysis:task-managment-frontend-8577187c`, righe 27 e 36).

**Criteri osservabili:** il badge riflette il numero di notifiche in-app non lette; marcare una notifica letta non modifica la conversazione e viceversa; disattivare una categoria email non impedisce la relativa notifica in-app; un errore email non cambia l’esito già persistito dell’azione principale. Il significato lato backend dei controlli di canale è ora determinato dalla clarification accettata, non dai soli render.

## Feasibilità, limiti di verifica e blocker

Le regole di autorizzazione, ciclo di vita, consegne con input limitato, esiti di errore, notifiche e preferenze definiscono un comportamento backend sufficientemente concreto per la pianificazione. Le clarification accettate risolvono i precedenti dubbi backend su dettaglio per ruolo, limiti upload, stato di lettura indipendente e canale email dei quattro interruttori. **Non rimangono blocker backend di prodotto** (`blockedQuestionIds: []`).

La fattibilità rispetto all’implementazione esistente resta **non verificabile**: il commit backend indicato contiene solo README e non offre codice o configurazione con cui verificare autenticazione, persistenza, caricamenti, notifiche o email (`analysis:task-managment-backend-21c6dc4a`, righe 7–15). Anche il repository frontend non contiene un’applicazione da confrontare (`analysis:task-managment-frontend-8577187c`, righe 7–18). La consegna email effettiva e le relative dipendenze non sono verificabili dai repository; l’obbligo di prodotto e il comportamento in caso di fallimento sono espliciti, mentre la scelta del meccanismo resta fuori da questa analisi. Nessun build, test, applicazione o integrazione è stato eseguito.

Il registro operativo indicava il documento backend come mancante e senza recovery (`review:working-documents`, righe 25–31); questo file è la stesura completa per il digest corrente.
