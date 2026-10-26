---
reviewDomain: frontend
reviewRound: 1
evidenceDigest: aa0a318cea0a6209d6d5c449caa8f41e6ddd44924a275289d37f245d5c23b7d0
evidenceRefs:
  - work
  - design-description
  - analysis:task-managment-frontend-8577187c
  - analysis:task-managment-backend-21c6dc4a
  - clarification:15ef4e45-31a4-4e93-8d66-63bdcdfe7969
  - clarification:9970c26d-d463-4f30-87b0-4449d9a5ea8a
  - clarification:250d30b1-5b0e-4478-8a06-ac8db516bc7f
  - clarification:4da29b06-1b37-43e7-a898-8e2d9eb5d71c
  - repositories
  - review:working-documents
blockedQuestionIds: []
reviewStatus: ready
---

# Revisione frontend — TASK MANAGMENT - 3

## Esito e impatto dei chiarimenti accettati

La presente valutazione usa il Work come fonte delle regole e il design description come evidenza delle schermate, dei contenuti e dei controlli rappresentati. I frame sono riferimenti visivi, non prova di comportamenti non descritti. L’inventario `review:working-documents` conferma che questo documento era mancante e non disponeva di una copia di recupero.

I quattro chiarimenti accettati risolvono le precedenti domande materiali frontend:

- `clarification:15ef4e45-31a4-4e93-8d66-63bdcdfe7969`: dettaglio attività distinto per studente e mentor; lo studente vede le proprie consegne, versioni e stato; solo il mentor assegnato può scegliere una versione e completare o richiedere correzioni motivate. Le viste desktop e mobile mostrano invio riuscito/fallito, ritardo, versione superata e attività completata/non modificabile.
- `clarification:9970c26d-d463-4f30-87b0-4449d9a5ea8a`: per invio, massimo cinque file, massimo 10 MiB ciascuno e 25 MiB complessivi; formati PDF, DOCX, PPTX, XLSX, TXT, PNG e JPEG. ZIP non è ammesso. File non supportati, oltre limite o caricamenti falliti, annullati o interrotti comportano rifiuto senza creare una nuova versione o alterare le versioni precedenti; lo studente vede il motivo e può correggere e riprovare.
- `clarification:250d30b1-5b0e-4478-8a06-ac8db516bc7f`: la campanella apre un elenco in-app; il badge conta le notifiche non lette; ogni notifica ha un’azione esplicita “Segna come letta”. L’azione aggiorna solo quella notifica; leggere una conversazione aggiorna solo lo stato della conversazione. La collocazione dell’elenco può seguire il design desktop/mobile.
- `clarification:4da29b06-1b37-43e7-a898-8e2d9eb5d71c`: la risposta umana accettata (“La tua assunzione va bene”) conferma che i quattro interruttori Message, Task Update, Task Deadline e Mentor Help regolano solo le email per categoria. Non ci sono preferenze per disattivare categorie in-app; disattivare un’email non disattiva la notifica in-app corrispondente.

Queste decisioni sono origini umane accettate. Non estendono l’accesso del mentor oltre gli studenti assegnati né introducono ulteriori canali di comunicazione.

## Flussi e comportamento visibile

### Navigazione, dashboard ed elenco attività

Il Work circoscrive l’esperienza a dashboard, elenco/dettaglio attività, mentor, messaggi, notifiche e impostazioni. Il design mostra la navigazione desktop in una barra laterale e su mobile un menu compatto (`design-description`: `render-web---dashboard-6-2335`, `render-mobile---dashboard-36-3066`; pattern condiviso al §466–472). La navigazione deve portare alle sezioni indicate; il comportamento preciso del menu mobile è un dettaglio di interazione.

Lo studente visualizza solo le proprie attività; il mentor visualizza solo studenti assegnati e relative attività. Tali limiti si applicano anche all’accesso diretto a un dettaglio (`work`, regola di visibilità). La ricerca, i filtri e l’ordinamento rappresentati nell’elenco non devono allargare quell’insieme autorizzato (`render-web---task-36-3071`, `render-mobile---task-36-4048`). “Explore Task”, i nomi, i progressi e le date di esempio sono contenuti illustrativi, non autorizzazione a consultare attività non assegnate.

La dashboard può mostrare attività, prossime scadenze, calendario e riepiloghi coerenti con il ruolo e con l’insieme accessibile all’utente. I valori e le date specifici nei render (tra cui i campioni 2022/2024 e i conteggi di esempio) non definiscono metriche di prodotto (`render-web---dashboard-6-2335`, `render-web---dashboard-133-4811`, `render-web---dashboard-133-7928`). Non presentare “in revisione” come “completata”: il Work distingue i cinque stati da iniziare, in corso, in revisione, da correggere e completata.

### Dettaglio e consegna dello studente

