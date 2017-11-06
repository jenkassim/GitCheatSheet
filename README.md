# Git Cheat Sheet
#### How to use this cheat sheet
This sheet contains syntax examples for getting around with Git.
The first part deals with the quick and nitty way of working with repo on Git. This is useful if you just want to get things going on Git with complete workflow cycle, from getting the code onto your machine, syncing with the original remote repo, making changes and committing the code.
The second part list other necessary 'helper' commands to help you navigate around.
The third part covers some common command description.

Below describes the notation that's used in this sheet:
 >   $    denotes input command executables

 >   [ ] denotes the output examples from executables

 >-  denotes some notes / info

# Table of Content
## Part I   : Getting Git
- [The Gist of Git](#the-gist-of-git)


## Part II  : Git basic helper commands
- [Get Config Settings](#get-config-settings)
- [Get Status](#get-status)
- [View Log](#view-log)
- [Get Diff](#get-diff)
- [View Branches](#view-branches)
- [View Remote](#view-remote)


## Part III : Commands descriptions
- [Create A Fork](#create-a-fork)
- [Clone A Repo](#clone-a-repo)
- [Sync A Forked Repo](#sync-a-forked-repo)
- [Rebase To Remote](#rebase-to-remote)
- [Commits And Modifications](#commits-and-modifications)
- [Branches](#branches)
- [Remotes](#remotes)
- [Fetch](#fetch)
- [Pull](#pull)
- [Push](#push)
- [Merge](#merge)
- [Rebase](#rebase)
- [Tagging](#tagging)

# Part I   : Getting Git
As you probably have read everywhere else on the web, git is a distributed VCS, unlike other centralized VCS tool such as SVN. So if you are coming from a SVN-ish background, the main point to switch your mind's concept is that for Git, there's multiple redundant repository instead of a centralized repository.
For Git :

  ```
   Working directory   ---add--->   Index   ---commit---> HEAD
  ```
  Where,
  - Working directory : Is your local machine where it holds the actual files
  - Index : Acts as a staging area
  - HEAD  : Points to the last commit you made


## The Gist Of Git
  - This section describes the complete flow to work on github repository. Click the link to see each syntax description. At the end of each section, click on the **^** to get back to this section.

  - [Fork a repository](#create-a-fork)
    - Click on the Fork button on the respective repository on github

  - [Clone a repository](#clone-a-repo)
    - Gets a local working copy of the source

  - [Add remote](#add-remote) & [View remote](#view-remote)
    - A remote should be configured to point to an upstream repository in Git to sync changes between the initial repository with your own repo.

  - [Sync A Forked Repo](#sync-a-forked-repo)
    - If repo was forked from another repo, over time, the forked repo should be sync-ed with its source repo to get any latest changes made to it.

  - [Commits And Modifications](#commits-and-modifications)
    - Modifications to files for commit.

  - [Rebase to Remote](#rebase-to-remote)

# Part II  : Git basic commands

## Get config settings
- View list of configured user settings
  ```
    $ cat .git/config
  ```
## Get status
- Get status :
    `$ git status`

## View log
- View log :
  ```
    $ gitlog
    $ git log -l HEAD
  ```
## Get Diff
- Get stages / committed diff changes
  ```
    $ git show <commit-ID>
  ```
- Get diff between last check-in(HEAD) and current repo last checking:
  ```
    $ git diff HEAD
  ```
- Get diff made to staged files
  ```
    $ git diff --staged
  ```
- Preview any merge conflicts between branches
  ```
    $ git diff <source_branch> <target_branch>
  ```
- Get diff between SHA versions
  ```
    $ git diff <SHA ver1> <SHA ver2>
  ```
- Get 5th last commited diff
  ```
    $ git diff HEAD~5
  ```
- Get diff between 2nd last and last commit
  ```
    $ git diff HEAD^..HEAD
  ```
[^](#the-gist-of-git)


## View Branches
- Switch branches or restore working branch files
  ```
    $ git checkout <branch>
  ```
- View branches
- List all | remote | last commit
  ```
    $ git branch [-a | -r | -v ]
  ```
- View tracking info
  ```
    $ git branch [-vv | -av ]
  ```
- View merge info
  ```
    $ git branch [--merged | --no-merged]
  ```
[^](#the-gist-of-git)

## View Remote
- Show remote branches
  ```
    $ git remote -v
    $ git remove show <remote-name>
  ```
[^](#the-gist-of-git)


# Part III : Commands descriptions
## Create A Fork
- Git pushes only to matching branches: For every branch that exists on the local side, the remote side is updated if a branch with the same name already exists there.
- To create a fork, go to github and click on upper right button "fork"

## Clone A Repo
- Gets a local copy of the repo
  ```
    $ git clone -o <branchname> https://github.com/<YOUR-USERNAME>/<project-name>
  ```

- The shortcut clone command is a collective command of below :
  ```
  - Initialize git
    $ git init

  - Creates a pointer to its origin master branch and that pointer is named origin/master locally
  - Creates own local master branch starting at the same place[position/pointer] as origin's master branch at that point in time.
  - Auto fetch and merge the remote branch (origin/master) into your current (master) branch.    
    $ git fetch
    $ git pull origin master
  ```
[^](#the-gist-of-git)

## Sync A Forked Repo
- A remote needs to be configured so that it points to the upstream repository in Git and will sync any changes made to the original repo.
- This gets the updates from the original repo into local branch and pushes the updates into your forked branch, making your local and remote repo in sync with the original forked-from repo.

### Do Pull
- Get updates from remote source repo (where it was forked from)
  ```
    $ git pull <from remote repo> <to local branch>
  ```

### Do Merge
- Switch to branch
  ```
    $ git checkout <branch-name>
  ```
- Merge the latest changes from remote (upstream/master) into local master branch. This brings your fork's master branch into sync with the upstream repository, without losing your local changes.
  ```
    $ git merge <from branch> <to branch>
  ```

### Do Rebase
- Merge can also be replaced by using rebase, which re-writes your master branch so that your commits are replayed on top of the branch.
  ```
    $ git rebase <remote branch>
  ```

### Do Push
- Push to forked remote repo
  ```
    $ git push origin/master
  ```
[^](#the-gist-of-git)

## Rebase To Remote
- If remote repo was updated by others and your local repo version is not the latest, a push will cause an error. In the case of SVN, you'll need to do a svn update the local branch and resolve conflicts before being able to commit to the centralized repo.
- In Git, a rebase does the same thing, it will re-write your master branch changes to the remote repo so that your commits are replayed on the top of the changes.
  ```
    $ git pull --rebase <to remote branch><from local branch>
    $ git pull --rebase origin master

    $ git push <to remote branch><from local branch>
    $ git push origin master
  ```
[^](#the-gist-of-git)

## Commits And Modifications
  - To discard specific file changes in working directory and replace files with repo version
    ```
      $ git checkout -- <filename>
    ```

- To remove all changes in local branch
    ```    
      $ git rebase origin/master
      $ git reset --hard origin/master
    ```

### Staged-area
- Add changes to local repo staged-area
    ```
      $ git add .
      $ git add <filename>
    ```
- Remove files from staged-area
    ```
      $ git rm --cached <filename>
    ```      
- Remove newly added files from staged session
    ```
      $ git reset HEAD <filename>
    ```      

### Commit to HEAD
- Commit changes to local repo
  ```
    $ git commit <filename> -m "commit msg here"
  ```
- Adds to staging area and commits
  ```
    $ git commit -a -m "commit msg"
  ```

- Make/Add changes to the last commit
    ```  
      $ git commit --amend -m "amended commit msg to override the prev commit msg"
    ```     
- Undo prev commit, put changes into staging (^ refers to one rev before HEAD)
    ```  
      $ git reset --soft HEAD^
    ```

- Undo prev commit & revert all changes (^ refers to one rev before HEAD)
    ```  
      $ git reset --hard HEAD^
      $ git reset --hard HEAD^^ (undo last 2 commits and all changes)
    ```
[^](#the-gist-of-git)

## Branches
- A branch in Git is simply a lightweight movable pointer to one of these commits.
- The default branch name in Git is master (the tip of the 'trunk')
- As you start making commits, you’re given a master branch that points to the last commit you made.
- Every time you commit, it moves forward automatically.
- Creating a new branch, creates a new pointer to the local branch
- To move around, need to switch (git checkout)to that branch
- HEAD always points to latest commit on current working branch
- When HEAD moves, files in working directory will be reverted back to the snapshot that master points to
    (all current changes will be reverted in local working directory, but not in branch's staged area)

### Create New Branch
- To create a NEW branch locally
    ```
      $ git branch <branch-name>
    ```

### Switch Branches
- Switch branches or restore working tree files
- Updates files in the working branch to match the version in the index (staged) or the specified branch.
- If no paths specified, will also update HEAD to the specified branch as the current branch
    ```
      $ git checkout <branch-name>
    ```
- When switching branches, proceed even if the index or the working tree differs from HEAD. This is used to throw away local changes.
    ```
      $ git checkout -f <branch-name>
    ```
- Or Simplified command to create new branch and get HEAD version of specified branch
    ```
      $ git checkout -b <branch-name>
    ```
- List of branches available locally
- \* denotes the current/active branch working on
    ```
      $ git branch
          [ * master
              test2
          ]
    ```

### View Branches Status
- View branches that have been merged / unmerged into the master branch
- Branches on this list without the * in front of them are generally fine to delete with git branch -d; you’ve already incorporated their work into another branch, so you’re not going to lose anything.
  ````
    $ git branch [--merged | --no-merged]
        [   abcd
            * master
        ]
    ````
- View branches status in reference to revisions if local branch is ahead / behind of its remotes.

- Do execute fetch before getting updated view list, otherwise the references will be based on the last fetched from the remotes.
  ```
    $ git fetch --all
    $ git branch -vv
  ```

- Example :
  ```
    $ git branch -vv
        [  iss53     7e424c3 [origin/iss53: ahead 2] forgot the brackets
           master    1ae2a45 [origin/master] deploying index fix
           * serverfix f8674d9 [teamone/server-fix-good: ahead 3, behind 1] this should do it
           testing   5ea463a trying something new
        ]
  ```      
  - iss53 is tracking origin/iss53 : have 2 local commits that are not pushed to server
  - serverfix tracking teamone server : have 3 local commits and one server commit which havent merged into local branch


### Remove branches
- This removes branches that's not needed anymore or branches that's have already been merged.
  ```
    $ git branch -d <branch-name>
  ```

- This removes branches which have not been merged, having unresolved changes
  ```
    $ git branch -D <branch-name>
  ```

### Change Branch Remotes
- To change the remote it is tracking from (the relationship link)
  ```
    $ git branch --set-upstream-to <remote>/<branch>
    $ git branch -u origin/serverfix
        [
          Branch serverfix set up to track remote branch serverfix from origin.
        ]  
  ```

[^](#the-gist-of-git)

## Fetch
- Gets updated worked 'pushed' to remote repo since it was last cloned or fetched into own local, it will not modify/download to local working directory.
- Fetching from a repository grabs all the new remote-tracking branches and tags without merging those changes into your own branches.
- What this does is sets a remote-tracking branch called <remote>/<branch> with pointer movement to get new updated position on remote master.
- Note the command only takes remote name parameter and not the branch name, unlike the pull command.
  ```
    $ git fetch <remote-name>
    $ git fetch origin
        [
          remote: Counting objects: 3065, done.
          remote: Total 3065 (delta 0), reused 0 (delta 0), pack-reused 3065
          Receiving objects: 100% (3065/3065), 8.23 MiB | 1.27 MiB/s, done.
          Resolving deltas: 100% (1660/1660), done.
          From https://github.com/username/project-name
           * [new branch]      master     -> origin/master
        ]
  ```  
- Fetch all branches in the remote repo to local repo 'origin/master'
  ```
    $ git fetch [--all | origin]
        [ From https://github.com/username/project-name
           * [new branch]      master     -> origin/master
        ]
  ```

- To physically get files, need to manually merge to get all the changes into working directory, via pull
  ```
    $ git fetch origin
    $ git checkout master
    $ git merge origin
  ```
[^](#the-gist-of-git)

## Pull
- Pull command is equivalent to git fetch + merge
- If you have a tracking branch set up either by explicitly setting, git pull will look up what server and branch your current branch is tracking, fetch from that server and then try to merge in that remote branch.
- If branch is a tracking branch, pull command doesn't need input params
  ```
    $ git pull <remote> <branch>
    $ git pull upstream master
        [
            remote: Counting objects: 3028, done.
            remote: Total 3028 (delta 0), reused 0 (delta 0), pack-reused 3028
            Receiving objects: 100% (3028/3028), 8.10 MiB | 1.36 MiB/s, done.
            Resolving deltas: 100% (1639/1639), done.
            From https://github.com/username/<project-name>
             * branch            master  <branch-name>   -> FETCH_HEAD
             * [new branch]      master     -> origin/master
        ]
  ```
[^](#the-gist-of-git)

## Push
- Local branches needs to synchronize to the remotes - explicitly push the branch to collaborate.
- Push commited changes to repo
  ```
    $ git push <remote name> <local branch name>
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
- Note: DO NOT do git reset / commit --amend after doing git push

[^](#the-gist-of-git)

## Remotes
### Tracking Branches
- Remote tracking branches are references to the state of remote branches. Checking out a local branch from a remote-tracking branch auto creates a "tracking branch"
- They take the form <remote>/<branch> (refs to remote branches)
- Tracking branches are local branches that have a direct relationship to a remote branch.
- Origin/master points to the last known commit on the remote branch. If the remote's forked-from master (source of forked branch) updates and move forward, origin/master will still remain at the same location until updated.
- Branch it tracks from is usually called an "upstream branch"
- Tracking branches can directly call git pull and knows which server to fetch from and branch to merge into.
- When branches are tracked :
  ```
  master(local) -> 'tracks' -> origin/master (remote)
  ```
- Also when origin/master was forked from a different repo(someone's else github account), it can setup another remote to be able to sync updates
  ```
  master(local) -> 'tracks' -> upstream/master (remote's fork source)
  ```

- Remote details are stored in file .git/config

### Add Remote
- Branch is auto named origin if not specified
  ```
    $ git remote add <branch-name> https://github.com/username/<open-source-project-name>.git
    $ git remote add upstream https://github.com/username/<open-source-project-name>.git
  ```
[^](#the-gist-of-git)

### View Remote
- Show all remote relationship
  ```
    $ git remote -v
        [
          origin    https://github.com/YOUR_USERNAME/YOUR_FORK.git (fetch)
          origin    https://github.com/YOUR_USERNAME/YOUR_FORK.git (push)
          upstream  https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY.git (fetch)
          upstream  https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY.git (push)    [
        ]
  ```
[^](#the-gist-of-git)

### Change remote
  ```
    $ git remote set-url origin <new-remote-url>
  ```

### Rename Remote
  ```
    $ git remote rename <old-remote-name> <new-remote-remotename>
  ```

### Remove Remote
- This remove the relationship between local and remote but does not remove the actual branch
  ```
    $ git remote rm <remote-name>
  ```

### Remove Remote Branches
- To delete branches already on remote (ie branches created from master)
- This removes pointer from the server
  ```
    $ git push <remote> --delete <branch-name>
  ```

- To delete local branches which have been removed from remote, remove stale references
  ```
    $ git remote prune <branchname>
  ```
[^](#the-gist-of-git)

## Merge
- Merges specific branch in current working directory
- Merge is non-destructive operation, existing branches aren't changed in any way.
- Cons are history of merged into branch will have entire history branch merged from.
  ```
    - Switch to branch to merge INTO
      $ git checkout <to branch>

    - Merge FROM branch
      $ git merge <from branch>
  ```

- Single liner to do merge
  ```
      $ git merge <from branch> <to branch>
  ```  
- Merge terminology:
  - Fast-forward : Merged directly, like adding an additional node at the end of master, pointer just moves forward
  - Recursive strategy : Merged into a diverged path. Git does a 3-way merge using multiple snapshots pointed by branch tip

[^](#the-gist-of-git)

## Rebase
### Rebase rule of thumb
> Rebases are how changes should pass from the top of hierarchy downwards and merges are how they flow back upwards.

- Patching changes from a branched-out branch and merging it back into the diverged location.
- Going to common ancestor of two or more branches, gets the diff patch for all commits, saves to temp files and applying patch to rebase onto branch(master)
- Rebasing results in a perfectly linear history, this is done by re-writing commits history.
  ```
    $ git checkout <rebase from>
    $ git rebase <rebase to>
  ```
- When encountered with merge conflicts, mark Merge rebase conflicts as completed
  ```
    $ git rebase --continue
    $ git rebase --skip
    $ git rebase --abort
  ```
- When pulling changes from origin/master onto your local master use rebase.
- When finishing a feature branch merge the changes back to master.

### Rebase scenarios
- Branch abc branched-out from master, to rebase abc back into master
  ```
    $ git checkout abc
    $ git rebase master
  ```

- Git is able to rebase from multiple level branched out locations.
  - Rebase from 1-level branched out (master branch out to server branch)
  - Want to rebase from server branch back to master branch
  - This replays changes to server on top of master branch
  ```
    $ git rebase <base branch> <topic branch>
    $ git rebase master server
    $ git checkout master
    $ git merge server
  ```

  - Rebase from 2-level branched out (master branched out to server; server branched out to client)
  - master branch-to server (1st level) and server branch-to client(2nd level)
  - Only rebase from 2nd level branch back to master branch, leaving changes in 1st level out of rebase.
  - Takes client branch, figure out patches since it diverged from server branch and replay patches in client as though it was based directly off masster branch.
  ```
    $ git rebase --onto master server client
    $ git checkout master
    $ git merge client
  ```

- Note : always only rebase local changes made, which haven't been pushed to server; as it can modify the history and revert changes on those remotes.

[^](#the-gist-of-git)

## Tagging
- A tag is a reference to a commit (usually for release versioning)
- List of tag in branch
  ```
    $ git tag
        [v0.0.1
         v0.0.2]
  ```

- Checkout based on tag reference
  ```
    $ git checkout v0.0.1
  ```
- Create new tag
  ```
    $ git tag -a v.0.0.3 -m "tag msg"
  ```
- Push new tags to remove
  ```
    $ git push --tags
  ```
      - Verify remote added origin:
          $ git remote -v
[^](#the-gist-of-git)
