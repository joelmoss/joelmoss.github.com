--- 
layout: post
title: Closer to greatness!
categories: articles
---
If you keep an eye on the <a href="http://trac.cakephp.org">CakePHP trac</a> or the <a href="http://bakery.cakephp.org">Bakery</a>, you should have noticed that PHPNut and friends have just pushed out the latest alpha release of CakePHP 1.2.

Version 1.2.0.5137alpha introduces an all new caching system that supports multiple cache backends, including apc, memcache, xcache, file, and models. I have yet to explore this, but I intend to when I get a need for it.

Another major change/addition, is the old scripts system. This is now known as Cake's console shells and is a step in the right direction. It is now even easier to create console scripts (sorry; shells) when working with your app in Cake. I have already refactored my various tasks to work with this new system. So watch out for a new version of Cake Migrations and Fixtures.

A couple of other changes include a translation behaviour and improvements to the Security component. And according to PHPNut, this should be the last alpha release before beta is reached:

<blockquote>We have some more changes before we can release the Beta. The most major change will be the transition from defines in core.php to the $config array used by the Configure class. This will be the last release that allows for defines inside of core.php. Moving away from defines provides much greater flexibility. The next release will also see the inclusion of a Session model, which will allow easier access to the database session handling.</blockquote>

So as you may recognise, I have decided to leave Rails alone for a while and concentrate on developing with CakePHP, and perhaps helping out a bit in the community. I also have a few more scripts that I hope to make available to the public, that are currently making my life even easier with Cake.

And finally, I will soon be launching a really exciting new project that I hope will help the Cake community grow even more. If you know of Ryan Bates and his excellent <a href="http://railscasts.com">Railscasts</a> site, then you will like what I have planned.

Keep it here! ;)
