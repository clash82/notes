---
layout: default
title: Git
---

## Rebase the old branch against the master branch: ##

{% highlight bash %}
git fetch origin

# or if you want to fetch all branches:
git fetch -pv --all

git rebase origin/master
{% endhighlight %}

## Show operation log: ##

{% highlight bash %}
git reflog
{% endhighlight %}

## Checkout file from origin/master: ##

{% highlight bash %}
# you can replace origin/master with branch/tag/commit 
git checkout origin/master -- %file%
{% endhighlight %}

## Show branches already merged with master: ##

{% highlight bash %}
git branch --merged
{% endhighlight %}

## Show all branches including remotes: ##

{% highlight bash %}
git branch -avv
{% endhighlight %}

## Start tracking specified branch: ##

{% highlight bash %}
git branch %branch_name% upstream/master
{% endhighlight %}

## Create and checkout new branch: ##

{% highlight bash %}
git checkout -b %branch_name%
{% endhighlight %}

## Setup global user attributes: ##

{% highlight bash %}
git config --global user.name "%your_name%"
git config --global user.email "%your_email_address%"
{% endhighlight %}

## Create new tag: ##

{% highlight bash %}
git tag %tag_name%
{% endhighlight %}

## Push tags to repo: ##

{% highlight bash %}
git push --tags
{% endhighlight %}

## Fetch all changes from repo (remove unexisting branches): ##

{% highlight bash %}
git fetch --all -vp
{% endhighlight %}

## Show all branches: ##

{% highlight bash %}
git branch
{% endhighlight %}

## Create a new branch: ##

{% highlight bash %}
git branch %branch_name%
{% endhighlight %}

## Change to another branch: ##

{% highlight bash %}
git checkout %branch_name%
{% endhighlight %}

## Remove files from tracking stage: ##

{% highlight bash %}
git rm --cached %file%
{% endhighlight %}

## Show repo statistics: ##

{% highlight bash %}
git diff --cached -stat
{% endhighlight %}

## Show modified files: ##

{% highlight bash %}
git diff --cached --numstat | wc -l
{% endhighlight %}

## Clear unstaged files (beware): ##

{% highlight bash %}
git clean -f
{% endhighlight %}

## Remove files already removed from commit: ##

{% highlight bash %}
git checkout %commit_hash% %file1% %file2% ...
git add %file1% %file2% ...
git commit —ammend
{% endhighlight %}

## Resolve a merge conflicts: ##

{% highlight bash %}
git fetch -v fork
git fetch -v origin
git rebase origin/master
# remove conflicts in your files
git rebase --continue
{% endhighlight %}

## Show differences: ##

{% highlight bash %}
git diff --word-diff
{% endhighlight %}

## Squash 3 commits into one: ##

{% highlight bash %}
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
{% endhighlight %}

## Rename branch: ##

{% highlight bash %}
git branch -m %old_name% %new_name%

# if you want to rename the current branch, you can simply do:
git branch -m %new_name%
{% endhighlight %}
