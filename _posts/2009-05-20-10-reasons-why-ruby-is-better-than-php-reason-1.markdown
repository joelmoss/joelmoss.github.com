--- 
layout: post
title: "10 Reasons why Ruby is better than PHP - Reason #1"
categories: articles
---
<p>So it seems that I didn't provide the best of examples in <a href="http://developingwithstyle.com/articles/2009/05/19/why-i-chose-ruby-on-rails-instead-of-cakephp-for-codaset.html">my last post</a>, when explaining <a href="http://developingwithstyle.com/articles/2009/05/19/why-i-chose-ruby-on-rails-instead-of-cakephp-for-codaset.html">why I chose Ruby on Rails instead of CakePHP</a> for developing <a href="http://codaset.com">Codaset</a>. So I decided that I will write 10 [solid] reasons, why Ruby is better than PHP. After all, that is why I chose it.</p>

<p>I already explained a little bit about the aesthetics of Ruby, and how you can write a method without the need for any curly braces or even parenthesis. So I think I will leave the aesthetics alone for a little bit.</p>

<h3>What a wonderful Objectified world!</h3>

<p>I think one of the most significant differences between Ruby and PHP, and perhaps the basis for a lot of other features of Ruby, is that everything in Ruby is an object. Even though PHP supports Object Oriented Programming, OOP was not even thought of when PHP started out. OOP was simply hacked into the language, and so is not a pure object-oriented language. That is because it uses primitive types; things that are not objects. We use primitive types all the time in PHP. Things like integers, floats and strings are all primitive types. Pretty much all we can do with them, is store data in them and pass them around. On their own, they do very little.</p>

<p>Ruby is a pure object-oriented language, and it was built like that from the start.</p>

<p>So why should I care? I hear you say. Well, because everything in Ruby is an object, everything accepts method calls, even <code>nil</code>. (<code>nil</code> is Ruby's equivalent to PHP's <code>null</code>.)  In PHP, a string isn't smart enough to do anything on its own. If we want to get the length of a string, we would have to call a separate function, and pass the string to it:</p>

{% codeblock php %}
$my_string = 'Just another string';
echo strlen($my_string);
{% endcodeblock %}

<p>With Ruby, we can ask the string directly, to tell us its length:</p>

{% codeblock ruby %}
my_string = "Just another string"
puts my_string.length
{% endcodeblock %}

<p>FYI: PHP variables always start with a dollar sign <code>$</code>, but Ruby doesn't have this requirement. Yet another keystroke saved. Yay! You also may have noticed that we also don't need to type the semi-colon <code>;</code> at the end of each line in Ruby. You can, but you don't have to, unless of course the above two lines are placed on the same line. In which case, the semi-colon will be needed to separate the two.</p>

<p>We could also write the above ruby code like this:</p>

{% codeblock ruby %}
puts "Just another string".length
{% endcodeblock %}

<h3>Chicken or Egg?</h3>

<p>One of the biggest frustrations for me when it comes to coding in PHP, is the need to memorise the order of arguments to the language's many global functions. I've been coding in PHP for over 10 years now, and I still have trouble remembering which argument comes first in a function call. Was it the chicken or was it the egg?</p>

<p>For example, let's take the <code>in_array</code> function:</p>

{% codeblock php %}
in_array($chicken, $egg);
{% endcodeblock %}

<p>And then lets compare that with the <code>array_push</code> function, which takes its arguments in the reverse order:</p>

{% codeblock php %}
array_push($egg, $chicken);
{% endcodeblock %}

<p>Most of PHP's array functions take an array as the first argument, but there are a few exceptions. Inconsistencies such as this can get very frustrating, and PHP is riddled with them. When you don't know any differently, you tend to overlook these. But ever since I started working with Ruby, these little annoyances actually become big annoyances.</p>

<p>But this is the nature of PHP and it's procedural programming design. Fortunately, Ruby solves this problem with object orientation. Lets look at Ruby's equivalents to <code>in_array</code> and <code>array_push</code>.</p>

<p>First we create an array and assign it to the <code>fruit</code> variable:</p>

{% codeblock ruby %}
fruit = ['apple', 'orange']
{% endcodeblock %}

<p>Then we check to see if <code>'banana'</code> is in the fruit array. This is the same as PHP's <code>in_array</code> function:</p>

{% codeblock ruby %}
fruit.include? 'banana'
{% endcodeblock %}

<p>So the above obviously returns <code>false</code>, as <code>'banana'</code> does not exist, or is not included in the <code>fruit</code> array. So lets push it in:</p>

{% codeblock ruby %}
fruit.push 'banana'
{% endcodeblock %}

<p>And now <code>fruit</code> equals <code>['apple', 'orange', 'banana']</code></p>

<p>In Ruby, an array is an object, so if we want to push a variable into the array, we simply take that array and just call <code>push</code>. It needs only one argument, since the method is attached to the object on which it will operate. And we now have no source of confusion.</p>

<p>Not only does this help with remembering arguments, it also helps to organize the Ruby code space. Instead of having many procedural functions in a global space like PHP, Ruby packages all its methods nice and neatly into the objects that actually need them.</p>

<p>Of course, there are many more reasons why objectifying everything can help you, but these are some of the most notable. But I hope you can see that Ruby's object-oriented nature actually makes life simpler.</p>

<p>In my next post where I explain reason #2 as to why Ruby is better than PHP, I will attempt to explain and show you one of the biggest differences, and the reason why developing plugins in Rails is so powerful.</p>

<p>Thanks for tuning in guys, and don't forget to leave your comments. I'd love to know your thoughts and opinions.</p>
