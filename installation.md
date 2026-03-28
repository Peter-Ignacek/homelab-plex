# Installation Plex Media Server

## Base

```bash
apt update && apt upgrade -y
apt install curl -y

# Download Plex (latest .deb from official site)
wget https://downloads.plex.tv/plex-media-server-new/...
dpkg -i plexmediaserver*.deb

# Fix dependencies if needed
apt --fix-broken install -y
```

Enable GPU Passthrough (Proxmox Host)

Check if GPU is available:
````
ls /dev/dri
````
Edit container config:
````
nano /etc/pve/lxc/XXX.conf
````
Add:
````
lxc.cgroup2.devices.allow: c 226:* rwm
lxc.mount.entry: /dev/dri dev/dri none bind,optional,create=dir
````
Restart container:
````
pct restart XXX
4. Configure GPU inside Container
````
Check GPU:
````
ls -l /dev/dri
````
Install VAAPI tools:
````
apt install vainfo -y
vainfo
````
Add Plex user to groups:
````
usermod -aG video plex
usermod -aG render plex
````
Restart Plex:
````
systemctl restart plexmediaserver
````
### Enable Hardware Acceleration in Plex

Open Plex Web UI:

Settings → Transcoder
Enable:
✅ Use hardware acceleration when available
✅ Use hardware-accelerated video encoding
6. Verification
Play 4K video
Check dashboard → should show (hw) transcoding
CPU usage should stay low
✅ Result
Stable 4K streaming
Low CPU usage
Hardware transcoding working via VAAPI
⚠️ Notes
Requires Plex Pass
Tested on Intel iGPU (Quick Sync)
Works in unprivileged LXC with proper device mapping
