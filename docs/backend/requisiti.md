# 4.2 Requisiti e installazione
Per poter sviluppare sul proprio PC il backend del sistema Stalker sono necessari i software e gli strumenti indicati in questa pagina.
I software da installare saranno divisi in base al loro scopo.

<a name="prerequisiti"></a>
## 4.2.1 Prerequisiti hardware e software
Prima di procedere con i software, c'è da fare una premessa obbligatoria.

Le tecnologie utilizzate per sviluppare il backend richiedono parecchie risorse, non tanto prese singolarmente, ma quanto nel loro uso contemporaneo. Si consiglia quindi di avere un computer con processore almeno quad-core e RAM almeno 8 GB.

Per gli utenti Windows, è richiesto di avere il sistema Windows 10 Pro (o Enterprise), nella versione a 64 bit. La versione Windows 10 Home non supporta la virtualizzazione e ciò impedisce di eseguire il backend, seppur sia possibile svilupparne e anche compilare il codice sorgente. Questa versione permette di installare il **WSL - Windows Subsystem for Linux** che non è obbligatorio per lo sviluppo, ma per effettuare i test e verifiche di funzionamento risulta molto comodo.  
Per una guida sull'installazione, visionare la seguente [guida ufficiale](https://docs.microsoft.com/it-it/windows/wsl/install-win10) sul sito di Microsoft.

