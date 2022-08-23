# Home NAS on TrueNAS scale

## Plex server

1. Install Plex server
    - Apps -> Plex Media Server -> Install

    1.1.
    - Name - home-plex-media
    - Version - 1.7.14

    1.2.
    - Plex token - [claim-uZhFGxN2EjxS-Dxsch6M]
    - <https://www.plex.tv/claim>

    1.3.
    - Configure Host Network - No
    - port - 32400

    1.4.
    - Create new dataset
        - ssd-data/PlexServer
    - Transcode Volume
        - /mnt/ssd-data/PlexServer
    - Data Volume
        - /mnt/ssd-data/PlexServer
    - Config Volume
        - /mnt/ssd-data/PlexServer
    - exstra Volume
        - /mnt/HomeArchive/HomeArchiveData/Media

    1.5.
    - Kill existing pods

    1.6.
    - none
