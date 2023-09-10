# Working commands

commands to do various tasks to just to document what i used

## Useful links

Needed to make helm & kubectl work in ssh

[tutorial](https://www.reddit.com/r/truenas/comments/wqzkqq/scale_how_i_run_helm_and_kubectl_from_the_command/)

[kubectl cheatsheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet/#kubectl-context-and-configuration)
[kubectl cheatsheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)

## ix apps

```BASH
# list all helm apps
#  ix-* is app instaled via SCALE UI
helm list --all-namespaces 
```

```BASH
# scale ix-trafeik to 1 replica
kubectl scale -n ix-traefik --replicas=1 deployment traefik

# get current traefik configuration (installation)
helm get values -n ix-traefik traefik  | less
```

## instaling standelone traefik

```BASH
helm repo add traefik https://helm.traefik.io/traefik
helm repo update
helm install traefik traefik/traefik
```

## setup a minecraft server

[https://docker-minecraft-server.readthedocs.io/en/latest/commands/](https://docker-minecraft-server.readthedocs.io/en/latest/commands/)

[https://spacelift.io/blog/kubectl-auto-completion](https://spacelift.io/blog/kubectl-auto-completion)

```BASH
# autocomplete for kubectl
kubectl completion bash | sudo tee /etc/bash_completion.d/kubectl > /dev/null
echo 'alias kl=kubectl' >>~/.bashrc
echo 'complete -o default -F __start_kubectl kl' >>~/.bashrc

# or 

alias kl='sudo k3s kubectl'
kl config set-context --current --namespace=default
  # find pod id   
kl get pods
  #   OR
kl get pods -A

  # exec into pod and send commadns to server
kl exec -it minecraft-stoneblock-minecraft-java-769758c4bb-l2hsr -- 
rcon-cli

kl exec -it $(kl get pods -o=custom-columns=NAME:.metadata.name | tail -1) -- /bin/bash
```

note:

- [https://tcpshield.com/](https://tcpshield.com/)

- [iptables-cheatsheet.md](https://gist.github.com/egernst/2c39c6125d916f8caa0a9d3bf421767a)
- [simple iptables cheatsheet](https://andreafortuna.org/2019/05/08/iptables-a-simple-cheatsheet/)

## forwarding to a service on a different port

```BASH
# reset all rules
iptables -F
iptables -t nat -F
iptables -X

# forward port 25566 to
iptables -t nat -A PREROUTING -p tcp --dport 25566 -j DNAT --to-destination 192.168.0.21:25566
iptables -t nat -A POSTROUTING -p tcp -d 10.147.21.5 --dport 25566 -j SNAT --to-source 10.147.21.5
iptables -t nat -A PREROUTING -p udp --dport 25566 -j DNAT --to-destination 192.168.0.21:25566
iptables -t nat -A POSTROUTING -p udp -d 192.168.0.21 --dport 25566 -j SNAT --to-source 10.147.21.1

# show rules
iptables -t nat -L -n -v
```

```BASH
  apt install netcat -y

  nc -k -l 25566 < /dev/null | nc 192.168.0.21 25566 > /dev/null &

#   OR

    ip link add br0 type bridge
    ip link set zthnhlbjlt master br0

    # test ports are open
    nc -zv {ip} {port}
    nmap -sTU -O {ip}

    # test comunication using netcat
    nc -k -l 1234
```

```BASH
  # OR ngrok
  curl -s https://ngrok-agent.s3.amazonaws.com/ngrok.asc | sudo tee /etc/apt/trusted.gpg.d/ngrok.asc >/dev/null && echo "deb https://ngrok-agent.s3.amazonaws.com buster main" | sudo tee /etc/apt/sources.list.d/ngrok.list && sudo apt update && sudo apt install ngrok

  ngrok config add-authtoken 1pWLMplk9UeSEDLKOJZ5wqkmo0V_71t39ZkJgagwcG5ZokvAt

  ngrok tcp 25566
```

### Yet another backing up to an external drive

```BASH
  sudo mount /dev/sdc1 /mnt/external-drive

  # copy from HomeArchive to external drive
  sudo rsync --ignore-existing -ra --progress --log-file=/home/rsync.progress.log /mnt/HomeArchive/HomeArchiveData/Vašek/ /mnt/external-drive/_zaloha\ NAS/Vašek/
  df -h /mnt/external-drive

  # nohup sudo rsync --ignore-existing -ra --progress --log-file=/home/rsync.progress.log /mnt/HomeArchive/Archive/ /mnt/external-drive/_zaloha NAS &

  sudo mkdir -p /mnt/photo-movie-drive
  sudo install -d -m 0770 -o root /mnt/photo-movie-drive
  sudo mount /dev/sde2 /mnt/photo-movie-drive


  sudo rsync --ignore-existing -ra --progress --log-file=/home/rsync.progress.log /mnt/HomeArchive/HomeArchiveData/Vašek/ /mnt/photo-movie-drive/3TB Data-Filmy-Foto
  df -h /mnt/photo-movie-drive

  sudo rsync --ignore-existing -czraP -t --progress lantean@dakara:/mnt/HomeArchive/HomeArchiveData/Daniel/* /mnt/e/Daniel/
```
