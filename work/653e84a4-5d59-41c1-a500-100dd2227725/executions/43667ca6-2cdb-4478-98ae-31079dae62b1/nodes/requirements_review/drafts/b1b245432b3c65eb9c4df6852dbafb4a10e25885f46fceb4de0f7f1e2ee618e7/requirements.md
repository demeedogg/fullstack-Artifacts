---
reviewDomain: requirements
reviewRound: 2
evidenceDigest: 706bfc9b44fd85a4780e5c7234787486714d406acbd465679bff76166c8ac38a
evidenceRefs:
  - work
  - design-description
  - clarification:13a21ba9-7523-4d52-8810-86c8c18d2213
  - clarification:78331b3f-90e4-488c-8224-3e07ba80a770
  - clarification:b3df12f5-2538-4757-9446-11caa0b9315a
  - clarification:cfa8fc71-eefc-424c-96ba-05cf48a52d01
  - clarification:d2b1f4e7-a787-4bf0-8d03-e43b21ff1118
  - clarification:db9caab7-1536-4717-9c2c-47e4a580e88c
  - clarification:f43ef6d1-8449-4f3b-9a47-9ea743d6ad5b
  - analysis:task-managment-backend-21c6dc4a
  - analysis:task-managment-frontend-8577187c
  - analysis:backend-template-ba4f4065
  - repositories
  - review:previous:requirements
  - review:previous:frontend
  - review:previous:backend
  - review:working-documents
blockedQuestionIds: []
reviewStatus: ready
---

# Analisi funzionale — TASK MANAGMENT

## 1. Documento, fonti e modifiche

Questa AFU è una revisione del predecessore `review:previous:requirements` (round 1). Ho letto il predecessore, il candidato conservato e il recovery indicati da `review:working-documents`, quindi ho riusato il contenuto coerente e aggiornato metadati e provenienza per round 2. La chiarificazione 13 conferma senza variazioni il comportamento stale già scritto; tutti gli ID AFU precedenti sono mantenuti, senza rimozioni o supersedes.

Fonti vincolanti e di contesto: `work`; `design-description`; chiarificazioni accettate `clarification:13a21ba9-7523-4d52-8810-86c8c18d2213`, `clarification:78331b3f-90e4-488c-8224-3e07ba80a770`, `clarification:b3df12f5-2538-4757-9446-11caa0b9315a`, `clarification:cfa8fc71-eefc-424c-96ba-05cf48a52d01`, `clarification:d2b1f4e7-a787-4bf0-8d03-e43b21ff1118`, `clarification:db9caab7-1536-4717-9c2c-47e4a580e88c`, `clarification:f43ef6d1-8449-4f3b-9a47-9ea743d6ad5b`; documenti precedenti `review:previous:requirements`, `review:previous:frontend`, `review:previous:backend`; inventory `review:working-documents`; analisi read-only `analysis:task-managment-backend-21c6dc4a`, `analysis:task-managment-frontend-8577187c`, `analysis:backend-template-ba4f4065` e `repositories`.

La chiarificazione accettata `clarification:13a21ba9-7523-4d52-8810-86c8c18d2213` conferma integralmente e senza modifiche il comportamento stale già autorizzato nella risposta all’Interaction storico `6a9a330f-5be8-4d29-a473-76cb61c38dff`. Il registro usa 13 come origine umana corrente e risolvibile; il precedente ID resta citato come contesto storico nell’answer, senza inventare un evidenceRef.

