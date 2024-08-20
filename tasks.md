# Git commits to commit
### Creating a directory named work
```
mkdir work
```
### Creating a subdirectory named 'hello'
```
mkdir hello
```
### Generating a file named 'hello.sh' within the work directory
```
code hello.sh
```
### Initializing the git repository in the hello directory
```
git init
```
### Checking the status
```
git status
```
### Staging and commiting the changed file 
```
git add hello.sh
git commit -m "change content"
```
### Staging and commiting the changes in lines 3, 4 and 5
```
git add hello.sh
git commit -m "Added a comment explaining the default value for 'name' in hello.sh" -m "Added v
ariable assignment and echo statement in hello.sh"
```


# History
### Show history of the working directory
```
git log
```
### Show one-line history for condensed view
```
git log --oneline
```
### Controlled entries for last 2 entries
```
git log -n 2
```
### Controlled entries for the last five minutes
```
git log --since="5 minutes ago"
```
### Personalized Format
```
git log --pretty=format:'* %h %ad | %s (%d) [%an]' --date=short
```


# Check it out 
## Restore First Snapshot
### Find the first commit hash
```
git rev-list --max-parents=0 HEAD
```
### Checkout the first commit 
```
git checkout d6babbb565769c2228f19575cc265ba037d47146
```
### Print the content of the `hello.sh`
```
cat hello.sh
```
## Restore Second Recent Snapshot 
### Checkout to master
```
git checkout master
```
### Checkout the second most recent commit
```
git checkout HEAD~1
```
### Print the content of `hello.sh`
```
cat hello.sh
```
## Return to Latest Version 
```
git checkout master
```
### Print the content of `hello.sh`
```
cat hello.sh
```

# TAG me 
### Reference current version
```
git tag v1
```
### Tagging previous version
```
git tag v1-beta HEAD^ 
```
### Navigating current version
```
git checkout v1
``` 
### Navigating previous version
```
git checkout v1-beta
```
### List tags
```
git tag
```


### Reverting changes
```
git restore hello.sh
```
### Staging
```
git add hello.sh
```
### Cleaning 
```
git reset HEAD hello.sh
```
### Discard changes
```
git restore hello.sh
```
### Committing and reverting 
### Staging
```
git add hello.sh
```
### Committing 
```
git commit -m "unwanted but committed change"
```
### Revert the commit 
```
git revert HEAD
```


# Tagging and removing commits
### Tag latest commit with `oops`
```
git tag oops
```
### Find commit hash for v1
```
git show-ref --tags v1
```
### Reset Repository to the v1 commit
```
git reset --hard cf74c6451f49fd04935a982cef591ee37d73cff8
```


# Displaying logs with deleted commits
```
git reflog
```


# Cleaning unreferenced commits
```
git reflog expire --expire=now --all
```

# Author information
### Adding an author comment
```
git add hello.sh
``` 
### Commmitting the change
```
git commit -m "Add author comment"
```
### Including changes from last commit
```
git commit --amend --no-edit
```


# Move it
### Create the lib/ directory
```
mkdir lib/
```
### Moving hello.sh to lib/ directory
```
git mv hello.sh lib/
```
### Commiting the move
```
git commit -m "Move hello.sh into the lib/"
```
### Creating a Makefile in the root directory
```
code Makefile
```
### Commiting the Makefile
```
git commit -m "Add Makefile to run hello.sh"
```


# Blobs, trees and commits
### Explore .git/ DIrectory
```
cd .git/
```
### Getting latest object hash
```
git log -1 --format=%H
```
### Determine the type of an object(commit,tree,blob)
```
git cat-file -t 33c95dd5dfaf8d48390c4bf26e8ed73d077a673d
```
### Viewing the content of the object
```
git cat-file -p 33c95dd5dfaf8d48390c4bf26e8ed73d077a673d
```
# Dumping Directory Tree
### Dumping the directory tree
```
git ls-tree -r HEAD
```
### Dumping the contents of the lib/ directory
```
git show HEAD:lib/
```
### Dumping the contents of the lib/hello.sh
```
git show HEAD:lib/hello.sh
```


