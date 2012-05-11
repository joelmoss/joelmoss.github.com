---
layout: post
title: Handling Dates in MongoDB
categories: articles
---

<p>I've been using <a href="http://www.mongodb.org/">MongoDB</a> quite a bit recently in several different projects, and it kicks ass. But the hardest thing to learn and to get used to with Mongo, is it's schemaless structure. With SQL databases like MySQL, you always have a defined and very rigid structure, which is of course the schema for each table you create. You create a table with a few columns; each column has a set type, a length, and a whole host of other variables.</p>

<p>It's this rigid structure that most of us have gotten used to for years, and that is the hardest thing to shake off when using NoSQL databases such as MongoDB.</p>

<p>But that is not to say that Mongo has no defined structure. In fact, that is far from the truth. Mongo and all schemaless databases have defined structure, but the difference is that that structure is defined by you. And that is what makes Mongo so cool. No need to actually create any tables and define each column - Just insert some data in your own defined way.</p>

<p>But there is a side effect of this schemaless idea. Even though you no longer have to define a schema in the traditional sense, you still have to think about the structure of each collection, and how that will look. In fact, there is a lot more to think about, as there are a lot more ways to structure your data with Mongo and other schemaless databases.</p>

<p>It's somewhat of a steep learning curve, but well worth sticking with. I'm still leaning the best ways to structure certain data types, and dates is one that I think I've nailed.</p>

<!--more-->

<p>Nearly all your collections will no doubt contain some sort of date or time stamp. While Mongo does have it's own native <code>Date()</code> object, it's only really useful within the Mongo shell. I need to use it within PHP and Ruby and other languages. Up until recently, I've been saving <code>datetime</code> as "<code>2010-07-09 13:56:31</code>". This works fine most of the time, but when you start needing to gather your data in more advanced ways, it starts to fall apart.</p>

<p>For example, I'm currently using Mongo and the equally awesome <a href="http://code.google.com/p/redis/">Redis</a> for logging data for <a href="http://quicksearch.shermanstravel.com">ShermansTravel.com</a>. I needed to log a bunch of data each time a user clicks one of our paying ads. I ended up with collection records like this: (in PHP, as that is what this project calls for unfortunately)</p>

<div class="highlight"><pre><code class="javascript">
  {
    "_id" : ObjectId("4bfea7246c6151d127f80100"),
    "button_rank" : "5",
    "category" : "flights",
    "class" : "Economy",
    "cpc" : "0.17",
    "destination_place_id" : "197868",
    "from_code" : "ORD",
    "from_code_include_nearby" : false,
    "travelers" : "1",
    "created" : "2010-03-29 20:15:34"
  }
</code></pre></div>

<p>Notice the the <code>created</code> timestamp on the last line there. Nothing special there, and I can find by the <code>created</code> date without any issue at all. But I need to now count all clicks grouped by day, not time. This is where the above falls apart.</p>

<p>This is what I tried:</p>

{% codeblock lang:php %}
  $keys = new MongoCode('function(doc) { return { created: doc.created.split(" ")[0] }; }');
  $reduce = new MongoCode('function(doc, prev) { prev.count++; }');
  $clicks = $this->group($keys, array('count' => 0), $reduce);
{% endcodeblock %}

<p>Again, this works... almost! This week, the clicks collection ended up with 900,000 records, and using the above group query kept timing out. The problem is the second line where instead of simply specifying which key(s) to group by, I have to pass a PHP MongoCode object containing a Javascript function that creates and returns a custom key. In this case, I am simply grabbing the <code>created</code> key of each record, and splitting the string, so I have the date and the time. I then return the date only, and can now group by date. This means that Mongo is iterating over every record and applying that function to each one, which obviously can take some time on larger collections, and completely ignores any indexes you may have created.</p>

<p>So I quickly determined from this that I was storing the date and time in the wrong way. I need to split up the date and time. I now have this:</p>

<div class="highlight"><pre><code class="javascript">
  {
    "_id" : ObjectId("4bfea7246c6151d127f80100"),
    "button_rank" : "5",
    "category" : "flights",
    "class" : "Economy",
    "cpc" : "0.17"
    "destination_place_id" : "197868",
    "from_code" : "ORD",
    "from_code_include_nearby" : false,
    "travelers" : "1",
    "created" : { "d" : "2010-03-29", "t" : "20:15:34" }
  }
</code></pre></div>

<p>The last line still shows the <code>created</code> date and time, but instead stores each in an embedded object or hash. This means that I can still find by <code>created</code> date and time with just a little change, but more importantly, it means I can group much easier and much, much faster:</p>

{% codeblock lang:php %}
  $key = array('created.d' => 1);
  $reduce = new MongoCode('function(doc, prev) { prev.count++; }');
  $clicks = $this->group($key, array('count' => 0), $reduce);
{% endcodeblock %}

<p>As you can from the second line in the above, I am no longer passing a function to build the key I want to group by - which was what was causing the problem. I now simply pass the key I want to group by: <code>created.d</code>. The code is leaner and the query is loads faster, and my indexes are respected.</p>