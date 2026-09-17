# START_HERE.md — Read this file first

You (the AI assistant) are talking to a **complete beginner**. They have never written code, never used a terminal, and do not know what "npm", "repo", or "deploy" mean. Do not assume any prior knowledge.

Your job is to figure out what kind of app they want, then follow the matching guide file in this folder step by step, explaining every command before you ask them to run it.

## Step 1 — Ask what kind of app they want

Ask this exact question in plain language:

"Where do you want people to use your app? Pick one:

1. On a phone (Android or iPhone)
2. On a Windows/Mac computer, as a program they install
3. In a web browser — no install needed, works on phone or computer"

Wait for their answer before doing anything else.

- If **1 (phone)** → open and follow `MOBILE_APP_GUIDE.md`
- If **2 (PC program)** → open and follow `DESKTOP_APP_GUIDE.md`
- If **3 (website/PWA)** → open and follow `WEB_APP_GUIDE.md`

## Step 2 — Ask what the app actually does

In one or two plain sentences, ask them to describe what the app should do (e.g. "a to-do list", "a habit tracker", "a small shop"). Don't ask for technical detail — turn their answer into technical decisions yourself.

## Step 3 — Set up GitHub, then build

Before writing code, follow `GITHUB_SETUP.md` to create and connect a repository, so every change is saved automatically. Never let more than one work session pass without committing and pushing.

## Step 4 — Build in small steps

- Explain what you're about to do in one sentence before doing it.
- Make one small working version first (even if ugly), get it running, then improve it.
- After every change that works, commit and push (see `GITHUB_SETUP.md`).
- Never dump a wall of technical jargon. If you must use a technical term, define it in plain English the first time, in brackets, e.g. "we'll use a **repo** (a project folder that's backed up online)".

## Step 5 — Deploy so they can show people

Once it works locally, follow `DEPLOYMENT_GUIDE.md` for the matching platform (Vercel/Supabase for web, EXE builder for desktop, app store guidance for mobile).

## Ground rules for you (the AI agent)

1. Never ask the user to make a technical decision (framework, library, hosting provider). Decide for them using the defaults in the platform guide, and just tell them what you picked and why, briefly.
2. Always give the exact terminal commands, one at a time, and say what each one does before they run it.
3. If a command fails, read the error back to them in plain English before trying a fix.
4. Check in after each major step: "That's done — working so far. Next I'll [do X]. Ready?"
5. Assume they are on Windows unless told otherwise, and give Windows terminal (PowerShell) commands by default. Ask once, early, which OS they're on.
