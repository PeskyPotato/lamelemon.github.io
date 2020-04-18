---
layout: post
title: Useful git commands
date: 2019-05-09 13:55:58
link: /posts/git-commands
categories: posts
description: Useful git commands to refer to
keywords: "git, github, commands, version control, terminal"
parentPost: true
authors:
    - PeskyPotato
---

## Introduction
These are a few git commands that I refer to from time to time when I need a reminder. This is by no means a comprehensive guide on how to use git.

---
## Contents
- [Introduction](#introduction)
- [Add co-authors to a commit](#add-co-authors-to-a-commit)
- [Branching with Git](#branching-with-git)
    - [Checkout a remote branch](#checkout-a-remote-branch)
    - [Create a branch from another branch](#create-a-branch-from-another-branch)
- [Change the last commit](#change-the-last-commit)
    - [Set the author](#set-the-author)
    - [Set the date](#set-the-date-)
- [Fetch a pull request](#fetch-a-pull-request)
- [Squash commits already pushed to GitHub](#squash-commits-already-pushed-to-github)
- [Keep a fork up to date](#keep-a-fork-up-to-date)
- [Further reading](#further-reading)

---
## Add co-authors to a commit 
This will allow you to give credit to more than one author for a commit. This works on GitHub only, and count towards the contribution history of all authors.

Within the commit message add "Co-authored-by:" followed by the name and GitHub email of the individual you wish to credit.

```
git commit -m "Regular ol' commit
>
>
Co-authored-by: your-name <your-email@your-domain.com>
Co-authored-by: their-name <their-email@their-domain.com>"
```
From [GitHub](https://help.github.com/en/articles/creating-a-commit-with-multiple-authors){:class="small-link"}

[[top]](#introduction)

---
## Branching with Git
Branches allow developers to work on different features without affecting the master branch. Below are instructions to make a branch, switch to it, commit changes and merge with master. 

```
git branch feature-branch
git checkout feature-branch

git add .
git commit –m "a commit message"

git checkout master
git merge feature-branch
```

### Checkout a remote branch
If you wish to checkout a branch from a remote do the following where upstream is your remote and develop is the branch you wish to checkout.
```
git checkout -b develop upstream/develop
```

### Create a branch from another branch
Below `new-feature` is the name of the branch you want to create and `develop` is the branch you would like to checkout from.
```
git checkout -b new-feature develop
```

[[top]](#introduction)

---
## Change the last commit

### Set the author
Set the author username and email without editing the message for the last commit.
```
git commit --amend --no-edit --author="LameLemon <lame@lemon.com>"
```

### Set the date 
Set the date and time of the last commit without editing the message. 
```
git commit --amend --no-edit --date "Mon 29 Apr 2019 09:47:53 -0400"
```
From [VonC on StackOverflow](https://stackoverflow.com/questions/23609991/git-github-commit-at-past-date){:class="small-link"}

[[top]](#introduction)

---
## Fetch a pull request
Fetching a pull request to it's own branch allows you to test the code and see the changes locally before merging.

The following two lines fetchs the code from the remote `upstream`, replace `506` with the the pull request ID and `lamelemon/test-pr` with what you want to call the branch.
```
git fetch upstream pull/506/head:lamelemon/test-pr
git checkout lamelemon/test-pr
```

If there are any modification to the pull request that you want to pull do the following while in the `lamelemon/test-pr` branch.
```
git pull upstream pull/506/head
```
From [Gist](https://gist.github.com/adam-p/15413fabef6cffecd897) by [adam-p](https://gist.github.com/adam-p)

[[top]](#introduction)

----
## Squash commits already pushed to GitHub
This squash the last N commits by rebasing and force pushing to GitHub avoiding this helpful but unwanted error.
```
To https://github.com/LameLemon/pepe-is-the-man.git
 ! [rejected]        master -> master (non-fast-forward)
error: failed to push some refs to 'https://github.com/LameLemon/pepe-is-the-man.git'
hint: Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart. Integrate the remote changes (e.g.
hint: 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```

First, through interactive rebasing set the HEAD back to the number of commits you want to squash.
```
git rebase -i HEAD~3
```

In the text editor pick on commit to go with and squash the others.
```
pick 2871a3f adding the dankest pepe
squash ba1834f adding the second dankest pepe
squash 13ed324 adding the third dankest pepe

# Rebase 13ed324..2871a3f onto 9482e8a
#
# Commands:
#  p, pick = use commit
#  e, edit = use commit, but stop for amending
#  s, squash = use commit, but meld into previous commit
#
# If you remove a line here THAT COMMIT WILL BE LOST.
# However, if you remove everything, the rebase will be aborted.
#
```

Save and exit and on the next text file comment (#) everything except what you want the new commit message to be. Then save and exit again. Now the commits have been squashed.

Now force push the changes to the desired branch. 

```
git push origin +master
```

From [GitReady](http://gitready.com/advanced/2009/02/10/squashing-commits-with-rebase.html){:class="small-link"} and [StackOverflow](https://stackoverflow.com/questions/5667884/how-to-squash-commits-in-git-after-they-have-been-pushed){:class="small-link"}.

[[top]](#introduction)

---
## Keep a fork up to date
First after cloning the repository make sure to add the original repository as 'upstream', this only needs to be done once.
```
git remote add upstream https://github.com/GITHUB-USER/ORIGNIAL-REPO.git
```

Now everytime you need to update your local copy with changes from the original you need to do the following three steps.
Fristfetch the changes from the upstream repository.
```
git fetch upstream
```

Checkout your local master branch and merge with the upstream master.
```
git checkout master
git merge upstream/master
```

You can then push the changes to your GitHub fork.
```
git push
```

From [GitHub](https://help.github.com/en/articles/syncing-a-fork){:class="small-link"}

[[top]](#introduction)

---
## Further reading
[GitHub Help](https://help.github.com/en) - Great resource for help using Github

[git ready](http://gitready.com/) - Filled with useful git commands and explanations

[Oh, shit, git!](https://ohshitgit.com/) - Some bad situations and how to get out of them


`:)`
