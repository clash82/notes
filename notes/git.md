### Install Git bash-autocomplete

```bash
curl https://raw.githubusercontent.com/git/git/master/contrib/completion/git-completion.bash -o ~/.git-completion.bash

# edit `.bash_profile` file:
vi ~/.bash_profile

# add below:
if [ -f ~/.git-completion.bash ]; then
  . ~/.git-completion.bash
fi
```

### Add git branch name to command prompt

```bash
# edit `.bash_progfile` file:
vi ~/.bash_profile

# add below:
parse_git_branch() {
    git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/ (\1)/'
}
export PS1="\u@\h \W\[\033[32m\]\$(parse_git_branch)\[\033[00m\] $ "
```

### Rebase the old branch against the master branch

```bash
git fetch origin

# or if you want to fetch all branches:
git fetch -pv --all

git rebase origin/master
```

### Show operation log

```bash
git reflog
```

### Checkout file from origin/master

```bash
# you can replace origin/master with branch/tag/commit 
git checkout origin/master -- %file%
```

### Show branches already merged with master

```bash
git branch --merged
```

### Show all branches including remotes

```bash
git branch -avv
```

### Start tracking specified branch

```bash
git branch %branch_name% upstream/master
```

### Create and checkout new branch

```bash
git checkout -b %branch_name%
```

### Setup global user attributes

```bash
git config --global user.name "%your_name%"
git config --global user.email "%your_email_address%"
```

### Create new tag

```bash
git tag %tag_name%
```

### Push tags to repo

```bash
git push --tags
```

### Fetch all changes from repo (remove unexisting branches)

```bash
git fetch --all -vp
```

### Show all branches

```bash
git branch
```

### Create a new branch

```bash
git branch %branch_name%
```

### Change to another branch

```bash
git checkout %branch_name%
```

### Remove files from tracking stage

```bash
git rm --cached %file%
```

### Show repo statistics

```bash
git diff --cached -stat
```

### Show modified files

```bash
git diff --cached --numstat | wc -l
```

### Clear unstaged files (beware)

```bash
git clean -f
```

### Remove files already removed from commit

```bash
git checkout %commit_hash% %file1% %file2% ...
git add %file1% %file2% ...
git commit —ammend
```

### Resolve a merge conflicts

```bash
git fetch -v fork
git fetch -v origin
git rebase origin/master
# remove conflicts in your files
git rebase --continue
```

### Show differences

```bash
git diff --word-diff
```

### Squash 3 commits into one

```bash
git rebase -i HEAD~3

# use this if you want to squash initial commit too:
git rebase -i --root

# this will open up your editor with the following:
pick f392171 Added new feature X
pick ba9dd9a Added new elements to page design
pick df71a27 Updated CSS for new elements

# change your files to this:
pick f392171 Added new feature X
squash ba9dd9a Added new elements to page design
squash df71a27 Updated CSS for new elements
```

### Rename branch

```bash
git branch -m %old_name% %new_name%

# if you want to rename the current branch, you can simply do:
git branch -m %new_name%
```

### Undo last commit

```bash
git reset --soft HEAD~1
```

### Restore file from origin/master

```bash
git checkout origin/master %file%
```

### Assign credentials to repository

```bash
git config remote.origin.url https://%username%:%password%@github.com/some/repository.git
```

### Add parts of file to the index

```bash
git add -p
```

### Change default text editor

```bash
git config --global core.editor "vim"
```

### Update submodules

```bash
git submodule update --init --recursive
```

### Setup global .gitignore file

```bash
git config --global core.excludesfile '~/.gitignore'
```

### Disable CRLF line endings (used on Windows) globally

```bash
git config --global core.autocrlf false
```

### Leave file in the repo, but ignore any future changes to it

```bash
git update-index --assume-unchanged %file%

# undo
git update-index --no-assume-unchanged %file%
```

### Set default upstream branch

```bash
# this allows to use simple version of `git pull` without specifying remote branch

git branch --track master origin/master
```

### Delete remote tag

```bash
git tag -d %tag_name%
git push origin :refs/tags/%tag_name%
```

### Change commit author

```bash
git commit --author="%name% <%email%>"
```

### Change commit date

```bash
git commit --amend --no-edit --date "Mon 20 Aug 2018 20:19:19 BST"
```

### Delete all merged remote branches

```bash
git remote prune origin
```
