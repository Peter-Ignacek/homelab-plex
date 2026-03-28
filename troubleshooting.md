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
