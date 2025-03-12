
# IKSDP User Documentation

## Target Audience of the Document

This document is intended for users of the IKSDP Desktop Linux. This operating system is a live Linux system that supports two different operating modes.

## Starting the System

When starting the system, you will see the following screen:

![systemboot](../shared/images/systemboot.png)

"Live system (amd64)" is preselected. If you do not connect a USB stick to the system, it will start in non-persistent mode. If you connect a prepared USB stick, the system will start in persistent mode.

If the USB stick is inserted after the boot selection, the system will remain in non-persistent mode. The system must be restarted to switch to persistent mode.

### Non-Persistent Mode

This mode is the default mode. It can be recognized by the "non-persistent" label displayed in the top right corner of the desktop.

![non-persistent](../shared/images/non-persistent.png)

In this mode, changes to the system can be made; however, these changes will be completely lost after a system restart.

If you create files during a user session that you wish to edit later, they must be saved on a mobile storage device such as a USB stick, a smartphone, or a cloud service.

### Persistent Mode

In this mode, user changes are saved on a specially prepared USB stick. This means that user settings in programs, such as bookmarks in browsers, and files will be retained even after a system restart, unlike in non-persistent mode.

![persistent](../shared/images/persistent.png)

The USB stick must not be removed from the system while in persistent mode; otherwise, data loss may occur.

## Installing Additional Software

Additional software can be installed. In non-persistent mode, this must be done after every system start. If software should be permanently added to the installation, please contact your local IKSDP representative. They can arrange the installation for you.

Select "System Tools" -> "Software".

![Software_installation](../shared/images/install_software01.png)

Search for the software and select it:

![Software_installation](../shared/images/install_software02.png)

Install the software - "Flatpak" should be displayed under the software.

![Software_installation](../shared/images/install_software03.png)

The installation of the software may take some time depending on its size.

![Software_installation](../shared/images/install_software04.png)

![Software_installation](../shared/images/install_software05.png)

Once the software is installed, it can be started via "Open".

## Shutting Down the System

The system can be shut down via the power symbol in the top right corner. Select the icon and "Power Off", then confirm.

![Shutdown01](../shared/images/shutdown_01.png)

![Shutdown02](../shared/images/shutdown_02.png)
