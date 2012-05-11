--- 
layout: post
title: CakePHP Migrations v4.0 Beta
categories: articles
---
I am excited to announce the a beta of the next version of the popular database Migrations shell for CakePHP 1.2. It's a little later than expected (I wanted a release candidate out by now) due to a certain muppet who didn't commit his changes to SVN!

<strong><a href="http://code.google.com/p/cakephp-migrations/downloads/list">Get it now!</a></strong>

Take a look at the <a href="http://code.google.com/p/cakephp-migrations/source/browse/trunk/CHANGELOG">ChangeLog</a>, and you will see a few long needed changes. The most notable being the ones discussed <a href="http://developingwithstyle.com/articles/2008/05/05/the-problem-with-migrations.html">earlier</a>. Here's the rundown of what you can find in the beta...

<!--more-->

<strong>Timestamped Migrations</strong>

All migration files now use the current GMT timestamp of when they were generated. This has been added to almost eradicate any chance of conflicts when working as part of a team.

<strong>Interleaved Migrations</strong>

This helps solve the problem of migrating out of order or missed migration files. So when you migrate up, it will now run any migrations that have not been run, and when you migrate down, it will ignore migrations that have not been run. To help with this feature, the table that Migrations uses to keep track of the current version has been replaced with one that keeps a record of every migration that has been run.

<strong>Migrations love Arrays too</strong>

OK, so not everyone likes YAML, so I gave in. Migrations now supports native PHP arrays within your migration files. Something like this:

{% codeblock php %}
$migration = array(
    'up' => array(
        'create_table' => array(
            'rooms' => array(
                'name' => array(
                    'type' => 'string'
                ),
                'topic' => array(
                    'type' => 'text'
                )
            )
        )
    ),
    'down' => array(
        'drop_table' => 'rooms'
    )
);
{% endcodeblock %}
In fact, this now means you can use any old PHP code within your migrations. Opens up some nice possibilities.

<strong>New command: "migrate info"</strong>

A new command has been added that shows you the full list of migration files, along with some really useful info, such as what migrations have been run, and when.

<strong>Migrating Specific files</strong>

You can now also migrate a specific UP or DOWN section from any migration file. How specific is that?

Those are the changes so far, there may well be one or two more to come before the release candidate, but I am still looking into those and will be posting on them very soon. You can also expect to see some bug fixes by the time the release candidate arrives.

So please <a href="http://code.google.com/p/cakephp-migrations/downloads/list">download</a> and play to your hearts content. If you discover any bugs, or if you have any ideas for enhancements and want to see them included in this release, please <a href="http://code.google.com/p/cakephp-migrations/issues/list">create an issue</a>. If you just want to leave a comment and talk to me about this, leave your comment below.
