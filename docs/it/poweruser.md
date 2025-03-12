# Documentazione per utenti avanzati di IKSDP Desktop Linux  

## Creare una chiavetta USB per un utente  

TODO  

## Aggiornare il sistema operativo  

TODO

```bash
mount -t nfs 192.168.200.1:/usb2-part1 /mnt
dd if=/mnt/smb/debian-live* of=/dev/nvme0n1 status=progress 
```