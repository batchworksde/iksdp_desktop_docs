# IKSDP Desktop Linux Projekt-Dokumentation

## Das IKSDP

Das IKSDP (International Kenian Scout Development Program) ist eine Bildungseinrichtung in Nyandiwa/Kenia. An der Einrichtung befindet sich ein Kindergarten, eine Grundschule und eine weiterführende Schule (mixed secondary school). 

Für die weiterführende Schule wurde ein Computerlabor mit 5 Arbeitsplaetzen, Drucker und Internetzugang eingerichtet. Weiterhin koennen die Geräte auch von Personen aus der Umgebung genutzt werden.

## Das Computerlabor

Das Computerlabor steht für Schüler, Lehrer, die Schulleitung, Gäste des IKSDP und die öffentliche Bevölkerung offen. Dafuer wurden zwei Betriebsarten definiert: fuer die Schüler, Lehrer und die Schulleitung ein dauerhafter Modus (persistenter Modus), fuer die anderen Nutzergruppen der "non-persistente Modus". 
Es bietet eine Office-Plattform mit Text-, Tabellenkalkulations- und weiteren Programmen zur Erstellung und Bearbeitung von Dokumenten und verfuegt ueber einen Internetzugang, bspw. fuer Recherchen oder Behoerdenkommunikation. 
Bei der Auswahl der benoetigten Hard- und Software wurde auf Kosten, frei verfuegbare Software (Open Source) und Energieeffizienz geachtet. 
Es wurde eine umfangreiche Dokumentation fuer die unterschiedlichen Benutzergruppen erstellt und im Internet zur Verfuegung gestellt. 
Fuer die Administration der Computer des Computerlabors wurde der stellvertretende Schulleiter gewonnen und detailliert geschult. Die Organisation des Internet-Cafees ist im Aufbau.

### Die Betriebsarten fuer die unterschiedlichen Benutzergruppen
Es wurden zwei Betiebsarten festgelegt:

#### Modus für Schüler, Schulleitung (persistenter Modus)
Hierfür wurde ein USB Stick für den Benutzer oder die Benutzergruppe vorbereitet. Alle Änderungen auf dem Arbeitsplatz werden auf dem USB-Stick gespeichert. Der Benutzer kann Software nachinstallieren und Dokumente erzeugen, welche nach einem Neustart des Computers wieder vorhanden sind.
Die Daten auf dem USB Stick können optional verschlüsselt werden. Der Benutzer kann sich dann ebenfalls ein persönliches Passwort setzen. 

#### Modus für Gäste und die Bevölkerung (nicht-persistenter Modus)
Alle Änderungen werden bei einem (Neu-)Start des Computers verworfen. Somit ist sichergestellt, dass keine Benutzerdaten des Gastes oder des Internetcafe-Benutzers gespeichert werden und abhanden kommen.
Es kann Software durch den Benutzer nachinstalliert werden, diese wird aber nach einem (Neu-)Start genau wie alle Dokumente und Einstellungen wieder verworfen.

## Technik

### Internetzugang

Der Internetzugang wurde über Starlink installiert. Weiterhin wurde ein WLAN Accesspoint angebracht, welcher ebenfalls in der Zukunft die Rolle eines Internetrouters übernehmen könnte. Dieser hat ein LTE Modem integriert und könnte über mobile Provider wie Safaricom (4G+5G sind gut abgedeckt) genutzt werden. Somit ist das Internet theoretisch redundant aufgebaut, sollte Starlink in Zukunft abgeschalten werden.

### Hardware

Es wurde folgende Hardware angeschafft und verbaut:

- 5x BOSGAME Mini PC B100
- 5x Lenovo L22i-40 21.5" FHD Monitor
- 5x Logitech USB Headset H390 
- 5x Logitech C270 HD WEBCAM 
- 1x Epson L6290 EcoTank Printer 
- 1x Starlink Mini
- 1x Mikrotik L009UiGS-2HaxD
- 1x Mikrotik Hex 
- 1x Mikrotik WAP ac LTE kit
- 1x JetKVM
- ca. 50 USB-Sticks (Typ Orico UFSD 64 GB USB 3.0)

Die Netzwerkdokumentation steht dem Poweruser zur Verfügung.

### Software

