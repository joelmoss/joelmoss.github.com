---
layout: post
title: "The Right Way to Create an API"
categories: articles
---

I know, I know, it's been tooooo long. But whatever!

At [Shermans](http:///www.shermanstravel.com) we have begun a large project to rebuild the architecture around the travel deals system. And guess what? we chose to do it all in Ruby! Yay!

The deals server (as we are calling the entire system) will consist of a few separate apps, mostly Rails. A few of these apps will be REST based web API's, allowing our partners and publishers to fetch deals. Surprisingly, there are very few Ruby Gems available to help with creating an API. But that probably has more to do with the great support for exposing resources built in to Rails using `respond_with` and co.

But based on my experience building the [Codaset](http://codaset.com) [API](http://api.codaset.com), I knew I wanted a better way to expose the "views" for the API. For example, I don't want all attributes of my model to be exposed, and Rails doesn't provide a simple way to do that. Enter [RABL](https://github.com/nesquena/rabl)!

RABL bills itself as an API templating language, but all it really is, is a way to expose and define your API attributes from within the view itself, which is exactly the way it should be done, as it is only the view that has any concern with this. Exposing or defining the attributes for the API is not the responsibility of the model or even the controller.

Let's say our controller assigns the `@posts` instance variable, which is thusly available in our view, and our view looks like this:

{% codeblock lang:ruby %}
collection @posts
attributes :id, :title, :price
child(:user) { attributes :full_name }
node(:read) { |post| post.read_by?(@user) }
{% endcodeblock %}

Which would look like this as JSON:

{% codeblock lang:javascript %}
[{  post :
  {
    id : 5, title: "...", subject: "...",
    user : { full_name : "..." },
    read : true
  }
}]
{% endcodeblock %}

This means you don't have to dirty your controller with code that should be in your view.