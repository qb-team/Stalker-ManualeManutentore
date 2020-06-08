# 4.7 Diagrammi di Sequenza
Vengono presentati qui di seguito i diagrammi UML di sequenza relativi al backend.

## 4.7.1 POST /movement/track/place
![!diagramma di sequenza della ricezione di un movimento](/Immagini/Backend/Sequenza/tracciamento-sequenza.png)

Questo diagramma di sequenza rappresenta il comportamento del backend quando si effettua una richiesta HTTP POST */movement/track/place*.  
Come si può vedere viene restituita uno stato HTTP 401 **Unauthorized** nel caso in cui l'utente che ha effettuato la richiesta non sia autenticato su Firebase o ha fornito un access token non valido.
