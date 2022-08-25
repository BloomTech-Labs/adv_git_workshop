# The Git Reset Command

## Description

The `reset` command is the most powerful command when it comes to working with commit history.Unlike the `revert` and `checkout` commands, `reset` isn't "safe". This is because `reset` actually removes (or reverts) the commits from the history. In a shared repo this concidered dangerous in a shared repo.

> 🔴 Warning: Where possible, `reset` should only be used on local branches that have not been pushed. If it has been pushed, you will have to force push the changes and notify other users that they have to "force pull" process. (This is not a command, but a process)

For a local branch where we might have made some mistakes, this command will help us remove commits and get back to a code state that was working.

The `reset` command works on all 3 of the areas of git's internal state management. These are often refered to as the Three Trees. While they may not actually be data tree structures, they do contain timeline of changes. The 3 trees are:

- The working tree (or directory) - meaning all the local files you can see
- The staging index tree - all the changes that are staged for a commit.
- The commit history tree - each ref (branch) has a commit history

The `reset` command can remove commits fromt he commit history and move the changes into either of the other 2 "trees". In complex cases this can require the user to work thru multiple merge conflicts as `reset` works through each commit.

Lets look at how to reset a commit into each of the other trees.

## Reset to staging index tree --mixed

To move the commit changes into the staging tree we use the --mixed option. This is also the default, so we could leave the option off. Lets remove a commit and place the changes from that commit into the staging index (staged)

1. Lets inspect the commit history and make note of the HEAD commit message
   1. `git log`
   2. Also, lets output the current sha of the files. The sha hash will change as we work with the commit history.
      1. `git ls-files -s`
2. Now lets remove the current HEAD commit
   1. `git reset HEAD~1 --mixed`
      1. This will reset to 1 commit before HEAD
3. The contents of this file should not change but the file should now be staged.
   1. `git status`
   2. You should see `modified:   reset.md`
4. Since no content has been lost, let's commit the file again.
   1. `git commit -m "put commit back in history"`

> 🌕 Note: if you had changes already staged they will be moved to the working tree or replaced.

## Reset to the working tree
