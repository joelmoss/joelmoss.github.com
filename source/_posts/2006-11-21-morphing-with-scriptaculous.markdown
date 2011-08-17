--- 
layout: post
title: Morphing with Scriptaculous
categories: articles
---
A new beta version of the Scriptaculous javascript effects library has just been released, and very nice it is too. Version 1.7 features a new effect called morphing, which allows for CSS style effects. Effectively allowing you to change an element based on CSS. But the element doesn't just change. it morphs!

Here's an example

{% codeblock %}
new Effect.Morph('error_message',{
    style:'border-width:3px; font-size:15pt; color:#f00'
});
{% endcodeblock %}

Just take a look at the <a href="http://mir.aculo.us/demos/script-aculo-us-1-7-beta-demos">morphing demo</a>, then read all the <a href="http://mir.aculo.us/2006/11/21/script-aculo-us-hits-1-7-beta">details</a>.
