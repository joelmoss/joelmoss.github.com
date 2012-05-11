--- 
layout: post
title: Migrations v3.3
categories: articles
---
I just pushed out a pretty good update of Migrations today. Version 3.3 includes some cool updates that make migrations even easier and even faster to use. (didn't I say that last time?)

The biggest change is the introduction of migration file generation within the Migrate shell itself. This functionality used to be included within the accompanying Generator shell. But I decided that this was a little unnecessary, so as soon as Fixtures is updated (later this week) the Generator shell will be phased out and deprecated.

I also cleaned up the code a little and documented some more. There is now a help command that will help you with how to use it.

So, you can get v3.3 of Migrate.php from <a href="http://cakeforge.org/snippet/detail.php?type=snippet&amp;id=165">CakeForge</a>.

Here are the other changes:
<ul>
	<li>[*] a little cleanup and refactoring, including more detailed and friendly output</li>
	<li>[*] added more comments and documentation</li>
	<li>[+] migration file numbering now uses three digits starting from 001</li>
	<li>[+] added new 'version' and 'v' method as an alternative to the '-v' switch</li>
	<li>[+] can now generate migration files as generator shell is now deprecated.</li>
	<li>[+] can now run all migrations from the current version down, up to the latest version</li>
	<li>[+] can now use shortened YAML when specifying column properties</li>
</ul>

Examples:

<pre><code>name: [string, 32, not_null]  # will create a string(varchar) column with length 32 and not null
- no_dates   # no date columns will be created (don't forget the hyphen)
- [no_dates, no_id]   # no date or ID columns will be created (don't forget the hyphen)
</code></pre>

Enjoy one and all!
