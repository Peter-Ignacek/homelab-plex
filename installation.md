# Installation Plex Media Server

## Base

```bash
apt update && apt upgrade -y
apt install curl -y

# Download Plex (latest .deb from official site)
wget https://downloads.plex.tv/plex-media-server-new/...
dpkg -i plexmediaserver*.deb

# Fix dependencies if needed
apt --fix-broken install -y ```
 dfgdfg
