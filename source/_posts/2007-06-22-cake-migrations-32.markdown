--- 
layout: post
title: Cake Migrations 3.2
categories: articles
---
Cake DB Migrations has now been updated to work with the very latest version of CakePHP 1.2 and the new (hopefully final) console/shells system. I have also added a few extra goodies to make life a little easier.

The new features and changes are as follows:

<ul>
	<li>You can now specify a column without the need to specify the column type. Type is set to string, which is simply a varchar(255) column.</li>
	<li>Ability to add user definable foreign keys by simply specifying the 'fkey' as a column name, followed by the name(s) of the foreign key(s).</li>
	<li>You can now include PHP code within the YAML migration files</li>
</ul>

Because the console system in Cake 1.2 has changed a bit, you now have to place the below script in a slightly different place. Within your main 'vendors' directory above your app and cake core directories, paste the below code into a file called 'migrate.php' and place that file in a directory called 'shells'.

Now just bring up your favourite command line tool and cd into your cake applications root directory and run the following:

<pre><code>./cake migrate</code></pre>

And that is it! That will migrate to the lastest version. You can specify the version like this:

<pre><code>./cake migrate -v 3</code></pre>

As promised, I hope to create a screencast going through all aspects of migrations and how they can save your life.

You can find the script in <a href="http://cakeforge.org/snippet/detail.php?type=snippet&amp;id=165">CakeForge</a>, aswell as new versions of the <a href="http://cakeforge.org/snippet/detail.php?type=snippet&amp;id=166">Fixtures</a> and <a href="http://cakeforge.org/snippet/detail.php?type=snippet&amp;id=167">Generator</a> shells.
