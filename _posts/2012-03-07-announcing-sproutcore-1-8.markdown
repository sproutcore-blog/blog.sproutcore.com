---
author: tkeating
comments: true
date: 2012-03-07 06:48:23+00:00
layout: post
link: http://blog.sproutcore.com/announcing-sproutcore-1-8/
slug: announcing-sproutcore-1-8
title: Announcing SproutCore 1.8!
wordpress_id: 1941
---

I'm very pleased to announce the release of SproutCore version 1.8.0.  This release includes several new features, improvements and bug fixes and is a recommended upgrade for all SproutCore developers.

To install the latest version of SproutCore, visit [http://sproutcore.com/install/](http://sproutcore.com/install/) to get an updated installer for your system or if you are using the SproutCore gem, simply run:

    
    gem update sproutcore


<!-- more -->


## Thoughts on SproutCore


But before I get into some of the technical details of 1.8, I wanted to give a brief update on the status of the project.  I want to do this, because this release is about more than the code, it's also about marking a milestone and making a statement.

The milestone is that this is the first major release of SproutCore after the project's most active backer disappeared and the statement is, is that the SproutCore community is stronger than ever!

I cannot begin to express my enthusiasm for the way that the community has pulled together to make this release happen.  When I was asked to take on more of the care and feeding of SproutCore, Charles Jolley and I introduced a number of policies that were supposed to ensure that SproutCore never fell into the same predicament again. But I don't think anyone knew how successful these changes would be until today.

Although I generally like to sit on my opinions for as long as possible, I feel that this is a time to be firm.  I say SproutCore is not only the most complete JavaScript application framework, it is, or at least is going to be, the application framework with the strongest open source community.  And this is why:

Yes, we have been through a rocky period and like any period of transition, it was accompanied by a flurry of activity and opinion on what should become the new reality.  Most of the ideas came from those that believed change should be immediate, that we could simply cast off any previous concerns and leap frog into a new future.

This is of course, a pipe dream.  If we stopped building consensus and instead chased easy opportunities, we may generate hype, but the real issues, the issues of building trust; of fostering and supporting a community of experienced SproutCore committers and developers; these real issues would be completely unaddressed.  True change doesn't take radical ideas, it simply takes hard work, endurance and keeping a clean house where good ideas can grow, and that is what I believe SproutCore 1.8 represents.

We have a core of developers that are professional enough to put aside the fun and fancy of leaping at ideas in order to knuckle down on the unglamorous and tedious work that makes a framework truly great.  Things like improving documentation, adding rigor to tests and following proper deprecation procedures.  We will bring in good ideas, but we won't sacrifice quality to do so.


## Highlights of Version 1.8.0


So please forgive my long opinionated introduction and let me point out some of the latest highlights.



	
  * A brand new exceptionally detailed three part [introduction to SproutCore](http://guides.sproutcore.com/getting_started.html).

	
  * A new reference guide on the [build tools](http://guides.sproutcore.com/build_tools.html).

	
  * Many many bug fixes. See the CHANGELOG for a complete breakdown.

	
  * The beginnings of a major clean up initiative includes several deprecations.  Look for console warnings to indicate deprecated functions and check the CHANGELOG for the full list of deprecations.

	
  * The Desktop framework has been thoroughly updated to include correct WAI-ARIA attributes for improved compatibility with assistive technologies.

	
  * Get a basic statechart structure in new projects using the --statechart switch with sproutcore init or sproutcore gen app.

	
  * Statechart States can be made to represent a route (by default SC.routes routes) and if assigned, the state will be notified any time the app's location changes to match the state's assigned route.

	
  * Addition of SC.StatechartDelegate mixin. Apply this to objects that are to represent a delegate for a SC.Statechart object. When assigned to a statechart, the statechart and its associated states will use the delegate in order to make various decisions.

	
  * Added the ability to dynamically add substates to a statechart via a state's addSubstate method.

	
  * TextFieldView has a new property, hintOnFocus, which uses a div to act in place of the regular 'placeholder' so that it remains visible while the text field has focus.

	
  * Rewrite of SC.browser, which matches more browsers correctly and replaces the potpourri of various properties with seven standard properties: device, name, version, os, osVersion, engine and engineVersion.  For possible values, see the matching constants: SC.BROWSER, SC.DEVICE, SC.OS, SC.ENGINE.

	
  * APP_IMAGE_ASSETS is a new global array that contains the list of all sprited images, this is ideal to preload images at different points.  For example, even before the app or SproutCore finishes loading.

	
  * Sprites generated using @include slice(s) are now optimized to use space in the most optimal way to reduce memory foot print generated by a lot of extra transparent space.

	
  * Added a security feature for dev environment. By default sc-server can only be used from your local machine unless you set the flag --allow-from-ips.

	
  * Made sc-server non-blocking to work with long-polling requests.

	
  * Allow longer timeouts in sc-server proxy by setting connect_timeout and inactivity timeout in the Buildfile.

	
  * See the CHANGELOG for the full list of changes.


Finally, just thanks again to everyone that has made this release possible.  No matter if it was only a small part, I truly hope you feel pride in knowing that every part was essential.



* * *



Please use the mailing list [sproutcore@googlegroups.com](mailto://sproutcore@googlegroups.com) for all comments and questions.
