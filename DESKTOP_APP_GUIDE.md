# DESKTOP_APP_GUIDE.md — Windows/Mac programs (Electron)

Use **Electron** with **Electron Forge** (not Electron Builder — Forge has an easier, more beginner-friendly setup with fewer config files).

## What to install first

1. **Node.js** (LTS version) — https://nodejs.org — this installs both Node and `npm`, the tool used to install code libraries.
2. Confirm it worked:

   ```sh
   node -v
   npm -v
   ```

   Both should print a version number.
3. **VS Code** as the editor.

## Creating the project

```sh
npm init electron-app@latest my-app -- --template=vite
```

Explain: this creates a working Electron app template using Vite (a fast tool for building the interface), so they get hot-reload (changes show up instantly) out of the box.

```sh
cd my-app
npm start
```

This opens the app as a real desktop window.

## Where the code goes

- `src/` — the interface (HTML/CSS/JavaScript or a framework like React if added later). This is the part that looks like a webpage inside the app window.
- `src/main.js` (sometimes `index.js`) — controls the app window itself: size, menu bar, file access, etc. Changes here need the app restarted.
- Treat it like a website that happens to open in its own window — anything they know from HTML/CSS/JS applies directly.

## Common beginner tasks — quick reference

| They want to... | Do this |
| --- | --- |
| Save data between sessions | Use `electron-store` package (simple key-value storage on disk) |
| Access files on their computer | Use Electron's `dialog` and `fs` modules in `main.js`, not in the interface code |
| Add a menu bar item | Edit the `Menu` template in `main.js` |
| Add a new package | `npm install <package_name>` |
| Use a UI framework (React etc.) | Fine to add, but keep it optional — plain HTML/CSS/JS is enough for a first app |

## Building the installable .exe / .dmg

```sh
npm run make
```

Explain: this produces the installable program. Output appears in the `out/` folder:

- Windows → a `.exe` installer (Squirrel) or a portable `.exe`
- Mac → a `.dmg`
- Linux → a `.deb` or `.rpm`

This is the file they send to someone else to install the app — no coding tools needed on the other end.

### Note on code signing

Unsigned Windows `.exe` files trigger a "Windows protected your PC" warning on first run — this is normal and not a bug. Mention it so they aren't alarmed. Code signing certificates cost money and are only worth it for wide public distribution.

## When stuck

Electron errors show in two places: the terminal (main process errors) and the app's own DevTools console (interface errors — open with `Ctrl+Shift+I` on Windows/Linux, `Cmd+Option+I` on Mac). Check both before diagnosing.
