# Branches

Note on branches.

Jump to [here](#branch-commands) if you just want the commands.

---

## Quick overview

Git's killer branching model

Remember, git stores everything as a snapshot. Git stores a commit object that contains a pointer to the snapshot of the content. For example, if you commit three files:

- The versions of the files are stored. They are refered to as blobs.
- They are stored as a tree, with the commit point to the root of the tree

Add you add more commmits, the next commit will store a pointer to the commit that came before.

With multiple commits, the master/main branch should look like this ![commmit line](../Screenshot%202022-03-10%20175915.png)

With each commit looking like this ![single commit](../Screenshot%202022-03-10%20180133.png)

How does git know what branch or commit you are currently on? It's a special pointer called `HEAD`. It should look like this on a single branch: ![HEAD example](../headonmaster.png)

---

## Creating a new branch

Creating a new branch initally only creates a new branch *pointer* for you to move around. This is done with `git branch <name>`.

Note that the header will still be pointed at the original branch. ![new branch pic](../Screenshot%202022-03-10%20181931.png)

---

## Switching branches

To switch to an existing branch, use `git checkout <branchname>` or `git switch <branchname>`. This will switch the HEAD to the branch you specified.

If you make another commit on this branch, this will happen: ![branchcipic](../branchcommit.png)

So now the testing branch has moved forward, but the master/main branch still points to the older commit.

If you were to switch or checkout back to the master branch, *it will revert the files in your working directory back to the master snapshot*. This means any changes you make on this branch will diverge. This rewinds your work you've done in the testing branch so you can go in a different direction.

If you make some changes now and commit them, those changes wil be isolated from testing. You can switch back and forth and merge them when ready. ![divergence](../diverge.png)

---


---

## Branch commands

`git branch` by itself shows all the current local branches, with a * next to your current branch

`git branch <name>` creates a new branch pointer on the same commit you're working on.

`git checkout <branchname>` will switch you to branchname's branch

`git checkout -b <branchname>` will create a new branch and switch to it simultaneously

---
Note: you can use switch now in git 2.23

`git switch <branchname>`

`git switch -c <branchname>` to create and switch to new branch.

`git switch -` return to last checked out branch

---

`git status` or `git log --decorate` should let you know what branch you're on.

`git log --oneline --decorate --graph --all` is a handy command to print a history of your branches and commits

Note that `git log` only shows commit history of the branches BELOW the one you're checking out.

`git log <branchname>` shows the commit log for that branch.

`git log --all` will show the log of all branches.

