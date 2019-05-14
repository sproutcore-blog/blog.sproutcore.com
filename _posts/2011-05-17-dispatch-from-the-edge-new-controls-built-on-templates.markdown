---
author: gmoeck
comments: true
date: 2011-05-17 19:35:46+00:00
layout: post
link: http://blog.sproutcore.com/dispatch-from-the-edge-new-controls-built-on-templates/
slug: dispatch-from-the-edge-new-controls-built-on-templates
title: 'Dispatch From The Edge: New Controls Built on Templates'
wordpress_id: 1127
tags:
- Dispatch
---
{%raw %}
[![](/img/sprout7-300x167.jpg)](/img/sprout7.jpg)

The construction of the view layer has been greatly simplified by the new way of delegating the view's rendering to templates. With templates, most things have gotten easier to do-- particularly view rendering. However, there are a couple of benefits that the older ways of building views provide that became a bit more difficult within templates– namely, building controls. In this post, I'll take you through the ways in which Templates have affected how we construct controls, and how to build yours as efficiently as possible.

Before templates, we had several drop-in objects that handled common controls. If I wanted to add a button to a view, all I had to do was something like this:


    SC.View.extend({   
      button: SC.ButtonView.extend({     
       target: object,     
       action: 'something'   
      }) 
    })


What was nice about this approach was that you didn't have to worry about describing exactly how the button renders, or how it responds to things like mousedown or mouseup. This was convenient because generally all buttons have the same structure and code, and it let us work at a higher level of abstraction. If we were to do this inside of a new template structure, we would have to do something like the following:


    views:

    BaseView = SC.TemplateView.extend({   
            templateName: 'some_template' 
    })

    CheckAllView = SC.TemplateView.extend({   
        target: object,   
        action: 'something,   
        ...   
        mouseUp: function() {     
          ...
          this.get('target')[action]()
          ...
        }
        ...
     })

    template:
    <div class="something">
        ...   
        {{#view CheckAllView }}     

        {{/view}}   
        ...</div>


<!-- more -->
This makes it so that we're essentially re-inventing the wheel every time we want to create a button view. It would be nice if we had some standard control objects, so that we could specify how to create a simple view hierarchy in the template.

Enter the new controls build on templates. Now, for example, using the new Button controller, you could do the following:


    BaseView = SC.TemplateView.extend({
        templateName: 'some_template',
        buttonTarget: object,
        buttonAction: 'something'
     })
    <div class="something">
        ...
        {{view SC.Button targetBinding=".partentView.buttonTarget", actionBinding=".parentView.buttonAction"}}
        ...</div>


These sort of controls now exist for buttons, text fields, and checkboxes.


## So why not use the older view classes?


So why wouldn't we just use the standard SC.ButtonView? Can we not embed those in our templates?

Of course you can do that; the only tricky thing is that some of the views are built to be positioned by the layout property, whereas many applications that are now using templates are not.

Furthermore, the actual code for the controls is implemented using templates, and so they are much cleaner. Look at the render method for the textfield view:


    render: function(context, firstTime) {
          sc_super() ;
          var v, accessoryViewWidths, leftAdjustment, rightAdjustment;
         // always have at least an empty string
          v = this.get('fieldValue');
          if (SC.none(v)) v = '';
          v = String(v);

         // update layer classes always
          context.setClass('not-empty', v.length > 0);

         //addressing accessibility
          if(firstTime) { 
           context.attr('aria-multiline', this.get('isTextArea'));
           context.attr('aria-disabled', !this.get('isEnabled'));
          } 
         if(!SC.ok(this.get('value'))) {
            context.attr('aria-invalid', YES);
          }
         // If we have accessory views, we'll want to update the padding on the
         // hint to compensate for the width of the accessory view.  (It'd be nice
         // if we could add in the original padding, too, but there's no efficient
         // way to do that without first rendering the element somewhere on/off-
         // screen, and we don't want to take the performance hit.)     
         accessoryViewWidths = this._getAccessoryViewWidths() ;
         leftAdjustment  = accessoryViewWidths['left'] ;
         rightAdjustment = accessoryViewWidths['right'] ;

         if (leftAdjustment)  leftAdjustment  += 'px' ;
         if (rightAdjustment) rightAdjustment += 'px' ;

         this._renderField(context, firstTime, v, leftAdjustment, rightAdjustment) ;
          if(SC.browser.mozilla) this.invokeLast(this._applyFirefoxCursorFix);
        },


Versus the code to render the textfield in the new control:


    defaultTemplate: function() {
        var type = this.get('type');
        return SC.Handlebars.compile('
    <input type="%@" value="value"></input>'.fmt(type));
      }.property()


To me, this simplicity in and of itself is a win enough to use the new controls.

Until next time, this is Greg Moeck signing off.



* * *



**Announcements:**

We're excited to welcome not one, but ** two new Meetup groups** to the family of SproutCore groups!




  * [ Los Angeles](http://www.meetup.com/SproutCore-LA/events/18276271/) with their first Meetup Tuesday, June 7th


  * [Provo, Utah](http://www.meetup.com/SproutCore-Utah/) Their inaugural meeting is in the works– stay tuned!


There are also meetups coming up in [Chicago](http://www.meetup.com/sproutcore-chicago/): Tuesday, 5/24, with a talk by Core Team member Tom Dale; and in [San Francisco](http://www.meetup.com/SproutCore/): Tuesday, 6/14, with a talk by Core Team member Colin Campbell.

In case you haven't heard yet, there will be a SproutCore Bash on the first night of WWDC! [ Register here](http://www.sproutcorebash.com) for drink tickets and the chance to win some cool giveaways, including an iPad2!

Hope to see you around! And, as always, [let us know](mailto:community@sproutcore.com) if there's something you feel should be up here.
{% endraw %}