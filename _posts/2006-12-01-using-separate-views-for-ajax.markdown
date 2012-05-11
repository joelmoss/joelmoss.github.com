--- 
layout: post
title: Using separate views for ajax
categories: articles
---
In my current project I needed to have separate views when an action is called via ajax. Even though Cake supports a separate layout for ajax calls by prepending ajax onto your URL's, this not what I wanted. As each action needed its own view file due to the use of JSON in the app.

So I simply added the following method into my app_controller:

<pre><code>function beforeRender()
{
    if ($this-&gt;RequestHandler-&gt;isAjax())
    {
        $this-&gt;viewPath = $this-&gt;viewPath.'/ajax'; // change the view directory
        # $this-&gt;ext = '.jhtml'; // or change the extension
    }
}
</code></pre>

So now when an action is called by an ajax script, Cake sees this and changes the view path, and calls the following view <em>app/views/controller/ajax/action.thtml</em>.

Alternatively you can have the extension of your view files changed. So all ajax calls would call views ending in .jhtml for example. Your choice!

So now my ajax views are separated from my normal views.
