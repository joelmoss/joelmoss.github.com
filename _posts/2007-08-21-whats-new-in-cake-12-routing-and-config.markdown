--- 
layout: post
title: "Whats new in Cake 1.2: Routing and Config"
categories: articles
---
Haven't done one of these in a while, probably because there haven't been many feature changes in the 1.2 branch. But the last month or so have seen a few small feature changes that I think could be very useful.

<h4>No more global constants</h4>

The first of these changes is the transitioning of the configuration away from global constants. I am sure you are fully aware of the plethora of constants within the core.php file. Well, the final release of 1.2 will see these replaced with singleton calls to the Configure class.

So instead of

<pre><code>define('DEBUG', 2);</code></pre>

you get...

<pre><code>Configure::write('debug', 2);</code></pre>

Good move, as any sort of globals can cause issues.

<h4>RESTful Routes</h4>

Now this is one feature that I really loved when I played with Ruby on Rails. I really got to love the simplicity and the 'that makes sense' mentality of RESTful routes. If you have no idea what I am on about, I highly recommend that you take a little time to watch and listen to <a href="http://www.scribemedia.org/2006/07/09/dhh/">DHH's keynote presentation</a> at last years RailsConf.

Anyway, at the end of July, I noticed <a href="https://trac.cakephp.org/changeset/5454">changeset 5454</a>, which made changes to the Router. More importantly it added support for RESTful routes, which take advantage of the hidden beauty of the HTTP GET, POST, PUT and DELETE verbs.

I have yet to play with this fully, so not 100% sure of how it works, but I would like to thank the core team for including it. And I hope to write more about it in a future article.

<h4>Prefixed Routing</h4>

A recent changeset also introduced prefix based routing. Which lets you specify a prefix in any route, which is then prepended to the action called.

For example, with the prefix variable set to admin in your route, you could access the following URL:

<pre><code>/admin/posts/create</code></pre>

which would then call the admin_create action within the posts controller.

So we still have some new things to look forward to in 1.2. In fact I am beginning to think that CakePHP 1.2 would be best referred to as CakePHP 2.0.

Enjoy!
