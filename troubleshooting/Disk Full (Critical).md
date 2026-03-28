Problem

The container root filesystem became critically full.

### Observed state

- Root filesystem size: 32G
- Usage: 100%

### Main cause

Most of the space was consumed by Plex local data:

- 28G total in Plex application data
- 23G in `.../Plex Media Server/Media`
- 3.1G in `.../Plex Media Server/Metadata`

### Solution
1) Stop Plex
````
systemctl stop plexmediaserver
````
3) Check what is using space

Run:
````
du -sh /var/lib/plexmediaserver/Library/Application\ Support/Plex\ Media\ Server/*
````
Then more detailed:
````
du -sh /var/lib/plexmediaserver/Library/Application\ Support/Plex\ Media\ Server/Media/*
du -sh /var/lib/plexmediaserver/Library/Application\ Support/Plex\ Media\ Server/Metadata/*
````
🔥 Quick fix (safe)

Plex is already stopped — perfect.

💣 STEP 1 – remove the biggest junk
````
rm -rf "/var/lib/plexmediaserver/Library/Application Support/Plex Media Server/Media/localhost"
````
💡 This:

❌ does NOT delete your movies
❌ does NOT delete your library
✅ removes only cache / preview thumbnails

👉 frees ~23 GB immediately

🧹 STEP 2 – clean remaining unnecessary data (recommended)

````
rm -rf "/var/lib/plexmediaserver/Library/Application Support/Plex Media Server/Cache"/*
rm -rf "/var/lib/plexmediaserver/Library/Application Support/Plex Media Server/Logs"/*
rm -rf "/var/lib/plexmediaserver/Library/Application Support/Plex Media Server/Crash Reports"/*
rm -rf "/var/lib/plexmediaserver/Library/Application Support/Plex Media Server/Codecs"/*
````

👉 frees another ~500–700 MB

▶️ STEP 3 – start Plex again
````
systemctl start plexmediaserver
````
📊 STEP 4 – verify result
````
df -h /
````
