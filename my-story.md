# My Git Story: Nanu's Digital Recipe Book

## Chapter 1: The First Recipe
Today, Nanu handed me her tearing, handwritten recipe book and told me winter is coming, so I needed to write down the *bhapa pitha* recipe first. To make sure no recipe is ever lost, I set up Git!

* **Commands I ran:**
  ```bash
  git config --global user.name "Your Name"
  git config --global user.email "your.email@example.com"
  mkdir nanur-khata
  cd nanur-khata
  git init
  git branch -M main
  touch bhapa-pitha.md my-story.md
  git add bhapa-pitha.md

What happened:I initialized our family's digital recipe repository and created the first recipe file. Then, Nanu stopped me and corrected the ingredients: "One and a half cups of gur, not two!"   
When I checked git diff and git diff --staged, I learned how Git tracks what's currently changed versus what has already been staged. After committing my changes, I accidentally staged a grocery list (bazar-list.txt), but successfully un-staged it using git reset without losing the file.

## Chapter 2: The Secret Spice
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


  