--- 
layout: post
title: Enhanced Controller Callbacks for CakePHP
categories: articles
---
<p>I had this idea a while ago, and actually implemented it into a Cake project, but it was a bit hacky and required hacking the core. So I didn't like it. But today, I had a need for this same functionality, so I had a little think about how I could implement it without hacking the core, and thus was born the <a href="http://codaset.com/joelmoss/cakephp-callbacks">Callbacks plugin</a> for CakePHP.</p>

<p>If any of you have ever used Ruby on Rails, you should be familiar with its callback system. Well, it was this system that I needed.  I just started fleshing out a new Cake app, and needed to run a <em>beforeFilter</em> callback on a couple of specific controller actions. Of course, I could do this:</p>

{% codeblock php %}
class MyController extends AppController {
    function beforeFilter() {
        if ($this->params['action'] == 'index' || $this->params['action'] == 'view') {
            # do something here that only the 'index' and 'view' actions need
        }
    }
}
{% endcodeblock %}

<p>But that's just not very elegant, and will get pretty messy the more you do it. So I came up with the Callback plugin, which is basically a simple component that provides some sweetly fine grained control over your callbacks. So now I can do this instead:</p>

{% codeblock php %}
  class MyController extends AppController {
      var $beforeFilter = array('myCallback');

      function _myCallback() {
          # do something here
      }
  }
{% endcodeblock %}

<p>and I can even call several callbacks, each with their own methods:</p>

{% codeblock php %}
  class MyController extends AppController {
      var $beforeFilter = array('myCallback', 'anotherCallback', 'andAnotherOne');

      function _myCallback() {
          # do something here
      }

      function _anotherCallback() {
          # do something here
      }

      function _andAnotherOne() {
          # do something here
      }
{% endcodeblock %}

<p>Now the above is lovely and all, but it doesn't really provide any extra functionality above what Cake already provides. So far, my code just looks cleaner. What I really want to do is only run the <em>anotherCallback</em> when calling the <em>index</em> action. So I change the $beforeFilter param:</p>

{% codeblock php %}
  class MyController extends AppController {
      var $beforeFilter = array(
          'myCallback',
          'anotherCallback' => array(
              'only' => 'index'
          )
          'andAnotherOne'
      );
{% endcodeblock %}

<p>Much better! I can also specify to run a callback on all actions, except the 'delete' action:</p>

{% codeblock php %}
  class MyController extends AppController {
      var $beforeFilter = array(
          'anotherCallback' => array(
              'except' => 'delete'
          )
      );
{% endcodeblock %}

<p>Even better! But still I wanted more!</p>

<p>I wanted to be able to add even more control, and only run a callback if a certain condition is/not met:</p>

{% codeblock php %}
  class MyController extends AppController {
      var $beforeFilter = array(
          'anotherCallback' => array(
              'if' => 'ifTrue'
          )
      );

      function _ifTrue() {
          # do something here and return true for the callback to run
          return true;
      }
{% endcodeblock %}

<p>So the <em>anotherCallback</em> callback will now only run if the <em>_ifTrue</em> method returns true. Lovely!</p>

<p>Right now it supports the three main controller callbacks: beforeFilter, beforeRender and afterFilter. The plan is to provide the same functionality to Models.</p>

<p>You can checkout the code from Codaset repo at <a href="http://codaset.com/joelmoss/cakephp-callbacks">http://codaset.com/joelmoss/cakephp-callbacks</a>. Feel free to fork away!</p>
