# Troubleshooting

## 1. Disk Full (Critical)

### Problem

The container root filesystem became critically full.

### Observed state

- Root filesystem size: 32G
- Usage: 100%

### Main cause

Most of the space was consumed by Plex local data:

- 28G total in Plex application data
- 23G in `.../Plex Media Server/Media`
- 3.1G in `.../Plex Media Server/Metadata`

### Solution
1) Zatrzymaj Plex
systemctl stop plexmediaserver
2) Sprawdź dokładnie co zjada miejsce

Wklej po kolei:
´´´´
du -sh /var/lib/plexmediaserver/Library/Application\ Support/Plex\ Media\ Server/*
´´´´
a potem dokładniej:
´´´´
du -sh /var/lib/plexmediaserver/Library/Application\ Support/Plex\ Media\ Server/Media/*
du -sh /var/lib/plexmediaserver/Library/Application\ Support/Plex\ Media\ Server/Metadata/*

```



## 2. Media disappearing (NAS sleep issue)

### Problem

Media files disappeared from Plex libraries.

### Root Cause

The NAS (UGREEN) aggressively spins down HDDs (sleep mode).  
This caused the NFS mount to become inactive, and Plex temporarily lost access to media.

This is a known issue with some NAS systems in early firmware / aggressive power-saving modes.

---

## Solution

A keep-alive mechanism was implemented on the Proxmox host to prevent the NFS mount from going idle.

Instead of fixing it only on the NAS side, the solution ensures constant activity on the mount.

---

## Implementation (systemd timer)

### Service

```ini
[Unit]
Description=NFS Keepalive (prevent sleep)
After=network-online.target
Wants=network-online.target

[Service]
Type=oneshot
ExecStart=/usr/bin/stat /mnt/nfs-plex
```
Timer
[Unit]
Description=Run NFS keepalive every 10 minutes

[Timer]
OnBootSec=2min
OnUnitActiveSec=10min
AccuracySec=1min
Persistent=true

[Install]
WantedBy=timers.target


Why this works
- stat triggers minimal activity on the mount
- no directory scan (unlike ls)
- prevents NAS from fully idling the share
- keeps Plex library stable
- 
Result

- no more disappearing media
- stable Plex libraries
- no noticeable load on NAS
  
Notes
- keep-alive runs on the Proxmox host
- Plex container does not handle this directly
- long-term improvement would be NAS-side tuning (firmware / sleep settings)

