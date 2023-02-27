# Assessment instructions

*Note: The assessment was carried out in Linux VM using Qwiklabs*

# Introduction
In this lab, you'll use your knowledge of Git and Git commit history to check out an existing repo and make some changes to it. You'll also test what you learned about rolling back commits after bad changes in order to fix a script in the repo and run it to produce the correct output.

## What you'll do
- Check the status and history of an existing Git repo
- Create a branch
- Modify content on the branch
- Make rollback changes
- Merge the branch

## Start the lab

# Accessing the virtual machine
Please find one of the three relevant options below based on your device's operating system.

> Note: Working with Qwiklabs may be similar to the work you'd perform as an **IT Support Specialist**; you'll be interfacing with a cutting-edge technology that requires multiple steps to access, and perhaps healthy doses of patience and persistence(!). You'll also be using **SSH** to enter the labs -- a critical skill in IT Support that you’ll be able to practice through the labs.

## Option 1: Windows Users: Connecting to your VM
In this section, you will use the PuTTY Secure Shell (SSH) client and your VM’s External IP address to connect.

**Download your PPK key file**

You can download the VM’s private key file in the PuTTY-compatible PPK format from the Qwiklabs Start Lab page. Click on Download PPK.

**Connect to your VM using SSH and PuTTY**
1. You can download Putty from [here](https://the.earth.li/~sgtatham/putty/latest/w64/putty.exe)
2. In the Host Name (or IP address) box, enter username@external_ip_address. 
> Note: Replace username and external_ip_address with values provided in the lab
3. In the Connection list, expand SSH.
4. Then expand Auth by clicking on + icon.
5. Now, select the Credentials from the Auth list.
6. In the Private key file for authentication box, browse to the PPK file that you downloaded and double-click it.
7. Click on the Open button.
> Note: PPK file is to be imported into PuTTY tool using the Browse option available in it. It should not be opened directly but only to be used in PuTTY.
8. Click Yes when prompted to allow a first connection to this remote SSH server. Because you are using a key pair for authentication, you will not be prompted for a password.


## Option 2: OSX and Linux users: Connecting to your VM via SSH
**Download your VM’s private key file.**

You can download the private key file in PEM format from the Qwiklabs Start Lab page. Click on Download PEM.

**Connect to the VM using the local Terminal application**

A terminal is a program which provides a text-based interface for typing commands. Here you will use your terminal as an SSH client to connect with lab provided Linux VM.

1. Open the Terminal application.
   1. To open the terminal in Linux use the shortcut key Ctrl+Alt+t.
   2. To open terminal in Mac (OSX) enter cmd + space and search for terminal.
2. Enter the following commands.
> Note: Substitute the path/filename for the PEM file you downloaded, username and External IP Address.

You will most likely find the PEM file in Downloads. If you have not changed the download settings of your system, then the path of the PEM key will be `~/Downloads/qwikLABS-XXXXX.pem`

```chmod 600 ~/Downloads/qwikLABS-XXXXX.pem```

```ssh -i ~/Downloads/qwikLABS-XXXXX.pem username@External Ip Address```

## Explore repository
There is a Git repository named `food-scripts` consisting of a couple of food-related Python scripts.

Navigate to the repository using the following command:

```cd ~/food-scripts```

Now, list the files using the `ls` command. There are three files named **favorite_foods.log**, **food_count.py**, and **food_question.py**.

```ps
student-00-52eafef9dae2@linux-instance:~/food-scripts$ ls
favorite_foods.log  food_count.py  food_question.py
```

Let's explore each file. Use the cat command to view each file.

1. `favorite_foods.log`: This file consists of a list of food items. 

    You can view it using the following command: `cat favorite_foods.log`

    ```ps
    student-00-52eafef9dae2@linux-instance:~/food-scripts$ cat favorite_foods.log
    pie
    burgers
    pizza
    pie
    tacos
    fried chicken
    spaghetti
    rice
    cake
    broccoli
    cake
    cereal
    ```

2. `food_count.py`: This script returns a list of each food and the number of times the food appeared in the favorite_foods.log file.

    Let's execute the script food_count.py: `python food_count.py`

    ```ps
    student-00-52eafef9dae2@linux-instance:~/food-scripts$ ./food_count.py
    rice, 12
    burgers, 10
    fried chicken, 9
    pie, 8
    pizza, 7
    salad, 7
    avocados, 6
    tacos, 6
    ice cream, 5
    spaghetti, 5
    broccoli, 5
    bananas, 5
    fish, 4
    cake, 3
    strawberries, 3
    cereal, 3
    watermelon, 2
    ```

3. `food_question.py`: This prints a list of foods and prompts the user to enter one of those foods as their favorite. It then returns an answer of how many others in the list like that same food.
    
    Run the following command to see the output of food_question.py script: `python food_question.py`

    ```
    student-00-52eafef9dae2@linux-instance:~/food-scripts$ ./food_question.py
    Traceback (most recent call last):
    File "./food_question.py", line 10, in <module>
        if item not in counter:
    NameError: name 'item' is not defined
    ```

Uh oh , this gives us an error. One of your colleagues reports that this script was working fine until the most recent commit. We'll be fixing this error later during the lab.

# Understanding the repository
Let's use the following Git operations to understand the workflow of the repository:

- git status
- git log
- git branch

**Git status**: This displays paths that have differences between the index file and the current HEAD commit; paths that have differences between the working tree and the index file; and paths in the working tree that are not tracked by Git. You can view the status of the working tree using the command: `git status`

```ps
student-00-52eafef9dae2@linux-instance:~/food-scripts$ git status
On branch master
nothing to commit, working tree clean
```

**Git log**: This lists the commits done in the repository in reverse chronological order; that is, the most recent commits show up first. This command lists each commit with its SHA-1 checksum, the author's name and email, date, and the commit message. You can see logs by using the following command: `git log`

```ps
student-00-52eafef9dae2@linux-instance:~/food-scripts$ git log
commit 21cf376832fa6eace35c0bf9e4bae4a3400452e9
Author: Alex Cooper <alex_cooper@gmail.com>
Date:   Wed Jan 8 14:09:39 2020 +0530

    Rename item variable to food_item.

commit b8d00e33237b24ea1480c363edd972cf4b49eedf
Author: Alex Cooper <alex_cooper@gmail.com>
Date:   Wed Jan 8 14:08:35 2020 +0530

    Added file food_question.py that returns how many others in the list like that same food.
```

**Git branch**: Branches are a part of the everyday development process on the master branch. Git branches effectively function as a pointer to a snapshot of your changes. When you want to add a new feature or fix a bug, no matter how big or small, you spawn a new branch to encapsulate your changes. This makes it difficult for unstable code to get merged into the main codebase.

```ps
student-00-52eafef9dae2@linux-instance:~/food-scripts$ git branch
* master
```

## Configure Git
Before we move forward with the lab, let's configure Git. Git uses a username to associate commits with an identity. It does this by using the git config command. Set the Git username with the following command:

```git config user.name "Name"```

Replace Name with your name. Any future commits you push to GitHub from the command line will now be represented by this name. You can even use git config to change the name associated with your Git commits. This will only affect future commits and won't change the name used for past commits.

Let's set your email address to associate them with your Git commits.

```git config user.email "user@example.com"```

Replace user@example.com with your email-id. Any future commits you now push to GitHub will be associated with this email address. You can also use git config to change the user email associated with your Git commits.

# Add a new feature

In this section, we'll be modifying the repository to add a new feature, without affecting the current iteration. This new feature is designed to improve the food count (from the file `food_count.py`) output. So, create a branch named `improve-output` using the following command:

```git branch improve-output```

Move to the `improve-output` branch from the `master` branch.

```git checkout  improve-output```

```ps
student-00-52eafef9dae2@linux-instance:~/food-scripts$ git branch improve-outputstudent-00-52eafef9dae2@linux-instance:~/food-scripts$ git checkout improve-output
Switched to branch 'improve-output'
```

Here, you can modify the script file without disturbing the existing code. Once modified and tested, you can update the master branch with a working code.

Now, open `food_count.py` in the nano editor using the following command:

```nano food_count.py```

Add the line below before printing for loop in the `food_count.py` script:

```print("Favourite foods, from most popular to least popular")```

Save the file by pressing `Ctrl-o`, the Enter key, and `Ctrl-x`. Then run the script `food_count.py` again to see the output:

```./food_count.py```

```ps
student-00-52eafef9dae2@linux-instance:~/food-scripts$ ./food_count.py
Favourite foods, from most popular to least popular
rice, 12
burgers, 10
fried chicken, 9
pie, 8
salad, 7
pizza, 7
avocados, 6
tacos, 6
ice cream, 5
broccoli, 5
bananas, 5
spaghetti, 5
fish, 4
cereal, 3
cake, 3
strawberries, 3
watermelon, 2
student-00-52eafef9dae2@linux-instance:~/food-scripts$
```

After running the `food_count.py` script successfully, commit the changes from the `improve-output` branch by adding this script to the staging area using the following command:

```git add food_count.py```

Now, commit the changes you've done in the `improve-output` branch.

```git commit -m "Adding a line in the output describing the utility of food_count.py script"```

```ps
student-00-52eafef9dae2@linux-instance:~/food-scripts$ git add food_count.py
student-00-52eafef9dae2@linux-instance:~/food-scripts$ git commit -m "Adding a line in the output describing the utility of food_count.py script"
[improve-output 763594d] Adding a line in the output describing the utility of food_count.py script
 1 file changed, 1 insertion(+)
student-00-52eafef9dae2@linux-instance:~/food-scripts$ git log -2
commit 763594dc743f03479296caa672dbd7b277d7af28
Author: Prasanth <prasanththegalaxian@gmail.com>
Date:   Mon Feb 27 01:39:27 2023 +0000

    Adding a line in the output describing the utility of food_count.py script

commit 21cf376832fa6eace35c0bf9e4bae4a3400452e9
Author: Alex Cooper <alex_cooper@gmail.com>
Date:   Wed Jan 8 14:09:39 2020 +0530
```

# Fix the script
In this section, we'll fix the script `food_question.py`, which displayed an error when executing it. You can run the file again to view the error.

```./food_question.py```

This script gives us the error: `"NameError: name 'item' is not defined"` but your colleague says that the file was running fine before the most recent commit they did.

In this case, we'll revert back the previous commit.

For this, check the `git log` history so that you can revert back to the commit where it was working fine.

```ps
$ git log
commit 763594dc743f03479296caa672dbd7b277d7af28
Author: Prasanth <prasanththegalaxian@gmail.com>
Date:   Mon Feb 27 01:39:27 2023 +0000

    Adding a line in the output describing the utility of food_count.py script

commit 21cf376832fa6eace35c0bf9e4bae4a3400452e9
Author: Alex Cooper <alex_cooper@gmail.com>
Date:   Wed Jan 8 14:09:39 2020 +0530

    Rename item variable to food_item.

commit b8d00e33237b24ea1480c363edd972cf4b49eedf
Author: Alex Cooper <alex_cooper@gmail.com>
Date:   Wed Jan 8 14:08:35 2020 +0530

    Added file food_question.py that returns how many others in the list like that same food.

commit 8d5a3189b88d273ef08286e5074b5e38d616da21
Author: Alex Cooper <alex_cooper@gmail.com>
Date:   Wed Jan 8 14:07:15 2020 +0530
```

Here, you'll see the commits in reverse chronological order and find the commit having "Rename item variable to food_item" as a commit message. Make sure to note the commit ID for this particular commit.

To revert, use the following command:

```git revert [commit-ID]```

Replace ```[commit-ID]``` with the commit ID you noted earlier.

```ps
student-00-52eafef9dae2@linux-instance:~/food-scripts$ git revert 21cf3
[improve-output b0595f6] Revert "Rename item variable to food_item."
 1 file changed, 1 insertion(+), 1 deletion(-)
```

This creates a new commit again. You can continue with the default commit message on the screen or add your own commit message.

Then continue by clicking `Ctrl-o`, the Enter key, and `Ctrl-x`.`

Now, run `food_question.py` again and verify that it's working as intended.

```ps

student-00-52eafef9dae2@linux-instance:~/food-scripts$ ./food_question.py
Select your favorite food below:
burgers
fish
broccoli
watermelon
fried chicken
spaghetti
pizza
avocados
rice
cake
tacos
bananas
salad
pie
strawberries
cereal
ice cream
Which of the foods above is your favorite? fish
4 of your friends like fish as well!
```

# Merge operation
Before merging the branch `improve-output`, switch to the `master` branch from the current branch `improve-output` branch using the command below:

```ps
student-00-52eafef9dae2@linux-instance:~/food-scripts$ git checkout master
Switched to branch 'master'
```

Merge the branch improve-output into the master branch.

```ps
student-00-52eafef9dae2@linux-instance:~/food-scripts$ git merge improve-output
Updating 21cf376..b0595f6
Fast-forward
 food_count.py    | 1 +
 food_question.py | 2 +-
 2 files changed, 2 insertions(+), 1 deletion(-)
 ```

Now, all your changes made in the improve-output branch are on the master branch.

```./food_question.py```

To get the status from the master branch, use the command below:

```git status```

To track the git commit logs, use the following command:

```git log```