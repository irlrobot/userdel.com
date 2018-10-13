---
layout: post
title:  "brushing the dust off"
date:   2018-10-13 13:43:40 -0500
tags: jekyll migrate migration tumblr
---
Well, it's been a little awhile, but I'm finally reviving this blog. To start, I ditched [Tumblr](https://userdel.tumblr.com) and migrated to [GitHub Pages](https://pages.github.com/) powered by [Jekyll](https://jekyllrb.com/).  Jekyll has an [importer](https://import.jekyllrb.com/docs/tumblr/), but it's pretty naive. All the reblogs from Tumblr are broken and none of the images came along with the posts (though they were downloaded into a directory for me). Not a huge deal, I plan to just go back and slowly delete all the reblog posts since most are broken anyways and I'll manually add the images on the whopping four imported posts that had them.

The below is a tl;dr on how to migrate from Tumblr to GitHub Pages for those familiar with [Docker](https://docker.com) and Jekyll (at least a little bit).  It's 2018, so I assume everyone has at least played with Docker by now, but if you're late to the party then I highly recommend [Dive Into Docker](https://diveintodocker.com).

1. [Create a new Jekyll site](https://github.com/envygeeks/jekyll-docker/blob/master/README.md#docker-compose)
2. cd into the directory
3. [Import your Tumblr posts](https://github.com/irlrobot/dockerfiles/tree/master/jekyll-import-tumblr)
4. [Setup GitHub Pages](https://help.github.com/articles/configuring-a-publishing-source-for-github-pages/).