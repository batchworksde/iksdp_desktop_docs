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

## Customizing the Image

TODO