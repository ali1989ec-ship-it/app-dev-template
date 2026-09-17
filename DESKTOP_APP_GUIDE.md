# Desktop apps — Electron and Electron Forge

Follow [Start here](START_HERE.md) first. Use an installed desktop app when desktop integration, file access, or the user's preference justifies it. Keep an existing project's stack.

## Set up the project

For a new Electron app, Electron Forge provides a starting point and packaging tools. Check the OS, Node.js, package manager, and current Forge requirements first. In a new directory:

```sh
npm init electron-app@latest my-app -- --template=vite
cd my-app
npm start
```

Replace `my-app` with the project name. Inspect the generated configuration and entry points; template layouts can change. Verify that the application window opens before building more features.

## Keep responsibilities clear

- The **main process** manages windows and privileged desktop operations.
- The **renderer** draws the interface and handles user interaction.
- A **preload bridge** exposes specific, limited operations between them.

Keep context isolation enabled and Node integration disabled in the renderer. Retain sandboxing where supported. Do not expose unrestricted filesystem access or generic command execution through the bridge. Validate IPC requests, their sender, and inputs in the main process. Restrict navigation and external links to appropriate destinations.

Use native dialogs for file selection. Keep file operations in the privileged process and handle cancellation, missing files, and permission failures clearly. Store ordinary settings under the app's user-data location, not inside its installation directory. Use appropriate OS-backed credential storage for tokens rather than treating a settings file as a secret vault.

Do not ship backend secrets in the executable. Packaged application code can be inspected.

## Verify the app and its package

Test the main journey, keyboard use, resizing, saved state after restart, and relevant file-operation failures. Check both main-process logs and renderer errors. Run meaningful automated checks supported by the project.

For a Forge project, inspect the configured makers, then run:

```sh
npm run make
```

A **maker** determines the output format. An `.exe`, `.dmg`, `.zip`, `.deb`, or `.rpm` is only produced when the corresponding maker and its prerequisites are configured. A macOS build does not automatically create a Windows installer. Use suitable machines or CI runners for each target OS and architecture.

Find the actual artifacts under `out/` and test installation, launch, persistence, and uninstallation on the target platform. Report any target you could not test.

## Distribution

Development builds and public releases have different requirements. For public distribution, plan platform-appropriate signing, macOS notarization, and an update strategy. Check current vendor requirements and costs before purchasing anything.

An unsigned-app warning is a distribution limitation, not proof that a file is safe. Do not instruct users to disable OS security protections as a routine fix.

Follow [deployment](DEPLOYMENT_GUIDE.md) to publish an authorized release with the exact tested installer and clear platform requirements.

## Official references

- [Electron Forge](https://www.electronforge.io/)
- [Forge makers](https://www.electronforge.io/config/makers)
- [Forge build lifecycle](https://www.electronforge.io/core-concepts/build-lifecycle)
- [Electron security](https://www.electronjs.org/docs/latest/tutorial/security)
- [Electron context isolation](https://www.electronjs.org/docs/latest/tutorial/context-isolation)
