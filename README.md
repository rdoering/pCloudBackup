# My pCloud Backup

This is my approach to backup my data with following features.
- The backup encrypted
- The backup is configured in files
- The backup can run regular
- The backup can be verified
- The backup can be monitored
- The backup can be restored everywhere

## Initial operation

1. Ensure that the Rclone configuration exists in the `rclone.conf` file.
2. Configure Restic password and hostname in the .env file
3. Add at least one volume and adjust the **command** in the `docker-compose.yml`
4. (optional) Init Restic-Repository in the pCloud
5. Check configuration

### Init Restic-Repository in the pCloud

There is no container permanent running, if there is no ongoing operation. In the docker-compsoe file is a backup service configured. This service is used to run all other operations like initiation, verification and restore. To initialize a restic repository run the command.

```bash
docker compose run --rm backup restic init
```
With ´--rm´ we will prevent to leave exited containers.  

## Configure Restic

The Restic password for the backup repository is configured in the '.env' to prevent that sensitive information are stored in th.

```
RESTIC_PASSWORD=CHANGEME
```

To verify, that Rclone and Restic are configured correctly, you can run `docker exec -ti pcloudbackup-restic-1 restic stats` and you should get general status information about the Restic repository.

## Check configuration

As Restic is using rclone both tools needs to be configured correctly. To verify the whole configuration you can run.

```bash
docker compose run --rm backup restic stats
```

With a sample output of
```
repository dd516683 opened (version 2, compression level auto)
[0:00] 100.00%  1 / 1 index files loaded
scanning...
Stats in restore-size mode:
     Snapshots processed:  1
        Total File Count:  46
              Total Size:  24.784 MiB
```

### Check Rclone configuration

```bash
docker compose exec restic rclone lsd mypcloud:/
```

Beispiel-Output
```bash
          -1 2023-09-30 05:35:30        -1 Automatic Upload
          -1 2023-12-17 21:08:24        -1 Crypto Folder
          -1 2023-12-17 22:18:18        -1 backup
```

## Run a backup

Run a backup by this command.

```bash
docker compose up
```