Auf die PCs wurde ein Live Linux installiert. Dieses stellt sowohl das Betriebssystem, als auch alle Anwendungen bereit. Wir verwenden Linux, da es ein kostenloses und freies Betriebssystem ist. Aus folgenden Gründen wird Linux gerne an Bildungeinrichtungen verwendet:
- Linux als Betriebssystem und dessen Software kann kostenfrei benutzt und angepasst werden
- Linux ist weniger anfällig für Malware und Viren
- Linux ist das führende Betriebssystem für Server und im Embedded Bereich

Es ist eingeschraenkt moeglich eine Windows-Anwendung unter Linux zu installieren. Hierzu gaebe es verschiedene Moeglichkeiten
- 1. die Software per Wine zu emulieren
- 2. ein Windows ale virtuelle Maschine zu emulieren
- 3. einen WinPE USB-Boot-Stick zu verwenden oder
- 4. einen der Bestands-PCs umzukonfigurieren. 


## Open Source Projekt auf Github
 
Das verwendete Betriebssystem Linux liegt als Open Source Projekt auf Github unter der URL: [https://github.com/batchworksde/iksdp_desktop](https://github.com/batchworksde/iksdp_desktop) und kann von allen Projekteilnehmern weiterentwickelt werden. Github ist die aktuell weltweit größte Platform für Open-Source Entwicklung. Der "Harambee" Gedanke entspricht dem Open Source Gedanken, welcher auf Projektarbeit auf Augenhöhe setzt. Jeder kann sich diesem Projekt anschliessen, es kopieren und/oder weiterentwickeln.

Weiterhin soll das Projekt nicht an einzelnen Personen hängen und jederzeit durch Freiwillige oder das IKSDP übernommen oder weitergegeben werden können.

Sollte es neue Anforderungen an die Software geben oder sollten Fehler behoben werden müssen, so können diese als Issue im Github gemeldet werden. 

Weiterhin sollten die PCs mindestens 2x pro Jahr aktualisiert werden.

## Remoteunterstützung

Der lokale Ansprechpartner für die PC Umgebung ist der stellvertretende Schulleiter (Victor). Das Netzwerk ist per zerotier VPN in die Cloud verbunden. Die Supportler können sich falls benötigt über diesen VPN auf die lokalen PCs und das Netzwerkequipment verbinden.

Bei Problemen und Themen kann Victor zwischen mehreren Unterstützungswegen wählen:

#### 1. Öffnen von einem Issue im Github Projekt:
Hierfür ist es notwendig, dass der Internetzugriff funktioniert. Issues können auch von einem Handy oder Tablet aus erstellt werden.
Hier können Fehler, Einstellungsänderungen oder Anforderungen nach weiterer Software eingestellt werden, welche in der Grundinstallation und somit im persistenten und nicht persistenten Modus vorhanden sein soll.
Das Issue wird dann von einem der Projektentwickler ggf. weiter besprochen und implementiert. Wenn eine Änderung im Basissystem implementiert wurde, wird ein neues Basisimage erzeugt. Dieses Basisimage muss dann anschließend auf die PCs kopiert werden. 
Die Dokumentation zum Erstellen von Issues steht dem Poweruser zur Verfügung.
Die Dokumentation über den Updatevorgang steht dem Poweruser zur Verfügung.

#### 2. Live Support per Videokonferenz/Rustdesk:
Hierfür ist es notwendig, dass das IKSDP Linux startet und der Internetzugriff funktioniert.
Sollte es für ein Thema erforderlich sein, so kann die Anwendung **"rustdesk"** gestartet werden. Rustdesk gibt dem Anwender eine ID und ein Passwort. Diese zwei Daten müssen dem Supportler live mitgeteilt werden muss.
Der Supportler startet ebenfalls die Rustdesk Anwendung bei sich und kann nun den entfernten Bildschirm sehen sowie Maus und Tastatur steuern. 

#### 3. Support per JetKVM:
Hierfür ist es notwendig, dass der Internetzugriff funktioniert.
Der JetKVM ist für den Fall gedacht, dass ein PC nicht startet und ein Remotesupport notwendig ist. Das JetKVM Gerät wird per USB und HDMI mit einem der PCs verbunden. Der Supportler kann sich nun über einen definierten Account aus der Ferne mit dem entsprechenden PC verbinden und sogar Einstellungen im BIOS vornehmen.

