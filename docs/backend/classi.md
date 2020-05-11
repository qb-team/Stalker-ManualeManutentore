# 4.6 Diagrammi delle classi
Vengono presentati qui di seguito i diagrammi UML delle classi relativi al backend.  

!!! info
    Per rendere ogni componente riutilizzabile, mantenibile e facile da testare, si è cercato di progettare componenti che abbiano al loro interno poche responsabilità e che siano il più coese possibili, tenendo però sotto controllo il numero di dipendenze.

## 4.6.1 Diagrammi dei Service

### 4.6.1.1 Access Service
![!Access Service](../Immagini/Backend/Classi/AccessService.png)

L'`Access Service` si occupa di soddisfare le richieste provenienti dai controller per ottenere informazioni sugli accessi di un utente presso un luogo o un'organizzazione.
___

### 4.6.1.2 Administrator Service
![!Administrator Service](../Immagini/Backend/Classi/AdministratorService.png)

L'`Administrator Service` si occupa di soddisfare le richieste provenienti dai controller per ottenere informazioni sugli amministratori di un'organizzazione e per la gestione dei loro permessi.
___

### 4.6.1.3 Authentication Service
![!Authentication Service](../Immagini/Backend/Classi/AuthenticationService.png)

L'`Authentication Service` si occupa di soddisfare le richieste provenienti dai controller per ottenere informazioni sullo stato di autenticazione e i permessi (in questo caso intesi come "essere un utente dell'app" oppure "essere un amministratore della web-app") di un utente.
___

### 4.6.1.4 Favorite Service
![!Favorite Service](../Immagini/Backend/Classi/FavoriteService.png)

Il `Favorite Service` si occupa di soddisfare le richieste provenienti dai controller per ottenere informazioni sulle organizzazioni preferite di un utente dell'app e la gestione della loro lista dei preferiti.
___

### 4.6.1.5 Movement Service
![!Movement Service](../Immagini/Backend/Classi/MovementService.png)

Il `Movement Service` si occupa di soddisfare le richieste provenienti dai controller per tracciare i movimenti (ingressi o uscite) di un utente presso un luogo o un'organizzazione. In questo diagramma si può notare come `OrganizationMovementPublisher` e `PlaceMovementPublisher` implementino l'interfaccia `MovementPublisher`, a loro volta estese rispettivamente da `OrganizationMovementRedisPublisher` e `PlaceMovementRedisPublisher`. L'implementazione delle due tipologie di tracciamento è stata separata per permettere una maggiore flessibilità ed estendibilità delle loro implementazioni, oltre a poter cambiare del tutto lo strumento utilizzato per memorizzare i tracciamenti (Redis) e sostituirlo, senza richiedere che le classi che hanno dipendenze verso i due publisher debbano essere modificate.
___

### 4.6.1.6 Organization Service
![!Organization Service](../Immagini/Backend/Classi/OrganizationService.png)

L'`Organization Service` si occupa di soddisfare le richieste provenienti dai controller per ottenere informazioni sulle organizzazioni e altre funzionalità disponibili agli amministratori, come ad esempio la richiesta di eliminazione dell'organizzazione amministrata.
___

### 4.6.1.7 Place Service
![!Place Service](../Immagini/Backend/Classi/PlaceService.png)

Il `Place Service` si occupa di soddisfare le richieste provenienti dai controller per ottenere informazioni sui luoghi di un'organizzazione e per gestirli.
___

### 4.6.1.8 Presence Service
![!Presence Service](../Immagini/Backend/Classi/PresenceService.png)

Il `Presence Service` si occupa di soddisfare le richieste provenienti dai controller per ottenere informazioni sulle presenze correnti presso un luogo o un'organizzazione.
___

### 4.6.1.9 Report Service
![!Report Service](../Immagini/Backend/Classi/ReportService.png)

Il `Report Service` si occupa di soddisfare le richieste provenienti dai controller per ottenere report tabellari sugli accessi passati presso i luoghi di un'organizzazione da parte di utenti autenticati.
___

## 4.6.2 Diagrammi dei Controller

