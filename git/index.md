---
layout: default
title: Git
---

## Rebase the old branch against the master branch: ##

`git fetch origin
git rebase origin/master`

## Show operation log: ##

`git reflog`

## Show branches already merged with master: ##

`git branch --merged`

## Show all branches including remotes: ##

`git branch -avv`

## Start tracking specified branch: ##

`git branch %branch_name% upstream/master`

## Create and checkout new branch: ##

`git checkout -b %branch_name%`

## Setup global user attributes: ##

`git config --global user.name "%your_name%"
git config --global user.email "%your_email_address%"`

## Create new tag: ##

`git tag %tag_name%`

## Push tags to repo: ##

`git push --tags`

## Fetch all changes from repo (remove unexisting branches): ##

`git fetch --all -vp`

## Show all branches: ##

`git branch`

## Create a new branch: ##

`git branch %branch_name%`

## Change to another branch: ##

`git checkout %branch_name%`

## Remove files from tracking stage: ##

`git rm --cached %file%`

## Show repo statistics: ##

`git diff --cached -stat`

## Show modified files: ##

`git diff --cached --numstat | wc -l`

## Clear unstaged files (beware): ##

`git clean -f`

## Remove files already removed from commit: ##

`git checkout %commit_hash% %file1% %file2% ...
git add %file1% %file2% ...
git commit —ammend`

## Resolve a merge conflicts: ##

`git fetch -v fork
git fetch -v origin
git rebase origin/master
(remove conflicts in your files)
git rebase --continue`

## Show differences: ##

`git diff --word-diff`
