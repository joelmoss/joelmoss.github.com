--- 
layout: post
title: Cake Migrations 3.7 and Fixtures 3.5
categories: articles
---
Yes, it's another release, but just a small one. Grab it from its <a href="http://code.google.com/p/cakephp-migrations">Google code repo</a>

The main change is the support of Cake's UUID column naming. By default Migrations will use normal auto-increment ID columns. If you want to use the UUID columns, then you just need to set $use_uuid = true.

<!--more-->

Here's the changelog:

Migrations v 3.7

<ul>
	<li>[*] Removed backticks from table name when changing migration version, as they caused errors when using SQLITE.</li>
	<li>[+] Now supports Cake's UUID columns</li>
</ul>

Fixtures v 3.5

<ul>
	<li>[+] Fixtures can now be named, and referenced in foreign keys</li>
	<li>[+] If 'created' column exists in model, and it is not referenced in fixture, then the current datetime will automatically be entered.</li>
	<li>[+] Now supports Cake's UUID columns</li>
	<li>[*] Fixed instantiation of fixture helpers.</li>
</ul>

Enjoy!
