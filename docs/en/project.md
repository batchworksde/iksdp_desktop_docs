
# IKSDP Project Documentation

## The IKSDP

The IKSDP (International Kenyan Scout Development Program) is an educational institution in Nyandiwa, Kenya. The institution includes a primary school and, newly, a secondary school.

A computer lab with internet access is to be set up for the secondary school. Furthermore, the devices will also be made available to people in the surrounding area.

A computer lab is to be set up that will be open to students, teachers, school management, guests of the IKSDP, and the general public. Internet access has been installed via Starlink. Additionally, a Wi-Fi access point has been installed. This access point could also take on the role of an internet router in the future. It has an LTE modem installed and could connect via mobile providers such as Safaricom (4G+5G are well covered).

## Hardware

The following hardware has been purchased and installed:

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

A separate documentation for the network will be created.

## Software

A live Linux system has been installed on the PCs. This provides both the operating system and all applications. We use Linux because it is a free and open-source operating system. Linux is commonly used in educational institutions for the following reasons:

- The software and operating system can be used and customized for free.
- Linux is less vulnerable to malware and viruses.
- Linux is the leading operating system for servers and embedded systems.

The IKSDP Linux supports two operating modes:

1. **Mode for guests and the public - non-persistent mode**

   All changes are discarded after a reboot. This ensures that no user data from guests or internet café users is stored or lost.
   In this mode, users can install software, but it will be discarded along with all documents and settings upon reboot.

2. **Mode for students and school management - persistent mode**

   A USB stick is prepared for the user or user group. All system changes are saved on the USB stick. Users can install software and create documents that remain available after reboot.
   The data on the USB stick can optionally be encrypted. The user can also set a personal password.

## Open Source Project on Github

This Linux system is available as an open-source project on GitHub at: [https://github.com/batchworksde/iksdp_desktop](https://github.com/batchworksde/iksdp_desktop) and can be further developed by all project participants. GitHub is currently the world's largest platform for open-source development. The "Harambee" principle aligns with the open-source philosophy, which is based on collaboration at eye level. Anyone can join, copy, and/or further develop this project.

Furthermore, the project should not be dependent on specific individuals and should always be able to be taken over or continued by volunteers or the IKSDP.

If new software requirements arise or bugs need to be fixed, they can be reported as issues.

Additionally, the PCs should be updated at least twice a year.

## Remote Support

The local contact person for the PC environment is Victor. The network is connected to the cloud via a ZeroTier VPN. Support personnel can connect to local PCs and network equipment through this VPN if necessary.

For issues and concerns, Victor has multiple support options:

1. **Opening an issue in the GitHub project:** Here, bugs, configuration changes, or additional software requests can be submitted that should be included in the base installation for both persistent and non-persistent modes.
   The issue will be discussed and implemented by a project developer. Once a change is made to the base system, a new base image is created, which must be copied to the PCs. A separate update procedure documentation will be created.

2. **Live support via video conference/RustDesk:**

   If required, the RustDesk application can be started. This generates a password that must be shared live with the support personnel.
   The support personnel will also start the RustDesk application on their side and can then take control of the screen, mouse, and keyboard inputs.
   For this to work, IKSDP Linux must be running and have internet access.

3. **Support via JetKVM:**

   JetKVM is designed for situations where a PC does not start and remote support is required. The JetKVM device is connected to a PC via USB and HDMI. The support personnel can then access the system using a predefined account.
