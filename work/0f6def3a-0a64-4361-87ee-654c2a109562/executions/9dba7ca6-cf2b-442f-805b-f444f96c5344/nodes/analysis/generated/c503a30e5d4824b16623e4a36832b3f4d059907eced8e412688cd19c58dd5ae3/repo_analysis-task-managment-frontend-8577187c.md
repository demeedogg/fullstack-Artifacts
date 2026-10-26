# Analisi repository frontend — TASK MANAGMENT - 3

## Evidenza esaminata

- Repository: `https://github.com/demeedogg/task-managment-frontend.git`
- Branch richiesto/esaminato: `main`
- Commit: `5ef7900b2fbc037b03f50c58a6fdba9d8ee9c7bd` (`first commit`)
- File tracciati nel commit: solo `README.md`, contenente il titolo `task-managment-frontend`.
- Il checkout è un commit grafted/shallow: non è disponibile ulteriore storia locale da usare come evidenza.
- CodeGraph non ha trovato codice da indicizzare. Non risultano manifesti di dipendenze, sorgenti, configurazioni applicative o test. Di conseguenza non è possibile dedurre framework, architettura, API, comportamento corrente o comandi di test.

Questa analisi riguarda esclusivamente il repository frontend indicato in `objective.repository`. Il backend citato nella descrizione del prodotto e il file Figma non fanno parte dell'evidenza selezionata e non sono stati analizzati qui.

## Stato attuale e scostamento

Nel commit esaminato non è presente un'applicazione frontend implementata: non esistono schermate, navigazione, gestione sessione, client API, componenti responsive o test verificabili. Tutte le funzionalità richieste sono quindi da realizzare; non è possibile attribuire al frontend comportamenti esistenti o rilevare divergenze concrete rispetto a un'implementazione preesistente. Anche compatibilità e vincoli tecnici restano indeterminati finché non viene scelto/aggiunto lo stack e non sono disponibili i contratti backend.

Il brief nomina dashboard, elenco e dettaglio attività, elenco mentor, messaggi, notifiche e impostazioni. La disposizione desktop/mobile e i controlli visivi non sono verificabili da questo repository; la corrispondenza ai frame Figma resta da confrontare in una specifica analisi design.

## Pianificazione delle modifiche frontend

1. **Definire integrazione e modelli condivisi.** Scegliere lo stack e fissare contratti API per identità/ruolo, attività assegnate, consegne versionate, valutazioni, conversazioni, notifiche e preferenze. Chiarire formati di scadenza/fuso orario, paginazione/filtri, errori di autorizzazione e concorrenza. Il repository non offre punti di integrazione esistenti.
2. **Implementare sessione e navigazione per ruolo.** Separare viste e azioni studente/mentor e trattare risposte 401/403, risorsa non trovata e sessione scaduta. Nascondere azioni non consentite migliora l'interfaccia, ma non sostituisce l'autorizzazione server-side: accessi diretti a risorse e API devono essere negati dal backend.
3. **Costruire dashboard e liste.** Realizzare dashboard, elenco attività, filtri/intervalli temporali e dettaglio attività. Usare lo stesso insieme autorizzato e gli stessi filtri per conteggi, avanzamento e liste; calcolare il completamento solo dagli stati completati. Distinguere chiaramente attività in revisione da completate.
4. **Aggiungere invio e revisione delle consegne.** Consentire allo studente di iniziare e inviare un'attività, mostrare scadenza e indicazione di ritardo, cronologia delle versioni e feedback di revisione. Consentire al solo mentor assegnato completamento o richiesta di correzioni con motivazione. Rendere read-only l'attività completata per lo studente.
5. **Gestire conflitti e ripetizioni.** Integrare versionamento/ETag o altro token di concorrenza e presentare un conflitto senza sovrascrivere silenziosamente modifiche. Disabilitare o deduplicare l'invio ripetuto lato UI, mantenendo idempotenza lato server. Una valutazione su una versione non più corrente deve produrre un esito esplicito e non apparire come completamento dell'ultima versione.
6. **Implementare comunicazioni e preferenze.** Creare elenco mentor senza esporre le attività di altri studenti; conversazioni accessibili solo ai partecipanti; inbox notifiche con stato di lettura indipendente dalla lettura dei messaggi; impostazione email separata dalle notifiche in-app. Mostrare errori email senza annullare né presentare come fallita la consegna o valutazione già salvata.
7. **Realizzare layout desktop e mobile e verificare parità.** Applicare i frame Figma nelle rispettive dimensioni e mantenere equivalenti autorizzazioni, azioni, stati e risultati. Verificare anche caricamento, liste vuote, errori, conflitti, invii in ritardo e feedback di revisione. I dettagli visuali puntuali sono bloccati dalla mancata analisi del design.

## Regole da preservare nei contratti e nell'interfaccia

- L'interfaccia deve mostrare solo attività/conversazioni dello studente corrente o degli studenti assegnati al mentor; la navigazione diretta non deve aggirare i permessi.
- Le transizioni di stato sono distinte: lo studente avvia/invia in revisione; il mentor assegnato completa o richiede correzioni motivate. Una consegna in revisione non equivale al completamento.
- Ogni invio crea una versione persistente. La puntualità appartiene alla consegna al momento dell'invio, non al momento della valutazione; gli invii tardivi sono ammessi e segnalati.
- Gli aggiornamenti concorrenti e le valutazioni riferite a versioni precedenti richiedono risposte di conflitto/versione esplicite.
- Gli eventi di invio, richiesta correzioni e completamento devono generare notifiche non duplicate per i destinatari coinvolti. Le preferenze email e lo stato di lettura notifiche non devono alterare consegne, valutazioni o stato di lettura delle conversazioni.

## Chiarimenti e dipendenze aperte

- **Backend non verificato in questa analisi:** ottenere una specifica o analizzare il repository backend per confermare endpoint, enforcement dei permessi, transizioni, persistenza delle versioni, idempotenza, concorrenza, calcolo del ritardo e comportamento dei canali di notifica. Senza questi contratti il frontend non può garantire da solo le regole di business.
- **Figma non verificato in questa analisi:** confrontare i frame desktop/mobile e mappare ogni requisito a un controllo/feedback visibile prima di dichiarare la conformità visiva. In particolare, il brief richiede feedback per conflitti e valutazioni su versioni obsolete, esito di invio/errore email, motivazione obbligatoria delle correzioni e stato di ritardo; la presenza e posizione di tali elementi nel design non è accertata. Chiarire con il committente dove e come presentarli qualora manchino dai frame.
- **Scelta tecnica:** framework, autenticazione, gestione cache/stato, component library, convenzioni di test e supporto browser/dispositivi non sono specificati dal repository.

## Verifiche suggerite per l'implementazione

Quando esisteranno codice e contratti, coprire almeno: visibilità per ruolo anche su URL diretti; matrici di transizione e blocco modifica dopo completamento; versioni multiple e invio tardivo; doppio clic e aggiornamenti concorrenti; valutazione di versione superata; coerenza di filtri, conteggi e avanzamento; deduplicazione notifiche e separazione degli stati di lettura/preferenze; equivalenza dei flussi desktop e mobile. Nel commit analizzato non esiste una suite di test da eseguire o estendere.
