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

Lets look at how to reset of a commit impacts each of the other trees.

## Reset to staging index tree `--mixed`

To move the commit changes into the staging tree we use the --mixed option. This is also the default, so we could leave the option off. Lets remove a commit and place the changes from that commit into the staging index (staged)

1. Lets inspect the commit history and make note of the HEAD commit message
   1. `git log`
   2. Also, lets output the current sha of the files. The sha hash will change as we work with the commit history.
      1. `git ls-files -s`
2. Now lets remove the current HEAD commit
   1. `git reset HEAD~1 --mixed`
      1. This will reset to 1 commit before HEAD
      2. by default reset will work on HEAD, but if you don't have any changes in the stage or working trees then nothing will change.
3. The contents of this file should not change but the file should now be staged.
   1. `git status`
   2. You should see `modified:   reset.md`
   3. `git ls-files -s` should show new commit hashes
   4. `git log` will show that the HEAD commit now points to what was previously the second commit.
4. Since no content has been lost, let's commit the file again.
   1. `git commit -m "put commit back in history"`

> 🌕 Note: if you had changes already staged they will be moved to the working tree or replaced.

## Reset to remove a commit `--soft`

To remove a commit but not put the changes into the staging or working tree we use the `--soft` option. This one is a bit more tricky to understand so pay attention to the commit hashes. Also, we will need put this file into staging index tree otherwise the command will do nothing.

1. Lets start by looking at the some info about the file.
   1. `git status && git ls-files -s`
   2. This should show that our working tree is clean AND the current hash of the files
   3. `git log` notice the message of the HEAD commit
2. Let's make a change to this file and stage it.
   1. Put your name <HERE> <- inside the brackets
3. Let's check the state of the file again
   1. `git status && git ls-files -s`
   2. You should see `modified:     reset.md`
   3. Also, the hash of this file should be different
4. With the file staged lets see what happens when we reset --soft to the commit before HEAD
   1. `git reset --soft HEAD~1`
5. Lets check the info
   1. `git status && git ls-files -s`
   2. The file is still modified and the sha is not changed
   3. `git log`
   4. The HEAD commit we noticed from the last log command is now removed.
   5. Beacuse we have the changes in this file from that commit captured in the staged index tree nothing is lost, but it is not commited. 😉
