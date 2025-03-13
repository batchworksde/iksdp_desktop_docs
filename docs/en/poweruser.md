# IKSDP Desktop Linux Power User Documentation  

- we can choose if to encrypt the stick or not, **if the USB stick is encrypted and the password is lost, access to the documents on the stick is completly lost**

- start the shell script
- open "terminal": e.g.:  Applications -> Utilities -> Terminal
```bash
su - 
```
- enter superuser password

```
/opt/iksdp/bin/create-usb-stick.sh
```
- he will prompt to select the device to prepair
- choose the highest number
- "do you want to proceed" -> y
- "do you want to unmount" -> y
- "Enter size for the first partition in MB" -> default..
- do you want to encrypt the second partition? -> please choose
- proceed anyway -> y

TODO  

## Update the Operating System  

### Download latest image and copy to central storage

- on the running iksdp os
- download the newest image (.hybrid.iso) from the distribution share [http://iksdp.pfadfinderzentrum.org](http://iksdp.pfadfinderzentrum.org)
- get connection to storage on router
- open terminal -> windows key -> type "terminal"
- enter:

```bash
su - 
mount -t nfs 192.168.200.1:/usb2-part1/smb /mnt
```
- copy the downloaded image file to /mnt


### Update possibility 1: Update using the network

- start the pc to update and hit "Delete" Button - at black screen and hit delete multiple times.
- use keyboard to select boot and ensure "Network UEFI:.." is selected as Boot Option #1

![biossettings](../shared/images/netboot-bios1.png)

- select save+exit -> save settings and exit

![bios_save_exit](../shared/images/netboot-bios2.png)

- this screen might occur.. reboot at this step and hit F7 after boot

![bios_save_exit](../shared/images/netboot-error1.png)

- this is the correct bootscreen hit enter

![step1](../shared/images/netboot-step1.png)

- select "Upgrade IKSDP"

![step2](../shared/images/netboot-step2.png)

- when updater is started completely it will look like this

![step3](../shared/images/netboot-step3.png)


- enter the folling commands to connect to central storage and attach it to the /mnt directory

```bash
sudo bash
mount -t nfs 192.168.200.1:/usb2-part1/smb /mnt
```

- correct output will be something like this

![step4](../shared/images/netboot-step4.png)

- copy the image using the dd command to the NVME Harddisk of the pc - **ensure your image name is correct**

```bash
dd if=/mnt/debian-live-bookworm-0.5.0-20250313055721-amd64.hybrid.iso of=/dev/nvme0n1 status=progress
```

![copy_image](../shared/images/netboot-step5.png)

- run reboot command

![copy_image](../shared/images/netboot-step6.png)

- enter BIOS setup using the Delete button at start

![copy_image](../shared/images/netboot-step7.png)

- select boot and ensure "NVME" is selected as Boot Option #1

![copy_image](../shared/images/netboot-step8.png)

- select save+exit -> save settings and exit

![bios_save_exit](../shared/images/netboot-bios2.png)

- check that image have a higher version now

![copy_image](../shared/images/netboot-step9.png)

- Done


### Update possibility 2: use USB Stick

#### ensure usb boot is enabled

- start the pc to update and hit "Delete" Button - at black screen and hit delete multiple times.
- use keyboard to select boot and ensure **"USB"** is selected as Boot Option #1

![biossettings](../shared/images/bios_boot_usb.png)

- press F10 to save & exit
- reboot the PC


#### always
- enter special usb update stick
- select "try or install ubuntu"

![biossettings](../shared/images/usb_boot_step1.png)

- wait for the "Welcome to Ubuntu" to start fully
- when "choose your language" appears you can close the windows using the X

![biossettings](../shared/images/usb_boot_step2.png)

- start "terminal"

![biossettings](../shared/images/usb_boot_step3.png)


- run commands to connect to central storage
```bash
sudo bash
mount -t cifs -o username=user,password=live //192.168.200.1/smb /mnt
```

![biossettings](../shared/images/usb_boot_step4.png)



- update nvme harddisk using the commands
```bash
dd if=/mnt/debian-live-bookworm-0.5.0-20250313055721-amd64.hybrid.iso of=/dev/nvme0n1 status=progress
```

![biossettings](../shared/images/usb_boot_step5.png)


- type "reboot"
- pull out update stick and press enter when prompted

![biossettings](../shared/images/usb_boot_step6.png)

- check that image have a higher version now

![copy_image](../shared/images/netboot-step9.png)
