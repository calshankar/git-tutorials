# Git Command Reference

### GIT CONFIGURATION

+ git config —global user.name “Shankar”
+ git config —global user.email “callshank_78@yahoo.com”

+ git config —global —list
+ cat ~/.gitconfig

+ git config —global core.editor nano
+ gitit config —global help.autocorrect 1

+ git config —global color.ui.auto
+ git config —global core.autocrlf false

+ git config --global mergetool.kdiff3.path /Applications/kdiff3.app/Contents/MacOS/kdiff3

### CREATE/INITIALIZE LOCAL DIR

+ mkdir <git project/folder name>

+ git init

+ ls -la

Add file to the dir & then run 

+ git status  -> Tracks all changes to dir

Adding file

+ git add <file-name>

+ git commit -am ""  

History of commit including SHA

+ git log

Update the the file with more text & check # git status

+ git add -u <file name>

Please note that '-u' is only for file chaged or deleted not for newly created file

Changes between commit sha's # git diff <sha>..<sha>

As it is difficult to remember/get the sha of change we run the diff as 

+ git diff HEAD~1..HEAD
+ git diff HEAD~1..

### REVERTING THE CHANGES TO WORK OR LOCAL DIR

Modify a file & run # git status

now to revert back the changes use # git checkout <file modified>

To revert the changes run # git reset --hard

### UNDOING & RE-DOING CHANGES

Let's say that after pushing your change to remote, you wanted to remove last change that was checked-in

+ git reset --soft HEAD~1  (reset only HEAD)

Now you want to remove the recently checked-in commit, since you realise that it is broken

+ git reset —hard HEAD~1  ->(reset HEAD, index and working tree)

CLEANING WORKING COPY

+ git clean -n  —> would let you know which file will be removed before you actually remove
+ git clean -f
+ git status


SUBMITTING ALL CHANGES TO REMOTE REPO/ORIGIN

Assuming a remote repo exist, push all the changes to remote origin using the command

+ git remote add origin git@github.com:calshankar/git-tutorials.git  -> change ssh url accordingly

+ git remote -v 

+ git push -u origin master

This should push all committed code to remote repository created

### VIEW PAST COMMITS

+ git log --oneline --graph
		OR
+ git log --graph --online --all --decorate

 Shortlog is actually short for format equals short.

+ git shortlog    -> lists of the authors and the commit messages from each of them.

+ git shortlog -s -n -e  -> With sorting option

+ git show HEAD  -> show last commit
+ git show HEAD~1

 # git log --oneline

For specific commits or changes use # git show <commit hash>

Remote repo

+ git remote or # git remote -v

### TAGGING BRANCH

+ git tag V1.0 -> -> tag reflect the exact commit at all times future i.e. permanent point in time marker

Adding annotation to tag
+ git tag -am V1.0_msg "This is an annotated tag"
+ git tag -> shows the tag for the repo

PUSHING THE TAGS TO REMOTE

+ git push --tags

### CREATING BRANCHES

+ git branch feature-1
+ git checkout feature-1
		OR
+ git checkout -b feature-1  --> one liner

+ git branch -m bug1 fix-3429 --> rename the 'bug1' branch created to fix-3429

+ git branch -d fix-3429  --> For deleting branch. For unmerged changes, git will prevent you from deleting

+ git branch -D fix-3429  --> Force delete the branch (avoid it at all cost)

### RECOVERING DELETED COMMITS

Let's say you did not intend to delete branch but you accidentally deleted. How to recover?

+ git reflog  -> this is a log of all references where HEAD has pointed to from initialization. All changes to the branch/repo is tracked via commit id. Using the commit-id you can recover historical entry from the log

We can go all the way back to commit which is the commit to fix fix-3429, we can also see the SHA which is xxxxxx

STASHING CHANGES

+ git stash  --> Puts the the change in temp holding area. Stashing is done before commit

+ git stash list  --> get the stash-id

+ git stash pop <stash-id> --> Applies & removes the entry from stash list

### MERGING BRANCHES

+ git checkout master
+ git merge <branch-name> --> Merges the change to the checked-out branch, in this case it merges to master branch

+ git mergetool  --> now resolve the conflict by including the changes from local & remote

So we can either resolve this merge manually using our text editor or we can use merge tool. Merge tool allows us to use a variety of different tools for performing the merge. I've got this kdiff3 three way merge tool that is available for most platform. So this is a three way merge. After successfully merging, commit your changes

REBASING CHANGES

If you don't have any conflicting changes that you want merge & you don't want to leave trace of the branch that was merged, use re-base to replay the change on top of the branch you want to merge to

+ git checkout <branch to be rebased>

+ git rebase master  --> assumming you intent to merge/move the change on top of master branch

+ git mergetool  --> if conflict arises, resolve by including the changes from local & remote

+ git rebase --continue

### CREATING & PUSHING TO REMOTE

+ git fetch origin master --> I now want to push my changes backup to origin master.
+ git push -u origin master --> It's going to push those changes up to

 Now to push/expose branch from local to remote 
+ git push origin <branch name> --> It's going to create a new branch coming over to remote or GitHub. You should now have a new branch on the repo

 DELETING & COPYING BRANCH

+ git push origin <branch>:<copy of branch> --> creates copy of branch in remote or GitHub

+ git push origin :<branch>  --> You just have to Leave local branch name empty, put a colon and then specify that remote branch name
