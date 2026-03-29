# Git Merge vs Git Rebase — A Practical Lesson

## 1. The Core Concept

Both commands integrate changes from one branch into another, but in different directions and for different purposes.

> **merge** = integrate your work **into** the product (feature → main)

> **rebase** = integrate the product's updates **into** your work (main → feature)

```
rebase: main → your feature (you catch up)
merge: your feature → main (you ship)
```

## 2. Understanding the Three Layers

There are 3 things, not 2:

|No| Name | Where | Description |
|---|---|---|---|
|1| Remote branch | On GitHub server | The real `main` on GitHub, always latest |
|2| Remote tracking branch | On your local machine | `origin/main` — a local cached copy of GitHub's `main` |
|3| Local branch | On your local machine | Your `main`, `feature`, etc. |

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

## 3. Git Merge

Combines histories by creating a new merge commit. In real workflow, **you never run this manually** — it happens when you click "Merge pull request" on GitHub, GitLab, Bitbucket, or VS Code's Source Control panel.

```
main: A - B -  C -------\
                         \
feature:        D - E - [M] <- merge commit (created by GitHub/VS Code)
```

- `[M]` has two parents: the tip of `main` and the tip of `feature`
- Full history is preserved — you can always see where the branch came from
- Creates an extra merge commit `[M]` in `main` (this is fine and expected)
- **You do this via PR, MR on GitHub/GitLab/Bitbucket/Azure DevOps, not the terminal**

### What the UI does under the hood

When you click "Merge pull request", GitHub/VS Code runs:

```bash
git checkout main
git merge feature/your-branch  # creates [M] on main
```

You just never see it.

---

## 4. Git Rebase

Takes your commits and **replants them on top of the latest main**. No merge commit — history stays linear.

### Before rebase

Your feature branch was created when main was at `B`. Main has since moved to `C`.

```
main:    A - B - C
              \
feature:       D - E   (based on B, now behind)
```

### After `git rebase origin/main`

Git lifts `D` and `E` off their old base and replays them after `C`:

```
main:    A - B - C
                  \
feature:           D' - E'   (rebased on C, now up to date)
```

### Why D' and E' (not D and E)?

Rebase **rewrites** your commits. Each replayed commit gets:
- A new parent (previously `B`, now `C`)
- A new commit hash

The content of your changes is the same, but the commits are technically new objects.

### How to run it

```bash
git fetch                  # update origin/main cache
git rebase origin/main     # replay your commits on top
```

### Rules

- Only rebase **your own local/feature branches** — never a shared branch
- Rewriting a branch others have cloned breaks their history
- This is a local operation — no one sees it until you `git push`

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
| GitHub `main` | Source of truth, protected, never pushed directly |
| `origin/main` | Local cache, used for rebasing feature branches |
| local `main` | Optional — senior devs often delete it entirely |
| local `feature` | Where you develop |

### Senior devs: delete local `main`

Local `main` goes stale and is never needed. You can safely delete it:

```bash
git branch -d main
```

`origin/main` is always up to date after `git fetch` — that's all you need.

### If you need to build/test from latest main

```bash
git fetch
git checkout --detach origin/main  # detached HEAD, no branch created
# build, test, run
git checkout feature/your-branch   # return to your work
```

### When you are developing a feature

```bash
git fetch
git rebase origin/main  # origin/main is enough — no local main needed
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

## 9. Resolving Conflicts

A conflict happens when two branches edit the **same line** in the same file. Git can't decide which version to keep — it stops and asks you to choose.

### What a conflict looks like

When Git hits a conflict, it injects markers directly into the file:

```
<<<<<<< HEAD (your branch)
const timeout = 3000;
=======
const timeout = 5000;
>>>>>>> origin/main
```

- `<<<<<<< HEAD` — your version
- `=======` — divider
- `>>>>>>> origin/main` — the incoming version

You must edit the file to remove the markers and leave only the correct code.

### Step-by-step: resolve in terminal

```bash
# 1. See which files have conflicts
git status
# → both modified: src/config.ts

# 2. Open the file, find the markers, fix the code manually
# (remove <<<, ===, >>> and keep the right version)

# 3. Stage the resolved file
git add src/config.ts

# 4. Continue (do NOT commit manually during rebase)
git rebase --continue   # or: git merge --continue
```

### Step-by-step: resolve in VS Code

VS Code has built-in conflict UI — no need to edit markers by hand.

1. Open the conflicted file — VS Code highlights the conflict block
2. Click one of the options above the block:
   - **Accept Current Change** — keep your version
   - **Accept Incoming Change** — keep their version
   - **Accept Both Changes** — keep both (stacked)
   - **Compare Changes** — see a side-by-side diff
3. Save the file
4. In the Source Control panel, stage the file
5. Run `git rebase --continue` or `git merge --continue` in the terminal

### Rebase vs merge: key difference when conflicting

| | Merge | Rebase |
|---|---|---|
| Conflicts appear | Once, all at once | One per replayed commit |
| After resolving | `git merge --continue` | `git rebase --continue` |
| Abort everything | `git merge --abort` | `git rebase --abort` |

With rebase, if you have 3 commits and 2 of them conflict with main, you resolve conflicts **twice** — once per commit as Git replays them.

### If it gets too messy — abort

```bash
git rebase --abort   # restores your branch to exactly where it was before
git merge --abort    # same for merge
```

No harm done — you're back to the state before you started.

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