**[AFU-REQ-001](#provenance-AFU-REQ-001)** — Il prodotto consente agli studenti di seguire le proprie attività formative, consegnare il lavoro e comunicare con i mentor; i mentor verificano le consegne dei propri studenti assegnati.

**[AFU-REQ-002](#provenance-AFU-REQ-002)** — Lo scope comprende home/dashboard, elenco e dettaglio attività, elenco mentor, messaggi, notifiche e impostazioni rappresentati nel Figma, con comportamento funzionale disponibile su desktop e mobile. Il Figma è riferimento per l’esperienza visibile; le regole di business provengono dal testo Work.

**[AFU-REQ-003](#provenance-AFU-REQ-003)** — Nell’area Task è presente un percorso mentor approvato: elenco delle attività assegnate e dettaglio distinto per ruolo, con identificazione dello studente e della versione corrente, azioni di valutazione, motivazione obbligatoria per chiedere correzioni, esiti/stati delle versioni e feedback di rifiuto della valutazione obsoleta; il percorso ha comportamento equivalente su mobile.

## 2. Obiettivi e ambito

Il risultato richiesto è pianificare la realizzazione dell’app descritta da Work usando i frame Figma come riferimento visivo. La base nominata esplicitamente da Work per il backend è `https://github.com/demeedogg/task-managment-backend`, branch `main`; il template backend analizzato separatamente non sostituisce tale destinazione (`work`, descrizione e sezione repository; `analysis:backend-template-ba4f4065`, §§ “Evidence and scope” e “Verification”; `repositories`).

La copertura funzionale include le attività e il loro ciclo di consegna/revisione, le autorizzazioni per studente e mentor, la ricerca/catalogo e il dettaglio attività, la scoperta mentor, la comunicazione, le notifiche e le preferenze. Gli attori e gli effetti consentiti sono quelli specificati nelle sezioni 3–7. Non sono richiesti altri ruoli di prodotto oltre a studente, mentor e personale autorizzato alle identità/assegnazioni. I controlli di accesso non dipendono dalla navigazione: valgono anche su richieste dirette a una risorsa.

## 3. Attori, ruoli e permessi

**[AFU-RULE-001](#provenance-AFU-RULE-001)** — Il prodotto fornisce autenticazione. Solo personale autorizzato può creare/revocare account o attribuire/revocare i ruoli studente, mentor e personale addetto alle assegnazioni; utenti e mentor non possono autoattribuirsi ruoli privilegiati.

**[AFU-RULE-002](#provenance-AFU-RULE-002)** — Uno studente vede solo le proprie attività e conversazioni. Un mentor vede solo gli studenti a lui assegnati e le relative attività; il catalogo dei mentor non autorizza ad accedere alle attività di altri studenti. La stessa restrizione si applica all’accesso diretto a una risorsa e alle viste già aperte: dopo la revoca dell’assegnazione, i dati protetti non restano visibili al mentor precedente; si mostra un esito neutro di accesso non consentito senza rivelare se esiste una versione nuova.

**[AFU-RULE-003](#provenance-AFU-RULE-003)** — Un registro autorevole delle assegnazioni è gestito da personale autorizzato e l’assegnazione corrente determina i permessi. Alla riassegnazione, il nuovo mentor vede le attività correnti e la cronologia di versioni/consegne e valutazioni necessaria a proseguire; il mentor precedente perde accesso alle attività e alle conversazioni dello studente. Lo studente conserva la propria cronologia completa di attività, valutazioni e conversazioni; le conversazioni storiche non vengono condivise con il nuovo mentor.

**[AFU-RULE-011](#provenance-AFU-RULE-011)** — Le conversazioni nuove sono consentite solo tra lo studente e il mentor attualmente assegnato. “Follow” è una preferenza della directory e non assegna un mentor, non concede accesso alle attività né autorizza conversazioni con mentor non assegnati.

La regola di messaggistica per il solo mentor attualmente assegnato è una deduzione autorizzata dai limiti Work di visibilità (regola 1) e dalla chiarificazione che l’assegnazione corrente governa l’accesso alle conversazioni (`work`; `clarification:cfa8fc71-eefc-424c-96ba-05cf48a52d01`). Le schermate “Follow/Followed” non attribuiscono permessi (`design-description`, righe 251–270 e 506–511).

## 4. Entità, dati e stati

**[AFU-RULE-004](#provenance-AFU-RULE-004)** — Ogni attività assume uno stato tra `da iniziare`, `in corso`, `in revisione`, `da correggere` e `completata`. Lo studente può iniziare l’attività e inviarla in revisione; il mentor attualmente assegnato può completarla oppure richiedere correzioni.

**[AFU-RULE-005](#provenance-AFU-RULE-005)** — Una richiesta di correzioni include una motivazione non vuota associata alla versione valutata e visibile allo studente autorizzato. Una volta completata, l’attività non è più modificabile dallo studente.

**[AFU-RULE-006](#provenance-AFU-RULE-006)** — Ogni consegna accettata è una versione distinta e le versioni precedenti restano disponibili nella cronologia. Ogni valutazione si riferisce alla precisa versione esaminata; una valutazione di una versione storica non si applica implicitamente alla versione corrente.

**[AFU-RULE-008](#provenance-AFU-RULE-008)** — Ogni scadenza è un istante preciso dichiarato nel fuso dell’attività. Si confronta con l’ora della consegna accettata: consegna all’istante o prima = puntuale; successiva = accettata ma tardiva. Un’attività senza scadenza non è mai tardiva. Il fuso orario personale influenza la visualizzazione, non il calcolo della puntualità.

## 5. Processi e funzionalità

### Identità e assegnazioni

Il personale autorizzato registra o revoca identità e ruoli e mantiene le assegnazioni studente–mentor. Le viste, i dettagli, le azioni, le conversazioni e le aggregazioni rispettano sempre i limiti correnti per ruolo, anche per accesso diretto. Dopo la riassegnazione il nuovo mentor riceve il contesto di attività e valutazioni necessario per continuare, ma non le conversazioni storiche; il precedente mentor perde l’accesso operativo e lo studente conserva la propria cronologia. Se il precedente mentor ha già aperto il dettaglio, la perdita di accesso rimuove i dati protetti dalla vista e mostra un esito neutro; non si rivela la presenza di una nuova versione con il messaggio stale. Il risultato osservabile è l’assenza di dati e azioni non autorizzati in qualsiasi vista.

### Inizio, consegna e valutazione delle attività

**[AFU-AC-003](#provenance-AFU-AC-003)** — Lo studente avvia l’attività, prepara la consegna e la invia in revisione. Il mentor assegnato apre la versione corrente e può completare l’attività o richiedere correzioni con motivazione obbligatoria. Lo studente vede lo stato e l’eventuale motivazione; completata, l’attività non è più modificabile dallo studente.

**[AFU-RULE-007](#provenance-AFU-RULE-007)** — La decisione del mentor è riferita alla versione esaminata. Se prima della conferma è stata accettata una versione nuova, la decisione stale non viene applicata alla versione corrente; il mentor vede che la versione è stale, trova la versione corrente in `in revisione` e riceve esattamente: «È disponibile una nuova versione della consegna. Aprila e verifica il contenuto prima di valutarla». Il mentor deve aprire e verificare il contenuto corrente prima di decidere.

**[AFU-RULE-012](#provenance-AFU-RULE-012)** — Gli aggiornamenti concorrenti non sovrascrivono silenziosamente una modifica più recente; l’invio è idempotente rispetto a duplicazioni da doppio clic o retry. Il trattamento di una richiesta stale segue anche la regola atomica AFU-RULE-007.

**[AFU-AC-005](#provenance-AFU-AC-005)** — Studente e mentor vedono lo stesso esito temporale della consegna: all’istante limite o prima è puntuale; dopo è tardiva ma accettata; senza scadenza non compare come tardiva. La valutazione successiva non modifica retroattivamente la puntualità della versione.

**[AFU-AC-006](#provenance-AFU-AC-006)** — Se una nuova versione è accettata prima della conferma, l’interfaccia segnala il rifiuto stale, mostra la versione corrente in revisione e il messaggio esatto indicato; il mentor può aprire e verificare quella versione prima di un nuovo tentativo. L’esito deve valere anche se la nuova consegna arriva immediatamente prima della conferma.

### Limiti delle consegne e messaggi

**[AFU-RULE-009](#provenance-AFU-RULE-009)** — Una consegna accetta un solo file, di dimensione non superiore a 25 MiB, in formato PDF, DOCX, PPTX, JPEG o PNG. Un upload incompleto o fuori limite non crea né sostituisce la versione corrente. La capacità di archiviazione autorizzata è inclusa nell’ambito e deve avere un owner operativo.

**[AFU-RULE-010](#provenance-AFU-RULE-010)** — Un messaggio può contenere fino a 10.000 caratteri e al massimo un allegato JPEG/PNG fino a 10 MiB. Un upload incompleto o fuori limite non invia il messaggio. Conversazioni e allegati rispettano i permessi di AFU-RULE-002 e AFU-RULE-011.

**[AFU-AC-004](#provenance-AFU-AC-004)** — Un file valido entro limiti produce una sola nuova versione di consegna o, per un messaggio, un invio; un upload fallito/incompleto/fuori limite non sostituisce la consegna corrente e non invia un messaggio.

### Dashboard, notifiche ed email

**[AFU-RULE-013](#provenance-AFU-RULE-013)** — Dashboard, contatori e percentuali usano solo attività autorizzate all’attore. Solo lo stato `completata` vale come completamento; un’attività in revisione non è completata. Il periodo/filtro dei KPI è coerente con la lista di attività corrispondente.

**[AFU-RULE-014](#provenance-AFU-RULE-014)** — Le notifiche in-app e le preferenze email sono canali distinti. È inclusa una capacità email autorizzata con owner operativo; se non esiste una capacità autorizzata, se ne introduce una nell’ambito approvato. Un errore di email non annulla né modifica una consegna o una valutazione già registrata e non altera la notifica in-app. I destinatari e gli eventi di notifica seguono le regole Work; il prodotto non attribuisce alle preferenze email il potere di disattivare le notifiche in-app.

**[AFU-RULE-015](#provenance-AFU-RULE-015)** — La lettura di una notifica è distinta dalla lettura di una conversazione. Aprire una conversazione non segna automaticamente come letta la notifica associata; viceversa, la lettura di una notifica non segna letta la conversazione.

**[AFU-AC-008](#provenance-AFU-AC-008)** — Il conteggio e la percentuale dashboard riflettono i soli dati consentiti all’attore; la percentuale di completamento non include attività in revisione; filtrando una lista e il relativo KPI i dati restano coerenti.

**[AFU-AC-010](#provenance-AFU-AC-010)** — Se la consegna o la valutazione è registrata ma l’invio email fallisce, lo stato di lavoro, la valutazione e la notifica in-app restano invariati; l’errore email non è presentato come annullamento dell’azione principale.

### Accettazioni trasversali

**[AFU-AC-001](#provenance-AFU-AC-001)** — Un test funzionale con accesso diretto conferma che lo studente vede solo le proprie attività/conversazioni e il mentor solo i dati ammessi dall’assegnazione corrente; un utente non può elevare autonomamente il proprio ruolo. Se un mentor perde l’assegnazione mentre una sua vista è aperta, i dati dello studente vengono rimossi e il feedback non rivela attività o versioni successive; il messaggio stale è mostrato solo a un mentor che mantiene l’autorizzazione corrente.

**[AFU-AC-002](#provenance-AFU-AC-002)** — Dopo una riassegnazione il nuovo mentor vede le attività correnti e la cronologia di consegne/valutazioni necessaria a continuare; non vede conversazioni storiche; il mentor precedente non accede alle attività o conversazioni; lo studente mantiene la cronologia completa.

**[AFU-AC-007](#provenance-AFU-AC-007)** — Doppio clic o retry identico non crea una versione duplicata; una modifica concorrente non viene sovrascritta senza avviso e nessuna valutazione stale modifica una versione diversa da quella esaminata.

**[AFU-AC-009](#provenance-AFU-AC-009)** — Un nuovo contatto è disponibile solo con il mentor assegnato; Follow non rivela attività e non amplia i destinatari autorizzati.

**[AFU-AC-011](#provenance-AFU-AC-011)** — Su mobile il mentor può raggiungere le stesse attività assegnate, aprire la versione corrente, completare o richiedere correzioni con motivazione e ricevere i medesimi stati/feedback stale della versione desktop.

## 6. Schermate e interazioni

| Schermata/area | Informazioni e controlli richiesti | Comportamento/accesso |
| --- | --- | --- |
| **[AFU-REQ-004](#provenance-AFU-REQ-004)** — Home/dashboard | Riepilogo attività, indicatori e grafico, attività in evidenza, calendario, card mentor e attività; navigazione verso le aree in scope. | Dati filtrati per permessi; indicatori secondo AFU-RULE-013. Valori di esempio del Figma non sono formule di business. |
| **[AFU-REQ-005](#provenance-AFU-REQ-005)** — Elenco attività | Ricerca, categorie/filtri e ordinamento visibili nel design; card con nome, materia, avanzamento e indicazioni temporali. | Solo dati autorizzati; gli stati di business sono mostrati distintamente da barra/percentuale/checklist. |
| **[AFU-REQ-006](#provenance-AFU-REQ-006)** — Dettaglio attività studente | Descrizione/media/checklist, scadenza e fuso, stato, versione corrente e cronologia, upload file e Submit. | Lo studente agisce solo sulle proprie attività; errori di upload non sostituiscono versione e non simulano un invio riuscito. La versione completata è non modificabile. |
| Task assegnati e dettaglio mentor | Nuova estensione approvata: elenco work assegnato; dettaglio mostra studente, versione corrente, cronologia utile, controlli per completare o richiedere correzioni e campo motivazione. | Solo mentor assegnato; una decisione stale produce esattamente il messaggio AFU-RULE-007 e apre/indirizza alla versione corrente. Stessa funzionalità su mobile. |
| **[AFU-REQ-007](#provenance-AFU-REQ-007)** — Elenco mentor | Profilo, specialità, biografia/metriche visibili nel design; ricerca/categoria/ordinamento e Follow. | Follow non assegna e non autorizza accesso o messaggistica; si può iniziare una conversazione solo col mentor assegnato. |
| **[AFU-REQ-008](#provenance-AFU-REQ-008)** — Messaggi | Inbox e conversazione, ricerca, messaggi testuali, un allegato immagine entro limiti, stato della conversazione. | Solo conversazioni accessibili all’attore. Lettura della conversazione e lettura notifica sono indipendenti. |
| **[AFU-REQ-009](#provenance-AFU-REQ-009)** — Notifiche | Campanella e impostazioni delle categorie mostrate nel design. | Preferenze email non disabilitano le notifiche in-app; il loro stato non dipende dal successo dell’email. Feedback di salvataggio distinto dal risultato email. |
| **[AFU-REQ-010](#provenance-AFU-REQ-010)** — Impostazioni generali | Controlli per lingua, fuso e formato 12/24 ore come riferimento visivo. | Il fuso personale influenza solo la presentazione. Il Figma mostra “English (Default)” nel campo fuso e ripete “Timezone” per il formato: correggere le etichette/valori ambigui senza trasformare il campione in una regola di scadenza. |

Le schermate mobile del Figma riordinano i gruppi e usano menu/filtri compatti. **[AFU-RULE-016](#provenance-AFU-RULE-016)** — Tutte le funzioni, informazioni, permessi, validazioni ed esiti di processo richiesti sono disponibili su desktop e mobile; l’impaginazione può adattarsi al dispositivo. L’estensione mentor approvata deve essere presente su entrambi.

## 7. Input, output e integrazioni

Gli input di consegna e messaggio sono quelli e solo quelli definiti in AFU-RULE-009 e AFU-RULE-010. Limiti superati o input incompleti non creano effetti su versione o invio; la schermata distingue un rifiuto dal successo. La data e l’ora di consegna accettata, con fuso dichiarato dall’attività, determinano lo stato puntuale/tardivo secondo AFU-RULE-008.

Le uscite comprendono stati attività/versione, motivazioni di correzione, conversazioni, notifiche in-app e notifiche email previste dal Work. Le valutazioni restano associate alla versione esaminata. L’email è esterna e autorizzata con owner operativo; l’eventuale fallimento non modifica lo stato primario e non annulla l’in-app. La capacità autorizzata di archiviazione è inclusa e va verificata/fornita con owner operativo. Nessuna API, formato di contratto o provider è definito in questa AFU.

## 8. Vincoli, fattibilità e questioni aperte

### Vincoli e decisioni approvate

Le chiarificazioni umane accettate stabiliscono autenticazione/ruoli (`clarification:b3df12f5-2538-4757-9446-11caa0b9315a`); assegnazioni/riassegnazione (`clarification:cfa8fc71-eefc-424c-96ba-05cf48a52d01`); input e storage (`clarification:db9caab7-1536-4717-9c2c-47e4a580e88c`); scadenze (`clarification:f43ef6d1-8449-4f3b-9a47-9ea743d6ad5b`); email (`clarification:78331b3f-90e4-488c-8224-3e07ba80a770`); flusso mentor (`clarification:d2b1f4e7-a787-4bf0-8d03-e43b21ff1118`); e conferma stale senza cambiamenti (`clarification:13a21ba9-7523-4d52-8810-86c8c18d2213`). La conferma 13 rinvia esplicitamente all’Interaction storico `6a9a330f-5be8-4d29-a473-76cb61c38dff` e ne conferma l’answer; 13 è l’origine umana corrente registrata.

Non rimangono questioni materiali di comportamento o autorizzazione aperte. La regola dei messaggi limitati al mentor corrente è la deduzione esplicitata in sezione 3; “Follow” non conferisce diritti. La necessità di aggiungere la UI mentor è stata approvata, quindi l’assenza nei frame originari non è più un blocco. La chiarificazione 13 risolve il precedente blocco di provenienza del comportamento stale, senza modificarlo.

### Fattibilità verificata e da verificare

I repository Work-nominati sono `https://github.com/demeedogg/task-managment-backend`, `main@4985e4cfb8d0135b7aecf7b1b6e7412d1e443396`, e `https://github.com/demeedogg/task-managment-frontend`, `main@5ef7900b2fbc037b03f50c58a6fdba9d8ee9c7bd` (`repositories`). Le analisi descrivono entrambi come README-only, senza codice, dipendenze, configurazione, modello dati o test: comportamento preesistente, compatibilità e verifica runtime sono quindi **non verificabili**, non assenti in sistemi esterni (`analysis:task-managment-backend-21c6dc4a`, righe 5–14 e 42; `analysis:task-managment-frontend-8577187c`, righe 5–17, 44–48). La realizzazione nei checkout Work-nominati è greenfield. I risultati dei documenti specialistici precedenti sono incorporati: il frontend identifica la necessità di rimuovere dati da viste già aperte dopo revoca e mantenere parità desktop/mobile (`review:previous:frontend`, FE-08–FE-09 e FE-UX, righe 47–69, 98–110); il backend conferma i controlli per liste/dettagli/conversazioni/versioni e i prerequisiti operativi di identità, storage, email e bootstrap iniziale del personale (`review:previous:backend`, BE-AUTH-01–04 e BE-FEAS-01–03, righe 31–46, 80–90).

`analysis:backend-template-ba4f4065` riguarda un repository separato, `https://github.com/lucacimino-reply/backend-template.git`, `node-express@04e67bcedfdc2226ae6e24aa6e54a5ded09e3e67`. È un template infrastrutturale parziale con pool/migration runner e un esempio non pertinente, ma senza app/config, autenticazione o logica di dominio (`analysis:backend-template-ba4f4065`, righe 5–15). Non è il target dichiarato da Work e non cambia la destinazione del piano.

La storage capability e l’email capability sono autorizzate come interventi con owner operativo. Le analisi dei checkout non verificano che un servizio sia già disponibile né nominano l’owner: Delivery deve identificare o introdurre la capacità autorizzata, assegnarne l’owner e verificarne l’operatività prima del rilascio. Prima di operare, un operatore autorizzato deve predisporre in modo controllato il primo account del personale autorizzato; in seguito il provisioning e la revoca seguono AFU-RULE-001 (`review:previous:backend`, BE-AUTH-04, riga 46). Sono prerequisiti di Delivery entro lo scope approvato, non nuove autorizzazioni o scelte di provider/tecnologia in Requirements Review.

Le schermate di caricamento/skeleton Figma non sono prove di implementazione o di runtime. Le schermate campione e i valori visivi non introducono regole di business oltre quelle espresse qui. Non sono stati eseguiti build, test, applicazioni o integrazioni; la verifica è esclusivamente documentale e read-only.

### Questioni non bloccanti

Il Figma mostra campioni inglesi e controlli di lingua, ma né Work né una chiarificazione definiscono un catalogo di lingue supportate; non si assume quindi supporto multilingue né una lingua aggiuntiva. Il testo specifico di errori ordinari, la disposizione responsiva dei componenti e i valori dei dati demo possono essere rifiniti nel design senza alterare permessi, stati, dati o integrazioni definiti da questa AFU. La label confusa del formato ora va corretta nella presentazione; il fuso personale non modifica il calcolo delle scadenze.

<!-- sdlc-decision-provenance:v1
{
  "schemaVersion": 1,
  "reviewRound": 2,
  "evidenceDigest": "706bfc9b44fd85a4780e5c7234787486714d406acbd465679bff76166c8ac38a",
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
              "locator": "work.description \u003e OBIETTIVO E REQUISITI \u003e obiettivo del prodotto"
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
              "locator": "work.description \u003e OBIETTIVO E REQUISITI \u003e Ambito"
            },
            {
              "evidenceRef": "design-description",
              "locator": "render inventory; populated desktop/mobile screen descriptions"
            }
          ]
        }
      ]
    },
    {
      "subjectId": "AFU-REQ-003",
      "subjectKind": "requirement",
      "supersedes": [],
      "origins": [
        {
          "kind": "human_clarification",
          "sources": [
            {
              "evidenceRef": "clarification:d2b1f4e7-a787-4bf0-8d03-e43b21ff1118",
              "locator": "accepted answer and approved mentor review-flow extension"
            }
          ],
          "interactionId": "d2b1f4e7-a787-4bf0-8d03-e43b21ff1118",
          "question": "Chiarimento sul flusso del mentor assente dal Figma. Nei frame desktop e mobile del dettaglio attività sono mostrati l’upload e «Submit» per lo studente; non sono mostrati una lista delle consegne assegnate al mentor, le azioni per completare o richiedere correzioni, l’inserimento della motivazione né il feedback della valutazione. Approviamo l’estensione proposta qui sotto, oppure hai frame alternativi da indicare?",
          "answer": "perfetto"
        }
      ]
    },
    {
      "subjectId": "AFU-REQ-004",
      "subjectKind": "requirement",
      "supersedes": [],
      "origins": [
        {
          "kind": "explicit_source",
          "sources": [
            {
              "evidenceRef": "design-description",
              "locator": "desktop/mobile dashboard screen descriptions, lines 104–116 and 209–221"
            }
          ]
        }
      ]
    },
    {
      "subjectId": "AFU-REQ-005",
      "subjectKind": "requirement",
      "supersedes": [],
      "origins": [
        {
          "kind": "explicit_source",
          "sources": [
            {
              "evidenceRef": "design-description",
              "locator": "desktop/mobile task catalog descriptions, lines 118–130 and 223–235"
            }
          ]
        }
      ]
    },
    {
      "subjectId": "AFU-REQ-006",
      "subjectKind": "requirement",
      "supersedes": [],
      "origins": [
        {
          "kind": "explicit_source",
          "sources": [
            {
              "evidenceRef": "design-description",
              "locator": "desktop/mobile task-detail descriptions, lines 132–144 and 237–249"
            }
          ]
        }
      ]
    },
    {
      "subjectId": "AFU-REQ-007",
      "subjectKind": "requirement",
      "supersedes": [],
      "origins": [
        {
          "kind": "explicit_source",
          "sources": [
            {
              "evidenceRef": "design-description",
              "locator": "desktop/mobile mentor-directory descriptions, lines 146–158 and 251–263"
            }
          ]
        }
      ]
    },
    {
      "subjectId": "AFU-REQ-008",
      "subjectKind": "requirement",
      "supersedes": [],
      "origins": [
        {
          "kind": "explicit_source",
          "sources": [
            {
              "evidenceRef": "design-description",
              "locator": "desktop/mobile inbox and chat descriptions, lines 160–179 and 265–284"
            }
          ]
        }
      ]
    },
    {
      "subjectId": "AFU-REQ-009",
      "subjectKind": "requirement",
      "supersedes": [],
      "origins": [
        {
          "kind": "explicit_source",
          "sources": [
            {
              "evidenceRef": "design-description",
              "locator": "desktop/mobile notification-settings descriptions, lines 195–207 and 300–312"
            }
          ]
        }
      ]
    },
    {
      "subjectId": "AFU-REQ-010",
      "subjectKind": "requirement",
      "supersedes": [],
      "origins": [
        {
          "kind": "explicit_source",
          "sources": [
            {
              "evidenceRef": "design-description",
              "locator": "desktop/mobile general-settings descriptions, lines 181–193 and 286–298"
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
          "kind": "human_clarification",
          "sources": [
            {
              "evidenceRef": "clarification:b3df12f5-2538-4757-9446-11caa0b9315a",
              "locator": "accepted authentication and role-provisioning answer"
            }
          ],
          "interactionId": "b3df12f5-2538-4757-9446-11caa0b9315a",
          "question": "Chiarimento per chi definisce il prodotto — autenticazione e ruoli. Per applicare i permessi di studenti, mentor e personale autorizzato, esiste una fonte istituzionale di identità da usare oppure l’app deve gestire gli account? Chi può attribuire e revocare questi ruoli? La decisione determina come si applicano l’assegnazione mentor accettata e i controlli sugli accessi diretti.",
          "answer": "come la tua assunzione"
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
              "locator": "work.description \u003e Regole di business \u003e 1. Visibilità e permessi"
            }
          ]
        },
        {
          "kind": "agent_decision",
          "sources": [
            {
              "evidenceRef": "clarification:cfa8fc71-eefc-424c-96ba-05cf48a52d01",
              "locator": "accepted current-assignment access and former-mentor task/conversation revocation"
            },
            {
              "evidenceRef": "review:previous:frontend",
              "locator": "FE-09, lines 64–69 (reassignment loss of access and no stale-version disclosure to former mentor)"
            }
          ],
          "decisionType": "deduction",
          "rationale": "Current assignment governs current access. Therefore the access boundary also applies to an already-open view: once access is revoked, continued display of protected student data or a stale-version hint would reveal information the former mentor may no longer see. A neutral no-access outcome preserves the Work permission rule.",
          "specialists": [
            "requirements",
            "frontend",
            "backend"
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
          "kind": "human_clarification",
          "sources": [
            {
              "evidenceRef": "clarification:cfa8fc71-eefc-424c-96ba-05cf48a52d01",
              "locator": "accepted assignment registry, reassignment and history answer"
            }
          ],
          "interactionId": "cfa8fc71-eefc-424c-96ba-05cf48a52d01",
          "question": "Chiarimento per chi definisce il prodotto — assegnazioni mentor. Qual è la fonte autorevole che stabilisce e aggiorna l’assegnazione studente–mentor? Quando uno studente viene riassegnato, quale accesso devono avere il nuovo mentor, il mentor precedente e lo studente alle attività correnti, alle versioni e valutazioni precedenti e alle conversazioni? La risposta determina le autorizzazioni, anche per accesso diretto, e la cronologia disponibile durante la revisione.",
          "answer": "la tua assunzinoe mi va bene"
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
              "locator": "work.description \u003e Regole di business \u003e 2. Ciclo di vita delle attività"
            }
          ]
        }
      ]
    },
    {
      "subjectId": "AFU-RULE-005",
      "subjectKind": "rule",
      "supersedes": [],
      "origins": [
        {
          "kind": "explicit_source",
          "sources": [
            {
              "evidenceRef": "work",
              "locator": "work.description \u003e Regole di business \u003e 2. Ciclo di vita delle attività (required correction reason; completed-task immutability)"
            }
          ]
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
              "locator": "work.description \u003e Regole di business \u003e 3. Versioned submissions and reviews"
            }
          ]
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
              "locator": "work.description \u003e Regole di business \u003e 3–4 (version-specific review; no implicit action on a newer version)"
            }
          ]
        },
        {
          "kind": "human_clarification",
          "sources": [
            {
              "evidenceRef": "clarification:d2b1f4e7-a787-4bf0-8d03-e43b21ff1118",
              "locator": "accepted mentor-flow extension including current-version/status outcome and stale-rejection feedback"
            }
          ],
          "interactionId": "d2b1f4e7-a787-4bf0-8d03-e43b21ff1118",
          "question": "Chiarimento sul flusso del mentor assente dal Figma. Nei frame desktop e mobile del dettaglio attività sono mostrati l’upload e «Submit» per lo studente; non sono mostrati una lista delle consegne assegnate al mentor, le azioni per completare o richiedere correzioni, l’inserimento della motivazione né il feedback della valutazione. Approviamo l’estensione proposta qui sotto, oppure hai frame alternativi da indicare?",
          "answer": "perfetto"
        },
        {
          "kind": "human_clarification",
          "sources": [
            {
              "evidenceRef": "clarification:13a21ba9-7523-4d52-8810-86c8c18d2213",
              "locator": "accepted answer confirms unchanged atomic stale-decision behavior, no state/evaluation/notification side effects and exact message"
            }
          ],
          "interactionId": "13a21ba9-7523-4d52-8810-86c8c18d2213",
          "question": "Il comportamento sulle valutazioni obsolete è già stato deciso, ma l’Interaction ID della tua risposta precedente (`6a9a330f-5be8-4d29-a473-76cb61c38dff`) non è risolvibile nel contesto di provenance corrente. Per registrare l’origine umana senza trasformarla in una deduzione, puoi reinviare quel chiarimento tramite la risposta formale di Requirements Review? Il comportamento da registrare è: rifiuto atomico della valutazione sulla versione superata; nessuna modifica all’attività o alla versione corrente, nessuna nuova valutazione né notifica di completamento/correzione; versione corrente ancora in revisione, storico conservato e messaggio «È disponibile una nuova versione della consegna. Aprila e verifica il contenuto prima di valutarla».",
          "answer": "Confermo integralmente, senza modifiche, il comportamento già autorizzato nella mia risposta all’Interaction 6a9a330f-5be8-4d29-a473-76cb61c38dff: rifiuto atomico della valutazione obsoleta, senza modifiche all’attività o alla versione corrente, senza nuova valutazione né notifiche di completamento/correzione. La versione corrente resta in revisione e lo storico viene conservato. Mostrare: «È disponibile una nuova versione della consegna. Aprila e verifica il contenuto prima di valutarla». Il controllo vale anche per un nuovo invio immediatamente precedente alla conferma del mentor."
        }
      ]
    },
    {
      "subjectId": "AFU-RULE-008",
      "subjectKind": "rule",
      "supersedes": [],
      "origins": [
        {
          "kind": "human_clarification",
          "sources": [
            {
              "evidenceRef": "clarification:f43ef6d1-8449-4f3b-9a47-9ea743d6ad5b",
              "locator": "accepted deadline instant/timezone/boundary/no-deadline answer"
            }
          ],
          "interactionId": "f43ef6d1-8449-4f3b-9a47-9ea743d6ad5b",
          "question": "Chiarimento per chi definisce il prodotto — scadenze. Una scadenza è una data (per esempio, valida fino alla fine del giorno) o un istante preciso? Quale fuso determina il confine tra puntuale e in ritardo? Come vanno trattate le attività senza scadenza? La decisione influisce sull’esito di ogni consegna e sulle informazioni mostrate a studenti e mentor.",
          "answer": "la tua assunzione va bene"
        }
      ]
    },
    {
      "subjectId": "AFU-RULE-009",
      "subjectKind": "rule",
      "supersedes": [],
      "origins": [
        {
          "kind": "human_clarification",
          "sources": [
            {
              "evidenceRef": "clarification:db9caab7-1536-4717-9c2c-47e4a580e88c",
              "locator": "accepted submission-file limits, no-side-effect failure, authorized storage answer"
            }
          ],
          "interactionId": "db9caab7-1536-4717-9c2c-47e4a580e88c",
          "question": "Chiarimento per chi definisce il prodotto — file delle consegne e allegati dei messaggi. Il Figma mostra il caricamento di file per le consegne e allegati nelle conversazioni, ma non specifica se entrambi siano previsti né i formati, il numero o la dimensione massima. Quali limiti devono valere? Per considerarli realizzabili, occorre inoltre confermare una capacità di archiviazione autorizzata o approvare che ne venga introdotta una.",
          "answer": "la tua assunzione va bene"
        }
      ]
    },
    {
      "subjectId": "AFU-RULE-010",
      "subjectKind": "rule",
      "supersedes": [],
      "origins": [
        {
          "kind": "human_clarification",
          "sources": [
            {
              "evidenceRef": "clarification:db9caab7-1536-4717-9c2c-47e4a580e88c",
              "locator": "accepted message limits and no-send failure answer"
            }
          ],
          "interactionId": "db9caab7-1536-4717-9c2c-47e4a580e88c",
          "question": "Chiarimento per chi definisce il prodotto — file delle consegne e allegati dei messaggi. Il Figma mostra il caricamento di file per le consegne e allegati nelle conversazioni, ma non specifica se entrambi siano previsti né i formati, il numero o la dimensione massima. Quali limiti devono valere? Per considerarli realizzabili, occorre inoltre confermare una capacità di archiviazione autorizzata o approvare che ne venga introdotta una.",
          "answer": "la tua assunzione va bene"
        }
      ]
    },
    {
      "subjectId": "AFU-RULE-011",
      "subjectKind": "rule",
      "supersedes": [],
      "origins": [
        {
          "kind": "agent_decision",
          "sources": [
            {
              "evidenceRef": "work",
              "locator": "work.description \u003e Regole di business \u003e 1. Visibilità e permessi"
            },
            {
              "evidenceRef": "clarification:cfa8fc71-eefc-424c-96ba-05cf48a52d01",
              "locator": "accepted current-assignment access and former-mentor conversation revocation"
            },
            {
              "evidenceRef": "design-description",
              "locator": "lines 251–270 and 506–511 (Follow and messaging controls do not define permission)"
            }
          ],
          "decisionType": "deduction",
          "rationale": "The Work limits mentor visibility to assigned students; the accepted assignment rule makes current assignment authoritative for access. Follow is a visual directory state, not evidence of assignment or permission. Restricting new conversations to the assigned mentor preserves the access boundary.",
          "specialists": [
            "requirements",
            "frontend",
            "backend"
          ]
        }
      ]
    },
    {
      "subjectId": "AFU-RULE-012",
      "subjectKind": "rule",
      "supersedes": [],
      "origins": [
        {
          "kind": "explicit_source",
          "sources": [
            {
              "evidenceRef": "work",
              "locator": "work.description \u003e Regole di business \u003e 4. Concurrency, idempotency and no-silent-overwrite"
            }
          ]
        }
      ]
    },
    {
      "subjectId": "AFU-RULE-013",
      "subjectKind": "rule",
      "supersedes": [],
      "origins": [
        {
          "kind": "explicit_source",
          "sources": [
            {
              "evidenceRef": "work",
              "locator": "work.description \u003e Regole di business \u003e 5. Dashboard"
            },
            {
              "evidenceRef": "analysis:task-managment-backend-21c6dc4a",
              "locator": "lines 22 (authorized counts, completed-only completion, consistent filters)"
            }
          ]
        }
      ]
    },
    {
      "subjectId": "AFU-RULE-014",
      "subjectKind": "rule",
      "supersedes": [],
      "origins": [
        {
          "kind": "explicit_source",
          "sources": [
            {
              "evidenceRef": "work",
              "locator": "work.description \u003e Regole di business \u003e 6. Messaggi e notifiche"
            }
          ]
        },
        {
          "kind": "human_clarification",
          "sources": [
            {
              "evidenceRef": "clarification:78331b3f-90e4-488c-8224-3e07ba80a770",
              "locator": "accepted email capability and operational owner; introduce if absent; failure isolation"
            }
          ],
          "interactionId": "78331b3f-90e4-488c-8224-3e07ba80a770",
          "question": "Chiarimento per chi definisce il prodotto — invio email. Il requisito prevede notifiche email e specifica che un errore email non annulla consegne o valutazioni, ma nei repository analizzati non è documentata una capacità di invio né il relativo responsabile operativo. Esiste già un servizio autorizzato con un owner? Se non esiste, autorizziamo a includere nell’ambito l’introduzione di una capacità di invio email e la sua gestione operativa?",
          "answer": "si, la tua proposta è approvata"
        }
      ]
    },
    {
      "subjectId": "AFU-RULE-015",
      "subjectKind": "rule",
      "supersedes": [],
      "origins": [
        {
          "kind": "explicit_source",
          "sources": [
            {
              "evidenceRef": "work",
              "locator": "work.description \u003e Regole di business \u003e 6. Independent notification and conversation read state"
            },
            {
              "evidenceRef": "design-description",
              "locator": "lines 265–270 and 300–312"
            }
          ]
        }
      ]
    },
    {
      "subjectId": "AFU-RULE-016",
      "subjectKind": "rule",
      "supersedes": [],
      "origins": [
        {
          "kind": "explicit_source",
          "sources": [
            {
              "evidenceRef": "work",
              "locator": "work.description \u003e Regole di business \u003e 7. Desktop/mobile parity"
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
              "locator": "work.description \u003e Regole di business \u003e 1. Visibilità e permessi"
            }
          ]
        },
        {
          "kind": "human_clarification",
          "sources": [
            {
              "evidenceRef": "clarification:b3df12f5-2538-4757-9446-11caa0b9315a",
              "locator": "accepted product authentication and authorized-staff-only role management"
            }
          ],
          "interactionId": "b3df12f5-2538-4757-9446-11caa0b9315a",
          "question": "Chiarimento per chi definisce il prodotto — autenticazione e ruoli. Per applicare i permessi di studenti, mentor e personale autorizzato, esiste una fonte istituzionale di identità da usare oppure l’app deve gestire gli account? Chi può attribuire e revocare questi ruoli? La decisione determina come si applicano l’assegnazione mentor accettata e i controlli sugli accessi diretti.",
          "answer": "come la tua assunzione"
        },
        {
          "kind": "agent_decision",
          "sources": [
            {
              "evidenceRef": "work",
              "locator": "work.description \u003e Regole di business \u003e 1 (permissions apply to direct access)"
            },
            {
              "evidenceRef": "clarification:cfa8fc71-eefc-424c-96ba-05cf48a52d01",
              "locator": "accepted current-assignment and former-mentor access revocation"
            },
            {
              "evidenceRef": "review:previous:frontend",
              "locator": "FE-09, lines 64–69 (loss of authorization while a view is open; neutral denial/no stale leakage)"
            }
          ],
          "decisionType": "deduction",
          "rationale": "The same current-assignment access boundary applies to already-open views and direct requests. When the former mentor loses access, clearing protected data and providing a neutral denial avoids exposing student data or the existence of a newer version.",
          "specialists": [
            "requirements",
            "frontend",
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
              "evidenceRef": "clarification:cfa8fc71-eefc-424c-96ba-05cf48a52d01",
              "locator": "accepted assignment/reassignment access and history policy"
            }
          ],
          "interactionId": "cfa8fc71-eefc-424c-96ba-05cf48a52d01",
          "question": "Chiarimento per chi definisce il prodotto — assegnazioni mentor. Qual è la fonte autorevole che stabilisce e aggiorna l’assegnazione studente–mentor? Quando uno studente viene riassegnato, quale accesso devono avere il nuovo mentor, il mentor precedente e lo studente alle attività correnti, alle versioni e valutazioni precedenti e alle conversazioni? La risposta determina le autorizzazioni, anche per accesso diretto, e la cronologia disponibile durante la revisione.",
          "answer": "la tua assunzinoe mi va bene"
        }
      ]
    },
    {
      "subjectId": "AFU-AC-003",
      "subjectKind": "acceptance",
      "supersedes": [],
      "origins": [
        {
          "kind": "explicit_source",
          "sources": [
            {
              "evidenceRef": "work",
              "locator": "work.description \u003e Regole di business \u003e 2. Activity lifecycle and authorized actions"
            }
          ]
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
              "evidenceRef": "clarification:db9caab7-1536-4717-9c2c-47e4a580e88c",
              "locator": "accepted upload limits and failed/incomplete no-side-effect outcome"
            }
          ],
          "interactionId": "db9caab7-1536-4717-9c2c-47e4a580e88c",
          "question": "Chiarimento per chi definisce il prodotto — file delle consegne e allegati dei messaggi. Il Figma mostra il caricamento di file per le consegne e allegati nelle conversazioni, ma non specifica se entrambi siano previsti né i formati, il numero o la dimensione massima. Quali limiti devono valere? Per considerarli realizzabili, occorre inoltre confermare una capacità di archiviazione autorizzata o approvare che ne venga introdotta una.",
          "answer": "la tua assunzione va bene"
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
              "evidenceRef": "clarification:f43ef6d1-8449-4f3b-9a47-9ea743d6ad5b",
              "locator": "accepted deadline rule and late/no-deadline outcomes"
            }
          ],
          "interactionId": "f43ef6d1-8449-4f3b-9a47-9ea743d6ad5b",
          "question": "Chiarimento per chi definisce il prodotto — scadenze. Una scadenza è una data (per esempio, valida fino alla fine del giorno) o un istante preciso? Quale fuso determina il confine tra puntuale e in ritardo? Come vanno trattate le attività senza scadenza? La decisione influisce sull’esito di ogni consegna e sulle informazioni mostrate a studenti e mentor.",
          "answer": "la tua assunzione va bene"
        }
      ]
    },
    {
      "subjectId": "AFU-AC-006",
      "subjectKind": "acceptance",
      "supersedes": [],
      "origins": [
        {
          "kind": "explicit_source",
          "sources": [
            {
              "evidenceRef": "work",
              "locator": "work.description \u003e Regole di business \u003e 3–4 (version-specific review, no implicit application to a newer version)"
            }
          ]
        },
        {
          "kind": "human_clarification",
          "sources": [
            {
              "evidenceRef": "clarification:d2b1f4e7-a787-4bf0-8d03-e43b21ff1118",
              "locator": "approved stale-rejection feedback, current-version status and mentor flow"
            }
          ],
          "interactionId": "d2b1f4e7-a787-4bf0-8d03-e43b21ff1118",
          "question": "Chiarimento sul flusso del mentor assente dal Figma. Nei frame desktop e mobile del dettaglio attività sono mostrati l’upload e «Submit» per lo studente; non sono mostrati una lista delle consegne assegnate al mentor, le azioni per completare o richiedere correzioni, l’inserimento della motivazione né il feedback della valutazione. Approviamo l’estensione proposta qui sotto, oppure hai frame alternativi da indicare?",
          "answer": "perfetto"
        },
        {
          "kind": "human_clarification",
          "sources": [
            {
              "evidenceRef": "clarification:13a21ba9-7523-4d52-8810-86c8c18d2213",
              "locator": "accepted answer confirms atomic stale rejection, no state/evaluation/notification side effects, history retention and exact message"
            }
          ],
          "interactionId": "13a21ba9-7523-4d52-8810-86c8c18d2213",
          "question": "Il comportamento sulle valutazioni obsolete è già stato deciso, ma l’Interaction ID della tua risposta precedente (`6a9a330f-5be8-4d29-a473-76cb61c38dff`) non è risolvibile nel contesto di provenance corrente. Per registrare l’origine umana senza trasformarla in una deduzione, puoi reinviare quel chiarimento tramite la risposta formale di Requirements Review? Il comportamento da registrare è: rifiuto atomico della valutazione sulla versione superata; nessuna modifica all’attività o alla versione corrente, nessuna nuova valutazione né notifica di completamento/correzione; versione corrente ancora in revisione, storico conservato e messaggio «È disponibile una nuova versione della consegna. Aprila e verifica il contenuto prima di valutarla».",
          "answer": "Confermo integralmente, senza modifiche, il comportamento già autorizzato nella mia risposta all’Interaction 6a9a330f-5be8-4d29-a473-76cb61c38dff: rifiuto atomico della valutazione obsoleta, senza modifiche all’attività o alla versione corrente, senza nuova valutazione né notifiche di completamento/correzione. La versione corrente resta in revisione e lo storico viene conservato. Mostrare: «È disponibile una nuova versione della consegna. Aprila e verifica il contenuto prima di valutarla». Il controllo vale anche per un nuovo invio immediatamente precedente alla conferma del mentor."
        }
      ]
    },
    {
      "subjectId": "AFU-AC-007",
      "subjectKind": "acceptance",
      "supersedes": [],
      "origins": [
        {
          "kind": "explicit_source",
          "sources": [
            {
              "evidenceRef": "work",
              "locator": "work.description \u003e Regole di business \u003e 4. Concurrent changes, duplicate submits and no silent overwrite"
            }
          ]
        }
      ]
    },
    {
      "subjectId": "AFU-AC-008",
      "subjectKind": "acceptance",
      "supersedes": [],
      "origins": [
        {
          "kind": "explicit_source",
          "sources": [
            {
              "evidenceRef": "work",
              "locator": "work.description \u003e Regole di business \u003e 5. Dashboard and filters"
            }
          ]
        }
      ]
    },
    {
      "subjectId": "AFU-AC-009",
      "subjectKind": "acceptance",
      "supersedes": [],
      "origins": [
        {
          "kind": "agent_decision",
          "sources": [
            {
              "evidenceRef": "work",
              "locator": "work.description \u003e Regole di business \u003e 1 and 6"
            },
            {
              "evidenceRef": "clarification:cfa8fc71-eefc-424c-96ba-05cf48a52d01",
              "locator": "accepted current-assignment and reassignment conversation-access rule"
            },
            {
              "evidenceRef": "design-description",
              "locator": "lines 251–270 and 506–511"
            }
          ],
          "decisionType": "deduction",
          "rationale": "Only the current assigned mentor may access a student's mentor-related information; assignment establishes the access boundary and Follow does not alter it.",
          "specialists": [
            "requirements",
            "frontend",
            "backend"
          ]
        }
      ]
    },
    {
      "subjectId": "AFU-AC-010",
      "subjectKind": "acceptance",
      "supersedes": [],
      "origins": [
        {
          "kind": "human_clarification",
          "sources": [
            {
              "evidenceRef": "clarification:78331b3f-90e4-488c-8224-3e07ba80a770",
              "locator": "accepted email failure isolation and in-app independence"
            }
          ],
          "interactionId": "78331b3f-90e4-488c-8224-3e07ba80a770",
          "question": "Chiarimento per chi definisce il prodotto — invio email. Il requisito prevede notifiche email e specifica che un errore email non annulla consegne o valutazioni, ma nei repository analizzati non è documentata una capacità di invio né il relativo responsabile operativo. Esiste già un servizio autorizzato con un owner? Se non esiste, autorizziamo a includere nell’ambito l’introduzione di una capacità di invio email e la sua gestione operativa?",
          "answer": "si, la tua proposta è approvata"
        }
      ]
    },
    {
      "subjectId": "AFU-AC-011",
      "subjectKind": "acceptance",
      "supersedes": [],
      "origins": [
        {
          "kind": "human_clarification",
          "sources": [
            {
              "evidenceRef": "clarification:d2b1f4e7-a787-4bf0-8d03-e43b21ff1118",
              "locator": "accepted mentor queue/detail/review/reason/status/stale/mobile flow"
            }
          ],
          "interactionId": "d2b1f4e7-a787-4bf0-8d03-e43b21ff1118",
          "question": "Chiarimento sul flusso del mentor assente dal Figma. Nei frame desktop e mobile del dettaglio attività sono mostrati l’upload e «Submit» per lo studente; non sono mostrati una lista delle consegne assegnate al mentor, le azioni per completare o richiedere correzioni, l’inserimento della motivazione né il feedback della valutazione. Approviamo l’estensione proposta qui sotto, oppure hai frame alternativi da indicare?",
          "answer": "perfetto"
        }
      ]
    }
  ]
}
-->
