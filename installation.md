# Installation

## Base

```bash
sudo apt update && sudo apt upgrade -y


sudo dpkg -i plexmediaserver*.deb
sudo apt -f install

sudo apt install rclone
rclone config
rclone ls remote:
rclone sync remote:/media /mnt/media
sudo systemctl enable plexmediaserver
