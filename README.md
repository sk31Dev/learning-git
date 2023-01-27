# learning-git

A repository made for exploring git commands on a text file instead of actual projects.

Some of the commands used:

GIT
Command line basics
clear → clears the console

ls → List all the files and folders of directory, hidden files not included

ls -a → List all the files and folders of directory, hidden files are included

mkdir test → Creates a folder named test 

touch test.txt → Creates a .txt file with name as test

rm test.txt → Permanently deletes 

cat test.txt → Prints content of the file in console

For windows

ls -Force
cls/clear → clears the console

VIM
Default text editor for Git Bash
Commands can be written starting with vim or vi

vi test.txt → Opens the file in console in edit mode
Type to make changes in the file, observe 


Esc → switch to command mode
Insert → switch to insert or replace mode
dd → delete an entire line
hjkl or arrow keys → for navigating
u → Undo
:w → write out changes that were made
:q → exit Vim
:q! → exit Vim and discard any changes
:wq → saves the changes, and exits Vim
:x → save the changes made, and exits Vim

GIT commands
git init → Initialises a new git repository in your current folder
Creates a .git folder which will keep track of all the changes made in the file/folder structure as well as the contents of the files.


git add . → Put all files of the directory in the staging area

git add test.txt → Puts the test.txt file in staging area

git restore test.txt → Removes file from staging area

git status → Shows the changes/modifications made in the directory by you (added/removed files, changes in files)

git commit -m “your commit message” → Saves the changes/modifications
Commit is just a snapshot/milestone of changes made

git log → Views the commit history

Moving between commits

Each commit is built on top of each other, so you can move between different commits
Each commit has its own hashed id to keep track of an individual commit

git reset 7cb1419a95a43cbdfb9fb171227364c4963a95f8 → Resets to the provided commit id and moves modifications since the provided commit id to the unstaged area

Stashing
To save your uncommitted changes
Used when you don't want to commit your changes but don't want to lose them either
As the name suggests you can move your changes behind the stage making the working tree clean
Use with tracked files for untracked files use another syntax mentioned at the end of the command list, 

git stash →  Stash the changes in a dirty working directory away

git stash save "stash message" → Stash the changes with a message to keep track

git stash pop → Brings back the last stashed changes (changes removed from stash)

git stash clear → Clears the stash, changes in stash are lost forever

git stash list → To list your saved stashes

git stash apply stash@{x} → To apply/get back the uncommitted changes where x is 0,1,2...

git stash pop stash@{x} → To apply a stash and remove it from the stash list

git stash apply stash@{x} → To apply a stash and keep it in the stash list

git stash --include-untracked → Include untracked files in stash

git stash -all → Include all files in stash (ignored and untracked)

Guide on stashing: https://opensource.com/article/21/4/git-stash


GITHUB
Creating a repository on Github
In your local machine, setup git using git init command
Go to Github and create new repository, you should be able to see a repository URL
Copy the repository URL from Github and use command use the below command

git remote add origin https://github.com/Shubham7Nova/learning-git	

git remote -v → View the list of origins(repository URLs) attached with your directory

After you have connected your local repo with github you need to send the first set of changes to Github in the master branch for this use command

git push origin master 

BRANCHING
Git uses Directed Acyclic Graph for branching



Branching means creating a new copy of your code base and then adding changes to it so that the original code remains unaffected while you are making your new changes.

Head pointer is used by git to identify on which branch the new changes will be added

When you checkout a new branch the head points towards it hence your changes will get committed into the new branch instead of main.

git checkout main → switch to main branch, move head to the main branch

git checkout test-branch → If you have a branch named test-branch and you want to come on this branch

git branch new-branch → Creates a new branch named “new-branch”
git checkout new-branch → Switch to the new branch
git checkout -b my-new-branch → Creates a new branch with the name “my-new-branch”

Suppose you have made changes in your new branch and now you want to merge them to the main branch

git merge my-new-branch

Pull requests are used to get your code reviewed and merged in the main branch instead of direct merging.


FORKING
Prevents changes in your projects from other people
Create a copy of a project on Github in your own account so you can make changes to it
OEM’s fork AOSP maintained by Google to add their own custom features on Android
Go to a repository and at the top right you should see a button named Fork
Example of forking the dotnet core repository
https://github.com/Shubham7Nova/core
We can use the above URL now to clone this repository in our local machine and make changes, these changes will be sent over to our fork of the project instead of the original project.

Upstream URL → The URL of the original repository from where you forked a project

git remote add upstream https://github.com/dotnet/core.git → Will add dotnet core original project’s url as your upstream url



Pull requests
A process made by Git which requires you to get your code reviewed and approved before being merged
When you checkout on a branch and make changes and push them to Github, you will see an option to create a new Pull Request for merging your changes
You can open one pull request for one branch

Reverting a commit
Suppose you made 2 commits with ID A and B
Now you want to revert commit B from

git reset A

The changes of commit B will get moved to the unstaged area, stash them for later use

git stash

Now your PR must have both commits A and B but from your local machine you have removed commit B, when pushing this change you’ll have to use force push as there is a difference in commits.

git push origin reverting-commit -f

Keeping forked branch updated with main branch
If you are contributing to a big project the codebase of the main branch will get changed with time and you need to keep your fork updated with these changes

Method 1:
In Github use the sync fork button
 
Method 2:
Go to your fork’s main branch
git fetch –all –prune → To fetch all the branches along with deleted branches 
Now reset main branch of origin to main branch of upstream (moving head of your fork to the position where head of the original branch is), use the below command for this
git reset –hard upstream/main
Now we need to push these changes to the online repository use command 
git push origin main

Method 3:
Go to your fork’s main branch
git pull upstream/main (pull is a combination of fetch + reset)
git push origin main


SQUASHING COMMITS
Grouping a set of commits into one commit
Use rebase command for this
Suppose you have 4 commits A, B, C, D and you want to merge B, C and D into A
git rebase -i A
This will open an interactive window
	
Pick means all these commits are identified as unique and all 4 will be picked
Replace pick with s or squash for commits which you want to merge
	
Use :x to exit rebasing and add commit message
After adding commit message :x to exit


MERGE CONFLICTS
Occurs when the same line is changed by two commits. In this case git will ask for your intervention to decide what changes will get picked.
