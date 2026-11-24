# Planning disk space on a server that builds, stores images and runs databases

A single server that runs a deploy platform does three disk hungry jobs at once: it builds images, keeps old images for rollback, and stores database data. Each grows at its own pace, and the server only notices when the disk is full and Postgres refuses writes.

Measure each part separately. `docker system df` shows images, containers, volumes and build cache. The build cache is often the biggest surprise, since every build adds layers that nothing removes automatically.

Then set budgets. Keep a fixed number of old image tags per app, enough for rollback and no more. Prune build cache older than a week on a schedule with `docker builder prune --filter until=168h`. Watch volume growth weekly and plan storage for the database a year ahead.

Alert at 80 percent disk use, not 95. At 95 percent you are already in an incident.

If databases grow quickly, move their volumes to a separate block storage disk so a runaway build cannot fill the database disk. Handling builds, image retention and cleanup is part of what [self-hosted platform as a service](https://peon.sh/solutions/self-hosted-paas) should do for you.
