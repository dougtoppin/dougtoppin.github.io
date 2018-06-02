---
layout: post
title: "Which to use for private repositories, GitHub or AWS CodeCommit?"
date: 2018-06-02 15:15
comments: true
categories: [blog]
description: Should I continue to pay for GitHub private repositories or should I switch to using AWS CodeCommit
keywords: aws github codecommit
---
I have paid for a GitHub account for some years with the reason being able to create multiple private repositories.
This gives me the convenience of having a central place for keeping some files that I need to share between several computers.
I never share or collaborate any of my private repos at least so far.

I have been using AWS CodeCommit on a limited basis for some time and have been considering whether or not I should just move my GitHub private repositories to CodeCommit repos and stop paying GitHub.

[CodeCommit pricing](https://aws.amazon.com/codecommit/pricing/) is very likely going to not cost me anything where GitHub is costing me $7 per month.

Using CodeCommit is a little more involved than GitHub but not a decision maker by any comparison.

I use a Mac and have to fiddle around at times to let me be able to use CodeCommit and ran across a tip a while back that is very useful.
I unfortunately do not remember where I saw this but adding the following to my ~/.ssh/config file lets me use CodeCommit without any trouble on my Mac.

The ```MySshKeyId``` value is from my IAM account console ```SSH keys for AWS CodeCommit``` area.
The ```keyfile``` is my private key that I created for CodeCommit.

```
Host git-codecommit.*.amazonaws.com
    User MySshKeyId
    IdentityFile ~/.ssh/keyfile
```

I would appreciate hearing from anyone that has thoughts, opinions or experiences on this subject.
