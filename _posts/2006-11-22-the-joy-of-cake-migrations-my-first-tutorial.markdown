--- 
layout: post
title: The Joy of Cake Migrations - my first tutorial
categories: articles
---
As <a href="http://joelmoss.info/switchboard/blog/1992:Cake_DB_Migrations_strikes_back">promised</a>, the following is a tutorial on how to use and take advantage of Migrations in your <a href="http://cakephp.org">CakePHP</a> development. I suppose you could also call it a basic manual.

This article assumes that you already have an installation of CakePHP which is already configured and ready to go. It also assumes that you know what migrations are and why you need them.  For more information on DB Migrations, please see <a href="http://joelmoss.info/switchboard/blog/1992:Cake_DB_Migrations_strikes_back">here</a>.
<h4>Getting started</h4>
Once you have installed and configured CakePHP, you should download the Migrations package from <a href="http://homepageuniverse.com">HomepageUniverse</a> <a href="http://homepageuniverse.com/migrations.zip">here</a>. Unzip the archive into your <em>vendors</em> directory that is above your <em>app</em> directory.

<strong>Remember</strong> that you should place the migrations package in your top level <em>vendors</em> directory, not the <em>vendors</em> directory within your <em>app</em> directory.

Within the <em>migrations</em> directory are a number of files and two more directories. I will explain each here:
<ul>
	<li>migrate.php <em>[file]</em> - This is the main Migrations script.</li>
	<li>MDB2.php <em>[file]</em> - This is Pear's MDB2 database abstraction library.</li>
	<li>Spyc.php <em>[file]</em> - The Spyc YAML library (just in case you don't have the PHP Syck extension  installed)</li>
	<li>MDB2 <em>[directory]</em> - The included MDB2 library files.</li>
	<li>Examples <em>[directory]</em> - A few example YAML migration files</li>
</ul>
The main file you should be interested in, is the migrate.php file. This is the script that you need to run on your command line, and helps you generate, run and manage your migrations.

To use it, simply run the following from within your cake root directory and follow the on screen prompts:
<pre><code>php vendors/migrations/migrate.php
</code></pre>
Read on for more detailed description of its usage.
<h4>Migration Basics</h4>
I will quickly run through what migrations do and how they do it. This should help you understand how and why you should use them.

<strong>Database Support</strong>
All migrations let you do is run database queries in a structured and simple manner. Pear's <a href="http://pear.php.net/package/MDB2">MDB2</a> library is used to interface with your database, so you can use any database engine that MDB2 supports. Why do I use MDB2 when Cake has a very good database? Because Cake's DB classes do not support the creation of tables, fields, indexes, etc.

<strong>Migration Files</strong>
Migrations use a selection of migration files that are used to manage your database. You can roll forward and backwards through each file, just as you would with any version control system, such as subversion. The migration files are written in a very simple, human readable language called <a href="http://en.wikipedia.org/wiki/YAML">YAML</a>, and do not need to contain any SQL queries at all. This way, migrations are 100% portable and can be used with almost any database engine. You can find some example migration files in the Examples directory of the download.

When you run a migration, the script simply analyses each migration file and converts the YAML into database queries and performs the actions specified in the file. The best way to demonstrate this would be to actually do it. So on we go to the meat of this tutorial.
<h4>The Migration Script</h4>
Just like Cake's Bake.php script, the migrate.php script must be run via the command line. You can do three things with the migrate.php script:
<ol>
	<li>Generate Migration Files</li>
	<li>Run Migrations</li>
	<li>Reset your Migrations</li>
</ol>
We will go through each one in turn in the next section.

The migrate.php script also takes some optional command line arguments, but I will not go into them too much here. Just run the following for more help:
<pre><code>php vendors/migrations/migrate.php -h
</code></pre>
<h4>The Generation Game</h4>
Before you can do anything else, you need to generate your migration files. You can of course create these manually yourself, but it's much easier and less error prone if you use migrate.php. So go ahead and run the migrate script;
<pre><code>php vendors/migrations/migrate.php
</code></pre>
Assuming everything is good, you should see a lovely little <em>'CAKEPHP MIGRATIONS'</em> banner in your command line window.

If you have not already configured your Cake database config, it will help you with that in the same way that bake.php does. So go ahead and follow the prompts if you need to do that.

After that, the script will then check that the 'schema_info' table exists in your database, and creates it if it isn't there. This table is used to keep a record of what migration version your app is currently at. So it is very important and should not be tampered with.

Once all that is done, you should see a few lines of data. The first line tells you which application [dir] you are using. Then it tells you your current migration version, along with the number of migration files previously generated.

Now choose 'Generate' from the three Options menu. Then just follow the prompts and your very first migration file will be created for you and placed in a <em>migrations</em> directory in your app's <em>config</em> directory. Take a look and you will see that the script has numbered your file. It will do this for every file generated and simply increment each time. This numerical value is used to determine what order your migrations should be run. It is basically the version number.
<h4>YAML, YAML, YAML</h4>
Before we get started on editing your migration file, I strongly recommend that you get acquainted with YAML. You should read a brilliant little tutorial called <a href="http://yaml.kwiki.org/?YamlInFiveMinutes">YAML in Five Minutes</a>. And of course you can check out the <a href="http://www.yaml.org">official YAML site</a>

I am going to try and explain a migration file as best I can. So please bear with me, if I splutter.

A migration file consists of two main parts; an UP and a DOWN. The UP section contains the commands that you would like performed when migrating up to this file. And the contents of the DOWN section are run when you rollback from or through this file to a previous version. So usually, the DOWN section contains an exact opposite of what is in the UP section, as you would usually want it to reverse the changes made in the UP section.

Lets start by creating a table. Enter the following into your migration file;

{% codeblock %}
#
# migration YAML file
#
UP:
  create_table:
    users:
      first_name:
    type: text
    index: true
      last_name:
    type: text
      email:
    type: text
    unique: true
      age:
    type: integer
    length: 3
    notnull: false
DOWN:
  drop_table: users
{% endcodeblock %}

Directly under the UP section name, is the action that should be performed. We are creating a table, so we use 'create_table'. Then you tell the migrate script what we want to call this table. After which we create the fields by specifying each field name and its properties. All properties are optional, apart from the 'type', which is required.

Available field types are:
<ul>
	<li>text</li>
	<li>integer</li>
	<li>blob</li>
	<li>boolean</li>
	<li>float</li>
	<li>date</li>
	<li>time</li>
	<li>timestamp (datetime)</li>
</ul>
You can then set the following optional properties:
<ul>
	<li>length</li>
	<li>notnull</li>
	<li>default</li>
	<li>index</li>
	<li>unique</li>
	<li>primary</li>
</ul>
If you notice in the example above, I have not specified a primary key on any of the fields, and there is no ID field. That is because the migrate.php script will create an ID field for you and set it as the primary key. You can overide that if you wish. Just add a line directly under the UP line like this:

{% codeblock %}
UP:
  create_table:
    users:
      no_id: true
      first_name:
    type: text
    index: true
      last_name:
    type: text

....
{% endcodeblock %}

If you do use the 'no_id' line, you will need to set the primary key and ID field yourself.

Now we need to define the DOWN section. All we want to do is to reverse the actions of the UP section. So we simply say:

{% codeblock %}
DOWN:
  drop_table: users
{% endcodeblock %}

In both sections, you can create/drop more than one table. To create another table, just create another create_table section starting from the table name. To drop more than one table, do this:

{% codeblock %}
DOWN:
  drop_table: [users, table2, another_table]
{% endcodeblock %}

And that my friends, is your very first migration file. I won't go into the details of all the actions that migrations can do as the Examples are pretty good at doing that, and this tutorial is already pretty long.

Other actions available:
<ul>
	<li>alter_field</li>
	<li>add_field</li>
	<li>drop_field</li>
	<li>query</li>
</ul>
Pretty self explanatory really, but the last one; 'query', lets you run a raw SQL query. So you can use it to insert/update data. Something like:

{% codeblock %}
query: INSERT INTO users SET first_name='Joel'
{% endcodeblock %}

<h4>Run it!</h4>
Now we get to the exciting part. We run the migration.

Start the script again and accept the default option: "Migrate". It will then give you a list of migration files along with their version number. You only have one file, so type the number of that file, which should be '1'.

Ta Da!! migrate.php will then fetch and parse the file and run the commands on your database. Now check your database and you should see a spangly new table ready for your app to use.

But what happens if you don't like that table and want to change it. You got two options; roll back the version or generate and run a new migration file with the changes.

To rollback the changes, just run migrate.php, accept the default option and enter the number '0'. This happens to be the version prior to the migration you just made, and is also the base. So choosing that will rollback all migrations back to the beginning. Try it now. You should now notice that your table has been dropped.
<h4>Is that good or wot?</h4>
That is pretty much it. The last option: 'Reset', will do exactly that. It will reset all your migrations and optionally delete your migrations files. So be careful when using that.

Play around with it and <a href="http://developingwithstyle.com/switchboard/forum/create">create a forum post</a> here if you have any questions, bug reports or suggestions.

Thanks again and look out for more [shorter] tutorials and maybe a few screencasts in the near future.
