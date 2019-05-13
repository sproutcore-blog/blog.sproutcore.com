---
author: pbergstr
comments: true
date: 2011-09-01 20:44:18+00:00
layout: post
link: http://blog.sproutcore.com/localization-in-sproutcore-1-6/
slug: localization-in-sproutcore-1-6
title: Localization in SproutCore 1.6
wordpress_id: 1750
tags:
- Localization
---
{% raw %}
## Why Should I Care About Localization and Internationalization?


When developing applications, localization and internationalization are things that are easily overlooked and forgotten until the very end. In the case of smaller applications, they are targeted to only one language, and not having to account for localization or internationalization might work out in the end.

However, especially for larger applications or applications that are targeted to several international markets, planning and implementing an application with localization and internationalization is extremely important. Without proper planning, you can get into a lot of trouble that could have been alleviated with very little upfront effort. The type of planning you'll need to do is what we'll go over in this in this post.


## Factor in localization early in your development cycle!


As a developer, you should plan for localization and internationalization early in your development cycle, when it is easy to deal with. Once an application grows too large, it is very difficult to add localizable strings.

If you develop without taking into account localization, often text winds up hard coded and, as with any application, these strings are found in a million different places. Having to track down all the non-localized strings after the fact is time consuming and unnecessary if accounted for earlier in the project.



## Localizing Your Apps with SproutCore


SproutCore makes it easy to localize your application. Using a strings table for each language, developers can enter key-value pairs. These keys are generic and are referenced throughout the application.

When the application runs, instead of using the actual string in the view, SproutCore looks up the correct localized value from the strings table. This makes it easy not only to localize the application, but also to manage all of the strings in your application because they are all located in one place. If you need to finalize the strings, you can send that off to be finalized without having the stakeholders know any JavaScript.
<!-- more -->
However, there are more things to localize than just strings. For each language or locale, you can have a sub-directory that contains not only your strings file, but also other resources such as images, CSS, and HTML templates. We'll go into more detail how to properly set up your application for localization in the next section.



## Set Up Your Application for Localization


Now that you're thinking about localization, how do you go about setting up an application to be localized? There are some things that will need to be expanded upon from the normal directory structure that you are familiar with.



### The directory structure


The first thing to go over is the general structure of a SproutCore application as it is normally presented when you create a basic app. Below is the directory structure for an application, MyApp, that contains an image, `myapp_logo.png` inside of the `resources` directory that contains some English text, and the normal `en` directory with CSS and a strings file. Most of time the, the strings file will be empty because the developer hasn't considered localization.



    apps/
       myapp/
          core.js
          en/
             strings.js
             myapp.css
          main.js
          resources/
             images/
                myapp_logo.png



However, this is not very localizable. Let's say that we also want the application to be available in German. In this case, we'll have to readjust the directory structure a bit.

First, the image in the case has some text that needs to be in German. Second, there is some CSS layout that needs to be readjusted for the really long German words. Third, and most important, there are a lot of strings that need to be translated, so we need to create a strings file.




    apps/
       myapp/
          core.js
          en/
             strings.js
             myapp.css
             images/
                myapp_logo.png
          de/
             strings.js
             myapp.css
             images/
                myapp_logo.png
          main.js



In this structure, when you run the application in English, only the contents of the "en" directory will be loaded and vice versa for German. Therefore, you can optimize the code loaded for the specific language.



### About Those Language Codes


The language codes that are used in a SproutCore application are standard internationally recognized language codes in the format: 'language_REGION or just 'language'. For instance, if you want to localize your application into British English and American English, you would have two localizable directories: `en_US` and `en_UK`.



### The `strings.js` File


At the heart of the localization system that SproutCore provides is the strings file. Each language has its own file in its respective language directory. It is important to note that only the strings file in the language that you're running will be loaded for any given language when the application runs.

Basically, the string file is a lookup table for a string key, which you reference in your application code, and a string value, which is the corresponding localized string for the key.

The strings file has a specific format that you will need to follow:


    SC.StringsFor('en_US', {
    	'key': 'value'
    });





## Localizing Your Application


Now that you have everything set up, you can write your localizable application. Whenever you create a view element using either a `SC.View` or a `SC.TemplateView`, it is likely that you will need some text to go with it.

Instead of putting in some hardcoded text, even if it is temporary, you should create a key and add that to your view element and a corresponding value in your strings file, regardless if it is final or not.



### What is the Best Practice to Create a String Key-Value Pair?


There isn't a hard and fast rule on how to create a string key, but as long as you come up with a consistent formula, it will work out in the end. One way to do it is to refer to the path of the view inside your application.

For example, if you have a list view in the application that has items with a title, you could name the string key something like `MyApp.List.Item.Title`. While this seems verbose, any developer who looks at your view will know what the key stands in for.

Another tip is that if a string is not finalized, you should make it stand out clearly in the UI until it is finalized. One way to do so is to precede it with an underscore: `_MyApp is a great way search for beanie babies`. Once that string is approved by the stakeholders, you can easily remove the underscore.



### Localization in `SC.Views`


Several of the built-in SproutCore `SC.Views` have support for localization. for example, you can pass in localization string key into a `SC.LabelView`:




    MyApp.TitleLabel = SC.LabelView.extend({
    	localize: YES,
    	value: "MyApp.TitleLabel"
    });





## Using the .loc() Function for Computed Strings


To understand how to do more complex localizations with passed-in properties, it is important to know how the .loc() function operates. In many cases it is run for you by SproutCore, but there are cases where you want to do something more dynamic.

The .loc() function takes optional parameters like the .fmt() function. For example, let's say that you have a computed property on a customized SC.TemplateView that represents a list item. You want this list item to be more dynamic, showing a localized string with some parameters; note that the order of the parameters may be different in different languages.

The  key-value pair is the following: "MyApp.List.Item.Title": "%@1 employees working for %@2"

**list_item.js** view:



    	MyApp.ListItem = SC.TemplateView.extend({
    		templateName: 'list_item',
    		localizedTitle: function() {
    			var content = this.get('content'), ret = '';
    			if(content) {
    				ret = "MyApp.List.Item.Title".loc(content.get('employeeCount'), content.get('managerName'));
    			}
    			return ret;
    		}.property('*content.employeeCount', '*content.managerName').cacheable()
    	});



**list_item.handlebars** template:



    {{localizedTitle}}



Now, the computed 'localizedTitle' property will be used inside of the template and properly format for any language.



## Localizing Simple Values in Templates


In SC.TemplateView templates, there is a handlebars helper that allows you to easily localize strings without having to use a computed property. Computed properties only need to be be used if there are complex properties. In the case of a simple static string, you can use the 'loc' helper in the handlebars template directly.



    {{loc "MyApp.Path.To.Loc.String"}}






## Conclusion


SproutCore provides a powerful way to localize your application into as many languages as you need. The main takeaway from this post should be that if your application might support multiple languages, plan ahead and do the right thing early on. If you don't, it will be difficult to retrofit your existing application to support localization.
{% endraw %}