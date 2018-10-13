---
layout: post
title: git branching model
date: '2014-02-19T10:09:00+00:00'
category: howto
tags: git dev
tumblr_url: http://userdel.com/post/77189389114/git-branching-model
---
[This has been my guide for Git branching for my projects](http://nvie.com/posts/a-successful-git-branching-model/).

A condensed version with some of my own additions:

## Main Branches
Origin should have two main repo’s, “master” and “dev” (“develop”, “development”, whatever you prefer).

master is always stable, production ready.  Pull Requests should be to dev branch.  Features (discussed below) should also be pushed to dev before before a release to master/production.

## Features
Feature branches should be merged into dev with –no-ff so everything is packaged together.

Start by creating your feature branch with git checkout -b myfeature dev

After work is done and you’re feature is ready:
1. git checkout dev
1. git merge –no-ff myfeature
1. git branch -d myfeature
1. git push origin dev

## Releases
Cutting a release consists of grabbing the dev branch at a certain point and merging that into master.
1. git checkout -b release_name dev
1. Update a version file and commit if one exists
1. git checkout master
1. git merge –no-ff release_name
1. git tag -a release_name_or_number
1. git checkout dev
1. git merge –no-ff release_name
1. git branch -d release_name

## Hotfixes
Hot/bugfixes can be done on master, just be sure to also merge and push to dev.
1. git checkout -b hotfix_name master
1. git checkout master
1. git merge –no-ff hotfix_name
1. git tag -a release_name_or_number
1. git checkout dev
1. git merge –no-ff hotfix_name
1. git branch -d hotfix

## Keeping local branches up to date

1. git checkout dev
1. git pull origin dev
1. git checkout your_local_branch_name
1. git merge dev

## Merge Conflicts
[DiffMerge](http://www.sourcegear.com/diffmerge/) is a good visual tool. [Here’s how to set it up.](http://twobitlabs.com/2011/08/install-diffmerge-git-mac-os-x/)

## Reverting a Merge
[http://git-scm.com/blog/2010/03/02/undoing-merges.html](http://git-scm.com/blog/2010/03/02/undoing-merges.htm)

This is when doing a merge for your features makes a lot of sense because you can easily rollback an entire feature with git revert -m 1 merge_sha
