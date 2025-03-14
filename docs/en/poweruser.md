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

## Update the Operating System  

TODO

```bash
mount -t nfs 192.168.200.1:/usb2-part1 /mnt
dd if=/mnt/smb/debian-live* of=/dev/nvme0n1 status=progress 
```

## Support via Rustdesk Remote Session

### Establish a Remote Session
1. Open the application **"Rustdesk"** by pressing **"Windows"-Key** and then start typing **"Rustdesk"**. 
2. Now click the **"Rustdesk"-Icon**.  
![Rustdesk00](../shared/images/poweruser/rustdesk/rustdesk00.png)
3. A different way to start Rustdesk would be by opening the Applications Tab in the taskbar at the top and then click on **"Internet"** and **"Rustdesk"**.  
![Rustdesk01](../shared/images/poweruser/rustdesk/rustdesk01.png)
4. Now you will send the **"ID"** and the **"One-time Password"** which you can see on the left side to the person you want to receive Support from.  
![Rustdesk02](../shared/images/poweruser/rustdesk/rustdesk02.png)
5. A small window might appear which shows that a device wants to connect to your Computer. Normally the connection gets automatically established. If not, click the **"Accept"** Button.  
![Rustdesk03](../shared/images/poweruser/rustdesk/rustdesk03.png)
6. If its the first time someone connects to your Computer then you will have to select the screen which should be shared. Select the screen, tick the box **"Remember this selection"** and then click **"Share"**.
![Rustdesk04](../shared/images/poweruser/rustdesk/rustdesk04.png)
7. If you see this little icon in the top taskbar, then the connection is established.
![Rustdesk05](../shared/images/poweruser/rustdesk/rustdesk05.png)

### Stop the Remote Session
1. Move your mouse over the **"Rustdesk"-Icon** in the left sidebar. Now two smaller windows should appear next to the sidebar.  
2. Click on the window which shows the active connection.   
![Rustdesk07](../shared/images/poweruser/rustdesk/rustdesk07.png)
3. Now the **"Connection"-Window** should appear on the screen.
4. Click **"Disconnect"** to end the remote session.
![Rustdesk08](../shared/images/poweruser/rustdesk/rustdesk08.png)
5. The small icon in the top taskbar ![Rustdesk09](../shared/images/poweruser/rustdesk/rustdesk09.png) should now be disappeared, which means the connection is closed for the remote device.