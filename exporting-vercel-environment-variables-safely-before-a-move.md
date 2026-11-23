# Exporting Vercel environment variables safely before a move

Moving a project off Vercel starts with the environment variables, and there may be three sets of them: Production, Preview and Development.

The CLI can pull each one into a local file:

```bash
vercel env pull .env.production --environment=production
vercel env pull .env.preview --environment=preview
```

Read through the result. Variables named `VERCEL_*` are injected by the platform and will not exist elsewhere, so search your code for them and replace with your own names. Variables used by integrations, such as a database provider, may rotate when the integration is removed, so update the connection string after you switch.

Never commit these files. Load them into your new platform's secret store, then delete the local copies. Remember that `NEXT_PUBLIC_` values are baked in at build time and must be present during the build, not just at runtime. The differences in [self-hosted alternative to Vercel](https://peon.sh/compare/peon-vs-vercel) go beyond environment handling.
