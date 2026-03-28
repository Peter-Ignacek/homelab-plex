Media disappeared from Plex.

Solution: keep-alive
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



