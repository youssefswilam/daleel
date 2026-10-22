# Day 2 — Git properly

My study summary of Missing Semester [Version Control (Git)](https://missing.csail.mit.edu/2020/version-control/) and [Pro Git](https://git-scm.com/book/en/v2) chapters 2–3.

## 1. How Git thinks

Git is not "saving files". It saves **snapshots** of the whole project.

| Idea | What it is |
| --- | --- |
| **blob** | The contents of one file |
| **tree** | A folder: names pointing to blobs and other trees |
| **commit** | A snapshot (one top tree) + author + message + pointer to its **parent** commit(s) |
| **hash** | Every object is named by a SHA-1 of its contents, e.g. `529f22d` |
| **branch** | Just a movable **name** pointing to one commit (`main`, `day2-notes`) |
| **HEAD** | "Where you are now" — usually points to a branch |

History is a chain of commits, each pointing back to its parent:

```
b0ceb53 ← 820edc6 ← 1ed6d57 ← 045a56c ← 529f22d   ← main ← HEAD
```

A branch is cheap: creating one just makes a new name pointing at the current commit.

## 2. The three areas

```
working folder  --git add-->  staging area  --git commit-->  repository (history)
 (your files)                  (next snapshot)                (.git folder)
```

- `git add` chooses **what goes into the next commit**. You can stage some changes and leave others out.
- `git commit` saves the staged snapshot permanently.
- `git push` sends your commits to GitHub; `git pull` brings GitHub's commits to you.

## 3. Everyday commands

| Command | Does |
| --- | --- |
| `git status` | What's changed, what's staged — run it constantly |
| `git diff` | Changes **not yet staged** |
| `git diff --staged` | Changes staged for the next commit |
| `git add file` | Stage one file (`git add .` = everything in this folder) |
| `git commit -m "Day N: ..."` | Save a snapshot with a message |
| `git log --oneline --graph --all` | History as a compact graph |
| `git show <hash>` | What one commit changed |
| `git restore file` | Throw away unstaged changes to a file (careful: can't undo) |
| `git restore --staged file` | Unstage a file (keeps your changes) |

## 4. Branches and merging

| Command | Does |
| --- | --- |
| `git branch` | List branches (`*` = current) |
| `git switch -c day2-notes` | Create a branch and move to it |
| `git switch main` | Move back to `main` |
| `git merge day2-notes` | Bring that branch's commits into the current branch |
| `git branch -d day2-notes` | Delete a branch that's already merged |

- **Fast-forward merge:** `main` hasn't moved since you branched, so Git just slides `main` forward. No merge commit.
- **Merge commit:** both branches have new commits, so Git makes a commit with **two parents**.
- **Conflict:** both changed the same lines. Git marks the file:

```
<<<<<<< HEAD
the version on your current branch
=======
the version from the other branch
>>>>>>> day2-notes
```

Edit the file to the version you want, delete the markers, then `git add file` and `git commit`.

## 5. Remotes

| Command | Does |
| --- | --- |
| `git remote -v` | Show remotes (`origin` → `git@github-personal:youssefswilam/daleel.git`) |
| `git push -u origin day2-notes` | Push a new branch and remember where it goes (`-u` only the first time) |
| `git fetch` | Download new commits but don't change your files |
| `git pull` | `fetch` + merge into your current branch |

## 6. Pull requests (GitHub, not Git)

A pull request (PR) is GitHub's page for saying "please merge my branch into `main`". It shows the diff, lets people comment, and runs CI (from Day 18). Even working alone, PRs are good practice: they're how every team works.

Flow: branch → commit → push branch → open PR on GitHub → review the diff → merge → `git switch main` → `git pull` → delete the branch.

## 7. Good commit messages

- One commit = one logical change.
- Short summary line (≤ 72 characters), in this repo: `Day N: <what was done>`.
- Commit often; push at least at the end of each day.

## 8. Undoing things (Pro Git 2.4)

| Situation | Fix |
| --- | --- |
| Typo in the last commit message (not pushed yet) | `git commit --amend` |
| Staged a file by mistake | `git restore --staged file` |
| Want to discard edits to a file | `git restore file` |
| Pushed a bad commit | `git revert <hash>` — makes a new commit that undoes it (safe, keeps history) |

Avoid `git reset --hard` and `git push --force` until you fully understand them: they can destroy work.

## 9. `.gitignore`

A file listing things Git should never track: `.env` (secrets!), `.venv/`, `__pycache__/`, `*.pyc`. Check it before your first `git add .` in any project.

## Test yourself

1. What's the difference between the working folder, the staging area and the repository?
2. What actually *is* a branch?
3. When does a merge create a merge commit, and when is it a fast-forward?
4. What's the difference between `git fetch` and `git pull`?
5. You pushed a bad commit to `main`. Why use `git revert` instead of deleting it?
