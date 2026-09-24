# Git and GitHub 

## Git
* Git is a tool that tracks changes in your code and helps you manage different versions of your project.
* 👉 Simple example:
* Git keeps a history of your code, so you can see what you changed and go back to an older version if needed.
## GitHub
* GitHub is an online platform where you can store, share, and collaborate on Git repositories.
* 👉 Simple example:
* Git = your project's version-control system
* GitHub = online place where you store and share that Git project

* 🧠 Easy to remember
* Git manages your code history, while GitHub stores and shares your Git repositories online.

## How to set up Git and GitHub with code editor
1. Install Git: Download and install Git from [git-scm.com](https://git-scm.com/).

2. Create a GitHub account: Sign up at [github.com](https://github.com/).

3. Configure Git: Set your username and email in Git using the following commands:
   ```
   git config --global user.name "Your Name"
   git config --global user.email "your.email@example.com"
   ```
4. Check Git installation: Verify Git is installed by running `git --version` in your terminal.

5. GitHub account ko VS Code se connect kar
* VS Code ke top-right me Accounts/profile icon par click kar → Sign in with GitHub.
* Browser khulega → GitHub me login kar → authorization allow kar.
* Isse VS Code ko GitHub account ke saath authenticate karna easy ho jata hai.

6. Open your project folder in VS Code: Use `File > Open Folder` to open your project.

my-project/
├── index.html
├── style.css
├── script.js
└── ...

7. Project ko Git repository banane ke liye terminal me `git init` command run karein. check krne ke liye `git status` command run karein. Ye batayega ki kaunse files modified ya untracked hain.

8. GitHub par repository bana
ne ke liye:
   * GitHub par login karein.
   * "New" button par click karein.
   * Repository name, description (optional), aur visibility (public/private) select karein.
   * "Create repository" button par click karein.

*IMPORTANT:* Important: Agar tu existing local project push kar raha hai, beginner ke liye GitHub repository banate waqt README, .gitignore, etc. initially add na karna easiest hai.

9. Local project ko GitHub repository se connect karne ke liye terminal me ye commands run karein:
   a. `git remote add origin <repository-url>`: Connect local repository to remote repository.
   b. `git remote -v`: Verify the connection to the remote repository.

10. Changes ko GitHub par push karne ke liye:
   a. `git add .`: Stage all changes.
   b. `git commit -m "Your commit message"`: Commit the changes with a message.
   c. `git push -u origin main`: Push the changes to the main branch of the remote repository.
   

   #### Agar GitHub se latest code apne computer me lana hai:
   git pull

   * Ye 6 commands sabse important hain
    git status
    git add .
    git commit -m "message"
    git push
    git pull
    git log


*IMPORTANT:* Agar GitHub par already koi new commit hai jo tere local computer me nahi hai, tab:
git pull origin main karna important hai.
Otherwise git push reject ho sakta hai:

* Workflow:

1. git add .
2. git commit -m "Your commit message"
3. git pull origin main
4. git push origin main

recammendation: Always pull before pushing to avoid conflicts.

1. git pull origin main
2. git add .
3. git commit -m "message"
4. git push origin main


1. Use git push -u origin main the FIRST time you push a newly created branch to a remote repository. Setting the tracking link once saves you keystrokes going forward.  

2. Use git push (or git push origin main) for subsequent pushes once the tracking link is already established.  

___________________________________________________________________________________________________________________________________________________

## Branches

* A branch is a separate line of development.
* It allows me to work on changes without directly affecting the main branch.

### Useful commands:
- `git branch` → show local branches
- `git checkout -b <name>` → create and switch to a new branch
- `git checkout <name>` → switch branches


## Pull Request
* A Pull Request also known as PR is a request to merge the changes from one branch into another branch, usually from a feature branch into main, so the changes can be reviewed before merging.

1. itle likho: Add day 1 branch practice notes

2. Description mein likho:

* Kya change kiya
* Kyun kiya

3. "Create pull request" click karo

4. Ab khud ki PR review karo:

* Files changed tab mein jao
* Comments add karo (jaise "ye line improve kar sakta hoon")

5. "Merge pull request" click karo

6. Branch delete kar do (GitHub pe button aayega)

### Workflow
main → feature branch → changes → commit → push → PR → review → merge → pull main → delete branch


## Merge + Local Sync + Merge Conflict
* Concept: Merge GitHub pe hota hai, local main ko update karna zaroori hai. Conflict tab aata hai jab do branches same file edit karein.

1. Part A -Local Sync

* PR merge karne ke baad: 
1. `git checkout main` → Switches to the main branch.

2. `git pull origin main` → Downloads the latest changes from GitHub's main branch and updates your local main.
<!-- check this -> (`git pull origin < merged branch name>`) -->

3. `git branch -d feature/day1` → Deletes the local feature/day1 branch.


2. Part B - Merge Conflict

* Main branch pe ek file edit karo (conflict-test.txt)

* Commit + push karo
 
* Nayi branch banao: git checkout -b feature/conflict
 
* Same file mein alag change karo
 
* Commit + push karo
 
* PR banao → "This branch has conflicts" message aayega
 
* Local mein resolve karo:

1. `git checkout main` → Switches to the main branch.

2. `git pull origin main` → Gets the latest changes from GitHub's main and updates your local main.

3. `git checkout feature/conflict` → Switches to the feature/conflict branch.

4. `git merge main` → Merges the latest main changes into feature/conflict.

* → Conflict aayega. File kholo, <<<<<<<, =======, >>>>>>> markers dikhenge. Manually resolve karo.

`git add conflict-test.txt`
`git commit -m "fix: resolve merge conflict"`
`git push origin feature/conflict`

* PR merge ho jayegi

## How to change default branch in GitHub
* just search for it in google 🙃;

_____________________________________________________________________________________________________________________________________________

## Git Restore Mistakes
1. Discard changes in a specific file (Recommended)
* If you only deleted content in one specific file (e.g., conflict-test.txt):
`git restore filename.txt`

2. Discard all uncommitted changes across all files
* If you want to reset every modified or deleted file back to the last commit:
`git restore .`

3. If you already staged the deletion (git add)
* If you accidentally ran git add . or git add filename.txt after deleting the text, unstage it first, then restore:
1. Unstage the changes
`git restore --staged filename.txt`
2. Revert the file back to the last commit
`git restore filename.txt`

4. Alternative: Hard Reset (Nuclear Option)
* If you want to discard all local modifications, staged files, and uncommitted edits at once:
`git reset --hard HEAD`
*Note* git restore and git reset --hard permanently erase uncommitted changes. Make sure you don't need any of your current unstaged work before running them.


_____________________________________________________________________________________________________________________________________________________________


# Core Git Configuration Files

*.gitkeep*
* .gitkeep is an empty placeholder file used to force Git to track an otherwise empty folder.

### How to use it

1. Create a file named .gitkeep inside the empty folder.
2. Commit and push the .gitkeep file.

*.gitignore*
* .gitignore is a plain text file that tells Git which files, folders, or auto-generated build outputs to ignore.

* Files matched in .gitignore will not show up in git status and will never be committed or pushed to remote repositories like GitHub.

### Why use .gitignore?

*It prevents sensitive data, temporary files, and heavy dependencies from cluttering your repository:

1. API Keys & Credentials: .env, secrets.json
 
2. Dependency Folders: node_modules/, vendor/
 
3. Build Outputs: dist/, build/
 
4. System & OS Files: .DS_Store, Thumbs.db

### How do use it
1. Create the file
* Create a file named .gitignore (with the dot at the beginning) in the root directory of your Git project.

2. Add patterns to ignore
* Open .gitignore in your text editor and list the files or folders you want Git to ignore:

 
*.gitattributes*
* Sets file-specific rules, such as enforcing consistent line endings (LF vs CRLF) across Windows, Mac, and Linux.

*.gitmodules*
* Tracks external Git repositories embedded inside your main project as submodules.

*.mailmap*
* Cleans up commit history by merging duplicate author names and email addresses into single canonical identities.



# Platform & Project Metadata Files (GitHub / GitLab)

*README.md*
* The main project documentation file that explains what the project does and how to set it up.

*LICENSE*
* Defines the legal open-source or proprietary terms for using, modifying, and sharing the code.

*CODEOWNERS*
* Automatically assigns specific team members or reviewers to Pull Requests based on modified files.

*SECURITY.md*
* Outlines instructions and safety procedures for reporting security vulnerabilities responsibly.

*PULL_REQUEST_TEMPLATE.md*
* Provides a standardized checklist or description template that appears whenever someone opens a PR.