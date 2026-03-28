# 🎬 Plex Media Server – Homelab Setup

## 📌 Overview
his repository documents my real-world Plex setup, including storage, synchronization, and troubleshooting.

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

## Architecture Highlights

- Plex runs in LXC container
- Media is stored on external NAS (mounted via NFS)
- Remote services provide media automation (radarr/sonarr-like)
- Files are synchronized via Rclone (SFTP)
- Hardware acceleration enabled (`/dev/dri`)

  
## 🚀 Features
- Centralized media storage on NAS
- Automated media pipeline (remote → sync → Plex)
- Hardware transcoding
- Live TV / DVR (HDHomeRun)
- Custom troubleshooting and stability improvements

## 🌐 Network
- Internal access via LAN
- External via reverse proxy (optional)

## 📂 Data location
/var/lib/plexmediaserver/

## 🔧 Setup Guide
👉 See installation.md

## 🧠 Notes
- Cleaned storage to fix transcode issues
- Fixed repository update (Plex repo migration)

## 📸 Screenshots
(optional)

## Status

- Active
- Continuously improved
