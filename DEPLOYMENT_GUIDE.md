# DEPLOYMENT_GUIDE.md — Getting the app in front of real people

Which section to use depends on which guide they followed:

## If they followed WEB_APP_GUIDE.md → Vercel + Supabase

**Vercel (hosting the website):**

```sh
npm install -g vercel
vercel login
vercel
```

- First run asks a few questions — accept the defaults by pressing Enter.
- It prints a live URL immediately (e.g. `my-app-abc123.vercel.app`).
- To push a new live version after changes: `vercel --prod`
- Best long-term setup: go to https://vercel.com/new, sign in with GitHub, and import the repo — after that, every `git push` deploys automatically and no manual command is needed.

**Supabase CLI (optional — only if managing the database from the terminal rather than the dashboard):**

```sh
npm install -g supabase
supabase login
supabase init
supabase link --project-ref YOUR_PROJECT_REF
```

- `YOUR_PROJECT_REF` is found in the Supabase dashboard URL for the project.
- Most beginners can manage tables fine from the Supabase website dashboard and never need the CLI — only introduce this if they want to track database changes in Git alongside their code.

**Environment variables on Vercel:** once the app uses Supabase keys, add them in the Vercel dashboard under **Project → Settings → Environment Variables** — this keeps them out of the public GitHub repo entirely.

## If they followed DESKTOP_APP_GUIDE.md → sharing the .exe/.dmg

There's no "deploy" step — the built file itself is the deliverable.

```sh
npm run make
```

- Find the installer in the `out/` folder.
- Share it via GitHub Releases (`gh release create v1.0.0 out/**/*.exe`), a cloud drive link, or a file-sharing service — whichever is easiest for them.
- Remind them: Windows will show an "unrecognised app" warning for unsigned installers. This is expected and does not mean something is broken.

## If they followed MOBILE_APP_GUIDE.md → sharing the app

- **Android, quick sharing:** send the `.apk` file directly (from `flutter build apk --release`) — the other person needs to allow "install from unknown sources" once.
- **Android, proper store listing:** requires a one-off $25 Google Play Developer account, then upload the `.aab` file via the Play Console.
- **iPhone:** requires a Mac + a $99/year Apple Developer account, and submission through App Store Connect. Flag this as the one path with real cost and Apple-only tooling — there's no shortcut around it.

## General rule

Get it working and shareable in the cheapest, simplest way first (a raw `.apk`, a Vercel preview link, an unsigned `.exe`). Only go through app stores or paid accounts once they're sure they want to distribute it properly.
