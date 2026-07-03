### Problem

The NFS mount between the Proxmox host and the UGREEN NAS became unavailable, causing Plex to lose access to the media library.

### Symptoms

- Plex libraries appeared empty or partially unavailable
- Media path was no longer accessible

### Diagnosis

Manual checks confirmed that the mount was no longer active.

### Commands used & Solution

#### Check if the mount is active
````
findmnt /mnt/nfs-plex
````
or
````
df -h | grep nfs
````
Verify fstab configuration (on Proxmox host, NOT inside the Plex container) 
````
nano /etc/fstab
````
Expected entry:
````
<PRIVATE_IP>:/volume1/Plex /mnt/nfs-plex nfs vers=3,rw,hard,timeo=600,retrans=3,_netdev,nofail,x-systemd.automount,x-systemd.idle-timeout=600 0 0
`````

Check the "keep-alive" mechanism
````
stat /mnt/nfs-plex
````
Quick test (verify Plex can see files)
````
ls /mnt/nfs-plex
````
