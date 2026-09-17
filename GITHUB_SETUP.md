# GITHUB_SETUP.md — Saving your project online with GitHub

GitHub is where the project's code is backed up and its history is kept, so nothing is ever lost. Do this once at the start of every new project.

## One-time setup (only needed the very first time)

1. Create a free account at https://github.com if they don't have one.
2. Install **Git**: https://git-scm.com/downloads
3. Confirm it worked:

   ```sh
   git --version
   ```

4. Set their name/email (used to label their changes):

   ```sh
   git config --global user.name "Their Name"
   git config --global user.email "their@email.com"
   ```

5. Install **GitHub CLI** (`gh`) — lets you create repos from the terminal without opening a browser: https://cli.github.com
6. Log in:

   ```sh
   gh auth login
   ```

   Follow the on-screen prompts (choose GitHub.com, HTTPS, log in via browser — it's the simplest option).

## Creating the repository for a new project

From inside the project folder (e.g. `my-app`):

```sh
git init
gh repo create my-app --private --source=. --remote=origin
```

Explain:

- `git init` starts tracking changes in this folder.
- `gh repo create` makes a new repository on their GitHub account and connects this folder to it. `--private` keeps it hidden from the public — change to `--public` if they want it visible to anyone.

## Before the first commit — protect secrets

If the project has any API keys or passwords (e.g. Supabase keys), create a file called `.gitignore` in the project root containing:

```gitignore
.env
node_modules/
build/
dist/
```

This stops those files from ever being uploaded to GitHub.

## Saving changes (do this often — after every working change)

```sh
git add .
git commit -m "Describe what changed, e.g. added login screen"
git push
```

Explain each step in one line:

- `git add .` — selects all changed files to save.
- `git commit -m "..."` — saves a labelled snapshot.
- `git push` — uploads it to GitHub.

## Cloning the project onto another computer (e.g. your PC)

```sh
git clone https://github.com/USERNAME/my-app.git
cd my-app
npm install
```

Explain: this downloads a full copy of the project, ready to run.

## Simple rules to follow

1. Commit and push after every change that works — small, frequent commits, not one giant commit at the end.
2. Never commit `.env` files, passwords, or API keys.
3. If `git push` is rejected, it usually means the GitHub copy has changes the local copy doesn't — run `git pull` first, then `git push` again.
