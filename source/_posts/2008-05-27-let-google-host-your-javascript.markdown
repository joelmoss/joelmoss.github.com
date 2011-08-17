--- 
layout: post
title: Let Google host your Javascript
categories: articles
---
Google has just released yet another API. But this time, the API is not interfacing with any of Google's own services.

The <a href="http://code.google.com/apis/ajaxlibs/">Google Ajax Libraries API</a>, is a content delivery option and loading architecture for the most popular open source Javascript libraries. It means that with just one line of code, you can load your favourite Javascript library into your web app, and not have to worry about keeping the library up to date. It also means the files are gzipped and minified for you, and takes advantage of any caching. This should mean faster loading JS includes.

<!--more-->

As announced on <a href="http://ajaxian.com/archives/announcing-ajax-libraries-api-speed-up-your-ajax-apps-with-googles-infrastructure">Ajaxian</a>, the API is available now, and supports the following open source javascript libraries:

<ul>
	<li>Prototype</li>
	<li>Scriptaculous</li>
	<li>JQuery</li>
	<li>MooTools</li>
	<li>DoJo</li>
</ul>

The simplest way to load any of the above JS libraries, is as follows:

<pre lang="html"><script src="http://ajax.googleapis.com/ajax/libs/jquery/1.2.6/jquery.js"><!--mce:0--></script></pre>

Or you can use this nifty little snippet, which will always load the latest and greatest version of the library:

<pre lang="javascript"><script src="http://www.google.com/jsapi"><!--mce:1--></script>
<script type="text/javascript"><!--mce:2--></script></pre>

Take a look at the <a href="http://code.google.com/apis/ajaxlibs/documentation/">docs</a> and play. We like!
