---
layout: post
title: "Docker for Tools"
date: 2017-02-25 20:40
comments: true
categories: [docker]
description: Save time by using Docker containers for your tools instead of installing them (and all of their dependencies).
keywords: docker
---
Something that I've become a strong believer in is using Docker containers to run tools rather than installing them (and all of their dependencies) on your machine.
This is particularly true if you need to have access to multiple versions of a tool with Java being a good example.

What I mean by this is if you ran everything that you typically need as a container (from a Docker image) you should not need to install anything except Docker itself.

Over any period of time I need to use various versions of Java, Python among others.
I used to keep each version locally installed and then go through a process of setting environment variables (such as PATH) to use what I needed at that moment.
Instead, if I use the tools in Docker containers I can run them at will and never need to upgrade/downgrade or generally mess around with my machine.

Along with this is if you contribute any open source software (such as in Github repos) you should also include a Dockerfile that will run them.
Then also consider creating a DockerHub repo that is set to automatically build Docker images for them.
It is particularly important to include descriptive and usage information about your tool.
The DH automatic build will convey the GH README.md info if you do.
This makes it much easier for people to discover, develop trust in and use your tools.
The perfect world is when you provide a Docker image of your tool and someone being able to simply run it without their having to clone, build (with whatever development environment is required), install and then run your tool.

Since most tools require access to local files include in your usage instructions an example of using the Docker volume argument to let your tool operate of local files.
That might be as simple as something similar to the following
`docker run -v $(pwd):/tmp yourtool:1.0`

Note that you should also include version tags for your tools so that if they change the user can still run what has always worked for them.

If you want to see an example of this approach take a look at the following.
I do not claim to be a pro but I can carry a tune.
[https://hub.docker.com/r/dougtoppin/lenticular/](https://hub.docker.com/r/dougtoppin/lenticular/)

You may find that there are some things that you cannot easily do using Docker.
A couple of examples that come to mind are tools that need access to external devices (such as via USB) or use a GUI.
There may not be an existing way to do those with Docker but most everything else is likely to work well.
However, companies and individuals are coming up with ways around those issues with Nvidia being a good example of that.
They provide a Docker compatible driver that interfaces with their GPU.
This allows containers to make use of very high performance found in that sort of hardware.

The main point is think about using and provide support for Docker.
It will only make things easier for you and people that use your stuff.

