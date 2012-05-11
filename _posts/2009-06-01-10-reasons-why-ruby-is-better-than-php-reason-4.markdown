--- 
layout: post
title: "10 Reasons why Ruby is better than PHP - Reason #4"
categories: articles
---
<p>I bet you thought I'd never get any more reasons out did ya? Well, today, I'm going to tell you all about IRB and the Rails command line debugger, both of which I use religiously.</p>

<p>One of the great pleasures of using Ruby, apart from the <a href="http://developingwithstyle.com/articles/2009/05/20/10-reasons-why-ruby-is-better-than-php-reason-1.html">previous</a> <a href="http://developingwithstyle.com/articles/2009/05/21/10-reasons-why-ruby-is-better-than-php-reason-2.html">three</a> <a href="http://developingwithstyle.com/articles/2009/05/27/10-reasons-why-ruby-is-better-than-php-reason-3.html">reasons</a>, and of course the following five reasons, is the wonder that is the Interactive Ruby console, or IRB. IRB is an interactive interpreter; which means that instead of processing a file, it processes what you type in during a session. It's a great tool for testing Ruby code, and a great tool for learning Ruby. </p>

<p>Once you have Ruby installed on your computer, you will notice that the <code>ruby</code> command will do the same thing as PHP - it silently waits for a script to be streamed in on <code>stdin</code>. On it's own, that's not particularly friendly, or even that useful. But another command that is installed alongside Ruby, is the <code>irb</code> command. Start up your command line tool of choice, and simply enter these three immortal letters: <code>irb</code>. Then you will see this:</p>

{% codeblock ruby %}
irb>
{% endcodeblock %}

<p>This is the <code>irb</code> prompt. Now all you do is simply type any ruby code, and it will show you the result of each and every expression as it is evaluated. Not sure how a method works, or can't remember the output of a method? Then test it with IRB.</p>

<p>IRB lets you do things without having to fake out your controller. For example, in PHP, I'm forever using <code>echo</code> or CakePHP's <code>debug</code> function to print out some useful info to the browser when debugging my code. But when developing with Ruby, I simply have my trusty IRB prompt ready and waiting for me to inflict world domination.</p>

{% codeblock ruby %}
>> @george = Person.find_by_name('George')
>> @bob = Person.find_by_name('Bob')
>> @bob.friends << @george
{% endcodeblock %}

<p>Each of the above lines will be following by IRB echoing the result. So I can see exactly what is going on, and without me having to echo out data all through my code and to the browser.</p>

<p>This is actually very, very useful, and is a great way to test your code, or in fact any code at all. It's even better if you are a command line freak like me.</p>

<p>What is even better, better (!?) is that Rails also has its own command line interpreter, which is basically an extension of IRB. What makes it a little different, is that when it is started up, it also loads all your Rails code. So you have instant access to your Rails models, which is also very handy. Just cd to your Rails app root, and run:</p>

{% codeblock ruby %}
script/console
{% endcodeblock %}

<p>You are then shown a similar command line prompt to IRB, and can run any part of your Rails app code.</p>

<p>To wrap up reason #4, I want to tell you about one of the best things about developing with Ruby on Rails. It's another extension of IRB, similar to Rails <code>script/console</code>, but is simply genius when debugging your Rails code.</p>

<p>There are several ways in which you can run your Rails app, but the traditional method is by using the the <code>script/server</code> script within your app. When run on the command line, this will start up a small web server, usually run by Webrick or Mongrel. Now I wouldn't recommend this method when running your app in production, as <a href="http://www.modrails.com/">there are much better, and more efficient ways to do so</a>, but I use this all the time when developing or testing my app code.</p>

<p>Just <code>cd</code> to your Rails app root and run this on the command line:</p>

{% codeblock ruby %}
script/server -u
{% endcodeblock %}

<p>Notice I appended a command line flag; <code>-u</code>. This tells the Rails server to start up in Debug mode. If you use Mongrel, this is what you will see:</p>

{% codeblock ruby %}
=> Booting Mongrel
=> Rails 2.3.2 application starting on http://0.0.0.0:3000
=> Debugger enabled
=> Call with -d to detach
=> Ctrl-C to shutdown server
{% endcodeblock %}

<p>And the command line prompt will sit there blinking at you, waiting for you to load your app in your browser. So don't keep it waiting, open up your browser, and go to <code>http://localhost:3000</code>, and you will be shown your Rails app in all its glory.</p>

<p>Now we get to the good bit. Open up the code of any of your controllers in your favourite IDE or <a href="http://macromates.com">text editor</a>. Then type the word <code>debugger</code> within one of your actions. Then go back your browser and navigate to that page. You should the notice that the page does not appear to finish loading. That is because your <code>debugger</code> keyword within the action method, has paused the server until you tell it to continue.</p>

<p>Go back to your command line when you started the Rails server, and you will see a bunch of log data, following by what looks like an IRB prompt. That is effectively what it is. You can now type any Ruby code at that prompt, just like you would with IRB or <code>script/console</code>. But the beauty of this, is that you have access to all the variables and methods at exactly the same point in your code where you placed the <code>debugger</code> keyword.</p>

<p>So instead of having to type echo or print statements throughout your code, and running them through your browser to see the results. You can add the debugger keywork at the point where you want to debug, and use the command line to access your code in real time.</p>

<p>I really hope you got all that, as this feature has saved me hours and hours of time when debugging my code. I can honestly say that it is a life saver. You really should try it out now, or if you're a little impatient, <a href="http://tryruby.hobix.com/">try it out in your browser for instant gratification</a>. You should also check out Amy Hoy's "<em><a href="http://slash7.com/articles/2006/12/21/secrets-of-the-rails-console-ninjas">Secrets of the Rails Console Ninja's</a></em>".</p>

<p>Thanks again for sticking with me, and hold on to your pants for reason #5 where I will be talking about Modules; Ruby's answer to namespaces. Which will lead me nicely onto another Ruby exclusive: Mixins!</p>

<p>P.S. I really appreciate everyone's comments. Keep them coming.</p>
