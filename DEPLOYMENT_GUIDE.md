# Deployment — deliver and verify a usable result

Follow [Start here](START_HERE.md) and the chosen platform guide. For each new idea, create and push its own repository. A web app should also have a working live URL by default. A local preview alone does not meet that goal.

Prepare a working build first. Ask only for account access, cost, or release decisions that genuinely require user involvement; do not repeatedly reconfirm already authorized work.

## Before sharing

Run the relevant checks and exercise the main journey. Review configuration, data access rules, and any sensitive sample data. Record the source revision, required environment-variable names, and a practical way to return to the previous working version. A code rollback does not automatically reverse database changes, so plan those separately.

## Web apps

Use existing hosting when available. For a new static browser app, publish from its own GitHub repository with GitHub Pages and GitHub Actions. GitHub Pages serves static HTML, CSS, and JavaScript; it does not run an application server. A browser app may call a separately hosted service such as Supabase, provided its access rules are configured. Use another suitable host, such as Vercel, when the app needs server-side functions or GitHub Pages is unavailable.

For a standard Vite app, build and inspect the production output first:

```sh
npm run build
npm run preview
```

### GitHub Pages for a static Vite app

1. Confirm this app's repository exists and its source has been pushed. Check that its visibility and the GitHub account's plan support Pages. Pages sites are publicly reachable, even when a plan permits a private source repository. Do not publish private data or silently change repository visibility.
2. For a repository at `https://github.com/OWNER/REPO`, configure Vite's `base` as `/REPO/` so scripts and styles load from `https://OWNER.github.io/REPO/`. For a user site at `OWNER.github.io` or a custom domain, use `/`. Adapt this to the actual app and routing; test direct navigation and refresh.
3. In **Settings → Pages**, choose **GitHub Actions** as the build and deployment source. The assistant should perform this through an available CLI, API, or browser session rather than merely tell the user where the setting is.
4. Add `.github/workflows/deploy.yml` in **the app repository**, not this guide repository. For a standard npm/Vite app with `package-lock.json`, use this as a starting point and check current action versions before committing:

   ```yaml
   name: Deploy to GitHub Pages
   on:
     push:
       branches: [main]
     workflow_dispatch:
   permissions:
     contents: read
     pages: write
     id-token: write
   concurrency:
     group: pages
     cancel-in-progress: true
   jobs:
     deploy:
       runs-on: ubuntu-latest
       environment:
         name: github-pages
         url: ${{ steps.deployment.outputs.page_url }}
       steps:
         - uses: actions/checkout@v7
         - uses: actions/setup-node@v7
           with:
             node-version: '24'
             cache: npm
         - run: npm ci
         - run: npm run build
         - uses: actions/configure-pages@v6
         - uses: actions/upload-pages-artifact@v5
           with:
             path: dist
         - id: deployment
           uses: actions/deploy-pages@v5
   ```

   Change the branch, commands, output folder, and action versions to match the actual project and current official guidance. Set required public build variables in the workflow or repository settings; never put server secrets into the static bundle.
   If the web app lives in a subfolder such as `app/`, the example above will fail as written. Add `defaults: { run: { working-directory: app } }` under the job, set `actions/setup-node`'s `cache-dependency-path` to `app/package-lock.json`, and set the upload artifact `path` to `app/dist`. The workflow file still belongs at the repository root under `.github/workflows/`. Check the actual package and output paths before pushing.
5. Push the workflow, inspect the Actions run, and resolve any failure. Open the Pages URL and test the real app, including assets, navigation, refresh, saving, and sign-in if applicable. Record the verified URL in the app's README and return it with the repository URL. Future pushes to the configured branch should redeploy; verify that at least the first deployment succeeds.

For a plain HTML/CSS/JavaScript app with no build, use a Pages source or workflow suited to those static files. Do not add Vite just to publish it.

### Apps that need a server

Choose a host that can run the needed backend. Vercel is one option for compatible apps. Keep the app in its separate GitHub repository and connect that repository to the hosting project when practical. Use an existing Vercel CLI or install it from the official source if needed. Authenticate only when necessary:

```sh
vercel login
vercel
```

Inspect the selected account, project, framework, build command, and output directory. Do not accept defaults blindly or link to the wrong project. The normal Vite output is `dist`, unless configured otherwise. A normal `vercel` deployment creates a preview; production uses:

```sh
vercel --prod
```

Use that command when a production release is authorized. Alternatively, connect the intended GitHub repository and configure its production branch. Explain that pushes to that branch can publish changes automatically. If the frontend uses Pages and the backend is elsewhere, deploy and verify both pieces and configure the correct backend URL.

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

Provide the separate app repository URL and the live web URL or exact native artifact, supported platforms, what was tested, and any remaining limitations. Update the project's README with repeatable run, test, and release instructions. Verify that the remote branch contains the final source commit, that the deployment workflow succeeded, and that the live URL opens and completes the main journey. A localhost link, an Actions run that has only started, or a predicted Pages URL is not a verified delivery. If publishing is blocked, state the exact blocker and report partial completion honestly rather than calling the app done.

## Official references

- [Vite deployment to GitHub Pages](https://vite.dev/guide/static-deploy#github-pages)
- [GitHub Pages publishing sources](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)
- [What GitHub Pages hosts](https://docs.github.com/en/pages/getting-started-with-github-pages/what-is-github-pages)
- [Vercel CLI deploy](https://vercel.com/docs/cli/deploy)
- [Vercel Git integration](https://vercel.com/docs/git)
- [Supabase CLI setup](https://supabase.com/docs/guides/local-development/cli/getting-started)
- [Supabase database migrations](https://supabase.com/docs/guides/deployment/database-migrations)
- [GitHub CLI releases](https://cli.github.com/manual/gh_release_create)
