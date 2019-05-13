---
author: gmoeck
comments: true
date: 2011-08-02 10:30:26+00:00
layout: post
link: http://blog.sproutcore.com/dispatch-from-the-edge-handlebars-debugging-helpers/
slug: dispatch-from-the-edge-handlebars-debugging-helpers
title: 'Dispatch From The Edge: Handlebars Debugging Helpers'
wordpress_id: 1566
tags:
- Dispatch
---
{% raw %}
[![](http://blog.sproutcore.com/wp-content/uploads/2011/08/handlebars-blog-300x167.png)](http://blog.sproutcore.com/wp-content/uploads/2011/08/handlebars-blog.png)

Greetings all! It's been a bit since our last Dispatch, and the edge waits for nobody, so quite a lot has been going on. This week I'm going to focus on a couple of helpers that have been added to aid in the debugging of view rendering with Handlebars templates.

Generally, when people start trying to debug a problem in their JavaScript, they go about it in one of two ways. Either they try and use console.log to log a value to the console, or they insert a debugger statement that essentially functions as a breakpoint that stops execution of the application at that point.

Both of these techniques have always worked fine inside of SproutCore, except inside of a Handlebars template. Since Handlebars does not allow you to execute arbitrary JavaScript code within your template, you were left trying to log or debug the view property that you were trying to display.

Enter two new Handlebars helpers: log and debugger. Now you can log a property on the template or add a debugger statement to pause execution directly into the template itself. What would this look like? Consider the following code:




      <div class="some-item">
        {{log name}}
        {{debugger}}
        {{name}}
      </div>



This would log the name property to the console, and then stop the execution, setting the current "this" property to the template. This means that you can do a this.get('name'), or any other property, on the template and it will print the value to the console window.

If you interested in how to do this sort of thing for yourself, the source file is very simple and [you can read it for yourself here](https://github.com/sproutcore/sproutcore20/blob/master/packages/sproutcore-handlebars/lib/helpers/debug.js).

Hope this helps you in debugging your busted templates. Until next time this is Greg signing off.

{% endraw %}