---
reviewDomain: backend
reviewRound: 2
evidenceDigest: 706bfc9b44fd85a4780e5c7234787486714d406acbd465679bff76166c8ac38a
evidenceRefs:
  - work
  - clarification:13a21ba9-7523-4d52-8810-86c8c18d2213
  - clarification:78331b3f-90e4-488c-8224-3e07ba80a770
  - clarification:b3df12f5-2538-4757-9446-11caa0b9315a
  - clarification:cfa8fc71-eefc-424c-96ba-05cf48a52d01
  - clarification:d2b1f4e7-a787-4bf0-8d03-e43b21ff1118
  - clarification:db9caab7-1536-4717-9c2c-47e4a580e88c
  - clarification:f43ef6d1-8449-4f3b-9a47-9ea743d6ad5b
  - design-description
  - analysis:backend-template-ba4f4065
  - analysis:task-managment-backend-21c6dc4a
  - analysis:task-managment-frontend-8577187c
  - repositories
  - review:previous:backend
  - review:working-documents
blockedQuestionIds: []
reviewStatus: ready
---

# Requirements Review backend — TASK MANAGMENT

## Modifica rispetto al predecessore

Il contenuto di prodotto e fattibilità del predecessore `review:previous:backend` resta invariato. Questa versione aggiorna solo la provenienza di BE-REV-01: l’interazione `clarification:13a21ba9-7523-4d52-8810-86c8c18d2213` riconferma senza modifiche il comportamento sulle valutazioni obsolete. L’Interaction ID `6a9a330f-5be8-4d29-a473-76cb61c38dff` resta indicato solo come origine storica ripetuta; non è usato come evidenceRef in questo round.

## Esito e perimetro

Non restano domande materiali di comportamento backend da chiarire. Le precedenti domande Q-BE-02 (scadenze), Q-BE-04 (capacità email), Q-BE-06 (destinatari delle conversazioni) e Q-BE-07 (limiti di file e allegati) sono risolte dalle fonti umane e dal perimetro di accesso accettato; le loro conseguenze sono specificate qui. L’estensione visuale del flusso mentor è approvata, senza cambiare le regole di stato lato backend.

`review:working-documents` e il controllo del percorso assegnato indicano che questo file non aveva una versione precedente né un recupero da riconciliare. La fonte comportamentale primaria è `work`, che dichiara l’applicazione da realizzare, nomina il backend target e stabilisce che Figma sia riferimento visivo mentre i requisiti testuali stabiliscono le regole di business. Le chiarificazioni umane accettate sono citate separatamente; analisi di repository e design attestano lo stato osservato, non aggiungono requisiti.

## Identità, ruoli e autorizzazioni

**BE-AUTH-01 — Autenticazione e provisioning.** L’app fornisce l’autenticazione. Solo personale autorizzato attribuisce o revoca ruoli di studente, mentor e personale addetto alle assegnazioni; gli utenti non possono attribuirsi ruoli privilegiati. Origine umana: `clarification:b3df12f5-2538-4757-9446-11caa0b9315a`, campi question/answer/acceptance (righe 7–10). Non è specificato un metodo tecnico di autenticazione, né viene scelto qui.

**BE-AUTH-02 — Scope di lettura e mutazione.** Lo studente accede solo alle proprie attività e conversazioni. Il mentor accede agli studenti attualmente assegnati e alle attività autorizzate di quegli studenti; l’elenco pubblico dei mentor o un controllo “Follow” non concede accesso a uno studente, alle sue attività o alle sue conversazioni. Il controllo vale anche per accessi diretti a una risorsa e per dashboard, notifiche, cronologie e operazioni di mutazione. Origini: `work`, “Regole di business” § 1; `clarification:cfa8fc71-eefc-424c-96ba-05cf48a52d01`, accettazione sul registro autorevole e sull’assegnazione corrente (righe 7–10); `design-description`, directory mentor e messaggi (righe 146–179).

**BE-AUTH-03 — Riassegnazione e cronologia.** Un registro autorevole, gestito da personale autorizzato, determina l’assegnazione corrente e quindi l’accesso del mentor. Dopo una riassegnazione:

- il nuovo mentor può accedere al lavoro corrente e alla cronologia di versioni e valutazioni necessaria per continuare la revisione;
- il mentor precedente perde l’accesso alle attività e alle conversazioni dello studente;
- lo studente conserva la propria cronologia completa di attività, versioni, valutazioni e conversazioni;
- le conversazioni storiche non vengono condivise con il nuovo mentor.

