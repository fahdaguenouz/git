# git


## Setting Up Git

* Installing the git 

    - sudo apt install git-all

    - git --version 


* Configure Git with username and email addres
    
    - git config --global user.name "fahd"
    - git config --global user.email "faguenouz@gmail.com"

## Git commits to commit



* creation directory **work** with subdirectory **hello** inside the       folder hello generating a file named **hello.sh** 

* writing **echo "Hello, World"** in the hello.sh file 
* navigate to hello directory and initialize the directory using the   command **git init** 
* checking the status using **git status** and it says the hello.sh untracked
* after checking the status i added the file to track it with **git add hello.sh**
* committing the changes with a message using **git commit -m "commiting the hello.sh"**
* changing the content of the hello.sh to **#!/bin/bash echo "Hello $1"**
* stging the file and commiting it with a message **changing the content of the hello.sh**
* checking if the working tree is clean with git status it says **On branch master nothing to commit, working tree clean**
* changing the content of the hello.sh and adding just the comment with a commit 
* adding now the lines 4 and 5 and verifier that with **git log** and **git show**

## History

* showing the history using **git log**
* showwing on-line history using **git log --oneline**
* Controlled Entries:

    - customize the log output to display the last 2 entries using **git log --oneline -n 2**
    - customize the log oytput to display the commit made the last 5 min using **git log --oneline --since="5 minutes ago"**

* Personalized Format
    - showing logs personalized format using **git log --pretty=format:'* %h %ad | %s (%d) [%an]' --date=short**
     - "h" refere to the hash of the commit 
     - "ad"date of the commit to format it "--date=short"
     - "s" refere to commit message
     - "d" branch info 
     - "an" the author name

## Check it out

* Restore First Snapshot
    - Revert the working tree to the initial state using **git rev-list  --max-parents=0 HEAD**
     This command asks Git to list all the commits starting from HEAD but filter them down to only those with zero parents, which means it only returns the very first commit in the history of the repository.
    - after that runing the **git checkout b4a54bc4b2f63803bbda754ddbe2302ff044a6a6** to detached to head state
    - runing cat hello.sh to see the content of the hello.sh
    
* Restore Second Recent Snapshot
    -  Revert working tree ti thr second most recent snapshot usong **git rev-list HEAD | sed -n '2p'**
    and checkout and cat hello.sh

* Return to Latest Version
    - return to the last working directory using **git checkout master**

## TAG me

* Referencing Current Version
   - tag the current version of the repo using **git tag v1**
* Tagging Previous Version
   - tag the version immediately prior to the current version using **git tag v1-beta HEAD^**
* Navigating Tagged Versions
    - Move back and forth between the two tagged versions, v1 and v1-beta using **git checkout v1** and **git checkout v1-beta** use git status to see the detail 
* Listing Tags
    - listing all the tags using **git tag**

## Changed your mind

* Reverting Changes
    - Modify the latest version of the file with unwanted comments, then revert it back to its original state before staging using **git restore hello.sh**
    -the same thing but this time after staging them and remove them using **git restore --staged hello.sh** and **git restore hello.sh** 
* Committing and Reverting
    -making te same think but this time after staging it and committing it using **git revert HEAD**
* Tagging and Removing Commits
    - taging the last commit oops using **git tag oops** and ramove commits made after the v1 using **git reset --hard v1**
* Displaying Logs with Deleted Commits
    - show the log with the deleted commits using **git reflog** that display history

* Cleaning Unreferenced Commits

    - Ensure that unreferenced commits are deleted from the history using   **git gc --prune=now**
* Author Information
    - Add an author comment to the file and commit the changes
    - update the file and without committing it using **git commit --amend --no-edit** no edite to not chnage the message of the commit 

## Move it

