# Sowtware
- [debian.org](https://www.debian.org/devel/debian-installer/)
    - Debian Bullseye RC 2 release
    
- [Rufus.ie](https://rufus.ie/cs/)
    - v 3.14

<br><br>

# Hardware
- tátuv starý pc

<br><br>

# Steps
1. create boot USB (via Rufus)
2. Installation
3. [System Configuration](#configuration-of-system)
4. Installation of OMV
    ```BASH
    echo "deb http://packages.openmediavault.org/public erasmus main" > /etc/apt/sources.list.d/openmediavault.list
    apt-get update
    apt-get install openmediavault-keyring postfix
    apt-get update
    apt-get install openmediavault
    omv-initsystem
     ```
4. loging in web admin [192.168.0.21](http://192.168.0.21)
    - U: admin U: openmediavault
5. password change
6. lantean add groups (users, ssh)
7. power managment
    - weekly restart
8. **Update system**

<br><br>

# Configuration of system
Information about system settings Network, User.

## Network 
- static IPv4: [192.168.0.21](http://192.168.0.21)
- IPv4 mask: 255.255.255.0
- Default gateway: [192.168.0.1](https://192.168.0.1)
- DNS: 8.8.8.8 

## Localization 
- Language: English - United Kingdom
- Timezone: 
## System
- Name: Dakara
- domain name: local

| Users     | username  | password  |
| -----     | --------  | --------  |
| Root      | root      | 331927bf  |
| WebAdmin  | admin     | 331927bf  |
| SuperUser | lantean   | Ll123456  |

* adduser lantean
* usermod -aG sudo lantean
* su - lantean

### footnote
- Root password is = first 8 char from (Dd123456 in sha256) LOWERCASE  

## Storage
### 256 SSD
steps:
```BASH
sudo parted
resizepart 1 32G
```
| ID | type    | size    | map   | type  |
|----|---------|---------|-------|-------|
| #1 | primary | 510.7MB | /boot | ext2  |
| #5 | logical | 230.0GB |       | lvm   |
| └> | logical | 32.0GB  | /     | ext4  |
| └> | logical | 198.0GB | /srv  | ext4  |
| #  | pri/log | 3.6GB   |       | EMPTY |
| #3 | primary | 6.0GB   | swap  | swap  |


<br><br>

# Useful links
- [How to setup openmediavault](https://www.youtube.com/watch?v=M_oxzpvMPTE)
- [Community plugins](https://omv-extras.org/)