## 4.2.2 Come ottenere il codice sorgente
Per scaricare il codice sorgente del backend, è sufficiente andare nella pagina di GitHub che lo ospita, che si trova [qui](https://github.com/qb-team/Stalker-Backend), cliccare su `Clone or download` e successivamente premere su `Download ZIP`.

Un'alternativa più efficace a questo procedimento è scaricare il progetto tramite **Git**. Se non si dispone di Git è possibile scaricarlo seguendo quanto indicato in [Source Code Management](#source-code-management). Per scaricare il progetto in questo modo, invocare il seguente comando tramite un terminale o prompt dei comandi nel sistema in uso:
```bash
git clone https://github.com/qb-team/Stalker-Backend.git
```

## 4.2.3 Linguaggi utilizzati
### 4.2.3.1 Java
Il backend è stato sviluppato utilizzando in linguaggio di programmazione Java, in particolare la sua versione 8 (conosciuta come Java 8).

#### Installazione di Java su Windows
È possibile installare Java su Windows visitando il sito ufficiale dell'azienda che lo produce, Oracle. Il link per la pagina da cui si può scaricare Java si trova cliccando [qui](https://www.oracle.com/java/technologies/javase/javase-jdk8-downloads.html).  
Il link porta alla pagina del sito Oracle per scaricare il Java Development Kit (JDK) 8. Esso include al suo interno anche il Java Runtime Environment (JRE) 8 per l'esecuzione.
Il pacchetto da scaricare, una volta all'interno del sito web, è quello sotto la voce *Windows x64*.

#### Installazione di Java su MacOS
L'installazione per MacOS è identica a quella per Windows, ad eccezione del fatto che il pacchetto da scaricare è sotto la voce *macOS x64*.

#### Installazione di Java su Ubuntu (e derivate, e altri derivati di Debian)
È possibile installare Java su Ubuntu invocando i seguenti comandi sul terminale del sistema:
```bash
sudo apt-get update
sudo apt-get install openjdk-8-jre openjdk-8-jdk
```

<a name="xml"></a>
## 4.2.4 XML
Come verrà successivamente illustrato, la configurazione del progetto e la dichiarazione delle dipendenze è gestita tramite un file denominato `pom.xml`, che si trova nella cartella principale scaricata da GitHub, il quale richiede una conoscenza almeno minima della struttura di XML, in caso si renda necessario effettuare alcune modifiche.

<a name="yaml"></a>
## 4.2.5 YAML
Il backend permette all'app e alla web-app di funzionare tramite delle **REST API**. La definizione delle API è stata fatta sfruttando la specifica OpenAPI e gli strumenti offerti da Swagger (per maggiori informazioni, visita la sezione [REST API](/restapi/introduzione/)). Grazie a questi due strumenti è stato possibile generare in maniera semi-automatica:

- Le interfacce per il controller (visita la sezione [Architettura](/restapi/architettura/) per una spiegazione migliore di cosa si intende per Controller) del backend e le classi del modello;
- Il Software Development Kit (SDK) per interrogare le REST API fornite dal backend e il modello sia per l'app Android che per la web-app;
- La documentazione in formato HTML e Markdown delle REST API.

La specifica delle API si presenta sotto forma di un file .yaml chiamato all'interno del progetto `stalker.yaml`. Per generare i sorgenti eseguire da un terminale Linux il seguente comando:
```bash
source generate-sources.sh
```

Per il funzionamento il comando richiede che nel sistema siano installati **Node.js** e **openapi-generator-cli**. Attenersi a quanto indicato in [Generazione del codice sorgente](#generazione-codice-sorgente) per installarli.

<a name="source-code-management"></a>
## 4.2.6 Source code management
Per poter effettuare il versionamento del codice sorgente è richiesto di utilizzare **Git**.
Per poterlo installare è necessario recarsi a [questa pagina](https://git-scm.com/downloads).  
Non è strettamente necessario, ma è consigliato per integrare le proprie modifiche nel repository.

## 4.2.7 Build automation
La build automation (ovvero la gestione del processo di build) è affidata a **Maven**. Maven è installabile scaricandolo dal seguente [link](https://maven.apache.org/download.cgi).  
Tramite Maven il progetto del backend viene compilato, rilasciato sotto forma di pacchetto .jar (formato di Java per i file eseguibili), testato e, volendo, eseguito.

## 4.2.8 Containerization
Il backend utilizza come supporti di persistenza [MySQL](https://www.mysql.com/it/) e [Redis](https://redis.io/). Per evitare di installarli e doverli configurare entrambi, essi vengono resi disponibili già configurati sotto forma di container Docker. L'installazione di Docker è diversa in base al sistema in uso.  

### 4.2.8.1 Installazione di Docker su Windows
È possibile installare Docker su Windows visitando il suo sito ufficiale, alla seguente [pagina](https://hub.docker.com/editions/community/docker-ce-desktop-windows). Docker su Windows richiede la virtualizzazione, come precedentemente anticipato nei [Prerequisiti](#prerequisiti).  
La guida all'installazione e al primo utilizzo è presente nello stesso link in cui si scarica l'eseguibile per l'installazione.

### 4.2.8.2 Installazione di Docker su MacOS
L'installazione per MacOS è identica a quella per Windows, ma la pagina a cui scaricarlo si trova a [questo link](https://hub.docker.com/editions/community/docker-ce-desktop-mac).

### 4.2.8.3 Installazione di Docker su Ubuntu (e derivate, e altri derivati di Debian)
È possibile installare Docker su Ubuntu seguendo le guide presenti sul sito ufficiale, disponibili a [questo indirizzo](https://docs.docker.com/engine/install/ubuntu/).

<a name="generazione-codice-sorgente"></a>
## 4.2.9 Generazione codice sorgente
Per poter generare il codice sorgente citato nella sezione [YAML](#yaml) sono necessari i due strumenti sopra citati: **Node.js** e **openapi-generator-cli**.

### 4.2.9.1 Node.js
L'installazione di Node.js su Windows e MacOS si può fare attraverso degli eseguibili scaricabili presso il sito dello strumento, disponibile [qui](https://nodejs.org/en/download/). È consigliato scaricare la versione LTS, attualmente la 12.

Su sistemi Ubuntu, e al solito anche per distribuzioni derivate e distribuzioni derivate da Debian (con piccole differenze), si può installare con i seguenti comandi invocati da terminale:
```bash
curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -
sudo apt-get install -y nodejs
```

### 4.2.9.2 OpenAPI Generator
Una volta installato Node.js, è possibile installare openapi-generator-cli, da terminale o prompt dei comandi, con il seguente 0comando:
```bash
npm install @openapitools/openapi-generator-cli -g
```

<a name="firebase-authentication"></a>
## 4.2.10 Firebase Authentication
Il backend di Stalker utilizza come provider di autenticazione la piattaforma [Firebase Authentication](https://firebase.google.com/docs/auth) di Google. Per ottenere un'istanza funzionante e personale di un database di autenticazione presso la piattaforma, seguire [questa guida](https://firebase.google.com/docs/projects/learn-more#setting_up_a_firebase_project_and_adding_apps), che spiega come creare un generico progetto su Firebase.

Per utilizzare Firebase Authentication (l'unico strumento che è necessario degli innumerevoli offerti), recarsi su `Impostazioni progetto`, poi su `Account di servizio` e:

- Premere il pulsante `Genera nuova chiave privata`, che permette di scaricare un file con estensione .json;
- Copiare da uno qualsiasi degli `Snippet di configurazione SDK Admin` la stringa corrispondente ad un URL sotto la voce `databaseURL`.

Sia il file che la stringa vanno tenuti da parte, serviranno dopo nella spiegazione in [Variabili d'ambiente e container Docker](#env-var-container).

## 4.2.11 Installazione
Una volta scaricato il codice sorgente, si ottiene una cartella che contiene i seguenti file:
![!Contenuto della cartella Stalker-Backend](../Immagini/Backend/Requisiti/contenuto.jpg)

<a name="contenuto-cartella"></a>

###  4.2.11.1 Contenuto della cartella Stalker-Backend
Come si può vedere dall'immagine, al suo interno sono presenti cinque cartelle (evidenziate in blu) e altri file.  
I file (in ordine di apparizione):

- `checkstyle.xml`: Contiene la configurazione per avvisare, in fase di compilazione, di errori riguardanti l'analisi statica. Questi errori vengono solamente segnalati ma non impediscono la compilazione, seppur sia possibile configurarlo;
- `docker-compose.yml`: Configurazione per Docker per poter lanciare assieme una serie di programmi (tra cui i sopra citati MySQL e Redis) necessari per l'esecuzione del backend, ma anche altri come l'interfaccia per MySQL **phpMyAdmin**, oltre che l'eseguibile stesso del backend;
- `Dockerfile`: File per generare un'immagine di Docker a partire dal pacchetto .jar generato dal processo di compilazione. Non è obbligatorio usarlo, specialmente durante lo sviluppo, ma è consigliato;
- `example.env`: File contenente variabili d'ambiente di esempio. **ATTENZIONE**: questo file deve essere clonato e chiamato `.env` (perché da esso dipende l'esecuzione del backend e il funzionamento di *docker-compose*). Il contenuto del file `.env` deve essere valorizzato con valori reali da utilizzare per eseguire il backend;
- `generate-sources.sh`: Script per la generazione del codice sorgente, come indicato in [YAML](#yaml) e in [Generazione codice sorgente](#generazione-codice-sorgente);
- `ldaptest.sh`: Genera un server [OpenLDAP](https://www.openldap.org/) di test. Un requisito del capitolato d'appalto di *Stalker* consisteva nel permettere l'autenticazione degli utenti tramite LDAP, di conseguenza si è reso necessario avere un server LDAP di test su cui effettuare prove di autenticazione. Per soddisfare i requisiti del capitolato, LDAP viene utilizzato, ma è possibile sostituirlo con un altro sistema di autenticazione come indicato nella sezione Sostituire LDAP nella pagina [Estendibilità](../estendibilita);
- `LICENSE`: Contiene la licenza di utilizzo del prodotto;
- `pom.xml`: Contiene la configurazione del progetto Java, come indicato in [XML](#xml);
- `README.md`: Contiene informazioni utili introduttive all'utilizzo del prodotto;
- `stalker.yaml`: Contiene quando indicato in [YAML](#yaml).

Le cartelle (in ordine di apparizione):

- `containers`: Contiene le cartelle in cui vengono di default salvati i dati provenienti dai container Docker in esecuzione e della configurazione;
- `database-schema`: Contiene lo schema del database MySQL;
- `generated-sources`: Contiene la struttura di cartelle in cui viene generato il codice sorgente come indicato in [YAML](#yaml) e in [Generazione codice sorgente](#generazione-codice-sorgente);
- `load-test`: Contiene un semplice file eseguibile con Python per effettuare test di carico sul backend. Per una breve introduzione su come configurarlo, vedere la sezione [Test di carico](#test-di-carico);
- `openapi-config`: Contiene i file di configurazione per la generazione del codice sorgente;
- `postman-collections`: Contiene dei file che se importati sul software [Postman](https://www.postman.com/) permettono di effettuare i test delle API (particolarmente utili durante lo sviluppo);
- `src`: Contiene il codice sorgente del prodotto, sia quello di produzione (sotto-cartella main), che quello di test (sotto-cartella test).

### 4.2.11.2 Compilazione
Per compilare il codice del prodotto (sia il codice di produzione che di test) è sufficiente invocare il comando su un terminale o prompt dei comandi (e lo stesso per i comandi da qui in avanti):
```bash
mvn compile test-compile
```

### 4.2.11.3 Installazione sul proprio repository locale di Maven
Maven dispone di una cartella, una volta installato, chiamata `.m2`, in cui salva tutti i package e le librerie che vengono usati nei progetti installati e/o eseguiti nel computer in uso. Per installare il progetto sullo stesso repository, usare il seguente comando:
```bash
mvn install
```

<a name="creazione-pacchetto-jar"></a>
### 4.2.11.4 Creazione del pacchetto .jar
Uno dei modi per eseguire il backend è quello di eseguire un file .jar eseguibile. Per generarlo, è necessario invocare il comando:
```bash
mvn package
```

### 4.2.11.5 Pulizia
Per rimuovere l'output della compilazione, contenuto nella cartella target (che viene generata una volta eseguita la compilazione, non viene e non è da mettere sotto controllo di versione), eseguire il seguente comando:
```bash
mvn clean
```

### 4.2.11.6 Altro
In generale, tutti i comandi fino ad ora elencati sono combinabili, quindi può anche essere eseguito un comando come il seguente:
```bash
mvn clean install package
```

## 4.2.12 Esecuzione
Ci sono attualmente due modi per eseguire il backend:

- Tramite comando Maven;
- Tramite pacchetto .jar;
- Tramite Docker (consigliato).

<a name="env-var-container"></a>

### 4.2.12.1 Variabili d'ambiente e container Docker
Se si provasse ad eseguire il backend senza svolgere quanto segue in questa sezione il backend andrebbe in crash ancor prima di partire.

Il framework con cui è realizzato il backend, [Spring](https://spring.io/), fa largo uso di configurazione e in particolare, nel backend di Stalker, è largamente usata. La configurazione di Spring dipende dal valore di alcuni variabili d'ambiente. La configurazione del backend si trova sia sotto forma di classi Java, che di un file chiamato `application.properties`, situato nella cartella scaricata, dentro: `src/main/resources`.
Queste variabili d'ambiente, di cui si trova un esempio nel file `example.env`, vanno impostate nel file `.env` indicato in [Contenuto della cartella Stalker-Backend](#contenuto-cartella), dove viene illustrato il file.  
In particolare, nelle due variabili seguenti viene configurato Firebase:

- **FIREBASE_DATABASE_URL**: Assegnare il valore della stringa precedentemente salvata come indicato nella sezione [Firebase Authentication](#firebase-authentication);
- **GOOGLE_APPLICATION_CREDENTIALS**: Assegnare il path assoluto alla posizione del file con estensione json precedentemente scaricato come indicato nella suddetta sezione.

Altre due variabili importanti sono:

- **LOCAL_URL**: Indirizzo IP o URL con cui si accede al backend durante lo sviluppo locale. Per esempio, la web-app (che è sviluppata in Angular) quando viene eseguita in modalità di sviluppo è disponibile localmente (in localhost) alla porta 4200, con protocollo HTTP. Conseguentemente il valore di LOCAL_URL dovrà essere: `http://localhost:4200`;
- **REMOTE_URL**: Indirizzo IP o URL con cui si accede al backend da remoto, per esempio se il software è in produzione. Sempre riferendosi alla web-app, si dovrà inserire l'URL o IP a cui essa risulta disponibile (ovvero all'indirizzo completo che viene fornito all'amministratore per utilizzare l'interfaccia per amministratori).

Infine, se si decide di utilizzare il protocollo HTTPS (altamente consigliato), è bene assegnare il valore alle seguenti variabili:

- **SSL_ALIAS**: Alias di riferimento nella creazione del certificato;
- **SSL_PSW**: Password del certificato;
- **SSL_KEYSTORE**: Nome del file contenente il certificato (tipicamente l'estensione è di tipo .jks o .p12)

Ovviamente sono valori che dipendono strettamente dal certificato SSL in possesso all'utilizzatore del backend. Per ulteriori informazioni su come non usare HTTPS (sconsigliato ma utile nello sviluppo in locale), riferirsi alla sezione [Rimuovere HTTPS](../estendibilita#rimuovere-https).

Per caricare le variabili d'ambiente nella sessione di terminale corrente invocare il seguente comando (su sistemi Unix-like):
```bash
export $(cat .env | xargs)
```

Su Windows è conveniente utilizzare il WSL per caricare le variabili d'ambiente (e di conseguenza eseguire il backend) oppure usare il programma Git Bash, fornito assieme all'installazione di Git.

Una volta eseguito il precedente comando, eseguire anche il seguente, che si occupa di avviare le istanze di MySQL e Redis (eventualmente anche il backend, se si lascia il file così come scaricato) necessarie per la persistenza dei dati del backend:
```bash
docker-compose up
```

Il comando avvia il backend ma rende il terminale indisponibile (ridirige l'output dei programmi). L'alternativa è avviare i programmi senza che l'output venga mostrato, con quest'altro comando:
```bash
docker-compose up -d
```

Una volta che non è più necessario avere attivi, è possibile spegnerli con il comando:
```bash
docker-compose down
```

<a name="esecuzione-tramite-jar"></a>
### 4.2.12.2 Esecuzione tramite pacchetto .jar
Eseguendo il processo indicato in [Creazione del pacchetto .jar](#creazione-pacchetto-jar), il file generato sarà `stalker-backend-*X.Y.Z*.jar`, in cui *X.Y.Z* corrisponde alla versione del backend una volta scaricato. Il file si trova nella cartella target, e si può eseguire lanciando il comando:
```bash
java -jar target/stalker-backend-X.Y.Z.jar
```

### 4.2.12.3 Esecuzione tramite Maven
Per eseguire il backend tramite Maven è necessario eseguire il seguente comando:
```bash
mvn spring-boot:run
```

### 4.2.12.4 Esecuzione tramite Docker
Eseguendo il processo indicato in [Creazione del pacchetto .jar](#creazione-pacchetto-jar), si ottiene il file eseguibile tramite Java, come in [Esecuzione tramite pacchetto .jar](#esecuzione-tramite-jar). Una volta fatto quanto indicato nelle sezioni appena menzionate, per eseguire il backend tramite Docker (o meglio docker-compose) è necessario eseguire il seguente comando:
```bash
docker-compose up [--build] [-d]
```
L'argomento `-d` è quello indicato fino ad ora per **docker-compose**, mentre `--build` forza Docker a ricostruire il container del backend a partire dal pacchetto .jar attualmente disponibile (altrimenti eseguirebbe l'immagine che trova disponibile sulla macchina, se la ha già disponibile).

<a name="test-di-carico"></a>
### 4.2.13 Test di carico
Una richiesta del capitolato era eseguire test di carico per vedere quanto il sistema fosse in grado di reagire alle richieste. È quindi disponibile, nella cartella `load-test`, un file chiamato `locustfile.py` che esegue attraverso un tool per **Python** una serie di test di carico (lotti di richieste HTTP al backend contemporanee crescenti fino a un limite predefinito e con una rapporto di crescita preimpostata).
Per utilizzarlo è ovviamente necessario connettersi a un'istanza del database funzionante e che accetti le CORS (Cross-Origin Request Sharing) dall'indirizzo da cui provengono le richieste del tool di test. Il tool in questione si chiama [Locust](https://locust.io/), e di default è disponibile all'indirizzo `http://localhost:8089`. Inoltre, va configurato con degli access token validi, ottenuti dal provider di autenticazione (nel caso di *qbteam*, Firebase) e con dati come gli id dell'organizzazione e del luogo validi. Infatti, i dati presenti sul file sono o vuoti o di esempio.

Prima di poter eseguire il file è necessario avere Python installato. Per installarlo è possibile scaricare l'eseguibile di installazione dal [sito ufficiale](https://www.python.org/downloads/).   
Successivamente, eseguire i seguenti comandi:
```bash
pip install locust
pip install pytz
```

Infine, per eseguire il file è sufficiente invocare da terminale:
```bash
locust
```

Se il backend non è disponibile in locale, ovvero nella macchina cui si stanno facendo i test, si può specificare a che indirizzo (`URL`) è disponibile il backend in questo modo:
```bash
locust --host=URL
```

Per ulteriori informazioni sull'uso del tool Locust, recarsi alla [guida ufficiale](https://docs.locust.io/en/stable/).