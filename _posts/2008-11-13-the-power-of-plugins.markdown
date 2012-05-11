--- 
layout: post
title: The power of plugins
categories: articles
---
Since I discovered the <a href="http://github.com/cakephp/debug_kit">DebugKit plugin</a> for CakePHP that is currently in early development by Mark Story and others (including me. well, one commit still means I helped ;)), I have been left rocked about the power of plugins. I always thought that plugins were simply a way to create a Cake app that can be plugged in to an existing application. But It seems I underestimated their power.

So I began to think about how I could refactor Migrations into a plugin, rather than a bunch of files that you drop into your vendors directory. And that took me all of 20 seconds! I didn't have to change a thing. Thanks to <a href="https://trac.cakephp.org/changeset/7871">this latest commit</a>, you can now use a shell script from any plugin.

So I just drop the migrations directory directly into my plugins directory, and wham bam thank you maam! I created my first Cake plugin.

Of course, I can still drop the migrations shells into my global vendors/shells directory, but I just like the way I can plug it in.

So a plugin is now the recommended way to use Migrations.
