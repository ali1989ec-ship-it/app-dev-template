# Web apps — browser-first development

Follow [Start here](START_HERE.md) first. A browser app is a useful default when the user wants a link that works on phones and computers.

## Choose and inspect

Keep an existing project's tools. For a small new app, use Vite with HTML, CSS, and JavaScript. Choose React when the amount of reusable UI and state warrants it. Explain that decision simply; do not require the beginner to select a framework.

Check Node.js and the package manager before installing anything. Use a supported Node release compatible with the current Vite version. Create the app in a new directory, replacing `my-app` with the agreed project name:

```sh
npm create vite@latest my-app -- --template vanilla
cd my-app
npm install
npm run dev
```

For React, choose the appropriate Vite template instead. Inspect the generated files rather than assuming a particular folder layout. Keep the lockfile. Use the URL reported by the development server; the port may differ from examples.

## Add only the storage the app needs

For non-sensitive, single-device preferences or small records, browser storage may be sufficient. Explain that it is tied to the browser and can be cleared. Use a backend such as Supabase when accounts, sharing, or cross-device data are required.

For Supabase, create or use an authorized project, define the data model, and install the client:

```sh
npm install @supabase/supabase-js
```

Record configuration names in `.env.example`, using placeholders:

```dotenv
VITE_SUPABASE_URL=https://YOUR_PROJECT.supabase.co
VITE_SUPABASE_PUBLISHABLE_KEY=YOUR_PUBLIC_KEY
```

Use real values in an ignored local environment file or the deployment service's configuration. Validate missing configuration with a useful message.

```js
import { createClient } from '@supabase/supabase-js'

export const supabase = createClient(
  import.meta.env.VITE_SUPABASE_URL,
  import.meta.env.VITE_SUPABASE_PUBLISHABLE_KEY
)
```

## Protect data at the backend

Supabase publishable keys, and legacy `anon` keys, are intended for client applications. They do not grant unlimited database access. Configure database privileges and Row Level Security (RLS), meaning rules that decide which records each user may read or change. Enable suitable policies before exposing private data; test signed-out access and two different users.

Secret keys, legacy `service_role` keys, database passwords, and private third-party API keys belong only in a trusted backend. Never embed them in web, desktop, or mobile builds. Route privileged operations through a backend that checks the caller's identity and permissions.

Vite includes `VITE_` values in the browser bundle. An environment file or hosting dashboard does not make those values private. Configure `.gitignore` before adding credentials; see [GitHub setup](GITHUB_SETUP.md).

Keep schema and policy changes in versioned migration files when a database is introduced, even if initial setup uses the dashboard.

## Build and verify

Implement the main journey, accessible labels and controls, and loading, empty, and error states. Check mobile and desktop layouts. Validate inputs on the server too when they affect protected data.

For the standard Vite scripts:

```sh
npm run build
npm run preview
```

Inspect `package.json` first; existing projects may use different scripts. Test the built app, persistence, important error cases, and account access boundaries. Run relevant existing tests and add focused tests for important logic.

Add a PWA only if installability or offline behavior is requested. It needs a manifest, suitable icons, HTTPS in deployment, and deliberate cache/update behavior. Test the intended offline journey and confirm new versions reach users; a plugin alone does not prove either works.

Deploy using [the deployment guide](DEPLOYMENT_GUIDE.md), then repeat a short check against the live URL.

## Official references

- [Vite getting started](https://vite.dev/guide/)
- [Vite environment variables](https://vite.dev/guide/env-and-mode)
- [Supabase API keys](https://supabase.com/docs/guides/getting-started/api-keys)
- [Supabase Row Level Security](https://supabase.com/docs/guides/database/postgres/row-level-security)