### 4.6.2.1 Access Controller
![!Access Controller](../Immagini/Backend/Classi/AccessAPI.png)

L'`Access Controller` si occupa di soddisfare le richieste ricevute dai client per ottenere informazioni sugli accessi di un utente presso un luogo o un'organizzazione, servendosi dell'`Access Service`.
___

### 4.6.2.2 Administrator Controller
![!Administrator Controller](../Immagini/Backend/Classi/AdministratorApi.png)

L'`Administrator Controller` si occupa di soddisfare le richieste ricevute dai client per ottenere informazioni sugli amministratori di un'organizzazione e per la gestione dei loro permessi, servendosi dell'`Administrator Service`.
___

### 4.6.2.3 Favorite Controller
![!Favorite Controller](../Immagini/Backend/Classi/FavoriteAPI.png)

Il `Favorite Controller` si occupa di soddisfare le richieste ricevute dai client per ottenere informazioni sulle organizzazioni preferite di un utente dell'app e la gestione della loro lista dei preferiti, servendosi del `Favorite Service`.
___

### 4.6.2.4 Movement Controller
![!Movement Controller](../Immagini/Backend/Classi/MovementAPI.png)

Il `Movement Controller` si occupa di soddisfare le richieste ricevute dai client per tracciare i movimenti (ingressi o uscite) di un utente presso un luogo o un'organizzazione, servendosi del `Movement Service`.
___

### 4.6.2.5 Organization Controller
![!Organization Controller](../Immagini/Backend/Classi/OrganizationAPI.png)

L'`Organization Controller` si occupa di soddisfare le richieste ricevute dai client per ottenere informazioni sulle organizzazioni e altre funzionalità disponibili agli amministratori, come ad esempio la richiesta di eliminazione dell'organizzazione amministrata, servendosi dell'`Organization Service`.
___

### 4.6.2.6 Place Controller
![!Place Controller](../Immagini/Backend/Classi/PlaceAPI.png)

Il `Place Controller` si occupa di soddisfare le richieste ricevute dai client per ottenere informazioni sui luoghi di un'organizzazione e per gestirli, servendosi del `Place Service`.
___

### 4.6.2.7 Presence Controller
![!Presence Controller](../Immagini/Backend/Classi/PresenceAPI.png)

Il `Presence Controller` si occupa di soddisfare le richieste ricevute dai client per ottenere informazioni sulle presenze correnti presso un luogo o un'organizzazione, servendosi del `Presence Service`.
___

### 4.6.2.8 Report Controller
![!Report Controller](../Immagini/Backend/Classi/ReportAPI.png)

Il `Report Controller` si occupa di soddisfare le richieste ricevute dai client per ottenere report tabellari sugli accessi passati presso i luoghi di un'organizzazione da parte di utenti autenticati, servendosi del `Report Service`.
___

## 4.6.3 Diagrammi di altre classi

### 4.6.3.1 Authentication Facade
![!Authentication Facade](../Immagini/Backend/Classi/AuthenticationFacade.png)

L'`Authentication Facade` è una classe che implementa il design pattern Facade. Si occupa di raggruppare tutte le funzionalità comuni ai vari controller fornendole da un unico punto di accesso. Queste funzionalità sono quelle offerte dall'`Authentication Service`, per verificare lo stato di autenticazione di un utente o amministratore, e quelle del Permission Service, per verificare se un utente è amministratore o meno e se ha i permessi presso una determinata organizzazione.

### 4.6.3.2 Movement Subscriber
![!Movement Subscriber](../Immagini/Backend/Classi/MovementSubscriber.png)

Avendo deciso di implementare il pattern Publisher-Subscriber, se il Movement Service dispone del publisher, deve esserci anche un subscriber. In questo caso, il subscriber si occupa di ottenere i messaggi dal Message Broker, di analizzarli per convertirli da semplici movimenti (di ingresso o di uscita) in istanze (parziali) di accessi che vengono memorizzate tramite i supporti di persistenza per poterli ottenere successivamente tramite le API fornite per gli Access.