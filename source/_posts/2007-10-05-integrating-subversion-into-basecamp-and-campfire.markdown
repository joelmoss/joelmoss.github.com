--- 
layout: post
title: Integrating Subversion into Basecamp and Campfire
categories: articles
---
For the last few days, I have been thinking about how me and the team around me can improve productivity and communications when developing. Currently, the system we use is a little disjointed, and utilizes several different systems and solutions. Fortunately one such solution is <a href="http://basecamphq.com">Basecamp</a>, which happens to be one of the best around and has been in use by the company for a while now. So after spending a little time with the web based application, I realised that it should be able to do, or at least manage everything we do.

So last night I sat down and played with the <a href="http://developer.37signals.com/basecamp">Basecamp API</a>, to see what could be done with it. And I came up with a post-commit hook for <a href="http://subversion.tigris.org/">Subversion</a>, that posts a message for each subversion commit. This message tells me the change log, what files were changed, and who made the commit. So now we can all see and receive Basecamp notices for every single changeset.

We have also started using <a href="http://www.campfirenow.com/">Campfire</a>, so I then had a little play with <a href="http://opensoul.org/2006/12/8/tinder-campfire-api">Tinder</a>; Campfire's unofficial API, and added some more code to the Subversion hook. So as well as creating a message in Basecamp detailing each Changeset, the same changeset is also posted in the appropriate Campfire room. So we have a real time view of our development progress.

So here is the code. It's all in Ruby, as it was easy peasy. And it utilises the Basecamp API Wrapper.

<pre lang="ruby"><code>
%w( rubygems tinder basecamp ).each { |f| require f }

config = {
:subdomain =&gt; 'My-Subdomain', # Campfire and Basecamp subdomain
:email =&gt; 'user@mydomain.com', # Campfire email login
:username =&gt; 'username', # Basecamp username
:pass =&gt; 'password',
:room =&gt; 'Development', # Campfire room
:project_id =&gt; 12345, # Basecamp project id
:category_id =&gt; 678910, # Basecamp message category ID
:ssl =&gt; true
}

svnlook = '/usr/bin/svnlook' # full path to the svnlook command
repo_path = ARGV[0]
revision = ARGV[1]
project = repo_path.split('/').last

commit_author = `#{svnlook} author #{repo_path} -r #{revision}`.chop
commit_log = `#{svnlook} log #{repo_path} -r #{revision}`
commit_files = `#{svnlook} changed #{repo_path} -r #{revision}`

# create a message in basecamp
basecamp = Basecamp.new("#{config[:subdomain]}.projectpath.com", config[:username], config[:pass], true)
basecamp.post_message config[:project_id], {
:title =&gt; "Changeset ##{revision}",
:body =&gt; "#{commit_author} just committed changeset ##{revision}...\n\n&lt;blockquote&gt;&lt;pre&gt;#{commit_log}\n#{commit_files}&lt;/pre&gt;&lt;/blockquote&gt;",
:category_id =&gt; config[:category_id]
}

# create a message in campfire
campfire = Tinder::Campfire.new(config[:subdomain], :ssl =&gt; config[:ssl])
campfire.login config[:email], config[:pass]
room = campfire.find_room_by_name config[:room]
room.speak "#{commit_author} just committed changeset ##{revision}..."
room.paste "#{commit_log}\n#{commit_files}"
</code></pre>

Simply copy and paste this into a file called 'post-commit.rb' and save that in your subversion repository's hooks directory. Don't forget to set its permissions as required (chmod 755 on linux/unix). Then create another file in your hooks directory and call it 'post-commit' and do the same with the permissions. In the 'post-commit' file, paste the following code:

<pre lang="sh"><code>#!/bin/sh

REPOS="$1"
REV="$2"

ruby /Users/joelmoss/dev/src/testing/hooks/campfire.rb "$REPOS" "$REV"
</code></pre>

If 'post-commit' already exists, just append the last line above to the end of the file.

You will then need to install a few Ruby Gems. Namely Tinder and XML-Simple. So just run the following command:

<pre><code>sudo gem install tinder xml-simple --include-dependencies
</code></pre>

And finally, you will need the <a href="http://developer.37signals.com/basecamp/basecamp.rb">Basecamp API wrapper</a>. You can get that at <a href="http://developer.37signals.com/basecamp/basecamp.rb">http://www.basecamphq.com/api/basecamp.rb</a>. Save that in somewhere in your Ruby path. Ideally, that would be in your 'site<em>ruby' directly. On my Mac, that is at '/usr/local/lib/ruby/site</em>ruby/1.8/'.

And now you should be good to go. As long as you have enabled the API in your Basecamp and your settings are correct, whenever anyone makes a commit to Subversion, you will all be able to see it in Basecamp and Campfire.

I plan to do more with this, as we will need a better bug management system, as Bugzilla is just so damn ugly. But I will leave that to another post.

Enjoy!
