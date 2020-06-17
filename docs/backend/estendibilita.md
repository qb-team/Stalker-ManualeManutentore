# 4.3 Estendibilità

In questa pagina del Manuale Manutentore sono indicate tutte le possibili modifiche effettuabili secondo alcuni criteri che crediamo necessari evidenziare (per esempio la sostituzione di Firebase con un altro provider di autenticazione) oppure punti non sviluppati dal prodotto software rilasciato e che si ritengono utili da implementare per rendere ancora più robusto il sistema.

<a name="sostituire-firebase"></a>
## 4.3.1 Sostituire Firebase
Il backend attualmente fornisce Firebase come sistema di autenticazione, ma è possibile sostituirlo con un qualsiasi altro sistema di autenticazione che abbia le seguenti caratteristiche:

- Permetta la registrazione e l'autenticazione con almeno un indirizzo e-mail e una password;
- Permetta il reset della password se dimenticata;
- Una volta autenticati, restituisca un JWT (acronimo di JSON Web Token) utilizzabile come access token per verificare l'autenticazione;
- Permetta di verificare se un access token è valido, non valido o scaduto;
- Permetta, dato un access token, di ottenere un identificativo dell'utente sotto forma di stringa alfanumerica;
- Permetta, dato un access token, di ottenere l'indirizzo e-mail dell'account annesso.

Se si dispone di un sistema di autenticazione con queste caratteristiche è possibile sostituire Firebase. Ovviamente va sostituito anche nell'applicazione utenti e nella web-app il riferimento a Firebase, poiché non potranno più autenticarsi con Firebase e successivamente inoltrare l'access token al backend: non verrebbe accettato.

I passi per la sostituzione sono i seguenti:

- Eliminazione della classe `FirebaseAdminConfig` appartenente al package `it.qbteam.config`;
- Eliminazione (o rimozione del contenuto) della classe `AdministratorServiceImpl` appartenente al package `it.qbteam.serviceimpl` poiché implementa l'interfaccia `AdministratorService` del package `it.qbteam.service` con le interfacce e le classi della libreria `firebase-admin` di Firebase.

