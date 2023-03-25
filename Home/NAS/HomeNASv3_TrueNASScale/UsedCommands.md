# Working commands

commands to do various tasks to just to document what i used

## Useful links

Needed to make helm & kubectl work in ssh

[tutorial](https://www.reddit.com/r/truenas/comments/wqzkqq/scale_how_i_run_helm_and_kubectl_from_the_command/)

[kubectl cheatsheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet/#kubectl-context-and-configuration)

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
