--- 
layout: post
title: HAML into PHAML?
categories: articles
---
I discovered <a href="http://haml.hamptoncatlin.com/">HAML</a> several months ago and instantly fell in love with it. I can just see how it would increase any developers productivity and speed up development time. Not to mention actually producing nice, clean and great looking XHTML markup.

This is your template:

<pre><code>!!!
%html{ :xmlns =&gt; "http://www.w3.org/1999/xhtml", :lang =&gt; "en", 'xml:lang' =&gt; "en" }
%head
%title BoBlog
%meta{ 'http-equiv' =&gt; 'Content-Type', :content =&gt; 'text/html; charset=utf-8' }/
= stylesheet_link_tag 'main'
%body
#header
%h1 BoBlog
%h2 Bob's Blog
#content
- @entries.each do |entry|
.entry
%h3.title= entry.title
%p.date= entry.posted.strftime("%A, %B %d, %Y")
%p.body= entry.body
#footer
%p
All content copyright</code></pre>
