# Hello World
### How to work with repo on Github

 > $ denotes executables

 > [] output from executables

 > - denotes notes and info

## 0) Git basics to get around 

    Working directory  --add-->  Index  --commit-->  HEAD

    Working Directory : where it holds the actual files
    Index : acts as staging area
    HEAD : points to the last commit you made
    Git functions as pointers to 'snapshots' in time, instead of actual file changes to be manipulated

#### Commands:

- Get status : 
    `$ git status`

- Get staged/committed diff changes : 
    `$ git show <commit ID>`

- Get repo details : 
    `$ cat .git/config`

- View log : 
    ```
    $ gitlog
    $ git log -l HEAD
    ```


- Get Diff : 
    ```
    $ git diff HEAD        // get diff between last checkin(HEAD) and current repo last checkin
    $ git diff --staged    // get diff made to staged files
    $ git diff <source_branch> <target_branch>   // preview any merge conflicts btw branches
    ```


- Switch branches or restore working branch files
    ```
    $ git checkout <branch>
    ```


- View branches
    ```
        $ git branch [-a | -r | -v ] // list all | remote | last commit
    or  $ git branch [-vv | -av ] // View tracking info
    or  $ git branch [--merged | --no-merged] 
    ```


- Show remote branches :
    ```
    $ git remote -v
    $ git remote show <remote-name>
    ```


- Push commited changes to repo
    ```
    $ git push <remote name> <branch name>
    ```


- Pull from remotes :
    ```
    $ git pull <remote name> <branch name>
    ```
    
## 1) Create fork on Github
- Git pushes only to matching branches: For every branch that exists on the local side, the remote side is updated if a branch with the same name already exists there. 

## 2) Create a local clone of fork

`   $ git clone -o <branchname> https://github.com/<YOUR-USERNAME>/<project-name>`


- Clone does these cmd :
    ```
    $ git init
    $ git remote add origin[url] //branch is auto named origin
    $ git pull origin master : 
        - Creates a pointer to its origin master branch and that pointer is named origin/master locally
        - Creates own local master branch starting at the same place[position/pointer] as origin's master branch at that point in time.
        - Auto fetch and merge the remote branch (origin/master) into your current branch.
    ```

- Verify remote added origin: 
    ```
    $ git remote -v
      [  origin  https://github.com/YOUR_USERNAME/YOUR_FORK.git (fetch)
         origin  https://github.com/YOUR_USERNAME/YOUR_FORK.git (push)
      ]
    ```

## 2b) Manually create local link to remote repo
- Git clone cmd does all the below automatically, manual instructions below:
- Configure Git to sync your fork with the original <project-name> repository

- Init git 
    ```
    $ git init
    ```


- To add a remote that points to the original-remote repo
    ```    
    $ git remote add <branchname> https://github.com/user/[openSourceProject].git
    ```


- Verify remote added origin: 
    ```
    $ git remote -v
    ```


- Get updated work 'pushed' to remote since last cloned / fetch and into local repo
- Only downloads the data to your local repository – it doesn’t automatically merge with current local branch.
- What this does is sets a remote-tracking branch called <remote>/<branch> to point to the commit
    ```
    $ git fetch <remote-name>
        [
          remote: Counting objects: 3065, done.
          remote: Total 3065 (delta 0), reused 0 (delta 0), pack-reused 3065
          Receiving objects: 100% (3065/3065), 8.23 MiB | 1.27 MiB/s, done.
          Resolving deltas: 100% (1660/1660), done.
          From https://github.com/teamone/project-name
           * [new branch]      master     -> origin/master
        ]
    ```


- Fetch all branches in the repo to local repo 'origin/master'
    ```
    $ git fetch [--all | origin]
        [ From https://github.com/teamone/<projectname>
           * [new branch]      master     -> origin/master
        ]
    ```


- If fetching new remote-tracking branch, no file downloaded locally. Only have pointer to <remote>/<branchname> that you cant modify.
- To get local copy of new branch, can base it off remote-tracking branch
    ```
    $ git checkout -b <localbranchname> <remote/branchname>
        [ Branch <localbranchname> set up to track remote branch <remote/branchname> from <remote>
          Switched to a new branch '<localbranchname>'
        ]
    ```


## 3) Modification to local staged files
- To create a NEW branch locally for local repo
    ```
    $ git branch <branchname>
    ```

