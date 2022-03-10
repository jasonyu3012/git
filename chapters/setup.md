# Table of Contents

[Setting up a repository](#setting-up-a-repository)

[Checking and recording changes](#recording-any-changes)

[Committing changes](#committing-your-changes)

[Removing and renaming a file](#removing-a-file)

[View commit history](#viewing-commit-history)

[Undoing changes](#undoing-any-changes)

---


# First things when starting a project

## What is a git repository?

A git repository is a virtual storage of your project. It allows you to save versions of your code, which you can access when needed.

This page will contain most of your commands for git.

---

## Setting up a repository

If starting a local repository, we start by cd'ing to the root project folder and then executing:

`git init` initiates the empty git repository. This will create a new .git subdirectory in your current working directory. In Window's Explorer, this may be hidden.

You can also copy an existing repository with `git clone`. This works with the following syntax:

`git clone <url>` clones the .git directory as well as a working copy of all the project files.

---

## Recording any changes

Each file can be in one of two states: tracked or untracked.

- Tracked files are files that were in the previous snapshot or new files that are currently staged. They can be modified, unmodified, or staged.
- Untracked files are new and unstaged files that were not in the previous snapshot.

### How do you check for modified files and untracked files?

`git status`  shows modified files as well as untracked files if there are any. It also informs you what branch you are on.

- It will also show any modifications (new files, modified files) that are ready to be committed.
- It will show anything modifications that are unstaged.
- Will also show any untracked files.

`git diff` lets you know what exactly has been changed and which files has been changed in the unstaged area

`git diff --staged` will let you know the differences of the files in the staged area

`git add <filename>` adds a file to staging area for it to be committed. We can add a markdown file (such as README.md) to start.

- git add will stage a file exactly how it is when you run the add command. Meaning if you stage a file and change it again, you will have to stage it again.

`-a` - adds all tracked files (so no new files)

---

## Committing your changes

`git commit -m '<message>` commits all files in the staging area to the repository.

`-v` explicitly places the diff of your change in the editor so you can exactly what changes you're committing

`-a` commits all tracked files (no new files).

If you want to amend a commit, see the [amend specifier](#undoing-any-changes).

---

## Removing a file

`git rm <filename>` removes a file from git and the file system

`--cached` adding this flag removes it from the repository but not locally

`-f` - if you already added the file into the staging area, you have to include this flag so you that you don't accidentally delete changes.

---

## Rename a file

`git mv <fileold> <filenew>` renames the file

---

## Viewing commit history

`git log` - lists the recent commits in reverse chronological order (meaning latest commit will be first). To navigate, use:

```
next line : return
next page : spacebar
previous page : w
quit : q
help : h
```

`-p or --patch` shows the difference (patch output) introduced in each commit.

`--stat` shows some abbreviated stats for each commit

`--pretty=<value>` changes the log output

- oneline - print each commit on one line
- short, full, fuller show the output in roughly the same format but with more and more information, repsectively.
- format, done in `--pretty=format:"<format>"`, view format specifiers [here](https://git-scm.com/docs/pretty-formats).
  
`--graph` shows an ASCII graph of the branches merge history

`--since=` and `--until=` use the formats `2.weeks` or `"2008-10-15"` or `"2 years 1 day 3 minutes ago"`

`--author='<author>'` allows you to filter on a specfic author

`--grep='<keyword>'` allows you to search for key words in the commit message

`-S` is a flag that shows only commits that changed the number of occurences of that string. This is useful for `git log -S <function_name>` to see all the commits that added/removed a reference to a function

`git log -- path/to/file` often placed at the end, will only show commits that introduced a change in that file path.

An example of some of these specifiers being used:

`git log --pretty="%h - %s" --author='Junio C Hamano' --since="2008-10-01" -- before="2008-11-01" --no-merges -- c/projects`

More specifiers on git's [documentation website](https://git-scm.com/docs/git-log).

---

## Undoing any changes

`git commit --amend -m "updated message"` or use the `--no-edit` specifer (for no message updates) takes the most recent commit and adds the new staged changes to it.

*Only use this on local commits that have no been pushed anywhere*

`git reset HEAD <file>` will remove a file from the staging area.

`git restore` is an alternative to git reset, and is commonly used in git 2.23.0 and onwards.

`git restore --staged <file>` to remove a file from the staging area.

Unmodifying a modified file - well, `git status` will tell you how to discard changes.

`git checkout -- <file>` will remove any local changes and replace that file with the last staged or committed version.

`git restore <file>` will do the same thing.

---

`git branch -m main` - if you're creating a local repository first, git defaults to naming the default branch "master." We can use the branch command to change the name to "main" so that it matches github's default repository name.

`git remote add <name> <url>` - Adds a remote named "name" (usually origin) with the URL of "url". The command `git fetch` can be used to 

