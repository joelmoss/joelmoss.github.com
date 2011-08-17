--- 
layout: post
title: Concerned with Rails
categories: articles
---
<p><a href="http://codaset.com/joelmoss/rails-concerns">Concerns</a> is a simple Rails plugin that provides you with a simple way to organise your Controllers, Models and Mailers, and split them into smaller chunks of logic. It is especially useful when you have lengthly models, and get fed up with having to scroll through several hundred lines of code.</p>

<h3>How does it work?</h3>

<p>So let's say we have a Post model (doesn't everyone?!) which is getting a bit lengthy, and frankly not very nice to look at. With the Concerns plugin, we can split it up into nice little chunks. Because we have lots of validations, let's start by pulling them out and placing them within a concern file.</p>

<h3>Let's get going then...</h3>

<p>First of all, install the plugin:</p>

<div class="highlight"><pre>
script/plugin install git://codaset.com/joelmoss/rails-concerns.git
</pre></div>

<p>Then, create a new directory in your app/models drectory and call it "post", which is the same name as your model.</p>

<p>Within this new directory, create a new file at app/models/post/validations.rb. Now all this should do is reopen your Post model, and define your validations like this:</p>

{% codeblock ruby %}
class Post < ActiveRecord::Base
  validates_presence_of :title, :body
  validates_uniqueness_of :title, :scope => :project_id, :case_sensitive => false
  validates_exclusion_of :title, :in => %w(edit new blog delete destroy create update post posts)
  validates_inclusion_of :markup_language, :in => %w( markdown textile wikitext ), :allow_nil => true
end
{% endcodeblock %}

<p>It's just like writing your model again.</p>

<p>Now within your main Post model; right at the top, we simply call:</p>

{% codeblock ruby %}
concerned_with :validations
{% endcodeblock %}

<p>Multiple concerns can be called like so:</p>

{% codeblock ruby %}
concerned_with :validations, :class_methods
{% endcodeblock %}

<p>And we're done!</p>

<p>You can do this as many times as you wish, and with as many concerns as you want. And it works with models, controllers and mailers.
Need help?</p>

<p>Grab and/or fork the code from the <a href="http://codaset.com/joelmoss/rails-concerns">Codaset project</a></p>
