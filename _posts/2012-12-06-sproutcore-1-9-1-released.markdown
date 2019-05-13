---
author: admin
comments: false
date: 2012-12-06 05:16:42+00:00
layout: post
link: http://blog.sproutcore.com/sproutcore-1-9-1-released/
slug: sproutcore-1-9-1-released
title: SproutCore 1.9.1 Released
wordpress_id: 2070
tags:
- Release
---

We are pleased to announce the immediate release of **SproutCore 1.9.1**.  This release contains important fixes to the 1.9 code-base and is fully backwards compatible.  We recommend that all users of SproutCore upgrade to this latest version in order to get the best development experience.  To upgrade to the latest version, simply run:

`gem update sproutcore`

This is a patch release and contains the following bug fixes:



	
  * Fixes a bug that left childView elements in the DOM when they were rendered as part of their parent's layer and the child was later removed.

	
  * Fixes improper implementation of SC.SelectionSet:constrain() that prevented the last object in the set from being constrained.

	
  * Fixes minor memory leak due to implicit globals in SC.MenuPane.

	
  * Fixes memory leak with child views of SC.View. The 'owner' property prevented views from being able to be garbage collected when they were destroyed.

	
  * Fixes SC.stringFromLayout() to include all the layout properties.

	
  * Fixes the excess calling of parentViewDidResize() on child views when the view's position changes, but it's size doesn't.

	
  * Fixes an issue that occurs with SC.ImageView's viewDidResize implementation, where it fails to resize appropriately.

	
  * Fixes a bug in SC.Locale that caused localizations to be overwritten by the last language localized.

	
  * Fixes SC.Request's application of the Content-Type header. It was incorrectly adding the header for requests that don't have a body which would cause some servers to reject GET or DELETE requests.

	
  * Fixes a bug where SC.Record relationships modified within a nested store, would fail to propagate the changes to the parent store if isMaster was NO in the toOne or toMany attribute.


As always, every bug fix includes an accompanying unit test to ensure that the bug does not re-appear in the future.  For further details, please view the complete [Change Log](https://github.com/sproutcore/sproutcore/blob/master/CHANGELOG.md).
