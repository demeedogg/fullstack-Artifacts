# Analisi planning — task-managment-backend

## Ambito ed evidenza

Analisi del solo repository indicato nell'obiettivo, `https://github.com/demeedogg/task-managment-backend`, branch `main`, commit `4985e4cfb8d0135b7aecf7b1b6e7412d1e443396` (2026-10-16, `first commit`). Il tree a quel commit contiene esclusivamente `README.md`, il cui unico contenuto è il titolo `task-managment-backend`. Non sono presenti istruzioni di repository, codice applicativo, configurazione, dipendenze, schema dati, API, migrazioni o test. CodeGraph non ha trovato codice indicizzabile. L'analisi è quindi una valutazione di copertura e un piano, non una descrizione di comportamento implementato.

La richiesta complessiva cita anche frontend e Figma, ma questo input seleziona il backend come unica fonte di evidenza. Non sono state dedotte funzionalità o schermate da quei materiali.

## Stato attuale e vincoli verificabili

- Non è possibile confermare autenticazione, ruoli, assegnazioni mentor-studente, persistenza o alcun endpoint.
- Non risultano flussi esistenti, contratti d'integrazione o vincoli tecnologici da preservare. La scelta di stack e architettura backend resta aperta.
- Non sono presenti test che documentino o verifichino i requisiti; non è stato eseguito alcun build o test.
- Non emergono contraddizioni osservabili tra comportamento implementato e requisiti: il repository non espone comportamento applicativo con cui confrontarli. Questo non prova che gli altri repository o il design siano coerenti.

## Piano backend rispetto ai requisiti

1. **Identità e autorizzazione (requisito 1).** Definire utenti e ruoli studente/mentor, assegnazioni e policy server-side. Applicare lo scope dell'attore a ogni lettura e mutazione, incluse risorse richieste per ID, conversazioni e aggregazioni dashboard; l'elenco mentor non deve concedere accesso alle attività di studenti non assegnati. Verificare accessi consentiti e negati per entrambi i ruoli.
2. **Attività e transizioni (requisito 2).** Modellare gli stati `da iniziare`, `in corso`, `in revisione`, `da correggere`, `completata` e consentire soltanto transizioni valide. Autorizzare l'avvio e l'invio allo studente proprietario; limitare completamento e richiesta di correzioni al mentor assegnato. Rendere obbligatoria e persistente la motivazione della correzione. Rifiutare modifiche dello studente a un'attività completata.
3. **Consegne versionate e scadenze (requisito 3).** Conservare ogni invio come versione immutabile con autore e istante di invio; collegare ogni valutazione alla versione precisa esaminata. Calcolare il ritardo rispetto all'istante della consegna, non a quello della revisione, e accettare invii tardivi marcandoli come tali.
4. **Concorrenza e idempotenza (requisito 4).** Proteggere gli aggiornamenti concorrenti con versione/ETag o controllo atomico equivalente, restituendo conflitto invece di sovrascrivere. Rendere l'invio idempotente (ad esempio chiave idempotenza) contro doppio clic e retry. Accettare una valutazione solo per la versione indicata e impedire che una valutazione obsoleta completi implicitamente l'ultima versione: definire una risposta esplicita di conflitto/stato da riconciliare.
5. **Dashboard coerente (requisito 5).** Derivare conteggi e percentuali da query autorizzate e dalla stessa definizione di filtri/intervalli usata nelle liste. Calcolare il completamento esclusivamente dalle attività in stato completato, non da quelle in revisione. Verificare che filtri temporali e fuso orario siano applicati coerentemente a indicatori e risultati.
6. **Messaggi e notifiche (requisito 6).** Modellare conversazioni e partecipanti con autorizzazione per studente e mentor coinvolti; mantenere separati lo stato di lettura della notifica e quello dei messaggi. Produrre notifiche in-app distinte dalla preferenza email e deduplicarle per evento/destinatario. Disaccoppiare la consegna email (per esempio tramite outbox e retry) dalla transazione di invio o valutazione, così un errore email non annulla l'azione primaria.
7. **Client desktop/mobile (requisito 7).** Esporre contratti e regole server-side identici per entrambi i client. La disposizione dei frame è responsabilità dei client e non è verificabile in questo repository.

## Contratti e decisioni da chiarire

- Precisare il tipo di contenuto della consegna (testo, file o entrambi), limiti e sostituzione degli allegati; il repository non offre un contratto da riutilizzare.
- Definire precisione e fuso della scadenza (timestamp o data locale) e il trattamento di attività senza scadenza.
- Definire la riconciliazione di una valutazione su versione superata: il requisito vieta il completamento automatico della versione più recente, ma non specifica se rifiutare la valutazione o registrarla solo sulla versione storica.
- Precisare come cambiano accesso e responsabilità quando uno studente viene riassegnato a un mentor e chi conserva visibilità sulle consegne/conversazioni storiche.
- Il testo chiede di individuare le azioni e i feedback richiesti dal business ma assenti nei frame Figma. Il solo repository backend non consente di identificare punti precisi nel design; serve l'analisi del materiale Figma e dei frame desktop/mobile prima di dichiarare coperto quel confronto.

## Sequenza di implementazione e verifica

1. Scegliere stack e confini API; definire schema per identità, assegnazioni, attività, versioni consegna, valutazioni, conversazioni, notifiche e preferenze.
2. Implementare autorizzazione e transizioni di stato, quindi test d'integrazione con attore autorizzato/non autorizzato e accesso diretto per ID.
3. Implementare invio versionato, scadenze, controllo concorrenza e idempotenza; testare invii ripetuti, aggiornamenti concorrenti e revisione di versione obsoleta.
4. Implementare dashboard, messaggi e notifiche con test su scope, coerenza dei conteggi, deduplicazione e fallimento email senza rollback.
5. Validare i contratti con i due client e il design una volta disponibili le analisi frontend/Figma; mantenere equivalenza dei risultati desktop/mobile.

Non è possibile stimare modifiche incrementali, riuso o compatibilità con l'implementazione attuale: al commit analizzato non è presente una base backend oltre al README.
