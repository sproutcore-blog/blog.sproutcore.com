---
author: pwagenet
comments: true
date: 2011-08-30 19:33:52+00:00
layout: post
link: http://blog.sproutcore.com/sproutcore-1-7-beta-released/
slug: sproutcore-1-7-beta-released
title: SproutCore 1.7 Beta Released
wordpress_id: 1792
tags:
- Release
---

I'm pleased to announce that SproutCore 1.7 beta is now available. This release is largely a bug fix release and the addition of some minor features so if you're using 1.6 and like the cutting edge you should check it out. Installers are available for [Mac](http://installers.sproutcore.com/SproutCore-Beta.pkg) and [Windows](http://installers.sproutcore.com/SproutCore-Beta.exe). If you're using RubyGems, just run `gem install sproutcore --pre`. A word of warning, however: if you're using the installers the beta will overwrite any previously installed versions of SproutCore. As always, share any issues you encounter on [Github Issues](https://github.com/sproutcore/sproutcore/issues).

Read on for more information on the changes.<!-- more -->

In the framework itself changes include:



	
  * Safari Lion browser detection.

	
  * Speed improvements

	
  * Flag to stop PickerPane repositioning when resizing the window

	
  * Option to enable or disable overflow in SegmentedView

	
  * Support for autoCorrect and autoCapitalize in TextFields

	
  * Minor improvements in SC.Statechart

	
  * New SC globals to provide information like build mode, build number and locale.

	
  * Lots of bug fixes


New features in the build tools include:

	
  * When a stylesheet hits the 4096 CSS selectors limit in IE , the files will now be automatically split.

	
  * Sprites are optimized to use less space

	
  * Layout.js, which includes location metrics, will be always first when building the js files

	
  * Added security feature for dev environment. By default sc-server can only be used from your local machine unless you set a flag.


Along with the following bug fixes:

	
  * Sprites are again the default for abbot due to performance issues with data-uris in some browsers

	
  * index.html will be minified again

	
  * Whitelist and black list fixes

	
  * Fixed iOS retina display styling




For a full list of all changes see the Changelogs: [Framework](https://github.com/sproutcore/sproutcore/blob/master/CHANGELOG.md) and [Build Tools](https://github.com/sproutcore/abbot/blob/master/CHANGELOG).
