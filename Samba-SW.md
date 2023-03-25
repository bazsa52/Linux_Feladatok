# Feladat:
- Samba megosztás SW néven
- SPACE mappa írható, olvasható minden samba felhasználó által
- EMPIRE mappa csak az EMPIRE csoport tagjai által írható, olvasható
- REBELS mappa csak a REBELS csoport tagjai által írható, olvasható
- Az 1. színtű felhasználók csoportjuknak megfelelő máppájukban mindent írhatnak, olvashatnak
- A 2. szintű felhasználók csoportjuknak megfelelő mappájukban mindent olvashatnak, de csak a saját és a 3. szintű falhasználók mappáit írhatják
- A 3. szintű felhasználók csoportjuknak megfelelő mappájukban mindent olvashatnak, de csak a saját mappájukat írhatják
## Felhasználók:
- EMPIRE
  - EMPEROR
  - VADER
  - TARKIN
- REBELS
  - LUKE
  - LEIA
  - CHEWIE
## Parancsok:
```
sudo mkdir -p /srv/samba/SPACE
sudo mkdir /srv/samba/EMPIRE
sudo mkdir /srv/samba/REBELS
sudo groupadd EMPIRE
sudo groupadd REBELS
sudo useradd -M -s /bin/false -G EMPIRE EMPEROR
sudo useradd -M -s /bin/false -G EMPIRE VADER
sudo useradd -M -s /bin/false -G EMPIRE TARKIN
sudo useradd -M -s /bin/false -G REBELS LUKE
sudo useradd -M -s /bin/false -G REBELS LEIA
sudo useradd -M -s /bin/false -G REBELS CHEWIE
sudo groupadd smbgroup
sudo useradd -M -g smbgroup -s /bin/false smbuser
cd /srv/
sudo chown smbuser:smbgroup samba/
cd samba/
sudo chown smbuser:smbgroup SPACE/
sudo chown smbuser:EMPIRE EMPIRE/
sudo chown smbuser:REBELS REBELS/
sudo chmod 777 SPACE/
sudo chmod 770 EMPIRE
sudo chmod 770 REBELS
sudo adduser EMPEROR VADER
sudo adduser EMPEROR smbgroup
sudo adduser VADER TARKIN
sudo adduser VADER smbgroup
sudo adduser TARKIN smbgroup
sudo adduser LUKE smbgroup
sudo adduser LEIA smbgroup
sudo adduser CHEWIE smbgroup
sudo adduser LUKE LEIA
sudo adduser LUKE CHEWIE
sudo adduser LEIA CHEWIE
sudo apt install samba -y
sudo nano /etc/samba/smb.conf 
sudo smbpasswd -a EMPEROR
sudo smbpasswd -a VADER
sudo smbpasswd -a TARKIN
sudo smbpasswd -a LUKE
sudo smbpasswd -a LEIA
sudo smbpasswd -a CHEWIE
sudo systemctl reload smbd.service 
```
## Samba konfiguráció:
```
[SW]
  path = /srv/samba
  browsable = yes
  read only = no
  guest ok = no
  valid users = @smbgroup
  directory mask = 775
  create mask = 664
```
