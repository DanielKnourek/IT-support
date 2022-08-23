# Used commands

## Sync FROM atached drive to NAS

Mounting drive to NAS

```BASH
mkdir /mnt/usbDrive0
mount /dev/sde1 /mnt/usbDrive0
```

```BASH
sudo nohup sudo rsync --ignore-existing -ra --progress --log-file=/home/rsync.progress.log /mnt/usbDrive0/_zaloha\ NAS/ /mnt/HomeArchive/Archive &

watch tail /home/rsync.progress.log 
```

```BASH
sudo rsync --ignore-existing -ra --progress /mnt/s/ root@192.168.90.21:/mnt/HomeArchive/HomeArchiveData

sudo rsync --ignore-existing -ra --progress /mnt/e/_zaloha\ NAS/Vašek/ root@192.168.90.21:/mnt/HomeArchive/HomeArchiveData/Vašek

sudo rsync --ignore-existing -ra --progress /mnt/h/Společné/ root@192.168.90.21:/mnt/HomeArchive/HomeArchiveData/Společné

sudo rsync --ignore-existing -ra --progress /mnt/h/Táta/ root@192.168.90.21:/mnt/HomeArchive/HomeArchiveData/Táta
```

## cleaning nohup.out

```BASH
sudo rm /home/rsync.progress.log
```

## remove nohup.out in directory

```BASH
find . -name nohup.out
find . -name nohup.out | xargs rm
```

```BASH
sudo nohup sudo mv /mnt/HomeArchive/Archive/* /mnt/HomeArchive/HomeArchiveData/ &

sudo nohup sudo rsync --remove-source-files --ignore-existing -ra --progress --log-file=/home/rsync.progress.log /mnt/HomeArchive/Archive/ /mnt/HomeArchive/HomeArchiveData &
```

```BASH
root@dakara[~]# zpool status
  pool: HomeArchive
 state: DEGRADED
status: One or more devices are faulted in response to persistent errors.
        Sufficient replicas exist for the pool to continue functioning in a
        degraded state.
action: Replace the faulted device, or use 'zpool clear' to mark the device
        repaired.
config:

        NAME                                      STATE     READ WRITE CKSUM
        HomeArchive                               DEGRADED     0     0     0
          raidz1-0                                DEGRADED     0     0     0
            c32dae76-7001-4827-9fdd-0e1e1a173f62  ONLINE       0     0     0
            64b8e4a7-d03d-4543-8423-010a31fab6b4  FAULTED     35     0     0  too many errors
            52d80bcf-7c1d-4174-8329-e4f04b982711  ONLINE       0     0     0
```

commands to create new partiton

```BASH
gdisk /dev/sda
        p
        n
        <enter> # first sector
        <enter> # last sector
        BF01 # type
        w
```

find Guuid

```BASH
gdisk /dev/sda
        i
        4
```

- GUID: D08B1137-4FA5-4749-BCFB-F3BD2C12EAFC  
        to_lowecase
- d08b1137-4fa5-4749-bcfb-f3bd2c12eafc

reload partition table and create new pool

```BASH
partprobe
zpool create -f ssd-data /dev/sda4
# zpool create ssd-data gptid/d08b1137-4fa5-4749-bcfb-f3bd2c12eafc
# zpool create ssd-data /dev/disk/by-partuuid/d08b1137-4fa5-4749-bcfb-f3bd2c12eafc
zpool export ssd-data
```
