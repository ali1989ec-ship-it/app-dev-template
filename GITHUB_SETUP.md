# GitHub — save and verify the work

Follow [Start here](START_HERE.md). Git records local history; GitHub stores the commits that have actually been uploaded. Unsaved files and local-only commits are not backed up to GitHub.

## Inspect existing state first

Check the working directory, existing project instructions, repository status, branch, remotes, and available authentication before changing anything. Do not initialize a second repository, replace a remote, or overwrite user changes blindly.

```sh
git --version
gh --version
git status --short
git remote -v
gh auth status
```

Run repository-specific checks only inside a repository. Install missing tools from official sources when needed. If Git is unavailable but GitHub CLI is authenticated, its API commands can still manage repository files; do not claim to have a local Git checkout in that case.

Prefer CLI or API operations for repeated changes. Browser and CLI authentication are separate. For CLI sign-in:

```sh
gh auth login --hostname github.com --git-protocol https --web
```

If user action is needed, provide the current activation link and code with a short explanation. Do not reuse expired codes or ask for passwords or tokens in chat. Verify with `gh auth status` afterward.

## Protect secrets before the first commit

Preserve the framework's generated `.gitignore` and add relevant patterns, for example:

```gitignore
.env
.env.*
!.env.example
node_modules/
build/
dist/
out/
.DS_Store
```

Add framework-specific generated directories and any signing-key or credential files. Keep dependency lockfiles. Commit `.env.example` with placeholder values and documentation, never real secret credentials.

An ignore rule does not remove files already tracked or erase earlier commits. If a real secret has been published, revoke or rotate it first and assess history cleanup separately. Public client keys are different from secret backend keys; see [the web guide](WEB_APP_GUIDE.md#protect-data-at-the-backend).

## Create or connect a repository

Use the repository the user requested for an existing app. For every new app idea, create a separate repository from this template in the user's intended GitHub account, with a descriptive name. Do this during the initial working version; creating only a local Git repository is insufficient. Confirm the owner and name from available context rather than asking for technical choices unnecessarily.

Choose visibility for the intended delivery. GitHub Pages is a public website, including when its source repository is private. GitHub Free normally requires a public repository for Pages; paid plans may allow a private source repository, but the Pages site remains public. If the app is meant to be private, keep the repository private and use a suitable access-controlled preview instead of making it public silently. Never publish secrets, personal data, or private sample content.

For a genuinely new local folder with no Git history:

```sh
git init -b main
```

Inspect Git's author settings. Use an established identity or ask for the preferred one; do not invent an email address. Prefer repository-local configuration over changing global settings unnecessarily.

Review the files, stage the intended paths, and make an initial commit. The following example assumes the only initial file is `README.md`; adapt the file list to the real project:

```sh
git add -- README.md
git diff --cached
git commit -m "Initialize project"
```

For a new public repository intended for a GitHub Pages demo, replace `OWNER/REPO` with the app's actual destination:

```sh
gh repo create OWNER/REPO --public --source=. --remote=origin --push
```

Use `--private` when private source is required; choose a hosting route compatible with that privacy requirement. For an existing repository, inspect its history before connecting or pushing. Prefer cloning a nonempty repository into a separate folder and applying the intended changes there. For an empty destination connected as `origin`, the first push is normally `git push -u origin main`; confirm the branch name first.

## Save meaningful milestones

Review the diff and stage only the intended work. Avoid blindly staging unrelated changes or generated files. Run relevant checks, commit a coherent milestone, then push when GitHub backup is authorized.

If a push is rejected, fetch and inspect the remote changes. Integrate them deliberately and resolve conflicts without discarding work. Do not force-push or run a blind pull as a universal fix. Be aware that a push may trigger an existing deployment workflow.

Verify the remote branch contains the intended commit and return the repository URL before reporting success. If using the Contents API, supply the current file SHA when updating an existing file. For a multi-file revision, prefer one Git tree and commit so the changes arrive together, and update the branch without force. If the branch advanced meanwhile, inspect and rebuild against the new head.

## Continue on another computer

Clone the actual repository, read its README, and restore dependencies using its tools: for example, `npm ci` for an npm project with a lockfile, or `flutter pub get` for Flutter. Restore required configuration securely. Do not assume every project uses npm.

## Official references

- [Git downloads](https://git-scm.com/downloads)
- [GitHub CLI](https://cli.github.com/)
- [CLI authentication](https://cli.github.com/manual/gh_auth_login)
- [Creating repositories](https://cli.github.com/manual/gh_repo_create)
