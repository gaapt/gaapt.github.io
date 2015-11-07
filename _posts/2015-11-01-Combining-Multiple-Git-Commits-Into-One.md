---
layout: post
title: Combining Multiple Git Commits Into One
---

I [previously wrote](http://sumof.xyz/Silly-Contributions/) about including small contributions in my projects. That being said, it often becomes necessary to combine multiple git commits into one.

Let's assume our multiples commits are located in the `features` branch:

```bash 
git checkout features
```

To combine our commits, we will use the following structure:

```bash
git rebase -i features
```

A command similar to the following will be retrieved:

```bash
pick 3ksk4f0 My first commit
pick d01jb3f My second commit
pick gf0b3b0 My third commit 

# Rebase 9frt191..gf0b3b0 onto 9frt191
#
# Commands:
#  p, pick = use commit
#  r, reword = use commit, but edit the commit message
#  e, edit = use commit, but stop for amending
#  s, squash = use commit, but meld into previous commit
#  f, fixup = like "squash", but discard this commit's log message
#  x, exec = run command (the rest of the line) using shell
#
# If you remove a line here THAT COMMIT WILL BE LOST.
# However, if you remove everything, the rebase will be aborted.
#
```

We then `pick` the first commit and `squash` subsequent commits:

```bash
pick 3ksk4f0 My first commit
squash d01jb3f My second commit
squash gf0b3b0 My third commit 

# Rebase 9frt191..gf0b3b0 onto 9frt191
#
# Commands:
#  p, pick = use commit
#  r, reword = use commit, but edit the commit message
#  e, edit = use commit, but stop for amending
#  s, squash = use commit, but meld into previous commit
#  f, fixup = like "squash", but discard this commit's log message
#  x, exec = run command (the rest of the line) using shell
#
# If you remove a line here THAT COMMIT WILL BE LOST.
# However, if you remove everything, the rebase will be aborted.
#
```

Save and close the editor. Following, another file will be retrieved, allowing you to modify the new commit's message:

```bash
# This is a combination of 4 commits.
# The first commit's message is:
First commit

# This is the 2nd commit message:

Second commit

# This is the 3rd commit message:

Third commit


# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
# Explicit paths specified without -i nor -o; assuming --only paths...
# Not currently on any branch.
# Changes to be committed:
#   (use "git reset HEAD <file>..." to unstage)
#
#	new file:   LICENSE
#	modified:   README.textile
#	modified:   Rakefile
#	modified:   bin/jekyll
```

After making desired changes, save the file and close the editor. Once you're done, your new squashed commit will be displayed.

