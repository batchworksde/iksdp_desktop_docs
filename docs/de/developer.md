# IKSDP Desktop Linux Entwickler-Dokumentation

## Zielgruppe des Dokumentes

Dieses Dokument wendet sich an Personen, welche das IKSDP Linux anpassen oder erweitern wollen.

Das Projekt wird aktuell auf [Github](https://github.com/batchworksde/iksdp_desktop) gehostet. Die Dokumentation wird hier gehostet.

## Download und Installation

Auf dem Zielsystem wird das Livesystem von SSD gebootet. Zum testen kann das System allerdings auch von einem USB-Stick an Hardware oder von einem DVD Image in einer VM gestartet werden.

Das aktuelle release kann über [Github Releases](https://github.com/batchworksde/iksdp_desktop/releases) runtergeladen werden. Dort ist unter "ISO Image" ein link zum aktuellen ISO hinterlegt.

Zwischenreleases werden über den Webserver [iksdp.pfadfinderzentrum.org/](http://iksdp.pfadfinderzentrum.org) bereitgestellt.

## Image lokal erstellen

Um das Image lokal zu erstellen gibt es aktuell 2 getestet Varianten. In beiden Fällen wird ein Linux basiertes System benötigt.

- man verwendet eine .deb basierte Distribution (wir haben Debian 12 und Ubuntu 24.04 getestet) 
- man erstellt das Image über einen `docker` oder `podman` Container

In beiden Fällen muss der Nutzer unter dem das Image gebaut wird über `sudo` Berechtigungen verfügen.

Zuerst muss das Image von github gecloned werden:

`git clone git@github.com:batchworksde/iksdp_desktop.git`

Nun wird eine Umgebunsvariable `ROOTPW` gesetzt, welches als Passwort des Nutzers `root` im Image gesetzt wird. 

### Image auf Debian basierendem System erzeugen

Es wird das buildscript `debian-live/build.sh` gestartet.

```bash
cd iksdp_desktop
export ROOTPW=MYPASSWORD
./debian-live/build.sh
``` 

### Image per Build Container erzeugen

Auf der Buildinstanz muss `docker` oder `podman` installiert sein. 

```bash
cd iksdp_desktop
./debian-live/container-build.sh --build
``` 

Ausgabe:
```bash
Use apt caching proxy (highly recommended)? [Y|n]: 

Apt caching proxy URL [http://localhost:3142]: 
Successfully built 9f7804923f2d
Successfully tagged iksdp_desktop-builder:latest
```

```bash
export ROOTPW=MYPASSWORD
./debian-live/container-build.sh --run
``` 

Je nach Geschwindigkeit der Buildinstanz wird das Erstellen des Image zwischen 10-XX Minuten dauern.

Das fertige image wird im Unterordner `build` mit dem Namen `debian-live-bookworm-RELEASEVERSION-TIMESTAMP-ARCH.hybrid.iso` abgelegt.

### Empfehlungen

Beim mehrfachen Erzeugen des lokalen Images kann es hilfreich sein einen lokalen apt-proxy zu verwenden. Auf debian basierenden systemen kann man dies per 

```bash
apt install apt-cacher-ng -y
```

nachinstalliert werden. Der Dienst läuft auf `tcp/3142`. Beim build container wird dieser beim Erstellen des builder containers konfiguriert. 
Beim Erstellen über `container-build.sh` kann dies per Umgebungsvariable gesetzt werden.

```bash
export LB
```

## das Image kopieren

Das Image kann sowohl von USB-Stick, DVD oder als Festplattenimage gebootet werden. 


### Testbetrieb

Um das Image auf einen USB Stick zu kopieren kann man unter Linux oder MacOS beispielsweise `dd` verwenden.

Linux:
```bash
dd if=./debian-live-bookworm-RELEASEVERSION-TIMESTAMP-ARCH.hybrid.iso of=/dev/sdX bs=1M status=progress
```

MacOS:
TODO raussuchen.. 

Alternativ kann für MacOS auch die Anwendung [Raspberry Pi Imager](https://www.raspberrypi.com/software/) verwendet werden.

Für Windows bietet sich beispielsweise die Anwendung [rufus](https://rufus.ie) oder ebenfalls der [Raspberry Pi Imager](https://www.raspberrypi.com/software/) an.

### Empfehlungen

Für kleinere Tests bietet sich eine lokale Virtualisierungslösung wie VMware Fusion oder Parallels an. Dort kann das Image einfach von einem virtuellem CDROM gebootet werden.

### Produktivbetrieb

In der konreten Installation beim IKSDP wird als bootmedium die SSD verwendet. Um sicherzustellen, dass keinerlei Dateien durch das lokale OS im Zugriff sind verwenden wir einen PXE Boot. 
Das System wird gebootet und im Startscreen `F7` vom Netzwerk gebootet. Es wird ein minimales Live Helperlinux gestartet. Um die Dateien auf den lokalen SSD zu kopieren wird folgendes durchgeführt:

```bash
sudo -s
mount -t cifs //192.168.XXX.XXX /mnt
dd if=/mnt/debian-live-bookworm-RELEASEVERSION-TIMESTAMP-ARCH.hybrid.iso of=/dev/nvme0n1 bs=1M status=progress
sync
reboot
```

## Image anpassen

TODO