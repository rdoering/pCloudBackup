# My pCloud Backup

## Inbetriebnahme

1. Sicherstellen, dass die Rclone Konfiguration in der Datei `rclone.conf` existiert.
2. Container starten mit `docker compose up -d`
3. (optional) Restic-Repository initiiren in der pCloud. `docker compose exec restic restic init`


## Restic Konfigurieren

In der ´.env´ ist das Restic-Password für das Backup-Repository konfiguriert.

```
RESTIC_PASSWORD=CHANGEME
```

## Rclone Konfiguration prüfen

```bash
docker compose exec restic rclone lsd mypcloud:/
```

Beispiel-Output
```bash
          -1 2023-09-30 05:35:30        -1 Automatic Upload
          -1 2023-12-17 21:08:24        -1 Crypto Folder
          -1 2023-12-17 22:18:18        -1 backup
```

## Run a Backup

