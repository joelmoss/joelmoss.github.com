--- 
layout: post
title: The problem with Migrations
categories: articles
---

Back in February in sunny Orlando, I gave a presentation on why and how one should use CakePHP Migrations. I think the presentation went down well, but when it came to the Q&A at the end of the session, a few issues were raised that - quite honestly - I hadn't actually thought about. It's not that I didn't know about them, it's just that I never came across them to make them a problem for me. But since I began to actually use Migrations in a team of developers, I have come to understand some issues that could potentially be a deal breaker for some teams and users.

<!--more-->

The main issues are related to the use of a version control system such as Subversion, when managing your applications source code and migration files, and it only really applies when using migrations as part of a team. Basically when more than one member of the team creates a migration file and checks it into SVN near the same time, you could end up with an SVN conflict and two migration files that have the same name, but consist of different migration code. Of course you won't see this problem until you SVN update, but when you do, and you try running those migrations, not all will be run. If they are, they could be run in the completely wrong order.

The other issue is that of file naming. You may come across times when migration files have been given the same name. So combine this issue with the first one above, we have a potential for all out world war three!

Let me give you an example...

We have a team of top notch CakePHP developers; Harry, Ron and Hermione (excuse the sad Harry Potter conventions for a second). They all use CakePHP Migrations as part of this new spangly Blog application that they are building. They have already baked the application, so have their skel setup and ready to use, and they have checked in the code into Subversion.

Now Harry starts off by creating a migration file called "001_create_users.yml" so he can create the users table. He modifies the file as he sees fit, creating a few columns etc. He then runs that migration and the users table is created perfectly. So no problems so far and all works great.

However... Ron, being the half-wit he can sometimes be, has gone ahead and created another migration file so he can start work on the posts table. So he creates "001_create_posts.yml" migration file, edits it and runs it. He now has the posts table created, and we still have no problems - yet!

So along skips the team leader; Hermione who wants to check out what Harry and Ron have done so far and make sure all works. So Ron and Harry go ahead and commit the code they have created so far, along with their migration files, then Hermione updates her working copy. Again, all is fine.

But now we come across problems, because Hermione wants to run the migrations. Dun, dun, derrr!

She now sees two migration files:

<ul>
	<li>001_create_users.yml</li>
	<li>001_create_posts.yml</li>
</ul>

She goes ahead and runs these migrations, which work, but because we have two files with a version number of 001, only the first one is run, and the second is ignored.

And there my friends, is the crux of the problem.

So a few weeks ago, I sat down and started thinking about how I could get around these issues. But then all of a sudden, Rails came along and solved it for me.

I still have a great interest in Ruby on Rails. After all, Cake Migrations was inspired greatly by Rails implementation of the same system. I therefore keep a close eye on the Rails changesets. A few weeks ago, I saw quite a large change to the way Migrations are handled in Rails. It seems quite a few people have come across the same problem I just described so eloquently. ;)

So they introduced timestamped migrations. Now why didn't I think of that?

So now instead of using incremental version numbers for each migration file (i.e. 001 or 002), migration files in Rails now use a UTC timestamp indicating the time that the file was created. So now they look something like 12345678_create_users.yml.

This slap in the face simple change now means that all migration files are unique, and conflicts are never experienced. It means that all Migration files can now be run in the correct order. That is, as long as each member of the team has the correct time set!

This change also introduces a nice little extra called Interleaved Migrations. Meaning that any missed migrations can still be caught and run at any time. We will also be able to migrate down and ignore any migrations that have not yet been run. After all, we don't to drop a table that has not yet been created.

So as long as I haven't confused you too much, you now know when is coming in the next version of CakePHP migrations. You can also expect to see support for native PHP arrays in migration files, as well as the YAML. This will mean that you can use your Cake Schema migration files with CakePHP Migrations.

I already started work on this before I left for my holidays, and will continue when I return. Expect a release by the end of May. So hopefully, these changes will make Migrations a non-blocker for all your guys working on Cake apps as part of a team. Hey, but if you think it won't, please let me know. I appreciate any comments and questions any of you may have.