Origine umana: `clarification:cfa8fc71-eefc-424c-96ba-05cf48a52d01`, accettazione della proposta di riassegnazione (righe 7–10). Un accesso diretto o una conversazione preesistente non deve aggirare l’assegnazione corrente.

**BE-AUTH-04 — Bootstrap iniziale del personale.** Il prodotto non permette auto-assegnazione di privilegi. Prima del rilascio, un operatore autorizzato deve fornire in modo controllato il primo account di personale autorizzato; poi il provisioning e la revoca dei ruoli seguono BE-AUTH-01. La persona e la procedura operativa vanno assegnate in Delivery: non sono determinate dalle fonti funzionali né implementate nei checkout. È un prerequisito operativo, non una domanda di prodotto.

## Attività, consegne e scadenze

**BE-LIFE-01 — Stati e transizioni.** L’attività ha gli stati `da iniziare`, `in corso`, `in revisione`, `da correggere` e `completata`. Lo studente può avviarla e inviarla in revisione; il mentor attualmente assegnato può completarla oppure richiedere correzioni con motivazione; lo studente non può modificare un’attività completata. Una richiesta senza la motivazione richiesta non è una decisione valida. Origine: `work`, “Regole di business” § 2; `analysis:task-managment-backend-21c6dc4a`, riga 19 come riscontro dei requisiti.

**BE-SUB-01 — Versioni immutabili e invio accettato.** Ogni consegna accettata è una nuova versione, con autore e istante di accettazione; la versione e la valutazione ad essa collegata restano identificabili. Un invio ripetuto dovuto a retry o doppia attivazione non deve creare una versione duplicata; modifiche concorrenti non devono sovrascrivere silenziosamente uno stato più recente. La decisione del mentor riguarda una versione precisa. Origine: `work`, “Regole di business” §§ 3–4; `analysis:task-managment-backend-21c6dc4a`, righe 20–21.

**BE-SUB-02 — Limiti e failure di consegna.** Una consegna accetta un solo file, massimo 25 MiB, nei formati PDF, DOCX, PPTX, JPEG o PNG. Un upload incompleto, interrotto o fuori limite non crea una versione e non sostituisce quella corrente; lascia invariati contenuto accettato e stato dell’attività. Un invio tardivo conforme ai limiti è accettato, con indicazione del ritardo. Origine umana: `clarification:db9caab7-1536-4717-9c2c-47e4a580e88c`, domanda/risposta/accettazione (righe 7–10), con i limiti e gli esiti accettati nell’interazione umana.

**BE-DUE-01 — Calcolo puntuale/tardivo.** Ogni scadenza è un istante preciso nel fuso dichiarato per l’attività. La puntualità si calcola all’ora della consegna accettata: al momento esatto della scadenza o prima è puntuale; dopo è tardiva. Un’attività senza scadenza non è tardiva. Il fuso dell’utente modifica la presentazione dell’istante, non il confine di accettazione. Origine umana: `clarification:f43ef6d1-8449-4f3b-9a47-9ea743d6ad5b`, domanda/risposta/accettazione (righe 7–10). `analysis:backend-template-ba4f4065`, riga 23, conferma la necessità di distinguere l’ora di invio da quella di revisione; non introduce un diverso criterio.

**BE-REV-01 — Rifiuto atomico della decisione obsoleta.** Se, quando il mentor conferma la decisione, è già stata accettata una versione più recente di quella esaminata, la decisione obsoleta viene rifiutata atomicamente: nessuna transizione di stato, valutazione, completamento o richiesta di correzione; nessuna notifica di completamento o correzione. La versione corrente resta `in revisione`; le versioni e valutazioni precedenti restano intatte. Il mentor riceve esattamente: «È disponibile una nuova versione della consegna. Aprila e verifica il contenuto prima di valutarla». L’ordine concorrente è risolto rispetto allo stato corrente al momento della conferma, incluso un invio accettato immediatamente prima. Origine umana corrente: `clarification:13a21ba9-7523-4d52-8810-86c8c18d2213`, domanda/risposta/accettazione (righe 7–10), che riconferma integralmente la risposta originaria dell’Interaction ID `6a9a330f-5be8-4d29-a473-76cb61c38dff`; ancoraggio ai requisiti di versionamento/concorrenza in `work`, “Regole di business” §§ 3–4, e `analysis:task-managment-backend-21c6dc4a`, righe 20–21. Il contenuto coincide con BE-REV-01 in `review:previous:backend`.

