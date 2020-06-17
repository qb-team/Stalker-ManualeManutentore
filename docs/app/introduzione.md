# 2.1 Introduzione
Questa parte del prodotto è orientata all'uso da parte degli utenti che voglio essere tracciati dalle organizzazioni utilizzando l'applicazione Android.

## 2.1.1 Scopo del prodotto
L'applicazione Android offre all'utente le seguenti funzionalità:

- **Registrazione**: L'utente ha la possibilità di registrarsi inserendo un e-mail, password e accettando le condizioni d'uso;

- **Login**: L'utente ha la possibilità di autenticarsi inserendo la propria email e password;

- **Scaricamento della lista delle organizzazioni**: L'utente, per poter visualizzare la lista di tutte le organizzazioni disponibili in Stalker, deve prima scaricarla connettendosi al backend. Una volta richiesto lo scaricamento, se dovesse decidere di annullarlo o se venisse a mancare la connessione ad Internet, apparirebbe nella schermata principale un tasto per ritentare il download;

- **Aggiornamento della lista delle organizzazioni**: L'utente può aggiornare la lista delle organizzazioni eseguendo uno *swipe down* nella schermata principale;

- **Drawer**: L'utente può accedere ad una serie di funzionalità e informazioni utilizzando l'*Hamburger button* riportato in alto a sinistra.
In cima al menù è scritta l'email dell'account dell'utente mentre nella sezione "Info Tracciamento" verrà indicata la presenza dell'utente all'interno di un organizzazione o di un luogo, seguita dal tempo di permanenza all'interno di quella organizzazione.
Nella sezione "Impostazioni tracciamento" del menù è possibile avviare il tracciamento tramite uno pulsante switch, disattivato di default, oppure sempre tramite uno switch è possibile passare da tracciamento autenticato a tracciamento anonimo. Alla prima attivazione del tracciamento compare sulla schermata dell'applicazione un pop-up che invita l'utente ad accettare i permessi necessari per permettere all'applicazione di utilizzare il GPS. Altre funzionalità in questo menu permettono di effettuare il logout e l'ordinamento alfabetico della lista delle organizzazioni;

- **Ricerca**: In alto a destra sulla barra principale dell'applicazione vi è una lente di ingrandimento che funge da ricerca ed una volta selezionata mostrerà una barra dove è possibile scrivere del testo. Quindi è possibile eseguire delle ricerche testuali per filtrare e visualizzare la lista delle organizzazioni. 
Di default la ricerca è impostata per eseguire delle ricerche sui nomi delle organizzazioni, ma si può anche cambiare tale funzione servendosi del menù di filtraggio in alto a destra nello schermo. I filtri di ricerca funzionano tramite mutua esclusione ed è possibile scegliere questi campi: nome, città, nazione (selezionabile tramite pop-up scrollabile), organizzazioni anonime (stampa il risultato dopo la selezione) e organizzazioni autenticate (stampa il risultato dopo la selezione);

- **Visualizzazione pagina organizzazione**: L'utente può entrare nella pagina dedicata di un'organizzazione in due diversi modi: 
    - Cliccando l'elemento della lista ad essa appartenente; 
    - Tenendo premuto su un elemento della lista apparirà un pop-up che permetterà di cliccare sul pulsante 'Maggiori informazioni' e accedere così alla visualizzazione dell'organizzazione selezionata. 
    
    Al suo interno è possibile visualizzare il nome dell'organizzazione, una descrizione, l'immagine di anteprima e un pulsante che se premuto mostrerà l'ultimo accesso effettuato dall'utente all'interno dell'organizzazione. 
    Un'organizzazione che richiede un'autenticazione aziendale avrà in aggiunta il pulsante Autenticazione' che, se cliccato, visualizzerà un pop-up per poter inserire le credenziali LDAP;
 
- **Aggiunta organizzazione nella lista MyStalker (lista preferiti)**: L'utente, tenendo premuto su un elemento della lista delle organizzazioni fa apparire un pop-up che permette di aggiungere l'organizzazione selezionata nella lista MyStalker, o più semplicemente visualizzarne il contenuto. Se l'organizzazione richiede un'autenticazione aziendale (tramite LDAP) allora con il pop-up è possibile solamente visualizzarne il contenuto. Una volta avuto accesso alla pagina dedicata dell'organizzazione bisogna autenticarsi tramite credenziali LDAP. Se l'autenticazione avviene con successo, tale organizzazione compare nella lista MyStalker;

- **Eliminazione organizzazione dalla lista MyStalker**: L'utente, tenendo premuto sull'elemento della lista delle organizzazioni MyStalker, fa comparire un pop-up che richiede se si intende rimuovere l'organizzazione da tale lista;

- **Tracciamento**: La funzionalità di tracciamento consente all'utente di tracciare, in maniera autenticata o anonima, gli ingressi e le uscite presso le organizzazioni presenti nella lista MyStalker e i loro luoghi. 
Più distante si trova l'utente dall'organizzazione più vicina meno frequenti saranno gli intervalli di tempo in cui verrà tracciato. In questo modo ci sarà un consumo minore della batteria.

- **Storico Accessi**: Nell'applicazione, oltre ad esserci una sezione principale dedicata alla lista di tutte le organizzazioni e una per le organizzazioni presenti nella lista MyStalker (lista preferiti), è presente una terza sezione (indicata nel tab con un'icona a forma di orologio) che mostra un elenco di tutti gli accessi presso le organizzazioni da parte dell'utente.
Se l'utente entra in un'organizzazione e poi esce, verrà aggiunto un elemento nella lista (riga) nella quale vengono mostrate le seguenti informazioni:
    - Nome dell'organizzazione;
    - Data di accesso;
    - Ora di accesso;
    - Ora di uscita.

    È presente anche un pulsante, contrassegnato dal simbolo di un cestino, che permette di eliminare tutte le informazioni sullo storico degli accessi (quindi verranno eliminate tutte le righe presenti in questa sezione).
    Gli elementi della lista dello storico accessi possono essere cliccati una volta oppure tenuti premuti a lungo:
            
    - Nella prima funzionalità l'utente verrà conseguentemente proiettato in una pagina dedicata che mostra lo storico degli accessi presso ai luoghi dell'organizzazione. Anche in questo caso ci sarà il pulsante a forma di cestino che permette l'eliminazione del contenuto;
    - Nella seconda funzione apparirà un pop-up che mostra informazioni aggiuntive come il tempo di permanenza presso l'organizzazione e la modalità di tracciamento utilizzata in quel determinato accesso.
