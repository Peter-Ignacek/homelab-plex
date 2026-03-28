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


---

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



