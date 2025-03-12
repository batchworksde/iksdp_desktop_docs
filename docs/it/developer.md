# Documentazione per sviluppatori di IKSDP Desktop Linux  

## Destinatari del documento  

Questo documento è rivolto a chi desidera personalizzare o ampliare il sistema IKSDP Linux.  

Il progetto è attualmente ospitato su [GitHub](https://github.com/batchworksde/iksdp_desktop). La documentazione è disponibile nello stesso repository.  

## Download e installazione  

Sul sistema di destinazione, il sistema live viene avviato da un SSD. Tuttavia, per i test, il sistema può essere avviato anche da una chiavetta USB su hardware fisico o da un'immagine DVD in una macchina virtuale (VM).  

L'ultima release può essere scaricata da [GitHub Releases](https://github.com/batchworksde/iksdp_desktop/releases). Il link all'ISO più recente si trova sotto "ISO Image".  

Le versioni intermedie sono disponibili tramite il server web [iksdp.pfadfinderzentrum.org/](http://iksdp.pfadfinderzentrum.org).  

## Creazione dell'immagine locale  

Attualmente, ci sono due metodi testati per creare un'immagine localmente. In entrambi i casi, è necessario un sistema operativo basato su Linux.  

- Utilizzare una distribuzione basata su `.deb` (abbiamo testato Debian 12 e Ubuntu 24.04).  
- Creare l'immagine utilizzando un container `docker` o `podman`.  

In entrambi i casi, l'utente che esegue la creazione dell'immagine deve avere permessi `sudo`.  

Per prima cosa, è necessario clonare il repository da GitHub:  

```bash
git clone git@github.com:batchworksde/iksdp_desktop.git
```

Ora bisogna impostare la variabile d'ambiente `ROOTPW`, che definisce la password dell'utente `root` nell'immagine.

### Creazione dell'immagine su un sistema basato su Debian

Eseguire lo script di build `debian-live/build.sh`:

```bash
cd iksdp_desktop
export ROOTPW=MYPASSWORD
./debian-live/build.sh
``` 

### Creazione dell'immagine tramite un container di build

Sul sistema di build deve essere installato `docker` o `podman`.

```bash
cd iksdp_desktop
./debian-live/container-build.sh --build
``` 

Output:
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

A seconda della potenza del sistema di build, la creazione dell'immagine può richiedere tra 10 e XX minuti.

L'immagine finale viene salvata nella sottocartella `build` con il nome `debian-live-bookworm-RELEASEVERSION-TIMESTAMP-ARCH.hybrid.iso`.

### Raccomandazioni

Se si creano più immagini localmente, può essere utile utilizzare un proxy apt locale. Su sistemi basati su Debian, questo può essere installato con:

```bash
apt install apt-cacher-ng -y
```

Il servizio funziona su `tcp/3142`. Quando si utilizza il container di build, questo viene configurato automaticamente durante la creazione del container.
Per `container-build.sh`, questo può essere impostato tramite una variabile d'ambiente:

```bash
export LB
```

## Copia dell'immagine

L'immagine può essere avviata da una chiavetta USB, un DVD o come immagine su disco.


### Modalità di test

Per copiare l'immagine su una chiavetta USB, è possibile utilizzare `dd` su Linux o macOS.

Linux:
```bash
dd if=./debian-live-bookworm-RELEASEVERSION-TIMESTAMP-ARCH.hybrid.iso of=/dev/sdX bs=1M status=progress
```

macOS:
(TODO: trovare il comando appropriato)

In alternativa, su macOS, si può utilizzare [Raspberry Pi Imager](https://www.raspberrypi.com/software/).

Per Windows, strumenti come [rufus](https://rufus.ie) o il [Raspberry Pi Imager](https://www.raspberrypi.com/software/) sono consigliati.

### Raccomandazioni

Per test di piccola scala, una soluzione di virtualizzazione locale come VMware Fusion o Parallels è raccomandata. L'immagine può essere avviata direttamente da un CD-ROM virtuale.

### Produktivbetrieb

Nell'installazione presso l'IKSDP, l'SSD viene utilizzato come dispositivo di avvio. Per garantire che nessun file venga modificato dal sistema operativo locale, viene utilizzato un avvio PXE.
Il sistema viene avviato e, nella schermata di avvio, si preme `F7` per avviare dalla rete. Viene avviato un sistema Linux live minimale. Per copiare i file sull'SSD locale, eseguire i seguenti comandi:

```bash
sudo -s
mount -t cifs //192.168.XXX.XXX /mnt
dd if=/mnt/debian-live-bookworm-RELEASEVERSION-TIMESTAMP-ARCH.hybrid.iso of=/dev/nvme0n1 bs=1M status=progress
sync
reboot
```

## Personalizzazione dell'immagine

TODO