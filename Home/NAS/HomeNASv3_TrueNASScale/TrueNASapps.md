# TrueNAS scale app install manual

## Installation steps

0. Add catalog for TrueCharts
    - [tutorial](https://truecharts.org/docs/manual/SCALE%20Apps/Quick-Start%20Guides/Adding-TrueCharts/)
    - truecharts; [https://github.com/truecharts/catalog](https://github.com/truecharts/catalog); stable; main

1. Pi-Hole
    1. create Dataset
        ssd-data0/app-data/Pi-Hole
    2. Setup
        1. Application Name
            - Name - pihole
            - Version - 6.0.35
        2. Controller
            N/A
        3. Container configuration
            N/A
        4. App configuration
            WEBPASSOWRD: PiHole credentials
            DNS1: 1.1.1.1
        5. Networking
            N/A
        6. Storage
            - Type
                Host Path: /mnt/ssd-data0/app-data/Pi-Hole
        7. Ingress
            N/A
        8. Security
            N/A
    3. Login into Pi-Hole
        1. Tools -> Update Gravity

2. Traefik
    1. Setup
        ```BASH
        helm install traefik TrueCharts/traefik

        helm upgrade --install traefik TrueCharts/traefik
        --namespace hub-agent --create-namespace \
        --set=additionalArguments='{--experimental.hub,--hub}' \
        --set metrics.prometheus.addRoutersLabels=true \
        --set providers.kubernetesIngress.allowExternalNameServices=true \
        --set ports.web=null --set ports.websecure=null --set ports.metrics.        expose=true \
        --set ports.traefikhub-tunl.port=9901 --set ports.traefikhub-tunl.      expose=true --set ports.traefikhub-tunl.exposedPort=9901 --set ports.   traefikhub-tunl.protocol="TCP" \
        --set service.type="ClusterIP" --set fullnameOverride=traefik-hub 

        helm repo add traefik-hub https://helm.traefik.io/hub
        helm repo update

        helm upgrade --install hub-agent traefik-hub/hub-agent \
        --set token="d8c508a5-010a-4fc1-8c0e-d7e98026c932" --namespace hub-agent \
        --create-namespace 
        ```