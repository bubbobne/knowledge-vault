# Git issue: remote branch exists but `origin/dev` not found

## Problem

The remote repository contains a branch `dev`, verified with:

```bash
git ls-remote --heads origin
```

Output:

```
670b975870485f20dc6d793f922848b2382df294  refs/heads/dev
be714f052262f6b7bc080492f24dd8e3a9ab410d  refs/heads/main
```

However, locally the branch was not available:

```bash
git branch -r
```

Output: *(empty)*

Attempting to create the branch failed:

```bash
git switch -c dev origin/dev
```

Error:

```
fatal: invalid reference: origin/dev
```

## Diagnosis

The remote configuration was fetching only the `main` branch.

Verification:

```bash
git remote show origin
```

Output:

```
Remote branch:
  main tracked
```

The fetch refspec was missing or restricted:

```bash
git config --get-all remote.origin.fetch
```

Output: *(empty)*

Therefore `git fetch` did not create remote-tracking branches such as `origin/dev`.

## Solution

Restore the standard fetch refspec and fetch again:

```bash
git config remote.origin.fetch "+refs/heads/*:refs/remotes/origin/*"
git fetch origin --prune
```

Now the remote branches are visible:

```bash
git branch -r
```

Output:

```
origin/dev
origin/main
```

Create the local branch tracking the remote one:

```bash
git switch -c dev origin/dev
```

Result:

```
branch 'dev' set up to track 'origin/dev'
Switched to a new branch 'dev'
```

## Key point

`git ls-remote` queries the remote repository directly, while `git fetch` only creates local remote-tracking branches according to the configured `fetch refspec`.  
If the refspec is restricted, some remote branches will not appear locally.
