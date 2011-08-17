--- 
layout: post
title: Migrations V2.1 - Now with Fixtures
categories: articles
---
I have just pushed out a new version of Cake Migrations available for <a href="http://homepageuniverse.com/migrations.zip">download</a> right now. Version 2.1 fixes a few bugs here and there, but more significantly, Migrations now come with Fixtures.

Following is a quick rundown of what's new in this release.
<h4>Fixtures</h4>
Fixtures are pretty much the same thing as migrations, but are only used for inserting test data into your development database. So after you run your migrations, simply create a fixture for each of your tables, which will fill them up with test data you can use to test your apps. Coz if you think about it, it's a bit pointless testing without actual data.

So now when you run the migrate script, you get to choose whether you want to work with your migrations or your fixtures. Select fixtures and presuming you have some tables in your DB, it will ask you which table you want to create fixtures for. Selecting a table will then create a blank fixture file in <em>app/config/fixtures</em> which you should then place your fixtures into.

Something like this:

{% codeblock %}
#
# Fixture YAML file
#
-
 name: bob1
 username: bobby1
 password: mypass
 created: NOW
-
 name: bob2
 username: bobby2
 password: mypass
 created: NOW
 modified: NOW
-
 name: bob3
 username: bobby3
 password: mypass
 created: NOW
-
 name: bob4
 username: bobby4
 password: mypass
 created: NOW
-
 name: bob5
 username: bobby5
 password: mypass
 created: NOW
-
 name: bob6
 username: bobby6
 password: mypass
 created: NOW
{% endcodeblock %}

After each hyphen a fixture or table row is set. You simply set key:value pairs for the fields you want to fill. Don't forget the hyphen before each fixture and of course the usual YAML indents, etc.

You may notice that I have not specified a date in any of the <em>created</em> values. I used the <em>NOW</em> keyword instead, which basically inserts the current datetime for you (and in the right format).

Now all you need to do is run migrate.php again, select fixtures and the table you want to run these fixtures for. It will detect this fixture file and insert your data. And voila! Instant test data for your app.
<h4>Created/Modified fields</h4>
Previously you had to specify that you wanted the <em>created</em> and <em>modified</em> fields created in your migrations. Not anymore! These two fields will be created for you in every table, so just leave them out completely.
<h4>Primary Key auto incremented</h4>
One thing that I left out in previous versions was to make the primary key field auto increment. This is now added.

As you can see, not many changes there, but I thought it deserved a minor increment in version number because of the addition of Fixtures. Watch out for more changes, including the ability to generate migration files from the structure of an existing database. I also plan on making the Migrations script independant. So it will work with and without Cake.

So as usual, please play around with it and let me if you find any bugs. It would also be great to hear what you all think about it all.

Enjoy!
