---
layout: post
title: "GitPitch for Presentations"
date: 2017-05-12 18:21
comments: true
categories: [tools]
description: GitPitch is an online tool that renders markdown for presentations.
keywords: gitpitch
---
I occasionally do presentations on technical topics and have never been able to settle on what format/tool to do them in (txt, pdf, ppt, md).
I've tried a wide range of tools and recently have been trying to stick with using markdown for the content.
Of course this means using something else to render for viewing.

I recently ran across [GitPitch](https://gitpitch.com/) and decided to give it a try for my next presentation.
GitPitch is an online tool that takes as an argument your Github or other repo and a markdown file called PITCHME.md at the top directory in it.

Assuming it finds that file it will use revealJS to render your markdown as a presentation.
Page navigation is done using the left/right and up/down arrow keys.
Right/left can be considered major topic slides and the up/down are slides associated with each major topic.
This is as opposed to a simple sequential progression of slides.

There are two methods for viewing your presentation while working on it.

One is by using a local markdown editor, pushing the revised file to your repo and then viewing it via the GitPitch url.

The other is that you can download a zip file via the GitPitch url that contains the initial version of your presentation and includes the rendering related js and css type files.
Then you unzip the file and run python in SimpleHTTPServer  mode on the index.html found in the archive and use a browser to preview the content.
After you update your markdown just reload the new version in the browser.
This saves you having to do multiple pushes to your repo particularly while getting the hang of the GitPitch syntax and structure.

Once you are satisfied with your presentation you just send the updated PITCHME.md file to your repo and use the GitPitch url to present.

Something else to be aware of is that `---` and `+++` are used in your markdown for delineating pages.
Using `---` indicates a major slide change (left/right) and `+++` indicates a sub-slide change (up/down) in you content.

So far I have also not been able to find a way to use a remote slide control device with it that includes the up/down actions in addition to the left/right actions while navigating the slides.
I typically use the Logitech Wireless Presenter R400 and have not been able to remap the extra couple of buttons on it to act as up/down keys so far.
Most remote slide control devices do a simple left/right action for slide changes which will continue to work but will just pass through the presentation in the typical sequential manner.
I am pretty sure that I can find a device or phone app that will let me do all navigation actions eventually but no luck so far.

It is a little different to plan and prepare your presentation in a non-linear style when you are used to sequential slides.
It is a good idea to plan your major topics and then each subtopic and then fill them in.

In general GitPitch is interesting and I like using revealJS style presentations but they do have changes in your approach that you need to be prepared for.

It does provide you with greater opportunities for creativity in presenting and can make it easier for someone viewing to get to the sections they are interested in more quickly than just paging all the way through it.
