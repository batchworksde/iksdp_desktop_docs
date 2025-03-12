# IKSDP Projekt Dokumenation

## das IKSDP

Das IKSDP (International Kenian Scout Development Program) ist eine Bildungseinrichtung in Nyandiwa/Kenia. An der Einrichtung befindet sich eine Grundschule, Primary School und neu eine Secondary School. 

Für die Secondary School soll ein Computerlabor mit Internetzugang eingerichtet werden. Weiterhin sollen die Geräte auch Menschen aus der Umgebung bereitgestellt werden.

Es soll ein Computerlabor eingerichtet werden, welches Schüler, Lehrern, der Schulleitung, Gästen des IKSDP und der öffentlichen Bevölkerung  offenstehen. Es wurde ein Internetzugang über Starlink installiert. Weiterhin wurde ein WLAN Accesspoint installiert. Dieser Accesspoint könnte ebenfalls in der Zukunft die Rolle eines Internetrouters übernehmen. Er hat ein LTE Modem installiert und könnte über mobile Provider wie Safaricom (4G+5G sind gut abgedeckt).

## Hardware

Es wurde folgende Hardware angeschafft und verbaut:

- 5x BOSGAME Mini PC B100
- Lenovo L22i-40 21.5" FHD Monitor
- Epson L6290 EcoTank Printer 
- Logitech USB Headset H390 
- LOGITECH C270 HD WEBCAM 
- Starlink Mini
- Mikrotik L009UiGS-2HaxD
- Mikrotik Hex 
- Mikrotik WAP ac LTE kit
- JetKVM

Eine Dokumentation für das Netzwerk wird seperat erstellt.

## Software

Auf die PCs wurde ein Live Linux installiert. Die stellt sowohl das Betriebssystem, als aucha alle Anwendungen bereit. Wir verwenden Linux, da es ein ein kostenloses und freies Betriebssystem ist. Aus folgenden Gründen wird Linux gerne an Bildungeinrichtungen verwendet.
- die Software und das Betriebssystem kann kostenfrei benutzt und angepasst werden
- Linux ist weniger anfällig für Malware und Viren
- Linux ist das führende Betriebssystem bei Server und und im embedded Bereich

Das IKSDP Linux unterstützt 2 Betiebsmodi:
1. Modus für Gäste und die Bevölkerung - non-persistent Modus

Alle Änderungen werden nach einem Neustart verworfen. Somit ist sichergestellt, dass keine Benutzerdaten des Gastes oder Internetcafe benutzers gespeichert werden und abhanden kommen.
In diesem Modus kann Software durch den Benutzer nachinstalliert werden. Diese wird aber nach einem Neustart genau wie alle Dokumente und Einstellungen wieder verworfen.

2. Modus für Schüler, Schulleitung - persistent Mode

Hierfür wird ein USB Stick für den Benutzer oder die Benutzergruppe vorbereitet. Alle Änderungen an dem System werden auf dem USB-Stick gespeichert. Der Nutzer kann Software nachinstallieren und Dokumente erzeugen, welche nach nach einem Neustart wieder vorhanden sind.
Die Daten auf dem USB Stick können optional verschlüsselt werden. Der Benutzer kann sich ebenfalls ein persönliches Passwort setzen.

## Open Source Projekt auf Github
 
Dieses Linux liegt als Open Source Projekt auf Github unter der URL: [https://github.com/batchworksde/iksdp_desktop](https://github.com/batchworksde/iksdp_desktop) und kann von allen Projekteilnehmern weiterentwickelt werden. Github ist die aktuell weltweit größte Platform für Open-Source Entwicklung. Der "Harambee" Gedanke entspricht dem Open Source Gedanken, welcher auf Projektarbeit auf Augenhöhe setzt. Jeder kann sich diese Projekt anschliessen es kopieren und/oder weiterentwickeln.

Weiterhin soll das Projekt nicht an einzelnen Personen hängen und jederzeit durch Freiwillige oder das IKSDP übernommen oder weitergegeben werden können.

Sollte es neue Anforderungen an Software oder Fehler behoben werden müssen, so können die als Issue gemeldet werden. 

Weiterhin sollte die PCs mindestens 2x pro Jahr aktualisiert werden.

## Remoteunterstützung

Der lokale Ansprechpartner für die PC Umgebung ist Victor. Das Netzwerk ist per zerotier VPN in die Cloud verbunden. Die Supportler können sich falls notwendig über dieses VPN auf die lokalen PCs und Netzwerkequitment verbinden.

Bei Problemen und Themen kann Victor mehrere Unterstützungwege wählen:

1. Öffnen von einem Issue im Github Projekt: Hier können Fehler, Einstellungsänderungen oder Anforderungen nach weiterer Software eingestellt werden, welche in der Grundinstallation und somit im persistent und non-persistent mode vorhanden sein muss.
Das Issue wird dann von einem der Projektentwickler ggf. weiter besprochen und implementiert. Wenn eine Änderung im Basissystem implementiert wurde, wird ein neues Basisimage erzeugt. Dieses Basisimage muss auf die PCs kopiert werden. Eine Dokumentation über den Updatevorgang wird seperat erstellt

2. live support per videokonferenz/rustdesk:

Sollte es für ein Thema erforderlich sein, so kann die Anwendung rustdesk gestartet werden. Diese gibt dem Anwender ein Passwort aus, welches dem Supportler live mitgeteilt werden muss.
Der Supportler startet ebenfalls die Rustdesk Anwednung bei sich und kann nun screen, maus und tastatureingaben übernehmen. 
Hierfür ist es notwendig, dass das IKSDP Linux startet und und einen Interetzugriff hat.

3. Support per JetKVM

Der JetKVM ist für den Fall gedacht, dass ein PC nicht startet und ein Remotesupport notwendig ist. Das JetKVM Gerät wird per USB und HDMI mit einem der PCs verbunden. Der Supportler kann sich nun über eine definierten Account  