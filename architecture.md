# Architecture

## High-Level Overview

```text
Remote Seedbox (Prowlarr,Sonarr,Radarr,Bazarr)
    │
    │  (SFTP / Rclone sync)
    ▼
NAS (UGREEN)
    │
    │  (NFS mount)
    ▼
Plex LXC Ubuntu 22.04 (Proxmox PL) + (Tautulli,Maintainer,Overseerr)
    │
    ▼
Clients (TV / Apps)



### NAS

- IP: 192.168.1.100
- NFS share: /volume1/Plex
- mounted to: /data

## Data Flow

Media files are stored on NAS and accessed via NFS mount.

## Notes

Rclone is NOT running inside this container. (runs on PVE node)

Media synchronization is handled externally.
