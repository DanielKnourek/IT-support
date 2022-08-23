## copy files with progres file in output file

```BASH
rsync --progress 2017_06_17/ /srv/dev-disk-by-uuid-22dc9d73-eaa0-4c0b-b4fa-3fa646dca88a/Archive/Vašek/2017_06_17 -r > /tmp/progress.log
```

```BASH
nohup rsync --progress 2017_06_17/ /srv/dev-disk-by-uuid-22dc9d73-eaa0-4c0b-b4fa-3fa646dca88a/Archive/Vašek/2017_06_17 -r > /tmp/progress.log &
```

```BASH
nohup rsync --progress ./ /srv/dev-disk-by-uuid-22dc9d73-eaa0-4c0b-b4fa-3fa646dca88a/Archive/Vašek/ -r >> /tmp/progress.log &
```

```BASH
rsync --progress ./ /srv/dev-disk-by-uuid-22dc9d73-eaa0-4c0b-b4fa-3fa646dca88a/Archive/Vašek/ -r >> /tmp/progress.log &
disown

ps -ef |grep rsync
```

## Sync from NAS to atached drive

```BASH
sudo rsync --ignore-existing -ra --progress --log-file=/home/rsync.progress.log /srv/dev-disk-by-uuid-22dc9d73-eaa0-4c0b-b4fa-3fa646dca88a/Archive/Vašek/UHK /srv/dev-disk-by-uuid-141E2C951E2C71C2/_zaloha\ NAS/Vašek/
```

```BASH
sudo rsync --ignore-existing -ra --progress --log-file=/home/rsync.progress.log /srv/dev-disk-by-uuid-22dc9d73-eaa0-4c0b-b4fa-3fa646dca88a/Archive/Vašek /srv/dev-disk-by-uuid-141E2C951E2C71C2/_zaloha\ NAS/
```

```BASH
sudo nohup rsync --ignore-existing -ra --progress --log-file=/home/rsync.progress.log /srv/dev-disk-by-uuid-22dc9d73-eaa0-4c0b-b4fa-3fa646dca88a/Archive/Vašek /srv/dev-disk-by-uuid-141E2C951E2C71C2/_zaloha\ NAS/ &

watch tail /home/rsync.progress.log 
```

```BASH
sudo nohup rsync --ignore-existing -ra --progress --log-file=/home/rsync.progress.log /srv/dev-disk-by-uuid-22dc9d73-eaa0-4c0b-b4fa-3fa646dca88a/Archive/Táta /srv/dev-disk-by-uuid-D842EDBD42EDA10C/ &

watch tail /home/rsync.progress.log 
```

## rsync from NAS to localhost

```BASH
sudo rsync --ignore-existing -ra --progress --log-file=/home/rsync.progress.log lantean@192.168.90.21:/srv/dev-disk-by-uuid-22dc9d73-eaa0-4c0b-b4fa-3fa646dca88a/Archive/Táta/zal_tata  ./
```

```BASH
sudo rsync --ignore-existing -raz --progress --log-file=/home/rsync.progress.log lantean@192.168.90.21:/srv/dev-disk-by-uuid-22dc9d73-eaa0-4c0b-b4fa-3fa646dca88a/Archive/Táta/ ./
```

```BASH
sudo rsync --ignore-existing -raz --progress --log-file=/home/rsync.progressDaniel.log lantean@192.168.90.21:/srv/dev-disk-by-uuid-22dc9d73-eaa0-4c0b-b4fa-3fa646dca88a/Archive/Mamča/ ./Mamča
```

```BASH
sudo rsync --ignore-existing -raz --progress --log-file=/home/rsync.progressDaniel.log lantean@192.168.90.21:/srv/dev-disk-by-uuid-22dc9d73-eaa0-4c0b-b4fa-3fa646dca88a/Archive/Daniel/ ./Daniel
```



```
rsync --ignore-existing -ra --progress --log-file=/home/rsync.progress.log /srv/dev-disk-by-uuid-22dc9d73-eaa0-4c0b-b4fa-3fa646dca88a/Archive/Táta /srv/dev-disk-by-uuid-D842EDBD42EDA10C/Táta/
```

rsync --ignore-existing -ra --progress --log-file=/home/rsync.progress.log /srv/dev-disk-by-uuid-22dc9d73-eaa0-4c0b-b4fa-3fa646dca88a/Archive/Táta /srv/dev-disk-by-uuid-D842EDBD42EDA10C/


