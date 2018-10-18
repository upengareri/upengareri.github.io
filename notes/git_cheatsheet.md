---
layout: single
title: <span style="color:#ABB2B9">Github Cheatsheet</span>
date: 2018-10-16

---


### Check git version installed on your machine
&emsp;&emsp;`git --version`

### Create a new repository
1. Go to the project directory
2. Run `git init`

### &emsp;&emsp;&emsp;&emsp;&emsp;&emsp; _<span style="color:orange">or</span>_

### Clone an existing repository
Cloning is the process of downloading a copy of the repository from a server.
&emsp;&emsp;`git clone [repository url]`

> _Note: HTTPS is the recommended url. You might be asked for your Github username and password._<br/>
No need to `git init` in this case as it automatically does it.

### Check status of the repository
&emsp;&emsp;`git status`

<p style="font-family: 'Lucida Console';color:#181818; background-color:#FEFEFE; padding: 1em; border-radius: 4px;">
	<b>WORKFLOW THEORY:</b><br/>
	local repository consists of three trees maintained by git.<br/>
	1. <b>Working Directory</b> which holds the actual files.<br/>
	2. <b>Index</b> which acts as a staging area. It's like telling git to track.<br/>
	3. <b>Head</b> which points to the last commit you've made. Technically, points to the branch(master by defalut) which points to the last commit you have made.<br/>
	So, first any changes in your working directory has to be added to the staging area. After that, you need to finally commit the staging area to the Head.<br/>
</p>

### Add file(s) to the staging area (INDEX)
&emsp;&emsp;`git add <filename>`&emsp;`[adds modified file]`<br/>
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;**<span style="color:orange">or</span>**<br/>
&emsp;&emsp;`git add *`&emsp;`[adds all modified files]`<br/>
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;**<span style="color:orange">or</span>**<br/>
&emsp;&emsp;`git add '*.py'`&emsp;`[adds modified files with .py extension]`


### Tell git not to track file anymore
> If you have manually deleted any file from your working directory and you no longer want to track it<br/>
&emsp;&emsp;`git rm filename`<br/>
If the filename is within a folder<br/> 
&emsp;&emsp;`git rm folder/filename`<br/>
If it was a directory that you deleted<br/> 
&emsp;&emsp;`git rm -r folder`

> If you have not manually deleted any file but just want to ignore or untrack that file<br/>
&emsp;&emsp;`git rm --cached filename`

> To both delete (automatically) as well as untrack file at the same time<br/>
&emsp;&emsp;`git rm -f filename`<br/>
**Warning:** This will delete the file from your working directory

### Commit file(s) (HEAD)
&emsp;&emsp;`git commit -m "Some message about the changes you made"`

> _Note: The file is committed to the **HEAD**, but not in your **REMOTE** repository yet_

### Push changes to remote (online) repository
&emsp;&emsp;`git push -u origin master`
> - _This is when you have cloned an existing repository._<br/>
> - master is the name of the branch and origin is the default name of the repository<br/>
> - -u links the local branch with remote branch so that later we can use git pull without arguments

&emsp;&emsp;`git push add origin <server_url>`
> - _This is when you have not cloned an existing repository and want to connect to a new repository._<br/>
> - _You need to go to github.com, create a new repository and use the repository's url._

### View all branches
&emsp;&emsp;`git branch`

### Create branch
&emsp;&emsp;`git branch <feature_x>`

### Switch to a branch
&emsp;&emsp;`git checkout <feature_x>`

### Create branch and switch to it
&emsp;&emsp;`git checkout -b <feature_x>`

### Delete a branch (soft delete)
&emsp;&emsp;`git branch -d <feature_x>`
> It'll complain if the branch is not merged 

### Delete a branch (hard delete)
&emsp;&emsp;`git branch -D <feature_x>`
> It'll not complain if the branch is not merged 

### Merge one branch into another
> Switch to the branch you want to pull changes into<br/>
&emsp;&emsp;`git branch master`<br/>
Pull changes from another branch<br/>
&emsp;&emsp;`git merge feature_x`

### Pull down latest commit from remote to local repository
&emsp;&emsp;`git pull origin master`

### View all remote branches
&emsp;&emsp;`git branch --remote`

### View log (repository history)
&emsp;&emsp;`git log` 

> To see commits of a certain author:&emsp;  `git log --author=upen`<br/>
To see each commit is one line:&emsp;&emsp; `git log --pretty=online`<br/>
To see which files changed in every commit: `git log --name-status`<br/>
To see art tree of all branches:&emsp; `git log --graph --oneline --decorate --all`


### Edit a commit
> To edit a commit message<br/>
&emsp;&emsp;`git commit --ammend`<br/> 
&emsp;&emsp;`git commit --ammend -m "New message"` 

>Did you forget to add a file?<br/>
&emsp;&emsp;`git add forgotten_file`<br/>
&emsp;&emsp;`git commit --ammend`  

### View unstaged changes to files
&emsp;&emsp;`git diff` 

### Unstage a file
&emsp;&emsp;`git reset filename` 

### Undo last commit and move commit changes to staging
&emsp;&emsp;`git reset --soft HEAD^` 

### Undo last commit and drop all your local changes
&emsp;&emsp;`git reset --hard HEAD^` 

### Save current changes, without having to stage or commit 
&emsp;&emsp;`git stash` [>This is done in case you are wor]ing on something messy and let's say your boss
pops out of nowhere and now you have to show him/her your working feature. You can thus
use this command to save all your local and stage changes somewhere, and now you are on last clean commit.

### To return to those changes
&emsp;&emsp;`git stash pop`


## For in-depth understanding of git: 
[Git Pro ebook](https://book.git-scm.com/book/en/v2])

















