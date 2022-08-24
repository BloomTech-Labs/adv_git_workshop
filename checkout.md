# The Git Checkout Command

## Description

You've likely used `checkout` to switch branches. Did you know you can use `checkout` to change the version of a file(s) or folder? In fact, `checkout` gets a specific version and makes it the current local version. Branch names are references to versions of the entire folder structure, so when we run `git checkout branch_name` we are actually changing the entire local folder to be the "version" that the branch references.

It is very common to use checkout on files and folders as well.

## File checkout

Let's have a look at the outcome of `checkout` on files in 2 scenarios. (more scenarios exist but let's just start with 2 😉)

- discard uncommited changes
- restore file to previous commit (based on commit hash)
