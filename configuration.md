# Configuration

This file describes how Plex is configured in my homelab.

## Media Storage

Media files are NOT stored inside the Plex container.

They are stored on an external NAS and mounted into the container.

### Mount point
NFS Mount
```text
/mnt/media

Active mount:

```bash
/data ← 192.168.1.100:/volume1/Plex
Verified with:
findmnt -t nfs,nfs4
Mount Options
vers=3
proto=tcp
hard
timeo=600
retrans=3
Meaning
hard → retry until server responds
tcp → stable connection
timeo/retrans → timeout and retry tuning
