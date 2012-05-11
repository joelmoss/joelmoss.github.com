---
layout: post
title: Tail your Logs with a Touch of Color
categories: articles
---

<p><a href="http://eric.lubow.org">Eric Lubow</a> (@elubow), a colleague of mine just released his first <a href="http://eric.lubow.org/2010/ruby/colortail-gem/">Ruby Gem</a> and published it on <a href="http://codaset.com/elubow/colortail">Codaset</a>, and I gotta say, it's a pretty damn useful one too.</p>

<p>ColorTail - or ColourTail if you want the correct english spelling - is a very easy way to give your log files a touch of color when you tail them. Tailing logs can be very useful, but can also be very confusing, and sometimes a touch mind blowing with all the data that some logs can spew out at you. So adding a bit of color, or underlining certain lines, or even flashing them would really help you identify the important bits of your log.</p>

<p>Just install ColorTail:</p>

<div class="highlight"><pre>
  <span class="x"># sudo gem install colortail</span>
</pre></div>

<p>Then create a file in your home directory called <code>.colortailrc</code>, and define your colortail config:</p>

{% codeblock lang:ruby %}
Groupings = {
  # This default matching scheme
  'default' => [
      { :match => /Completed in/,    :color => :red,     :attribute => :reverse },
      { :match => /EMERGENCY/,    :color => :red,     :attribute => :reverse },
      { :match => /FATAL/,        :color => :red,     :attribute => :bright },
      { :match => /CRITICAL/,     :color => :red },
      { :match => /DEBUG/,        :color => :green },
      { :match => /ERROR/,        :color => :green },
      { :match => /INFO/,         :color => :none },
      { :match => /WARN/,         :color => :yellow }
  ]
}
{% endcodeblock %}

<p>The above is the default, so will apply to all logs whenever you tail them with the colortail command, like so:</p>

<div class="highlight"><pre>
  <span class="x"># colortail -g log/development.log</span>
</pre></div>

<p>Which will give you this:</p>

<p><img src="/img/posts/colored_log_example.jpg" width="590" /></p>

<p><a href="http://codaset.com/elubow/colortail">Check out the project</a>, and enjoy!</p>