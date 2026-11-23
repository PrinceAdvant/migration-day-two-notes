# Pinning the Node.js version for Nixpacks builds

Nixpacks picks a Node.js version for you, and the default moves over time. A build that worked last month can break after a platform update because a new major version arrived.

Pin it explicitly. Nixpacks reads the `engines` field in `package.json`:

```json
{
  "engines": { "node": "20.x" }
}
```

An `.nvmrc` file works as well, and the `NIXPACKS_NODE_VERSION` environment variable overrides both. Pick one source of truth so local development and builds agree.

Do the same for the package manager. Commit the lockfile, and set the `packageManager` field if you use pnpm or Yarn so the right tool and version are installed.

When builds still differ, run `nixpacks plan .` locally to print the detected providers, packages and commands. It shows exactly what will run, which beats guessing from build logs. The full flow for [Next.js builds with Nixpacks](https://peon.sh/blogs/deploy-next-js-on-peon-with-git-ci-cd-and-nixpacks) uses the same detection.
