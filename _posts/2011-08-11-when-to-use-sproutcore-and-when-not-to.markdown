---
author: mtaby
comments: true
date: 2011-08-11 20:02:26+00:00
layout: post
link: http://blog.sproutcore.com/when-to-use-sproutcore-and-when-not-to/
slug: when-to-use-sproutcore-and-when-not-to
title: When To Use SproutCore, and When Not To
wordpress_id: 1585
tags:
- Features
---

I _could_ tell you to use SproutCore for every single web destination you build, but that would be disingenuous. SproutCore is built to address a certain class of applications that need the help of its robust binding and observer layer, as well as its ecosystem of packages (DataStore, gesture support, etc). There are other classes of applications that simply don't have the same functionality.

On a spectrum of interactivity, you have Wikipedia on one end, and iCloud.com on the other. The high level of interactivity in a suite of applications like iCloud mandates a foundation that dictates architecture and allows the developers to think and develop at a higher level of abstraction. Wikipedia, on the other hand, lacks rich interactivity or client-side data management, so it does not need state management.

The key consideration you have to make is whether or not you need state management on the client (the browser). When I refer to "state" in this context, I'm referring to a couple of types of state:




  * Server data: If you need to fetch, store, and maintain a data set delivered to you from the server, then SproutCore's bindings model and the DataStore package ensure that what the user sees and what your server knows about never get out of sync.


  * Application state: In an application's UI, multiple related pieces of information are usually displayed simultaneously: the aggregate number of items in a list, a list of the most recent items in a collection, etc. Using traditional web development techniques to maintain this sort of application state necessitates a large amount of boilerplate code writing and upkeep.


Finally, SproutCore helps manage the complexity of the code base and keeps marginal-cost of new features low over the lifetime of your project.

[caption id="attachment_1600" align="aligncenter" width="523" caption="The effort required to scale your application in terms of complexity grows at a much lower rate than a traditional, roll-your-own technique."][![](/img/app-complexity-final1.png)](/img/app-complexity-final1.png)[/caption]

This is emergent from SproutCore's binding and observer layer. Because you describe the path your data follows from the model layer to the view layer, any new feature that impacts the data in the model layer will automatically propagate through your application.

Alternatively, when using an event-driven system where you primarily respond to user action, adding a new feature requires you to review the list of current features in your application to ensure that the new addition integrates well with the others. This normally involves keeping disparate functionality in sync by hand, which can become unruly over time.

You, the application developer, write and maintain the application code. However, the community writes and maintains the framework code, allowing the benefits trickle down to you when you update the framework. As a result, by offloading the code you have to write from the application to the framework, you ensure that you build robust, interactive, and fast applications.
