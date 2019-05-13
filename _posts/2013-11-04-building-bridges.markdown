---
author: admin
comments: false
date: 2013-11-04 19:52:37+00:00
layout: post
link: http://blog.sproutcore.com/building-bridges/
slug: building-bridges
title: Building Bridges
wordpress_id: 2252
---

This post is about one of the most important goals of SproutCore, _making web app development easier and faster_. SproutCore has always been largely about really fast app performance, but in many ways the performance benchmarks of a framework are only as good as the real world performance of the developers using that framework. Therefore, we wanted to highlight a number of recent additions to SproutCore purely for the purpose of helping developers create even faster SproutCore applications even faster.

<!-- more -->

For instance, one of the least publicized changes in version 1.10 is the large number of additional debugging statements in order to help guide developers to the source of any problems. These range from general warnings, prefixed with "Developer Warning:", that should be fixed  before release, to outright errors prefixed by "Developer Error:" that must be fixed immediately.

For example, if you had a missing child view named in the `childViews` array previously it would throw an exception that had to be tracked down. In the latest version however, if your `childViews` array had a value "missingLabel" with no matching property for example, you would see the following in the console and your app would continue to run:

    
    "Developer Warning: The child view named 'missingLabel' was not found in the view, SC.View:sc1247 (ATTACHED_SHOWN). This child view will be ignored."


Warnings like these serve to alert you of possible bugs without getting in the way of testing. In this case, a quick search for the value 'missingLabel' would highlight the source of the problem. There are also instances where a developer will do something unintentional that would cause unknown and hard to diagnose bugs in the app. For example, it was previously taboo to set the `layerId` property of a view, because this is how SproutCore maps view objects to DOM elements and if you ever accidentally created two views with the same `layerId`, your views would suddenly behave very strangely. However, with the new approach we can confidently use `layerId` in 1.10+, because if we ever accidentally used the same `layerId` twice we would see the following on the console with a full stack trace:

    
    "Developer Error: A view with layerId, 'duplicateId', already exists.  Each view must have a unique layerId."


_Of course, we fully leverage SproutCore's development tools so that all of this debug code is stripped from production builds_, so don't worry about these messages adding to the code weight. In fact, in 1.10 we marked tens to hundreds of lines of existing debugging code for debug mode only at the same time as we added many new helpful messages. The overall result is a clearer debug process at the same time as a smaller production package.

Two other useful additions worth mentioning that came out shortly before 1.10 are the [SproutCore Debug inspector pane for Chrome](https://chrome.google.com/webstore/detail/sproutcore-debug/kdjpmpfkllnnjndcfoefebpajggihpni) and the [SproutCore package for Sublime Text 2](https://sublime.wbond.net/packages/SproutCore%20Snippets%20and%20JSHint%20Integration). The first is a free addition for Chrome's inspector that lets you inspect elements and easily see important information about the SC.View object of that element. Accessing the SC.View object in the console becomes as easy as having an element selected and typing `$0v` (or `$0pv` for the parent view). The second is a free package for Sublime Text 2 that adds several SproutCore specific snippets and automatically integrates in JSHint to flag JavaScript bugs early and enforce code cleanliness and consistency in your team.

Along similar lines, the docs have been built and packaged into the documentation browsing app [Dash](http://kapeli.com/dash). Dash provides nice and fast local access to multiple doc sets.

As well, the SproutCore docs have seen a lot of love in 1.10 with many fixes, additions and the removal of any internal only docs. Of course there's always room for improvement and work on the docs and guides continues each day. Fortunately, for those that want even more in depth detail on SproutCore right now, the first [official SproutCore book](http://www.packtpub.com/creating-html5-apps-with-sproutcore/book) is now available from Packt publishing.

So in conclusion, we hope that these additions make a positive difference for you in your own projects each day and please trust that many more improvements are on their way.

_Note: Every part of SproutCore is open source, including the [Website](https://github.com/sproutcore/website), [Guides](https://github.com/sproutcore/guides), [Docs](https://github.com/sproutcore/docs), [Chrome inspector pane](https://github.com/sproutcore/add-ons) and [Sublime Text 2 package](https://github.com/sproutcore/sproutcore-sublime-text-2-package). If you'd like to see even more improvement to any of these, please consider contributing yourself._
