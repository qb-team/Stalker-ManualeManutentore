# 2.2 Requisiti e installazione

## 2.2.1 Requisiti
Per poter sviluppare sul proprio PC l'applicazione del sistema Stalker sono necessari i software e gli strumenti indicati in questa pagina.
I software da installare saranno divisi in base al loro scopo.

Per scaricare il codice sorgente dell'applicazione, è sufficiente andare nella pagina di GitHub che lo ospita, che si trova [qui](https://github.com/qb-team/Stalker-App), cliccare su `Clone or download` e successivamente premere su `Download ZIP`.

Un'alternativa più efficace a questo procedimento è scaricare il progetto tramite Git. Se non si dispone di Git è possibile scaricarlo seguendo quanto indicato in [Source Code Management](#source-code-management). Per scaricare il progetto in questo modo, invocare il seguente comando tramite un terminale o prompt dei comandi nel sistema in uso:
```bash
git clone https://github.com/qb-team/Stalker-App.git
```

<a name="prerequisiti"></a>

## 2.2.2 Prerequisiti hardware e software
Le tecnologie utilizzate per sviluppare l'applicazione Android richiedono parecchie risorse nel loro uso contemporaneo. Si consiglia quindi di avere un computer con processore almeno quad-core e una memoria RAM di almeno 8 GB.

## 2.2.3 Ambiente di sviluppo
### 2.2.3.1 Android Studio
L'applicazione è stata sviluppata utilizzando l'ambiente di sviluppo Android Studio, attualmente alla versione 3.6.1.

#### Installazione di Android Studio su Windows
È possibile scaricare Android Studio su Windows visitando il sito ufficiale riportato in seguito, che inoltre fornisce un'ottima documentazione per lo sviluppo di applicazioni. Il link per la pagina da cui si può scaricare Android Studio si trova cliccando [qui](https://developer.android.com/studio), andando alla sezione *"Android Studio downloads"*.  
Per eseguire l'installazione, bisognerà seguire la guida riportata nella sezione **Windows** cliccando nel seguente link [qui](https://developer.android.com/studio/install).

#### Installazione di Android Studio su MacOS
La guida per scaricare Android Studio per MacOS è identica a quella per Windows.  
Per eseguire l'installazione, invece, bisognerà seguire la guida riportata nella sezione **Mac** cliccando nel seguente link [qui](https://developer.android.com/studio/install).

#### Installazione di Android Studio su Ubuntu (e derivate, e altri derivati di Debian)
La guida per scaricare Android Studio per Linux è identica a quella per Windows e MacOS.  
Per eseguire l'installazione, invece, bisognerà seguire la guida riportata nella sezione **Linux** cliccando nel seguente link [qui](https://developer.android.com/studio/install).

## 2.2.4 Linguaggi utilizzati
### 2.2.4.1 Java
L'applicazione è stata sviluppata utilizzando il linguaggio di programmazione Java, in particolare la sua versione 8 (conosciuta come Java 8).

#### Installazione di Java su Windows
È possibile installare Java su Windows visitando il sito ufficiale dell'azienda che lo produce, Oracle. Il link per la pagina da cui si può scaricare Java si trova cliccando [qui](https://www.oracle.com/java/technologies/javase/javase-jdk8-downloads.html). Il link porta alla pagina del sito Oracle per scaricare il Java Development Kit (JDK) 8. Esso include al suo interno anche il Java Runtime Environment (JRE) 8 per l'esecuzione.
Il pacchetto da scaricare una volta all'interno del sito web è quello sotto la voce *Windows x64*.

#### Installazione di Java su MacOS
L'installazione per MacOS è identica a quella per Windows, ad eccezione del fatto che il pacchetto da scaricare è sotto la voce *macOS x64*.

#### Installazione di Java su Ubuntu (e derivate, e altri derivati di Debian)
È possibile installare Java su sistemi Linux invocando i seguenti comandi sul terminale del sistema:
```bash
sudo apt-get update
sudo apt-get install openjdk-8-jre openjdk-8-jdk
```

### 2.2.4.2 XML
La configurazione dell'applicazione e alcune sue dipendenze sono gestite tramite un file denominato **AndroidManifest.xml**.
Inoltre, lo sviluppo di applicazioni Android richiede una cartella di progetto denominata **res** che contiene file XML per gestire risorse come layout, immagini, menu, stringhe ed altro ancora.
Quindi è richiesta una buona conoscenza del linguaggio XML.

## 2.2.5 Librerie utilizzate
### 2.2.5.1 UnboundID SDK
UnboundID SDK è una libreria Java utilizzata per effettuare l'autenticazione su un server LDAP.
Per poterla utilizzare è necessario aggiungere nel file *build.gradle(:app)* la dipendenza:
```bash
implementation 'com.unboundid:unboundid-ldapsdk:4.0.14'
```
La documentazione viene fornita nel seguente [link](https://github.com/pingidentity/ldapsdk).
Per verificare che è stata eseguita una corretta autenticazione su un server LDAP, sono stati svolti dei test seguendo la guida presente al [link](https://www.forumsys.com/tutorials/integration-how-to/ldap/online-ldap-test-server/).

### 2.2.5.2 Retrofit
Retrofit è una libreria Java e Android che permette di utilizzare e gestire i servizi REST, un tipo di architettura software che utilizza il protocollo HTTP per effettuare richieste al server.
Per poterla utilizzare è necessario aggiungere nel file *build.gradle(:app)* la dipendenza: 
```bash
implementation 'com.squareup.retrofit2:retrofit:(2.8.1)'
```
La documentazione viene fornita nel seguente [link](https://square.github.io/retrofit/).

### 2.2.5.3 GSON
Gson è una libreria Java che può essere utilizzata per convertire oggetti Java nella loro rappresentazione JSON o per convertire una stringa JSON in un oggetto Java equivalente. 
Per poterla utilizzare è necessario aggiungere nel file *build.gradle(:app)* la dipendenza: 
```bash
implementation 'com.google.code.gson:gson:2.8.6'
```
La documentazione viene fornita nel seguente [link](https://github.com/google/gson).

### 2.2.5.4 UrlImageViewHelper 
UrlImageViewHelper è una libreria Java che permette di scaricare e gestire automaticamente tutte le immagini Web e ImageView.
Per poterla utilizzare è necessario aggiungere nel file *build.gradle(:app)* la dipendenza:  
```bash
implementation files('libs/urlimageviewhelper-1.0.4.jar')
```
E' necessario scaricare e includere il file eseguibile *urlimageviewhelper-1.0.4.jar*.
La documentazione viene fornita nel seguente [link](https://github.com/koush/UrlImageViewHelper).

<a name="source-code-management"></a>
## 2.2.6 Source code management
Per poter effettuare il versionamento del codice sorgente è richiesto di utilizzare Git.
Per poterlo installare è necessario recarsi a [questa pagina](https://git-scm.com/downloads).  
Non è strettamente necessario, ma è consigliato per integrare le proprie modifiche nel repository.

## 2.2.7 Build automation
La build automation (ovvero la gestione del processo di build) è affidata a Gradle, integrato e utilizzato in Android Studio.
I file di build sono due: uno per tutto il progetto ed uno per il solo modulo app.  
Tramite Gradle il progetto dell'applicazione viene compilato, testato ed eseguito attraverso l'IDE Android Studio.
