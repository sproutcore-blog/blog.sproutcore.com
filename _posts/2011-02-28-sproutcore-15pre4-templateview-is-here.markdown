---
author: TomHuda
comments: true
date: 2011-02-28 20:14:17+00:00
layout: post
link: http://blog.sproutcore.com/sproutcore-15pre4-templateview-is-here/
slug: sproutcore-15pre4-templateview-is-here
title: SproutCore 1.5.pre.4 - TemplateView is Here
wordpress_id: 13
post_format:
- Aside
tags:
- Release
---
{% raw %}
Today we released the fourth pre-release of SproutCore 1.5, moving us a step closer to a final release next month. This version has a bunch of new features, including the initial release of TemplateView, which makes it easier to build SproutCore applications in a more conventional HTML style.




You can get the prerelease gem by typing:




    <code>gem install sproutcore --pre
    </code>




Here are some of the improvements:




## SC.TemplateView




Template views can form the basis of an entire application, or can integrate seamlessly with an existing SproutCore view hierarchy. This release incorporates support for the [Handlebars](http://handlebars.strobeapp.com/) template engine in both SproutCore itself and the SproutCore build tools.




Templates are HTML files with special tags included that can reference properties on your view or other objects.  These properties can be setup as bindings so the HTML will automatically update whenever the properties change.




In general you define templates in your `resources/templates` directory and then use SC.TemplateView to render them.  Working with SC.TemplateView is just like any other view except you specify a `templateName` property instead of a `render` method. For instance, if you had a template at `resources/templates/post_item.handlebars`, you could use it in your app with something like:




    MyApp.PostItemView = SC.TemplateView.extend({
      templateName: 'post_item'
    });



<!-- more -->


## View Mixins




SproutCore 1.5 also comes with two new mixins for use with SC.TemplateView: `SC.TextFieldSupport` and `SC.CheckboxSupport`.  You can apply these mixins to any view whose HTML includes the relevant HTML element:




    MyApp.CreatePostView = SC.TemplateView.extend(SC.TextFieldSupport, {
      insertNewline: function() {
        // instead of directly observing the keyUp event and filtering
        // by keycode, you can use a higher level event
      }
    });

    MyApp.StarPostView = SC.TemplateView.extend(SC.CheckboxSupport, {
      // bind the value of the checkbox to a controller
      valueBinding: 'MyApp.postController.isStarred',

      valueDidChange: function() {
        // observe a change to a SproutCore property, rather than
        // observing the DOM directly
      }.observes('value')
    });





In general these mixins are intended for use with TemplateView-driven apps that do not require the full richness of the built-in `SC.TextFieldView` and `SC.CheckboxView`.




## Handlebars and Helpers




This release includes a new template rendering engine called Handlebars.  Handlebars is based on the popular Mustache template engine, but is much faster and capable of supporting plugins (which is what we use to support bindings).




We’ve added several helpers to Handlebars to allow you to assign views to your HTML and have it update when properties change.




You can use the `view` block helper to assign HTML to a SproutCore view class, and the `bind` helper to tell SproutCore to print the value of a property (and update it when it changes). For example:




    <code>{{#view "MyApp.PostView"}}
        <h1>{{bind "title"}}</h1>
    {{/view}}
    </code>




The `bind` helper works in block form too:




    <code>{{#bind "content"}}
        <h1>{{title}}</h1>
        <div>{{{body}}}</div>
    {{/bind}}
    </code>




Whenever the underlying property changes, SproutCore will replace the contents of the block by re-rendering it with the new value of the property.  This can eliminate a lot of glue code for views.




You can also use the `collection` helper to display a template for each item in an enumerable:




    <code>{{#collection "MyApp.MyTemplateCollectionView"}}
        <b>{{bind "content.title"}}</b>
    {{/collection}}
    </code>




Then, just bind the `content` property of the collection to an enumerable:




    <code>MyApp.MyTemplateCollectionView =
      SC.TemplateCollectionView.extend({
        contentBinding: 'MyApp.myArrayController'
      });
    </code>




## Experimental Framework




As of SproutCore 1.5, we will include new, in-progress features as part of the `experimental` framework. It will not be included by default, and you can add any experimental features to your `Buildfile`:




The purpose of this change is to make it easier for us to include new features from the community.




    <code>config :all, :required => [:sproutcore,
                "sproutcore/experimental/device_motion"]
    </code>




## Core Foundation




In order to make it easier to use a smaller subset of SproutCore in constrained environments, this release also includes a new `core_foundation` framework that contains a basic SproutCore environment, with no extras. You can use it by specifying it in your `Buildfile`:




    <code>config :all, :required => "sproutcore/core_foundation"

    # if you want to include other frameworks normally included by :sproutcore

    config :all, :required => ["sproutcore/core_foundation", "sproutcore/datastore"]
    </code>




You can also use `SC.CoreView` rather than `SC.View`, which is a significantly stripped down version of a SproutCore view. However, it is missing quite a few features you probably expect (like layout), so it probably makes sense to wait until the release candidates of SproutCore 1.5, when we’ll have much better appropriate usage information.




## Other Improvements




SC.ImageView will use a `<canvas>` tag on platforms that support it, which improves performance significantly.




SC.SegmentedView now creates an overflow menu if there are too many segments to display. Class names for SC.SegmentedView have been cleaned up. You may need to update your CSS if you were theming SC.SegmentedView.




You can now observe the contents of enumerables using the special `@each` key.




    <code>SC.postsController = SC.ArrayController.create({
        isDoneDidChange: function() {
            // this observer is triggered when:
            // * an element is added
            // * an element is removed
            // * any child element's `isDone` property changes
        }.observes('.@each.isDone')
    });
    </code>




Dependent keys can accept property paths. For example, you can say .property(‘foo.bar’), and it will be invalidated if the `bar` property of `foo` changes. This works with the new `@each` property as well.




We deprecated SC.viewportOffset(). Please use SC.offset() instead, which is more explicit about what it returns and has more features.




SC.browser now detects Android devices.




SC.device.orientation now works reliably on desktop, iOS, and Android 2.1 and above.




The experimental framework includes support for gyroscope information, if provided by the browser. This is in the `sproutcore/experimental/device_motion` framework.
{% endraw %}