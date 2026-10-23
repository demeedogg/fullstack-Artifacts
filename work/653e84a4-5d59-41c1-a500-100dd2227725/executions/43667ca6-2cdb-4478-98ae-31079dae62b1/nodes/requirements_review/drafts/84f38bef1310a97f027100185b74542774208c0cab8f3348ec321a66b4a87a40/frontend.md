---
reviewDomain: frontend
reviewRound: 1
evidenceDigest: 6bc864aa9b692a5c66a0127a440130bd6a5076cd7c82d919fb8f1464a3741960
evidenceRefs:
  - work
  - analysis:backend-template-ba4f4065
  - analysis:task-managment-backend-21c6dc4a
  - analysis:task-managment-frontend-8577187c
  - clarification:78331b3f-90e4-488c-8224-3e07ba80a770
  - clarification:b3df12f5-2538-4757-9446-11caa0b9315a
  - clarification:cfa8fc71-eefc-424c-96ba-05cf48a52d01
  - clarification:d2b1f4e7-a787-4bf0-8d03-e43b21ff1118
  - clarification:db9caab7-1536-4717-9c2c-47e4a580e88c
  - clarification:f43ef6d1-8449-4f3b-9a47-9ea743d6ad5b
  - design-description
  - repositories
  - review:working-documents
blockedQuestionIds: []
reviewStatus: ready
---

# Revisione requisiti frontend — TASK MANAGMENT

## Esito e perimetro

Non restano domande materiali sul comportamento frontend nel perimetro analizzato: le risposte umane accettate hanno definito autenticazione/ruoli, assegnazioni e storico, limiti di upload, scadenze, capacità email e l’estensione visuale per il mentor. `blockedQuestionIds` è quindi vuoto e lo stato è `ready`. Rimangono estensioni di design necessarie per rendere visibili flussi già richiesti e dipendenze operative da realizzare/verificare in Delivery.

Work definisce l’app per studenti e mentor e cita dashboard, attività, mentor, messaggi, notifiche e impostazioni; il Figma è riferimento visuale, mentre le regole di business provengono dal testo di Work (`work`: `work.description` → `OBIETTIVO E REQUISITI`, `Ambito`, `Regole di business` 1–7). I fatti visuali qui sotto sono distinti dalle regole: nomi, date, conteggi e profili nei render sono dati esemplificativi, non permessi o semantica del prodotto (`design-description`, righe 3, 314–326, 498–504).

La revisione considera i chiarimenti umani accettati elencati nell’indice corrente: autenticazione e ruoli (`clarification:b3df12f5-2538-4757-9446-11caa0b9315a`); assegnazione/riassegnazione e visibilità storica (`clarification:cfa8fc71-eefc-424c-96ba-05cf48a52d01`); limiti dei file e capacità di archiviazione autorizzata con responsabile operativo (`clarification:db9caab7-1536-4717-9c2c-47e4a580e88c`); scadenze (`clarification:f43ef6d1-8449-4f3b-9a47-9ea743d6ad5b`); capacità di invio email in uscita con responsabile operativo (`clarification:78331b3f-90e4-488c-8224-3e07ba80a770`); estensione visuale del flusso mentor (`clarification:d2b1f4e7-a787-4bf0-8d03-e43b21ff1118`).

## Findings e comportamento osservabile

### FE-AUTH-01 — Identità, ruoli, assegnazioni e accesso diretto

**Origine:** Work regola 1; chiarimenti umani accettati `clarification:b3df12f5-2538-4757-9446-11caa0b9315a` e `clarification:cfa8fc71-eefc-424c-96ba-05cf48a52d01`. I render mostrano un utente studente autenticato e shell desktop/mobile, ma non autenticazione o stati di autorizzazione (`design-description`, righe 3, 104–116, 499–504).

- L’app usa l’autenticazione fornita dal prodotto. Ruoli studente, mentor e personale assegnatario sono attribuiti/revocati solo da personale autorizzato; l’interfaccia non offre auto-registrazione con scelta del ruolo, auto-promozione o auto-assegnazione.
- Lo studente vede le proprie attività e conversazioni. Il mentor vede solo gli studenti attualmente assegnati e le attività pertinenti. L’assegnazione corrente nel registro autorizzato è la fonte di accesso; Follow nella directory non equivale ad assegnazione né autorizza accesso.
- Alla riassegnazione, il nuovo mentor vede il lavoro corrente e lo storico di versioni e valutazioni pertinenti a proseguire la revisione; non vede le conversazioni storiche del mentor precedente. Il mentor precedente perde accesso alle attività e conversazioni dello studente. Lo studente conserva tutto il proprio storico.
- Un link diretto a una risorsa non autorizzata non deve mostrare dati. Con sessione assente/scaduta, il client usa l’autenticazione del prodotto; con ruolo o assegnazione mancante/revocata, mostra un esito neutro di accesso non consentito, rimuove i dati protetti dalla vista e offre ritorno a un’area consentita. Non esporre nome, attività o versione non autorizzati.
- Raccomandazione UX derivata: la conversazione col mentor precedente rimane nello storico dello studente come archivio separato, non modificabile; una conversazione col nuovo mentor è distinta e non eredita messaggi precedenti. Ciò preserva lo storico dello studente senza dare al nuovo o al vecchio mentor accesso non autorizzato.

