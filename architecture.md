# Architecture

## High-Level Overview

```text
Remote Seedbox (NL)
    │
    │  (SFTP / Rclone sync)
    ▼
NAS (UGREEN)
    │
    │  (NFS mount)
    ▼
Plex LXC (Proxmox PL)
    │
    ▼
Clients (TV / Apps)
