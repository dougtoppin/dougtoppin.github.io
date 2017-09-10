---
layout: post
title: "AngularJS static site propane calculator tool"
date: 2014-08-31 15:32
comments: true
categories: 
---
In our area it is most convenient to replace your gas grill propane tank with a full one at local stores such as Home Depot rather than actually refill your own tank.
The difficulty with this is knowing when your tank is nearing empty so that you are not paying for replacement propane when you still have enough remaining.
The keys to knowing how much gas usage time that you have remaining are to know how much propane is still in your tank and how much is used by your grill.
The grill usage is recorded in BTUs (such as 12,000) and weighing your tank and subtracting that weight from the empty weight (Tare Weight) to get the amount remaining.

I decided to write a simple AngularJS page to calculate this and wanted to host it using a static site in an AWS S3 bucket.
This is not at all a difficult process and I particularly like static site hosting (as opposed to having the html on an EC2 or other compute instance).
Advantages of static hosting (in the S3 for example) include putting it up really quickly, not being concerned about scaling nor security.
Of course it is limiting to not have a server behind the code for enhanced functionality but for things like this the trade off is worth the limitations.

The set up of the static site is trivial in that the bucket holding the code only requires the static site flag being set.
For ease of use it is worthwhile to also use Route53 to create a domain (CNAME in my case) to point to it.

With my use of this tool I ended up cooking with it 3 more times than I typically would have in the past because I had greater confidence that I could predict how much usage time remained.

The result can be found at [http://propanecalculator.dougtoppin.name/](http://propanecalculator.dougtoppin.name/).

 