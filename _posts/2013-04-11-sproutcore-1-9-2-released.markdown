---
author: tkeating
comments: false
date: 2013-04-11 09:08:14+00:00
layout: post
link: http://blog.sproutcore.com/sproutcore-1-9-2-released/
slug: sproutcore-1-9-2-released
title: SproutCore 1.9.2 Released
wordpress_id: 2114
tags:
- Release
---

We are pleased to announce the immediate release of **SproutCore 1.9.2**.  This release contains important fixes to the 1.9 code-base and is fully backwards compatible.  We recommend that all users of SproutCore upgrade to this latest version in order to have the best development experience.  To upgrade to the latest version, simply run:

`gem update sproutcore`

This is a patch release and contains the following bug fixes:

**Build Tools**



	
  * We've softened the build tools dependency requirements from being ultra-pessimistic (i.e. within the minor version) to being just pessimistic (i.e. within the major version).  This helps to prevent Bundler conflicts.

	
  * Fixes the snake case generator for '`sproutcore gen`', so that names like 'SCProject' get properly transformed to '`sc_project`' and not '`s_c_project`'.

	
  * Fixes the '`$repeat: repeat`' property used with the `@slice` SCSS directive when generating the @2x version.  It was incorrectly appending @2x to the end of the whole path (ex. `/resources/images/image-sliced-from.png@2x`) instead of inserting it before the extension (ex. `/resources/images/image-sliced-from@2x.png`).

	
  * Fixes incorrectly named "responder" generator to "state" generator for generating SC.State subclasses.  You can now generate an SC.State file using '`sproutcore gen state`' or '`sc-gen state`'.

	
  * Added support for un-prefixed `background-size` CSS attribute when spriting.  This allows spriting to work properly in retina Firefox.

	
  * Fixes inconsistencies and improper syntax in several templates created with '`sproutcore gen`'.  Generated files are now cleaner and provide more descriptive help comments.

	
  * Fixes missing stylesheet warnings on a clean app generated with '`sproutcore gen app`' or '`sproutcore gen statechart_app`' by adding a default stylesheet to the app. Also adds a default stylesheet to a design, when using '`sproutcore gen design`' (i.e. creating an SC.Page resource).


**Framework**



	
  * Fixes regression in IE7 and IE8 which caused XHR requests to fail to notify.

	
  * Fixes improper binary search used by` SC.ManyArray.prototype.addInverseRecord` that resulted in an infinite loop when using `addInverseRecord` with an `orderBy` function.

	
  * Fixes bug that allowed the context menu to appear regardless of overriding contextMenu in a view or setting `SC.CONTEXT_MENU_ENABLED` (globally) or `isContextMenuEnabled` (on a view) to false.  This makes the context menu event handling behave the same as the key, mouse, etc. event handling.

	
  * Fixes actions: insertNewLine, deleteForward, deleteBackward, moveLeft, moveRight, selectAll, moveUp and moveDown to be always handled by the SC.TextFieldView element when it has focus.

	
  * Fixes the hint value for SC.LabelView so that it will appear when the label has no value and isEditable is true.

	
  * No longer modifies the underlying items given to an SC.SegmentedView directly so that we don't dirty the original objects.

	
  * Fixes debug files being included in builds. These files (one of which is a 2.5MB test image) would get included into every build, because they were at the wrong path.  These files should not ever be loaded in an app, but if you created an app manifest based on the contents of the built static directory, you could invariably cause the client to download over 2.5MB of files that are never used.

	
  * Fixes determination of touch support in Chrome on Win 8.

	
  * Adds missing un-prefixed border-radius rules to the default theme for browsers that have dropped the prefix.


As always, every bug fix includes an accompanying unit test to ensure that the bug does not re-appear in the future.
