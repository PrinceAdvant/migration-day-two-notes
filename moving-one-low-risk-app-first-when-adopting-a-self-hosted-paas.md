# Moving one low risk app first when adopting a self-hosted PaaS

Teams adopting a self-hosted platform often start by planning the migration of everything. A better first step is to move one app end to end and learn from it. Pick it with a few rules.

Choose an app that has real traffic but low stakes: an internal dashboard, a docs site, or a marketing page. It should have a working health endpoint and no stateful data, or only a small database you can dump and restore in minutes. Avoid anything with payments, heavy background jobs or an unusual build.

Then run it for two weeks and write down everything that surprised you. Typical notes: the build needed a missing system package, logs were harder to find than expected, the domain took a while because DNS TTLs were high, or nobody knew who should get deploy alerts. Each note becomes a checklist item for the next app.

Measure two things during the trial: time from merge to live, and time to recover from a failed deploy. If both are at least as good as on the old platform, move the next three apps. If not, fix the process before moving more. This approach keeps the risk small while you evaluate an [an open-source self-hosted PaaS](https://peon.sh/solutions/self-hosted-paas) against your current setup.
