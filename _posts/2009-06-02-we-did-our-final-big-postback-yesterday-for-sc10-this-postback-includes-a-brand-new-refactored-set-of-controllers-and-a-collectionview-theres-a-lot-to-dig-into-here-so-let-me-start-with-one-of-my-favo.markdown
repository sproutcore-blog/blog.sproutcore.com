---
author: admin
comments: true
date: 2009-06-02 18:51:00+00:00
layout: post
link: http://blog.sproutcore.com/we-did-our-final-big-postback-yesterday-for-sc10-this-postback-includes-a-brand-new-refactored-set-of-controllers-and-a-collectionview-theres-a-lot-to-dig-into-here-so-let-me-start-with-one-of-my-favo/
slug: we-did-our-final-big-postback-yesterday-for-sc10-this-postback-includes-a-brand-new-refactored-set-of-controllers-and-a-collectionview-theres-a-lot-to-dig-into-here-so-let-me-start-with-one-of-my-favo
title: We did our final big postback yesterday for SC1.0.  This postback includes
  a brand new refactore
wordpress_id: 153
post_format:
- Image
tags:
- Features
---

We did our final big postback yesterday for SC1.0.  This postback includes a brand new refactored set of Controllers and a CollectionView.  There's a lot to dig into here, so let me start with one of my favorite features: Outlines.




Drawing an outline view is actually pretty tricky.  For the most part, you're simply displaying a list of items with some items indented more than others.  SproutCore's new CollectionView comes with support for inspecting a content array of items and rendering it as a tree, which is pretty cool.




Of course, usually your data structure for outlines is usually some kind of tree; not a flat list.  Keeping track of all the nodes in this tree to generate the list can be fairly difficult.




Until now at least.




The new [SC.TreeController](http://github.com/sproutit/sproutcore/blob/2b0ca5dbd25c2ca087133ab34720770a721342d9/frameworks/foundation/controllers/tree.js) in SproutCore 1.0 accepts a root node for any tree-like data structure and automatically generates a flattened outline list suitable for display in a collection view.  It keeps track of changes to your data model and automatically updates this list as needed.




There are still a lot of bugs here - this is new code afterall - but I've put together a little demo app so you can see what I'm talking about.  It's called "Outline" and its available on our demo site here:




[Outline Demo »](http://woot.sproutcore.com/outline)




We're still chasing down a perf bug in Firefox for this so I suggest checking it out in a Webkit browser for now.    We'll be publishing the code shortly.




Just another example of how SproutCore 1.0 can handle large amounts of data in the cloud with ease. (and without pagination!)
