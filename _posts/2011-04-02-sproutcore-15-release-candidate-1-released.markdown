---
author: TomHuda
comments: true
date: 2011-04-02 04:42:00+00:00
layout: post
link: http://blog.sproutcore.com/sproutcore-15-release-candidate-1-released/
slug: sproutcore-15-release-candidate-1-released
title: SproutCore 1.5 Release Candidate 1 Released
wordpress_id: 10
post_format:
- Aside
tags:
- Release
---
{% raw %}
We're happy to announce the release of SproutCore 1.5 RC1, which includes significant improvements to TemplateView. Those improvements include:




  * You can now use the normal Handlebars helpers (`{{with}}`, `{{if}}`, `{{unless}}`, and `{{each}}`) in your templates. If the properties they reference change, SproutCore will automatically update the DOM. For instance, if you use the `{{#if}}` helper with a true value, and the property later becomes falsy, SproutCore will automatically hide its contents.


  * If you were using the `{{#collection}}` helper for simple iteration, you can now use the regular Handlebars `{{#each}}` helper, and it will automatically update the DOM as the underlying Enumerable changes.




  * You can now use the normal Handlebars interpolation syntax (`{{name}}`), and SproutCore will automatically update the DOM when the underlying property changes; no need to use the `{{bind}}` helper anymore.




  * These new features mean that you can use an existing Handlebars template and, through the power of bindings, have it automatically update as its content changes in other parts of the application.<!-- more -->




  * Handlebars helpers can now accept hash arguments. The syntax is: `{{view id="my-view" class="my-class"}}` You can use hash arguments in several important ways:


    * The view helper now takes `id` and `class` hash arguments. SproutCore will apply those attributes to the DOM element created for the view.


    * The `{{view}}` helper also accepts a `classBinding` attribute. When the value of the `classBinding` evaluates to true, SproutCore dasherizes the last part of the property name, and inserts the class. When it evaluates to false, SproutCore removes the class. For instance, if you say `classBinding="content.isDone"`, SproutCore will insert and remove the class `'is-done'` as the underlying property changes.


    * When you are creating a tag in markup, you can specify that certain attributes are bound. For instance, you could create a bound image tag: `<img {{bindAttr src="url" alt="title"}}>`. This will keep the src and alt attributes of the `<img>` tag in sync with the url and title properties on the current context object.







  * Fixed a number of performance issues and memory leaks associated with using TemplateView and `@each` dependent keys.


We want to thank members of the SproutCore community for trying out our first version of TemplateView and providing excellent feedback. Your feedback helped nail down the thorniest problems in the new template syntax, and we think the result is pretty spectacular. Keep in mind that this release is not yet the final release of SproutCore 1.5, so please continue to provide feedback as you use the new functionality.Also, as the feature-set is pretty new, there are bound to be bugs. If you encounter a bug, please let us know right away so we can fix it!

As we approach our final release, we will prioritize bug fixes that correct regressions since the 1.4 series, as well as bug fixes for SC.TemplateView and Handlebars. If you find something amiss, please file an issue at our [GitHub Issues](https://github.com/sproutcore/sproutcore/issues) page. Bugs with unit tests always get priority!

**Release Schedule**

An addition, as of this release, we are making some changes to how SproutCore manages its release schedule.  From now on, SproutCore is moving to regular six-week release cycles - just like Chrome. This means that you can expect the SproutCore 1.6 RC in six weeks (May 15).  At each release date, we will create a stable branch where further bug fixes will be added while master will always contain new tested but possibly unstable features.  This will allow us to continue polishing the final release while moving on to new features.

To goal for adopting short release cycles is to make it easier for you to adopt new features by ensuring that the framework regularly reaches a stable state.

Here's a graphical representation of the next couple of release cycles:

![](https://img.skitch.com/20110402-bkdg6ax6tcxm8t51st5bbk39tk.png)

You can find out the big-picture features that we are working on at any point in time, as well as features planned for future releases on [our public Pivotal Tracker](http://www.pivotaltracker.com/projects/123270)[.](http://www.pivotaltracker.com/projects/123270)

{% endraw %}