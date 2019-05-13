---
author: admin
comments: false
date: 2013-11-25 19:24:54+00:00
layout: post
link: http://blog.sproutcore.com/sproutcore-1-10-2-release/
slug: sproutcore-1-10-2-release
title: SproutCore 1.10.2 Release
wordpress_id: 2265
---

SproutCore 1.10.2 is now available. This is a patch level release and includes the following fixes:



	
  * Fixed problems with keypress handling in IE8 and Opera.

	
  * Fixed the swap transition plugin, `SC.ContainerView.REVEAL`, to properly reset the content view's layout after transitioning out.

	
  * Fixed a problem with `SC.View.prototype.cancelAnimation(SC.LayoutState.CURRENT)` that failed to stop at the proper top or left positions when using CSS transform animations when the top or left values were negative. This also improves the `SC.ContainerView.PUSH` transition, making it possible to push multiple content views without overlapping (see [example](http://showcase.sproutcore.com/#ui/SC.ContainerView)).

	
  * Fixed `SC.ContentValueSupport` to notify a change to each of the dependent content keys when the content changes entirely (i.e. the '*' property changes).

	
  * Fixed `SC.SelectView` to update correctly when its items collection is replaced.

	
  * Fixed `SC.AutoMixin` to prevent the attributes from the former child views being applied to the latter child views.

	
  * Fixed locally-scoped 'and' & 'or' bindings.

	
  * Fixed a problem when the initial `isEnabled` value of a view is `false`, that failed to update the `isEnabledInPane` value of that view and its child views.

	
  * Fixed the problem that setting the `isEnabled` value to `true` of a view which had disabled ancestors, could change the value of `isEnabledInPane` for that view to `true`.

	
  * Fixed `SC.TextFieldView` being able to still be edited if it had focus at the same time that an ancestor view was disabled.

	
  * Fixed the `defaultTabbingEnabled` property of `SC.TextFieldView` to actually prevent tabbing when the property is set to `false`. Also added `insertBacktab` handler support to `interpretKeyEvents` in order to prevent tabbing on shift-tab in `SC.TextFieldView`.

	
  * Added missing support for touch events to `SC.PopupButtonView`.

	
  * Fixed a bug that caused `SC.TextFieldView` hints to have a `0px line-height` at times.

	
  * Fixed a regression in collection views that prevented them from properly re-rendering when inside nested scroll views.

	
  * Removed a duplicate listener on `selectstart` events in `SC.RootResponder`.

	
  * Removed the jQuery ready hold in `SC.platform` that was used to delay launching of the app until the transition and animation event names tests completed. Several browsers will not run the transition/animations in hidden tabs, which slows and possibly blocks an app from launching. Since the results of these tests are used only to optimize the event listeners set up in `SC.RootResponder`, the code has been changed to setup the root responder at whatever point the tests successfully finish.

	
  * Fixed picker panes failing to popup in the wrong place if they have some form of resizing. Added an observer to `SC.PickerPane` border frames so that the pane will re-position itself if it changes size.

	
  * Removed the appearance of an `undefined` attribute in `SC.TextFieldView`.

	
  * Fixed internal identification of IE7 to prevent any possible future version of Trident from being mistaken for IE7.

	
  * Fixed a minor memory leak when manually removing event listeners from an element.

	
  * Fixed a minor memory leak when using `SC.InlineTextField`.


