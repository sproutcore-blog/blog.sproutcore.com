---
author: admin
comments: false
date: 2014-12-10 17:02:50+00:00
layout: post
link: http://blog.sproutcore.com/sproutcore-1-11-0-release-candidate-2/
slug: sproutcore-1-11-0-release-candidate-2
title: SproutCore 1.11.0 Release Candidate 2
wordpress_id: 2355
tags:
- Release
---

The next release candidate for version 1.11.0 is now available.

This release candidate addresses a few bugs, makes some important under-the-hood improvements (e.g. SC.View layout update performance, reducing SC.Event memory churn, avoiding leaking `arguments`) and updates the API of SC.ActionSupport. The detailed change log can be viewed here: [https://github.com/sproutcore/sproutcore/blob/master/CHANGELOG.md]()

To install SproutCore 1.11.0.rc2 for testing, please upgrade your previous version of SproutCore by running the following:


    
    <code>gem update sproutcore --prerelease
    </code>



We will be using your feedback over the next few weeks to finalize 1.11.0, so please be sure to try it out and let us know what issues remain: [Github Issues](https://github.com/sproutcore/sproutcore/issues). To discuss the next version or to discuss SproutCore in general, as always please use #sproutcore on IRC or email to sproutcore@googlegroups.com.