I frame desktop e mobile mostrano contenuto/criteri dell’attività, area di consegna e azione generica “Submit” (`render-web---detail-task-39-1865`, `render-mobile---detail-task-84-2102`). Per conformarsi al Work e al chiarimento accettato, il dettaglio presenta allo studente il proprio stato e la cronologia/versioni della propria consegna. Lo studente può iniziare e inviare; il semplice invio non deve essere rappresentato come completamento. Ogni invio accettato crea una versione; la puntualità è mostrata per quella versione e un invio tardivo resta possibile, con indicazione di ritardo (`work`, regole su ciclo di vita e consegne; `clarification:15ef4e45-31a4-4e93-8d66-63bdcdfe7969`).

Prima dell’invio, il controllo visibile applica i limiti accettati: massimo 5 file, 10 MiB ciascuno, 25 MiB complessivi e soltanto PDF, DOCX, PPTX, XLSX, TXT, PNG e JPEG. Se un file è non supportato, supera un limite o il caricamento fallisce, viene annullato o interrotto, l’invio è rifiutato, non viene creata una versione, le versioni precedenti restano inalterate e lo studente vede il motivo per poter correggere e riprovare (`clarification:9970c26d-d463-4f30-87b0-4449d9a5ea8a`). L’interfaccia deve distinguere l’esito dell’invio dall’esito della valutazione.

Il dettaglio deve mostrare gli esiti di successo/fallimento e ritardo. Se la valutazione riguarda una versione non più corrente, il risultato deve essere esplicito e non apparire come completamento della versione corrente. Un’attività completata è non modificabile dallo studente (`work`, regole di ciclo di vita e consegne; `clarification:15ef4e45-31a4-4e93-8d66-63bdcdfe7969`). Messaggio, disposizione, caricamento e retry UI sono decisioni di presentazione, purché rispettino questi effetti.

### Dettaglio e valutazione del mentor

Il mentor può aprire soltanto attività degli studenti assegnati e non acquisisce accesso attraverso la directory mentor (`work`, regola di visibilità). Nel dettaglio role-aware può selezionare la versione da valutare; solo il mentor assegnato può completare l’attività o richiedere correzioni. La richiesta di correzione richiede una motivazione; il risultato e la versione valutata devono essere visibili. Il mentor non deve poter completare implicitamente una versione più recente valutando una versione obsoleta (`work`, regole su visibilità e ciclo di vita; `clarification:15ef4e45-31a4-4e93-8d66-63bdcdfe7969`).

### Mentor, messaggi e notifiche

La directory mostra ricerca, categorie, ordinamento, schede e controlli Follow/Followed (`render-web---mentors-36-5489`, `render-mobile---mentors-36-6747`). Seguire un mentor non concede accesso alle attività di studenti non assegnati (`work`, regola di visibilità). L’eventuale significato di Follow oltre alla presentazione non è definito e non va usato per modificare l’assegnazione.

La messaggistica desktop separa lista e conversazione; su mobile lista e chat sono render distinti (`render-web---message-38-2152`, `render-mobile---message-53-2129`, `render-mobile---message---chat-53-2749`). Uno studente vede solo le proprie conversazioni; le conversazioni mentor sono limitate ai partecipanti autorizzati (`work`, regola di visibilità). I marcatori grafici rosso/blu nei render non sono etichettati; la UI deve comunicare chiaramente lo stato pertinente senza confondere lettura della conversazione e lettura della notifica.

In base a `clarification:250d30b1-5b0e-4478-8a06-ac8db516bc7f`, la campanella apre un elenco in-app e il badge rappresenta il numero di notifiche non lette. Ogni elemento consente di segnare letta la singola notifica. Questa azione cambia soltanto lo stato della notifica; leggere una conversazione cambia soltanto quello della conversazione. La forma responsive (pagina, pannello o altra composizione) è lasciata al design e non costituisce una domanda materiale.

### Impostazioni e significato dei quattro interruttori

Il design mostra quattro interruttori per Message, Task Update, Task Deadline e Mentor Help, ma non indica il canale (`render-web---settings---notification-58-2195`, `render-mobile---settings---notification-58-2279`; `design-description` §482). La decisione vincolante è ora esplicita per origine umana: `clarification:4da29b06-1b37-43e7-a898-8e2d9eb5d71c` conferma che gli interruttori regolano soltanto le email per categoria e che non esistono opt-out in-app per categoria. Disattivare un’email lascia attiva la notifica in-app corrispondente nell’inbox approvato; gli stati di lettura della notifica e della conversazione restano distinti. L’etichetta “Preferenze email” rende visibile questo significato senza introdurre una regola ulteriore.

