# Shipping container logs off the server with a small Vector config

Logs that only live on the server vanish with it, and grepping across several containers over SSH gets old quickly. Vector is a small agent that can read Docker logs and send them elsewhere.

A minimal config reads every container and forwards to an HTTP endpoint or object storage:

```toml
[sources.docker]
type = "docker_logs"

[sinks.out]
type = "http"
inputs = ["docker"]
uri = "https://logs.example.com/ingest"
encoding.codec = "json"
```

Run it as a container with the Docker socket mounted read only. Remember the socket gives broad access, so keep the image pinned and updated.

Keep the local json-file driver with rotation enabled too, so `docker logs` still works when the remote end is down:

```yaml
logging:
  driver: json-file
  options: {max-size: "10m", max-file: "3"}
```

Have your apps log JSON to stdout and you get searchable fields for free. The wider picture is in [handling Docker logs in production](https://peon.sh/blogs/handle-docker-logs-production).
