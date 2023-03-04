# Notes: Week 3 - Working with Remotes

- [Notes: Week 3 - Working with Remotes](#notes-week-3---working-with-remotes)
  - [Introduction to GitHub](#introduction-to-github)
    - [Intro to Module 3: Working with Remotes](#intro-to-module-3-working-with-remotes)
    - [What is GitHub?](#what-is-github)
    - [Basic Interaction with Github Cheat-Sheet](#basic-interaction-with-github-cheat-sheet)
  - [Basic interaction with GitHub Cheat-Sheet](#basic-interaction-with-github-cheat-sheet-1)
  - [Using a Remote Repository](#using-a-remote-repository)
    - [What is a remote?](#what-is-a-remote)
    - [Working with Remotes](#working-with-remotes)
    - [Fetching New Changes](#fetching-new-changes)
    - [Updating the Local Repository](#updating-the-local-repository)
    - [Git Remotes Cheat-Sheet](#git-remotes-cheat-sheet)
  - [Solving Conflicts](#solving-conflicts)
    - [The Pull-Merge-Push Workflow](#the-pull-merge-push-workflow)
    - [Pushing Remote Branches](#pushing-remote-branches)
    - [Rebasing Your Changes](#rebasing-your-changes)
    - [Another Rebasing Example](#another-rebasing-example)
    - [Best Practices for Collaboration](#best-practices-for-collaboration)
    - [Conflict Resolution Cheat Sheet](#conflict-resolution-cheat-sheet)
- [To clarify](#to-clarify)

## Introduction to GitHub
### Intro to Module 3: Working with Remotes

### What is GitHub?
**Git** - Distributed Version Control System
> Distributed: Each developer has a copy of the whole repository on their local machine. Each copy is peer (equal) of the others. We can host one of these copies on the remote server and use it as a remote repository for other copies. This lets us synchronise work between copies through the server.

Either we can create/host our own git server, or use one of the off-the-shelf solutions like GitHub, GitLab, BitBucket, etc.  

**GitHub**
- Web-based Git repository hosting service. 
- On top of the version control functionality of Git, GitHub includes extra features like bug tracking, wikis, and task management. 
- GitHub lets us share and access repositories on the web and copy/clone them to our local computer, so we can work on them.
- GitHub provies free access to a Git server for public and private repositories. However, the number of contributors for free private repositories.

> For real configuration and development work, we should use a secure and private Git server, and limit the people authorized to work on it.

### Basic Interaction with Github Cheat-Sheet

- Using the web-based GitHub platform, we can create a fresh/new remote repository. 
  - https://github.com/prasanth-ntu/health-checks
- Then, we need to create a local copy of the repo using `git clone <repo-url>` in the terminal. This command will download the copy of the remote repo to our local machine.
  ```ps
  $ git clone https://github.com/prasanth-ntu/health-checks.git
  Cloning into 'health-checks'...
  remote: Enumerating objects: 3, done.
  remote: Counting objects: 100% (3/3), done.
  remote: Compressing objects: 100% (2/2), done.
  remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
  Receiving objects: 100% (3/3), done.

  $ cd health-checks/

  $ ls -a -l
  total 9
  drwxr-xr-x 1 Prasanth 197121  0 Feb 28 06:53 ./
  drwxr-xr-x 1 Prasanth 197121  0 Feb 28 06:53 ../
  drwxr-xr-x 1 Prasanth 197121  0 Feb 28 06:53 .git/
  -rw-r--r-- 1 Prasanth 197121 65 Feb 28 06:53 README.md
  ```
- Then, `cd` into the repo folder and `ls` to see its contents.
- Let's add some content by opening it with `code README.md`. Add a new line "This repo will be populated with lots of fancy checks."
- Let's stage the change and commit it
  ```ps
  $ git commit -a -m "Add one more line to README.md"
  [main 3d00c9c] Add one more line to README.md
  1 file changed, 2 insertions(+)
  ```
- Let's send our changes made in our local repository to remote repostiory set up on GitHub by using `push` command that will gather all the snapshots we have taken and send them to remote repo.
  - GitHub will ask for username and password. However, in this case, it didn't ask for username and password as we have already setup the credentials globally in the past.
  ```ps
  git push
  Enumerating objects: 5, done.
  Counting objects: 100% (5/5), done.
  Delta compression using up to 8 threads
  Compressing objects: 100% (2/2), done.
  Writing objects: 100% (3/3), 361 bytes | 361.00 KiB/s, done.
  Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
  To https://github.com/prasanth-ntu/health-checks.git
    b5ffeb2..3d00c9c  main -> main
  ```
  ![health-checks.md after ](attachments/health-checks-readme-after-first-push.png)
- Few ways we can avoid typing password everytime we run `git push
  - Use SSH key-pair and store the public key in our profile so that GitHub recognizes our computer.
  - Another option is to use credential helper which caches our credentials for a time window so that we don't need to enter password with every interaction. Git already comes with credential helper, and we just need to enable it using `git config --global credential.helper cache`, and enter credentials one more time, which will then cache our credentials for 15 mins.
- Let's run `git pull` to retrieve new changes from repo.
  ```ps
  $ git pull
  Already up to date.
  ``` 

## Basic interaction with GitHub Cheat-Sheet
There are various remote repository hosting sites:
- GitHub
- BitBucket
- Gitlab

Some useful commands to getting started

| Command | Explanation & Link |
|---------------------------|----------------------------------------|
| `git clone URL` | [Git clone is used to clone a remote repository into a local workspace](https://git-scm.com/docs/git-clone) |
| `git push` | [Git push is used to push commits from your local repo to a remote repo](https://git-scm.com/docs/git-push) |
| `git pull` | [Git pull is used to fetch the newest updates from a remote repository](https://git-scm.com/docs/git-pull) |

This can be useful for keeping your local workspace up to date.
- https://help.github.com/en/articles/caching-your-github-password-in-git
- https://help.github.com/en/articles/generating-an-ssh-key  

---

## Using a Remote Repository
### What is a remote?
- Remote repositories are big part of distributed nature of git collaboraiton.
- It lets lots of collaborators contribute to a project from their own workstations making changes to local copies of the project independently of one another. When they need to share their changes, they can issue git commands to pull code from a remote repository or push code into one. 
- There are many ways to host remote repos
  - There is many internet based git hosting providers like GitHub, BitBucket, GitLav, etc.
  - We can also setup a Git server on our own network to host private repos, which offers increased proivacy, control, and customization.
- Using Git to manage a project helps us collaborate successfully.
- If someone has updated a repository since the last time you synchornize your local copy, Git will tell us it's time to an update by asking us to `pull`. If we have your own local changes when we pull down the code from the remote repo, we might need to fix `merge` conflicts before we can `push` our own changes. This way Git let's multiple people work on the same project at the same time.
  ![Pull Merge Push cycle from local to remote repo](attachments/pull-merge-push-to-remote.png)
- When working with remotes, the workflow for making changes has some extra steps
  - We will still modify, stage, and commit our local changes
  - After commiting, we'll fetch any new changes from remote repo manually merge if necessary and only then will push our changes to our remote repo

### Working with Remotes
When we do `git clone` to get local copy of remote repo, Git setups up that remote repo with the default `origin` name. We can look at the configuration for that remote by running `git remote -v` in the directory of the repo. There will be two URLs, which usually point at the same place:
1. To fetch data from the remote repo
2. To push date to the remote repo
```ps
$ git remote -v
origin  https://github.com/prasanth-ntu/coursera_google_it_aut_with_python.git (fetch)
origin  https://github.com/prasanth-ntu/coursera_google_it_aut_with_python.git (push)
```

> The default names assinged to remote repositories is `origin`.

This lets us track more than one remote in same git directory. To get even more info about our remote, we can call `git remote show origin` that provides ton of info.
- We can see fetch and push url, as well as remote and local branch too.
- For now, we only have `main` branch that exists locally and remotely. 
  - Once we start having more and difference branches, this info becomes more complex
```ps
$ git remote show origin
* remote origin
  Fetch URL: https://github.com/prasanth-ntu/coursera_google_it_aut_with_python.git
  Push  URL: https://github.com/prasanth-ntu/coursera_google_it_aut_with_python.git
  HEAD branch: main
  Remote branch:
    main tracked
  Local branch configured for 'git pull':
    main merges with remote main
  Local ref configured for 'git push':
    main pushes to main (up to date)
```

Whenever we are working with remote repos, Git uses remote branches to keep copies of the data that's stored in the remote repository. We can look at the remote branches that Git repo is currently tracking by running `git branch -r`
- These branches are read only. We can look at the commit history of these remote branches, but we cannot make changes to them directly. To modify their contents, we need to go through the workflow discussed earlier: pull > merge > push.
```ps
$ git branch -r
  origin/HEAD -> origin/main
  origin/main
```

We can also use `git status` to check the status of our changes in remote branches as well.
- It tells us that our local branch is upto date with `origin/master` branch => The master branch in remote repo called `origin` has the same commits as our local `master` branch.
```ps
$ git status
On branch main
Your branch is up to date with 'origin/main'.

nothing to commit. working tree clean
```

### Fetching New Changes
```ps
$ git remote show origin
* remote origin
  Fetch URL: https://github.com/prasanth-ntu/health-checks.git
  Push  URL: https://github.com/prasanth-ntu/health-checks.git
  HEAD branch: main
  Remote branch:
    main tracked
  Local branch configured for 'git pull':
    main merges with remote main
  Local ref configured for 'git push':
    main pushes to main (up to date)
```
Here, it says the local branch is *up to date* with remote branch.

Now, lets a new file `temp.txt` with commit message "Added this temp.txt file to try out git fetch", and try the git command again. This time, it will show that the local branch is *out of date*. This happens when there were commit done to the repo that are not yet reflected locally. 
```ps
$ git remote show origin
* remote origin
  Fetch URL: https://github.com/prasanth-ntu/health-checks.git
  Push  URL: https://github.com/prasanth-ntu/health-checks.git
  HEAD branch: main
  Remote branch:
    main tracked
  Local branch configured for 'git pull':
    main merges with remote main
  Local ref configured for 'git push':
    main pushes to main (local out of date)
```

Git does not keep remote and local branches in sync automatically. It waits until we execute commands to move data around when we are ready. To sync data, we use `git fetch` command that copies the commits done in remote repo to the remote branches locally, so we can see what other people have commited using `git log origin/main. 
```ps
$ git fetch
fatal: credential-cache unavailable; no unix socket support
remote: Enumerating objects: 4, done.
remote: Counting objects: 100% (4/4), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), 708 bytes | 78.00 KiB/s, done.
From https://github.com/prasanth-ntu/health-checks
   3d00c9c..b108c19  main       -> origin/main

$ git log origin/main 
commit b108c19986fe355130353c79e537929bad2c2a0c (origin/main, origin/HEAD)
Author: Prasanth <prasanththegalaxian@gmail.com>
Date:   Tue Feb 28 08:32:02 2023 +0800

    Added this temp.txt file to try out git fetch

commit 3d00c9ce91927c054e3bcd1fdd10bf1170ea4ee8 (HEAD -> main)
Author: prasanth-ntu <prasanththegalaxian@gmail.com>
Date:   Tue Feb 28 06:58:58 2023 +0800

    Add one more line to README.md

commit b5ffeb2f1ffcb255f6b5312425d30a8525c22844
Author: Prasanth <prasanththegalaxian@gmail.com>
Date:   Tue Feb 28 06:52:39 2023 +0800
```
From the output, we can see that the `remote origin/main` is pointing to the latest commit that we made directly in GitHubs web-interface. However, the `local main` branch is pointing to the previous commit we made earlier on. 

When we run `git status`, it will tell us that there's a commit in `remote origin/main` that we don't have in our `local main` branch.
```ps
$ git status
On branch main
Your branch is behind 'origin/main' by 1 commit, and can be fast-forwarded.
  (use "git pull" to update your local branch)

nothing to commit, working tree clean
```

To integrate the remote branch to our local main branch, we could perform merge operation `git merge origin/main`, which merges the `origin/main` branch into our local `main` branch.
```ps
$ git merge origin/main
Updating 3d00c9c..b108c19
Fast-forward
 temp.txt | 1 +
 1 file changed, 1 insertion(+)
 create mode 100644 temp.txt
```
So, we successfully merged the changes of master branch of the remote repo into our local branch. During the merge operation, Git also tells us that the code was integrated using **fast-forward**. It also shows that one file was added "temp.txt".

If we look at the log output on our branch now, we should see the new commit.
```ps
$ git log origin/main
commit b108c19986fe355130353c79e537929bad2c2a0c (HEAD -> main, origin/main, origin/HEAD)
Author: Prasanth <prasanththegalaxian@gmail.com>
Date:   Tue Feb 28 08:32:02 2023 +0800

    Added this temp.txt file to try out git fetch

commit 3d00c9ce91927c054e3bcd1fdd10bf1170ea4ee8
Author: prasanth-ntu <prasanththegalaxian@gmail.com>
Date:   Tue Feb 28 06:58:58 2023 +0800

    Add one more line to README.md

commit b5ffeb2f1ffcb255f6b5312425d30a8525c22844
Author: Prasanth <prasanththegalaxian@gmail.com
```
> Using, `git fetch`, we can review the changes/commits made to our remote repo. Use `git merge` to integrate them into our local branch.

### Updating the Local Repository

Basic workflow when working with remotes: fetch > merge > push. Since fetching and merging are so common, git offers us `git pull` that does both.

> `git pull` will fetch the remote copy of the current branch, and automatically try to merge it into the current local branch.

I have done few changes to remote repo via GitHub Web-UI.
1. Modified `temp.txt` by adding additional lines in `main` branch
2. Created a new branch `experimental` and added `temp_in_experimental.txt`

Let's run `git pull` to see what changes we get. 
```ps
4 git pull
remote: Enumerating objects: 8, done.
remote: Counting objects: 100% (8/8), done.
remote: Compressing objects: 100% (6/6), done.
remote: Total 6 (delta 1), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (6/6), 1.38 KiB | 128.00 KiB/s, done.
From https://github.com/prasanth-ntu/health-checks
   b108c19..6ef7555  main         -> origin/main
 * [new branch]      experimental -> origin/experimental
Updating b108c19..6ef7555
Fast-forward
 temp.txt | 3 +++
 1 file changed, 3 insertions(+)
```
The output the results of both `fetch` and `merge` commands that we saw earlier. First, git fetched the updated contents from the remote repo, including new branch.
```ps
  b108c19..6ef7555  main         -> origin/main
* [new branch]      experimental -> origin/experimental
```
Then, it did a fast forward `merge` to the local branch `main`. We can see that `temp.txt` file was updated as well.
```ps
Fast-forward
 temp.txt | 3 +++
 1 file changed, 3 insertions(+)
```
We can look at the changes made to the file using `git log -p -1`
```ps
git log -p -1
commit 6ef75558674cc0e18d9d384496926cf99bb1f0e2 (HEAD -> main, origin/main, origin/HEAD)
Author: Prasanth <prasanththegalaxian@gmail.com>
Date:   Tue Feb 28 09:01:28 2023 +0800

    Update temp.txt

diff --git a/temp.txt b/temp.txt
index 1410f7b..39fd38e 100644
--- a/temp.txt
+++ b/temp.txt
@@ -1 +1,4 @@
 Added this file to try out git fetch
+Adding few more lines to try out git pull
+Adding line 3
+Adding line 4
```

When we run `git pull`, we also saw that a new remote branch named `experimental` was created. Let's checkout the output of `git remote show origin` and see what it says about the new branch.
```ps
git remote show origin    
* remote origin
  Fetch URL: https://github.com/prasanth-ntu/health-checks.git
  Push  URL: https://github.com/prasanth-ntu/health-checks.git
  HEAD branch: main
  Remote branches:
    experimental tracked
    main         tracked
  Local branch configured for 'git pull':
    main merges with remote main
  Local ref configured for 'git push':
    main pushes to main (up to date)
```  
We can see that for the new remote branch `experimental`, we do not have a local branch, yet. So, lets create a local branch for it by running `git checkout experimental`. Interestingly, when we checkout the `experimental` branch, Git automatically copied the contents of the experimental branch.
```ps
$ git branch
* main
$ git checkout experimental
Switched to a new branch 'experimental'
branch 'experimental' set up to track 'origin/experimental'.
$ git branch
* experimental
  main
$ ls
README.md  temp.txt  temp_in_experimental.txt
```
In this example, we got the contents of the `experimental` branch together with those of the `main` branch, when we called `git pull`, which also merge new changes to our `main` branch locally. If we want to get the contents of the remote branches without automatically merging any contents into our local branches, we can call `git remote update`. This will fetch the contents of all remote branches, so that we can just call checkout or merge as needed.  

### Git Remotes Cheat-Sheet
| Command                | Explanation & Links |
|------------------------|---------------------|
| git remote             | [Lists remote repos](https://git-scm.com/docs/git-remote) |
| git remote -v          | [List remote repos verbosely](https://git-scm.com/docs/git-remote#Documentation/git-remote.txt--v) |
| git remote show <name> | [Describes a single remote repo](https://git-scm.com/docs/git-remote#Documentation/git-remote.txt-emshowem) |
| git remote update      | [Fetches the most up-to-date objects](https://git-scm.com/docs/git-remote#Documentation/git-remote.txt-emupdateem) |
| git fetch              | [Downloads specific objects](https://git-scm.com/docs/git-fetch) |
| git branch -r          | [Lists remote branches](https://git-scm.com/docs/git-branch#Documentation/git-branch.txt--r); can be combined with other branch arguments to manage remote branches |

You can also see more in the video [Cryptography in Action](https://www.coursera.org/learn/it-security) from the course [IT Security: Defense against the digital dark arts](https://www.coursera.org/learn/it-security/home/welcome).

---
## Solving Conflicts
### The Pull-Merge-Push Workflow
 

### Pushing Remote Branches


### Rebasing Your Changes


### Another Rebasing Example


### Best Practices for Collaboration


### Conflict Resolution Cheat Sheet


---

# To clarify
- `git remote update` vs. `git fetch`