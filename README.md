# Git basics

Git is a free and open-source distributed version control system designed to handle everything from small to very large projects with speed and efficiency.

From this article, you will learn how to:
- Create and work with Git repo.
- Define Git branches, create, and work on branches.
- Understand HEAD pointer.
- Merge branches.
    - Use fast-forward merge and delete branches.
    - Use 3-way merge.
    - Resolve merge conflicts.
- Work with a detached HEAD state.
- Work with Git stash.

This article contains a specific case and explanations of commands.


## Create and work with Git repo

Git repo tracks and saves the history of all changes made to the files in a project.

Run the following commands:
``````
mkdir netauto
`````` 
The command creates a new directory named *netauto* in a file system.
``````
cd netauto
``````
The command changes the current working directory to *netauto*.
``````
git init
``````
The command initializes an empty Git repo in the current directory.
``````
vi s1 
``````
The command opens the file *s1* *(you are to edit the file)*.
``````
wq!
``````
The command closes the file and saves the changes.
``````
git add s1
``````
The command adds the file *s1*.
``````
git commit -m "create s1"
``````
The command makes a commit named *"create s1"*.
``````
cp s1 s2
``````
The command copies the file *s1* to the file *s2*.
``````
git add s2.
``````
The command adds the file *s2*.
``````
git commit -m "create s2"
``````
The command makes a commit named *"create s2"*.
``````
git log
``````
The command displays made commits.
``````
git status
``````
The command displays the state of the working directory and the staging area.

After creating a new repo, main branch has a name *master*.
 

## Define Git branches, create, and work on branches.

A branch represents an independent line of development. Branches allow you to work on different versions on the same files in parallel. Edits on one branch can be independent on work of other branches. You can incorporate, or you can merge changes from one branch into other branches.

