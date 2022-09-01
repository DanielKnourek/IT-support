# Sowtware
- [openmediavault.org](https://www.openmediavault.org/)
    - Debian distro 11 - bullseye
    - v 6.0 (16-amd64)
- [Rufus.ie](https://rufus.ie/cs/)
    - v 3.14

# Hardware
- tátuv starý pc
  
# Steps
1. create boot USB (via Rufus)
2. Installation
3. System Configuration [[Jump](#configuration-of-system)]
4. loging in web admin [192.168.0.21](http://192.168.0.21)
    - U: admin U: openmediavault
5. password change
6. lantean add groups (users, ssh)
7. power managment
    - weekly restart
8. **Update system**

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

### footnote
- Root password is = first 8 char from (Dd123456 in sha256) LOWERCASE

# Useful links
- [How to setup openmediavault](https://www.youtube.com/watch?v=M_oxzpvMPTE)
- [Community plugins](https://omv-extras.org/)