Le impostazioni generali mostrano lingua, fuso orario, formato 12/24 ore e Save Changes nelle composizioni desktop/mobile (`render-web---settings---general-53-3034`, `render-mobile---settings---general-55-2018`). Il design descrive i controlli, ma non stabilisce i valori disponibili o il comportamento di salvataggio in caso di errore; nessuna regola Work qui esaminata fa dipendere da ciò il flusso principale. Questi dettagli possono essere definiti durante il design/implementazione senza cambiare regole di accesso, consegna o notifiche.

## Stati visibili e criteri di accettazione frontend

- Dashboard ed elenchi rispettano la visibilità per ruolo; un link diretto a un’attività non accessibile non ne rivela i dati.
- Lo studente distingue i cinque stati dell’attività; in revisione non significa completata; dopo completamento non può modificare o reinviare.
- L’invio accettato produce una versione, mostra il relativo esito e lo stato di ritardo. Formato o limiti non validi e upload fallito/annullato/interrotto non producono una versione, non alterano le precedenti e mostrano un motivo correggibile.
- Solo il mentor assegnato può valutare una versione, completare o richiedere correzioni motivate; un esito su versione superata non viene presentato come esito della versione corrente.
- In tutte le composizioni desktop/mobile, notifiche e conversazioni hanno stati di lettura distinti; l’azione “Segna come letta” modifica soltanto la notifica selezionata e aggiorna il conteggio del badge.
- Le quattro preferenze email non sopprimono le notifiche in-app per la categoria corrispondente e non esistono interruttori di opt-out in-app per categoria (`clarification:4da29b06-1b37-43e7-a898-8e2d9eb5d71c`).

## Responsive, accessibilità e fedeltà visiva

I render forniscono pattern desktop e mobile per dashboard, attività, mentor, messaggi e impostazioni; desktop usa barra laterale e aree affiancate, mobile collassa la navigazione e impila i contenuti. La chat mobile è una vista separata dalla lista. Mantenere equivalenza di permessi, azioni e stati tra i due formati, adattando la composizione ai frame (`design-description` §466–472; `work`, richiesta di usare Figma come riferimento desktop/mobile).

La libreria visiva rappresenta pulsanti abilitati, disabilitati e con focus (`render-button-2-47116`). I frame non specificano ulteriori requisiti espliciti di accessibilità, standard, uso da tastiera o annunci assistivi. Non è quindi possibile attestare conformità a uno standard dai soli render; i controlli e gli stati devono comunque restare comprensibili e distinguibili nell’interfaccia realizzata.

## Fattibilità verificata e limiti

Il repository frontend fornito, `https://github.com/demeedogg/task-managment-frontend`, branch `main`, commit `5ef7900b2fbc037b03f50c58a6fdba9d8ee9c7bd`, contiene soltanto README: non risultano codice UI, configurazione, sessione, integrazione, gestione responsive o test (`analysis:task-managment-frontend-8577187c`; identità e percorso in `repositories`). Il frontend è quindi da realizzare; non è possibile verificare compatibilità con comportamento esistente.

Il repository backend fornito, `https://github.com/demeedogg/task-managment-backend`, branch `main`, commit `4985e4cfb8d0135b7aecf7b1b6e7412d1e443396`, contiene soltanto README e non offre implementazione verificabile per permessi, versioni, validazione file, conflitti o notifiche (`analysis:task-managment-backend-21c6dc4a`; `repositories`). La fattibilità end-to-end di questi esiti resta da verificare quando esisterà il backend; questa analisi non prescrive endpoint o contratti tecnici. Non sono stati eseguiti build, test, applicazioni o integrazioni di rete e nessun repository è stato modificato.

## Chiarimenti materiali e incertezze residue

Non rimangono blocker frontend nel materiale esaminato: i chiarimenti accettati `clarification:15ef4e45-31a4-4e93-8d66-63bdcdfe7969`, `clarification:9970c26d-d463-4f30-87b0-4449d9a5ea8a`, `clarification:250d30b1-5b0e-4478-8a06-ac8db516bc7f` e `clarification:4da29b06-1b37-43e7-a898-8e2d9eb5d71c` fissano i flussi precedentemente mancanti. In particolare, l’ambiguità di canale in `design-description` §482 è risolta dalla decisione umana: i quattro controlli sono solo preferenze email, non esistono opt-out in-app per categoria e disattivare un’email non spegne la notifica in-app corrispondente. L’etichetta del gruppo dei controlli chiarisce il canale e non richiede una diversa regola di prodotto.

Restano dettagli non bloccanti di composizione/feedback (per esempio se la lista notifiche sia resa come pagina, pannello o altra forma responsive, scelta espressamente lasciata al design dalla terza chiarificazione) e specifiche opzioni di ricerca/filtri non enumerate nei render. Non si inferiscono comportamenti business da valori campione o da affordance il cui esito non è mostrato.
