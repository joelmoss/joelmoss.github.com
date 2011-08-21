---
layout: post
title: Trigger Javascript Events after Binding with jQuery
categories: articles
---

<p>I use jQuery - a lot! In fact, I wonder how I ever lived my developer life without it. And even though I've used for a good few years now, I am still learning. Not just it's API, but simple things like best practises. Here is a simple tip, that I seem to have overlooked in the past.</p>

<!--more-->

<p>When binding an event on an element; for example if I want to trigger some sort of action when the user makes a change to a select element in a form, I would use this piece of code:</p>

{% codeblock javascript %}
  $(function(){
    $('#mySelect').change(function(){
      // do something here that is really cool, and it will occur
      // each time a user changes the value of 'myLink' which is a
      // select form element
    });
  });
{% endcodeblock %}

<p>But sometimes, I also need to trigger that change event on page load. As the user may be editing the data in the form, and I need to be sure that what the user sees on the page reflects the form value of the select element.</p>

<p>Previously, I did this:</p>

{% codeblock javascript %}
  $(function(){
    function mySelectFunction(){
      // do something here that is really cool, and it will occur
      // each time a user changes the value of 'myLink' which is a
      // select form element
    }
    
    $('#mySelect').change(mySelectFunction);
    
    mySelectFunction();
  });
{% endcodeblock %}

<p>So I define a function that performs the action that should take place when user changes the select element, then I pass that function to the jQuery <code>change</code> event. But then I also call the function on it's own, so that it is called on page load.</p>

<p>Yes I know!! It's pretty damn obvious, and to be honest a pretty big oversight on my part. What I should have been doing from the start, and what I now do all the time, is this:</p>

{% codeblock javascript %}
  $(function(){
    $('#mySelect').change(function(){
      // do something here that is really cool, and it will occur
      // each time a user changes the value of 'myLink' which is a
      // select form element
    }).change();
  });
{% endcodeblock %}

<p>See what I did there? I simply added a few characters; <code>.change()</code> to the jQuery chain. But that extra call to the <code>change()</code> event, will trigger the event that I bound earlier in the chain.</p>

<p>So all I am doing is binding the event to my desired action, then triggering it. Luurrvely!</p>