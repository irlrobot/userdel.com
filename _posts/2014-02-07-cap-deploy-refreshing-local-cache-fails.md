---
layout: post
title: cap deploy refreshing local cache fails
date: '2014-02-07T06:09:58+00:00'
tags: capistrano osx wtf
tumblr_url: http://userdel.com/post/75896741312/cap-deploy-refreshing-local-cache-fails
---
If you’re trying to cap deploy and getting

```
fatal: Not a git repository (or any of the parent directories): .git
```

during the “refreshing local cache to revision …” step on OSX, try deleting the `/tmp/caches/<project-name>` directory on your Mac and retry the deploy.

Kudos to [http://www.outofcph.dk/2009/05/capistrano-deployment-with-git-failing-periodically/](http://www.outofcph.dk/2009/05/capistrano-deployment-with-git-failing-periodically/)