# Branching
### Create and switch to new branch
```
git checkout -b greet
```
### Creating a new file named greeter.sh
```
code greeter.sh
```
### Staging 
```
git add hello.sh
```
### Commiting the changes on hello.sh
```
git commit -m "Update hello.sh to source greeter.sh and use Greeter function"
```
### Staging changes on Makefile
```
git add Makefile
```
### Commiting changes on Makefile
```
git commit -m "Update Makefile with comment to
 run updated hello.sh"
 ```
 ### Switch to main branch
 ```
 git checkout master
 ```
 ### Compare the Makefile between the main and greet branches
 ```
 git diff master greet -- Makefile
```
### Compare the hello.sh file between the main and greet branches
```
git diff master greet -- lib/hello.sh
```
### Compare the greeter.sh file between the main and greet branches
```
git diff master greet -- lib/greeter.sh
```
### Create a README.md
```
code README.md
```


# Conflicts, merging and rebasing
### Merge main into the greet branch
```
git checkout greet
```
```
git merge master
```
### Switch to main branch and make changes to the hello.sh file
```
git checkout master
```
### Commiting the changes made to the hello.sh file
```
git add hello.sh
```
```
git commit -m "Update hello.sh to greet the user by name"
```
### Merging main into greet branch(Conflict)
```
git checkout greet
```
```
git merge master
```
### Solve conflict manually and commit changes
```
git add hello.sh
```
```
git commit -m "Resolved merge conflict by accepting changes from main branch"
```
### Go back to point before the initial merge
```
git log --oneline
```
### Rebasing greet branch
```
git reset --hard 1cad675
```
```
git rebase master
```
* Git will apply the commits from the greet branch on top of the main branch's latest commit. If there any conflicts during the rebase, Git will pause the rebase process, and you'll need to resolve the conflicts manually.

* If there are conflicts, Git will mark the conflicting sections in the affected files. Open the files, resolve the conflicts by choosing the desired changes, and stage the resolved files.

bash
```
git add <resolved-file>  # Replace <resolved-file> with the actual filename
```
After resolving all conflicts, continue the rebase process:

```
git rebase --continue
```
Repeat this process until the rebase is complete.
### Merging greet into main
```
git checkout master
```
```
git merge greet
```


* Fast-forwarding occurs during a merge operation when the base branch that's being merged into has no new commits since the feature branch (the branch being merged) was created or last updated. Instead of creating a new "merge commit," Git simply moves the pointer forward, hence the term "fast forward."

* Git merging refers to Git's way of putting a forked history back together again. The git merge command lets you take the independent lines of development created by git branch and integrate them into a single branch. On the other hand, git rebase refers to one of two Git utilities designed to integrate changes from one branch onto another. Rebasing is the process of combining or moving a sequence of commits on top of a new base commit. Git rebase is the linear process of merging


# Local and remote repositories
### Make a clone of the repository cloned_hello
```
git clone hello/ cloned_hello
```
### Show logs of cloned_hello
```
cd cloned_hello
```
```
git log --oneline --graph --all
```
### Provide information about the remote repository
```
git remote -v
```
```
git remote show origin
```
### List all remote and local branches
```
git branch -a
```
### Commiting changes
```
git commit -m "Update README.md with Hello World example content"
```
### Fetch changes for cloned_hello
```
git fetch origin
```
### Displaying the logs
```
git log --oneline --graph --decorate --all
```
### Merge changes from the remote main into the local branch
```
git merge origin/master
```
### Add a local branch named greet
```
git checkout -b greet origin/greet
```
### Add remote to git repository
```
git remote add gitea https://learn.zone01kisumu.ke/git/shaokoth/git
```
### Push the main and greet branches to the new route
```
git push gitea master
```
```
git push gitea greet
```
* "What is the single git command equivalent to what you did before to bring changes from remote to local main branch?"
```
git pull origin master
```


# Bare repositories
### Definition bare repository
A bare repository in Git is a repository that doesn’t contain a working directory with the actual files. Instead, it contains only the Git metadata (branches, tags, commit history, etc). Bare repositories are typically used as a central repository for collaboration, where multiple developers push and pull changes. It helps prevent conflicts that could arise if developers pushed to a non-bare repository with a working durectory.
### Create a bare repository
```
cd work
```
### Create
```
git clone --bare /home/shaokoth/git/work/hello hello.git
```
### Add hello.git repository as a remote to the original repository
```
cd hello
```
### Add the bare repository as a remote
```
git remote add bare /home/shaokoth/git/work/hello/he
llo.git
```
### Verify remote was added 
```
git remote -v
``` 
### Commit changes to README.md
```
git add README.md
```
```
git commit -m "updated README.md with new content"
```
### Push the changes to the shared(bare) repository
```
git push bare master
```
### Switch to the cloned_hello
```
cd cloned_hello
```
### Pull the changes from the shared repository
```
git pull origin master
```

















	
