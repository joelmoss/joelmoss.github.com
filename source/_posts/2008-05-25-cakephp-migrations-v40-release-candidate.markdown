--- 
layout: post
title: CakePHP Migrations v4.0 Release Candidate
categories: articles
---
OK boys and girls; I just posted the first and hopefully only release candidate of Migrations v4.0. <strong><a href="http://code.google.com/p/cakephp-migrations/downloads/list">Get it while it's hot</a></strong>.

This release includes a few bug fixes. In fact, it fixes most known bugs, and allowed me to close a lot of the bug tickets. There are only <a href="http://code.google.com/p/cakephp-migrations/issues/list">three or four left</a>, which I hope to eradicate by the time the stable release comes around.

<!--more-->

Here's the changes since the beta...

<strong>UUID Switch</strong>

Migrations have supported Cake's UUID columns as of v3.7, but in that release you could only use them if you had enabled the appropriate variable within the script itself. This obviously meant that you couldn't enable UUID's on a per migration basis. No more I tell you, no more!

If you want your ID column to use UUID's, just use this in your migration:

<pre lang="yaml">up:
  create_table:
    users:
      id: uuid
</pre>

And now when you run that migration,the id column will be created with the correct type and length for using UUID's.

<strong>No ID Syntax Change</strong>

Following on from the above, and to make things just a little easier; using the following will create a table with no ID column:

<pre lang="yaml">up:
  create_table:
    users:
      id: false
      name: text
      age: int
</pre>

This replaces the <code>no_id</code> syntax.

MySQL Specific Commands

And because we all use MySQL right? You can now use some extra commands when creating tables:

<pre lang="yaml">up:
  create_table:
    users:
      id: false
      name: text
      age: int
      mysql_charset: UTF8
      mysql_engine: innodb
      mysql_collate: utf8_general_ci
      mysql_comments: Oooh, this is really fantastic!
</pre>

Pretty much self-explanatory right?

So as I said, I hope this will be the only release candidate, so please <a href="http://code.google.com/p/cakephp-migrations/issues/entry">submit your bug reports</a>, so I can push out a perfect stable release.

Enjoy!
