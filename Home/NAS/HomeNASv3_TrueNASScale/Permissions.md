# Permissions for SMB share

## ~/HomeArchive/HomeArchiveData

```BASH
sudo -i
cd /mnt/HomeArchive/HomeArchiveData
install -d -m 0770 -o daniel -g noFamily Daniel/
install -d -m 0770 -o vaclav -g noFamily Táta/
install -d -m 0770 -o vasek -g noFamily Vašek/
install -d -m 0770 -o blanka -g noFamily Mamča/

install -d -m 0770 -o root -g Family Společné/
install -d -m 0770 -o root -g Family Media/
install -d -m 0770 -o root -g Family Media/Filmy
install -d -m 0770 -o root -g Family Media/Filmy&Videa
install -d -m 0770 -o root -g Family Media/Hudba
install -d -m 0770 -o root -g Family Media/Seriály
```
