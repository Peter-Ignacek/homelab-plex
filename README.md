# 🎬 Plex Media Server – Homelab Setup

## 📌 Overview
This repository documents my real-world Plex setup, including storage, synchronization, and troubleshooting.

The setup is designed for:
- reliable media access
- separation of services
- automated media workflow

## ⚙️ Environment
- **Platform:** Proxmox VE
- **Location:** Poland
- **Type:** LXC container
- **OS:** Ubuntu 22.04 LTS
- **Storage:** External NAS (NFS mount)
- **Sync:** Rclone (SFTP)

## Storage

Media is stored on NAS:

- Plex IP 192.168.1.155
- Media on Ugreen NAS + NFS mount:
  192.168.1.100:/volume1/Plex → /data 

## Media Structure

- /data/Movies
- /data/TV
- /data/_radarr
- /data/_sonarr

## Architecture Highlights

- Remote services provide media automation (radarr/sonarr/Prowlarr/Bazarr/Overserr-like)
- Files are synchronized via Rclone (SFTP)
- Hardware acceleration enabled (`/dev/dri`)

  
## 🚀 Features
- Centralized media storage on NAS
- Automated media pipeline (remote → sync → Plex)
- Hardware transcoding
- Live TV / DVR (HDHomeRun)
- Custom troubleshooting and stability improvements
- Stable uptime (40+ days)

## 🌐 Network
- Internal access via LAN
- External via reverse proxy (optional)
- External via VPN WireGuard

## 📂 Data location

/var/lib/plexmediaserver/

## 🔧 Setup Guide
👉 See installation.md

## 🧠 Notes
- Cleaned storage to fix transcode issues
- Fixed repository update (Plex repo migration)


## Status

- Active
- Continuously improved
