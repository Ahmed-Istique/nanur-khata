# My Git Story: Nanu's Digital Recipe Book

## Chapter 1: The First Recipe
### Task Overview
Today, Nanu handed me her tearing, handwritten recipe book and told me winter is coming, so I needed to write down the *bhapa pitha* recipe first. To make sure no recipe is ever lost, I set up Git!

* **Commands I ran:**
  ```bash
  git config --global user.name "Istique_Ahmed"
  git config --global user.email "istiqueahmed.01@gmail.com"
  mkdir nanur-khata
  cd nanur-khata
  git init
  git branch -M main
  touch bhapa-pitha.md my-story.md
  git add bhapa-pitha.md

What happened:I initialized our family's digital recipe repository and created the first recipe file. Then, Nanu stopped me and corrected the ingredients: "One and a half cups of gur, not two!"   
When I checked git diff and git diff --staged, I learned how Git tracks what's currently changed versus what has already been staged. After committing my changes, I accidentally staged a grocery list (bazar-list.txt), but successfully un-staged it using git reset without losing the file.

## Chapter 2: The Secret Spice
### Task Overview
Nanu has a strict rule: her secret spice blend (`secret-masala.txt`), along with random temporary notes (`*.tmp`) and draft folders, must never leak to GitHub or be tracked by Git, otherwise Chapter 2 fails!

* **Commands I ran:**
  ```bash
  touch secret-masala.txt temp-notes.tmp backup.tmp
  mkdir draft
  touch draft/rough-recipe.txt
  touch .gitignore
  # (Added secret-masala.txt, *.tmp, and draft/ inside .gitignore)
  git status
  git add .gitignore bhapa-pitha.md my-story.md
  git commit -m "Add .gitignore to keep secret masala and draft files private"


## Chapter 5: Half-Cooked Halua and Time Travel

### Task Overview
In this chapter, I handled an interruption during recipe writing by stashing unfinished work, fixing a missing ingredient in the biryani, organizing files with Git's move and remove commands, inspecting historical commits, and experimenting with destructive resets on an isolated test branch.

---

### Step-by-Step Workflow & Commands Executed

1. **Task A — Stash, Hotfix, and Restore:**
   - Started writing edits in `halua.md` (leaving it in an uncommitted, halfway state).
   - Saved the unfinished halua work to temporary storage:
     ```bash
     git stash
     ```
   - Added the missing cardamom ingredient to `biryani.md`, saved, staged, and committed the fix:
     ```bash
     git add biryani.md
     git commit -m "Fix biryani: add missing cardamom"
     ```
   - Restored the uncommitted halua work back to the working directory:
     ```bash
     git stash pop
     ```

2. **Task B — Refactoring and Clean-up:**
   - Created subdirectories to structure the recipe files:
     ```bash
     mkdir desserts mains
     ```
   - Moved the recipe markdown files into their respective directories using Git's move tracker:
     ```bash
     git mv halua.md desserts/
     git mv biryani.md mains/
     ```
   - Removed an obsolete/old recipe file safely using `git rm` and committed the changes:
     ```bash
     git rm old-recipe.md
     git commit -m "Organize recipes into folders and remove old recipe"
     ```
   - Verified that Git tracked the file relocations rather than a simple delete/create using rename detection:
     ```bash
     git log --stat -M
     ```

3. **Task C — Commit Inspection:**
   - Selected a historical commit SHA from the log and inspected its exact code modifications and metadata:
     ```bash
     git show <SHA>
     ```

4. **Task D — Hard Reset Experiment (Test Branch):**
   - Created and switched to a temporary, safe test branch:
     ```bash
     git checkout -b test-branch
     ```
   - Performed a hard reset pointing to an older commit:
     ```bash
     git reset --hard <older-commit-SHA>
     ```
   - **What was lost:** Running `git reset --hard` permanently destroyed all uncommitted working directory changes as well as any committed history that occurred after the targeted older commit on that branch.

---

### Conceptual Questions

**Question: Why are rebase and reset --hard dangerous on a shared branch?**

- **Rewriting Commit History:** Both `git rebase` and `git reset --hard` alter, move, or erase existing commit SHAs.
- **Branch Divergence:** If the modified commits have already been pushed to a remote shared repository (like GitHub), rewriting them causes local and remote histories to heavily diverge.
- **Permanent Data Loss for Team Members:** Forcing updates onto a shared branch requires a force push (`git push --force`), which can silently overwrite and erase valuable work contributed by teammates, resulting in permanent code loss across the team.