# IKSDP Desktop Linux Developer Documentation  

## Target Audience  

This document is intended for individuals who want to customize or extend the IKSDP Linux system.

The project is currently hosted on [GitHub](https://github.com/batchworksde/iksdp_desktop). The documentation is also hosted there.

## Download and Installation  

On the target system, the live system is booted from the SSD. However, for testing, the system can also be started from a USB stick on hardware or from a DVD image in a virtual machine (VM).

The latest release can be downloaded from [GitHub Releases](https://github.com/batchworksde/iksdp_desktop/releases). A link to the latest ISO can be found under "ISO Image".

Intermediate releases are provided via the web server [iksdp.pfadfinderzentrum.org/](http://iksdp.pfadfinderzentrum.org).  

## Creating the Image Locally

There are currently two tested methods for creating the image locally. In both cases, a Linux-based system is required.

- A `.deb`-based distribution is used (we have tested Debian 12 and Ubuntu 24.04).  
- The image is created using a `docker` or `podman` container.

In both cases, the user building the image must have `sudo` privileges.  

First, the image must be cloned from GitHub:

```bash
git clone git@github.com:batchworksde/iksdp_desktop.git
```

Next, an environment variable `ROOTPW` is set, which defines the password for the `root` user in the image.

Creating the Image on a Debian-Based System
Run the build script `debian-live/build.sh`.

```bash
cd iksdp_desktop
export ROOTPW=MYPASSWORD
./debian-live/build.sh
``` 

### Creating the Image using a Build Container

On the build system `docker` or `podman` must be installed.

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

Depending on the performance of the build system, creating the image can take between 10 and XX minutes.

The finished image is stored in the `build` subfolder with the name `debian-live-bookworm-RELEASEVERSION-TIMESTAMP-ARCH.hybrid.iso`.

### Recommendations
When creating the image multiple times locally, using a local apt-proxy can be helpful. On Debian-based systems, this can be installed with:

```bash
apt install apt-cacher-ng -y
```

The service runs on `tcp/3142`. When using the build container, this is configured when creating the builder container. For `container-build.sh`, this can be set via an environment variable:

```bash
export LB
```

## Copying the Image
The image can be booted from a USB stick, DVD, or as a disk image.

## Testing
To copy the image to a USB stick, `dd` can be used on Linux or macOS.

Linux:
```bash
dd if=./debian-live-bookworm-RELEASEVERSION-TIMESTAMP-ARCH.hybrid.iso of=/dev/sdX bs=1M status=progress
```

### MacOS:
(TODO: Find appropriate command)

Alternatively, on macOS, the [Raspberry Pi Imager](https://www.raspberrypi.com/software/) can be used.

For Windows, tools like [Rufus](https://rufus.ie)  or the [Raspberry Pi Imager](https://www.raspberrypi.com/software/) are recommended.

### Recommendations

For small-scale testing, a local virtualization solution such as VMware Fusion or Parallels is recommended. The image can simply be booted from a virtual CD-ROM.

### Production Deployment

For the IKSDP installation, the SSD is used as the boot medium. To ensure that no files are accessed by the local OS, a PXE boot is used.
The system is booted, and on the startup screen, F7 is pressed to boot from the network. A minimal Live Helper Linux is started. To copy the files to the local SSD, execute the following:

```bash
sudo -s
mount -t cifs //192.168.XXX.XXX /mnt
dd if=/mnt/debian-live-bookworm-RELEASEVERSION-TIMESTAMP-ARCH.hybrid.iso of=/dev/nvme0n1 bs=1M status=progress
sync
reboot
```

### Installation on an UEFI partition

The goal is to install the ISDP dektop to a local disk and use the rest of the disk (e.g. for persistent data instead of an USB stick). If you would use the option described in [Production Deployment](#production-deployment) you would always overwrite the disk partition table and loose your data. With the option desctibed here you have to copy the IKDSP dektop files manually. To be able to do this you have to build the Image with the options `DEBIAN_BINARY_IMAGE="tar"` and `DEBIAN_BOOTLOADERS="grub-efi"` in the file `build.env`. As a result you will get a tar-file instead of an iso-file. 

First you have to prepare the partitions of the local disk. We will create one FAT32 partition with the size of 512 MB. This is necessary for UEFI booting. Another ext4 partition with the size of 10 GB will contain the files of the IKSDP desktop. The third (optional encrypted) ext4 partition will use the rest of the disk space and can be used for persitent data. For the creation of the partition table a live CD like [rescuezilla](https://rescuezilla.com/) can be used:

```
parted /dev/nvme0n1
mkpart primary fat32 1MiB 513MiB 
set 1 esp on
mkpart ext4 513MiB 10000MiB
mkpart ext4 10000MiB 100%
quit
mkfs.fat -F32 /dev/nvme0n1p1
mkfs.ext4 /dev/nvme0n1p2
```

Now the folder EFI from the tar-file needs to get copied to the first partition (`/dev/nvme0n1p1`) kopiert werden. All other directories from the tar-file need to get copied to the second partition (`/dev/nvme0n1p2`):

```
mkdir -p /media/p1 /media/p2
mount /dev/nvme0n1p1 /media/p1
mount /dev/nvme0n1p2 /media/p2
tar -xvf debian-live-bookworm-0.8.0-20250516183746-amd64.tar.tar --directory /media/p1 --strip-components 1 binary/EFI
tar --exclude='binary/EFI' -xvf debian-live-bookworm-0.8.0-20250516183746-amd64.tar.tar --directory /tmp --strip-components 1
```

In addtion a file has to be created once. This file tells the bootloader the block device uuid of the second partiton which is needed to boot:

```
UUID=$(blkid /dev/nvme0n1p2 -s UUID -o value)
cat <<EOT > /tmp/grub.cfg
search.fs_uuid $UUID root
set prefix=(\$root)'/boot/grub'
configfile $prefix/grub.cfg
EOT
```

The third partition can be prepared for persistentn data (in thes example with enrcryption):

```
/usr/sbin/cryptsetup luksFormat /dev/nvme0n1p3
/usr/sbin/cryptsetup luksOpen /dev/nvme0n1p3 persistence
/usr/sbin/mkfs.ext4 /dev/mapper/persistence
/usr/sbin/e2label /dev/mapper/persistence "persistence"
mkdir -p /mnt/p3
mount /dev/mapper/persistence /mnt/p3
echo "/home union" > /mnt/p3/persistence.conf
echo "/etc/iksdp_persistent union" >> /mnt/p3/persistence.conf
umount /mnt/p3
/usr/sbin/cryptsetup luksClose persistence
```

When you reboot the host the IKSDP desktop should start from the local disk.

#### Update for the local disk

The process is similar to [Update possibility 3](../en/poweruser.md#update-possibility-3-use-image-updater). While booting choose the option "Live System (amd64 update)". Afterwards you have to replace the files on the local disk:

```
mkdir -p /media/p1 /media/p2
mount /dev/nvme0n1p1 /media/p1
mount /dev/nvme0n1p2 /media/p2
tar -xvf debian-live-bookworm-0.8.0-20250516183746-amd64.tar.tar --directory /media/p1 --strip-components 1 binary/EFI
tar --exclude='binary/EFI' -xvf debian-live-bookworm-0.8.0-20250516183746-amd64.tar.tar --directory /tmp --strip-components 1
```

If the client has not enough memory for booting `toram` (Option "Live System (amd64 update)") you can also boot something like [rescuezilla](https://rescuezilla.com/) and run the commands there.

## Customizing the Image

TODO