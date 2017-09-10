---
layout: post
title: "Static Website Photo Gallery Generator"
date: 2015-05-11 22:59
comments: true
categories: 
---
Some months ago I needed to host a simple photo gallery and decided to do it with a static site hosted in an AWS S3 bucket.
Using a static website is the simplest (and likely cheapest) approach for hosting material but it does require that the html be generated and then uploaded to the bucket along with the needed images.
For that first attempt I used the FGallery tool which worked reasonably well but it does not support directories so all of your pictures will be at one level.

The next site that I needed to generate had to have a number of directories for organization so I looked around for another generator tool and stumbled on [ThumbsUp](https://github.com/rprieto/thumbsup)

This worked very well for me and did exactly what I needed so I decided to pass along what I did to use it.
One important thing to note is that the archive organization that I want is a top level directory with subdirectories under it for each photo set.
`thumbsup` worked very well for that.

To run ThumbsUp (a NodeJS tool) I used an AWS EC2 Ubuntu m3.medium instance.
I could have done it on my MacBook Pro but I decided to use a bigger than usual EC2 instance just for the experience.
Note that using a bigger instances may be more expensive than the free or cheap tiers but they may also get the job done more quickly.

Here are the steps that I followed:

* start up your EC2 instance, note that if you start it using a roll with S3 read/write access then you should not need your account credentials later

* ssh into a shell on your new instance

  ssh -i yourkeypair ubuntu@ip
  
* if necessary, copy your AWS account credentials to ~/.aws/config, these will be used by the AWS S3 cli to copy your files into your bucket

* bring the instance up to date

  sudo apt-get update
  
* install the AWS cli, if you use an AWS AMI then the cli will likely already be on it

  sudo apt-get install awscli

* install NodeJS, note that you will have to link the binary to the correct name `/usr/bin/node`

  sudo apt-get install nodejs
  
  sudo ln -s /usr/bin/nodejs /usr/bin/node

* install npm (which will be used to install ThumbsUp)

  sudo apt-get install npm
  
* now install ThumbsUp

  sudo npm install -g thumbsup

* install GraphicsMagick and ImageMagick

  sudo apt-get install ImageMagick graphicsmagick
  
* copy your pictures up to the EC2 instance into `picturesdir`

* now run thumbsup specifying your input and output directories, the `original-photos` argument tells ThumbsUp to enable photo downloads for the user, the `original-photos` and `google-analytics` arguments are optional

  thumbsup --input picturesdir --output htmldir --title "My Pictures" --original-photos true --google-analytics xx-xxxxx
  
* create your new bucket and enable the static website hosting property

* now copy your newly generated files into your S3 bucket, note that this will use the S3 cli and include making the files all readable by anyone (the `read=` argument, the `full=` argument enables all access to your AWS authenticated account)

  aws s3 cp htmldir s3://yourbucketname --recursive --grants read=uri=http://acs.amazonaws.com/groups/global/AllUsers full=emailaddress=yourawsaccount
  
* don't forget to terminate your EC2 instance

The site should now be available.
You can find the url in the static website hosting property for the S3 bucket.
The only charges that you should experience are associated with S3 storage costs and the photo transfers for upload and people viewing your new gallery.

Also note that hosting a static site this ways makes worldwide availability a bit easier via AWS CloudFront.



