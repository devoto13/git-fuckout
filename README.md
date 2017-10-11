# git fuckout

Command to make `git checkout` fucking happen.

## Why?

```bash
~/my-repo (on feature/awesome) $ git checkout feature/cool
error: Your local changes to the following files would be overwritten by checkout:
	some-file.txt

~/my-repo (on feature/awesome) $

# WTF?! Oh, I have to stash changes...

~/my-repo (on feature/awesome) $ git stash -u
Saved working directory and index state WIP on feature/awesome: 6b6309d0 Some commit message
~/my-repo (on feature/awesome) $ git checkout feature/cool

# do some work on feature/cool

~/my-repo (on feature/cool) $ git checkout feature/awesome
~/my-repo (on feature/awesome) $ git stash pop
```

Life is too short for this shit. Especially when you do it regularly on many branches. So welcome `git fuckout` to do this fucking job.

```bash
~/my-repo (on feature/awesome) $ git fuckout feature/cool
~/my-repo (on feature/cool) $

# Yay! 
```

The name is an abbreviation from "**fuck**ing check**out**".

## What it does?

The idea is very simple. 

1. When you do `git fuckout <my-branch>` it checks if there are any local changes. If there are any tool will commit them into current branch and than perform usual `git checkout` command with same arguments as provided to `git fuckout`.

2. After `git checkout` is completed, tool will look for the commit with local changes it created when you switched from the branch and will perform a soft reset to transform this commit back into local changes. Note that this part is performed even if you use usual `git checkout` command for changing branch.

## Installation

Instructions below are for Mac OS, but steps for other platforms should be pretty similar.

```bash
$ git clone https://github.com/devoto13/git-fuckout.git
$ cd git-fuckout
$ ln -s `pwd`/git-fuckout /usr/local/bin/git-fuckout # link main executable to your $PATH
$ ln -s `pwd`/git-fuckout-completion.bash /usr/local/etc/bash_completion.d/git-fuckout-completion.bash # optionally add completion for command
$ ln -s `pwd`/hooks/post-checkout /path/to/my-repo/.git/hooks/post-checkout # should be done for every repo separately
``` 

## Usage

Simply `git fuckout <branch>`.