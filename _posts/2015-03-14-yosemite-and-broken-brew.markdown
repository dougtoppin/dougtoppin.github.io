---
layout: post
title: "Yosemite and Broken Brew"
date: 2015-03-14 23:52
comments: true
categories: 
---
If you are running Yosemite on your Mac, use or have brew installed and have not used brew in a while you might find that it is broken.
you might see something like this:

    /usr/local/bin/brew: /usr/local/Library/brew.rb: /System/Library/Frameworks/Ruby.framework/Versions/1.8/usr/bin/ruby: bad interpreter: No such file or directory. 
    
There are a variety of posts with different fixes (which did not work for me) but this one worked perfectly. [http://vancelucas.com/blog/fixing-homebrew-on-osx-yosemite-10-10/](http://vancelucas.com/blog/fixing-homebrew-on-osx-yosemite-10-10/)

It ended up being the simplest fix (no edits required) for me.
I tried two others and had to back both out for various reasons.

What prompted me to use `brew` was that I am always interested in static sites and stumbled on `Hugo` at [http://gohugo.io/](http://gohugo.io/) and wanted to give it a try.
More to come on that.