- Switch branches or restore working tree files
- Updates files in the working branch to match the version in the index (staged) or the specified branch.
- If no paths specified, will also update HEAD to the specified branch as the current branch
    ```
    $ git checkout <branchname>

    - When switching branches, proceed even if the index or the working tree differs from HEAD. This is used to throw away local changes.

    $ git checkout -f <branchname>
    ```

    Or
- Simplified command to create new branch and get HEAD version of specified branch
    ```
    $ git checkout -b <branchname>
    ```

- List of branches available locally 
- \* denotes the current/active branch working on
    ```
    $ git branch
      [ * master
          test2
      ]
    ```


- Add changes to local repo "staged area"
    ```
        $ git add .
    or  $ git add <filename>
    ```


- Remove files from "staged area"
    ```
    $ git rm --cached <filename>
    ```


- Remove newly added files from staged session
    ```
    $ git reset HEAD <filename>
    ```

- To discard changes in working directory and replace files with repo version
    ```
    $ git checkout -- <filename>
    ```


- Commit changes to local repo
    ```
    $ git commit <filename> -m "commit msg here"
    ```


- Push commited changes to repo
    ```
    $ git push <remote name> <local branch name>
    ```


## 4) Branching in Git
- A branch in Git is simply a lightweight movable pointer to one of these commits. 
- The default branch name in Git is master (the tip of the 'trunk')
- As you start making commits, you’re given a master branch that points to the last commit you made. 
- Every time you commit, it moves forward automatically.
- Creating a new branch, creates a new pointer to the local branch
- To move around, need to switch (git checkout)to that branch
- HEAD always points to latest commit on current working branch
- When HEAD moves, files in working directory will be reverted back to the snapshot that master points to 
    (all current changes will be reverted in local working directory, but not in branch's staged area)

- View branches that have been merged / unmerged into the branch currently o
    ```
    $ git branch [--merged | --no-merged]
        [   iss53
            * master
        ]

    - Branches on this list without the * in front of them are generally fine to delete with git branch -d;
    - You’ve already incorporated their work into another branch, so you’re not going to lose anything.
    ```


## 5) Merging in Git
- Merge specific branch in current working branch
    ```
    $ git checkout <tobranch> //switch to branch to check INTO
    $ git merge <frombranch> //merge FROM branch
    ```


- To 'merge back branches into the trunk aka master' 
- After branched out, changes which have been commited/staged and already pushed to repo needs to merge back into master
    ```
    - Switched to branch to merge INTO
        $ git checkout master
    - Run the merge from branches back into master
        $ git merge <branchname>
    ```


- Merge terminology:
    - Fast-forward : Merged directly, like adding an additional node at the end of master, pointer just moves forward
    - Recursive strategy : Merged into a diverged path. Git does a 3-way merge using multiple snapshots pointed by branch tip


## 6) Remote repository 
- Remote tracking branches are references to the state of remote branches. 
- They take the form <remote>/<branch> (refs to remote branches)
- Acts as bookmarks to remind you where the branches in your remote repo were the last time you conected to them.
- Tracking branches are local branches that have a direct relationship to a remote branch.
- Origin/master points to the last known commit on the remote branch. If the remote's origin master (source of forked branch) updates and move forward, origin/master will still remain at the same location until updated.
- Git gives own local master branch starting at the same location as origin's master branch.

    ###### From Remote -> Local : Pull
    - To update / synchronize with origin
    ```
        $ git pull <remote name> <branch name>
    ```

    - Merge the changes from upstream/master into your local master branch. 
    - This brings your fork's master branch into sync with the upstream repository, without losing your local changes.

        `$ git rebase origin/master`

    - See part (8) for Fetch cmd


    ###### From Local -> Remote : Push
    - Push commited changes to repo
    ```
        $ git push <remote name> <local branch name>
        $ git push <remote> <localbranchname:toreponewbranchname>
    ```


- Remove any unused branches
    ```
    $ git branch -d <branchname>
    $ git branch -D <branchname> // Branches which have not been merged, having unresolved changes
    ```


- To delete remote branches
- This removes pointer from the server
    ```
    $ git push <remote> --delete <branchname>
    ```

## 7) Pushing
- Local branches needs to synchronize to the remotes - explicitly push the branch to collaborate.
    ```
    $ git push origin serverfix
        [
          Counting objects: 24, done.
          Delta compression using up to 8 threads.
          Compressing objects: 100% (15/15), done.
          Writing objects: 100% (24/24), 1.91 KiB | 0 bytes/s, done.
          Total 24 (delta 2), reused 0 (delta 0)
          To https://github.com/user/project
           * [new branch]      serverfix -> serverfix
        ]
    ```


## 8) Pulling
- Fetch command gets all the changes on server that you don't have yet, it will not modify working directory.
- It is a pointer movement for origin/master to get new updated position on remote master.
- Need to manually merge to get all the changes into working directory.
    ```
    $ git fetch origin
    $ git checkout master
    $ git merge origin
    ```


- Pull command is equivalent to git fetch + merge
- If you have a tracking branch set up either by explicitly setting it (2b) or created by clone/checkout command (2), git pull will look up what server and branch your current branch is tracking, fetch from that server and then try to merge in that remote branch.
- If branch is a tracking branch, pull cmd doesnt need input params
    ```
    $ git pull <remote> <branch>
    [
        remote: Counting objects: 3028, done.
        remote: Total 3028 (delta 0), reused 0 (delta 0), pack-reused 3028
        Receiving objects: 100% (3028/3028), 8.10 MiB | 1.36 MiB/s, done.
        Resolving deltas: 100% (1639/1639), done.
        From https://github.com/jenkassim/<project-name>
         * branch            master     -> FETCH_HEAD
         * [new branch]      master     -> origin/master
    ]
    ```


## 9) Tracking Branches
- Checking out a local branch from a remote-tracking branch auto creates a "tracking branch"
- Branch it tracks from is called an "upstream branch" (the remote branch)
- Tracking branches are local branches that have direct relationship to a remote branch.
- Tracking branches can directly call git pull and knows which server to fetch from and branch to merge into.

- When a repo is cloned : 
    master -> 'tracks' -> origin/master (remote)

- To change the remote it is tracking
    ```
    $ git branch --set-upstream-to <remote>/<branch>
    $ git branch -u origin/serverfix
        [
          Branch serverfix set up to track remote branch serverfix from origin.
        ]
    ```


- View branch tracking and if local branch is ahead / behind /etc 
    ```
    $ git branch -vv
        [  iss53     7e424c3 [origin/iss53: ahead 2] forgot the brackets
           master    1ae2a45 [origin/master] deploying index fix
           * serverfix f8674d9 [teamone/server-fix-good: ahead 3, behind 1] this should do it
           testing   5ea463a trying something new
        ]
        
        - iss53 is tracking origin/iss53 : have 2 local commits that are not pushed to server
        - serverfix tracking teamone server : have 3 local commits and one server commit which havent merged into local branch
    ```
        

- View is from last fetched from server is obtain from local cache
- Execute fetch before getting view list
    ```
    $ git fetch --all
    $ git branch -vv
    ```


## 10) Rebasing
- Patching changes from a branched out branch and merging it back into the diverged location.
- Going to common ancestor of two branches, gets the diff patch for all commits, saves to temp files and applying patch to rebase onto branch(master)
    ```
    $ git checkout <rebase from>
    $ git rebase <rebase to>
    ```

    - e.g: Branch abc branched from master, to rebase abc back into master
    ```
        $ git checkout abc
        $ git rebase master    
    ```

- Git able to rebase from multiple level branched out locations.
    ###### Rebase from 1-level branched out 
    - (master branch out to server branch)
    - Want to rebase from server branch back to master branch
    - This replays changes to server on top of master branch
    ```
        $ git rebase <base branch> <topic branch> 
        $ git rebase master server
        $ git checkout master
        $ git merge server
    ```

    ###### Rebase from 2-level branched out
    - (master branched out to server; server branched out to client)
        - master branch-to server (1st level) and server branch-to client(2nd level)
    - Only rebase from 2nd level branch back to master branch, leaving changes in 1st level out of rebase.
    - Takes client branch, figure out patches since it diverged from server branch and replay patches in client as though it was based directly off masster branch.
    ```
        $ git rebase --onto master server client
        $ git checkout master
        $ git merge client
    ```

- Note : always only rebase local changes made which haven't been pushed; never rebase anything that has been pushed somewhere.

