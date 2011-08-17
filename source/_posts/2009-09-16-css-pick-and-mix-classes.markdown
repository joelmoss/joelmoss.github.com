--- 
layout: post
title: CSS Pick and Mix Classes
categories: articles
---
<p>
  I was just browsing through my tweets and came across this little gem as put forward my Nate Abele; he of CakePHP lead developer fame...
</p>

<p><a href="http://twitter.com/nateabele/statuses/4031886580"><img src="http://twictur.es/i/4031886580.gif" /></a></p>

<p>
  It got me thinking about how I organise my CSS files and code, and as I have been writing a lot of CSS recently when developing <a href="http://codaset.com">Codaset</a>, it made me realise that I have developed a bit of a habit with my own CSS. So I thought I'd share it all with you.
</p>

<p>
  Over the last year or so, there seems to have been an explosion of CSS frameworks. I suppose it was inevitable really, as it happened with Javascript, so why not CSS. ANd to be honest, I would say that is a good thing, and there are some decent ones out there. But my CSS framework of choice is the excellent <a href="http://www.blueprintcss.org/">Blueprint framework</a>. It's a great starting point for all your CSS, and sets some good reset points. It's also very lite-weight.
</p>

<p>Before I continue, I just want to say that I will not be telling you how to use Blueprint or indeed, how to write CSS. I use Blueprint's grid classes, but again, I won't be talking about them. This post is more about how I use a class based system for my CSS.</p>

<p>
  First, if I don't already have one, I create a <code>css</code> directory within my public root, the place Blueprint's three CSS base files within a sub-directory. I usually call that <code>blueprint</code>. (surprise, surprise). Then I create two files within my <code>css</code> directory called <code>base.css</code> and <code>site.css</code>.
</p>

<p>I've used this structure for this site:</p>

<p><img src="/img/wpuploads/2009/09/one.png" /></p>

<p>
  Pretty obvious so far! Now let me explain what I do with the <code>base.css</code> and <code>site.css</code> file.
</p>

<h3><code>base.css</code></h3>
<p>
  Blueprint has a great set of resets or default styles, but sometimes, I want to overwrite these. I also find myself writing my own default styles, so I put all these within the <code>base.css</code> file. A simple rule of thumb is that only classes are allowed in the <code>base.css</code> file.
</p>
<p>
  Since I started using Blueprint, I've started using it's default classes a lot. Classes such as <code>.quiet</code> and <code>.small</code> make it very obvious what I am doing to a particular element. So if I want told make a line of text a little smaller, I can simply wrap the text with a <code>div</code> or a <code>span</code>, and give that <code>div</code> or a <code>span</code> a class of <code>small</code>:
</p>

{% codeblock html %}
<div class="small">
  Here is some text I made a little smaller than the rest.
</div>
{% endcodeblock %}

<p>If I wanted it to be colored a little lighter too, then I can add another class to the <code>div</code>:</p>

{% codeblock html %}
<div class="small quiet">
  Here is some text I made a little smaller than the rest, and it's quieter.
</div>
{% endcodeblock %}

<p>
  Both those classes and more are all ready to go as part of Blueprint. But I know also want to make this text bold. So I could either give this <code>div</code> an <code>id</code> and create a CSS rule for that new ID like this:
</p>

{% codeblock css %}
#myNewDiv {
  font-weight: bold;
}
{% endcodeblock %}

{% codeblock html %}
<div class="small quiet" id="myNewDiv">
  Here is some text I made a little smaller than the rest, and it's quieter and now bolded.
</div>
{% endcodeblock %}

<p>But that's a bit daft, as I am likely to want to make other elements bold. So a new class would be better:</p>

{% codeblock css %}
.bold {
  font-weight: bold;
}
{% endcodeblock %}

{% codeblock html %}
<div class="small quiet bold">
  Here is some text I made a little smaller than the rest, and it's quieter and now bolded.
</div>
{% endcodeblock %}

<p>Now I could easily have given this <code>div</code> an ID instead and done away with all the classes completely. But again, that isn't reusable. Another thing I like about the above, is that is very readable and obvious what the classes are doing. It's very expressive, and even makes it very easy and fast to style, as all I need to do is assign a few classes, rather than creating any new CSS styles. It's like a pick and mix for CSS!</p>

<p>So I'm now finding that my HTML is full of classes, and I'm seeing less and less ID's. I only tend to use an ID to style an element if that element is more complex, or has specific needs that are not used elsewhere.</p>

<h3>site.css</h3>
<p>So the <code>site.css</code> file is therefore used for element specific styling. So any CSS styles that are defined with an ID, are placed in this file. Not much more to say about that actually.</p>

<p>For more about how it all fits in, check out the source and CSS of this site and of <a href="http://codaset.com"></a>. I would love to know your thoughts and feedback on this. Comment away...</p>
