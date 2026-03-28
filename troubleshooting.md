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

### Check

```bash
du -h --max-depth=1 "/var/lib/plexmediaserver/Library/Application Support/Plex Media Server" | sort -hr
df -hT

```
2. Media disappearing (NFS idle issue)
Problem

Media files intermittently disappeared from Plex libraries.

Root Cause

NFS mount became inactive / idle, causing Plex to temporarily lose access to media.

Old (initial workaround)

Previously, a cron-based keep-alive approach was considered:

*/5 * * * * ls /mnt/media > /dev/null

This approach was not used in the final setup.

Final Solution (production)

A keep-alive mechanism was implemented on the Proxmox host using systemd.

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
