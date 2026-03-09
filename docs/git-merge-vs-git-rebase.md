# Git Merge vs Git Rebase — A Practical Lesson

## 1. The Core Concept

Both commands integrate changes from one branch into another, but in different directions and for different purposes.

> **merge** = integrate your work **into** the product (feature → main)
> **rebase** = integrate the product's updates **into** your work (main → feature)

```
rebase: main → your feature (you catch up)
merge: your feature → main (you ship)
```

---

## 2. Understanding the Three Layers

There are 3 things, not 2:

| Name | Where | Description |
|---|---|---|
| Remote branch | On GitHub server | The real `main` on GitHub, always latest |
| Remote tracking branch | On your local machine | `origin/main` — a local cached copy of GitHub's `main` |
| Local branch | On your local machine | Your `main`, `feature`, etc. |

### `origin/main` is a local cache, not GitHub itself

`origin/main` lives on **your machine** inside `.git/refs/remotes/origin/main`. It is a read-only, cached representation of what GitHub looked like the last time you fetched.

```
GitHub (real): main → A-B-C-D
↑
git fetch (refresh cache)
↓
Your machine: origin/main → A-B-C-D (cache, read-only)
main → A-B (your local branch, untouched)
```

**Analogy:** Think of it like a news app on your phone.
- GitHub = the actual news server
- `origin/main` = news cached on your phone
- `git fetch` = hitting refresh to get latest news

### What `git fetch` does (and does NOT do)

| Command | What it updates |
|---|---|
| `git fetch` | Only `origin/*` (remote tracking branches) |
| `git pull` | `fetch` + auto-merges into your current local branch |

`git fetch` is "safe" — it never touches your local branches or working files.

```
After git fetch:

origin/main → updated ✓
origin/dev → updated ✓

local main → unchanged ✗
local dev → unchanged ✗
```

---

## 3. Git Merge

Combines histories by creating a new merge commit.

```bash
git checkout feature
git merge main
```

```
main: A - B - C --------\
\ \
feature: D - E - [M] <- merge commit
```

- History is preserved as-is
- Creates an extra merge commit `[M]`
- Safe for shared/public branches
- Used when **shipping** (feature → main), typically via PR on GitHub

---

## 4. Git Rebase

Replays your commits on top of the target branch. No merge commit.

```bash
git checkout feature
git rebase origin/main
```

```
main: A - B - C
\
feature: D' - E' <- new commits (replayed)
```

- History is linear and clean
- `D'` and `E'` are new commits with new hashes
- **Never rebase a public/shared branch** — it rewrites history
- Used when **catching up** locally before opening a PR

---

## 5. Why `git merge main` locally is discouraged

Using `git merge main` locally to catch up creates a noisy merge commit in your feature branch:

```
feature: D - E - [M] <- "merged main into feature" — this is just noise
```

When you open a PR, reviewers see this extra merge commit mixed in with your actual work. It makes history harder to read.

**Rule of thumb:**
- `merge` flows one direction — feature → main (shipping)
- `rebase` flows the other direction — main → feature (catching up)

---

## 6. `git merge main` vs `git merge origin/main`

Even after `git fetch`, these are **not the same**:

| | Source | Up to date after fetch? |
|---|---|---|
| `git merge main` | Your local `main` branch | No — local main is still stale |
| `git merge origin/main` | Remote tracking cache | Yes ✓ |

`git fetch` updates `origin/main` but does **not** update your local `main`. To make local `main` match `origin/main`, you'd need to checkout main and pull.

**Always prefer `origin/main` as the reference.**

---

## 7. Branch Purposes Summary

| Branch | Purpose |
|---|---|
| GitHub `main` | Source of truth, protected, never pushed directly |
| `origin/main` | Local cache, used for rebasing feature branches |
| local `main` | Where you build, test, and run locally |
| local `feature` | Where you develop |

### When you need to build/test from main

```bash
git checkout main
git pull # fetch + merge origin/main into local main
# now build, test, run
```

### When you are developing a feature

```bash
git fetch
git rebase origin/main # no need to touch local main at all
```

---

## 8. Interactive Rebase: Cleaning Up History

### `git rebase origin/main`
Just replays your commits on top of latest main. Automatic.

### `git rebase -i origin/main`
`-i` = interactive. Opens an editor to clean up commits before replaying.

```
pick abc "wip"
pick def "fix"
pick ghi "fix again"

# change to:
squash abc "wip"
squash def "fix"
pick ghi "add login feature" # squash all 3 into 1 clean commit
```

**Interactive mode options:**

| Command | What it does |
|---|---|
| `pick` | Keep commit as-is |
| `squash` | Merge into previous commit |
| `reword` | Keep commit but edit the message |
| `drop` | Delete commit entirely |

| | When to use |
|---|---|
| `rebase origin/main` | Just catching up, commits are already clean |
| `rebase -i origin/main` | Before opening PR, want to clean up messy history |

---

## 9. Conflict Handling

Both merge and rebase can produce conflicts.

| | Merge | Rebase |
|---|---|---|
| Resolve conflicts | Once | Per replayed commit |
| Continue after resolve | `git merge --continue` | `git rebase --continue` |
| Abort | `git merge --abort` | `git rebase --abort` |

---

## 10. Professional Daily Workflow

```bash
# Start a new feature
git checkout -b feature/TICKET-123-short-description

# Do your work
git add .
git commit -m "meaningful commit message"

# Catch up with latest main (before PR)
git fetch
git rebase origin/main

# Optional: clean up commit history before PR
git rebase -i origin/main

# Push and open PR
git push origin feature/TICKET-123-short-description

# PR approved → merge on GitHub → done
```

### Senior developers never:
- Force push to `main`
- Commit directly to `main`
- Use `git merge main` locally to catch up
- Leave stale branches for weeks

---

## 11. Golden Rules

> **Rebase to clean up your local work. Merge to integrate into shared history.**

> **main is protected and always merged online via PR.**

> **Feature branches are always rebased locally to catch up.**

```
main (protected, on GitHub)
^
└── merged via PR only (never directly pushed)

feature (local)
└── rebased to catch up with main
└── pushed → PR → merged on GitHub
```

