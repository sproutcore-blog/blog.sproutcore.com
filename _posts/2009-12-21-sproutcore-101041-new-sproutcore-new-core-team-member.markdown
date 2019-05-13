---
author: admin
comments: true
date: 2009-12-21 18:39:00+00:00
layout: post
link: http://blog.sproutcore.com/sproutcore-101041-new-sproutcore-new-core-team-member/
slug: sproutcore-101041-new-sproutcore-new-core-team-member
title: 'SproutCore 1.0.1041: New SproutCore, New Core Team Member'
wordpress_id: 70
post_format:
- Aside
tags:
- Team
---

I pushed a new gem today.  SproutCore 1.0.1041/1.0.1042 (both build numbers point to the same release due to a bug in Gemcutter) is mostly a maintenance release with lots of minor bug fixes, but it also includes experimental support for an exciting new feature called SC.Animatable.




SC.Animatable is a mixin you can apply to a view which will then automatically animate certain properties on the view (such as layout or opacity).  Animatable makes it terribly easy to make your UI rich and fluid.  Over the next year, we will be building on this API to make sure it works well across all browsers and scales well with bindings, so stay tuned.




Along those lines, I am also pleased to announce that the author of SC.Animatable, [Alex Iskander](http://create.tpsitulsa.com/blog/) ([ialexi](http://github.com/ialexi) on Github) is joining the SproutCore Core Team.  He owns the new sproutcore/animation framework for now along with some other cool features he has in the pipeline.  For a preview of his work, checkout his profile on Github.




Welcome to the team Alex!




Here's a full rundown of the changes in 1.0.1041:




**SPROUTCORE 1.0.1041:**




  1. yui-compressor now runs once at the end of a build, significantly shortening build time for many projects.


  2. Added Button Hold behavior for SC.Button.  Holding a button will repeatedly fire an action (think arrow buttons on a scroll bar)


  3. Improved SC.Logger


  4. Incorporated rough draft of new SC.Animatable framework


  5. Minor bug fixes - mostly tweaks required for better IE7 support


  6. Improved documentation on a few methods


  7. Added a logging for invokeOnce() and invokeLater() making it easier to track when these events occurs and what caused them


  8. Moved some images into themes so they won’t load when Apple uses its own private theme


  9. Fixed some bugs in SC.SheetPane introduced when merging the public source code


  10. Added didAppendLayer and willRemoveLayer callbacks to SC.View so we can add events for video tags


  11. Added SC.get() which works on any object, even null values


  12. Added SC.WellView


  13. New animating SC.SheetPane


  14. Better support for SC.DateTime


