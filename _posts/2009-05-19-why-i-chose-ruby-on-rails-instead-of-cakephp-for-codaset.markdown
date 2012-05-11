--- 
layout: post
title: Why I chose Ruby on Rails instead of CakePHP for Codaset
categories: articles
---
<p>So <a href="http://codaset.com">Codaset</a> is being written in Ruby on Rails and not CakePHP. A bold decision I think, but a decision backed up by years of sitting on the fence when it came to Ruby and Rails, but also a little controversial, since I have been working with PHP and Cake for a long time now. So I wanted to lay out my reasons for going with Rails for the development of Codaset.</p>

<p>CakePHP is and probably always will be, the best PHP framework out there. I like to think that it has its head screwed on. Of course, that is all about the heads of the core team leading it, but as long as they stay focused on what Cake is there for, then it should stay like that. I continue to use Cake extensively with my day job at <a href="http://shermanstravel.com">ShermansTravel</a>, and will do so for while to come. But, ever since I discovered Ruby on Rails a few years ago, I've been constantly teased by it's power - due largely in part by the Ruby language it is written in. A power that PHP simply does not have, and probably never will. Cake is severely limited by PHP, and makes the most of a language that is probably a little inadaquet at times. Unfortunately PHP has bad design decisions written all over it.</p>

<p>In fact, there is not a day goes by, that PHP does not frustrate me with its design. A task completed in PHP, is - most of the time - completed so much more elegantly if done in Ruby. Ruby is just so damn expressive, and actually, very, very natural. PHP is not! I mean, why the hell should I have to write curly braces around every single expression, or wrap things in parenthesis? In Ruby, parentheses are optional in method calls, except to clarify which parameters go to which method calls.</p>

<p>This is PHP:</p>

{% codeblock php %}
class Parrot {
  public function say($word) {
    // say it here
  }
}
{% endcodeblock %}

<p>And this is Ruby:</p>

{% codeblock ruby %}
class Parrot
  def say(word)
    # say it here
  end
end
{% endcodeblock %}

<p>Now isn't that so much nicer?</p>

<p>Yes, I know that's all about aesthetics, but I like my code to look good. It makes looking at it and working with it, much more pleasant. But also this is just one of the hundreds of reasons why I chose Ruby and Rails. I suppose you could name this post "Why I chose Rails instead of Cake: <strong>Reason #1</strong>".</p>

<p>The bottom line, is that I have played around with Rails for years now, but never took the plunge and wrote an entire - completed - application with it. I started a few times, but then went back to using Cake. But this was because I didn't know Ruby well enough, and because of that, it was taking a long time to do something that I could have done much quicker in PHP. But because of all that tinkering, I can confidently say that I now know the basics of Ruby and can quite easily write a Ruby script, or a full Rails app.</p>

<p>So writing Codaset in Rails was the right decision. Every time I open it up in Textmate, I'm excited by what I see. Everytime I see another Rails plugin or Ruby gem, I want to install it. The thought of developing the next feature of Codaset exites me in ways that PHP almost never has. And because of all that, I'm learning a new programming language at an incredible rate. Once you get past the learning curve, you really start zooming through any app.</p>

<p>I'm even considering open sourcing Codaset! I want the world to see what I've done, and how I did it.</p>

<p>Lovin' it!</p>
