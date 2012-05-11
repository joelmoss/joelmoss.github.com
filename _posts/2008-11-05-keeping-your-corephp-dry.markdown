--- 
layout: post
title: Keeping your core.php DRY
categories: articles
---
Something that I have been taking advantage of in my Cake 1.2 apps for quite a while now, is the ability to separate your custom config options from your app's core.php file. And I am pretty sure that it is one of those lesser know features in 1.2.

The core.php file within your app's config directory is used to store application wide configuration variables. Things like your debug level, cache settings and sessions store are set here using Cake's very useful Configure class. This file can start to get quite large and unruly as the development of your app progresses. So one of the first things I do when I start a new app, is to separate my custom application config variable into another file within the config directory. This then keeps the core Cake configure settings separate from your custom ones, and keeps things a little dry.

Just create a new file in your app/config directory. You can name this anything you want, but I usually go with something like 'config.php' or 'app.php'. As long as it ends with '.php', it doesn't matter.

Then in your app/config/core.php file, add the following line to the top of the file:

<code>Configure::load('config');</code>

As long as you pass the name of your newly created file, then it will be fine. So the above will work if I created a file called app/config/config.php.

Then within your new config file, you can set any config variables you wish. However, you don't use the familar <code>Configure::write('name', 'value');</code> convention. The variables that you set within your custom config file should be specified using arrays. Like this:

<code>$config['name'] = 'value';</code>

All variables in this file only, should set within the <code>$config</code> array as array name/value pairs. If your custom config file is called 'app.php', then the array name would be <code>$app</code>. So effectively, you could create as many of these custom config files as you wish. Perhaps if you had distinct sections of the app. I usually just create one, so I can easily access my custom config vars, without worrying about Cake's built in config vars.

You access these custom config variables in the exact same way as you would any of the other built in core config vars.

<code>Configure::read('name');</code>

Enjoy!
