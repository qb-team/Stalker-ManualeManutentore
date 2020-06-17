# 4.6 Diagrammi delle classi
Vengono presentati qui di seguito i diagrammi UML delle classi relativi al backend.  

!!! info
    Per rendere ogni componente riutilizzabile, mantenibile e facile da testare, si è cercato di progettare componenti che abbiano al loro interno poche responsabilità e che siano il più coese possibili, tenendo però sotto controllo il numero di dipendenze.

## 4.6.1 Diagrammi dei Service

### 4.6.1.1 AccessService
![!AccessService](../Immagini/Backend/Classi/AccessService.png)
<figcaption align=center> <em> Diagramma delle classi - AccessService </em> </figcaption>

L'`AccessService` si occupa di soddisfare le richieste provenienti dai controller per ottenere informazioni sugli accessi di un utente presso un luogo o un'organizzazione.

Sono disponibili i seguenti metodi:

- `getAnonymousAccessListInOrganization`: ritorna una lista di **OrganizationAccess** che rappresenta tutti gli accessi di un utente anonimo (tracciati nel sistema tramite degli **exitToken** che permettono di reperire gli accessi a posteriori dall'utente che li ha effettuati) all'interno di una specifica organizzazione, identificata dal suo **organizationId**. Viene utilizzato il metodo `findByExitTokenAndOrganizationId` dell'interfaccia **OrganizationAccessRepository** che opera la query sul database per ottenere gli accessi dell'utente. Questa chiamata viene ripetuta per tutti gli *exitToken* passati al metodo e viene composta così la lista finale;
- `getAnonymousAccessListInPlace`: ritorna una lista di **PlaceAccess** che rappresenta tutti gli accessi di un utente anonimo (tracciati nel sistema tramite degli **exitToken** che permettono di reperire gli accessi a posteriori dall'utente che li ha effettuati) all'interno di uno specifico luogo di un'organizzazione, identificato dal suo **placeId**. Viene utilizzato il metodo `findByExitTokenAndPlaceId` dell'interfaccia **PlaceAccessRepository** che opera la query sul database per ottenere gli accessi dell'utente. Questa chiamata viene ripetuta per tutti gli *exitToken* passati al metodo e viene composta così la lista finale;
- `getAuthenticatedAccessListInOrganization`: ritorna una lista di *OrganizationAccess* che rappresenta tutti gli accessi di un insieme di utenti riconosciuti, tramite il loro codice identificativo nel server di autenticazione dell'organizzazione (**orgAuthServerId**), all'interno di un'organizzazione che permette il tracciamento autenticato, identificata dal suo **organizationId**. Viene utilizzato il metodo `findByOrgAuthServerIdAndOrganizationId` dell'interfaccia **OrganizationAccessRepository** per ottenere tutti gli accessi di un utente dato il suo identificativo e l'id dell'organizzazione. Viene chiamato per ogni *orgAuthServerId* passato ottenendo la lista completa di tutti gli accessi di tutti gli utenti richiesti;
- `getAuthenticatedAccessListInPlace`: ritorna una lista di *PlaceAccess* che rappresenta tutti gli accessi di un insieme di utenti riconosciuti, tramite il loro codice identificativo nel server di autenticazione dell'organizzazione (**orgAuthServerId**), all'interno di un luogo di un'organizzazione che permette il tracciamento autenticato, identificato dal suo **placeId**. Viene utilizzato il metodo `findByOrgAuthServerIdAndPlaceId` dell'interfaccia **OrganizationAccessRepository** per ottenere tutti gli accessi di un utente dato il suo identificativo e l'id del luogo. Viene chiamato per ogni *orgAuthServerId* passato ottenendo la lista completa di tutti gli accessi di tutti gli utenti richiesti.

### 4.6.1.2 AdministratorService
![!AdministratorService](../Immagini/Backend/Classi/AdministratorService.png)
<figcaption align=center> <em> Diagramma delle classi - AdministratorService </em> </figcaption>

L'`AdministratorService` si occupa di soddisfare le richieste provenienti dai controller per ottenere informazioni sugli amministratori di un'organizzazione e per la gestione dei loro permessi.

Sono disponibili i seguenti metodi:

- `bindAdministratorToOrganization`: assegna un amministratore già esistente ad una organizzazione esistente. Il parametro di tipo **Permission** contiene tutte le informazioni necessarie al metodo; Viene utilizzato il metodo `save` dell'interfaccia **PermissionRepository** (che lo eredita da **CrudRepository** di **org.springframework.data.repository**) per salvare nel database l'oggetto di tipo **Permission** che rappresenta i privilegi di gestione (intesi in senso generico, quindi possono essere di visualizzazione - viewer -, gestione - manager -, possesso - owner -) concessi all'amministratore all'interno di una organizzazione;
- `createNewAdministratorInOrganization`: crea un nuovo account per un amministratore nel provider di autenticazione e ne assegna i permessi ad un'organizzazione tramite l'oggetto **Permission**. Viene utilizzato il metodo `save` dell'interfaccia **PermissionRepository** per salvare nel database il nuovo amministratore;  
- `getAdministratorListOfOrganization`: ritorna una lista di **Permission** che rappresenta l'insieme di amministratori che operano in una data organizzazione identificata dal suo **organizationId**. Viene utilizzato il metodo `findByOrganizationId` dell'interfaccia **PermissionRepository** per ottenere tutti gli amministratori in una organizzazione;
- `getPermissionList`: ritorna una lista di **Permission** che rappresenta tutte le organizzazioni in cui un dato amministratore (identificato tramite **administratorId**) ha permessi di gestione (intesi in senso generico). Viene utilizzato il metodo `findByAdministratorId` dell'interfaccia **PermissionRepository**; 
- `updateAdministratorPermission`: ritorna un oggetto di tipo **Permission** all'interno di un Optional (wrapper per oggetti introdotto in Java 8 e disponibile nel package **java.util**) che contiene le modifiche appena apportate ai permessi di uno specifico amministratore all'interno di un'organizzazione richieste passando a questo metodo un parametro di tipo **Permission**. Viene utilizzato il metodo `save` dell'interfaccia **PermissionRepository**;
- `unbindAdministratorFromOrganization`: cancella i permessi di un amministratore da un'organizzazione passando al metodo un oggetto di tipo **Permission**. Viene utilizzato il metodo `deleteById` dell'interfaccia **PermissionRepository** (che lo eredita).  

### 4.6.1.3 AuthenticationServerService
![!AuthenticationServerService](../Immagini/Backend/Classi/AuthenticationServerService.png)
<figcaption align=center> <em> Diagramma delle classi - AuthenticationServerService </em> </figcaption>

L'`AuthenticationServerService` si occupa di soddisfare le richieste provenienti dai controller per ottenere informazioni sulle utenze presenti nel server che autentica gli utenti dell'organizzazione. L'indirizzo del server a cui inoltrare le richieste è indicato nell'organizzazione, attraverso il campo **authenticationServerURL**.

- `getUserInfoFromAuthServer`: ritorna una lista di **OrganizationAuthenticationServerInformation** che rappresenta tutte le informazioni degli utenti richiesti, e di cui sono stati passati gli identificativi (**orgAuthServerId**) al metodo tramite l'oggetto **OrganizationAuthenticationServerRequest**, che nel campo orgAuthServerIds contiene una lista di stringhe con gli identificativi degli utenti per i quali ritornare le informazioni. Nell'implementazione per LDAP, in **LDAPServerConnectorAdapter**, orgAuthServerIds può contenere un singolo elemento ( **\***, un asterisco) e sta a significare che si intendono ottenere tutte le informazioni di tutti gli utenti dell'organizzazione. Condizione necessaria: l'organizzazione della quale si vogliono ricevere informazioni sugli utenti deve permettere il tracciamento autenticato.

### 4.6.1.4 AuthenticationService
![!AuthenticationService](../Immagini/Backend/Classi/AuthenticationService.png)
<figcaption align=center> <em> Diagramma delle classi - AuthenticationService </em> </figcaption>

L'`AuthenticationService` si occupa di soddisfare le richieste provenienti dai controller per ottenere informazioni sullo stato di autenticazione e i permessi (in questo caso intesi come "essere un utente dell'app" oppure "essere un amministratore della web-app") di un utente.    

Nella sua implementazione attraverso il provider di autenticazione [Firebase](requisiti.md#firebase-authentication), sono disponibili i seguenti metodi:

- `checkToken`: metodo privato che data una stringa utilizza il metodo `verifyIdToken` della classe **FirebaseAuth** per determinare se l'utente è autenticato tramite Firebase.  
- `isWebAppAdministrator`: data una stringa **accessToken** determina, utilizzando il metodo `getFirebaseUser` e `findByAdministratorId` di **PermissionRepository**, se l'utente identificato dall'**accessToken** sia un amministratore; in caso il token non sia valido lancia una **AuthenticationException**.  
- `isAppUser`: data una stringa **accessToken** determina, utilizzando il metodo `getFirebaseUser` e `findByAdministratorId`, se l'utente identificato dall'**accessToken** non sia un amministratore; in caso il token non sia valido lancia una **AuthenticationException**.   
- `createUser`: date tre stringhe (accessToken, email, password) utilizza il metodo `createUser` della classe **FirebaseAuth** per creare un utente su Firebase. Se l'operazione non ha successo ritorna **false**, mentre se avviene con successo ritorna **true**; in caso il token non sia valido lancia una **AuthenticationException**;  
- `getUserIdByEmail`: date due stringhe (accessToken, email) ritorna un **Optional&lt;String&gt;** che rappresenta l'identificativo dell'utente. Utilizza il metodo `getUserByEmail` della classe **FirebaseAuth**; in caso l'**accessToken** non fosse valido lancia una **AuthenticationException**, se invece non viene trovato l'identificativo dell'utente ritorna **Optional.empty()**;
- `getUserId`: ritorna l'identificativo dell'utente dato il suo **accessToken**, utilizzando il metodo `getFirebaseUser`; in caso il token non sia valido lancia una **AuthenticationException**;
- `getFirebaseUser`: ritorna un **Optional&lt;FirebaseToken&gt;** dato un **accessToken** utilizzando il metodo `verifyIdToken` della classe **FirebaseAuth**, se quest'ultimo metodo lancia una **FirebaseAuthException** `getFirebaseUser` ritorna **Optional.empty()**; 
- `getEmailByUserId`: ritorna **Optional&lt;String&gt;** contenente l'email dell'utente identificato da **userId**, utilizza il metodo `getUser` della classe **FirebaseAuth**, ritorna **Optional.empty()** nel caso in cui userId fornito sia vuoto o nullo, oppure se la chiamata di `getUser` lancia una **FirebaseAuthException** o **IllegalArgumentException**; nel caso l'**accessToken** passato non sia valido lancia **AuthenticationException**.  

### 4.6.1.5 FavoriteService
![!FavoriteService](../Immagini/Backend/Classi/FavoriteService.png)
<figcaption align=center> <em> Diagramma delle classi - FavoriteService </em> </figcaption>

Il `FavoriteService` si occupa di soddisfare le richieste provenienti dai controller per ottenere informazioni sulle organizzazioni preferite di un utente dell'app e la gestione della loro lista dei preferiti.  

- `addFavoriteOrganization`: fornisce la possibilità per un utente di salvare un'organizzazione nei preferiti (nell'app utenti indicata come MyStalkersList) associando il suo identificativo all'identificativo dell'organizzazione nell'oggetto **Favorite** che riceve il metodo e quest'ultimo, utilizzando il metodo `save` della classe **FavoriteRepository** (che lo eredita come è stato detto fin qui per **PermissionRepository**), lo salva sul database e ritorna il risultato di tale operazione;
- `getFavoriteOrganizationList`: ritorna una lista di **Organization** che rappresenta tutte le organizzazioni inserite tra i preferiti da parte di uno specifico utente identificato dal suo **userId**. Viene utilizzato il metodo `findAllFavoriteOfOneUserId` della classe **FavoriteRepository** per ottenere tutti gli oggetti **Favorite** associati a un utente e in seguito utilizza il metodo `findAllById` della classe **OrganizationRepository** per ottenere tutte le organizzazioni contenute nella lista di **Favorite**;
- `removeFavoriteOrganization`: rimuove un oggetto **Favorite** dal database grazie al metodo `deleteById` della classe **FavoriteRepository** (che lo eredita, al solito);
- `getFavorite`: determina la presenza o meno di un record di tipo **Favorite** nel database grazie al metodo `existsById` della classe **FavoriteRepository** che accetta un parametro **FavoriteId** e ritorna **true** in caso sia già salvato, **false** in caso contrario.

### 4.6.1.6 MovementService
![!MovementService](../Immagini/Backend/Classi/MovementService.png)
<figcaption align=center> <em> Diagramma delle classi - MovementService </em> </figcaption>

Il `MovementService` si occupa di soddisfare le richieste provenienti dai controller per tracciare i movimenti (ingressi o uscite) di un utente presso un luogo o un'organizzazione. In questo diagramma si può notare come `OrganizationMovementPublisher` e `PlaceMovementPublisher` implementino l'interfaccia `MovementPublisher`, a loro volta estese rispettivamente da `OrganizationMovementRedisPublisher` e `PlaceMovementRedisPublisher`. L'implementazione delle due tipologie di tracciamento è stata separata per permettere una maggiore flessibilità ed estendibilità delle loro implementazioni, oltre a poter cambiare del tutto lo strumento utilizzato per memorizzare i tracciamenti (Redis) e sostituirlo, senza richiedere che le classi che hanno dipendenze verso i due publisher debbano essere modificate.

Si dispone dei seguenti metodi:

- `trackMovementInOrganization`: si occupa di verificare l'integrità dell'oggetto **OrganizationMovement** e, nel caso il movimento sia d'entrata viene chiamato il metodo `setExitToken` della classe **OrganizationMovement** per salvare nell'oggetto **OrganizationMovement** un **exitToken** generato da `generateExitToken`; in seguito l'oggetto viene passato al metodo `publish` della classe **OrganizationMovementPublisher** per essere pubblicato su un canale Publisher/Subscriber di Redis;
- `trackMovementInPlace`: si occupa di verificare l'integrità dell'oggetto **PlaceMovement** e, nel caso il movimento sia d'entrata viene chiamato il metodo `setExitToken` della classe **PlaceMovement** per salvare nell'oggetto **PlaceMovement** un **exitToken** generato da `generateExitToken`; in seguito l'oggetto viene passato al metodo `publish` della classe **PlaceMovementPublisher** per essere pubblicato su un canale Publisher/Subscriber di Redis;
- `generateExitToken`: ritorna una stringa contenente caratteri alfanumerici randomizzati che rappresentano un **exitToken**.  

### 4.6.1.7 OrganizationService
![!OrganizationService](../Immagini/Backend/Classi/OrganizationService.png)
<figcaption align=center> <em> Diagramma delle classi - OrganizationService </em> </figcaption>

L'`OrganizationService` si occupa di soddisfare le richieste provenienti dai controller per ottenere informazioni sulle organizzazioni e altre funzionalità disponibili agli amministratori, come ad esempio la richiesta di eliminazione dell'organizzazione amministrata.

Si dispone dei seguenti metodi:

- `getOrganization`: il metodo ritorna un oggetto **Organization** se esiste nel database. Questo oggetto viene identificato tramite **organizationId** e passato al metodo. Rappresenta un'organizzazione presente nel sistema con tutte le informazioni ad essa associate. Viene utilizzato il metodo `findById` di **OrganizationRepository** (che lo eredita) per eseguire l'operazione sul database;  
- `getOrganizationList`: il metodo non richiede parametri e ritorna una lista di **Organization** che rappresenta tutte le organizzazioni presenti nel sistema. Viene utilizzato il metodo `findAll` della classe **OrganizationRepository** (che lo eredita) per ricevere tutte le organizzazioni dal database;  
- `requestDeletionOfOrganization`: il metodo serve a salvare la richiesta di eliminazione di un'organizzazione nel database per essere presa in carico da un'amministratore Stalker. Ha come parametro un oggetto **OrganizationDeletionRequest** che contiene tutte le informazioni necessarie e chiama il metodo `save` della classe **OrganizationDeletionRequestRepository**  (che lo eredita);  
- `updateOrganization`: il metodo aggiorna i dati di un'organizzazione esistente sostituendoli con i nuovi dati passati al metodo tramite l'oggetto **Organization**. Il metodo controlla che l'organizzazione da aggiornare sia presente nel sistema grazie al metodo `findByName` e che l'area di tracciamento si possa aggiornare rispettando i vincoli di grandezza grazie al metodo `canTrackingAreaBeUpdated`;  
- `updateOrganizationTrackingArea`: il metodo aggiorna solamente l'area di tracciamento di un'organizzazione identificata tramite un **organizationId**. La nuova area di tracciamento specificata nel parametro **trackingArea** deve rispettare i vincoli di dimensione imposti per l'organizzazione e il metodo li verifica chiamando `canTrackingAreaBeUpdated`. Se l'organizzazione a cui si vuole aggiornare l'area non viene trovata nel sistema l'operazione restituisce esito negativo.

### 4.6.1.8 PlaceService
![!PlaceService](../Immagini/Backend/Classi/PlaceService.png)
<figcaption align=center> <em> Diagramma delle classi - PlaceService </em> </figcaption>

Il `PlaceService` si occupa di soddisfare le richieste provenienti dai controller per ottenere informazioni sui luoghi di un'organizzazione e per gestirli.

Si dispone dei seguenti metodi:

- `createNewPlace`: crea un nuovo luogo all'interno di una organizzazione. Tutte le informazioni sono contenute nell'oggetto **Place** passato come parametro;  
- `deletePlace`: elimina un luogo da una organizzazione grazie al parametro **Place** passato al metodo, nel caso in cui il luogo specificato non esistesse all'interno dell'organizzazione specificata nell'oggetto **Place** l'operazione non va' a buon fine; utilizza il metodo `delete` della classe **placeRepository**;  
- `updatePlace`: il metodo aggiorna un luogo con le informazioni passate al metodo dal parametro **Place**. L'organizzazione del luogo da aggiornare deve esistere e viene recuperata dal database con il metodo `findById` di **OrganizationRepository**. Successivamente, il metodo controlla che il nuovo luogo sia all'interno dell'organizzazione con il metodo `isPlaceInsideOrganization` e solo allora, e in caso di risposta positiva, salva le modifiche nel database;  
- `getPlace`: il metodo ritorna un'istanza dell'oggetto **Place** che rappresenta un luogo specificato dal parametro **placeId** passato al metodo; utilizza il metodo `findById` della classe **PlaceRepository** per ottenere il luogo dal DB.  

### 4.6.1.9 PresenceService
![!PresenceService](../Immagini/Backend/Classi/PresenceService.png)
<figcaption align=center> <em> Diagramma delle classi - PresenceService </em> </figcaption>

Il `PresenceService` si occupa di soddisfare le richieste provenienti dai controller per ottenere informazioni sulle presenze correnti presso un luogo o un'organizzazione.

Sono implementati i seguenti metodi:

- `getOrganizationPresenceCounter`: si occupa di interrogare Redis per ottenere il numero di persone attualmente all'interno di una organizzazione specificata passando un **organizationId** al metodo. Il contatore viene ottenuto chiamando il metodo `opsForValue` della classe **RedisTemplate** che fornisce il metodo `get` di Redis, con parametro una stringa formata come segue: **"organization:" + organizationId**. La stringa corrisponde alla chiave per ricercare nella memoria delle coppie chiave-valore di Redis. Infine, viene ritornato **Optional** dell'oggetto, dopo aver verificato non sia nullo, e in caso sia nullo viene settato a zero.
- `getPlacePresenceCounter` si occupa di interrogare Redis per ottenere il numero di persone attualmente all'interno di un luogo di un'organizzazione specificata passando un **placeId** al metodo. Il contatore viene ottenuto chiamando il metodo `opsForValue` della classe **RedisTemplate** che fornisce il metodo `get` di Redis, con parametro una stringa formata come segue: **"place:" + placeId**. La stringa corrisponde alla chiave per ricercare nella memoria delle coppie chiave-valore di Redis. Infine, viene ritornato **Optional** dell'oggetto, dopo aver verificato non sia nullo, e in caso sia nullo viene settato a zero.

### 4.6.1.10 ReportService
![!ReportService](../Immagini/Backend/Classi/ReportService.png)
<figcaption align=center> <em> Diagramma delle classi - ReportService </em> </figcaption>

Il `ReportService` si occupa di soddisfare le richieste provenienti dai controller per ottenere record di report tabellari sugli accessi passati presso i luoghi di un'organizzazione da parte di utenti autenticati.  

I metodi sono i seguenti:

- `getDuration`: dati due istanze di **OffsetDateTime**, il metodo calcola la differenza tra la seconda data e la prima trasformandole in secondi e dunque ritorna il numero di secondi trascorsi tra la prima data e la seconda;
- `getTimePerUserReport`: ritorna una lista di **TimePerUserReport** che rappresenta tutti gli accessi a uno specifico luogo degli utenti autenticati di un'organizzazione, il luogo viene indicato passando al metodo un **placeId**; utilizza il metodo `findByPlaceId` della classe **placeAccessRepo** per ottenere tutti gli accessi a un determinato luogo, questi accessi vengono controllati, raggruppati assieme per identificativo **orgAuthServerId** e viene calcolato il tempo trascorso tra l'entrata e l'uscita usando il metodo `getDuration`; infine da una lista di **PlaceAccess** si costruisce la lista di ritorno di **TimePerUserReport**.

## 4.6.2 Diagrammi dei Controller

### 4.6.2.1 AccessApiController
![!AccessApiController](../Immagini/Backend/Classi/AccessAPI.png)
<figcaption align=center> <em> Diagramma delle classi - AccessApiController </em> </figcaption>

L'`AccessApiController` si occupa di soddisfare le richieste ricevute dai client per ottenere informazioni sugli accessi di un utente presso un luogo o un'organizzazione, servendosi dell'`AccessService`. 

I seguenti metodi permettono di rispondere agli end-point offerti dal backend:

- `getAnonymousAccessListInOrganization`: il metodo, in caso di successo (poiché in caso di insuccesso ritorna semplicemente un codice di stato), ritorna una istanza di **List&lt;OrganizationAccess&gt;**, ovvero tutti gli accessi ad un'organizzazione a tracciamento anonimo o autenticato fatti dallo stesso utente che effettua la richiesta. Deve essere passato al metodo uno o più **exitToken** che identificano uno o più accessi dell'utente e un **organizationId** che identifica l'organizzazione della quale ritornare gli accessi;
- `getAnonymousAccessListInPlace`: il metodo, in caso di successo (poiché in caso di insuccesso ritorna semplicemente un codice di stato), ritorna una istanza di **List&lt;PlaceAccess&gt;**, ovvero tutti gli accessi ad un luogo di un'organizzazione a tracciamento anonimo o autenticato fatti dallo stesso utente che effettua la richiesta. Deve essere passato al metodo uno o più **exitToken** che identificano uno o più accessi dell'utente e un **placeId** che identifica il luogo della ;quale ritornare gli accessi;
- `getAuthenticatedAccessListInOrganization`: il metodo, in caso di successo (poiché in caso di insuccesso ritorna semplicemente un codice di stato), ritorna una **List&lt;OrganizationAccess&gt;** che rappresenta tutti gli accessi di uno o più utenti autenticati ad una organizzazione a tracciamento autenticato. Il metodo richiede come parametri una lista di **orgAuthServerId** che, in caso la richiesta sia fatta da un'amministratore, contiene uno o più identificativi degli utenti, mentre se la richiesta viene fatta dal singolo utente sarà presente solo il proprio identificativo; il secondo parametro è invece l'identificativo dell'organizzazione;
- `getAuthenticatedAccessListInPlace`: il metodo, in caso di successo (poiché in caso di insuccesso ritorna semplicemente un codice di stato), ritorna una **List&lt;PlaceAccess&gt;** che rappresenta tutti gli accessi di uno o più utenti autenticati ad un luogo di un'organizzazione a tracciamento autenticato. Il metodo richiede come parametri una lista di **orgAuthServerId** che, in caso la richiesta sia fatta da un'amministratore, contiene uno o più identificativi degli utenti, mentre se la richiesta viene fatta dal singolo utente sarà presente solo il proprio identificativo; il secondo parametro è invece l'identificativo del luogo dell'organizzazione.

### 4.6.2.2 AdministratorApiController
![!AdministratorApiController](../Immagini/Backend/Classi/AdministratorApi.png)
<figcaption align=center> <em> Diagramma delle classi - AdministratorApiController </em> </figcaption>

L'`AdministratorApiController` si occupa di soddisfare le richieste ricevute dai client per ottenere informazioni sugli amministratori di un'organizzazione e per la gestione dei loro permessi, servendosi dell'`AdministratorService`. 

I seguenti metodi permettono di rispondere agli end-point offerti dal backend:

- `bindAdministratorToOrganization`: il metodo, in caso di successo (poiché in caso di insuccesso ritorna semplicemente un codice di stato), assegna ad una organizzazione un amministratore già registrato nel sistema. Questo metodo può essere utilizzato solamente da un amministratore almeno gestore che sia autenticato nel sistema. Come parametro richiede un'istanza di **AdministratorBindingRequest** che contiene tutte le informazioni necessarie. Il metodo controlla che sia l'organizzazione che l'amministratore esistano e dunque chiama il metodo `bindAdministratorToOrganization` della classe **AdministratorService**. In caso di successo nella creazione ritorna l'oggetto **Permission** che rappresenta i permessi dell'amministratore nell'organizzazione;
- `createNewAdministratorInOrganization`: il metodo, in caso di successo (poiché in caso di insuccesso ritorna semplicemente un codice di stato), crea un nuovo amministratore come account nel provider di autenticazione. Il metodo riceve come parametro un'istanza di **AdministratorBindingRequest** che contiene tutte le informazioni necessarie. Il metodo controlla che l'amministratore che effettua la richiesta sia autenticato nel sistema, altrimenti ritorna Unauthorized, e che sia owner dell'organizzazione nella quale vuole creare l'amministratore, altrimenti ritorna Forbidden. In seguito, chiama il metodo `createUserAccount` della classe **AuthenticationFacade** per creare un'utenza su Firebase e poi il metodo `createNewAdministratorInOrganization` della classe **AdministratorService** per creare l'amministratore nell'organizzazione;
- `getAdministratorListOfOrganization`: il metodo, in caso di successo (poiché in caso di insuccesso ritorna semplicemente un codice di stato), ritorna una **List&lt;Permission&gt;** che rappresenta tutti gli amministratori associati ad una determinata organizzazione identificata passando al metodo un **organizationId**. Il metodo controlla che la richiesta sia stata fatta da un amministratore che si è autenticato nel sistema e che sia owner dell'organizzazione per la quale vuole sapere la lista degli amministratori. Per recuperare la lista chiama `getAdministratorListOfOrganization` della classe **AuthenticationFacade**;
- `getPermissionList`: il metodo, in caso di successo (poiché in caso di insuccesso ritorna semplicemente un codice di stato), ritorna una **List&lt;Permission&gt;** che rappresenta le organizzazioni in cui è stato nominato l'amministratore che ha invocato il metodo. Il metodo richiede un **administratorId**; l'amministratore che effettua la richiesta deve essere autenticato nel sistema e l'identificativo che viene inserito come parametro al metodo deve corrispondere all'identificativo dell'amministratore che effettua la richiesta, altrimenti viene ritornato Forbidden. Per ottenere la lista di permessi viene chiamato il metodo `getPermissionList` della classe **AdministratorService**;
- `unbindAdministratorFromOrganization`: il metodo, in caso di successo (poiché in caso di insuccesso ritorna semplicemente un codice di stato), toglie i permessi di un amministratore in una organizzazione. Richiede come parametro un oggetto di tipo **Permission** che contiene tutte le informazioni necessarie. L'amministratore che effettua la richiesta deve essere autenticato nel sistema e deve essere owner dell'organizzazione alla quale fa parte l'amministratore che deve essere rimosso. Per compiere l'operazione viene chiamato il metodo `unbindAdministratorFromOrganization` della classe **AdministratorService**;  
- `updateAdministratorPermission`: il metodo, in caso di successo (poiché in caso di insuccesso ritorna semplicemente un codice di stato), aggiorna il livello di permessi di un amministratore all'interno di una specifica organizzazione. Richiede un oggetto **Permission** come parametro, la richiesta deve essere effettuata da un'amministratore che si è autenticato nel sistema e che sia owner dell'organizzazione nella quale cambiare i permessi dell'amministratore. Per effettuare tale operazione si serve del metodo `updateAdministratorPermission` della classe **AdministratorService**. 

### 4.6.2.3 AuthenticationServerApiController
![!AuthenticationServerApiController](../Immagini/Backend/Classi/AuthenticationServerApiController.png)
<figcaption align=center> <em> Diagramma delle classi - AuthenticationServerApiController </em> </figcaption>

L'`AuthenticationServerApiController` si occupa di soddisfare le richieste ricevute dai client per ottenere informazioni sulle utenze presenti nel server che autentica gli utenti dell'organizzazione, servendosi dell'`AuthenticationServerService`.

Il seguente metodo permette di rispondere all'end-point offerto dal backend:

- `getUserInfoFromAuthServer`: il metodo, in caso di successo (poiché in caso di insuccesso ritorna semplicemente un codice di stato), ritorna un'istanza di **List&lt;OrganizationAuthenticationServerInformation&gt;** che rappresenta tutte le informazioni richieste da un'amministratore che si è autenticato nel sistema tramite un oggetto **OrganizationAuthenticationServerRequest**. La lista di ritorno contiene tanti elementi quanti gli identificativi degli utenti inseriti nella lista interna all'oggetto passato come parametro al metodo.

### 4.6.2.4 FavoriteApiController
![!FavoriteApiController](../Immagini/Backend/Classi/FavoriteAPI.png)
<figcaption align=center> <em> Diagramma delle classi - FavoriteApiController </em> </figcaption>

Il `FavoriteApiController` si occupa di soddisfare le richieste ricevute dai client per ottenere informazioni sulle organizzazioni preferite di un utente dell'applicazione e la gestione della loro lista dei preferiti, servendosi del `FavoriteService`.

I seguenti metodi permettono di rispondere agli end-point offerti dal backend:

- `addFavoriteOrganization`: il metodo, in caso di successo (poiché in caso di insuccesso ritorna semplicemente un codice di stato), riceve come parametro un oggetto **Favorite** e, utilizzando il metodo `addFavoriteOrganization` di **FavoriteService**, salva nel database l'oggetto;
- `getFavoriteOrganizationList`: il metodo, in caso di successo (poiché in caso di insuccesso ritorna semplicemente un codice di stato), ritorna un'istanza di una lista di **Organization** che rappresenta tutte le organizzazioni presenti nella lista dei favoriti di un utente identificato tramite il codice **userId** fornito come parametro al metodo. Per ottenere la lista utilizza il metodo `getFavoriteOrganizationList` della classe **FavoriteService**; 
- `removeFavoriteOrganization`: il metodo, in caso di successo, rimuove un oggetto **Favorite** passato come parametro dalla lista dei preferiti dell'utente che effettua la richiesta, che deve essere necessariamente un utente dell'applicazione in possesso dell'organizzazione nella propria lista di preferiti, altrimenti viene restituito un codice di errore.  

### 4.6.2.5 MovementApiController
![!MovementApiController](../Immagini/Backend/Classi/MovementAPI.png)
<figcaption align=center> <em> Diagramma delle classi - MovementApiController </em> </figcaption>

Il `MovementApiController` si occupa di soddisfare le richieste ricevute dai client per tracciare i movimenti (ingressi o uscite) di un utente presso un luogo o un'organizzazione, servendosi del `MovementService`.

I seguenti metodi permettono di rispondere agli end-point offerti dal backend:

- `trackMovementInOrganization`: il metodo, in caso di successo (poiché in caso di insuccesso ritorna semplicemente un codice di stato), riceve come parametro un oggetto **OrganizationMovement** da parte di un utente dell'applicazione e, utilizzando il metodo `trackMovementInOrganization`, pubblica su un canale Publisher/Subscriber di Redis il movimento. Per poter effettuare questa operazione il metodo controlla che l'utente sia autenticato tramite il provider di autenticazione;  
- `trackMovementInPlace`: il metodo, in caso di successo (poiché in caso di insuccesso ritorna semplicemente un codice di stato), riceve come parametro un oggetto **PlaceMovement** da parte di un utente dell'applicazione e, utilizzando il metodo `trackMovementInPlace`, pubblica su un canale Publisher/Subscriber di Redis il movimento. Per poter effettuare questa operazione il metodo controlla che l'utente sia autenticato tramite il provider di autenticazione;   

### 4.6.2.6 OrganizationApiController
![!OrganizationApiController](../Immagini/Backend/Classi/OrganizationAPI.png)
<figcaption align=center> <em> Diagramma delle classi - OrganizationApiController </em> </figcaption>

L'`OrganizationApiController` si occupa di soddisfare le richieste ricevute dai client per ottenere informazioni sulle organizzazioni e altre funzionalità disponibili agli amministratori, come ad esempio la richiesta di eliminazione dell'organizzazione amministrata, servendosi dell'`OrganizationService`.

I seguenti metodi permettono di rispondere agli end-point offerti dal backend:

- `getOrganization`: il metodo, ricevendo come parametro un identificativo **organizationId** di un'organizzazione, ritorna un'istanza di un oggetto **Organization** che contiene tutte le informazioni sull'organizzazione. Per effettuare questa operazione sia l'utente che amministratore devono essere autenticati tramite il provider di autenticazione;
- `getOrganizationList`: il metodo ritorna un'istanza della lista di tutte le organizzazioni presenti nel sistema. Solo gli utenti dell'applicazione possono inviare questa richiesta. Inoltre, devono anche essere autenticati presso il provider di autenticazione. Il metodo utilizza `getOrganizationList` di **OrganizationService** per leggere all'interno del database;
- `requestDeletionOfOrganization`: il metodo richiede come parametro un oggetto **OrganizationDeletionRequest** che permette solo ad un amministratore owner di eliminare l'organizzazione nella quale possiede questi permessi. L'amministratore deve essere autenticato tramite il provider di autenticazione. Viene utilizzato il metodo `requestDeletionOfOrganization` di **OrganizationService**;
- `updateOrganization`: il metodo richiede come parametro un oggetto **Organization** che contiene le modifiche fatte ad un'organizzazione da parte di un amministratore gestore della stessa. Queste modifiche devono riflettersi su una organizzazione esistente, altrimenti vengono scartate. L'amministratore deve essere autenticato tramite il provider di autenticazione e viene utilizzato il metodo `updateOrganization` di **OrganizationService** per portare a termine la richiesta;  
- `updateOrganizationTrackingArea`: il metodo richiede come parametri l'identificativo dell'organizzazione e una stringa che rappresenta l'area di tracciamento in formato JSON. Il compito del metodo è aggiornare l'area di tracciamento della specificata organizzazione con la nuova area di tracciamento passatagli. Questa modifica può essere effettuata solo da un'amministratore che si è autenticato tramite il provider di autenticazione e almeno manager della stessa organizzazione. Nel caso in cui l'organizzazione non esista o l'area di tracciamento ecceda il limite stabilito o non sia valida, la modifica viene scartata.  

### 4.6.2.7 PlaceApiController
![!PlaceApiController](../Immagini/Backend/Classi/PlaceAPI.png)
<figcaption align=center> <em> Diagramma delle classi - PlaceApiController </em> </figcaption>

Il `PlaceApiController` si occupa di soddisfare le richieste ricevute dai client per ottenere informazioni sui luoghi di un'organizzazione e per gestirli, servendosi del `PlaceService`.

I seguenti metodi permettono di rispondere agli end-point offerti dal backend:

- `createNewPlace`: questo metodo permette a ad un amministratore che si è autenticato di creare un nuovo luogo all'interno di una organizzazione nella quale sia almeno manager. Il metodo richiede come parametro un oggetto di tipo **Place** contenente tutti i dettagli del nuovo luogo da creare. Per creare il luogo il metodo usa `createNewPlace` di **PlaceService**;  
- `deletePlace`: il metodo permette ad un amministratore che si è autenticato di eliminare un luogo da un'organizzazione in cui sia almeno manager. Il metodo richiede come parametro un identificativo **placeId** di un luogo, che verrà passato al metodo `getPlace` della classe **PlaceService** per recuperare l'oggetto **Place** da eliminare. Nel caso si voglia eliminare un luogo inesistente la richiesta non potrà essere soddisfatta e verrà ritornato un codice di errore, in caso il luogo esista viene usato `deletePlace` di **PlaceService** per compiere la rimozione;  
- `updatePlace`: permette ad un amministratore che si è autenticato di modificare l'area di un luogo passando al metodo un oggetto **Place** che sostituirà quello già esistente. L'amministratore deve almeno essere manager dell'organizzazione a cui fa parte il luogo. In caso il luogo inserito non abbia lo stesso codice identificativo di un luogo già esistente la modifica viene scartata;   
- `getPlaceListOfOrganization`: il metodo richiede un identificativo **organizationId** di una organizzazione della quale restituirà tutti i luoghi al suo interno, sia gli utenti dell'applicazione che gli amministratori possono usare questa funzionalità previa autenticazione attraverso il provider di autenticazione.  

### 4.6.2.8 PresenceApiController
![!PresenceApiController](../Immagini/Backend/Classi/PresenceAPI.png)
<figcaption align=center> <em> Diagramma delle classi - PresenceApiController </em> </figcaption>

Il `PresenceApiController` si occupa di soddisfare le richieste ricevute dai client per ottenere informazioni sulle presenze correnti presso un luogo o un'organizzazione, servendosi del `PresenceService`.

I seguenti metodi permettono di rispondere agli end-point offerti dal backend: 

- `getOrganizationPresenceCounter`: il metodo ritorna un'istanza di **OrganizationPresenceCounter** che contiene il numero di utenti attualmente all'interno dell'organizzazione specificata dal **organizationId** passato al metodo. Solo gli amministratori autenticati e appartenenti all'organizzazione specificata possono richiedere il numero delle presenze;  
- `getPlacePresenceCounter`: il metodo ritorna un'istanza di **PlacePresenceCounter** che contiene il numero di utenti attualmente all'interno del luogo specificato dal **placeId** passato al metodo. Solo gli amministratori autenticati e appartenenti all'organizzazione specificata possono richiedere il numero delle presenze.

### 4.6.2.9 ReportApiController
![!ReportApiController](../Immagini/Backend/Classi/ReportAPI.png)
<figcaption align=center> <em> Diagramma delle classi - ReportApiController </em> </figcaption>

Il `ReportApiController` si occupa di soddisfare le richieste ricevute dai client per ottenere report tabellari sugli accessi passati presso i luoghi di un'organizzazione da parte di utenti autenticati, servendosi del `ReportService`.

Il seguente metodo permette di rispondere all'end-point offerto dal backend:

- `getTimePerUserReport`: il metodo ritorna un'istanza di una lista di **TimePerUserReport** che rappresenta il tempo trascorso dagli utenti all'interno di uno specificato luogo passato al metodo tramite **placeId**. L'amministratore deve essere autenticato tramite il provider di autenticazione; viene chiamato il metodo  `getTimePerUserReport` della classe **ReportService** per ottenere i dati da ritornare.

## 4.6.3 Diagrammi di altre classi

### 4.6.3.1 AuthenticationFacade
![!AuthenticationFacade](../Immagini/Backend/Classi/AuthenticationFacade.png)
<figcaption align=center> <em> Diagramma delle classi - AuthenticationFacade </em> </figcaption>

L'`AuthenticationFacade` è una classe che implementa il design pattern Facade. Si occupa di raggruppare tutte le funzionalità comuni ai vari controller fornendole da un unico punto di accesso. Queste funzionalità sono quelle offerte dall'`AuthenticationService`, per verificare lo stato di autenticazione di un utente o amministratore, e quelle del PermissionService, per verificare se un utente è amministratore o meno e se ha i permessi presso una determinata organizzazione.

### 4.6.3.2 GpsAreaFacade
![!GpsAreaFacade](../Immagini/Backend/Classi/GpsAreaFacade.png)
<figcaption align=center> <em> Diagramma delle classi - GpsAreaFacade </em> </figcaption>

Le funzionalità che controllano la dimensione di un'area geografica espressa dall'area di tracciamento (trackingArea) di un'organizzazione o di un luogo vengono realizzate dalle classi che permettono a `GpsAreaFacade` di funzionare. Nuovamente, come dice il nome, viene utilizzato il design pattern Facade per avere un unico punto di accesso alle tre funzionalità di calcolo dell'area data una lista di coordinate geografiche, verifica di appartenenza di un punto all'interno di un certo perimetro e costruzione di oggetti di tipo `Coordinate`, che corrisponde all'interfaccia che permette di elaborare i dati ricevuti dalle trackingArea. Inoltre, le tre interfacce `AreaCalculator`, `CoordinateFactory` e `PointInsidePolygon` sono implementate attualmente in un modo abbastanza semplice, ma potrebbero essere aggiornate o sostituite da altre implementazioni più precise, indicandone l'uso nella configurazione del software.

### 4.6.3.3 MovementSubscriber
![!MovementSubscriber](../Immagini/Backend/Classi/MovementSubscriber.png)
<figcaption align=center> <em> Diagramma delle classi - MovementSubscriber </em> </figcaption>

Avendo deciso di implementare il pattern Publisher-Subscriber, se il MovementService dispone del publisher, deve esserci anche un subscriber. In questo caso, il subscriber si occupa di ottenere i messaggi dal Message Broker, di analizzarli per convertirli da semplici movimenti (di ingresso o di uscita) in istanze (parziali) di accessi che vengono memorizzate tramite i supporti di persistenza per poterli ottenere successivamente tramite le API fornite per gli Access.