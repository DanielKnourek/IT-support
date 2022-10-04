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
        1. Application Name
            - Name - traefik
            - Version - 13.4.5
        2. Controller
            - Extra Args
                - --experimental.plugins.traefik-ondemand-plugin.modulename=github.com/acouvreur/traefik-ondemand-plugin
                - --experimental.plugins.traefik-ondemand-plugin.version=v1.3.0
                - --providers.kubernetesingress.allowEmptyServices=true
        3. Container configuration
            N/A
        4. App configuration
            N/A
        5. Networking
            - Entrypoints Port (Dashboard): 9000
            - web Entrypoints conf
                - Port: 80
            - websecure Entrypoints
                - Port: 443
        6. Ingress
            N/A
        7. Security
            N/A