**Conseguenza se omesso:** nascondere soltanto i link non impedisce l’accesso diretto né la persistenza di dati non più autorizzati in una vista aperta. **Cross-domain:** il backend deve applicare assegnazione e ruoli a ogni lettura e mutazione; il frontend rende i risultati e non sostituisce l’autorizzazione server-side.

### FE-MENTOR-01 — Lista assegnazioni e dettaglio di revisione del mentor

**Origine:** Work regole 1–2; estensione visuale accettata da `clarification:d2b1f4e7-a787-4bf0-8d03-e43b21ff1118`. Il Figma non mostra questa esperienza: il dettaglio desktop/mobile mostra upload e Submit per lo studente (`design-description`, righe 132–144, 237–249, 342–354); le pagine Mentor sono directory di profili senza studenti assegnati o attività (`design-description`, righe 146–158, 251–263, 356–368).

- Nel punto Task aggiungere la lista del lavoro assegnato al mentor, con studenti autorizzati e stato delle attività. L’apertura porta a un dettaglio specifico del mentor che identifica lo studente, la versione corrente e lo stato.
- Il dettaglio mostra le versioni e valutazioni precedenti pertinenti e le azioni autorizzate: completare oppure richiedere correzioni. La richiesta di correzioni richiede una motivazione non vuota; il risultato e la motivazione devono essere visibili allo studente sulla consegna interessata.
- La vista mobile mantiene lista, identità dello studente, versione corrente, storico pertinente, azioni e feedback; può riordinare i contenuti ma non omettere capacità o controlli.
- In caso di decisione sulla versione superata, mantenere il comportamento stabilito dalla risposta umana precedente (Interaction ID `6a9a330f-5be8-4d29-a473-76cb61c38dff`; non presente come `evidenceRef` nell’indice corrente): rifiuto atomico, nessuna mutazione/valutazione/notifica di completamento o correzione, versione corrente ancora in revisione, storico preservato. Mostrare esattamente: «È disponibile una nuova versione della consegna. Aprila e verifica il contenuto prima di valutarla». Il mentor deve poter aprire e verificare la nuova versione prima di rivalutarla. Work regola 4 mantiene il vincolo di non applicare silenziosamente una decisione obsoleta alla versione nuova (`work`: `work.description` → regola 4).

**Conseguenza se omesso:** il mentor non ha un percorso per effettuare la revisione richiesta; lo studente non può distinguere revisione, correzione richiesta e completamento. **Cross-domain:** backend fornisce lista scope-assignment, versioni, valutazioni e rifiuto stale senza side effects. La forma della lista e del dettaglio è approvata; restano scelte di impaginazione, non blocker di prodotto.

### FE-SUBMIT-01 — Ciclo attività, versioni, file e feedback

**Origine:** Work regole 2–4; chiarimento `clarification:db9caab7-1536-4717-9c2c-47e4a580e88c`. I frame task mostrano progresso e gruppi “Time Limit”/“New Task”, non gli stati richiesti; il dettaglio espone file drop e Submit ma nessun badge di stato, versione, scadenza tardiva, feedback o storico (`design-description`, righe 121–144, 223–249, 328–354).

- Rappresentare gli stati da iniziare, in corso, in revisione, da correggere e completata con etichette esplicite. Non dedurre completamento dalle percentuali, barre o spunte di checklist (`design-description`, righe 212–228, 501).
- Consentire allo studente di iniziare e inviare in revisione; consentire al solo mentor assegnato completamento/richiesta di correzione; rendere la consegna completata non modificabile dallo studente.
- Mostrare quale versione è corrente/in revisione e rendere consultabili le precedenti con le valutazioni pertinenti. L’upload studente accetta al massimo un file PDF, DOCX, PPTX, JPEG o PNG, dimensione massima 25 MiB. Mostrare i limiti prima della selezione.
- Se il file è incompleto o fuori limite, non creare né sostituire la versione corrente. Segnalare l’errore presso il controllo, mantenere visibile la versione già accettata e consentire correzione/riprova. Non mostrare conferma di successo prima dell’accettazione della nuova versione.
- Feedback su invio riuscito, upload fallito, stato in revisione, correzione richiesta e completamento. L’invio tardivo è ammesso e marcato come tardivo; una versione inviata puntualmente resta puntuale anche se valutata dopo la scadenza.