## Conversazioni, messaggi e notifiche

**BE-MSG-01 — Destinatario della conversazione.** L’accesso alle conversazioni segue l’assegnazione corrente; l’unico mentor ammesso a iniziare o ricevere una nuova conversazione con lo studente è il mentor attualmente assegnato. “Follow” nella directory non autorizza la messaggistica. Alla riassegnazione, lo studente conserva la conversazione precedente, che non è visibile né al mentor precedente né a quello nuovo; lo studente può iniziare nuove conversazioni con il mentor corrente. Questo applica il controllo sull’assegnazione accettato per le conversazioni, senza aggiungere un’eccezione per mentor non assegnati. Fonti: `work`, §§ 1 e 6; `clarification:cfa8fc71-eefc-424c-96ba-05cf48a52d01`, righe 7–10; `design-description`, righe 160–179.

**BE-MSG-02 — Limiti e invio messaggi.** Il testo del messaggio è limitato a 10.000 caratteri e può avere al massimo un allegato JPEG o PNG di 10 MiB. Un allegato incompleto, interrotto o fuori limite non invia il messaggio. Origine umana: `clarification:db9caab7-1536-4717-9c2c-47e4a580e88c`, righe 7–10 e limiti accettati nell’interazione. Lo stato di lettura della conversazione resta distinto da quello della notifica; gli indicatori grafici Figma non definiscono ulteriori semantiche (`design-description`, righe 160–179).

**BE-NOT-01 — Notifiche in-app ed email.** Le notifiche in-app restano attive indipendentemente dalle preferenze email. Il sistema evita duplicati per lo stesso evento e destinatario secondo le categorie/eventi definiti da Work. Un errore email non annulla né modifica l’azione attività già registrata e non annulla la notifica in-app. La capacità email in uscita, con owner operativo, è autorizzata; se non esiste una capacità autorizzata, ne è autorizzata l’introduzione. Origine umana: `clarification:78331b3f-90e4-488c-8224-3e07ba80a770`, domanda/risposta/accettazione (righe 7–10); fonte del comportamento di notifica: `work`, “Regole di business” § 6.

Le schermate impostazioni mostrano categorie di notifica e preferenze generali ma non precisano un servizio email o stati di consegna (`design-description`, righe 181–207). La separazione dei canali e gli esiti sopra derivano da Work e dalla chiarificazione accettata, non dai valori d’esempio nel design.

## Dashboard e coerenza dei dati

**BE-DASH-01 — Aggregazioni autorizzate e filtri.** Conteggi, percentuali e liste usano solo attività visibili all’attore e rispettano i filtri/intervalli definiti da Work; KPI e lista corrispondente non devono usare scope o intervalli incompatibili. Solo lo stato `completata` conta come completamento; `in revisione` non equivale a completata. I valori numerici e i progressi esemplificati nei frame sono dati visivi di esempio, non formule di business (`work`, “Regole di business” § 5; `analysis:task-managment-backend-21c6dc4a`, riga 22; `design-description`, `render-web---dashboard-6-2335`, righe 209–214). Nessuna aggregazione può esporre dati di studenti fuori dallo scope autorizzato.

## Estensione visuale e comportamento comune ai client

**BE-UX-01 — Flusso mentor approvato.** Il mentor accede a una lista di consegne dei soli studenti attualmente assegnati e a un dettaglio role-specifico che identifica studente, versione corrente e cronologia pertinente, espone completamento o richiesta di correzione con motivazione obbligatoria e mostra esito/versione. Una decisione obsoleta mostra il messaggio di BE-REV-01. La medesima funzionalità è disponibile su mobile. Origine umana: `clarification:d2b1f4e7-a787-4bf0-8d03-e43b21ff1118`, approvazione della proposta visuale (righe 7–10); Work, § 2; `design-description`, righe 237–263. Questa estensione colma un’assenza dei frame e non modifica le transizioni o i permessi già stabiliti.

**BE-UX-02 — Parità desktop/mobile.** Desktop e mobile devono applicare le stesse regole di autorizzazione, validazione, stati, versioni, scadenze, fallimenti e risultati. La disposizione può differire; nessuna differenza di layout deve cambiare l’esito di una richiesta o rendere disponibile una funzione a un attore non autorizzato. Fonte: `work`, regola desktop/mobile; riscontro in `analysis:task-managment-backend-21c6dc4a`, riga 24.

