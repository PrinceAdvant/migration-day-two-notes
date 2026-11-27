# Checking how a Docker control panel stores your secrets before you commit

Every Docker control panel stores your environment variables, registry passwords and SSH keys somewhere. Before you put production secrets into one, find out where and how, because leaving the panel later or recovering from a breach depends on it.

Questions to answer during a trial:

- Where are secrets stored: a database on the same server, files on disk, or the panel's cloud service?
- Are they encrypted at rest, and where does the encryption key live? A key on the same disk only helps against some threats.
- Who can read them in the UI? Can a developer role see values, or only names?
- Are secret values written to build logs or shown in deploy output?
- Can you export them in a standard format, such as a `.env` file, when you migrate?
- Is there an audit log of who viewed or changed a secret?

Test the last two yourself: add a dummy secret, run a build that echoes environment variables, and check the logs; then try an export.

Also check how the panel reaches your servers. An SSH key held by the panel is effectively root on every connected server, so protect the panel's admin accounts with strong passwords and two factor login. A wider comparison of two panels is in [EasyPanel compared with Peon](https://peon.sh/blogs/peon-vs-easypanel).