**Conseguenza se omesso:** l’utente non sa quale contenuto è salvato o sotto revisione e può confondere una bozza/upload incompleto con una nuova versione. **Cross-domain:** persistenza/versionamento e limiti validati dal servizio; il frontend conserva la distinzione tra file in preparazione e versione accettata.

### FE-DATE-01 — Visualizzazione delle scadenze

**Origine:** chiarimento umano `clarification:f43ef6d1-8449-4f3b-9a47-9ea743d6ad5b`; Work regola 3; Figma mostra “days left”, calendario e selezione timezone ambigua (`design-description`, righe 212–235, 286–298).

- Ogni attività ha un istante preciso interpretato nel fuso dell’attività. Confrontare l’istante di consegna accettata: al o prima del limite è puntuale, dopo è tardiva. Senza deadline non esiste stato “in ritardo”. Il fuso dell’utente modifica soltanto la visualizzazione.
- Presentare lo stesso istante su dashboard, lista, dettaglio studente e revisione mentor, convertito nel fuso selezionato dall’utente e con indicazione del fuso mostrato. L’esito puntuale/tardivo non cambia tra utenti o in base all’istante della valutazione.
- Correggere “English (Default)” nel controllo timezone usando un valore di fuso reale; rinominare il gruppo 12/24 ore “Formato orario”.

**Conseguenza se omesso:** schermate o utenti possono mostrare confini apparenti diversi per la stessa consegna. **Cross-domain:** il servizio fornisce l’esito basato sull’istante accettato e sul fuso dell’attività; il client formatta la data senza ricalcolare la regola.

### FE-MESSAGE-01 — Destinatari, allegati e notifiche

**Origine:** Work regole 1 e 6; chiarimenti `clarification:cfa8fc71-eefc-424c-96ba-05cf48a52d01`, `clarification:db9caab7-1536-4717-9c2c-47e4a580e88c` e `clarification:78331b3f-90e4-488c-8224-3e07ba80a770`; `design-description`, righe 160–179, 265–284, 300–312, 498–504.

- Derivazione dalle regole di assegnazione e conversazione: lo studente può inviare messaggi al mentor attualmente assegnato; un mentor non assegnato o precedente non ottiene accesso perché appare nella directory o è seguito. Lo storico conversazioni resta allo studente, ma non è condiviso col nuovo mentor.
- Il messaggio consente fino a 10.000 caratteri e al massimo una immagine JPEG/PNG fino a 10 MiB. Se l’upload è incompleto o input/allegato fuori limite, non inviare il messaggio. Mostrare errore specifico e conservare il draft/allegato per correggere o ritentare; non presentare un invio parziale come riuscito.
- Etichettare i quattro switch Message, Task Update, Task Deadline, Mentor Help come preferenze **email**. Le notifiche in-app restano attive se l’email è disabilitata.
- Il campanello deve aprire le notifiche in-app e lo stato letto/non letto deve restare indipendente dallo stato della conversazione. Figma mostra campanello e indicatori distinti ma non l’elenco né l’azione di lettura (`design-description`, righe 268–277, 502).
- Se l’azione primaria (consegna/valutazione) riesce ma l’invio email fallisce, mostrare l’azione primaria come riuscita e mantenere la notifica in-app. L’esito email, se visibile, è feedback separato e non deve indurre l’utente a ripetere consegna/valutazione.

**Conseguenza se omesso:** possibili invii a mentor non autorizzati, perdita di draft o confusione tra notifica, messaggio e azione task. **Cross-domain:** controlli di membership, limite/accettazione allegati, letture separate e consegna email disaccoppiata sono responsabilità del backend/capability di delivery.

### FE-DASH-01 — Dashboard e liste coerenti

**Origine:** Work regole 5 e 7; `analysis:task-managment-frontend-8577187c`, righe 23, 29; `design-description`, righe 209–235, 498–504.

Filtrare dashboard e liste sul perimetro autorizzato; contare come completate soltanto attività nello stato completato. Usare definizioni coerenti tra KPI, intervalli/filtri e liste correlate. Percentuali, anello “Running Task”, barre progresso e checklist del Figma non costituiscono da sole la semantica degli stati. Mobile deve mantenere filtri, dati, deadline, stati e azioni funzionalmente equivalenti a desktop; l’impaginazione può adattarsi.

## Stati di errore, accessibilità e criteri di accettazione osservabili

