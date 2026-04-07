Learning git - Summary

1. General
git -v or git --version 
git config [--global | --local] --list
git config -h
git config --get user.name

2. Initialization
git config --global user.name "Name"
git config --global user.email "email@example.com"
git config --global init.defaultbranch main [very important]
git init
git clone [url]
git branch --show-current or git branch [and look for *]

3. Basic Snapshot Workflow
git status: Shows which files are modified, staged, or untracked
git diff: Shows exact line changes between files that are not yet staged
git add [file]: Adds a file to the staging area (preparing it for a commit)
git add .：Add all in the unstaged to the staging area
git commit -m "message"
git log

4. Branching & Merging
git branch: Lists all local branches; the one with an asterisk is current
git switch [branch-name]: modern way to change branches (vs git checkout)
git switch -c [branch-name]: modern way to create a new branch and switches to it
git merge [branch]: Combines changes from another branch into your current one

5. Working with Remotes
git remote add origin [url]: Connects local repository to a remote server - use once per local repo
git push origin [branch]: Sends your local commits to the remote repository
git push -u origin [branch]: Only if you want to push to a branch other than the default
git pull: Fetches updates from the remote and automatically merges them into your local branch [1, 8].
git fetch: Downloads updates from the remote but does not change your local code yet

6. Typical Flow
    1. Clone the repo (git pull)
    2. Create a new branch from main or another branch (git switch -c [branch])
    3. Make changes / git add . / git commit
    4. Push the branch to remote repo (git push)
    5. [github] Open a pull request
    6. Merge the changes
    7. Pull the merged changes into local repo
    8. Repeat step 2

7. Managing Conflicts
    1. git switch [incoming branch with conflicts e.g. main]
    2. git pull: restore the incoming branch to local repo]
    3. git switch [working branch - with conflicting PR]
    4. git merge [incoming branch]
    5. [IDE] for conflicts resolution
    6. git add . / git commit -m " .... resolution message ...."
    7. git push
    8. [github] Create a new PR / approve and merge

8. Clean up local repository
    1. If remote branch has been deleted : git fetch --prune 
    2. Delete merged local Branches
        2.1 git switch main (for an example)
        2.2 git pull: to get the latest main image from remote repo
        2.3 git branch --merged main: to find out which local branches have been merged
        2.4 git branch -d [branch to be deleted]

9. Savior
9.1 git reset: reset to a release before the hash, no trace after the hash
    1. git log
    2. git reset --soft [hash]
    3. git reset --hard [hash] - remove from working 
    4. git reset [hash] - changes retain in working (user to decide)
9.2 git revert: revert to a release before the hash, with all logs in between intact
    1. git log
    2. git revert [hash]
        2a. Resolve conflicts (if any)
            git add.
            git revert --continue
        2b. git revert --skip (skip current commit done by git revert --continue)
        2c. git revert --abort (back to original state)
9.3 git stash: push current work aside and resume afterwards
    1. [IDE] editing ....
    2. git stash: set the current changes aside into stash cache
    3. [IDE] editing urgent changes / git add . / git commit -m "...."
    4. git stash list: list out the current stach cache entries
    5. git stash apply ["stach@{index}] or git stash apply [index]
