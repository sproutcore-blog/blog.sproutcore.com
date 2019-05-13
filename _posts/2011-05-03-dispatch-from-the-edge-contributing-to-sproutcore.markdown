---
author: gmoeck
comments: true
date: 2011-05-03 13:09:00+00:00
layout: post
link: http://blog.sproutcore.com/dispatch-from-the-edge-contributing-to-sproutcore/
slug: dispatch-from-the-edge-contributing-to-sproutcore
title: 'Dispatch From The Edge: Contributing To Sproutcore'
wordpress_id: 728
post_format:
- Aside
tags:
- Community
- Dispatch
- Video
---

The recent release of 1.5 has brought many new people to SproutCore, and as our community grows, more and more people are asking how they can help. This week, instead of focusing on whats new, I'm going to focus on how **you** can contribute to the bleeding edge of SproutCore. I'll start with my top three suggestions.


## 1. Contribute to the SproutCore Guides


Back in the beginning of January, we recognized that the biggest challenge to new users trying to learn SproutCore was the limited quality and quantity of documentation. To solve this problem the [SproutCore Guides](http://guides.sproutcore.com) project was born. To date, 15 guides have been completed and made available to the community, drastically improving the help that is available for people. But there's still more work that can be done.


### How can you start helping?


To be able to contribute to the project, the first thing you need to do is build the guides on your own system. In order to do that, do the following:



	
  1. Download and install the [guides package](http://guides-pkg.strobeapp.com/Guides.pkg)

	
  2. Clone the guides source from git://github.com/sproutcore/sproutguides.git (git clone git://github.com/sproutcore/sproutguides.git within the directory you want to work).

	
  3. cd into the cloned directory (sproutguides), and run "guides build" to generate an the output directory, where you can build the files locally.


Once you've set up the directory, you can modify any of the files within the source directory.

Next, run "guides generate" to see them reflected in the output. The following video illustrates a typical workflow:



If you're interested in writing a new guide for a section of SproutCore that hasn't yet been covered, contact Yehuda at wycats@sproutcore.com with your idea.


## 2. Contribute to the Source Itself


There are two ways that you can contribute to improving the code of SproutCore itself. <!-- more -->


### Report Bugs


The first way you can help is by reporting any bugs that you find while working with SproutCore. We try the best we can to keep them out before releases, but we know they still exist. You can be our eyes and ears letting us know when we have a problem.

You can report these bugs to us by filing an issue within the SproutCore repository on GitHub. Please be as descriptive as you can within your description—we would much rather have too much information than not enough.

Also, if you're able to write a failing unit test for the bug that you're reporting, this will enable us to address your issue much faster. Along those lines, you could even go and write unit tests for other issues that have been submitted, and I guarantee you would get on the good side of the core team very quickly.

The following video illustrates how to file issues, and write a unit test:





## 3. Modify The Source Yourself


The last way for you to help is to directly modify and improve the source code of SproutCore. In order to do that, the first thing to do is to get the source itself. You can git clone our repository from `git://github.com/sproutcore/sproutcore.git.`

Once you've the source, you might need a little direction to be able to know where everything is because the source itself is structured a little differently than a regular SproutCore application. This video walks you through the file structure of the code base:



I won't go into how to modify the code, because being professional developers, I'm sure you already know how to do that. The only other thing that really needs to be covered is how to run the SproutCore unit tests.

SproutCore relies on its build tools for its unit tests, so the way that you run your tests is a little different than in Ruby or Java. In order to run the SproutCore unit tests, you actually hit a URL in your browser which tells the build tools which tests to run. The URL structure looks like this:

`localhost:4020/static/FRAMEWORK_NAME/en/current/tests[/further_refinements*].html`

So, for example, if I wanted to run the core_foundation tests, I would hit the following URL:

`localhost:4020/static/core_foundation/en/current/tests.html`

If I wanted to only run the tests for the controllers in core_foundation, I would hit the following:

`localhost:4020/static/core_foundation/en/current/tests/controllers.html`

This video will give you an example of how to run those unit tests:





## Conclusion


Hopefully this post has given you the motivation and tools to contribute back towards the SproutCore edge. If you run into any issues, feel free to track me down, and I'd be glad to help. You can tweet at me [@gregmoeck](http://twitter.com/gregmoeck), or ping me at gmoeck on IRC.

I'll be back soon with the next post in Dispatches from the Edge; see you then!
