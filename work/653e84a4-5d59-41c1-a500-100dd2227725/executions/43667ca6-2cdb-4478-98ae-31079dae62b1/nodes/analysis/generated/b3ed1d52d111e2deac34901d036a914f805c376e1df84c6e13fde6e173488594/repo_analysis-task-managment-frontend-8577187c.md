# Analisi repository frontend — TASK MANAGMENT

## Perimetro ed evidenze

- Repository: `https://github.com/demeedogg/task-managment-frontend.git`
- Branch: `main`
- Commit analizzato: `5ef7900b2fbc037b03f50c58a6fdba9d8ee9c7bd` (`first commit`, checkout shallow/grafted).
- Il commit contiene un solo file tracciato: `README.md`, con il solo titolo `# task-managment-frontend`.
- Non risultano codice applicativo, manifesti di dipendenze, configurazione, documentazione funzionale, test o istruzioni specifiche del repository. CodeGraph non ha trovato file da indicizzare.

Di conseguenza, non è possibile confermare funzionalità esistenti, stack, contratti API, test, comportamento mobile o vincoli implementativi. L'assenza di evidenza nel commit non prova che tali funzionalità non esistano in servizi esterni o in versioni non incluse nel commit. Non è stata esaminata la cronologia precedente al commit fornito.

Questa analisi è limitata al repository frontend indicato da `objective.repository`, come richiesto dall'analisi `repo`. Non sono stati ispezionati il repository backend né i frame Figma: il backend è un'integrazione da verificare in una relativa analisi, mentre i requisiti riportati sotto sono trattati come fonte delle regole di business, non come prova dello stato corrente del frontend. Non è possibile quindi affermare differenze puntuali rispetto ai frame o a comportamenti backend esistenti.

## Stato rispetto all'obiettivo

Non c'è un'app frontend rilevabile da estendere. Tutte le funzionalità richieste sono da considerare **non documentate e non verificabili** nel commit, non comportamenti già implementati. Per realizzare il prodotto sarà necessario creare l'applicazione e concordare il suo contratto con il backend; non è possibile raccomandare uno stack o attribuire endpoint al sistema sulla base delle evidenze disponibili.

## Piano delle modifiche necessarie

1. **Definire fondamenta e integrazione.** Stabilire stack, routing, gestione della sessione e client API sulla base del contratto backend. Modellare esplicitamente i ruoli studente/mentor e gli errori di autorizzazione, conflitto e validazione. La UI deve applicare le regole ai controlli e agli stati mostrati, ma l'autorizzazione effettiva — incluse richieste dirette a una risorsa — deve essere garantita e verificata dal backend.
2. **Costruire shell e navigazione responsive.** Implementare le aree dashboard/home, attività, mentor, messaggi, notifiche e impostazioni richieste. Usare i frame Figma desktop e mobile per disposizione e resa visiva; non ci sono elementi nel repository che specifichino navigazione, componenti o breakpoint.
3. **Implementare dashboard e liste attività.** Visualizzare solo dati autorizzati; derivare conteggi e progressi dai record visibili e conteggiare come completate soltanto le attività nello stato completato. Coordinare filtri e intervalli temporali tra KPI e liste corrispondenti, mantenendo gli stessi risultati funzionali su desktop e mobile.
4. **Implementare dettaglio e transizioni di stato.** Rappresentare gli stati da iniziare, in corso, in revisione, da correggere e completata. Consentire allo studente di iniziare e inviare in revisione; consentire solo al mentor assegnato completamento o richiesta di correzioni, con motivazione obbligatoria. Rendere non modificabile allo studente un'attività completata e mostrare gli esiti/validazioni delle azioni.
5. **Gestire versioni e scadenze delle consegne.** Ogni invio deve riferirsi a una nuova versione, conservare e rendere consultabili le precedenti e indicare quale versione è in valutazione. Consentire invii tardivi e mostrare che sono in ritardo; mantenere puntuale una versione inviata entro la scadenza anche se valutata successivamente. Proteggere l'invio da doppio clic e retry duplicati usando un contratto idempotente lato servizio oltre al feedback/disabilitazione UI durante l'invio.
6. **Gestire concorrenza e valutazioni obsolete.** Includere la revisione/versione del record nelle modifiche e gestire il conflitto senza sovrascrittura silenziosa (per esempio, avviso e ricaricamento/confronto dello stato aggiornato). Collegare ogni valutazione a una versione precisa; se la versione è superata, informare il mentor e non segnare automaticamente completata la versione più recente. Il comportamento definitivo dipende dal contratto del backend, non presente in questo checkout.
7. **Applicare visibilità per ruolo a tutte le viste.** Lo studente può consultare solo le proprie attività e conversazioni; il mentor solo gli studenti assegnati e le rispettive attività. La lista mentor non deve esporre attività altrui. La navigazione e i link diretti devono produrre stati coerenti con i dinieghi del backend e non rendere visibili dati non autorizzati.
8. **Implementare messaggi, notifiche e preferenze.** Separare stato di lettura della notifica da stato di lettura della conversazione; creare una sola notifica per ciascun evento/destinatario previsto (invio in revisione, correzione richiesta, completamento); mantenere le notifiche in-app attive anche con email disabilitate. Comunicare gli esiti email senza annullare o rappresentare come fallita la consegna/valutazione già registrata.
9. **Verificare equivalenza e accessibilità d'uso.** Aggiungere test mirati per flussi dei due ruoli, accesso e stati vietati, conteggi/filtri, versioni e scadenze, doppio invio, conflitti, notifiche e preferenze. Verificare le stesse regole e gli stessi dati sui layout desktop e mobile, con test visuali/usabilità sui frame concordati. Nessun test o ambiente di esecuzione è fornito dal repository.

