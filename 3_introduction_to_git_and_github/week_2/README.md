# Notes: Week 2 - Using Git Locally

- [Notes: Week 2 - Using Git Locally](#notes-week-2---using-git-locally)
  - [Advanced Git Interaction](#advanced-git-interaction)
    - [Skipping the Staging Area](#skipping-the-staging-area)
    - [Getting more information about our changes](#getting-more-information-about-our-changes)
    - [Deleting and Renaming Files](#deleting-and-renaming-files)
    - [Advanced Git Cheat Sheet](#advanced-git-cheat-sheet)

## Advanced Git Interaction
### Skipping the Staging Area
Basic git workflow
- Make changes
- Stage them 
- Commit them

> The separate steps between staging and commiting allows us to stage several changes into one commit.

However, if we are sure that the current small changes are what we want to commit, we can skip staging and go directly to commit using `-a` flag to `git commit` command. This **`-a` flag automatically stages all files that is tracked and modified** before doing this commit, thereby allowing us to skip `git add` step. 

> `git commit -a` is not same as `git add` > `git commit`. `git commit -a` does not work on new files as they are not tracked. **It's just a shortcut to stage any changes to tracked files and commit them in one step**.
If the modified files has never been committed to the repo, we still need to use `git add` to track it first.

**Example**

Let's modify the `all_checks.py` file, which is already being tracked by git.
```
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   all_checks.py

no changes added to commit (use "git add" and/or "git commit -a")
```
So, now we can stage and commit in one step
```
$ git commit -a -m "Call check_reboot fn from main fn, exit with 1 on error"
[master cbc7dba] Call check_reboot fn from main fn, exit with 1 on error
 1 file changed, 4 insertions(+), 1 deletion(-)
```

Let's check the commit logs. 
```
$ git log
commit cbc7dba8833ec43f51700aeaa2e2822b761ec105 (HEAD -> master)
Author: prasanth-ntu <prasanththegalaxian@gmail.com>
Date:   Sun Feb 5 10:16:24 2023 +0800

    Call check_reboot fn from main fn, exit with 1 on error

commit 05343e7ca05fbaf4209c6ca7d9215bf23a630886
Author: prasanth-ntu <prasanththegalaxian@gmail.com>
Date:   Sun Feb 5 10:06:00 2023 +0800

    Add all checks py file that checks whether reboot required

commit 7dc5534c427eb36a9d1b2857b32c4be44db0d4af
Author: prasanth-ntu <prasanththegalaxian@gmail.com>
Date:   Sun Feb 5 06:54:48 2023 +0800

    Added periods at the end of print statements.

commit 8b5b272f7edeb99cd60cb505b81dc038543aeb32
Author: prasanth-ntu <prasanththegalaxian@gmail.com>
Date:   Sat Feb 4 18:08:36 2023 +0800

    Add new disk_usage.py file
```
We can see that the `HEAD` indicator has moved to our latest commit (currently checked-out snapshot).

**`Head`**
> Git uses `HEAD` alias to represent the currently checked-out snapshot of our project. In simple terms, think of `HEAD` as pointer to our current branch. 

When we use branches, `HEAD`  can be a commit in a different branch of the project. We can even use git to go back in time and have `HEAD`  representing old commit from before the last changes were applied. In all cases, `HEAD` indicates what the currently checked out snapshot is. This is how git marks our place in the project. Think of it as bookmark that we can use to keep track of where we are. Even if we have multiple books to read, the bookmark allows us to pick up right where we left off.

### Getting more information about our changes
We know `git log` shows us the list of commits made in the current Git repo along with commit message, author, and date of change.
```
$ git log
commit cbc7dba8833ec43f51700aeaa2e2822b761ec105 (HEAD -> master)
Author: prasanth-ntu <prasanththegalaxian@gmail.com>
Date:   Sun Feb 5 10:16:24 2023 +0800

    Call check_reboot fn from main fn, exit with 1 on error

commit 05343e7ca05fbaf4209c6ca7d9215bf23a630886
Author: prasanth-ntu <prasanththegalaxian@gmail.com>
Date:   Sun Feb 5 10:06:00 2023 +0800

    Add all checks py file that checks whether reboot required

commit 7dc5534c427eb36a9d1b2857b32c4be44db0d4af
Author: prasanth-ntu <prasanththegalaxian@gmail.com>
Date:   Sun Feb 5 06:54:48 2023 +0800

    Added periods at the end of print statements.

commit 8b5b272f7edeb99cd60cb505b81dc038543aeb32
Author: prasanth-ntu <prasanththegalaxian@gmail.com>
Date:   Sat Feb 4 18:08:36 2023 +0800

    Add new disk_usage.py file
```

If we also need to look at the actual lines changed in each commit, we can use the `-p` flag with `git log`. The p comes from patch which is equivalent to `diff -u` we learnt earlier in [week 1](./../week_1/README.md#before-version-control). We can use page up, page down, and the arrow keys to navigate/scroll the output. Using this option, we can quickly see what changes were made to the files in our repository. This can be especially useful if we're trying to track down a change that recently broke our tools.
```
$ git log -p
commit cbc7dba8833ec43f51700aeaa2e2822b761ec105 (HEAD -> master)
Author: prasanth-ntu <prasanththegalaxian@gmail.com>
Date:   Sun Feb 5 10:16:24 2023 +0800

    Call check_reboot fn from main fn, exit with 1 on error

diff --git a/all_checks.py b/all_checks.py
index ea7ff5a..f96abe4 100644
--- a/all_checks.py
+++ b/all_checks.py
@@ -1,8 +1,11 @@
 import os
+import sys

 def check_reboot():
     """Returns True if the computer has pending reboot."""
     return os.path.exist("/run/reboot-required")

 def main():
-    check_reboot()
\ No newline at end of file
+    if check_reboot():
+        print ("Pending Reboot")
+        sys.exit(1)
\ No newline at end of file

commit 05343e7ca05fbaf4209c6ca7d9215bf23a630886
Author: prasanth-ntu <prasanththegalaxian@gmail.com>
Date:   Sun Feb 5 10:06:00 2023 +0800

    Add all checks py file that checks whether reboot required

diff --git a/all_checks.py b/all_checks.py
:
```

If we need to look at the actual lines changed in a specific commit, we can use `git show <commit_id>`
```
$ git show 05343e7ca05fbaf4209c6ca7d9215bf23a630886
commit 05343e7ca05fbaf4209c6ca7d9215bf23a630886
Author: prasanth-ntu <prasanththegalaxian@gmail.com>
Date:   Sun Feb 5 10:06:00 2023 +0800

    Add all checks py file that checks whether reboot required

diff --git a/all_checks.py b/all_checks.py
new file mode 100644
index 0000000..ea7ff5a
--- /dev/null
+++ b/all_checks.py
@@ -0,0 +1,8 @@
+import os
+
+def check_reboot():
+    """Returns True if the computer has pending reboot."""
+    return os.path.exist("/run/reboot-required")
+
+def main():
+    check_reboot()
\ No newline at end of file
```

Using `git log --stat`, we can see some stats about the changes in the commit, like which files were changed and how many lines were added or removed.
```
$ git log --stat
commit cbc7dba8833ec43f51700aeaa2e2822b761ec105 (HEAD -> master)
Author: prasanth-ntu <prasanththegalaxian@gmail.com>
Date:   Sun Feb 5 10:16:24 2023 +0800

    Call check_reboot fn from main fn, exit with 1 on error

 all_checks.py | 5 ++++-
 1 file changed, 4 insertions(+), 1 deletion(-)

commit 05343e7ca05fbaf4209c6ca7d9215bf23a630886
Author: prasanth-ntu <prasanththegalaxian@gmail.com>
Date:   Sun Feb 5 10:06:00 2023 +0800

    Add all checks py file that checks whether reboot required

 all_checks.py | 8 ++++++++
 1 file changed, 8 insertions(+)

commit 7dc5534c427eb36a9d1b2857b32c4be44db0d4af
Author: prasanth-ntu <prasanththegalaxian@gmail.com>
Date:   Sun Feb 5 06:54:48 2023 +0800

    Added periods at the end of print statements.

 disk_usage.py | 22 +++++++++++++++++++++-
 1 file changed, 21 insertions(+), 1 deletion(-)

commit 8b5b272f7edeb99cd60cb505b81dc038543aeb32
Author: prasanth-ntu <prasanththegalaxian@gmail.com>
Date:   Sat Feb 4 18:08:36 2023 +0800

    Add new disk_usage.py file
:
```

Let's make some changes to a script and try out `git diff` command.
```
$ git diff all_checks.py
diff --git a/all_checks.py b/all_checks.py
index f96abe4..e33470f 100644
--- a/all_checks.py
+++ b/all_checks.py
@@ -8,4 +8,8 @@ def check_reboot():
 def main():
     if check_reboot():
         print ("Pending Reboot")
-        sys.exit(1)
\ No newline at end of file
+        sys.exit(1)
+    print ("Everything ok.")
+    sys.exit(0)
+
+main()
\ No newline at end of file
```

Alternatively, to review the changes before adding them to staging is to use `-p` flag with the `git add` command
```
$ git add -p
diff --git a/all_checks.py b/all_checks.py
index f96abe4..e33470f 100644
--- a/all_checks.py
+++ b/all_checks.py
@@ -8,4 +8,8 @@ def check_reboot():
 def main():
     if check_reboot():
         print ("Pending Reboot")
-        sys.exit(1)
\ No newline at end of file
+        sys.exit(1)
+    print ("Everything ok.")
+    sys.exit(0)
+
+main()
\ No newline at end of file
(1/1) Stage this hunk [y,n,q,a,d,e,?]? y
```

If we call `git diff`, it will not show us any changes because, it will only show unstaged changes by default.
```
$ git diff
```

So, we can use `git diff --staged` to show the changes that are staged, but not commited. So, we can see the actual staged changes before we call `git commit` 
```
$ git diff --staged
diff --git a/all_checks.py b/all_checks.py
index f96abe4..e33470f 100644
--- a/all_checks.py
+++ b/all_checks.py
@@ -8,4 +8,8 @@ def check_reboot():
 def main():
     if check_reboot():
         print ("Pending Reboot")
-        sys.exit(1)
\ No newline at end of file
+        sys.exit(1)
+    print ("Everything ok.")
+    sys.exit(0)
+
+main()
\ No newline at end of file
```

Now, let's commit the staged changes.
```
$ git commit -m "Add a message when everything is ok"
[master 45af652] Add a message when everything is ok
 1 file changed, 6 insertions(+), 2 deletions(-)
```

### Deleting and Renaming Files
To remove/delete a file, we can use `git rm` command
```
$ ls -l
total 4
-rw-r--r-- 1 Prasanth 197121 306 Feb  5 10:59 all_checks.py
-rw-r--r-- 1 Prasanth 197121 306 Feb  5 10:59 all_checks_del.py
-rw-r--r-- 1 Prasanth 197121 306 Feb  5 10:59 all_checks_rm.py
-rw-r--r-- 1 Prasanth 197121 655 Feb  5 06:47 disk_usage.py

$ git rm all_checks_rm.py
rm 'all_checks_rm.py'

$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        deleted:    all_checks_rm.py

$ git commit -m "Delete unneeded all checks file"
[master c20b806] Delete unneeded all checks file
 1 file changed, 15 deletions(-)
 delete mode 100644 all_checks_rm.py

```
After the `rm` command, the delete changes are added to staging.  

To rename an existing file, we can use `git mv` command
```
$ ls -l
total 3
-rw-r--r-- 1 Prasanth 197121 306 Feb  5 10:59 all_checks.py
-rw-r--r-- 1 Prasanth 197121 306 Feb  5 10:59 all_checks_del.py
-rw-r--r-- 1 Prasanth 197121 655 Feb  5 06:47 disk_usage.py

$ git mv all_checks_del.py all_checks_new.py

$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        renamed:    all_checks_del.py -> all_checks_new.py

$ git commit -m "Rename all_checks_del.py "
[master ee7dbbb] Rename all_checks_del.py
 1 file changed, 0 insertions(+), 0 deletions(-)
 rename all_checks_del.py => all_checks_new.py (100%)
```

To ignore file(s) that are automatically generated by scripts or OS generated artifacts, we need to ignore them so that they won't add noise to the output of git status. To do this, we can use `.gitignore` file. Inside this file, we can specify rules to tell git to which files to skip for the current repo.
```
$ ls -a -l
total 12
drwxr-xr-x 1 Prasanth 197121   0 Feb  5 11:18 ./
drwxr-xr-x 1 Prasanth 197121   0 Feb  4 17:47 ../
-rw-r--r-- 1 Prasanth 197121 102 Feb  5 11:18 .file_to_be_ignored
drwxr-xr-x 1 Prasanth 197121   0 Feb  5 11:19 .git/
-rw-r--r-- 1 Prasanth 197121 306 Feb  5 10:59 all_checks.py
-rw-r--r-- 1 Prasanth 197121 306 Feb  5 10:59 all_checks_new.py
-rw-r--r-- 1 Prasanth 197121 655 Feb  5 06:47 disk_usage.py
```
Let's create a `.gitignore` file containing the name of the file to be hidden `.file_to_be_ignored`. Then, add it to staging and then commit the staged changes.
```
$ echo .file_to_be_ignored > .gitignore

$ ls -l -a
total 17
drwxr-xr-x 1 Prasanth 197121   0 Feb  5 11:23 ./
drwxr-xr-x 1 Prasanth 197121   0 Feb  4 17:47 ../
-rw-r--r-- 1 Prasanth 197121 102 Feb  5 11:18 .file_to_be_ignored
drwxr-xr-x 1 Prasanth 197121   0 Feb  5 11:19 .git/
-rw-r--r-- 1 Prasanth 197121  20 Feb  5 11:23 .gitignore
-rw-r--r-- 1 Prasanth 197121 306 Feb  5 10:59 all_checks.py
-rw-r--r-- 1 Prasanth 197121 306 Feb  5 10:59 all_checks_new.py
-rw-r--r-- 1 Prasanth 197121 655 Feb  5 06:47 disk_usage.py

$ git add .gitignore

$ $ git commit -m "Add a gitignore file, ignoring .file_to_be_ignored"
[master f1e5e4a] Add a gitignore file, ignoring .file_to_be_ignored
 1 file changed, 1 insertion(+)
 create mode 100644 .gitignore
```

### Advanced Git Cheat Sheet
[Git Cheat Sheet](https://training.github.com/downloads/github-git-cheat-sheet.pdf)

| Command   | Explanation & Link |
| --------- | ------------------------- |
| `git commit -a` | [Stages files automatically](https://git-scm.com/docs/git-commit#Documentation/git-commit.txt---all) |
| `git log -p` | [Produces patch text](https://git-scm.com/docs/git-log#_generating_patch_text_with_p) | 
| `git show` | [Shows various objects](https://git-scm.com/docs/git-show) |
| `git diff` | [Is similar to the Linux `diff` command, and can show the differences in various commits](https://git-scm.com/docs/git-diff) |
| `git diff --staged` | [An alias to --cached, this will show all staged files compared to the named commit](https://git-scm.com/docs/git-diff) | 
| `git add -p` | [Allows a user to interactively review patches to add to the current commit](https://git-scm.com/docs/git-add) |
| `git mv` | [Similar to the Linux `mv` command, this moves a file](https://git-scm.com/docs/git-mv) |
| `git rm` | [Similar to the Linux `rm` command, this deletes, or removes a file](https://git-scm.com/docs/git-rm) |

`.gitignore` files -  to tell the git tool to intentionally ignore some files in a given Git repository. For example, this can be useful for configuration files or metadata files that a user may not want to check into the master branch. Check out more at: https://git-scm.com/docs/gitignore.

A few common examples of file patterns to exclude can be found [here](https://gist.github.com/octocat/9257657).