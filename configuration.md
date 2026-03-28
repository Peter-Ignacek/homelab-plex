# Configuration

This file describes how Plex is configured in my homelab.

## Media Storage

Media files are NOT stored inside the Plex container.

They are stored on an external NAS and mounted into the container.

### Mount point
NFSv3
Active mount:

```bash
/data ← 192.168.1.100:/volume1/Plex


Mount Options

vers=3
proto=tcp
hard
timeo=600
retrans=3