## Gap e decisioni da chiarire

Non sono rilevabili contraddizioni con il comportamento esistente: il commit non contiene comportamenti applicativi da confrontare. Neppure è possibile stabilire se i frame Figma mostrino i controlli e feedback necessari. Prima di considerare il requisito UX risolto, confrontare i frame desktop/mobile con questi punti e chiedere decisione sui dettagli non mostrati:

- **Correzioni:** dove si inserisce e visualizza la motivazione richiesta; quali sono i vincoli di testo e il feedback per campo vuoto/non valido?
- **Invio e versioni:** come si conferma un invio, si comunica il successo/errore, si segnala una consegna tardiva e si accede alle versioni precedenti e alla versione esaminata?
- **Conflitti:** quale messaggio e azione deve ricevere l'utente quando il record è cambiato in un'altra sessione? È richiesto confronto o basta ricaricare e ripetere?
- **Valutazione obsoleta:** come si avvisa il mentor che sta valutando una versione non più corrente e quale azione permette di valutare la versione corretta?
- **Permessi:** quali viste/stati sono previsti per risorsa non autorizzata o non trovata, sia da link diretto sia dalla navigazione?
- **Notifiche:** quali destinatari, contenuti, indicatori e azioni sono previsti per ciascun evento? Come si distingue visivamente la lettura della notifica da quella della conversazione e lo stato delle email dalle notifiche in-app?
- **Dashboard e filtri:** quali intervalli, criteri di filtro e stati vuoti/errore mostrano i frame? Come si comunica la coerenza tra KPI e lista filtrata?
- **Mobile:** quali controlli diventano menu, pannelli o navigazione secondaria, e come si espongono gli stessi filtri, dettagli, versioni e feedback presenti su desktop?

Servono inoltre l'analisi del repository backend al commit previsto e l'ispezione dei frame Figma per sostituire queste dipendenze aperte con un piano di integrazione e una mappatura visiva verificabili. In particolare, la presenza di autenticazione, autorizzazioni server-side, versionamento, idempotenza, concorrenza, notifiche e semantica delle scadenze rimane sconosciuta in questa analisi frontend.

## Verifica eseguita

La verifica è stata di sola lettura: confronto del commit `HEAD` col commit richiesto, inventario dei file Git e README, stato del working tree e indicizzazione CodeGraph. Non sono stati eseguiti build, test o applicazioni: non sono presenti codice o manifesti con cui eseguirli.
