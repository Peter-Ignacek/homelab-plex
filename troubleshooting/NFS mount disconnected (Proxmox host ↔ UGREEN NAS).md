### Problem

The NFS mount between the Proxmox host and the UGREEN NAS became unavailable, causing Plex to lose access to the media library.

### Symptoms

- Plex libraries appeared empty or partially unavailable
- Media path was no longer accessible

### Diagnosis

Manual checks confirmed that the mount was no longer active.

Commands used & Solution:

Sprawdzenie czy jest zamontowane:
````
findmnt /mnt/nfs-plex
````
or
````
df -h | grep nfs
````
Spawdzenie wpisu na hoscie pve (nie w kontenerzy plex) 
````
nano /etc/fstab
````
Powinno byc: 
````
192.168.1.100:/volume1/Plex /mnt/nfs-plex nfs vers=3,rw,hard,timeo=600,retrans=3,_netdev,nofail,x-systemd.automount,x-systemd.idle-timeout=600 0 0
`````

Sparwdz tajna bron "keep Alive"
````
stat /mnt/nfs-plex
````
Szybki test (czy Plex widzi pliki)
````
ls /mnt/nfs-plex
````
