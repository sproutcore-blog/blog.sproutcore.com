---
author: tdale
comments: true
date: 2011-10-03 06:20:35+00:00
layout: post
link: http://blog.sproutcore.com/why-handlebars/
slug: why-handlebars
title: Why Handlebars?
wordpress_id: 1872
tags:
- Handlebars
---
{% raw %}
**UPDATE**:



<blockquote>**The following post refers to SproutCore 2.0, which has split off as a separate project.  However, the information within this post is entirely applicable with respect to using SC.TemplateView and Handlebars in SproutCore 1.8.  If you wish to use SC.TemplateView in SproutCore, you only need be aware that the many views and controls in the Desktop framework may contain templates, but should not themselves be contained within templates.**</blockquote>





* * *



When people check out SproutCore 2.0 for the first time, one question that they frequently ask is: Do I have to use Handlebars?

[Handlebars](http://www.handlebarsjs.com/), if you're not familiar with it, is a semantic templating language written entirely in JavaScript. It's an expressive language with a tag syntax reminiscent of HTML, except expressions (oftentimes referred to as "mustaches") are wrapped in double-curly braces. A simple template might look like this:



    <div class="entry">
      <h1>{{title}}</h1>
      <div class="body">
        {{body}}
      </div>
    </div>



Handlebars, unlike other templating solutions like Eco, doesn't tempt you to embed domain logic in your HTML. Anything other than simple conditionals and loops must be contained in your application's JavaScript, which enforces the separation of concerns and leads to better testability. The language is also extensible with custom helpers, which allows you to effectively write a template DSL for your particular application.

So, while the answer to the question is_ use whatever templating system you'd like,_ we think Handlebars is a great option. Perhaps most importantly, we've spent a lot of time deeply integrating SproutCore and Handlebars, such that you get a lot for free just by using bindings, computed properties, and the SproutCore object system. In fact, while we like the features and simple-yet-expressive syntax of Handlebars, the real reason we chose it when creating SproutCore 2.0 was because of its speed and architecture, allowing us the kind of integration that would be very difficult with other templating libraries.
<!-- more -->
Handlebars compiles a given template only once. After that, it generates a JavaScript function that can be executed repeatedly without the expense of re-parsing the template. For example, a template like this:




    {{#if arrived}}
    	Hello,
    {{else}}
    	Goodbye,
    {{/if}}
    {{name}}!




might be translated into a function like this:




    function() {
      var arrived = this.arrived,
          name = this.name,
          result = '';

      if (arrived) {
        result += "Hello, ";
      } else {
        result += "Goodbye, ";
      }

      result += name+"!";

      return result;
    }




(Please note that the generated code looks different; this is just illustrative of the effect.)

Because you declare your intent, Handlebars knows how to generate the JavaScript that gets executed at runtime. If your templates don't change, you can precompile the templates into JavaScript during the build process for additional speed and file size improvements. It also means that, as Handlebars is optimized, so is your application.

But most importantly, because of its declarative nature, we can make your templates bindings-aware. Here's where the real advantage appears: **you never have to write code that updates the DOM.** Most other frameworks require you to have two separate code paths: one that creates the initial representation (often via a templating solution), and one to update it, usually with something like:




    $('#welcome').text("Goodbye, "+this.name);




With SproutCore and Handlebars, both behaviors are contained in the same template.

But beyond simple values, we also support things like conditionals and loops. If you use the `{{#each}}` helper to print an array, for example, the DOM will update _automatically_ whenever items are added, removed, or modified. This eliminates lots of boilerplate and common bugs from your application, and it means you don't need to anticipate all of the places data may change and manually re-render. Just modify the array (or the contents of the array) and let Handlebars take care of the rest.

So, while we encourage you to use whatever templating system makes most sense to you, we think that using the built-in Handlebars integration will let you write less code--and have fewer bugs--by eliminating the tedious boilerplate that you're used to writing.

You can expect many improvements to these auto-updating templates as time goes on. In particular, we are focused on ensuring they work flawlessly with elements, such as `<tr>`, that have strict requirements about their enclosing tag. Yehuda and I have been working on [metamorph.js](https://github.com/tomhuda/metamorph.js), which we are in the process of integrating into SproutCore 2.0, that will both improve compatibility with these kinds of elements, as well as offer performance improvements. Look for these commits to SproutCore soon!

{% endraw %}