# Home NAS on TrueNAS scale

## Installation steps

0. Requirements
    - Install ISO TrueNAS-SCALE-22.02.3.iso
    - Smaller drive (old 40GB)
    - Live Gpadted install

1. Install/Upgrade

2. Select initial install device (40GB drive)

3. Password - root

4. Open UI and change settings
    1. DHCP off
    2. static IP 192.168.90.21
    3. hostname dakara
    4. add user lantean

5. Transfer installation to the SSD
    0. [Instructions](https://www.truenas.com/community/threads/truenas-scale-installation-on-partitioned-drive.93533/)
    1. enable SSH in the UI and log into shell as lantean login as root
    2. used commands

        ```BASH
        su root
        # password
        lsblk
        # sdb smaller current boot drive, sda larger empty drive
        sudo gdisk /dev/sdb
            b
            backup_sdb
            q
        sudo gdisk /dev/sda
            r
            l
            backup_sdb
            w
            y
        sudo zpool status boot-pool
        sudo zpool attach boot-pool sdb3 sda3 -f
        sudo zpool status boot-pool #resilvering
        dd if=/dev/sdb2 of=/dev/sda2 # ~5min, 512M
        dd if=/dev/sdb1 of=/dev/sda1
        sudo zpool offline boot-pool sdb3
        sudo zpool detach boot-pool sdb3
        sudo zpool status boot-pool

        sudo gdisk /dev/sda
            p
            n
            <enter> # part number
            <enter> # first sector
            <enter> # last sector
            BF01 # type
            w
            y
        
        sudo gdisk /dev/sda
            x
            i
            4
            # Partition GUID code: 6A898CC3-1DD2-11B2-99A6-080020736631 (Solaris /usr & Mac ZFS)
            # Partition unique GUID: 57208DBD-12C7-4084-91A8-C42BABFB8790
            # First sector: 78163968 (at 37.3 GiB)
            # Last sector: 500118158 (at 238.5 GiB)
            # Partition size: 421954191 sectors (201.2 GiB)
            # Attribute flags: 0000000000000000
            # Partition name: 'Solaris /usr & Mac ZFS'

        ```

    3. shutdown
    4. remove small drive
    5. boot system
    6. used commands

        ```BASH
        zpool create -f ssd-data00 /dev/sda4
        # zpool create ssd-data0 gptid/d08b1137-4fa5-4749-bcfb-f3bd2c12eafc
        # zpool create ssd-data0 /dev/disk/by-partuuid/d08b1137-4fa5-4749-bcfb-f3bd2c12eafc
        zpool export ssd-data00
        ```

    7. Import ssd-data00 in UI
    8. mirror boot pool from UI on another EMPTY drive
    9. repat steps 2.5 - 6

6. Import data pools
    1. shutdown
    2. reconect drives
    3. boot and import pools - HomeArchive

7. create users
    1. u daniel 1001 1002
    2. g Family 1002
    3. u vaclav 1002 1002
    4. u vasek  1003 1002
    5. u blanka 1004 1002

8. Set-up SMB
    - service SMB on, auto start
    - share edit NetBios Name dakara

9. Add catalog for TrueCharts
    - [tutorial](https://truecharts.org/docs/manual/SCALE%20Apps/Quick-Start%20Guides/Adding-TrueCharts/)
    - truecharts; [https://github.com/truecharts/catalog](https://github.com/truecharts/catalog); stable; main

10. install plex
    - TrueCharts/plex
    0. Create Share Dataset for media in HomeArchiveData
        1. new user plex
        2. add user to permissions HomeArhiveData
        3. add mask RWX
        4. New Dataset HomeArchiveData/Media
        5. Permission copy partent
        6. add user to permissions
        7. add mask RWX
        8. create Dataset ssd-data0/app-data
        9. create Dataset ssd-data0/app-data/PlexServer
        10. chown root:plex ; chmod 775

    1. Application Name
        - Name - plex-server
        - Version - 10.1.3
    2. Controller
        N/A
    3. Container configuration
        - server IP: 192.168.90.21
        - image Enviroment: 192.168.0.0/16
        - Plex token - [claim-km_24z49ZJcFzJJHi9Eh]
            - <https://www.plex.tv/claim>

    4. Networking
        - service type: Simple
        - port: 32400
    5. Storage
        - Type
            Host Path: /mnt/ssd-data0/app-data/PlexServer
        - Additional storage
            name: media
            Host Path: /mnt/HomeArchive/HomeArchiveData/Media
            Mount Path: /mnt/media
    6. Ingress
        N/A
    7. Permissions
        - supplimental groups: 1003 (plex)

11. Installing HomeAssistant
    - tutorial [YT](https://www.youtube.com/watch?v=l6EJyK6xO0c)
    0. Create Dataset for media in ssd-data0
        1. new user hauser
        2. create Dataset ssd-data0/app-data
        3. create Dataset ssd-data0/app-data/HomeAssistantServer
        4. create Dataset ssd-data0/app-data/MosquittoBroker
        5. create Dataset ssd-data0/app-data/Zigbee2mqtt
        6. Commands

        ```BASH
        # chown root:hauser ; chmod 775
        sudo install -d -m 0775 -o hauser -g hauser HomeAssistantServer/config/
        ```

    1. Application Name
        - Name - home-assistant-server
        - Version - 15.0.44
    2. Controller
        N/A
    3. Container configuration
        N/A
    4. Networking
        - service type: Simple
        - port: 8123
    5. Storage
        - Type
            Host Path: /mnt/ssd-data0/app-data/HomeAssistantServer/config
    6. Ingress
        N/A
    7. Permissions
        - runAsUser: 0
        - runAsGroup: 0
        - fsGroup 1004 (hauser)
        - supplimental groups: 1004 (hauser)

### System

- Name: Dakara

- domain name: local

- Users

    | Users         | username  | password              |
    | -----         | --------  | --------              |
    | Root          | root      | 331927bf1a85          |
    | WebAdmin      | admin     | 331927bf1a85          |
    | SuperUser     | lantean   | Ll123456              |
    | MQTT          | mqtt      | mqtt                  |
    | PLEX          | plex      | mur0xba*KNU4ptc7cnu   |
    | HomeAssistant | hauser    | GCT2cyf!pwm6pra9zqr   |

    footnote  
  - Root password is = first 12 char from (Dd123456 in sha256) LOWERCASE
