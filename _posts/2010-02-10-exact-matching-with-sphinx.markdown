---
layout: post
title: Exact Matching with Sphinx
categories: articles
---

<p>
  So I've been working with <a href="http://sphinxsearch.com">Sphinx</a> a lot over the last few months for several different projects, including <a href="http://codaset.com">Codaset</a>. It's an amazing piece of software, and solves the myriad of problems when trying to implement any kind of full text or intensive searches.
</p>

<p>
  But, it's still not had a final release yet, as we are at 0.9.9. Which means that there may be some things missing or incomplete from the API. One thing I was missing was a way to find or add weight to exact matches. I can do phrase matching by enclosing the search string in quotes. But that returns all docs which include any or all of that phrase, which is fine, as I want to see all of them. But what I want to do is make sure that the exact matches are listed first, or are given increased weighting. And right now, that is not the case.
</p>

<p>
  So I had a think, and came up with the idea of including a new <code>SELECT</code> item in my Sphinx index. So we have something like this:
</p>

{% codeblock lang:sql %}
SELECT CONCAT('__START__ ', my_field, ' __END__') AS exact_matched_field FROM table;
{% endcodeblock %}

<p>
  And now I can run the following Sphinx search, which will match my full and exact search string:
</p>

<div class="highlight"><pre>
  <span class="x">@exact_matched_field "__START__ my value __END__"</span>
</pre></div>