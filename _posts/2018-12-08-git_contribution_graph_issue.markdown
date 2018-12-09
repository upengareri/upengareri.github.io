---
layout: single
title:  "Git contribution graph issue"
date:   2018-12-08
---

Recently I have had this issue related to the github contribution graph. For a while, I was able to see the changes in the graph when pushing any commits to the server. But suddenly the graph stopped showing any contributions even though the files and commits were getting updated. 

![github contribution graph](../assets/images/git_contribution_graph.png)

The problem in my case was that my email somehow got misconfigured in my local machine settings.

`To check your git configuration, open your terminal and type:`
    
    git config --list

This will show you your username and email associated with the github account.
The username here is not the same as your github account username and you can change as many times as you want to anything.
The email part here is important for graph contribution.

___In my case email id was missing somehow and that is why the graph contribution was not updating.___

> Note: The email has to be the same one that you have provided in your github settings. 
> In order to check or add email address go to [https://github.com/settings/emails](https://github.com/settings/emails)


### How to fix the problem?

> `Set your email for a single repository`

`In the terminal, go from current directory to your local repository where you want to configure`
    
    git config user.email "email@example.com"

> `Set your email for every repository on your machine:`

    git config --global user.email "email@example.com"


> `To confirm the settings:`

    git config user.email

