---
layout: post
title: "Using Docker for quick actions"
date: 2015-02-05 14:59
comments: true
categories: 
---
Docker can be very helpful for quick activities where you just want to accomplish some task and then not leave any "leftovers" when it completes.
A simple example of this might be where you want to use something available on Linux rather than install it on your host machine.
One challenge to note that is there is no direct Docker command to copy a file from the host to the container without building a new image.
This can be easily overcome using the Docker `exec` command.

Let's say that you receive a file in `7zip` archive format and need to extract the contents.
If you do not want to install a suitable unarchiver on your machine you could perform the following steps.
Note that each line starts with `host` or `container` to indicate where the action is performed.
This assumes that you already have a working Docker environment.
You will need two shell terminals, one for the Docker container interaction and one for your host commands.

Start a stock image Ubuntu container and go directly into the shell

    host: docker run -i -t ubuntu

Bring Ubuntu up to date (which should make it aware of the `p7zip` package) and then install the package
   
    container: # apt-get update
    container: # apt-get install p7zip
    
Using `ps` get the container id
    
    host: docker ps

The container id will be a string that looks something like `d6e2146e1d94`.
There are a few methods to copy files from a host to a container that involve additional steps such as mounting disk volumes which can be more complicated if you are using a Mac and `boot2docker`.
A simpler way is to use the Docker `exec` command as follows
    
    host: cat archivefile.7z | docker exec -i CONTAINERID sh -c 'cat > /tmp/archivefile.7z'

Now from your container shell do the archive extract and next create a compatible archive format that you can read (such as a `tarball`). Note that `p7zip` will delete the archive file when it completes the unarchive.
    
    container: # cd /tmp
    container: # p7zip -d archivefile.7z
    container: # tar cvf archivefile.tar *
    
Now copy the newly created archive file back to your host machine (which can use the Docker `cp` command) 
    
    host: docker cp CONTAINERID:/tmp/archivefile.tar .
    
The container can be exited

    container: # exit

The new resulting `archivefile.tar` can be found in your current directory.


    