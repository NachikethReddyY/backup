cover:
- Branches
- remotes
- conflicts

# Branches
A branch is an independent version of a repository. Git enables parallel development using branches so you can safely work on features, fixes, and experiments without impacting the main line.

## Branch management
- `git branch` - list local branches.
- `git branch <name>` - create a new branch.
- `git branch -m <old> <new>` - rename a branch.
- `git branch -d <name>` - delete a branch (safe delete, branch must be merged).

- `git switch <name>` - switch to an existing branch.
- `git switch -c <name>` - create and switch to a new branch.

## Inspect changes
- `git diff main summary-statistics` - show diff between `main` and `summary-statistics`.

## Merging branches
1. Checkout the target branch (where changes should land): `git switch <target>`.
2. Merge from the source branch: `git merge <source>`.

Alternative form for a fast merge:
- `git merge <source> <destination>` (less common if you’re already on destination).

# Remotes
Remote repositories let you collaborate and store backups.

- `git clone <path-to-repo> <new-repo>` - clone a repository locally.
- `git remote` - list remote names.
- `git remote -v` - list remote URLs.

### Add and rename remotes
- `git remote add <name> <url>` - add a new remote. Example: `git remote add back-up /home/repl/datacamp`.

### Fetch and sync
- `git fetch` - fetch updates from all remotes.
- `git fetch origin main` - fetch the `main` branch from the `origin` remote.
- `git merge origin/main` - merge fetched remote branch into current branch.
- `git pull` - shorthand for `git fetch` + `git merge` (current branch).

> Note: `git merge origin` is not common; usually merge a branch ref like `origin/main`.

---

## Quick glossary
- Branch: independent history line, e.g. `feature-x`.
- Remote: named URL of a remote repo, e.g. `origin`, `back-up`.
- Fetch: download remote commits.
- Pull: fetch + merge in one command.

