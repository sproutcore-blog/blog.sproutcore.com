---
author: dcporter
comments: false
date: 2014-08-07 19:19:49+00:00
layout: post
link: http://blog.sproutcore.com/dispatch-horizontal-list-view/
slug: dispatch-horizontal-list-view
title: 'Dispatches from the Edge: ListView Goes Sideways'
wordpress_id: 2297
tags:
- Dispatch
---

`SC.ListView` has a new trick in the upcoming v1.11 (available now on [latest master](https://github.com/sproutcore/sproutcore/)): a new `layoutDirection` property which can turn it from vertical to horizontal with one line of code. It's a long-requested feature, and now it's as easy as `layoutDirection: SC.LAYOUT_HORIZONTAL`.

In support of this brave new world, a number of list view properties have new names, replacing all now-outdated mentions of "height" with "size": `rowHeight` is now `rowSize`, et cetera. The new API is backwards-compatible with the old one, with the usual crew of helpful developer warnings to ease your project over without breaking it.

Happy horizontaling!