I frame includono skeleton/loading ma non stati vuoti, errori, dinieghi o recupero (`design-description`, righe 419–504). Integrare almeno: sessione scaduta; risorsa non autorizzata senza rivelare dati; errore di caricamento e retry; upload invalido/incompleto senza nuova versione; messaggio non inviato senza perdita del draft; conflitto/stale decision; salvataggio impostazioni fallito; successo del task distinto da email fallita. Il Figma presenta controlli icon-only; dare loro nomi accessibili e feedback leggibile/operabile anche da tastiera. Non è specificato uno standard WCAG o un breakpoint numerico; nessun requisito mobile può ridurre capacità rispetto al desktop.

Criteri di accettazione frontend osservabili:

1. Studente e mentor ricevono solo navigation e dati autorizzati; un accesso diretto fuori scope non mostra contenuto protetto.
2. Mentor raggiunge la lista di lavoro assegnato, apre lo studente/versione corrente, completa oppure chiede correzione con motivazione obbligatoria; gli stessi esiti sono utilizzabili da mobile.
3. Upload valido crea una nuova versione solo dopo accettazione. Nessun file incompleto/fuori limite sostituisce la versione corrente. Invio puntuale/tardivo e attività senza scadenza sono mostrati secondo FE-DATE-01.
4. La decisione su versione superata produce il rifiuto e il feedback concordati, non un falso successo. **Provenienza:** Interaction ID `6a9a330f-5be8-4d29-a473-76cb61c38dff` (risposta umana precedente; non è un `evidenceRef` dell’indice attuale). Dopo il rifiuto, il mentor apre e verifica la versione più recente prima di riprovare.
5. Un messaggio valido è inviato al mentor assegnato; testo/allegato non valido o upload incompleto non invia il messaggio e conserva input correggibile.
6. Disattivare email non elimina notifiche in-app. Email fallita non cambia stato task, esito visualizzato dell’azione o disponibilità della notifica in-app.
7. Scadenza, stato puntuale/tardivo, versioni, azioni e feedback sono coerenti tra desktop/mobile e viste autorizzate di studente/mentor.

## Feasibility e limiti di verifica

Il checkout frontend identificato da `repositories` (`https://github.com/demeedogg/task-managment-frontend`, `main` @ `5ef7900b2fbc037b03f50c58a6fdba9d8ee9c7bd`) contiene solo un README titolo; non ci sono app, configurazione o test (`analysis:task-managment-frontend-8577187c`, righe 5–17). Il backend nominato da Work (`https://github.com/demeedogg/task-managment-backend`, `main` @ `4985e4cfb8d0135b7aecf7b1b6e7412d1e443396`) contiene solo README, senza codice, auth, API o schema (`analysis:task-managment-backend-21c6dc4a`, righe 5, 9–14). Il `backend-template` è un repository accessorio distinto, parziale, senza app/auth/dominio/email/storage; non va trattato come backend di prodotto o prova di funzionalità esistente (`analysis:backend-template-ba4f4065`, righe 5–7, 11–15, 21, 26, 41). Il Work nomina il backend task-management; il template resta evidenza di template, non sostituisce il target senza nuova autorizzazione.

Le chiarifiche accettate autorizzano le capacità di archiviazione e invio email necessarie con owner operativo, includendone l’introduzione se assenti (`clarification:db9caab7-1536-4717-9c2c-47e4a580e88c`, `clarification:78331b3f-90e4-488c-8224-3e07ba80a770`). Owner/capability devono quindi essere assegnati e verificati in Delivery: nei repository disponibili non sono dimostrati. Non costituiscono una domanda di prodotto frontend ancora aperta.

Analisi e verifica sono di sola lettura. Non sono stati eseguiti build, test, applicazioni o integrazioni. Le affermazioni di fattibilità runtime non sono verificabili da checkout privi di applicazione.

## Allineamento al documento funzionale condiviso

Il documento frontend non assegna ID all’AFU né ne modifica il registro. L’AFU deve riportare come comportamento vincolante le regole di visibilità/assegnazione, lifecycle/ruoli, versione e late state, limiti input, stale decision, messaggistica/notifiche/email, coerenza dashboard e parità desktop/mobile, preservando l’origine Work o human clarification per le rispettive decisioni.

## Fonti e stato dei working documents

L’indice corrente è `context/index.md`; Work e chiarifiche hanno digest `6bc864aa9b692a5c66a0127a440130bd6a5076cd7c82d919fb8f1464a3741960` (`work` e ciascuna chiarifica nel contesto corrente). La design description è `design-description`. Il frontend usa il repository evidence alla revisione indicata in `repositories` e le analisi `analysis:task-managment-frontend-8577187c`, `analysis:task-managment-backend-21c6dc4a`, `analysis:backend-template-ba4f4065`. L’inventario `review:working-documents` segnala tutti e tre i documenti assegnati missing, senza recovery (righe 1–22); questo documento è scritto solo nel percorso frontend assegnato.
