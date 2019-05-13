---
author: fairbanksg
comments: false
date: 2014-04-26 13:28:08+00:00
layout: post
link: http://blog.sproutcore.com/phantomjs/
slug: phantomjs
title: Automating SproutCore Unit Testing with PhantomJS
wordpress_id: 2232
---

One of the new features in SproutCore v1.10.0 was a PhantomJS unit test runner. It allowed us to automate SproutCore's own framework unit tests, giving us awesome continuous integration support right in GitHub via the great [Travis-CI](https://travis-ci.org/) service.

If you use CoreTest, SproutCore's built-in (QUnit-like) unit test framework, then you can also use this to run your own tests from the command line – meaning you can automate it, and hook it up to your own CI scaffolding. It's impossible to overstate the impact that continuous, automatic unit testing has on the quality and stability of your codebase.



# Prerequistites


You will need to have PhantomJS installed before using the test runner. Full instructions for this can be found [here](http://phantomjs.org/download.html).

If you are using SproutCore 1.10.1 or later, you can use the new **sc-phantom** command. This will handle invoking the test runner, passing through any arguments to PhantomJS.

**If you are using 1.10.0** or are not using the gem, you will need to track down SproutCore's installed location in order to run its test runner script. If you've got a copy checked out into your project's frameworks directory, great! Just use that. If you're using the gem, you'll have to track it down yourself. It's usually somewhere like `~/.rvm/gems/ruby-1.9.3-p374/gems/sproutcore-1.10.0` – if you're unable to track it down, run `gem env` and look under the GEM PATHS heading for a hint.



# Running the tests



First, start sc-server as you normally would. Once that is running, we can start the test runner. (If you are running SproutCore v1.10.0, replace `sc-phantom` with `phantomjs $SC_PATH/lib/frameworks/sproutcore/phantomjs/test_runner.js` in the following examples. See $SC_PATH note above for details.)

`sc-phantom`

By default, this will run all the unit tests that abbot knows about, including the tests in SproutCore itself. This is probably not what you want, so you can use the `--include-targets` flag to tell the test runner what tests you want to run.

For example, if your app is called todos, running

`sc-phantom --include-targets=/todos`

will run only the unit tests in your app. If you also have a framework you want to test, you can make the argument to --include-targets a comma-delimited list of targets:

`sc-phantom --include-targets=/todos,/my_framework`

There are a few other options available for excluding certains tests and only running certain types of tests (app, framework, etc). For the full list, run:

`sc-phantom --help`
