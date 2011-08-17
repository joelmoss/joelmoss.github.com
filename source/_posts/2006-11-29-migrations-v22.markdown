--- 
layout: post
title: Migrations v2.2
categories: articles
---
Another day, another Migrations release. Version 2.2 is now available for <a href="http://homepageuniverse.com/migrations.zip">download</a>.

This release fixes a few more bugs aswell as the following two minor - but nice - changes:
<h4>'created' &amp; 'modified' fields now optional</h4>
Creation of <em>created</em> and <em>modified</em> fields can now be prevented. Example:

{% codeblock %}
UP:
  create_table:
    users:
      first_name:
        type: text
        length: 64
        notnull: true
        index: true
      last_name:
        type: text
        length: 64
      created: false
      modified: false
{% endcodeblock %}

Note the last two lines. Leave these lines out completely and 'created' and 'modified' fields will be created for you.
<h4>Instant operation</h4>
Thanks to a comment from <a href="http://cakebaker.42dh.com">Daniel Hofstetter</a>, you can now run migrations and fixtures with one command and bypassing all prompts. This makes the whole process very fast and save a bundle of time.

Just do the following to run your latest migrations:

```php vendors/migrations/migrate.php -migrate latest```

or specify the migration version:

```php vendors/migrations/migrate.php -migrate 4```

You can also run any specified fixture in the same way:
<pre><code>php vendors/migrations/migrate.php -fixture users
</code></pre>
<strong>BE WARNED</strong> that running the above commands will not prompt you at all, or ask you to confirm the action. So if you mistype a version number of fixture name, and delete all your work, I will not be held responsible.

As usual, play nicely and post away if you have anything to say or request.
