# Architecture

## High-Level Overview

```text
Remote Seedbox (Prowlarr,Sonarr,Radarr)
    │
    │  (SFTP / Rclone sync)
    ▼
NAS (UGREEN)
    │
    │  (NFS mount)
    ▼
Plex LXC (Proxmox PL) + (Tautulli,Maintainer,Overseerr)
    │
    ▼
Clients (TV / Apps)
