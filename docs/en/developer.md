# IKSDP Desktop Linux Developer Documentation

## Target Audience of the Document

This document is intended for individuals who want to customize or extend IKSDP Linux.

The project is currently hosted on [GitHub](https://github.com/batchworksde/iksdp_desktop). The documentation is hosted here.

## Download and Installation

On the target system, the live system is booted from an SSD. However, for testing purposes, the system can also be started from a USB stick on hardware or from a DVD image in a virtual machine.

The latest release can be downloaded from [GitHub Releases](https://github.com/batchworksde/iksdp_desktop/releases). Under "ISO Image," a link to the current ISO is provided.

Intermediate releases are made available via the web server [iksdp.pfadfinderzentrum.org](http://iksdp.pfadfinderzentrum.org).

## Creating an Image Locally

There are currently two tested methods to create the image locally. In both cases, a Linux-based system is required.

- A .deb-based distribution is used (we have tested Debian 12 and Ubuntu 24.04).
- The image is created using a `docker` or `podman` container.

In both cases, the user building the image must have `sudo` privileges.

First, the image must be cloned from GitHub:

```bash
git clone git@github.com:batchworksde/iksdp_desktop.git
```

Next, an environment variable `ROOTPW` must be set, which will be used as the password for the `root` user in the image.

### Creating an Image on a Debian-Based System

The build script `debian-live/build.sh` is executed.

```