![Git branch](https://github.com/marina-jpg/rsschool-cv/assets/124706815/37a62ef3-7167-40d8-95e4-ec429ecad51c)

Run the following commands:
``````
git branch SDN
``````
The command creates a branch named *SDN*.
``````
git branch auth
``````
The command creates a branch named *auth*.
``````
git checkout SDN
``````
The command moves to *SDN* branch.
``````
vi s1
`````` 
The command opens the file *s1* *(you are to add controller IP)*.
``````
wq!
 ``````
The command closes the file and saves the changes.
``````
git add s1
``````
The command adds the file *s1*.
``````
git commit -m "SDN for s1"
``````
The command makes a commit named *"SDN for s1"*.
``````
git checkout auth
``````
The command moves to *auth* branch.
``````
graph
``````
The command graphically displays commits with branches, in which they are created.

>*There are no commits in *auth* branch. You return to the files *s1* and *s2*. They are committed to *"create s2"*.*

``````
vi s1
``````
The command opens the file *s1* *(you are to add identification server)*.
``````
wq!
``````
The command closes the file and saves the changes.
``````
git status
``````
The command displays the state of the working directory and the staging area (changes in the file *s1*).
``````
git commit -a -m "auth for s1"
 ``````
The command commits all file changes in all branches named *"auth for s1"*.


## Understand HEAD pointer

HEAD is a pointer that normally points to a branch. HEAD usually points to a branch and not directly to a commit. It is sometimes called a symbolic pointer. HEAD pointer informs you what you have checked out. Default state is attached, where any manipulation to the history is automatically recorded to the branch HEAD referencing.

![HEAD pointer](https://github.com/marina-jpg/rsschool-cv/assets/124706815/3870fb1b-c85c-49d1-a87f-39afa1c6c115)
 
![HEAD pointer](https://github.com/marina-jpg/rsschool-cv/assets/124706815/55bb4cff-0364-4c86-80ec-3cbb6b1fe091)

![HEAD pointer](https://github.com/marina-jpg/rsschool-cv/assets/124706815/471e0cae-d6d5-4b93-b6a0-63eeab709856)


## Merge branches

### Use fast-forward merge and delete branches

Fast-forward merge can be performed when there is a direct linear path from the source branch to the target branch. In fast-forward merge, Git moves the source branch pointer to the target branch pointer without creating an extra merge commit.

Run the following commands:
``````
git checkout master
``````
The command moves to *master* branch.
``````
git diff master..SDN
`````` 
The command displays the difference between *master* branch and *SDN* branch.
``````
git merge SDN
``````
The command merges the current branch with *SDN* branch.
``````
git branch --merged
``````
The command displays merged branches.
``````
git branch -d SDN
``````
The command deletes *SDN* branch.


### Use 3-way merge

3-way merge is frequently used to merge two derived files into a common-ancestor or base version.

Run the following commands:
``````
git status
``````
The command displays the state of the working directory and the staging area.
``````
git merge auth
``````
The command merges the current branch with *auth* branch.

>*You have a commit message. You can accept the default message here, save, and exit. The merge is done. The output does not inform fast-forward merge like last time.  Merge made by the *recursive* strategy.*
``````
git branch --merged
``````
This command displays merged branches.
``````
git branch -d auth
``````
The command deletes *auth* branch.


## Resolve merge conflicts

Merge conflicts occur when competing changes are made to the same line of a file.

Run the following commands:
``````
git checkout –b dev
``````
The command creates a branch named *dev* and move to *dev* branch.
``````
vi s1 
``````
The command opens the file *s1*. *(you are to edit the file)*.
``````
wq!
``````
The command closes the file and saves changes.
``````
git diff
``````
The command displays new modifications.
``````
git commit -a -m "update s1 VLANs"
`````` 
The command makes a commit named *"update s1 VLANs"*.
``````
git checkout master
``````
The command moves to *master* branch.
``````
vi s1
``````
The command opens the file *s1* *(you are to edit the file in the lines where changes are made to *dev* branch)*.
``````
wq!
``````
The command closes the file and saves changes.
``````
git commit -a -m "update s1"
``````
The command makes a commit named *"update s1"*.
``````
git merge dev
``````
The command merges the current branch with *dev* branch.

>*Git informs: "Merge conflict is in the file s1".
If you try to merge master branch and dev branch, there is a conflict. Git cannot guess for you which one you want to merge commit.*

If you don't want to resolve a conflict here, run command: `git merge -abort`. The command stops merging.
``````
git status
``````
The command displays the state of the working directory and the staging area.
``````
vi s1
``````
The command opens the file *s1* *(you are to decide how you are merged file to look, edit the file for deleting conflicts)*.
``````
wq!
``````
The command closes the file and saves changes.
```````
git add s1
```````
The command adds the file *s1*.
``````
git commit
``````
>*We are in the process of merging. The command displays the default commit message is acceptable, saves the changes made, and ends the merge.*


## Work with a detached HEAD state

HEAD state occurs when the HEAD does not point to a branch.

Run the following commands:
``````
git log
``````
The command displays commit history.
``````
git checkout 96f5b29
``````
The command checks out a commit directly by its sha1-hash *(type the name of a commit (`git checkout "name of your commit"`))*.
>*Git informs: "You have the HEAD pointer directly referencing a commit not a branch." This is a detached HEAD.*
``````
git checkout master
``````
The command moves to *master* branch. *After this command, HEAD points to the branch again.*
``````
git branch stage
``````
The command creates a branch named *stage*.
``````
git checkout stage
``````
The command moves to *stage* branch.


## Work with Git stash

You can use `git stash` to store your changes when they are not ready to be committed, but you are to change to a different branch.

Run the following commands:

``````
git checkout master
``````
The command moves to *master* branch.
``````
vi s1 
``````
The command opens the file *s1* *(you are to edit the file *s1*)*.
`````` 
wq!
``````
The command closes the file and saves changes.
``````
git status
``````
The command displays the state of the working directory and the staging area (*changes for the file s1*).
``````
git checkout stage
``````
>*The command checks out the stage branch you made earlier. Git informs checking out the *stage* branch. Git can update your working tree and staging area. If Git does it, you can lose your recent changes to the file *s1*. Git stops you from deleting those changes. Git informs "You can commit changes, or you can run `git stash`."*
``````
git stash
``````
The command saves made changes. *You can apply your changes back later.*
``````
vi s1
``````
The command opens the file *s1* *(you are to edit the file *s1*, delete auth_server)*.
``````
wq!
``````
The command closes the file and saves changes.
``````
git stash
``````
The command saves changes. *You can apply your changes back later.*
``````
git stash list
``````
The command displays all stashes.
``````
git stash apply
``````
The command reapplies the most recent stash.
``````
git diff
``````
The command displays unsaved changes.

*There are two methods to go.*

- ***Method 1*** 
``````
git commit –a –m "remove auth"
``````
The command makes a commit named *"remove auth"*.

- ***Method 2*** 
``````
git stash pop
``````
The command applies the stash point and removes it from the list.
``````
git diff
``````
The command displays unsaved changes.
``````
git commit -a -m "remove auth"
``````
The command makes a commit named *"remove auth"*.
``````
git stash list
``````
The command displays stashes.
``````
git stash save
``````
The command provides a message with a stash and then your message.

To get more information about Git, follow [Pro Git book by Scott Chacon](https://git-scm.com/book/en/v2).
