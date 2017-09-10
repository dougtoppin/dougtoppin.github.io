---
layout: post
title: "Jekyll Experiences Update"
date: 2016-02-08 21:10
comments: true
categories: [blog]
description: Update on my experiences in using Jekyll for my static site blog
keywords: blog, jekyll

---
I've used a few different blogging platforms over a few years with Jekyll being my most recent starting months ago.
I chose Jekyll because I wanted a static site blog rather than a dedicated instance running a blogging platform.
I also wanted to have it hosted using GitHub Pages.

Jekyll is a markdown based blogging system that provides the basics.
I had no real problems with it until I tried a recent Jekyll 3.x update and was no longer able to create the site.

I ran across errors like this

    $ bundle exec rake generate

    Generating Site with Jekyll
    identical source/stylesheets/screen.css
    Configuration from dougtoppin.github.io/_config.yml
    Building site: source -> public
    Liquid Exception: Unknown tag 'include_array' in post
    /Library/Ruby/Gems/2.0.0/gems/liquid-2.3.0/lib/liquid/block.rb:62:in `unknown_tag'
    /Library/Ruby/Gems/2.0.0/gems/liquid-2.3.0/lib/liquid/tags/if.rb:31:in `unknown_tag'
    /Library/Ruby/Gems/2.0.0/gems/liquid-2.3.0/lib/liquid/block.rb:32:in `parse'
    
After spending a few hours over a few evenings trying to figure out what I missed in either the update or configuration changes I finally gave up on Jekyll 3 and reverted with this

    $ sudo gem install jekyll -v 2.5.3
    
After that, and reverting the changes I had made to `_config.yml` and `Rakefile` I appear to be back to normal and am able to post again (if you are reading this then it was successful).

The real intent of this post is to pass along my thoughts of using Jekyll, static sites or blogging in general.
I like static sites because they provide the lowest cost platform while still giving you some element of creativity.
The drawback of course is that if you want something simple that just lets you post you may be in for trouble particularly in terms of updates to the system.
It is also important to ensure that whatever system your choose you are preserving your posts in a manner that lets you rehost them or migrate to another system.
I think that both GitHub Pages and markdown based systems provide those abilities but you will probably have to experiment and learn a little more than you might have intended.

More to come on this subject.
