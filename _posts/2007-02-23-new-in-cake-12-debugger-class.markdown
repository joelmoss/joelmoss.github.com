--- 
layout: post
title: "New in Cake 1.2: Debugger class"
categories: articles
---
Just checked out the CakePHP 1.2 branch this morning and discovered a shiny new class called Debugger. It's pretty obvious what this is, but it ain't no simple debugging function.

The Debugger replaces the default PHP error handling and "provides enhanced logging, stack traces, and rendering debug views". Basically, if any errors occur, Debugger will print these to your browser and tell you everything you need to know about the problem.

To use it, simply include the Debugger class file into your app. This can be achieved very easily by placing the following line at the top of your app/config/bootstrap.php file:

<pre><code>uses('debugger');</code></pre>

And now you get all the data you need when something goes wrong, and right within your browser.

One thing that is lacking though, that I would really like to see, is the option to output the debugging results to a log file instead. As outputting to the browser can be very messy. I have already opened a ticket with this suggestion, so hopefully the core team will add that.
