---
author: dcporter
comments: false
date: 2013-10-28 23:48:04+00:00
layout: post
link: http://blog.sproutcore.com/1-10-upgrade-splitview/
slug: 1-10-upgrade-splitview
title: 'v1.10 Upgrade Tips: New SC.SplitView'
wordpress_id: 2244
---

One of the underpublicized changes we made in v1.10 was the inclusion of a great new `SC.SplitView`. The existing view was broken in some key ways, and the new view, which had been marinating in an experimental framework for some time, was snazzy and stable. We decided that few enough people had gotten `SplitView` working in their production apps that we could afford to swap in the new view, but it's API-noncompliant and we should have made a bigger deal about it. Sorry about that!

Luckily, updating to the new `SplitView` is easy. The most important thing to do is mix `SC.SplitChild` into your `topLeftView` and `bottomRightView`. If you want your views to have an initial height or width, depending on `layoutDirection`, just set the `size` property (whole-number pixel values only). The best news is that a `SplitView` can now handle an arbitrary number of sections – you specify them in its `childViews` array, just like a normal view.

Full documentation for the new SC.SplitView available [here](http://docs.sproutcore.com/#doc=SC.SplitView&src=false); more information about the new SplitChild mixin available [here](http://docs.sproutcore.com/#doc=SC.SplitChild&src=false).
