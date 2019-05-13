---
author: admin
comments: false
date: 2012-05-12 21:49:35+00:00
layout: post
link: http://blog.sproutcore.com/sproutcore-1-8-2-released/
slug: sproutcore-1-8-2-released
title: SproutCore 1.8.2 Released
wordpress_id: 2015
---

<blockquote>_[edit] Due to a mistake in the included files of the published 1.8.2 gem, the gem needed to be re-built.  Therefore the current working version of the gem for SproutCore 1.8.2 is sproutcore-1.8.2.1.  Sorry for any confusion._</blockquote>


We are pleased to announce the release of **SproutCore 1.8.2**. This release contains minor fixes to the 1.8 code-base and will likely be the last patch of 1.8 prior to the 1.9.0 release. To upgrade to the latest version, simply run:

`gem update sproutcore`

This is a patch release and contains the following bug fixes:



	
  * Fixed syntax error in Datastore unit test.

	
  * SC.SplitView can now mixin SC.SplitChild.

	
  * Thinned picker pane border divs so that they don't overlap the content view.

	
  * Prevents target property conflict when configuring button targets with SC.AlertPane.

	
  * Changed the aria-orientation of horizontal SC.ScrollView to 'horizontal' from 'vertical'.

	
  * Allows SC.CollectionFastPath to work with sparse content by always returning an item view even when content isn't yet available.

	
  * Prevents SC.GridView from iterating over its content array in order to work with sparse content.

	
  * The 'mobile-safari' body class name is no longer being added in all browsers.

	
  * Enables pasting in SC.TextFieldView to notify that the value changed.

	
  * Prevents default touch behavior being intercepted on <textarea> and <select> elements.


