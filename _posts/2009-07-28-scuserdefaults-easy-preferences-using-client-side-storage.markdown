---
author: admin
comments: true
date: 2009-07-28 22:23:17+00:00
layout: post
link: http://blog.sproutcore.com/scuserdefaults-easy-preferences-using-client-side-storage/
slug: scuserdefaults-easy-preferences-using-client-side-storage
title: 'SC.UserDefaults: Easy preferences using client-side storage'
wordpress_id: 129
post_format:
- Aside
tags:
- Features
---

One of the cool things about the release of FireFox 3.5 and IE8 is that all the major web browsers now support the HTML5 standard for client-side storage using localStorage.




SproutCore was designed from the beginning to yield apps that are offline-capable.  Given the widespread availability of this localStorage now, it's time to start focusing offline mode to the framework.




About a year ago we added the SC.UserDefaults to provide easy client-side user preferences in SproutCore apps.  Now we just pushed live some fixes that make the code work on all modern browsers along with some new demo code to show you how it works.




[![](http://img.skitch.com/20090728-x1qygwe9d249jbhren8225jeyn.png)](http://demo.sproutcore.com/user_defaults)




Working with SC.UserDefaults is incredibly easy.  You just create an instance and then use get() and set() to read/write preference values; just like any other SproutCore object.  Setting properties will automatically save them to local storage.  The object is also bindings aware so you can easily bind to preferences from the other parts of your app.  In fact, this is how most of the demo application works.




In addition to simply reading/writing preferences to local storage, SC.UserDefaults also allows you to set a default appDomain and userDomain for these keys so that you can save preferences for different apps and users.  It also has a facility for you to load in a default set of preferences which will be returned if no override has been saved on the local browser.




**MORE INFO**




If you want to use SC.UserDefaults in your own app, there is a lot of info available for you now thanks to the hard work of so many team members.




  * Check out the [user_defaults demo](http://demo.sproutcore.com/user_defaults) for starters.


  * Then checkout the [demo code itself](http://github.com/sproutit/sproutcore-samples/tree/80f2a37858369348a78c04504edbb849fc519d9d/apps/user_defaults)


  * And finally, get the [reference documentation for SC.UserDefaults](http://docs.sproutcore.com/symbols/SC.UserDefaults.html)


