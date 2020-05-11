# 4.5 Diagrammi dei package
Vengono presentati qui di seguito i diagrammi UML dei package relativi al backend.

## 4.5.1 Generale
Nel seguente diagramma dei package vengono mostrate tutte le dipendenze che esistono tra i vari package che compongono il backend. 
![!it.qbteam](../Immagini/Backend/package/package-it.qbteam.png)
<figcaption align=center> <em> Diagramma dei package - Package generale </em> </figcaption> 
 
## 4.5.2 Model
Nel seguente diagramma vengono rappresentate le classi che compongono il package del modello.  
![!model](../Immagini/Backend/package/package-model.png)
<figcaption align=center> <em> Diagramma dei package - Package del modello </em> </figcaption>

## 4.5.3 API
Nel seguente diagramma vengono rappresentate le interfacce che compongono il package delle api, che corrispondo alle interfacce per i Controller.
![!api](../Immagini/Backend/package/package-api.png)
<figcaption align=center> <em> Diagramma dei package - Package delle API</em> </figcaption>

## 4.5.4 Controller
Nel seguente diagramma vengono rappresentate le classi che compongono il package dei controller, che corrispondono alle classi che possiedono i metodi che rispondo alle richieste REST dei client (app utenti e web-app amministratori).
![!controller](../Immagini/Backend/package/package-controller.png)
<figcaption align=center> <em> Diagramma dei package - Package del controller</em> </figcaption>

## 4.5.5 Service
Nel seguente diagramma vengono rappresentate le interfacce che compongono il package dei service, che rappresentano le interfacce per le classi del package serviceimpl.
![!service](../Immagini/Backend/package/package-service.png)
<figcaption align=center> <em> Diagramma dei package - Package dei service </em> </figcaption>

## 4.5.6 Serviceimpl
Nel seguente diagramma vengono rappresentate le classi che implementano le interfacce del package Service e vanno a comporre il package ServiceImpl.  
![!serviceimpl](../Immagini/Backend/package/package-serviceimpl.png)
<figcaption align=center> <em> Diagramma dei package - Package delle implementazioni dei service</em> </figcaption>

## 4.5.7 Repository
Nel seguente diagramma vengono rappresentate le classi che compongono il package Repository, che rappresenta il persistence layer. Queste interfacce estendono tutte CrudRepository.  
![!repository](../Immagini/Backend/package/package-repository.png)
<figcaption align=center> <em> Diagramma dei package - Package delle repository </em> </figcaption>

## 4.5.8 Movementtracker
Nel seguente diagramma vengono rappresentati i due package che compongono il Movement Tracker. Questo package si occupa di implementare il design pattern Publisher-Subscriber, consigliato nel capitolato. Disaccoppia l'atto di tracciamento dalla memorizzazione dei dati tracciati. I due package interni contengono le classi che si occupano della implementazione nel sistema di **Redis** come *Message Broker*.  
![!movementtracker](../Immagini/Backend/package/package-movementtracker.png)
<figcaption align=center> <em> Diagramma dei package - Package del sistema di tracciamento </em> </figcaption>

## 4.5.9 Exception
Nel seguente diagramma viene rappresentata la classe che compone il package delle Exception.  
![!exception](../Immagini/Backend/package/package-exception.png)
<figcaption align=center> <em> Diagramma dei package - Package delle eccezioni </em> </figcaption>

## 4.5.10 Dipendenze esterne
Nel seguente diagramma vengono rappresentati tutti i package verso i quali il nostro package **it.qbteam** ha dipendenze.  
![!dipendenze esterne](../Immagini/Backend/package/package-dependencies.png)
<figcaption align=center> <em> Diagramma dei package - Package delle dipendenze esterne </em> </figcaption>
