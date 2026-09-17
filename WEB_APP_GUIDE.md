# WEB_APP_GUIDE.md — Websites & PWAs (Vercel + Supabase)

Use plain **HTML/CSS/JavaScript** (or React via Vite if the app grows), a **Supabase** database if data needs to be saved online, and **Vercel** to host it live on the internet with a real URL.

## What to install first

1. **Node.js** (LTS) — https://nodejs.org
2. Confirm: `node -v` and `npm -v` both print a version.
3. **VS Code** as the editor.

## Creating the project

```sh
npm create vite@latest my-app -- --template vanilla
cd my-app
npm install
npm run dev
```

Explain: this creates a small website project and starts a local preview — they'll get a link like `http://localhost:5173` to open in a browser and see live changes as code is edited.

(If they want it to feel like an installable app on phones — a **PWA** — add the `vite-plugin-pwa` package later; don't front-load this, get the basic site working first.)

## Where the code goes

- `index.html` — the page structure.
- `style.css` (or `src/style.css`) — appearance.
- `main.js` (or `src/main.js`) — behaviour/interactivity.

## Adding a database (Supabase)

Use Supabase when the app needs to remember data between visits or across devices (accounts, saved items, etc.).

1. Create a free project at https://supabase.com (sign up, "New Project").
2. In the Supabase dashboard, go to **Project Settings → API** and copy the **Project URL** and **anon public key**.
3. Install the client library:

   ```sh
   npm install @supabase/supabase-js
   ```

4. In code:

   ```js
   import { createClient } from '@supabase/supabase-js'
   const supabase = createClient('YOUR_PROJECT_URL', 'YOUR_ANON_KEY')
   ```

5. Use the Supabase dashboard's **Table Editor** to create tables visually (no SQL needed for a beginner's first table).
6. **Never put the keys in a public GitHub repo as plain text long-term** — once it's working, move them into a `.env` file and add `.env` to `.gitignore` (see `GITHUB_SETUP.md`).

## Deploying live with Vercel

```sh
npm install -g vercel
vercel login
vercel
```

Explain: `vercel` asks a few yes/no questions (accept the defaults), then gives a live URL within seconds. Every time they run `vercel --prod`, that URL updates with the latest version.

Better long-term setup: connect the GitHub repo to Vercel at https://vercel.com/new — once connected, every `git push` automatically deploys, with no manual `vercel` command needed. Set this up once the app is past its first working version.

## Common beginner tasks — quick reference

| They want to... | Do this |
| --- | --- |
| Add a new page | Create a new `.html` file, link it from the nav |
| Store login/signup | Use Supabase Auth (`supabase.auth.signUp`, `.signInWithPassword`) |
| Make it installable on phones | Add `vite-plugin-pwa`, generate icons, done automatically |
| Style it quickly | Use a simple CSS framework like Pico.css via a CDN link — no build step needed |

## When stuck

Browser errors show in DevTools Console (`F12` or right-click → Inspect → Console). Read the first red error line back in plain English before suggesting a fix. Deployment errors show directly in the terminal after running `vercel`.
