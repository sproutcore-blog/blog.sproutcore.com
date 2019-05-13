---
author: gmoeck
comments: true
date: 2011-06-14 22:22:05+00:00
layout: post
link: http://blog.sproutcore.com/dispatches-from-the-edge-handlebars-without-spans/
slug: dispatches-from-the-edge-handlebars-without-spans
title: 'Dispatches From The Edge: Handlebars Without Spans'
wordpress_id: 1332
tags:
- Dispatch
---
{% raw %}
[![](http://blog.sproutcore.com/wp-content/uploads/2011/06/handlebars-1-300x167.png)](http://blog.sproutcore.com/wp-content/uploads/2011/06/handlebars-1.png)
As more people have been using templates to map the state of their views into the DOM, a couple of questions have continually come up. In this week's Dispatch, I want to focus on how SC.TextField solves one of the common questions and offer some advice on building similar custom views.

Let's first specify the common question: How would one go about implementing something like a textarea tag? Just about everyone tries to do it like this:



    <textarea>{{content}}</textarea>



You would like it to render something like this:



    <textarea>Some Content</textarea>



But instead, SproutCore outputs something that looks like the following:



    <textarea><span>Some Content</span></textarea>



Why would SproutCore wrap your content inside of the span tag? Because the Handlebars template isn't only responsible for the initial rendering, it's also keeping that rendered content in sync with the state of your view. Because of this, it needs to be able to target an element inside of the DOM to replace when the state of your view changes. So SproutCore inserts that span tag into the rendered DOM so that it can later change the DOM when content changes.
<!-- more -->
So, then, how would we implement a textarea sort of view? Although you might not have known it, SproutCore 1.6 actually allows you to use a textarea instead of a text input within SC.TextField by changing the isMultiLine parameter.

A template using this might look something like this:



    {{view SC.TextField isMultiLine="true" valueBinding="MyApp.someController.someValue"}}




Which would then output something like this:



    <textarea>Some Content</textarea>



How did the core team create a view that does that? Since we don't really have a way to handle this updating baked into the SproutCore extensions to Handlebars, we bypass the delegating to the template for the value of the text area, and handle that updating directly in our view. So if you were to build a custom TextArea view, it might look something like this:




    SC.TextArea = SC.TemplateView.extend({
      value: '',
      template: SC.Handlebars.compile('<textarea></textarea>'),

      $input: function() {
        return this.$('textarea');
      },

      didCreateLayer: function() {
        this.$input().val(this.get('value'));
        SC.Event.add(this.$input(), 'keyup', this, this.domValueDidChange);
      },

      domValueDidChange: function() {
        var input = this.$input();
        if(input.val() !== this.get('value'))
          this.set('value', input.val());
      },

      viewValueDidChange: function() {
        var input = this.$input();
        if(this.get('value') !== input.val())
          input.val(this.get('value'));
      }.observes('value')
    })




What is this code doing?

First, we're specifying the basic render with the template method to be just a basic textarea tag without any handlebars tags. This way, when initially rendering the view it just renders a blank text area, and doesn't insert the span tag that we saw earlier.

Second, we implement a didCreateLayer function which is called after the view is initially rendered.  Within that, we set the initial value of the textarea DOM to be the value of our view. Then we register the input tag to call into an API called domValueDidChange when a keyup event is fired upon the textarea element. We need this so that we can manually keep our view state in sync when changes happen to the state in the DOM.

Third, in order to keep our view state in sync with the DOM, we need to actually implement the domValueDidChange function. In order to ensure we don't enter an infinite loop, we double check that we don't set the value if it is already identical to the value in the DOM. And if it is not identical, we update the value of our view with the current value of the textfield. Then we also need to implement a function that will update the DOM when the value of the view changes. This is what the viewValueDidChange function is. It observes the value of the view object and when it changes if the textarea is not in sync, it syncs it.

The basic idea behind the whole view is that instead of delegating to the template to keep the view in sync, we manually do that with observers in the DOM.

If you want to see how we do this directly, you should read the actual source for textfield view in both [1.6](https://github.com/sproutcore/sproutcore/blob/master/frameworks/core_foundation/mixins/template_helpers/text_field_support.js) and [2.0](https://github.com/sproutcore/sproutcore20/blob/master/packages/sproutcore-handlebars/lib/controls/text_field.js). And remember- however the core team builds views, you can too if you just look at the source and learn how it's being done.



* * *



**Announcements:**

We're excited to welcome our first Meetup group in Asia, [SproutCore Kuala Lumpur](http://www.meetup.com/sproutcorekl/), to the family of SproutCore meetup groups! More international meetups are in the pipeline, so keep your eyes peeled for announcements in the next few weeks!

There is also the [San Francisco meetup tonight](http://bit.ly/lq7WsY). If you can't make it, watch for video posted here on the blog.

Hope to see you around! And, as always, [let us know](mailto:community@sproutcore.com) if there's something you feel should be up here.
{% endraw %}