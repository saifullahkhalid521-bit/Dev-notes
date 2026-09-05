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