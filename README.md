**Committing detached head**

`git checkout 6363c29d-20cb-5c38-bd6a-e4d754b556a7`

> for detached head mode

> add & commit changes

`git branch BRANCH_NAME`

> create a new branch with the committed changes

`git checkout master`

`git merge BRANCH_NAME `

**Bring back lost commit by git reset --hard using reflog**

`git reflog`

> copy COMMIT_ID

`git reset --hard COMMIT_ID`

**Bring back deleted branch using reflog**

`git reflog`

> copy COMMIT_ID

`git checkout COMMIT_ID`

> detached head mode

`git branch BRANCH_NAME`

> create branch same deleted branch name can be used, it will contain the changes

---

## Basic Commands Summary: General

`git --version`

`git init`

> create empty git repository

`git status`

> check working directory and staging area status

`git log`

> show all commits of current branch

`git ls-files`

> list data in staging area

## Basic Commands Summary: Commit Creation and Access

`git add FILE_NAME`

> add single file to staging area

`git add .`

> add all working directory files to staging area

`git commit -m "CUSTOM_MESSAGE"`

> create a new commit

`git checkout COMMIT_ID`

> checkout commit (detached head!)

## Basic Commands Summary: Branch Creation and Access

`git branch BRANCH_NAME`

> create new branch

`git checkout BRANCH_NAME`

> go to branch

`git checkout -b BRANCH_NAME`

> create and access new branch

`git merge OTHER_BRANCH`

> bring other branch's changes to current branch

## Basic Commands Summary: Deleting Data

### Working Directory File

`git rm FILE_NAME` && `git add FILE_NAME`

> run command after file was deleted from working directory

### Unstaged changes

`git checkout (--) .`

> revert changes in tracked files

`git restore FILE_NAME OR .`

> same as above

`git clean -dn`

> check Untracked files to be removed

`git clean -df`

> force delete untracked files

### Staged changes

`git reset FILE_NAME OR .`

> remove files from staging area

`git checkout -- FILE_NAME`

> same as above

`git restore --staged FILE_NAME OR .`

> same as above

### Latest commit

`git reset --soft HEAD~1`

> undo latest (~1) commit and put files in staging area, i.e., undo git commit -m

`git reset HEAD~1`

> undo latest (~1) commit and put files in untracked area, i.e., undo both git add FILE_NAME && git commit -m ""

`git reset --hard HEAD~1`

> undo latest (~1) commit along with files

### Branches

`git branch -D BRANCH_NAME`

> delete branch

## Deep Dive Summary [STASH, REFLOG, MERGE, REBASE, CHERRY_PICK, TAG]

1. Git Stash
   > temporary storage for unstaged and uncommitted changes

`git stash list`

> show all stash

`git stash push -m "CUSTOM_MESSAGE"`

> stash with custom message

`git stash apply STASH_NUMBER `

> apply selected stash

`git stash pop`

> apply and remove stash

`git stash drop STASH_NUMBER`

> delete stash

`git stash clear`

> clear all stash

2. Git Reflog
   > a log of all project changes made including deleted commits

   > allow us bring back lost information be it commit or branches

3. Git Merge
   > combine commits from different branches by creating a new merge commit (recursive) or by moving the HEAD (fast-forward)
   
   > Fast-Forward
   
   > Non Fast-Forward -> Recursive, Ours, Octopus, Subtree

`git merge OTHER_BRANCH`

> bring all commits without losing commit information, HEAD of the current branch was moved forward to OTHER_BRANCH

`git merge --squash OTHER_BRANCH`

> bring all changes while losing commit information in staging area

`git merge --no-ff OTHER_BRANCH`

> bring all changes with commit information and create a separate commit on top of that

`git merge --abort`

> return back to stage before merge command and abort merge in case of conflicts

`git log --merge`

> show only commits that are going to be merged

4. Git Rebase
   > Reapply commits on top of another base tip

`git rebase OTHER_BRANCH`

> change the base (i.e., the parent commit) of commits in another branch

`git rebase master`

> update base commit in current branch and COMMIT_ID all of existing commits

5. Git Cherrypick
   > Apply the changes introduced by some existing commits

`git cherry-pick COMMIT_ID`

> create new commit and copy changes using COMMIT_ID

6. Git Tag
   > Git supports two types of tags: lightweight and annotated

`git tag TAG_NAME COMMIT_ID`

> create a lightweight tag for a given commit

`git tag -a TAG_NAME -m CUSTOM_MESSAGE`

> create a annotated tag for a given commit

`git tag`

> list all tags

`git show TAG_NAME`

> show details of tag

`git tag -d TAG_NAME`

> delete tag

## Understanding Github

`git remote add origin URL`

> "Name of the remote machine" or alias/shorthand of the URL of the remote repository

> "origin" keyword is just a placeholder

`git push origin BRANCH_NAME`

> push to remote

`git branch -a`

> list all branches including remote tracking branches

`git branch -r`

> list all remote tracking branches

`git pull origin BRANCH_NAME`

> git fetch from remote branch and add into local tracking branch

> git merge into local branch

> git pull is a combination of fetch and merge

`git ls-remote`

> makes a network call and fetch branches from remote

`git fetch origin`

> fetch all branches from remote

`git branch --track BRANCH_NAME origin/BRANCH_NAME`

> creates a local tracking branch based on a remote branch

> local branch and remote branch names should match

> one can simply `git pull` and `git push` with local tracking branches

`git remote show origin`

> show detailed configuration

`git branch -vv`

> list local tracking branches and their remotes

`git branch --delete --remotes origin/BRANCH_NAME`

> delete remote tracking branch only

`git push origin --delete BRANCH_NAME`

> delete branch on remote along with its remote tracking branch

`git push --force origin master`

> delete commit on remote

> reset HEAD~1 and then force push
