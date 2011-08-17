--- 
layout: post
title: "10 Reasons why Ruby is better than PHP - Reason #2"
categories: articles
---
<p>Well now then. <a href="/articles/2009/05/20/10-reasons-why-ruby-is-better-than-php-reason-1.html">My last post</a>, or the comments in it, seemed to have stirred up a little hornets nest. I had my fair share of supporters and my fair share of thanks for my writings, but I also received a little criticism. I think I've covered most of those in the <a href="/articles/2009/05/20/10-reasons-why-ruby-is-better-than-php-reason-1.html#comments">comments</a> and also on <a href="http://twitter.com/joelmoss">Twitter</a>, so I won't say much more, other than to simply remind you all what I am trying to do.</p>

<p>In this little series of blog posts, my objective was to be as fair as possible when explaining my reasons why I think Ruby is better than PHP. But at the same time, this is not a comparison. Which means I won't be pointing out PHP's strong points - of which there are many. Also, this is my opinion, and no one elses, and I am entitled to that. And so to, are you guys.</p>

<p>And one last thing before I start reason #2. I want to say thanks to <a href="http://www.littlehart.net/atthekeyboard/2009/05/21/laziness-vs-efficiency/">Chris Hartjes for his blog post</a> earlier today. I made a comment on Twitter about lazy coders, being good coders, and he basically put me to rights, and explained what I was saying in much better terms, than I could ever do. But also, I do think he was a little harsh on me. Hear my other reasons first Chris. No hard feelings though.</p>

<p>Back to business. In todays post, I wanted to give more of a solid reason why I think Ruby excels over PHP. So I picked one that simply cannot be matched in any way by PHP. Add probably won't ever be. But I would love to see this being made possible.</p>

<h3>Re-opening in Classes is soooo Useful!</h3>

<p>Both languages support the creation of classes as part of their object-oriented design. And they do so in much the same way. Both languages allow you to set method visibility with the use of <code>public</code>, <code>protected</code> and <code>private</code> declarations, and behave accordingly. Classes are written in a similar fashion:</p>

{% codeblock php %}
class Person {
  public function greeting() {
    return 'Hello you!';
  }
}
{% endcodeblock %}

{% codeblock ruby %}
class Person
  def greeting
    'Hello you!'
  end
end
{% endcodeblock %}

<p>Very similar, but let me explain one thing. In the PHP example above, I returned the string "<code>Hello you!</code>" by prefixing it with the <code>return</code> keyword. Like this:</p>

{% codeblock php %}
return 'Hello you!';
{% endcodeblock %}

<p>But in the Ruby example, you may have noticed that there is no <code>return</code> keyword before the "<code>Hello you!</code>" string. It was just this:</p>

{% codeblock ruby %}
'Hello you!'
{% endcodeblock %}

<p>That works perfectly fine, and the "<code>Hello you!</code>" string will still be returned when calling the <code>greeting</code> method of the <code>Person</code> class. That is because Ruby will return the value from the last line of the method. You can use <code>return</code> if you want to, but you don't have to.</p>

<p>So we've determined that writing classes is pretty much on the par in both PHP and Ruby. But, you may have accidentally redeclared a class in PHP, and received a nasty error:</p>

{% codeblock php %}
class Person {
  public function greeting() {
    return 'Hello you!';
  }
}

class Person {
  public function greeting() {
    return 'Hey, hey, hey!';
  }
}
{% endcodeblock %}

<p>Doing the above will give tell you <code>PHP Fatal error: Cannot redeclare class Person</code>. Everyone knows that you just cannot do that with PHP. And to be honest it seems to make sense for it to prevent this from happening. But Ruby actually allows you to do this. In fact, you are almost encouraged to reopen classes if and when needed.</p>

{% codeblock ruby %}
class Person
  def greeting
    'Hello you!'
  end
end

class Person
  def greeting
    'Hey, hey, hey!'
  end
end
{% endcodeblock %}

<p>In the above case, no error will be returned. Instead, Ruby will simply redefine the <code>greeting</code> method in the first class, with the same method from the second class. So you get this:</p>

{% codeblock ruby %}
p = Person.new
puts p.greeting
{% endcodeblock %}

Which returns "<code>Hey, hey, hey!</code>" and not "<code>Hello you!</code>"

<p>Oh no, here it comes. I can hear the cries now: "But that's gonna cause untold problems and bugs in my code!". Not if you use it wisely! Part of Ruby's philosophy is to provide you with all the tools you need, then entrusting you to use that power with care. What was it Uncle Ben said to Peter? "With great power comes great responsibility."</p>

<p>This type of feature may seem a little dodgy, but in practice it becomes extremely useful. It means that I can reopen any class that I want, at any time, which often leads to more manageable code.</p>

<p>But I'm not just limited to reopening my own classes. I can even reopen Ruby's base classes. This is referred to as "Monkey patching", and is usually frowned upon, as it is not very wise to be overriding the core of the language. But if used carefully and sparingly, we are able to add a little extra functionality to our app by extending a base class or two.</p>

<p>When it comes to Rails, Ruby's base classes are extended quite a bit, especially within its ActiveSupport library, which reopens the String, Integer, and many other base classes. But it does so to add a lot of extra, and very useful functionality. It's done so with care and attention.</p>

<p>For example, I want to know if an integer is odd or even, but Ruby provides no such method for doing so, so I write my own. But instead of writing a standalone function within my class, I can reopen Ruby's Integer class like so:</p>

{% codeblock ruby %}
class Integer
  def odd?
    self % 2 == 1
  end
end
{% endcodeblock %}

and now I can call:

{% codeblock ruby %}
3.odd?
{% endcodeblock %}

<p>which would of course return true. All I am doing is reopening the Integer class, and adding a new method.</p>

<p>"But what's that question mark doing there? Is that part of the method name?" Actually, yes it is. In PHP, you can only use letters, number, and underscores in method and function names. But Ruby lets be a little more expressive, and use other characters such as <code>?</code>, <code>!</code>, and even <code>/</code>. So in the <code>odd</code> example above, I ended the method name with a question mark, because what I am doing is effectively asking a question of the number. "Are you an odd integer?". Which it replies with a true or false value. Neat hey?</p>

<p>One of the most powerful uses of reopening classes, is the plugin system available in Rails. We can use Rails plugins to extend and override nearly every part of Rails. Which is why there are thousands of Rails plugins. You can do pretty much anything you want.</p>

<p>So I hope I have provided a good, solid reason why Ruby is better than PHP, with a feature that simply cannot be achieved with PHP. It really is very powerful, that when used carefully, can save you a lot of time, and make coding with Ruby lots of fun. Which after all, that's why we're here isn't it?!</p>

<p>Next time, I think I'll talk about Blocks; yet another feature of Ruby that PHP cannot emulate.</p>
