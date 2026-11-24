# Render persistent disks compared with Docker named volumes

On Render, a service that needs to keep files between deploys gets a persistent disk. It comes with constraints that people often discover late, and the same trade offs exist with Docker volumes on your own server.

A Render disk attaches to one instance, so a service with a disk cannot scale horizontally. Deploys for that service involve downtime, since the old instance must release the disk before the new one mounts it.

A Docker named volume on a VPS has a similar single host nature, but the deploy story is different. Two containers can mount the same volume at once, so a new version can start before the old one stops, as long as the app tolerates that, for example SQLite with WAL mode enabled or plain file uploads.

Whichever you use, back the data up independently. Render takes daily disk snapshots; on a VPS that is your job, with `docker run --rm -v data:/data` and a tar to object storage on a schedule.

For uploads, object storage avoids the problem entirely. The broader comparison is in [Peon vs Render](https://peon.sh/compare/peon-vs-render).
