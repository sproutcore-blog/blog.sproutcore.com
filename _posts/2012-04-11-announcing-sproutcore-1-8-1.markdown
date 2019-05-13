---
author: admin
comments: false
date: 2012-04-11 03:01:27+00:00
layout: post
link: http://blog.sproutcore.com/announcing-sproutcore-1-8-1/
slug: announcing-sproutcore-1-8-1
title: Announcing SproutCore 1.8.1!
wordpress_id: 1997
---

We're pleased to announce the release of SproutCore 1.8.1.  To upgrade to the latest version, simply run:

    
    gem update sproutcore




If you installed SproutCore using the installer, please note that due to the strain that maintaining the installers puts on the release process, we will not be updating the installer for each patch level release.   Therefore, to get the very latest stable version, it is recommended that you install the SproutCore gem.




Installing the gem is actually quite easy and there are detailed instructions for each platform at [http://sproutcore.com/install/](http://sproutcore.com/install/).  Simply find your platform and go to the Advanced Install tab, which helps you get Ruby properly installed.  If you’ve already got Ruby 1.9 installed, it is as simple as `gem install sproutcore.`


<!-- more -->
This is a patch level release and contains the following bug fixes:

    
    * Documentation fixes.
    * Fixes the timeout proxy settings: :inactivity_timeout & :connect_timeout. Setting them in a Buildfile proxy statement allows the developer to extend the timeout for the connection to be setup and for activity to occur.
    * Adds missing CSS for SC.PickerPane left and right pointer.
    * Tidies up index.rhtml template:
      - removes self-closing HTML
      - renames app.manifest to manifest.appcache
    * Fixes the styling of ModalPane backdrop for SC.PanelPane.
    * Fixes regression with Firefox specific SC.TextFieldView CSS.
    * Improves use and compatibility of SC.TextFieldView:
      - applies 'autocapitalize' and 'autocorrect' attributes to all browsers
      - automatically centers hint text
      - fixes problem centering input elements in IE8
      - fixes problem positioning hint in textareas
      - improves readability of hints by making them antialiased in Webkit
    * Fixes issue when subsequent attempts to load a failed/aborted image will result in queue processing being stalled.
    * Fixes nesting SC.ScrollViews not passing mousewheel events from child to parent scroll view when child can no longer scroll.
    * Fixes styling problem with SC.ListItemView right-icon.
    * Fixes SC.StaticContentView not removing previous content when setting content to null.
    * Fixes Safari focus ring artifacts in panes and Chrome bug with non-HW accelerated animations in render layers, by removing the default .sc-pane --webkit-transform: translate3d(0,0,0) CSS. This also makes it possible to accurately manage which parts of the page should become layers, because making everything a layer is not optimal.


To view the individual changes, check out the [1-8-stable](https://github.com/sproutcore/sproutcore/tree/1-8-stable) branch on github.
