---
layout: post
title: "Junk Mail Processing and Classification Project"
date: 2015-07-26 20:40
comments: true
categories: 
---
I have a project that I am interested that has been sitting on the back burner that I did a little prep work on today.
The project is that my mother in law receives an amazing amount of junk mail and I wanted to capture, compare and analyze it.

I picked up a few weeks of it a while back and scanned it today (117 pieces) which took a couple of hours.
I did the scanning to my MacBook Pro using my Fujitsu S1500M scanner which is pretty quick and will also produce searchable PDFs.
The slowest part of the process was physically opening the envelopes and scanning each set of sheets individually into separate files.
I could have done a bulk scan of all or many of the sheets at once but I could not think of a way to identify each mailing so I had to do them individually.

I intend to do the processing using the AWS.

An overview of what I am going to do follows.

* classify each file
	* you’ve won
	* donation request from charity
	* other
* identify sender
	* look for duplicates
	* address to/from
	* phone numbers
* note key strings
	* name from
	* phone numbers
	* numeric amounts
		* award
		* cost to participate
	* words
		* soldier
	* animal, horse, dog
* note any embedded imagery found
* text processing
	* most used word
	* most used phrase
	* most fear inducing phraseology
	* most official sounding or looking

Architecture/artifacts

* store PDFs in S3
* DynamoDB for metadata (and entire text from PDF?) for each file
	

This will be a background project so I will only be occasionally getting to it.
Please check back for update.
