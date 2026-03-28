## 2. Media disappearing (NFS idle issue)

### Problem

Media files intermittently disappeared from Plex libraries.

### Root Cause

NFS mount became inactive / idle, causing Plex to temporarily lose access to media.

---

## Old (initial workaround)

Previously, a cron-based keep-alive approach was considered:

```bash
*/5 * * * * ls /mnt/media > /dev/null
This approach was not used in the final setup.

Final Solution (production)

A keep-alive mechanism was implemented on the Proxmox host using systemd.

Service
[Service]
Type=oneshot
ExecStart=/usr/bin/stat /mnt/nfs-plex
Timer
runs every 10 minutes
starts automatically after boot
Why stat instead of ls
stat touches the mount only (inode access)
no directory listing
minimal I/O load on NAS
Result
stable NFS mount
no disappearing media
consistent Plex library behavior
Location

Keep-alive is configured on the Proxmox host, not inside the Plex container.





# 📄 troubleshooting.md (🔥 FINAL)

```md
# Troubleshooting

## 1. Disk Full (Critical)

### Problem

Root filesystem reached 100%.

### Cause

Plex stored large local data:

- 28GB total
- 23GB in Media (cache/previews)

### Check

```bash
du -h --max-depth=1 /var/lib/plexmediaserver/Library/Application Support/Plex Media Server