!!! info
    È opzionale, ma è consigliato per una rimozione completa di Firebase, rimuovere il file di configurazione di Firebase (con estensione .json) indicato in [§4.2.10 Firebase Authentication](/backend/requisiti/#firebase-authentication) e [§4.2.11.1 Contenuto della cartella Stalker-Backend](/backend/requisiti/#contenuto-cartella), oltre alle due variabili d'ambiente **FIREBASE_DATABASE_URL** e **GOOGLE_APPLICATION_CREDENTIALS**.

Fatti questi due passaggi è possibile implementare nuovamente l'interfaccia `AdministratorService` in `AdministratorServiceImpl` con le specifiche del nuovo sistema di autenticazione. Se è necessario aggiungere della configurazione, come nel caso di Firebase, inserire la classe di configurazione all'interno del package `it.qbteam.config`.

<a name="rimuovere-https"></a>
## 4.3.2 Rimuovere HTTPS
Il backend così come è stato implementato richiede un certificato HTTPS sotto forma di un file con estensione .jks o .p12, così come spiegato in [Requisiti e installazione](../requisiti).
Può risultare più comodo, specialmente se non si ha a disposizione un certificato HTTPS, disabilitarlo. Per fare ciò è sufficiente rimuovere (o commentare), nel file `application.properties` presente in `src/main/resources` della cartella `Stalker-Backend` scaricata, le righe seguenti:
```yaml
server.ssl.key-alias=${SSL_ALIAS}
server.ssl.key-password=${SSL_PSW}
server.ssl.key-store=classpath:${SSL_KEYSTORE}
server.ssl.key-store-password=${SSL_PSW}
server.ssl.key-store-type=PKCS12
```

<a name="sostituire-ldap"></a>
## 4.3.3 Sostituire LDAP
Il backend attualmente fornisce LDAP come sistema di autenticazione per le organizzazioni, ma è possibile sostituirlo con un qualsiasi altro sistema di autenticazione che abbia le seguenti caratteristiche:

- Permetta la registrazione e l'autenticazione con almeno un identificativo (nome utente o e-mail) e una password;
- Permetta l'apertura e la chiusura di una connessione;
- Permetta di cercare utenti attraverso un identificativo univoco o richiedere la lista intera degli utenti.

Se si dispone di un sistema di autenticazione con queste caratteristiche è possibile sostituire LDAP. Ovviamente va sostituito anche nell'applicazione utenti e nella web-app il riferimento a LDAP, poiché non potranno più autenticarsi con LDAP e successivamente inoltrare l'identificativo al backend, questo perché non verrebbe compreso e si genererebbero errori a runtime.

I passi per la sostituzione sono i seguenti:

- Modifica della classe `AuthenticationServerConfig` appartenente al package `it.qbteam.config`, ritornando con il metodo `authenticationServerConnector()` la nuova implementazione di `AuthenticationServerConnector`, attualmente implementato da `LDAPServerConnectorAdapter`, che può quindi essere rimosso;
- Modifica, se necessaria, della classe `AuthenticationServerServiceImpl` appartenente al package `it.qbteam.serviceimpl` poiché implementa l'interfaccia `AuthenticationServerService` del package `it.qbteam.service`;
- Implementazione di `AuthenticationServerConnector` in una classe che sfrutta librerie o metodologie per connettersi e permettere l'autenticazione attraverso il nuovo sistema di autenticazione.

<a name="terminazione-accessi-obsoleti"></a>
## 4.3.4 Terminazione di accessi obsoleti
Il backend attualmente permette due tipologie di movimenti:

- Entrata, segnalata nel tracciamento con `movementType == -1`;
- Uscita, segnalata nel tracciamento con `movementType == -1`.

Nell'eventualità in cui un utente compia un movimento di entrata e che per un qualsiasi motivo non effettui l'uscita dal luogo o dall'organizzazione dove ha avuto accesso, attualmente il backend non fa alcuna assunzione sulla sua uscita. Ciò significa che un accesso potrebbe non venire mai terminato, rendendo i contatori delle presenze _inquinati_.
Per garantire che non si verifichi questa eventualità una possibile miglioria è avere un meccanismo per cui, sfruttando una nuova tipologia di tracciamento, diciamo con `movementType == 0`, l'utente invia, periodicamente e dopo il primo ingresso, una notifica al sistema informandolo di essere effettivamente ancora all'interno dell'organizzazione o luogo.
A questo punto l'implementazione potrebbe essere la seguente:

- Quando un utente invia un tracciamento di ingresso viene registrato in una nuova struttura dati un record contenente il suo **exitToken** e il timestamp di avvenimento dell'ingresso;
- Periodicamente, diciamo dopo _x_ minuti (da decidere in fase di implementazione), l'utente invia un movimento con `movementType == 0` agli stessi endpoint del tracciamento, con l'**exitToken** che il backend ha fornito nell'atto dell'ingresso e che è necessario per tracciare l'uscita. Questo movimento segnala al backend che l'utente si trova ancora all'interno dello stesso luogo o organizzazione in cui è entrato, il backend ricevuta questa richiesta aggiorna, accedendo alla struttura dati sopra citata, il record con l'**exitToken** dell'utente e mettendo il nuovo timestamp;
- Quando l'utente effettua un tracciamento di un'uscita e inoltra il movimento con `movementType == -1` il backend, oltre a quello che già fa, ha il compito di rimuovere dalla struttura dati già citata il record con il corrispondente **exitToken**;
- Infine, deve esserci un servizio in background del backend (per esempio un microservizio) che ha il compito di controllare periodicamente, diciamo ogni _y_ minuti (da decidere in fase di implementazione), la struttura dati contente gli **exitToken** e i timestamp, verificando che i timestamp memorizzati non siano più vecchi di _x_ + _z_ minuti (tempo dopo il quale l'utente invia il movimento con `movementType == 0` più un tempo di scarto, da decidere in fase di implementazione, per avere un certo tipo di tolleranza a possibili ritardi da parte dell'utente e da parte della rete nell'invio e ricezione del tracciamento). Se il servizio trova un timestamp più vecchio di _x_ + _z_ minuti, effettua un tracciamento di un movimento di uscita con l'**exitToken** corrispondente e il timestamp associato trovato. In caso l'utente successivamente inoltri il movimento di uscita mancante, esso non verrà considerato in quanto l'accesso con quell'**exitToken** è già stato concluso.