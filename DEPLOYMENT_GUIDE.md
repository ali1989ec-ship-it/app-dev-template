# Deployment — deliver and verify a usable result

Follow [Start here](START_HERE.md) and the chosen platform guide. A local preview, a hosted preview, and a public production release are different outcomes. Establish which the user needs and act within that authorization.

Prepare a working build first. Ask only for account access, cost, or release decisions that genuinely require user involvement; do not repeatedly reconfirm already authorized work.

## Before sharing

Run the relevant checks and exercise the main journey. Review configuration, data access rules, and any sensitive sample data. Record the source revision, required environment-variable names, and a practical way to return to the previous working version. A code rollback does not automatically reverse database changes, so plan those separately.

## Web apps

Use existing hosting when available. Vercel is a default option for a new compatible web app, not a requirement to migrate an existing project.

For a standard Vite app, build and inspect the production output first:

```sh
npm run build
npm run preview
```

Use an existing Vercel CLI or install it from the official source if needed. Authenticate only when necessary:

```sh
vercel login
vercel
```

Inspect the selected account, project, framework, build command, and output directory. Do not accept defaults blindly or link to the wrong project. The normal Vite output is `dist`, unless configured otherwise. A normal `vercel` deployment creates a preview; production uses:

```sh
vercel --prod
```

Use that command when a production release is authorized. Alternatively, connect the intended GitHub repository and configure its production branch. Explain that pushes to that branch can publish changes automatically.

Set required configuration for the correct preview or production environment and redeploy when build-time values change. Values bundled into client code remain public even if entered in the hosting dashboard. Store privileged keys in backend-only configuration.

Open the actual deployed URL. Test the main journey, refresh on nested routes if applicable, persistence, sign-in callbacks, and relevant access rules. Record the working URL and any access restrictions. Check service limits and current pricing before enabling paid features.

## Supabase database changes

Use the dashboard for simple inspection and the CLI when versioned migrations or local development are useful. Do not install the Supabase CLI globally with npm. A supported project-local installation is:

```sh
npm install --save-dev supabase
npx supabase login
npx supabase init
npx supabase link --project-ref YOUR_PROJECT_REF
```

Replace the project reference with the intended project. Inspect existing configuration before initializing or linking. Check current Node and container-runtime requirements if local Supabase services are needed; do not add Docker merely to inspect a hosted database.

Store schema and policy changes in migration files. Review and test them against an appropriate development environment before applying them to production. Keep access policies and required configuration aligned with the deployed app. Verify migration results and protect existing data.

## Desktop apps

Use the platform-specific makers described in [the desktop guide](DESKTOP_APP_GUIDE.md). Build and test the actual installer on its target OS and architecture. For public distribution, address signing, notarization where applicable, release notes, and updates.

Publish only the intended tested artifacts to an authorized destination such as GitHub Releases. Prefer explicit file paths over broad globs that could upload unrelated output. Check release visibility and download access, then verify the downloadable file is the expected artifact.

## Mobile apps

Follow [the mobile guide](MOBILE_APP_GUIDE.md) for release signing and builds. Choose the appropriate route: Android device testing, Play testing tracks, iOS TestFlight, or a store release. A compiled file is not proof that installation, review, or publication succeeded.

Check current developer-account, testing, privacy, and store-submission requirements. Prepare the package and listing before any final user action. Distinguish uploaded, processing, under review, available to testers, and publicly released states in progress reports.

## Final handoff

Provide the live URL or exact artifact, supported platforms, what was tested, and any remaining limitations. Update the project's README with repeatable run, test, and release instructions. Verify the remote source revision and the delivery itself; report partial completion honestly when a service or user action is still pending.

## Official references

- [Vercel CLI deploy](https://vercel.com/docs/cli/deploy)
- [Vercel Git integration](https://vercel.com/docs/git)
- [Supabase CLI setup](https://supabase.com/docs/guides/local-development/cli/getting-started)
- [Supabase database migrations](https://supabase.com/docs/guides/deployment/database-migrations)
- [GitHub CLI releases](https://cli.github.com/manual/gh_release_create)
