# Git & CLI Commands

## [Useful Git Commands](https://medium.com/flawless-app-stories/useful-git-commands-for-everyday-use-e1a4de64037d)

* `git init` >> initialize a local folder as a git repo to be tracked and push to the cloud
* `git branch feature-1-berger` >> Create the branch on your local machine called "feature-1-berger".
* `git checkout -b feature-1-berger` >> Create the branch on your local machine **and** switch into this branch.
* `git checkout feature-1-berger` >> Switch into this branch.
* `git branch` >> return the current branch you are working in.
* `git status` >> Check the status of tracked/untracked changed files
* `git add fileName.js ` >> Add the file "fileName.js" to be tracked for the next commit.
* `git add -A` >> Add all changed files to be tracked.
* `git commit -m "message" ` >> Make a commit with the message "message".
* `git push` - Push the commit to the current working branch
* `git push origin branch_name` >> Push the commit to the branch "branch_name"
* `git pull` >> Pulls down changes from the repo to bring your local codebase up-to-date
* `git push —set-upstream origin resume` >>  set the initial push to know where all future pushes need to go in the gitHub cloud.

cd => // change directories
cd workspace => // will change to a new folder/directory called workspace
ls => // list out the files in that directory

## List CLI Commands

* `mkdir jsDev` >> will make a folder(aka, directory) called "jsDev"
* `cd` >>  change directories
* `cd workspace` >>  will change to a new folder(aka, directory) called "workspace"
* `pwd` >> Print Working Directory, will return the name of the current directory you are in.
* `ls` >>  list out the files in that directory
* `code .` >> open the current directory in VS Code (Macs have to install the PATH)
* `touch index.html` >> will create a file inside the current directory called "index.html"
* `echo "USERNAME=meathead" >> .env` >> create a file called `.env` and writes "USERNAME=meathead" inside of it.

### Other useful commands to research

* `mv` >> move directory
* `cp` >> copy file
* `rm` >> remove file or directory
* `tree` >> Must install with brew or bash, but is a very useful command to see your entire working directory's tree.
