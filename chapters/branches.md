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

If you make some changes now and commit them, those changes wil be isolated from testing. You can switch back and forth and merge them when ready. 

![divergence](../diverge.png)

---

## Basic branching and Merging

Assume we need to take the following course of action:

1. Do some work on the main branch
2. Create a new branch to work on a new feature
3. Do some work in that branch

But you receive a call to issue out a hotfix for a issue. You need to do the following

1. Go back to the main branch (which is left the way before you worked on the feature branch)
2. Create another branch to work on the hotfix
3. Merge the hotfix branch with the main branch
4. Go back to the feature branch and work on that.

It's important to note in part 2 step 3, the hotfix merge looks like this:
![hotfixpre](../hotfixpre.png)
![hotfixpost](../hotfixpost.png)

Because the merges are not divergent, git able to simply merge by fast forwarding, that is, moving the master branch pointer ahead.

Now you can delete your hotfix branch because master/main is already inline with it.

But as you work on the feature branch (shown as iss53 in the pictures), there will be a divergence. You check out into master/main again and merge. But this one won't be a fast forward, as the divergence means that you have to combine the commits of the common ancestor, the feature branch, and the hotfix into 1 snapshot.

Before:

![threepointmergepre](../threepointtruepre.png)

After:

![threepointmergepost](../3pointpost.png)

There will be merge conflicts sometimes. Think about it. If you change different parts of the file, it will just combine the differences. But if the branches change the same part of the file, it will conflict.

`git status` will let you know, and the file will contain a section like this:

```
<<<<<<< HEAD:index.html
<div id="footer">contact : email.support@github.com</div>
=======
<div id="footer">
please contact us at support@github.com
</div>
>>>>>>> iss53:index.html
```

The HEAD (on the master branch, which is what you merged into) is above the ======, and the iss53 branch is below it.

You can choose one or the other, or merge them yourself.

Afterwards, run `gitadd`, as staging the file marks it as resolve.

Then just `git commit` to conclude the merge.

More about merging in advanced merging.

---

## Branch Management

`git branch` with no arguments gets a listing of your current branches

`-v` shows the last single commit on each branch

`--merged` and `--no-merged` lists branches that have merged into your checked-out branch.

Add a `<branchname>` in order to apply the merge command to that specific branch.

The branches that `--merged` lists that don't have the * next to them are generally fine to delete.

`--no-merged`  will show branches not yet merched. 

To delete unmerged branches, you need to use `git branch -D <branchname>`.

---

## Changing a branch name

You can a branch name via:

`git branch --move <prebranchname> <postbranchname>`

Then push the correct branch to remote:

`git push --set-upstream origin <postbranchname>`

Then delete the bad branch from remote with:

`git push origin --delete <prebranchname>`

NOTE: changing the master/main branch of a work in progress repo will break intergrations and services. Change it on a newly started project or talk to your collaborators.

- Code that depend on the original maaster will need to update code and config.
- Adjust release scripts and builds.
- Update references in documentation
- Close or merge any pull requests that target the old branch.

Only then can you delete the old branch master.

---

## Branch commands

`git branch` by itself shows all the current local branches, with a * next to your current branch

`-v` shows the last single commit on each branch

`--merged` and `--no-merged` lists branches that have merged into your checked-out branch.

`git branch <name>` creates a new branch pointer on the same commit you're working on.

`git branch -d <branchname>` deletes the merged branch

`git branch -D <branchname>` deletes unmerged branch

`git checkout <branchname>` will switch you to branchname's branch

`git checkout -b <branchname>` will create a new branch and switch to it simultaneously

---
Note: you can use switch now in git 2.23

`git switch <branchname>`

`git switch -c <branchname>` to create and switch to new branch.

`git switch -` return to last checked out branch

---

merging

`git checkout master` or the branch that you're merging into

`git merge <branch>` will merge that branch into your checked-out branch


---


`git status` or `git log --decorate` should let you know what branch you're on.

`git log --oneline --decorate --graph --all` is a handy command to print a history of your branches and commits

Note that `git log` only shows commit history of the branches BELOW the one you're checking out.

`git log <branchname>` shows the commit log for that branch.

`git log --all` will show the log of all branches.

