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

## Reset to staging index tree

## Reset to the working tree