# Auto-stop machines and cold starts compared with an always-on VPS

Fly.io can stop machines when they are idle and start them on the next request. For side projects it keeps the bill near zero. For anything users touch every day, the cold start is the price.

Measure it before deciding. Stop the machine, request the slowest page, and time the response. A small Node or Go service may wake in well under a second. A Rails or Django app that loads a large framework and opens database connections can take several seconds.

An always-on VPS has no cold start but bills every hour. Compare the monthly total of your machines with auto stop disabled against a VPS that runs everything. If the always-on number is close, the predictable latency is usually worth it.

Keep auto stop for preview apps and internal tools that sit idle most of the day. The full comparison is in [Fly.io alternatives](https://peon.sh/blogs/fly-io-alternative).