* Moving hello.sh
    - creating the lib directory and moving the hello.sh to it using **mkdir lib** and **git mv hello.sh lib/**
    - creating the makefile in the hello directory 

## blobs, trees and commits

* Exploring .git/ Directory
    - runing ls -ls .git/objects to see the details of each one of objects and the refs and the config  
* Latest Object Hash
    - to  find the last object hash within the .git/objects using **git log -1 --pretty=%H** and to print the type of it **git cat-file -t 438240c3cc4f707b8fd0150334be6a1ed6406b5f**
    to print the content of it **git cat-file -p 438240c3cc4f707b8fd0150334be6a1ed6406b5f**
* Dumping Directory Tree
    - to dump the directory tree referenced we take the tree from the last command and run it like this  **git cat-file -p 9d592a14368f33d37b344b247204fdbb159dad2a**
    - to dump the content of the lib/ direcetory **git cat-file -p fbc167d8653e802da318ca77804e5ffe5a53064a**
    and for the hello.sh file **git cat-file -p 25477498cfde5872ba81ef6abb1a294b1b72758b**

## Branching 

* Create and Switch to New Branch
    - Create a local branch named greet and switch to it using **git checkout -b greet**
    - creating the file and putting the data in it  and committing it 
    - Updating the lib/hello.sh file  and commit the changes
    - updating the Makefile and commit the changes
    - switching to the main branch and comparing the makefile and hello.sh and greeter.sh **git checkout master** and **git diff master..greet -- Makefile hello.sh lib/greeter.sh**
    - generate the readme file 
    - draw the tree diagram using **git log  --graph --all** 
    
* commit 721a5c44b5f6c3930f0748c88ae9f16c0719be64 (HEAD -> master)
| Author: fahd <faguenouz@gmail.com>
| Date:   Fri Sep 27 16:51:41 2024 +0100
| 
|     Add README.md file with the provided content
|   
| * commit 9fad8027d1c43349354f37b07dfe41230c0bc439 (greet)
| | Author: fahd <faguenouz@gmail.com>
| | Date:   Fri Sep 27 16:32:57 2024 +0100
| | 
| |     updating the makefile
| | 
| * commit 5c9ed02e0cea3b47c88ace20c4d15ee2ae1c49b4
| | Author: fahd <faguenouz@gmail.com>
| | Date:   Fri Sep 27 16:31:37 2024 +0100
| | 
| |     updating the greeter file
| | 
| * commit 04acd52d17919ebb3bbddfdca4167ab75cfed0e9
|/  Author: fahd <faguenouz@gmail.com>
|   Date:   Fri Sep 27 16:30:25 2024 +0100
|   
|       creating the greeter file
| 
* commit 438240c3cc4f707b8fd0150334be6a1ed6406b5f (origin/fahd, fahd)
| Author: Fahd Aguenouz <fahd>
| Date:   Fri Sep 27 13:46:42 2024 +0100
| 
|     creating makefile
| 
:"
    
## Conflicts, merging and rebasing

* Merge Main into Greet Branch
    - merging the master branch into greet first chekcout to greet and  run **git merge master**
    - switching back to master and changing the hello.sh
* Merging Main into Greet Branch (Conflict)
    - after trying merging the master with greet and displaying this message 
    ""<<<<<<< HEAD
    # Changes from the greet branch
    echo "Hello, $my_name"
            =======
    # Changes from the Master branch
    echo "Hello, $name"
    >>>>>>> master""
    - Resolve the conflict  using **git config --global merge.tool meld** and after that **git mergetool**

* Rebasing Greet Branch
    - going back before the merge **git checkout 721a5c4**
    - rebase the greet **git rebase master**
* Merging Greet into Main
    - merging the greet into master 
* Understanding Fast-Forwarding and Differences
    - fast forwad merge :
    A fast-forward merge occurs when the branch you are merging into has not diverged from the branch you are merging. In other words, the target branch has not had any new commits since the branch you are merging off of was created.

    for example :
    A -- B -- C (main)
        \
         D -- E (feature)
    If you merge feature into main, and main has no new commits since B, the result will look like this
    A -- B -- C -- D -- E (main, feature)

    - Merging merge the commit and rebasing is rebase the main with the last commit from other brach 
    for example :
    A -- B -- C (main)
        \  
         D -- E (feature)

    it will be :
    A -- B -- C -- F (main)
        \     /
         D -- E

         
## Local and remote repositories

* making clone directory 
    - to clone a copy of hello we use **git clone hello cloned_hello**
    - to show the log **git log --oneline**
    - to display the name of the remote **git remote show origin**
    - list all the remote and local branches **git branch -a**
    - fetch the changes from the remote and diplay the logs **git fetch** **git log --oneline --all --graph --decorate**
    - merging the changes from the master the read me changed **git fetch** **git merge origin/master**
    this is what the red me in the clonned looks like :
            "This is the Hello World example from the git project.
        <<<<<<< HEAD
        =======
        (changed in the original)
        >>>>>>> origin/master
        "
    - tracking the remote origin/greet **git checkout -b greet origin/greet**
    - addding remote to the git repo and push the main and greet branches to the remote 
    - What is the single git command equivalent to what you did before to bring changes from remote to local main branch
    **git pull origin master**

## Bare repositories

* What is a bare repository and why is it needed
    - A bare repository in Git is a repository that contains only the version history of your project (the Git data), without the working files (i.e., no checked-out copies of the source code). It is used mainly for collaboration and as a central repository to which developers push and pull changes.
    - creating a bare repo from the hello using **git clone --bare . ../hello.git**
    - adding the bare repo to the remote to the origin repo **git remote add bare-origin ../hello.git**
    to verify **git remote -v**
    - chnaging the readme and commit it and push it to the shared repo using **git push bare-origin master**
    - switching to the clonned and pull the changes 