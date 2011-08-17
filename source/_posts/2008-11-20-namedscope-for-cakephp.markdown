--- 
layout: post
title: NamedScope for CakePHP
categories: articles
---
<p>I discovered the joys of NamedScope for Ruby on Rails quite a while ago now, and have always been an admirer. Its makes performing finds on models very elegant and convenient, by automagically creating model methods based on your pased scope params. Just like this:</p>

{% codeblock ruby %}
class User < ActiveRecord::Base
  named_scope :active, :conditions => {:active => true}
  named_scope :inactive, :conditions => {:active => false}
end

# Standard usage
User.active    # same as User.find(:all, :conditions => {:active => true})
User.inactive # same as User.find(:all, :conditions => {:active => false})
{% endcodeblock %}

<p>Then a few months ago I read <a href="http://codetunes.com/2008/09/05/named-scope-in-cakephp/">this blog post</a> and discovered that someone had created similar functionality for CakePHP, in the form of a model behavior. Although it's not quite as powerful as it's Rails cousin, it does let you define named scopes for any model quite easily. However, I wasn't crazy about a few things.</p>

<p>Named Scopes are defined like this:</p>

{% codeblock php %}
class User extends AppModel {
  var $actsAs = array(
    'NamedScope' => array(
      'activated' => array('User.activated in not null'),
      'online' => array('date_add(User.last_activity, interval 5 minute) > now()')
    )
  );
}
{% endcodeblock %}

<p>The above format means we can only pass find conditions to a named scope, and cannot pass any other params, such as ORDER and FIELDS.</p>

<p>Then a named scope is then called like this:</p>

{% codeblock php %}
$this->User->find('all', array('scope' => 'activated'));
$this->User->find('all',
  array('conditions' => 'points > 10', 'scope' => array('activated', 'online')))
{% endcodeblock %}

<p>I have to pass enough params to a find call as it is, so I don't want anymore.</p>

<p>What I want to do is this:</p>

{% codeblock php %}
class User extends AppModel {
  var $actsAs = array(
    'NamedScope' => array(
      'active' => array(
        'conditions' => array(
          'User.is_active' => true
        ),
        'order' => 'User.name ASC'
      )
    )
  );
};
{% endcodeblock %}

<p>and this</p>

{% codeblock php %}
$active_users = $this->User->active('all');
{% endcodeblock %}

<p>I can even do this:</p>

{% codeblock php %}
$active_users = $this->User->active('all', array(
    'conditions' => array(
        'User.created' => '2008-01-01'
    ),
    'order' => 'User.name ASC'
));
{% endcodeblock %}

<p>Much improved I think, and so much more powerful. <a href="http://codaset.com/joelmoss/cakephp-named-scope">So I've only gone and coded the damn thing</a>! You can find my version of Named Scope for Cake on Codaset at <a href="http://codaset.com/joelmoss/cakephp-named-scope">http://codaset.com/joelmoss/cakephp-named-scope</a>.</p>

<p>And you know what? Thanks to the power of CakePHP, the actual code is seven lines shorter than the aforementioned version.</p>
