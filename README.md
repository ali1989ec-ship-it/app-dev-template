# AI App Starter Kit

Always make a new github repo for each project idea i have.

Turn an app idea into a working project with an AI assistant, without needing to know the technical setup first.

These guides tell the assistant how to inspect your computer, choose suitable tools, build a small first version, test it, save the work, and help you share it. This repository contains instructions, not a runnable app or preinstalled development tools.

## Start here

Give your assistant access to this repository and paste:

> Read START_HERE.md and the relevant guides in this repository. I want to build [describe your idea] for [web, desktop, or phone — or help me choose]. Inspect the available tools and existing files first. Create a separate GitHub repository for this app idea, commit and push its source, and give me its repository link. For a web app, put a working version online and give me the live link; use GitHub Pages for a static app when it fits. Handle the technical work you can perform yourself, explain progress in plain English, and ask me only for missing product decisions, sign-ins, or actions that need my involvement. Build and verify a small working version first.

If your assistant cannot open repository links, download the repository using **Code → Download ZIP** and attach the Markdown files, or open the extracted folder in your coding assistant.

Each new app idea gets its own project folder and GitHub repository. The assistant should create them as part of the work, then return both the repository URL and, for web apps, a verified live URL. Keep this repository as the reusable guide collection. Copy the guides into a project if helpful; do not put the app's code back into this template repository.

## Guide map

| Guide | Purpose |
| --- | --- |
| [Start here](START_HERE.md) | How the assistant should work, choose a platform, and judge completion |
| [Web apps](WEB_APP_GUIDE.md) | Browser apps, optional online data, and client/server boundaries |
| [Desktop apps](DESKTOP_APP_GUIDE.md) | Installable Electron apps and platform-specific packaging |
| [Mobile apps](MOBILE_APP_GUIDE.md) | Flutter apps, device testing, and mobile build requirements |
| [GitHub setup](GITHUB_SETUP.md) | Save work safely, authenticate, commit, and verify uploads |
| [Deployment](DEPLOYMENT_GUIDE.md) | Share a tested website or installer and verify the result |

## What to expect

The assistant should do routine setup, editing, debugging, and checks when its tools allow. You provide the idea and feedback, and complete account sign-ins when needed. You should not have to choose libraries or copy a long list of commands.

The default starting points are Vite for web apps, Electron Forge for desktop apps, and Flutter for mobile apps. Supabase is optional for shared online data. GitHub Pages hosts static web apps; Vercel is one option for apps that need a server. Existing project choices and your preferences take priority.

A useful first delivery includes a working main user journey, evidence of testing, a repository link, a live web link or installable build you can open, clear limitations, and saved source files. A live deployment or GitHub upload is only complete once it has been verified. GitHub Pages works for static browser apps; apps that need a server require another host for that server.

## Scope and maintenance

These are practical starting points, not a guarantee that every app needs the same tools. Commands are examples for new projects; the assistant must adapt names, paths, versions, and operating-system requirements. Service pricing, store requirements, and tooling change, so check the official links in each guide when using them.

Adapted from the [original AI App Starter Kit artifact](https://claude.ai/artifact/Ke8VxzyHGfUZsmGNW91xd8), with revised workflow, security, testing, and release guidance.
