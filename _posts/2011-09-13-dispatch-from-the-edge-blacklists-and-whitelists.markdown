---
author: gmoeck
comments: true
date: 2011-09-13 18:40:30+00:00
layout: post
link: http://blog.sproutcore.com/dispatch-from-the-edge-blacklists-and-whitelists/
slug: dispatch-from-the-edge-blacklists-and-whitelists
title: 'Dispatch From The Edge: Blacklists and Whitelists'
wordpress_id: 1808
tags:
- Dispatch
---

The "true edge" of SproutCore nowadays is primarily the 2.0 branch, where the new and fresh is continually appearing. However that doesn't mean that the 1.x branch has been forsaken, or forgotten. The 1.7 beta release has some pretty cool features that allow you to improve the performance of your application. What I want to focus on today is how to use a blacklist or whitelist with the 1.x build tools.

One of the biggest knocks against SproutCore 1.x is that it is a "big, monolithic framework". You end up pulling in more than you're ever going to use or need. This is a problem, particularly in a JavaScript context, because it increases the size of the file that needs to be sent down from your server, and then parsed by the browser. Particularly in a mobile context, this can be a serious performance drain.

Enter the SproutCore whitelist/blacklist. If there is a section of SproutCore 1.x that you're not using inside of your application, you can use either a whitelist or a blacklist to tell the build tools not to include that code in the final packaged version of your application's JavaScript. So for example, if my application is not using collection view, I could create a file called Blacklist inside of the root of my file directory, and put the following into it to exclude collection view:

`
{
"/sproutcore/desktop": "views/collection.js"
}
`

"/sproutcore/desktop" is the "target" for the build tools, which you can think of as basically the framework to target. Then, "views/collection.js" which is the "rule" for the build tools. If the list is a whitelist, then the rule would mean to include the file in the final build, whereas if the list is a blacklist, then the rule would exclude that file. So in this case, "/sproutcore/desktop": "views/collection.js" tells the build tools to exclude the file "views/collection.js" from the desktop framework.

So if you have a 1.x app and you're looking to improve the initial load time of your app, I would create a blacklist for your application, and go file by file seeing what you can exclude from the framework. Happy optimizing.
