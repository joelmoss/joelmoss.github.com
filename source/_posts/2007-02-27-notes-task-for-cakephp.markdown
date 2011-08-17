--- 
layout: post
title: Notes Task for CakePHP
categories: articles
---
Just knocked up another bake2 task for CakePHP 1.2 that I think is pretty damn cool.

The Notes Task is a source-annotations extractor! ?!?!

What's that then? I hear you ask. Well, this task is a great way to keep track of your ToDo's and FixMe's that are most likely littering all over your code.

I have started adding annotations to my code to remind me to do, fix or optimise something within the    code. Just add any of the following anywhere in your code - usually at the point that needs attention:

<pre><code># TODO: this is my first todo item
# FIXME: please fix this
# OPTIMIZE: this has got to be optimised!
</code></pre>

The problem with this is how to track them all. So that is why I created this Notes Task.

Just get the code from <a href="http://cakeforge.org/snippet/detail.php?type=snippet&amp;id=170">CakeForge</a>, save [it as notes_task.php in your vendors/tasks directory and then run:

<pre><code>php bake2.php notes app_alias</code></pre>

and the task will check all your PHP scripts in your app for any of the above notes and print them out in a nice readable format, with line numbers, etc.

You can find specific notes like so:

<pre><code>bake2.php notes app_alias todo
bake2.php notes app_alias fixme
bake2.php notes app_alias optimise
</code></pre>

As a side note, you can now also find my other tasks - including migrations - at CakeForge.

<ul>
	<li><a href="http://cakeforge.org/snippet/detail.php?type=snippet&amp;id=165">Migration Task</a></li>
	<li><a href="http://cakeforge.org/snippet/detail.php?type=snippet&amp;id=166">Fixture Task</a></li>
	<li><a href="http://cakeforge.org/snippet/detail.php?type=snippet&amp;id=167">Generator Task</a></li>
</ul>
