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
1) Zatrzymaj Plex
systemctl stop plexmediaserver
2) Sprawdź dokładnie co zjada miejsce

Wklej po kolei:
````
du -sh /var/lib/plexmediaserver/Library/Application\ Support/Plex\ Media\ Server/*
````
a potem dokładniej:
````
du -sh /var/lib/plexmediaserver/Library/Application\ Support/Plex\ Media\ Server/Media/*
du -sh /var/lib/plexmediaserver/Library/Application\ Support/Plex\ Media\ Server/Metadata/*
````
🔥 Szybkie rozwiązanie (bezpieczne)

Masz Plex już zatrzymany — idealnie.

💣 KROK 1 – usuń największy syf
````
rm -rf "/var/lib/plexmediaserver/Library/Application Support/Plex Media Server/Media/localhost"
````
💡 To:

❌ NIE usuwa filmów
❌ NIE usuwa biblioteki
✅ usuwa tylko cache / miniatury

👉 odzyskasz ~23 GB od razu

🧹 KROK 2 – szybkie czyszczenie reszty (warto)

````
rm -rf "/var/lib/plexmediaserver/Library/Application Support/Plex Media Server/Cache"/*
rm -rf "/var/lib/plexmediaserver/Library/Application Support/Plex Media Server/Logs"/*
rm -rf "/var/lib/plexmediaserver/Library/Application Support/Plex Media Server/Crash Reports"/*
rm -rf "/var/lib/plexmediaserver/Library/Application Support/Plex Media Server/Codecs"/*
````

👉 kolejne ~500–700 MB odzyskane

▶️ KROK 3 – uruchom Plex
systemctl start plexmediaserver
📊 KROK 4 – sprawdź efekt
df -h /

