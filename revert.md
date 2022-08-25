# The Git Revert Command

## Description

There is a good chance you haven't used the `revert` command just yet. This is
OK. The `revert` command has a very specific use case of "undoing" a previous
commit. This means that git will figure out the inverse of that previous commit
and apply it to the local file(s) and a new commit will be created to record
the change. The old commit is not removed like a traditional "undo", this will
leave the old commit in your history but you will have a new commit that
"undoes" it.

> 🔴 Note: that your working tree must **not** have any changes since the HEAD
> commit. This includes staged changes.

This will not undo all the commits from HEAD back to the selected
commit, but rather only the specific commit(s) will be "undone" by the new
commit.

> 🔵 The option `-n` OR `--no-commit` will apply the changes but not make the
> new commit. This is handy for those times when you are unsure this will fix
> an issue.

## Revert a commit

Let's have a look at the outcome of `revert` on this working tree (branch):

1. Make sure the working tree is clean
   1. `git status`
2. Have a look at the current history.
   1. `git log`
   2. Make note of the HEAD commit message
3. Lets revert a specific commit
   1. `git revert`
4. Lets see the outcome of this command
   1. `git log`
      1. Do you see a new commit at HEAD with the old HEAD following it?
   2. `git status` - the tree should be clean still
