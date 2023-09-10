
- NAS 3x 4TB
- NAS 1x 3TB

- ExternalDrive 1x 2TB

- OfficePC 1x 4TB

- NewDrive 1x 4TB


## Target

- NAS 5x 4TB
    - NAS 3x 4TB
    - NewDrive 1x 4TB
    - OfficePC 1x 4TB


## tmp backup
 - current max
    - 7TB
 - used space
    - 4.8TB

- NAS 1x 3TB
- ExternalDrive 1x 2TB \\dakara\HomeArchive\Vašek

```BASH
/mnt/HomeArchive/HomeArchiveData/
├── Daniel ✔✔
│   └──> Daniel-GamingPC:/mnt/e/Daniel
├── Mamča ✔✔
│   └──> VERBATIM 2TB HDD:/_zaloha NAS/Mamča
├── Media ✔✔
│   └──> Daniel-GamingPC:/mnt/e/Media
├── Sdilene ✔✔
│   └──> VERBATIM 2TB HDD:/_zaloha NAS/Sdilene
├── Táta
│   ├── 'Archiv Filmy' ✔✔
│   │    └──> Kancelar-Doma:/mnt/f/3TB Data-Filmy-Foto/'Archiv Filmy'
│   ├── 'Archiv FOTO'
│   │    ├── ' FOTO Album Scener-ORIGINÁLU z fotoalbumu' ✔✔
│   │    │    └──> Daniel-GamingPC:/mnt/e/Táta/'Archiv\ FOTO'/'FOTO Album Scener-ORIGINÁLU z fotoalbumu'
│   │    ├── 'ARCHIV FOTO ORIGINÁLU' ✔✔ (535 GB) (48 875 souborů, 641 složek)
│   │         └──> Kancelar-Doma:/mnt/f/3TB Data-Filmy-Foto/'ARCHIV FOTO ORIGINÁLU'
│   │    └── 'FOTO ALBUM-ORIGINÁL Archiv' ✔✔
│   │         └──> Daniel-GamingPC:/mnt/e/Táta/'Archiv\ FOTO'/'FOTO ALBUM-ORIGINÁL Archiv'
│   ├──  aTáta
│   │    ├── 'Archiv FOTO' ✔✔
│   │    │    └──> Daniel-GamingPC:/mnt/e/Táta/'Archiv\ FOTO'
│   │    ├── 'Disk_D 150Gb Data' ✔✔
│   │    └── 'Disk_G 500Gb Music-Filmy' ✔✔
│   │         └──> Daniel-GamingPC:/mnt/e/Táta/'z_Disk_G 500Gb Music-Filmy'
│   ├── 'Disk_D 150Gb Data' ✔✔
│   │    └──> Kancelar-Doma:/mnt/f/'Disk_D 150Gb Data'
│   ├──  Kázetko_Images ✔✔
│   │    └──> Daniel-GamingPC:/mnt/e/Táta/Kázetko_Images
│   ├──  Kuchyn16GB ✔✔
│   │    └──> Daniel-GamingPC:/mnt/e/Táta/Kuchyn16GB
│   ├──  KZBack ✔✔
│   │    └──> Daniel-GamingPC:/mnt/e/Táta/KZBack
│   ├──  vaclav ✔x✔
│   │    └──> system, none
│   ├── 'z_Disk_G 500Gb Music-Filmy' ✔✔
│   │    └──> Daniel-GamingPC:/mnt/e/Táta/'z_Disk_G 500Gb Music-Filmy'
│   └──  zal_tata ✔✔
│        └──> Daniel-GamingPC:/mnt/e/Táta/zal_tata
└── Vašek ✔✔
    └──> VERBATIM 2TB HDD:/_zaloha NAS/Vašek
```

```BASH
/mnt/m/ (DiskSA_Data HDD-NAS) M: 830GB ✔✔
└──> Kancelar-Doma:/mnt/c/NAS_backup/DiskSA_Data HDD-NAS

/mnt/n/ (Archiv Foto-Filmy) N: 2.8TB
├── Archiv Filmy ✔xx✔
│   └──> Kancelar-Doma:/mnt/f/3TB Data-Filmy-Foto/
└── ARCHIV FOTO ORIGINÁLU ✔✔
    └──> Kancelar-Doma:/mnt/f/3TB Data-Filmy-Foto/
```


## HomeArchive disk schema v1.0

- RAIDz1
  - 3x 4TB
    - sdb
      - serial: WD-WCC4E5HTNKR6
      - size: 3.64TiB
      - model: WDC_WD40EFRX-68WT0N0
      - Last Short Test: SUCCESS
      - Last Extended Offline Test: SUCCESS
      - First use: (OG)
    - sdc
      - serial: WD-WCC4E4NYKP0J
      - size: 3.64TiB
      - model: WDC_WD40EFRX-68WT0N0
      - Last Short Test: FAILED   (Device: /dev/sdc [SAT], 8 Currently unreadable (pending) sectors.) 2023-06-15 02:20:15 (Europe/Prague)
      - Last Extended Offline Test: FAILED
      - First use: (OG)
    - sde
      - serial: WD-WCC7K0VP9RZ3
      - size: 3.64TiB
      - model: WDC_WD40EZRZ-00GXCB0
      - Last Short Test: SUCCESS
      - Last Extended Offline Test: SUCCESS
      - First use: (OG+)

## HomeArchive disk schema v2.0

- RAIDz2
  - 6x 4TB
    - sdb
      - serial: WD-WCC4E5HTNKR6
      - size: 3.64TiB
      - model: WDC_WD40EFRX-68WT0N0
      - Last Short Test: SUCCESS
      - Last Extended Offline Test: SUCCESS
      - First use: (OG)
    - sdc
      - serial: WD-WCC4E4NYKP0J
      - size: 3.64TiB
      - model: WDC_WD40EFRX-68WT0N0
      - Last Short Test: FAILED   (Device: /dev/sdc [SAT], 8 Currently unreadable (pending) sectors.) 2023-06-15 02:20:15 (Europe/Prague)
      - Last Extended Offline Test: FAILED
      - First use: (OG)
    - sde
      - serial: WD-WCC7K0VP9RZ3
      - size: 3.64TiB
      - model: WDC_WD40EZRZ-00GXCB0
      - Last Short Test: SUCCESS
      - Last Extended Offline Test: SUCCESS
      - First use: (OG+)
