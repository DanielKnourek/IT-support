# Home NAS on TrueNAS scale

## Installation steps

0. Requirements
    - Install ISO TrueNAS-SCALE-22.02.3.iso
    - Smaller drive (old 40GB)
    - Live Gpadted install

1. Install/Upgrade

2. Select initial install device (40GB drive)

3. Password - root

### System

- Name: Dakara

- domain name: local

- Users

    | Users     | username  | password      |
    | -----     | --------  | --------      |
    | Root      | root      | 331927bf1a85  |
    | WebAdmin  | admin     | 331927bf1a85  |
    | SuperUser | lantean   | Ll123456      |

    footnote  
    - Root password is = first 12 char from (Dd123456 in sha256) LOWERCASE
