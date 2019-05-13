---
author: admin
comments: false
date: 2012-10-01 03:56:28+00:00
layout: post
link: http://blog.sproutcore.com/announcing-sproutcore-1-9/
slug: announcing-sproutcore-1-9
title: Announcing SproutCore 1.9!
wordpress_id: 2053
tags:
- Release
---

The SproutCore team is pleased to announce the release of SproutCore 1.9.0.  This release includes several new features, improvements and bug fixes and is a recommended upgrade for all SproutCore developers.

To install the latest version of SproutCore, visit [http://sproutcore.com/install/](http://sproutcore.com/install/).  If you are upgrading from a previous version of SproutCore, simply run:

    
    gem update sproutcore


<!-- more -->


## Highlights of Version 1.9.0


The following list includes the major changes and new features in 1.9.0:



	
  * Introduces [SC.Color](http://docs.sproutcore.com/#doc=SC.Color&src=false), a powerful color utility class that supports many color calculations and transformations and includes the following features:

	
    * Provides rgba feature detection.

	
    * Is able to parse rgb(a), hsl(a), hex and argb values to a normalized rgb space.

	
    * Is able to convert from the normalized rgb space to rgb(a), hsl(a), hex and argb notations.

	
    * Provides hue, saturation and luminosity properties to modify a color.

	
    * To see a demo of SC.Color in action, visit [http://showcase.sproutcore.com/#demos/Using%20SC.Color](http://showcase.sproutcore.com/#demos/Using%20SC.Color).




	
  * Implements support for XMLHttpRequest Level 2 event listeners.  SproutCore's SC.Request function has long provided cross-browser support for "Ajax" requests ensuring that callbacks properly fire regardless of the browser's implementation of the XMLHttpRequest (XHR) standard.  Now that the XHR2 standard is supported in all the latest browsers, SproutCore has been expanded to include it, which allows SC.Request:notify() to be used with either a completion status code like normal or with a new event name, such as 'progress', 'abort' or even 'upload.progress'.

	
  * Updates the media framework to remove several flaws and make it more useable.  This includes the addition of SC.mediaCapabilities for media feature detection and the decoupling of SC.MediaSlider from SC.AudioView and SC.VideoView.

	
  * Replaces the TestControls app with the new Showcase app that appears on the website.  The source for the app is included as a submodule within SproutCore and the app can be run locally at [http://localhost:4020/sproutcore/showcase](http://localhost:4020/sproutcore/showcase) or viewed live at [http://showcase.sproutcore.com](http://showcase.sproutcore.com).  The Showcase app is the result of a lengthy effort to visit each View in the Desktop framework and create working examples for the many different configuration options to serve as a reference to new developers.

	
  * Adds indeterminate support to SC.ProgressView.  SC.ProgressView can now have isIndeterminate set to YES to display a continuous progress bar styled to match the SproutCore theme.  The animation for the continuous bar uses CSS if possible, falling back to a backwards compatible and highly optimized JavaScript animation otherwise.  You can see an example of it[ here](http://showcase.sproutcore.com/#ui/SC.ProgressView).

	
  * Adds vertical layout support to SC.SegmentedView.  SC.SegmentedView can now have its layoutDirection set to SC.LAYOUT_VERTICAL to display a vertically positioned set of segments/tabs styled in the default SproutCore theme.  You can see an example of it [here](http://showcase.sproutcore.com/#ui/SC.SegmentedView).

	
  * Adds 'interpretKeyEvents' support to SC.TextFieldView allowing you to implement special handling of many common keys. For example, it is now easy to submit the value of a field or fields when the 'Return' key is pressed by implementing the insertNewline() method on the text field view. Other interpreted keys are: escape, delete, backspace, tab, left arrow, right arrow, up arrow, down arrow,  home, end, page up and page down.

	
  * Adds the window.requestAnimationFrame() polyfill by Erik Möller:  [http://my.opera.com/emoller/blog/2011/12/20/requestanimationframe-for-smart-er-animating](http://my.opera.com/emoller/blog/2011/12/20/requestanimationframe-for-smart-er-animating).  The core function requestAnimationFrame() provides reliable 60fps JavaScript animations and is used originally by the SC.ProgressView indeterminate animation.  The polyfill ensures that the function can be called anywhere in the code, as is, without a browser specific prefix.

	
  * Improves SC.GridView so that it updates less frequently, can have a minWidth layout in order to scroll horizontally, doesn't overlap items when rotated on a tablet and can work with sparse content, such as provided when working with an SC.SparseArray.

	
  * Adds a new property to SC.Record attributes of type SC.DateTime called 'useUnixTime'.  If 'useUnixTime' is YES, then the record attribute transform will expect a Unix time value instead of the regular SC.DateTime ISO8601 format.  This makes it easier to work with APIs that provide Unix timestamps as times.

	
  * Improves internal support for nested records (i.e. isNested: YES).  The manner in which nested records are created and accessed has been refactored to prevent memory leaks that occurred as nested records were unloaded and reloaded.  This also removes the necessity of specifying primary keys on nested records in order to use them effectively.

	
  * Improves internal support for keys in SC.Record attributes.  Previously, the data hash backing the SC.Record in the store would incorrectly use the attribute names instead of the attribute key names, which meant that it was often unclear to the developer what property name would exist in the record's data hash (ex. 'myAttribute', the name of the attribute, or 'my_attribute', the key name of the attribute).  Now the data hashes consistently contain the attribute key name if it exists.

	
  * Adds support for assigning default values in place of missing properties given to createRecord().  Now a call to SC.Store:createRecord() will check the defaultValue property of each attribute and actually assign the value to the data hash, which is what the majority of developers expect to happen.

	
  * Changes the orderBy syntax on SC.ArrayController to match that of SC.Query and MySQL, which is 'key ASC' or 'key DESC'.

	
  * Automatically parses out URL encoded parameters through the SC.routes params object.  For example, the location 'videos/5?format=h264&size=small&url=http%3A%2F%2Fwww.youtube.com%2Fwatch%3Fv%3DG0k3kHtyoqc%26feature%3Dg-logo%26context%3DG21d2678FOAAAAAAABAA' now properly has  a property "url: 'http://www.youtube.com/watch?v=G0k3kHtyoqc&feature=g-logo&context=G21d2678FOAAAAAAABAA'" in the params object.

	
  * Adds support for the page up, page down, end and home keys in SC.MenuPane menus, which allows the keys to be used to jump to the next or previous page of menu items or to the start or end of the menu items.

	
  * Makes SC.WebView iframes scrollable on iOS.

	
  * Makes SC.StaticContentView clear its previous content if its value is set to null.




Along with new features and improvements, 1.9.0 includes a large number of bug fixes.  Here is a list of the most important fixes:



	
  * Fixes drop support for SC.ListView and implements it in SC.GridView, so that these views can act as drop targets for a drag operation and be styled appropriately.

	
  * Fixes many problems with SC.View:animate() which fixes issues such as the method failing to trigger callbacks or triggering multiple callbacks with grouped animations.

	
  * Fixes a problem with SC.ButtonView on touch devices that resulted in portions or all of the button being untouchable.  This was related to the calculation of the touch boundary, which is meant to improve the touch experience, by allowing a bit more wiggle room for a touch to slide out and still be considered inside the button.  However, the calculation could become incorrect, resulting in strange behavior which appeared as though the button was un-touchable.

	
  * Updates and corrects the styling of many of SproutCore's views and controls.  While creating the Showcase app, it was discovered that there were many minor problems and inconsistencies with SproutCore's default theme.  Each of these issues has been corrected.

	
  * Fixes core problems with SC.Object.reopen() and SC.Object:mixin() that resulted in any computed properties, bindings and observers included in the reopen or mixin, not have been applied to previous instances of the class.

	
  * Fixes problems with memory leaks and un-cleaned up observers on SC.SegmentedView items.

	
  * Fixes SC.Record attribute's defaultValue property.  This property failed to work when used with a key and also failed to work if the defaultValue was a function that expected the record instance to be given to it.





This release also includes many additions and corrections to the internal documentation, which has been rebuilt and posted at [http://docs.sproutcore.com](http://docs.sproutcore.com), and it includes all of the bug fixes from versions 1.8.1 and 1.8.2.   For the full list of changes, view the [CHANGELOG.md](https://github.com/sproutcore/sproutcore/blob/master/CHANGELOG.md) in the framework.

Thanks to all the many contributors that work tirelessly improving SproutCore and offering support to those in the community.
