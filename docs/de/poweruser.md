# IKSDP Desktop Linux Poweruser-Dokumentation

## USB-Stick für einen Nutzer erstellen

TODO

## Betriebssystem aktualisieren

TODO

```bash
mount -t nfs 192.168.200.1:/usb2-part1 /mnt
dd if=/mnt/smb/debian-live* of=/dev/nvme0n1 status=progress 
```