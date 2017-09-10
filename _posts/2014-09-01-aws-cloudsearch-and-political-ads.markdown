---
layout: post
title: "AWS CloudSearch and political ads"
date: 2014-09-01 15:34
comments: true
categories: 
---
I've been looking for a practical way to use AWS CloudSearch (CS) and found what I think is an interesting application for it.
Since the political season is rapidly approaching we will start regularly getting ads via the USPS.
I have been interested in how often ad content actually differs from each other but visually comparing them would be tough.
CloudSearch may provide an reasonable means of assisting in this area so I am going to scan each ad into a searchable PDF and upload it to CS as I get them.
Note that the OCR process to produce the searchable text may not always be perfect and thus impact the value of the data.

CS provides PDF support as one of the upload type options making it easier to get the process started.
CS has several tiers of use with the lowest cost one being a *Small Search Instance* at $0.100 per hour.
Once you are familiar with the configuration and upload process it is possible to have an instance up in less than an hour so if you do not need full time access to the data then it can be spun up as needed and then deleted.
Import methods include files contained in S3 buckets making it easy to start up using always accessible data.
Part of what makes this process a little easier is that CS can examine your files and suggests potential index fields to enable.

For my usage I am uploading the ad PDFs to an S3 bucket and then using that to populate the data set.
Getting used to the search syntax can take a little experimentation and practice.
An example of a search from a shell looks like this

*curl 'http://search-YOURSEARCHDOMAIN.us-east-1.cloudsearch.amazonaws.com/2013-01-01/search?q=john&return=content' | jq -r -M .hits[]*

	[
	  {
	    "fields": {
	      "content": "John Foust worked with both parties to cut waste, balance budgets, and invest in the future.  7 straight balanced budgets On the Board of Supervisors in Fairfax County, John Foust is known as a fiscal watchdog. John worked with Republicans and Democrats to identify priorities and trim the fat out of the budget. He balanced 7 straight budgets, while still investing in local priorities, like education and transportation.  Here are just a few ways John saved tax dollars: / Consolidated offices and shared printers. Nearly$750K  / Replaced computers, but not good monitors. $1.2 million  / Stopped the phone company from over-billing us. $3 million  / Put an end to useless government studies. Nearly $550K  S Stopped the construction of an unnecessary administrative  building. $110 million  JOHN FOUST for CONGRESS LEADERSHIP, NOT PARTISANSHIP  66 It wasn't easy with  Richmond trying to cut education and ignoring  Northern Virginia's needs, but we worked together because  protecting our quality of life is what counts, not politics. }}  - Uokrt fdusf  © F0USTF0RVIRGINIA.COM o /JOHNFOUSTFORVIRGINIA o ©JOHNFOUSTVA"
	    },
	    "id": "politicalads/johnfoust-01.pdf"
	  }
	]

The output is in json format so this is using the *jq* tool to extract the actual content of the PDF otherwise the output would include file name, creation date and various other fields.

For this ad application I used all default values and followed these steps

* scan ads into searchable PDFs (I use ScanSnap and a Fujitsu S1500M scanner)
* create an S3 bucket dedicated for the PDFs and upload your files
* using the CloudSearch console create a new search domain using the small instance type (*search.m1.small*) and default replication count
* set index fields to *Analyze sample object(s) from Amazon S3*
* select the S3 bucket that contains at least one of your PDFs
* use the *Suggested Index Field Configuration* fields and continue
* For access policies use *Search and Suggester service: Allow all. Document Service: Account owner only*
* confirm the domain creation and wait for a while for it to be created
* once created upload your PDFs from your bucket and it should then be available for you
* once you are finished delete your domain unless you want it always available

I am hoping to continue with this application and will post more details as I continue to set it up.





