---
author: admin
comments: false
date: 2015-01-08 21:54:42+00:00
layout: post
link: http://blog.sproutcore.com/sproutcore-1-11-0-release-candidate-3/
slug: sproutcore-1-11-0-release-candidate-3
title: SproutCore 1.11.0 Release Candidate 3
wordpress_id: 2361
---

The final release candidate for version 1.11.0 is now available.

This release candidate fixes a few of the remaining bugs and addresses the regressions that had crept in since RC1. It also introduces several improvements and nice new features, such as the ability for `SC.PickerPane`s to pop "out" of their anchors when using a scale `transitionIn` plugin (i.e. `SC.View.SCALE_IN`) for a really nice effect or the ability to easily check for conflicts between a nested store and its parent using the new `conflictedStoreKeys` property. For a list of all the changes, please view the detailed change log which can be seen here: [SproutCore CHANGELOG](https://github.com/sproutcore/sproutcore/blob/master/CHANGELOG.md).

To install SproutCore 1.11.0.rc3 for testing, please upgrade your previous version of SproutCore by running the following:


    
    <code>gem update sproutcore --prerelease
    </code>



We will be using your feedback over the next couple weeks to finalize 1.11.0, so please be sure to try it out and let us know what issues remain: [Github Issues](https://github.com/sproutcore/sproutcore/issues). To discuss the next version or to discuss SproutCore in general, as always please use #sproutcore on IRC or email to [sproutcore@googlegroups.com](mailto:sproutcore@googlegroups.com).
