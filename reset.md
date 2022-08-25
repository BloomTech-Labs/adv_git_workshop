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

Lets look at each reset mode impacts each of the other trees.

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
   2. save the file
   3. `git add reset.md`
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

## Reset to remove a commit and clear the other trees `--hard`

The `reset --hard` mode is the most dangerous. This is because it will not only remove the commit(s) but it will also clear changes in the staging and working trees so they match the new HEAD of the commit history tree. Any changes in these trees will be lost. While this might be dangerous, you might find yourself using it more frequently to "undo" some changes that you now realize aren't working and you want to start over from the last working commit.

Similar to the `reset --soft` command we're going to make changes to this file a couple times so we have changes in the stage and working trees.

1. Again, let's look at the status
   1. `git status`
   2. Clean working tree
   3. `git log`
   4. notice the HEAD commit
2. Now for a change that we can stage.
   1. Put your name <HERE> <- inside the brackets
   2. save the file
   3. `git add reset.md`
3. Let's check the state of the file again
   1. `git status`
   2. You should see the `Changes to be committed:` section with `modified:     reset.md`
4. Now for another change that we will leave in the working tree.
   1. Put your name <HERE> <- inside the brackets
   2. save the file
   3. DON'T `git add`
5. Checking the status again
   1. `git status`
   2. This time you should see the `Changes to be committed:` section as well as a new `Changes not staged for commit:` section. Both will have the `modified:     reset.md` item
6. Now we're ready to hard reset the trees.
   1. `git reset --hard HEAD~1`
7. Lets look at all the info
   1. `git log`
   2. The previous HEAD commit is now removed
   3. `git status`
   4. we now see `nothing to commit, working tree is clean` and both our stage and working trees match the new commit history tree. We are ready to over. 😀

Enjoy your new git powers!! ⚡️
