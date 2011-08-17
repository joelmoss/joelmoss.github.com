--- 
layout: post
title: CakePHP DB Migrations v4.0 is now Stable
categories: articles
---
After months and months of delays due to work constraints, and other crap, I decided that I needed to get my head down and release v4.0 of CakePHP DB Migrations. So that is exactly what I just did!

v4.0 is now available in all its glory at the Google Code repo at <a href="http://code.google.com/p/cakephp-migrations">http://code.google.com/p/cakephp-migrations</a> so get it while it is hot.

You can <a href="http://code.google.com/p/cakephp-migrations/downloads/list">download it here</a>.

I plan on creating a new screencast soon(ish), that will include all the updated features and shortcuts, and will also be easier to hear me and will hopefully be a little shorter and concise. But until then, please play around and let me know if you have any questions at all.

Here's the changes taken directly from the changelog:

<code>
[*] errr... lots of fixes
[*] Fixed bug with old style version numbers
[*] Fixed bug where fkeys were trying to be created with auto_increment
[+] Can now specify whether to use Cake's UUID for the ID column within migration files. Example: "id: uuid"
[+] Can now pass "id: false" within migration file, and no ID column will be created.
[-] Deprecated "no_id: true" in favour of "id: false"
[*] ID column is now correctly set as Primary Key when using UUID type.
[+] Added support for MySQL specific table options (comments, engine/type, collate and charset)
[+] Version numbers now use timestamps so as to minimize conflicts
[+] Now supports interleaved migrations;
when migrating up, will run migrations that have not yet been run, and will ignore any non-run migrations when running down.
[+] Added info option (cake migrate info), which shows information on migrations
[+] Can now specify version number when running up/down, thus allowing you to only run the up/down block of a specific migration
[+] Schema table name is now customizable
[+] Now supports PHP arrays in migration files</code>

I hope to write more about these when I don't have so much decorating on the house to do.
