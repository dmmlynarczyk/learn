# Commands

Basic terms and commands used in git.

## Basic Terms

**Directory:** A different word for a folder.  
**Terminal or Command Line:** The interface used for Text Commands.  
**CLI:** Command Line Interface.  
**`cd`:** CLI command to Change Directory.  
**Code Editor:** Application for writing code.  
**Repository:** Project, or the folder/place where your project is kept.  
**GitHub:** A website to host your repositories online.  

## Basic Commands

> [!NOTE]
> Git commands are in lowercase.

**`clone`:** Bring a repository that is hosted somewhere like Github into a folder on your local machine.  
**`add`:** Track your files and changes in Git.  
**`add .`:** shorthand for "approve everything."  
**`commit`:** Save your files in Git.  
**`commit -m "message here"`:** Save your files and add a message for your commit.  
**`push`:** Upload Git commits to a remote repo, like Github.  
**`pull`:** Download changes from remote repo to your local machine, the opposite of push. A request to have your code pulled into another branch.
**`branch`:** Allows you to see what branches you have and which branch you are currently working on (denoted with a \*).  
**`checkout`:** Switch branches or restore working tree files.  
**`checkout -b <name>`:** Create a new branch and name that branch whatever is in <name>.  
**`checkout <name>`:** Switch the branch you are on.  
**`merge`:** Merge Secondary Branch with Master Branch.  
**`diff`:** See the differences of what has been added, removed, and updated.  
**`reset`:** Allows you to undo the staged changes.  Removes them from `git status` command.  Opposite of `git add .`  
**`reset HEAD~1`:** Allows you to go back one full commit.  Useful if you have already staged and commited a change.  This will force it to go back 1 commit prior to last commit.  
**`log`:** View a log of all commits, arranged in reverse chronological order.  

## Using Commands

When you want to commit files always run `git status` first.
This will give you the status of the working tree.
Including what files are new, what files have been modified, and more.

If there are untracked changes you will want to run `git add <file_name>` if there are multiple files that you want to include you can run `git add .` instead. 
*Essentially the . is a wildcard for all.*

When all changes show up under tracked when `git status` is run they are ready to be committed.
We will run `git commit -m "message"` the message will be the title of the message in Github.
This only saves the code locally, to make it live we will use `git push`.

**`git push origin main`:**    
*origin* stands for the location of our git repository.  
*main/master* is the branch we want to push to.
