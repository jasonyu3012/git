# Addtional tips and useful tricks

## Tagging

Git has the ability to tag specific points in a repository's history as being important. This is typically used to mark release points (v1.0, v1.2, etc.)

### Listing tags

`git tag` lists your existing tags. It lists in them *alphabetical order* 

`git tag -l "v1.8.5*` will list all tags with 1.8.5u

---

### Creating tags

There are two types of tags:
- lightweight tags are just pointers to a specific commit.
- Annnotated tags are full objects. They're checksummed, contain the tagger name, email, and date; have a tagging message; and can be signed and verified with GNU Privacy Guard (GPG). Generally recommended you use this one, unless you want a temporary flag.

`git tag -a <v1.0> -m "my version 1.0"`  - creates an annotated tag

Tags created will be tagged to the head commit.

`git show <v1.0>` will show the tag data.

---

### Tagging later

If you forget to tag a specific commit, then you can run `git log` or something like `git log --pretty=oneline`, you can then just use 

`git tag -a <v1.0> <beginning few letters of checksum>` and that will tag that commit for you.

---

### Sharing tags

Note that git push does not push tags to remote servers!

`git push <remote> <tag_name>` will push that specific tag.

`git push <remote> --tags` will push all tags that are not already on the remote.\

---

### Deleting tags

`git tag -d <tagname>` deletes the tag locally.

`git push origin --delete <tagname>` deletes it remotely.

---

### Checkout tags

`git checkout <tagname>` will put your repository in a detached head stead. You can look around, make experimental changes, and commit them. You can save your changes by creating a new branch, but it will be different from the original commit you were looking at. More information [here](https://git-scm.com/book/en/v2/Git-Basics-Tagging).

---

## Git Alias

Simple way to write shortcuts to specific git commands.

`git config --global alias.<shortcutname> <original command>` will run the original commmand when you type `git <shortcutname>`

It works even for commands with flags and specifiers, just use a ''

```
git config --gloab alias.unstage 'reset HEAD --'

now

git unstage fileA
git reset HEAD -- fileA
```




