# Documentazione del progetto IKSDP Desktop Linux  

## L'IKSDP  

L'IKSDP (International Kenyan Scout Development Program) è un'istituzione educativa situata a Nyandiwa, in Kenya. La struttura comprende un asilo, una scuola primaria e, più recentemente, una scuola secondaria.  

Per la scuola secondaria verrà allestito un laboratorio informatico con accesso a Internet. Inoltre, i dispositivi saranno disponibili anche per l'uso da parte delle persone della comunità locale.  

## Il laboratorio informatico  

Il laboratorio informatico sarà accessibile agli studenti, agli insegnanti, all'amministrazione scolastica, agli ospiti dell'IKSDP e al pubblico generale. È stata installata una connessione Internet tramite Starlink. Inoltre, è stato configurato un punto di accesso Wi-Fi che potrebbe fungere da router Internet in futuro. Questo punto di accesso include un modem LTE integrato, che potrebbe essere utilizzato tramite provider mobili come Safaricom (la copertura 4G+5G è eccellente). Questa configurazione garantisce una ridondanza nell'accesso a Internet, nel caso in cui Starlink venga disattivato in futuro.  

### Hardware  

L'hardware acquistato e installato è il seguente:  

- 5x BOSGAME Mini PC B100  
- 5x Monitor Lenovo L22i-40 21.5" FHD  
- 5x Cuffie USB Logitech H390  
- 5x Webcam Logitech C270 HD  
- 1x Stampante Epson L6290 EcoTank  
- 1x Starlink Mini  
- 1x Mikrotik L009UiGS-2HaxD  
- 1x Mikrotik Hex  
- 1x Mikrotik WAP ac LTE kit  
- 1x JetKVM  

La documentazione di rete è disponibile per l'utente avanzato.  

### Software  

Sui PC è stato installato un sistema Linux live. Questo fornisce sia il sistema operativo che tutte le applicazioni necessarie. Abbiamo scelto Linux perché è un sistema operativo gratuito e open source. Linux è ampiamente utilizzato nelle istituzioni educative per i seguenti motivi:  

- Linux e il suo software possono essere utilizzati e modificati gratuitamente.  
- Linux è meno vulnerabile a malware e virus.  
- Linux è il sistema operativo leader per i server e i sistemi embedded.  

IKSDP Linux supporta due modalità operative:  

#### Modalità ospiti e pubblica: modalità non persistente  

Tutte le modifiche vengono eliminate dopo un riavvio. Questo garantisce che i dati degli utenti ospiti o degli utenti del caffè Internet non vengano salvati o persi.  
Gli utenti possono installare software, ma tutte le applicazioni, i documenti e le impostazioni verranno resettati al riavvio.  

#### Modalità studenti e amministrazione: modalità persistente  

Per questa modalità, viene preparata una chiavetta USB per l'utente o il gruppo di utenti. Tutte le modifiche al sistema vengono salvate sulla chiavetta USB. Gli utenti possono installare software e creare documenti che rimarranno disponibili dopo un riavvio.  
I dati sulla chiavetta USB possono essere crittografati opzionalmente. Gli utenti possono anche impostare una password personale.  

## Progetto Open Source su GitHub  

Il sistema operativo Linux utilizzato è disponibile come progetto open-source su GitHub all'indirizzo [https://github.com/batchworksde/iksdp_desktop](https://github.com/batchworksde/iksdp_desktop) e può essere ulteriormente sviluppato da tutti i partecipanti al progetto. GitHub è attualmente la più grande piattaforma mondiale per lo sviluppo open-source. Il concetto di "Harambee" si allinea perfettamente con l'idea dell'open-source, che promuove la collaborazione alla pari. Chiunque può unirsi al progetto, copiarlo e svilupparlo ulteriormente.  

Inoltre, il progetto non dovrebbe dipendere da singoli individui e dovrebbe sempre essere trasferibile a volontari o all'IKSDP.  

Se emergono nuove esigenze software o problemi da risolvere, possono essere segnalati come issue su GitHub.  

Inoltre, i PC dovrebbero essere aggiornati almeno due volte all'anno.  

## Supporto remoto  

Il referente locale per l'ambiente PC è Victor. La rete è connessa al cloud tramite una VPN ZeroTier. Se necessario, il personale di supporto può connettersi in remoto ai PC locali e alle apparecchiature di rete tramite questa VPN.  

Per il supporto tecnico, Victor ha diverse opzioni:  

#### 1. Creazione di un issue nel progetto GitHub  

Per questa operazione è necessaria una connessione Internet funzionante. Le issue possono essere create anche da un telefono cellulare o un tablet.  
Gli issue possono includere segnalazioni di bug, richieste di modifiche alla configurazione o richieste di software aggiuntivo da includere nell'installazione di base (sia in modalità persistente che non persistente).  
Uno sviluppatore del progetto esaminerà e, se necessario, implementerà le modifiche richieste. Se una modifica viene applicata al sistema base, verrà creato un nuovo file immagine di base. Questo file dovrà poi essere copiato sui PC.  

La documentazione su come creare issue su GitHub è disponibile per l'utente avanzato.  
La documentazione sul processo di aggiornamento è disponibile per l'utente avanzato.  

#### 2. Supporto live tramite videoconferenza/RustDesk  

Per questa operazione, IKSDP Linux deve essere avviato e deve essere disponibile una connessione Internet.  
Se necessario, può essere avviata l'applicazione **"RustDesk"**. RustDesk fornisce all'utente un ID e una password, che devono essere comunicati in tempo reale al personale di supporto.  
Il personale di supporto avvia anche l'applicazione RustDesk e può quindi vedere lo schermo remoto e controllare il mouse e la tastiera.  

#### 3. Supporto tramite JetKVM  

Per questa operazione è necessaria una connessione Internet.  
JetKVM è pensato per i casi in cui un PC non si avvia ed è necessario un supporto remoto. Il dispositivo JetKVM viene collegato al PC tramite USB e HDMI. Il personale di supporto può quindi accedere al PC da remoto utilizzando un account designato e persino apportare modifiche al BIOS.  
