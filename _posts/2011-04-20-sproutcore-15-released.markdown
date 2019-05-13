---
author: ykatz
comments: true
date: 2011-04-20 16:46:23+00:00
layout: post
link: http://blog.sproutcore.com/sproutcore-15-released/
slug: sproutcore-15-released
title: SproutCore 1.5 Released
wordpress_id: 6
post_format:
- Aside
tags:
- Release
---

We’re excited to announce the final release of SproutCore 1.5. It’s been almost four months since 1.4.5 shipped, and we have lots of exciting new stuff for you.




# Changes




* * *

## Template View




SproutCore 1.5 offers a brand-new way to define your view layer. If you have an existing application, SC.TemplateView makes it easy to integrate Handlebars-flavored HTML into your view hierarchy. If you’re starting a brand new application, you can design your entire application using just HTML, CSS, and the power of SproutCore’s binding system.




We’ve put together a tutorial that takes you through the process of creating a new template-based SproutCore application from scratch. You’ll learn how to define a model, create a controller structure, create HTML using Handlebars, then hook all of the pieces together using bindings.




[Guide: Getting Started with HTML-Based Apps](http://guides.sproutcore.com/html_based.html)




Community member Greg Moeck created a screencast as part of his Dispatches from the Edge series that shows some of the power of these templates:




[Dispatches from the Edge: Template Views](http://blog.sproutcore.com/post/4393914581/dispatches-from-the-edge-part-1-template-views)




## Theme




If you are building a native-style application using SproutCore’s library of controls, we have a great new default theme called Ace 2.0 that looks at home on modern desktop and mobile operating systems.




We’ve also significantly improved theming flexibility for developers that desire their own look-and-feel. You can even include multiple themes in the same application.




To learn how to theme your application, read the guide by Alex Iskander:


<!-- more -->


[Guide: Theming Your App](http://guides.sproutcore.com/theming_app.html)




## SCSS and Data URIs




Under the hood, the SproutCore build tools include a new CSS parser called Chance. Chance builds on top of SCSS to provide helpers for doing things like including data URI representations of your images. By using data URIs, you can reduce the overhead of additional HTTP requests.




You also get the benefits of SCSS: variables, nested rules, mixins, selector inheritance, and more.




To learn more about SCSS, see the Sass website:




[Sass & SCSS](http://sass-lang.com/)




To learn more about the SproutCore-specific features of Chance, read the guide:




[Guide: Using Chance, SproutCore’s CSS Framework](http://guides.sproutcore.com/chance.html)




## WAI-ARIA Support




The desktop controls in 1.5 are now WAI-ARIA-enabled. WAI-ARIA defines a way to make web applications more accessible to people using assistive devices.




## Modular Loading




Your applications can now be split into modules which can be loaded automatically when the user is idle or in response to user events. This allows you to reduce the size of your initial application payload.




For example, if your application contains a preference pane, the user probably does not need the code or resources for that pane to be loaded within the first few seconds of using the application.




You can learn about how modules work by reading the modular loading specification:




[Specification: Modular Loading](http://www.sproutcore.com/specifications/modular_loading_specification.pdf)




To learn about how modular loading helped Google improve their load times, read this excellent article from the Gmail team:




[Reducing Startup Latency](http://googlecode.blogspot.com/2009/09/gmail-for-mobile-html5-series-reducing.html) (Note that unlike Google, we load your code as strings instead of block comments.)




## Experimental Features




Going forward, we are placing an even higher emphasis on quality. This means that features that we do not feel are yet production-ready, but fill an important need, will be placed into an experimental framework. If you’d like to add an experimental feature to your application, you’ll need to list it in your Buildfile.




For example, if you wanted to use the rewrite of SC.SplitView that is not yet fully documented, you would add the following line to your Buildfile:




`config :myapp, required => [:sproutcore, 'sproutcore/experimental/split_view']`




## Roadmap




In order to keep pace with the rapidly evolving world of web apps, and to ensure the development team remains focused, we will be switching to a six-week release cycle. These faster and more-focused releases will allow us to better react to the needs of the developer community.




![Roadmap](https://img.skitch.com/20110402-bkdg6ax6tcxm8t51st5bbk39tk.png)




We will have an announcement about the planned features shortly.




## Getting the Gem




To get the updated gem, type the following in your command line:




`gem install sproutcore`




If you run into any problems, please contact the [SproutCore Google Group](http://groups.google.com/group/sproutcore) or visit us in #sproutcore on irc.freenode.net.




If you find a bug, please file it on our [GitHub Issues page](http://github.com/sproutcore/sproutcore/issues).
