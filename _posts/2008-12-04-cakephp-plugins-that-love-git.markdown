--- 
layout: post
title: CakePHP plugins that love Git
categories: articles
---
Since the announcement of the <a href="http://github.com/cakephp/debug_kit">DebugKit plugin</a>, and its source control taking place on <a href="http://github.com">Github</a>, there have been a slew of Cake users placing their code under Git control, in particular, on Github. So I thought I would give you all a run down of the great and good in Cake/Git land.

<a href="https://github.com/joelmoss/cakephp-db-migrations"><strong>DB Migrations</strong></a>

Oh come on! You didn't really think I wouldn't mention this one did ya? The easiest and best way to manage your database schema has been Gittified for a few months now. And already the new wiki has received contributions from people other than me.

<a href="http://github.com/joelmoss/cakephp-namedscope"><strong>Named Scope</strong></a>

Last one of mine - I promise! Inspired by a Ruby on Rails feature, Named Scope is actually a very powerful and useful addition to Cake. I've started to use it extensively in my Cake apps. You really should check it out. You'll wonder how you ever got by without it.

<a href="http://github.com/cakephp/debug_kit"><strong>Debug Kit</strong></a>

Probably the most popular Cake repo controlled by Git and Github, this extremely useful plugin places a small bar at the top right of your app's pages, presenting you with debugging data, such as your DB log, view variables, and params. This should be part of the core, and is the best example of how Git can really help with developing open source code, and encouraging others to contribute. It has already been forked several times.

<a href="http://github.com/rafaelbandeira3/cakephp-plugins"><strong>Rafael Bandeira's Plugins</strong></a>

<em>Rafael Bandeira</em> created a couple of model behaviors, and has made them available on Github for all to see. One in particular sticks out and impresses, and that is the <a href="http://github.com/rafaelbandeira3/cakephp-plugins/tree/master/behaviors%2Flazy_loader.php">Lazy Loader behavior</a>. This will allow you to get related model data with simple, readable and nice method calls. <a href="http://rafaelbandeira3.wordpress.com/2008/11/21/lazy-loader-behavior-what-you-need-when-you-need-the-way-you-want/">His blog</a> explains more.

<a href="http://github.com/klevo/wildflower"><strong>Wildflower</strong></a>

Wildflower is a very promising "Content management system and application platform built on the CakePHP framework and jQuery Javascript library". I actually discovered this after a tip from Nate. If handled well, this could mean good things for Cake.

<a href="http://github.com/markstory/story-scribbles/tree/master/cakephp"><strong>Story Scribbles</strong></a>

Cake's very own <em>Mark Story</em> now has a Github repo full of lovely little Cake 'scribbles'. Enjoy things such as his ACL based Menu component, web service behavior and his Geshi helper.

<a href="http://github.com/felixge/debuggable-scraps/tree/master/cakephp"><strong>Felix's Scraps</strong></a>

Another bunch of Cake bits and bobs, but this time from <em>Felix Geisendorfer</em>, he of <a href="http://debuggable.com/">Debuggable</a> fame. What interests me the most is his collection of datasources, allowing you to connect your Cake apps to external services such as Akismet, Amazon and Google.

These are just what I feel are the pick of the crop, but there is <a href="http://github.com/search?q=cakephp">a lot more</a> than I originally thought on Github, including an <a href="http://github.com/georgious/cakephp-yaml-migrations-and-fixtures">alternative migrations shell</a>, that doesn't rely on Pear, and that just might spur me on to get rid of my reliance on the MDB2 library.

The Cake community seems to be loving Git right now. I only wish the powers that be will make that decision to switch.
