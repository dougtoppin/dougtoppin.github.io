---
layout: post
title: "Back to Jekyll from Octopress"
date: 2017-09-08 22:01
comments: true
categories: [blog]
description: Switching from Octopress back to plain Jekyll
keywords: jekyll octopress
---
When I first created this blog I opted to go with Octopress.
That worked well enough for a number of years but Octopress seems to have fallen in disrepair and I also got tired of needing to install/configure/update Rails to keep it working.
As a result I am switching back to plain old Jekyll for managing it.
I also had some issues with using different machines to compose posts because of Ruby/Rails/something or other problems.

What I intend to do now is use Docker containers to build and view the blog locally before pushing it to GitHub.
The primary advantage of using Docker for this is you don't have to install anything other than Docker.

From now on I should be only doing the following when I want to view it locally before pushing.

If you are familiar with Jekyll you might notice the use of the ```JEKYLL_ENV``` environment variable.
This is use to indicate whether or not this is a production environment and do things like notify Google Analytics.
For local testing I like to be able to see analytics data appear which is why I am enabling this by setting it during the Docker run command.

```
export JEKYLL_VERSION=3.5
docker run --rm --volume=$PWD:/srv/jekyll -it -p 4000:4000 -e JEKYLL_ENV=production jekyll/jekyll:$JEKYLL_VERSION jekyll serve
```

What I tend to find when reading about how to use Jekyll to create a GitHub Pages blog is that the writer assumes that you already know some basics (at least) and a few steps or tidbits are left out.

I intend to do my own little writeup on how to use Jekyll with GitHub Pages for a blog and it will tell how to
* create the blog
* add a new post to the blog
* clone the blog repo somewhere else and work on it
* build and view it locally
* what you do NOT need to commit once you do build it locally (this is the tidbit always left out of instructions)
* how to test new versions of the blog by doing things like forking a theme repo and renaming the existing GitHub Pages repo to test it

More to come.
