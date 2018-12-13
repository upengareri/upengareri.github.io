---
layout: single
title: <span style="color:#62c462">Open sublime file from terminal</span>
date: 2018-12-13

---

After doing a lot of stuff in the command line, it becomes boring to go to GUI. For example, let's say I start a project, and I do something like this:

```bash
cd Desktop
mkdir project && cd project
touch readme.md
touch hello_world.py
git init
```

With just a few keystrokes I created my project folder and files and initialised a git repo. Now, to use sublime text I have to right click and open with the editor or drag the folder/file to the editor. In computer world, this is called <span style="color: #55acee;background-color: #1E242C;font-size:14px; font-family: 'Lucida Grande'">`context switching`</span> which in rough sense means going from one application to another. Context switching both in computer and in the real world is costly in terms of time. 

Coming to the point, we can use some tweaks to save this time and enable opening the files from the terminal itself.

### Checking if everything is working fine before starting

Running the below command should open the Sublime Text editor:

    open -a /Applications/Sublime\ Text.app

Similarly, in order to open any file we can also type something like:

    open -a /Applications/Sublime\ Text.app hello_world.py

We want to make life easy and save time but the problem in the above command is that it is too long to type which doesn't sound like saving time.

The solution to this problem is <span style="color: #55acee;background-color: #1E242C;font-size:14px; font-family: 'Lucida Grande'">`.bash_profile`</span>.

### A little background on `.bash_profile`
`.bash_profile` is one of the hidden files in our Mac. What it does is it loads the configuration and preferences of the command line interface when we open the terminal. 

> To view hidden files in any directory, type: <br/>
`ls -a` <br/>
> To view `.bash_profile`, type:<br/>
`cd ~` <br/>
`ls -a` 

> Learn more about some of the most important bash commands in my article - [command line cheatsheet](https://github.com/upengareri/data_science/blob/master/notes/terminal/command_line_cheats.md)

So, in order to make an alias or short name of the above open sublime command, we can add it to the `.bash_profile`.

### How to edit the .bash_profile and execute sublime shortcut

<span style="color: yellow;font-size:14px; font-family: 'Lucida Grande'">___Step I:___ </span><span style="color: #55acee;background-color: #1E242C;font-size:14px; font-family: 'Lucida Grande'"> Fire up the terminal and type:</span> <br/>

`cd ~` <br/>

This will take you to the home directory, where .bash_profile resides.

<span style="color: yellow;font-size:14px; font-family: 'Lucida Grande'">___Step II:___ </span><span style="color: #55acee;background-color: #1E242C;font-size:14px; font-family: 'Lucida Grande'"> Type:</span> <br/>

`vim .bash_profile` <br/>

This will open the .bash_profile in vim editor in terminal.


<span style="color: yellow;font-size:14px; font-family: 'Lucida Grande'">___Step III:___ </span><span style="color: #55acee;background-color: #1E242C;font-size:14px; font-family: 'Lucida Grande'"> Add below line to the end of your .bash_profile</span> <br/>

`alias sublime="open -a /Applications/Sublime\ Text.app"` <br/>

This will create a shortcut command `sublime` to open any file in sublime text editor.

<span style="color: yellow;font-size:14px; font-family: 'Lucida Grande'">___Step IV:___ </span><span style="color: #55acee;background-color: #1E242C;font-size:14px; font-family: 'Lucida Grande'"> Save changes by pressing `Esc` button and then typing:</span> <br/>

`:wq`

This command will save the changes and exit the text editor mode.

<span style="color: yellow;font-size:14px; font-family: 'Lucida Grande'">___Step V:___ </span><span style="color: #55acee;background-color: #1E242C;font-size:14px; font-family: 'Lucida Grande'"> Refresh or activate the new changes by typing: </span> <br/>

`source .bash_profile`

<span style="color: yellow;font-size:14px; font-family: 'Lucida Grande'">___Step VI:___ </span><span style="color: #55acee;background-color: #1E242C;font-size:14px; font-family: 'Lucida Grande'"> Now, in order to open any file, go to that directory and type: </span> <br/>

`sublime script.py`

Voila! Enjoy your hack.



