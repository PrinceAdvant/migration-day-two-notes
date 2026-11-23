# Separating staging and production servers under one deploy platform

Running staging and production on the same host is cheap until a load test or a runaway migration takes production down with it. Separate servers fix that, but only if access is separated too.

Put each environment on its own server, with its own database and its own secrets. Staging should never hold production credentials, even read only ones.

In the deployment platform, map roles to environments. Most engineers can deploy to staging freely. Production deploys are limited to a smaller group or require an approval, and every action is recorded.

Promote builds rather than rebuilding them: the image tested in staging is the image that goes to production, identified by its tag or digest. Rebuilding for production reintroduces the chance of differences.

Finally, make the two environments look different in the dashboard so nobody confuses them under pressure. The features that support this are listed on [self-hosted deployment for larger organisations](https://peon.sh/solutions/enterprise).
