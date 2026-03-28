Plex package updates stopped working through `apt` because Plex migrated to a new Linux repository.

**Cause**

The old repository configuration was no longer valid, so `apt update` could not properly retrieve Plex package information.

**Solution**

The Plex APT repository was reconfigured using the new official repository and signing key.

```bash
curl -fsSL https://downloads.plex.tv/plex-keys/PlexSign.key | gpg --dearmor -o /etc/apt/keyrings/plex.gpg
echo "deb [signed-by=/etc/apt/keyrings/plex.gpg] https://downloads.plex.tv/repo/deb public main" | tee /etc/apt/sources.list.d/plexmediaserver.list
apt update
apt upgrade plexmediaserver
````
Result

Plex updates work again through the normal system package management process.
