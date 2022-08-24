# The Git Checkout Command

## Description

You've likely used `checkout` to switch branches. Did you know you can use `checkout` to change the version of a file(s) or folder? In fact, `checkout` gets a specific version and makes it the current local version. Branch names are references to versions of the entire folder structure, so when we run `git checkout branch_name` we are actually changing the entire local folder to be the "version" that the branch references.

It is very common to use checkout on files and folders as well.

## File checkout

Let's have a look at the outcome of `checkout` on files in 2 scenarios. (more scenarios exist but let's just start with 2 😉)

- discard uncommited changes
- restore file to previous commit (based on commit hash)

### Discard uncommitted changes

This is by far one of the most commonly used git command scenarios. Imagine you
have made a change in a file only to find that you broke dozens of tests. 😱 🤦
Well, it is likely worth just discarding these changes and starting over.

Lets see this in action:

1. Make a change to this file by adding some text at the end of this line
2. Save the file.
3. run the command `git status` to confirm that git noticed that the file has been modified.
   1. You should see `modified:   checkout.md`
4. Now lest discard this change with the command `git checkout checkout.md`
5. `git status` should now show that the branch tree is clean (no changes)

### Restore file to previous commit

Using checkout to "restore" a file to a previous commit isn't as common and
typically is only used to test or debug based on changes to a single or small
number of files.

It's important to note that we aren't restoring anything. The commit history
is unchanged. It's the local (current) file that is changed. Now if we were to
commit the local file in this state it would then be restored to the previous
version in the commit history.

Also note that in this scenario we can not use `git checkout checkout.md` to
discard the changes. Git knows that we asked for a previous revision of the
file and now has the ref in a special state. To discard these changes we have
to use the `git restore` command. ⭐️ Bonus command to learn.

Lets see this in action:

1. Lets confirm the branch is clean with `git status`
2. now lets checkout a previous version of this file
   1. `git checkout e10ec671574bb320a917ebf85117fb888d6a0a0d checkout.md
3. `git status` will confirm that the file is now modified.
   1. If you have the file open in an editor the contents should now be changed
4. Now lets restore the file to the most recent commit
   1. `git restore checkout.md`
