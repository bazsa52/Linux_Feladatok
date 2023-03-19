# Samba szerver telepítése és konfigurálása
Az alábbi leírás debian alapú linux disztribúciókhoz készült.

## Samba telepítése
- sudo apt update
- sudo apt install samba

## Samba konfigurálása
- sudo useradd -r -s /bin/false smbuser
- sudo groupadd smbgroup
- sudo useradd -r -s /bin/false <felhasználónév>
- sudo adduser <felhasználónév> smbgroup
- sudo smbpasswd -a <felhasználónév>
### Feltételezve, hogy a megosztani kívánt mappát a /srv mappán belülre tesszük.
- cd /srv
- sudo mkdir <mappa_neve>
- sudo chown -R smbuser:smbgroup <mappa_neve>
- sudo chmod 775 <mappa neve>
- sudo nano /etc/samba/smb.conf
### Konfig file minta
```
[<Megosztás neve>]
    path = /srv/<mappa_neve>
    directory mask = 766
    create mask = 755
    read only = no
    browsable = yes
    guest ok = no
    valid users = <felhasználók>
```
 - sudo systemctl restart smbd.service
### Ezek után a megosztani kívánt mappa elérhető mások számára.
