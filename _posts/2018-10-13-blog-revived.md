---
layout: post
title:  "brushing the dust off"
date:   2018-10-13 13:43:40 -0500
category: general
tags: jekyll migrate migration tumblr
---
Well, it's been a little awhile, but I'm finally reviving this blog. To start, I ditched [Tumblr](https://tumblr.com) and migrated to [GitHub Pages](https://pages.github.com/) powered by [Jekyll](https://jekyllrb.com/).  Jekyll has an [importer](https://import.jekyllrb.com/docs/tumblr/), but it's pretty naive. All the reblogs from Tumblr are broken and none of the images came along with the posts (though they were downloaded into a directory for me). Not a huge deal for me, I plan to just go back and delete all the reblog posts since most are broken anyways and I'll manually add the images on the whopping four imported posts that had images.

The rest of this post will cover a brief tutorial on migrating your own blog from Tumblr to Jekyll. [Docker](https://docker.com) is required. It's 2018 now, so I won't explain [how to get going with Docker](https://diveintodocker.com)...

tl;dr version for those familiar with Docker and Jekyll at least a little bit:
1. Create a new Jekyll site https://github.com/envygeeks/jekyll-docker/blob/master/README.md#docker-compose
2. cd into the dir for your new site
3. Import your Tumblr posts https://github.com/irlrobot/dockerfiles/tree/master/jekyll-import-tumblr
4. (Optional) Add [pagination](https://jekyllrb.com/docs/pagination/)