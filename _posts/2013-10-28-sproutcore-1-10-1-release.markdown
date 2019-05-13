---
author: admin
comments: false
date: 2013-10-28 15:31:51+00:00
layout: post
link: http://blog.sproutcore.com/sproutcore-1-10-1-release/
slug: sproutcore-1-10-1-release
title: SproutCore 1.10.1 Release
wordpress_id: 2241
tags:
- Release
---

The first patch release of SproutCore 1.10 is now available. This update includes the following fixes:



	
  * Allows inline text fields to work with automatic child view layout.

	
  * Fixed `SC.Module` loading for IE11 and future versions.

	
  * Fixed `SC.Drag` cancellation with the Escape key to call dragEnded for cleanup.

	
  * Added a retina image for the default theme of `SC.MenuPane`.

	
  * Fixed the touch selection of `SC.CollectionView` to prevent an item from appearing deselected when touched twice in a row.

	
  * Fixed the insertion point code for `SC.GridView` in order to show an insertion view when dragging and dropping onto grid views.

	
  * Fixed an issue with `SC.ScrollView` which would cause the HW accelerated content offset to be incorrect when the content view re-renders.

	
  * Improved the deceleration animation of `SC.ScrollView` for better performance.

	
  * Fixed an error in the deceleration animation of `SC.ScrollView` that could throw an exception when stopped very quickly.

	
  * Changed the `SC.EmptyTheme` class name to `sc-empty-theme` to avoid conflicts with the use of `sc-empty`. This fixes a bug where `SC.ProgressView` would always appear empty when used with the empty theme.

	
  * Fixed incorrect behavior of `SC.Statechart sendEvent` that allowed events to be sent during a state transition.

	
  * Fixed a bug that prevented queued events due to a state transition from being sent when the state transition was complete.

	
  * Fixed a caching problem with `SC.routes` that would allow the location property to be incorrect depending on how it was changed.

	
  * Fixed a regression in determining the OS of Linux and Android in `SC.browser`.


