# IKSDP Desktop Linux Project Documentation  

## The IKSDP  

The IKSDP (International Kenyan Scout Development Program) is an educational institution in Nyandiwa, Kenya. The facility includes a kindergarten, a primary school, and, more recently, a secondary school.

A computer lab with internet access is to be set up for the secondary school. Additionally, the devices should also be available for use by people in the surrounding community.  

## The Computer Lab  

The computer lab is intended to be accessible to students, teachers, school administration, guests of the IKSDP, and the general public. An internet connection via Starlink has been installed. Additionally, a Wi-Fi access point has been set up, which could serve as an internet router in the future. This access point includes an integrated LTE modem, which could be used via mobile providers like Safaricom (4G+5G coverage is strong). This setup ensures that internet access is theoretically redundant, in case Starlink is deactivated in the future.  

### Hardware  

The following hardware has been purchased and installed:  

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

The network documentation is available to the power user.  

### Software  

A live Linux system has been installed on the PCs. This provides both the operating system and all required applications. We use Linux because it is a free and open-source operating system. Linux is widely used in educational institutions for the following reasons:  

- Linux and its software can be used and modified free of charge.  
- Linux is less vulnerable to malware and viruses.  
- Linux is the leading operating system for servers and embedded systems.  

IKSDP Linux supports two operating modes:  

#### Guest and Public Mode: Non-Persistent Mode  

All changes are discarded after a reboot. This ensures that no user data from guests or internet café users is stored or lost.  
Users can install software, but all software, documents, and settings will be reset upon restart.  

#### Student and Administration Mode: Persistent Mode  

For this mode, a USB stick is prepared for the user or user group. All changes to the system are saved on the USB stick. Users can install software and create documents that will remain available after a restart.  
The data on the USB stick can optionally be encrypted. Users can also set a personal password.  

## Open Source Project on GitHub  

The Linux operating system used is available as an open-source project on GitHub at [https://github.com/batchworksde/iksdp_desktop](https://github.com/batchworksde/iksdp_desktop) and can be further developed by all project participants. GitHub is currently the world's largest platform for open-source development. The "Harambee" philosophy aligns with the open-source concept, which emphasizes collaborative project work on an equal footing. Anyone can join, copy, and further develop this project.  

Furthermore, the project should not depend on specific individuals and should always be transferable to volunteers or the IKSDP.  

If new software requirements arise or issues need to be resolved, they can be reported as an issue on GitHub.  

Additionally, the PCs should be updated at least twice a year.  

## Remote Support  

The local contact person for the PC environment is Victor. The network is connected to the cloud via ZeroTier VPN. Support staff can connect remotely to local PCs and network equipment via this VPN if needed.  

For troubleshooting and support, Victor has multiple options:  

#### 1. Creating an Issue on the GitHub Project  

This requires a working internet connection. Issues can also be created from a mobile phone or tablet.  
Issues can include bug reports, configuration changes, or requests for additional software to be included in the base installation (both persistent and non-persistent modes).  
A project developer will review and potentially implement the requested changes. If a change is made to the base system, a new base image will be created. This image must then be copied to the PCs.  

The documentation for creating GitHub issues is available to the power user.  
The documentation for the update process is available to the power user.  

#### 2. Live Support via Video Conference/RustDesk  

For this, IKSDP Linux must be running, and internet access must be available.  
If necessary, the **"RustDesk"** application can be launched. RustDesk provides the user with an ID and password, which must be communicated to the support staff in real time.  
The support staff also starts the RustDesk application and can then view the remote screen and control the mouse and keyboard.  

#### 3. Support via JetKVM  

For this, an internet connection is required.  
The JetKVM is intended for cases where a PC does not start, and remote support is needed. The JetKVM device is connected to a PC via USB and HDMI. The support staff can then remotely access the PC using a designated account and even make BIOS adjustments.  