## Fattibilità, limiti della verifica e prerequisiti di delivery

**BE-FEAS-01 — Target richiesto.** Il backend target resta `https://github.com/demeedogg/task-managment-backend`, branch `main`, commit `4985e4cfb8d0135b7aecf7b1b6e7412d1e443396` (`repositories`, righe 2–6). Nel checkout analizzato è presente solo un README; non sono verificabili applicazione, autenticazione, persistenza, migrazioni, storage, email, configurazione o test (`analysis:task-managment-backend-21c6dc4a`, righe 3–14). La realizzazione del backend è quindi greenfield rispetto a questo snapshot, coerentemente con Work.

`analysis:backend-template-ba4f4065` riguarda invece `https://github.com/lucacimino-reply/backend-template.git`, branch `node-express`, commit `04e67bcedfdc2226ae6e24aa6e54a5ded09e3e67` (`repositories`, righe 14–20). L’analisi segnala esplicitamente che è un repository separato e un template incompleto, non il servizio task-management nominato da Work (`analysis:backend-template-ba4f4065`, righe 5–15). Non viene trattato come target né come prova di funzionalità applicative. Un suo eventuale uso in sostituzione del target richiederebbe una distinta autorizzazione; questa review non lo propone.

**BE-FEAS-02 — Storage ed email.** Non è stata verificata la presenza attuale di capacità autorizzate di archiviazione o email nei checkout (`analysis:task-managment-backend-21c6dc4a`, righe 5–14 e 23; `analysis:backend-template-ba4f4065`, righe 7, 14–15 e 26). Le chiarificazioni `clarification:db9caab7-1536-4717-9c2c-47e4a580e88c` e `clarification:78331b3f-90e4-488c-8224-3e07ba80a770` autorizzano e richiedono le capacità con un owner operativo; per l’email è esplicitamente consentito introdurla se non disponibile. Identificazione degli owner, verifica della capacità complessiva e provisioning sono prerequisiti di Delivery e di rilascio, non autorizzazioni o scelte di prodotto ancora pendenti. Nessun provider o meccanismo di storage/email è prescritto.

**BE-FEAS-03 — Limiti di risorse.** I limiti per singolo file e messaggio sono definiti da `clarification:db9caab7-1536-4717-9c2c-47e4a580e88c`. L’owner operativo deve verificare che capacità complessiva, frequenza di invio e conservazione delle versioni/storico possano rispettare tali limiti e i requisiti di cronologia. Nessuna configurazione locale prova tale capacità; definire controlli operativi coerenti, senza perdere versioni accettate o violare la cronologia approvata, è un prerequisito di delivery e non lascia un’ulteriore domanda di prodotto.

La review documentale è `ready` e `blockedQuestionIds` è vuoto: non resta un blocco materiale backend che richieda un’altra decisione umana. “Fattibilità non verificata nel checkout” non significa che i servizi siano già presenti; significa che la realizzazione e la verifica operativa appartengono alla delivery autorizzata.

## Riferimenti usati

I riferimenti consentiti citati in questo documento sono: `work`; `clarification:13a21ba9-7523-4d52-8810-86c8c18d2213`; `clarification:78331b3f-90e4-488c-8224-3e07ba80a770`; `clarification:b3df12f5-2538-4757-9446-11caa0b9315a`; `clarification:cfa8fc71-eefc-424c-96ba-05cf48a52d01`; `clarification:d2b1f4e7-a787-4bf0-8d03-e43b21ff1118`; `clarification:db9caab7-1536-4717-9c2c-47e4a580e88c`; `clarification:f43ef6d1-8449-4f3b-9a47-9ea743d6ad5b`; `design-description`; `analysis:backend-template-ba4f4065`; `analysis:task-managment-backend-21c6dc4a`; `analysis:task-managment-frontend-8577187c`; `repositories`; `review:previous:backend`; `review:working-documents`.

L’Interaction ID `6a9a330f-5be8-4d29-a473-76cb61c38dff` è riportato solo come origine storica richiamata dalla chiarificazione corrente; non è inventato o aggiunto come evidenceRef. Non sono stati eseguiti build, test, applicazioni o integrazioni.
