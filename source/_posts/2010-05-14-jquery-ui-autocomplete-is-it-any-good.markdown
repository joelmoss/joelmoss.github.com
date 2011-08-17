---
layout: post
title: "jQuery UI Autocomplete and Caching Query Results"
categories: articles
---

<p>I've never managed to find a really good jQuery based autocomplete plugins, especially one that is flexible and easily extensible. So when the jQuery UI team <a href="http://blog.jqueryui.com/2010/03/jquery-ui-18/">released 1.8</a> back in March, I was intrigued to find that they included - amongst other new widgets - an <a href="http://jqueryui.com/demos/autocomplete/">autocomplete widget</a>. And it turns out to be pretty damn good, and flexible to boot.</p>

<p>So when I had a need to add the ability for a local data source for the autocomplete plugin that we use on <a href="http://quicksearch.shermanstravel.com">ShermansTravel QuickSearch</a>, I gave the new jQuery UI widget a go.</p>

<p>The jQuery UI Autocomplete widget can load in data in three ways... (examples taken straight from the jQuery UI docs)</p>

<h5>In an array with local data:</h5>
<p>Pass it an array with a list of strings, and it will use present a list of matching values based on your entered string.</p>

{% codeblock javascript %}
$(function() {
	$("#tags").autocomplete({
		source: ["php", "javascript", "asp", "ruby", "python", "c", "scala", "groovy", "haskell", "perl"]
	});
});
{% endcodeblock %}

<h5>A string, specifying a URL to get the data:</h5>
<p>Pass it a string of a relative URL, and it will make an ajax call to that URL, passing it the users entered string.</p>

{% codeblock javascript %}
$(function() {
	$("#birds").autocomplete({
		source: "search.php",
		minLength: 3
	});
});
{% endcodeblock %}

<h5>Via a callback (function):</h5>
<p>Pass it a callback and you can do pretty much anything you want. This example uses such a technique and caches the query results.</p>

{% codeblock javascript %}
var cache = {};
$("#birds").autocomplete({
	source: function(request, response) {
		if (cache.term == request.term && cache.content) {
			response(cache.content);
			return;
		}
		if (new RegExp(cache.term).test(request.term) && cache.content && cache.content.length < 13) {
			response($.ui.autocomplete.filter(cache.content, request.term));
			return;
		}
		$.ajax({
			url: "search.php",
			dataType: "json",
			data: request,
			success: function(data) {
				cache.term = request.term;
				cache.content = data;
				response(data);
			}
		});
	},
	minLength: 2
});
{% endcodeblock %}

<h4>A Caching Autocomplete for Remote Data</h4>

<p>What I really needed was a way to cache every single query when loading data in via an ajax call. The Autocomplete widget does not cache your returned query data at all, which means that an ajax call is made on every single key press. Even if you set the <code>minLength</code> to something like <code>3</code> - which will only trigger the autocomplete once the user has entered at least 3 characters - every character entered after that will trigger an ajax call.</p>

<p>So I came up with a somewhat simple, but effective caching strategy using the callback method for loading data.</p>

{% codeblock javascript %}
var cache = {};
$("#birds").autocomplete({
	source: function(request, response) {
	  var term          = request.term.toLowerCase(),
	      element       = this.element,
	      cache         = this.element.data('autocompleteCache') || {},
	      foundInCache  = false;

	  $.each(cache, function(key, data){
	    if (term.indexOf(key) === 0 && data.length > 0) {
	      response(data);
	      foundInCache = true;
	      return;
	    }
	  });

		if (foundInCache) return;
		
		$.ajax({
			url: 'search.php',
			dataType: "json",
			data: request,
			success: function(data) {
				cache[term] = data;
				element.data('autocompleteCache', cache);
				response(data);
			}
		});
	},
	minLength: 2
});
{% endcodeblock %}

<p>Here we are saving the cache as a hash in the corresponding element using jQuery's data function. And we are doing this for every query performed. We first loop through each element of the cache, and check if any of the keys begin with the current search term. If we find something, then we call the passed <code>response</code> callback function, and return from the <code>each</code> loop.</p>

<p>If no cache is found for the current term, then we call the ajax as usual. But if we do find a matching key in the cache, then we don't call the ajax, and instead return the cached data.</p>

<p>Simple, but works nicely.</p>