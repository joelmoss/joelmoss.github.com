--- 
layout: post
title: Replicating Rails RJS in CakePHP
categories: articles
---
One of the things that I like so much about the Ruby on Rails framework are its RJS templates. I will let the Rails API tell you more:

<blockquote>Unlike conventional templates which are used to render the results of an action, these templates generate instructions on how to modify an already rendered page. This makes it easy to modify multiple elements on your page in one declarative Ajax response. Actions with these templates are called in the background with Ajax and make updates to the page where the request originated from.</blockquote>

So when you make an Ajax call, you can return pure javascript and use that to modify the page that you are on. For example, you could create an RJS template that simply hides an element on the page you are on.

Replicating RJS templates in <a href="http://cakephp.org">CakePHP</a> is surprisingly easy with the <a href="http://bakery.cakephp.org/articles/view/197">all new 1.2 version</a> of the rapid application development framework for PHP.

All you gotta do is add the following function in your AppController:

<pre><code>function beforeRender()
{
    if (isset($this-&gt;params['url']['ext']) &amp;&amp; $this-&gt;params['url']['ext'] == 'js')
    {
        $this-&gt;layout = false;
        header("Content-type: text/javascript");
    }
}
</code></pre>

What that does is take advantage of the new <a href="http://joelmoss.info/switchboard/blog/2125:New_in_Cake_URL_Extensions">URL Extensions</a> introduced in CakePHP 1.2. It looks to see if you are using a JS extension. If you are, it disables the layout and sets the pages Content-Type to "<em>text/javascript</em>".

Now when you call http://MyCakeApp/controller/action.js it will return your Javascript template from /app/views/controller/js/action.ctp. This view template should contain only javascript, but of course you can still use PHP and your Helpers in there. It will also only work if you are using the Ajax functionality of the <a href="http://prototype.conio.net/">Prototype javascript library</a>.

So the following could be the entire contents of your JS view:

<pre><code>
  new Effect.Highlight('');
  Field.activate('');

  $('loading-text').update('Login Successful.');
  window.location.href = '/';
</code></pre>

As you can see, you don't need to use any SCRIPT tags. Just place the javascript directly into it.

Works a treat and does exactly what Rails RJS templates do. Please do try it and play with it some more, as you won't really know its full potential until you do.
