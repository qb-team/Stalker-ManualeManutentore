# 3.5 Diagrammi dei package
Vengono presentati qui di seguito i diagrammi UML dei package relativi alla applicazione web.
## 3.5.1 Visione generale delle dipendenze tra package
Nel seguente diagramma UML dei package vengono mostrate tutte le dipendenze che esistono tra i vari package.
<div align="center">
  ![!Dipendenze](../Immagini/WebApp/PDiagram.png "Diagramma dei package - Visione delle dipendenze")
  <figcaption align="center"> <em> Diagramma dei package - Visione delle dipendenze </em> </figcaption>
</div>

## 3.5.2 Tracking
Nel seguente package vengono raggruppate tutte le classi dedicate alle attività di monitoraggio, le quali condividono le stesse dipendenze. Si è scelto di fare un ulteriore sotto raggruppamento tra classi dedicate al monitoraggio di utenti anonimi separando la classe dedicata al monitoraggio di utenti riconosciuti.
<div align="center">
![!Tracking](../Immagini/WebApp/Trackingpackage.png "Diagramma dei package del Tracking")
<figcaption align="center"> <em> Diagramma dei package - Package del Tracking </em> </figcaption>
</div>

## 3.5.3 Organization
Nel seguente package vengono raggruppate tutte le classi dedicate alle funzionalità eseguite sulle organizzazioni e loro relativi luoghi, le quali condividono le stesse dipendenze. Si è scelto di creare 3 sotto package, uno per la gestione delle informazioni di una organizzazione, uno per la gestione dell'area di tracciamento dell'organizzazione e un altro analogo per i luoghi.
<div align="center">
![!Organization](../Immagini/WebApp/OrganizationPackage.png "Diagramma dei package del Organization")
<figcaption align="center"> <em> Diagramma dei package - Package del Organization </em> </figcaption>
</div>

## 3.5.4 Services
Nel seguente package vengono raggruppate tutti i services che contengono informazioni e metodi molto riutilizzati all'interno della applicazione web.
<div align="center">
![!Services](../Immagini/WebApp/ServicesPackage.png "Diagramma dei package dei Services")
<figcaption align="center"> <em> Diagramma dei package - Package dei Services </em> </figcaption>
</div>

## 3.5.5 API
Nel seguente package vengono raggruppate tutti le API utilizzate per comunicare con il backend.
<div align="center">
![!API](../Immagini/WebApp/APIPackage.png "Diagramma dei package delle API")
<figcaption align="center"> <em> Diagramma dei package - Package delle API </em> </figcaption>
</div>

## 3.5.6 UserNoAuthenticated
Nel seguente package vengono raggruppate tutte le component che vengono utilizzate solo quando l'utente non è autenticato.
<div align="center">
![!UserNoAuthenticated](../Immagini/WebApp/UserNoAuthenticatedPackage.png "Diagramma dei package del UserNoAuthenticated")
<figcaption align="center"> <em> Diagramma dei package - Package del UserNoAuthenticated </em> </figcaption>
</div>

## 3.5.7 AdminManagement
Nel seguente package vengono raggruppate tutte le component utilizzate per il tracciamento di utenti riconosciuti.
<div align="center">
  ![!UserNoAuthenticated](../Immagini/WebApp/AdminManagementPackage.png "Diagramma dei package del AdminManagement")
  <figcaption align="center"> <em> Diagramma dei package - Package del AdminManagement </em> </figcaption>
</div>
<br/>