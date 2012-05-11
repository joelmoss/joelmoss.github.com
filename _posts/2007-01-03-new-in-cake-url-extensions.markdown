--- 
layout: post
title: "New in Cake: URL Extensions"
categories: articles
---
Hi all and happy new year. Hope you all had a great Christmas.

I am hoping to increase my activity on this blog in the next year and post more tips and articles as I discover them. Let me start of with the first of a number of articles introducing whats new and changed in <a href="http://bakery.cakephp.org/articles/view/197">CakePHP 1.2</a>.

I have found URL Extensions to be extremely valuable when serving differing types of content in my Cake apps. They provide an extremely easy way to serve separate templates/views depending on what you want to see.

Usually when you call <em>http://MyCakeApp/controller/action</em> the actions view would be pulled from the <em>/app/views/controller/action.ctp</em> template file. (The .ctp extension is the new standard extension used for view templates in Cake.) Which is fine if all you ever want to do is serve the same type of content all day.

But what happens if you would like to display that same view in XML or RSS? I know there are other ways of doing this, but the use of URL Extensions is by far the easiest and quickest.

So all you would do is call <em>http://MyCakeApp/controller/action.xml</em>. And instead of <em>/app/views/controller/action.ctp</em> being rendered, it would look for your view template at <em>/app/views/controller/xml/action.ctp</em>.

If you want to do something different when the XML view is called, you can use

<pre><code>$this-&gt;params['url']['ext']
</code></pre>

The above will output the extension name. For example, if <em>http://MyCakeApp/controller/action.xml</em> were called, the above would equal "<em>xml</em>".

Hope that helps.
