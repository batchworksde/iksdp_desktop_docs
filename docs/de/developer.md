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

### Installation auf eigener UEFI Partition

Ziel ist es das System auf einer lokalen Disk zu installieren und den restlichen Speicherplatz der Disk zu nutzen (z.B. für persistente Daten statt eines USB-Sticks). Würde man die Variante aus [Produktivbetrieb](#produktivbetrieb) verwenden, würde die Partitionstabelle der Disk jedes Mal wieder komplett übeschrieben werden und die Daten verloren gehen. Mit dieser Variante werden die Daten manuell kopiert. Dafür muss das Image mit den Optionen `DEBIAN_BINARY_IMAGE="tar"` und `DEBIAN_BOOTLOADERS="grub-efi"` in der Datei `build.env` erstellt werden. Das Ergebnis ist eine tar-Datei statt einer iso-Datei.

Im folgenden muss die Partionierung der lokalen Disk vorbereitet werden. Auf der Disk wird eine 512 MB große FAT32 Partition erstellt. Diese ist zum UEFI booten notwendig. Eine zweite 10 GB große ext4 Partition enthält die Dateien des IKSDP Desktops. Eine dritte Partition nutzt den restlichen Speicherplatz der Disk und kann dann für die (optional auch verschlüsselten) persistenten Daten verwendet werden. Für die einmalige Partition kann eine Live-CD wie z.B. [rescuezilla](https://rescuezilla.com/) benutzt werden:

```
parted /dev/nvme0n1
mklabel gpt
mkpart primary fat32 1MiB 513MiB 
set 1 esp on
mkpart ext4 513MiB 10000MiB
mkpart ext4 10000MiB 100%
quit
mkfs.fat -F32 /dev/nvme0n1p1
mkfs.ext4 /dev/nvme0n1p2
```

Nun muss der Ordner EFI aus der tar-Datei auf die erste Partition (`/dev/nvme0n1p1`) kopiert werden. Alle anderen Ordner aus der tar-Datei werden auf die 2. Partition kopiert (`/dev/nvme0n1p2`):

```
mkdir -p /media/p1 /media/p2
mount /dev/nvme0n1p1 /media/p1
mount /dev/nvme0n1p2 /media/p2
tar -xvf debian-live-bookworm-0.8.0-20250516183746-amd64.tar.tar --directory /media/p1 --strip-components 1 binary/EFI
tar --exclude='binary/EFI' -xvf debian-live-bookworm-0.8.0-20250516183746-amd64.tar.tar --directory /media/p2 --strip-components 1
```

Zusätzlich muss noch einmalig eine Datei angelegt werden, die dem Bootloader mitteilt welche Block Device UUID die zweite Partition hat und zum Booten genutzt werden soll:

```
UUID=$(blkid /dev/nvme0n1p2 -s UUID -o value)
cat <<EOT > /media/p1/EFI/boot/grub.cfg
search.fs_uuid $UUID root
set prefix=(\$root)'/boot/grub'
configfile \$prefix/grub.cfg
EOT
```

Die dritte Partition kann noch für die persistenten Daten vorbereitet werden (im Beispiel inkl. Verschlüsselung):

```
/usr/sbin/cryptsetup luksFormat /dev/nvme0n1p3
/usr/sbin/cryptsetup luksOpen /dev/nvme0n1p3 persistence
/usr/sbin/mkfs.ext4 /dev/mapper/persistence
/usr/sbin/e2label /dev/mapper/persistence "persistence"
mkdir -p /media/p3
mount /dev/mapper/persistence /media/p3
echo "/home union" > /media/p3/persistence.conf
echo "/etc/iksdp_persistent union" >> /media/p3/persistence.conf
umount /media/p3
/usr/sbin/cryptsetup luksClose persistence
```

Nach einem Reboot sollte der IKSDP Deskto von der lokalen Disk booten.

#### Update der lokalen Disk

Der Ablauf ist ähnlich wie bei [Update Möglichkeit 3](../en/poweruser.md#update-possibility-3-use-image-updater) beschrieben. Beim Booten wird die Option "Live System (amd64 update)" ausgewählt. Danach werden die Dateien auf der lokalen Disk ausgetauscht:

```
mkdir -p /media/p1 /media/p2
mount /dev/nvme0n1p1 /media/p1
mount /dev/nvme0n1p2 /media/p2
tar -xvf debian-live-bookworm-0.8.0-20250516183746-amd64.tar.tar --directory /media/p1 --strip-components 1 binary/EFI
tar --exclude='binary/EFI' -xvf debian-live-bookworm-0.8.0-20250516183746-amd64.tar.tar --directory /media/p2 --strip-components 1
```

Falls der Client nicht genug RAM hat um mit `toram` (Option "Live System (amd64 update)") zu booten, kann alternativ auch z.B. wieder [rescuezilla](https://rescuezilla.com/) gebootet werden und die Befehle dort ausgeführt werden.

## Image anpassen

TODO