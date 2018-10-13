---
layout: post
title: git branching model
date: '2014-02-19T10:09:00+00:00'
tags:
- git
- dev
tumblr_url: http://userdel.com/post/77189389114/git-branching-model
---
This has been my guide for Git branching for my projects:  http://nvie.com/posts/a-successful-git-branching-model/
A condensed version with some of my own additions:
Main Branches
Origin should have two main repo’s, “master” and “dev” (“develop”, “development”, whatever you prefer).
master is always stable, production ready.  Pull Requests should be to dev branch.  Features (discussed below) should also be pushed to dev before before a release to master/production.
Features
Feature branches should be merged into dev with –no-ff so everything is packaged together.
Start by creating your feature branch with git checkout -b myfeature dev
After work is done and you’re feature is ready:
git checkout dev
git merge –no-ff myfeature
git branch -d myfeature
git push origin dev
Releases
Cutting a release consists of grabbing the dev branch at a certain point and merging that into master.
git checkout -b release_name dev
Update a version file and commit if one exists
git checkout master
git merge –no-ff release_name
git tag -a release_name_or_number
git checkout dev
git merge –no-ff release_name
git branch -d release_name
Hotfixes
Hot/bugfixes can be done on master, just be sure to also merge and push to dev.
git checkout -b hotfix_name master
git checkout master
git merge –no-ff hotfix_name
git tag -a release_name_or_number
git checkout dev
git merge –no-ff hotfix_name
git branch -d hotfix
Keeping local branches up to date

git checkout dev
git pull origin dev
git checkout your_local_branch_name
git merge dev

Merge Conflicts
DiffMerge is a good visual tool. Here’s how to set it up.
Reverting a Merge
http://git-scm.com/blog/2010/03/02/undoing-merges.html
This is when doing a merge for your features makes a lot of sense because you can easily rollback an entire feature with git revert -m 1 merge_sha
