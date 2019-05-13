---
author: admin
comments: false
date: 2013-09-03 20:47:11+00:00
layout: post
link: http://blog.sproutcore.com/sproutcore-1-10-0-release-candidate-2/
slug: sproutcore-1-10-0-release-candidate-2
title: SproutCore 1.10.0 Release Candidate 2
wordpress_id: 2191
tags:
- Release
---

We've just published the second release candidate of Version 1.10.0. The first candidate gem was incorrectly packaged and would not work with a regular install. If you've already installed the first release candidate, please run:

    
    gem update sproutcore --pre




# Changes in 1.10.0.rc.2





	
  * Fixes gem problem, which resulted in ``gem_original_require': no such file to load -- bundler/setup` errors when trying to run any of the SproutCore command line tools.

	
  * Removes a developer warning when animating with a duration of 0, which can be valid if the duration is calculated. In any case, animating a duration of 0 has always been supported by `SC.View.prototype.animate`.

	
  * Improves the regular expression used by `SC.RenderContext` to escape strings so that HTML entities like `&apos;` or `&agrave;` are preserved.

	
  * Fixes a regression with `SC.RadioView` that failed to add the `disabled` class to disabled radio items.

	
  * Fixes some internal SproutCore unit tests.


