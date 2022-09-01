# Home NAS documentation

## Sowtware

- [openmediavault.org](https://www.openmediavault.org/)
  - Debian distro 11 - bullseye
  - v 6.0 (16-amd64)
- [Rufus.ie](https://rufus.ie/cs/)
  - v 3.14

___

## Hardware

- tátuv starý pc

___

## Steps

1. create boot USB (via Rufus)
2. Installation
3. [System Configuration](#configuration-of-system)]
4. loging in web admin [192.168.0.21](http://192.168.0.21)
     - U: admin P: openmediavault
5. password change
6. lantean add groups (users, ssh, openmediavult-*)
7. [Drive setup](#system-drive)
8. power managment
     - weekly restart
9. **Update system**
10. Turn off system and connect other drives
11. [Archive drives setup](##archive-drive-setup)
12. OMV extras  
***As root***

```BASH
sudo wget -O - https://github.com/OpenMediaVault-Plugin-Developers/packages/raw/master/install | sudo bash
```

13. install
    - Addon/openmediavault-flashmemory
14. Install plex
    - omv-extras/docker install
    - omv-extras/portainer install
    - pull image linuxserver/plex:latest
    - create container
15. Plex setup
    ???
    - SSH tunel

    ```BASH
    # Servicies/SSH/TCP forwarding = yes
    ssh 192.168.0.21 -L 8888:localhost:49164 -l lantean
    ```

    - setup on <http://localhost:8888/web>

### plex container settings

| field         | value                        |
| ------------- | ---------------------------- |
| name          | plexServer                   |
| image         | linuxserver/plex:latest      |
| publish ports | yes                          |
| network       | host                         |
| env/PUID      | 1000                         |
| env/PGID      | 100                          |
| volume/bind   | /config <- /srv/config/plex  |
| volume/bind   | /transcode <- /srv/data/plex |
| volume/bind   | /media <- /srv/dev-disk-by-uuid-22dc9d73-eaa0-4c0b-b4fa-3fa646dca88a/Archive/Media |
| Restart policy| always |

___

## Configuration of system

Information about system settings Network, User.

### Network

- static IPv4: [192.168.0.21](http://192.168.0.21)
- IPv4 mask: 255.255.255.0
- Default gateway: [192.168.0.1](https://192.168.0.1)
- DNS: 8.8.8.8

### Localization

- Language: English - United Kingdom
- Timezone:

### System

- Name: Dakara
- domain name: local

| Users     | username  | password  |
| -----     | --------  | --------  |
| Root      | root      | 331927bf  |
| WebAdmin  | admin     | 331927bf  |
| SuperUser | lantean   | Ll123456  |

#### footnote

- Root password is = first 8 char from (Dd123456 in sha256) LOWERCASE

### Sytem Drive

1. Gparted Live image [https://gparted.org/download.php](https://gparted.org/download.php)
2. Resize as shown in table

| ID | type    | size    | map   | type         |
|----|---------|---------|-------|--------------|
| #1 | primary | 64.0GB  | /     | ext4         |
| #  | none    | 50MB    |       | unallocated  |
| #3 | primary | 148.57GB| /srv  | ext4         |
| #2 | logical | 10.95GB |       |              |
| └> | primary | 32.0GB  |       | swap         |

mount #3 to srv

```BASH
sudo cp /tmp/srv /srv -r
echo '#service data' | sudo tee -a /etc/fstab > /dev/null
# ls -al /dev/disk/by-uuid/ # sda3 # 3def2f5a-92d0-43c7-9d0d-598174035e00
echo 'UUID=3def2f5a-92d0-43c7-9d0d-598174035e00 /srv            ext4    defaults        0       0' | sudo tee -a /etc/fstab > /dev/null
sudo mount -a
sudo cp /tmp/srv / -r
```

### Archive drives setup

- RAID 5
- name: HomeArchive

___

## Useful links

- [How to setup openmediavault](https://www.youtube.com/watch?v=M_oxzpvMPTE)
- [Community plugins](https://omv-extras.org/)
- [Gparted](https://gparted.org/download.php)
- [How to mount a partition](https://confluence.jaytaala.com/display/TKB/Mount+drive+in+linux+and+set+auto-mount+at+boot)
- [OMV and plex in docker](https://www.youtube.com/watch?v=BNfk7ji4oh4&t)
