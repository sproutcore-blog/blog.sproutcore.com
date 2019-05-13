---
author: admin
comments: true
date: 2010-09-22 09:00:00+00:00
layout: post
link: http://blog.sproutcore.com/quilmes-enters-master/
slug: quilmes-enters-master
title: Quilmes Enters Master
wordpress_id: 32
post_format:
- Aside
tags:
- News
---

Late last night we merged the quilmes branch back into master. The merge includes all changes from quilmes, along with the fixes from master. This means that we now only have two major branches: master, new home of the quilmes code, heading towards 1.5 and 1-4-stable for the 1.4 code.




1-4-stable is a bug fix only branch. Any new features should go into master. If you do have a bug fix for 1-4-stable, please check to see if it also applies to master and vice-versa.




Also, a reminder for those of you who missed it. The git repo has now moved to the **sproutcore** acccount at [github.com/sproutcore](http://github.com/sproutcore). If you have not done so, please update the remote on any cloned repos you have as follows:



    
    <code>git remote rm origin
    git remote add origin git://github.com/sproutcore/sproutcore.git</code>




If you have SproutCore as a submodule, open your .gitmodules file and update the references there as well.
