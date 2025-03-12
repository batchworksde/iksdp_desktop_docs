
# Documentazione del Progetto IKSDP

## L'IKSDP

L'IKSDP (International Kenyan Scout Development Program) è un'istituzione educativa situata a Nyandiwa, in Kenya. L'istituzione comprende una scuola primaria e, di recente, una scuola secondaria.

Per la scuola secondaria verrà allestito un laboratorio informatico con accesso a Internet. Inoltre, i dispositivi saranno resi disponibili anche alle persone della comunità locale.

Il laboratorio informatico sarà aperto a studenti, insegnanti, direzione scolastica, ospiti dell'IKSDP e al pubblico. È stato installato un accesso a Internet tramite Starlink. Inoltre, è stato installato un access point Wi-Fi. Questo access point potrebbe in futuro svolgere anche il ruolo di router Internet. Dispone di un modem LTE e potrebbe connettersi tramite provider mobili come Safaricom (4G+5G sono ben coperti).

## Hardware

L'hardware acquistato e installato comprende:

- 5x BOSGAME Mini PC B100
- Monitor Lenovo L22i-40 21.5" FHD
- Stampante Epson L6290 EcoTank
- Cuffie USB Logitech H390
- Webcam LOGITECH C270 HD
- Starlink Mini
- Mikrotik L009UiGS-2HaxD
- Mikrotik Hex
- Mikrotik WAP ac LTE kit
- JetKVM

Una documentazione separata sarà creata per la rete.

## Software

Sui PC è stato installato un sistema operativo Linux live. Questo fornisce sia il sistema operativo che tutte le applicazioni necessarie. Utilizziamo Linux perché è un sistema operativo gratuito e open-source. È ampiamente utilizzato nelle istituzioni educative per i seguenti motivi:

- Il software e il sistema operativo possono essere utilizzati e personalizzati gratuitamente.
- Linux è meno vulnerabile a malware e virus.
- Linux è il sistema operativo leader per i server e i sistemi embedded.

L'IKSDP Linux supporta due modalità operative:

1. **Modalità per ospiti e pubblico - modalità non persistente**

   Tutte le modifiche vengono eliminate dopo un riavvio. Questo garantisce che nessun dato utente venga memorizzato o perso.
   In questa modalità, gli utenti possono installare software, ma tutto verrà eliminato, insieme ai documenti e alle impostazioni, al successivo riavvio.

2. **Modalità per studenti e direzione scolastica - modalità persistente**

   Una chiavetta USB viene preparata per l'utente o il gruppo di utenti. Tutte le modifiche al sistema vengono salvate sulla chiavetta USB. Gli utenti possono installare software e creare documenti che rimarranno disponibili anche dopo un riavvio.
   I dati sulla chiavetta USB possono essere criptati opzionalmente. L'utente può anche impostare una password personale.

## Progetto Open Source su Github

Questo sistema Linux è disponibile come progetto open-source su GitHub all'URL: [https://github.com/batchworksde/iksdp_desktop](https://github.com/batchworksde/iksdp_desktop) e può essere sviluppato ulteriormente da tutti i partecipanti al progetto. GitHub è attualmente la più grande piattaforma mondiale per lo sviluppo open-source. Il principio "Harambee" è in linea con la filosofia open-source, che si basa sulla collaborazione alla pari. Chiunque può unirsi, copiare e/o sviluppare ulteriormente questo progetto.

Inoltre, il progetto non dovrebbe dipendere da persone specifiche e dovrebbe sempre poter essere gestito o continuato da volontari o dall'IKSDP.

Se emergono nuove esigenze software o devono essere risolti errori, questi possono essere segnalati come issue.

I PC dovrebbero inoltre essere aggiornati almeno due volte all'anno.

## Supporto Remoto

Il referente locale per l'ambiente PC è Victor. La rete è connessa al cloud tramite una VPN ZeroTier. Se necessario, il personale di supporto può connettersi ai PC locali e alle apparecchiature di rete tramite questa VPN.

In caso di problemi, Victor può scegliere tra diversi metodi di supporto:

1. **Apertura di un issue nel progetto GitHub:** Qui possono essere segnalati errori, modifiche alle impostazioni o richieste di software aggiuntivo da includere nell'installazione di base per entrambe le modalità (persistente e non persistente).
   L'issue verrà discusso e implementato da uno sviluppatore del progetto. Una volta apportata una modifica al sistema base, verrà creato un nuovo file immagine di base, che dovrà essere copiato sui PC. Verrà creata una documentazione separata per la procedura di aggiornamento.

2. **Supporto live tramite videochiamata/RustDesk:**

   Se necessario, è possibile avviare l'applicazione RustDesk. Questa genererà una password da comunicare al personale di supporto in tempo reale.
   Il supporto avvierà a sua volta l'applicazione RustDesk e potrà controllare lo schermo, il mouse e la tastiera.
   Affinché questo funzioni, IKSDP Linux deve essere in esecuzione e avere accesso a Internet.

3. **Supporto tramite JetKVM:**

   JetKVM è pensato per i casi in cui un PC non si avvia e il supporto remoto è necessario. Il dispositivo JetKVM viene collegato a un PC tramite USB e HDMI. Il personale di supporto potrà quindi accedere al sistema utilizzando un account predefinito.
