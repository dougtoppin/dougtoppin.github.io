---
layout: post
title: "S3 image storage tidbit"
date: 2013-11-29 22:01
comments: true
categories: 
---
I recently moved my blog from a self hosted Wordpress site to Github pages (where you should be reading from now) started using Jekyll/Octopress.  I've been wanting to get around to adding images to it which is a little more involved when using a static site generator. I first tried using my Flickr account but that proved to be a little aggravating because Flickr wants you to link to their Lightbox view which forces the viewer into a web page.  You can get around that by looking at their BB link and extracting a url to the actual image but that adds another time consuming activity.  Another alternative (if you are familiar with the AWS) is to just upload your image files into an AWS S3 bucket and link directly to them.  However, to do that you need to make the bucket publicly viewable which means adding a policy to the bucket.  I ran across this helpful site which gives an example of a public read only policy:  http://havecamerawilltravel.com/tidbits/how-to-allow-public-access-to-an-amazon-s3-bucket/

