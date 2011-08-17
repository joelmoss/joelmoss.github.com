--- 
layout: post
title: "10 Reasons why Ruby is better than PHP - Reason #3"
categories: articles
---
<p>So onwards and upwards! It appears that I still have a little work to do to convince you non-believers, so lets try again...</p>

<p>As <a href="http://developingwithstyle.com/articles/2009/05/21/10-reasons-why-ruby-is-better-than-php-reason-2.html">previously mentioned</a>, Ruby has some features that simply cannot be found in many other languages, let alone PHP. So here I introduce yet another one, and this is a biggie. But, please be warned that this one is a little harder to explain, so please be bear with me as I attempt to enlighten you.</p>

<p>Some of you may have heard of a language feature known in computer science as <em>closures</em>. If you have done any Javascript development, you should be familiar with closures, but may not know them by name. Ruby uses closures extensively, but refers to them simply as <em>blocks</em>. Which is actually easier to understand.</p>

<p>Many developers seem to think that blocks are somewhat of an obscure language feature, as they are pretty hard to find an equivalent in other languages. PHP is not the only language without support for blocks, but you should understand them, as they can be very useful, and quite powerful.</p>

<p>Although there is no direct translation of blocks in PHP, we can make some analogies to PHP that will help us understand and become familiar with blocks, and how they are useful. Lets use PHP to start a family:</p>

{% codeblock php %}
function start_family($num) {
  echo "There are now $num kids in my family"
}
{% endcodeblock %}

{% codeblock php %}
for ($kids = 99; $kids &gt; 0; $kids--) {
  start_family($kids);
}
{% endcodeblock %}

<p>When the above code is executed, PHP evaluates the condition in the for loop, which calls the <code>start_family</code> function on each iteration.</p>

<p>The <code>for</code> and <code>function</code> keywords are built-in constructs of PHP, in the same way that semi-colons and curly braces are built-in. But there are very few control constructs in PHP that allow code to be attached to them within the curly braces. It's not actually possible to add or create new control constructs in PHP, unless of course you fancy whipping up a PHP extension in C. (eurghh!)</p>

<p>To be fair, we could condense the above into the following, as there really would be no need to use a function within the for loop.</p>

{% codeblock php %}
for ($num = 99; $num &gt; 0; $num--) {
  echo "There are now $num kids in my family"
}
{% endcodeblock %}

<p>So now lets do the same thing in Ruby:</p>

{% codeblock ruby %}
99.downto(1) { |num| puts "There are now #{$num} kids in my family" }
{% endcodeblock %}

<p>Slightly unfamilar syntax, but that's nothing new when comparing Ruby with PHP. But the above is actually quite declarative. Lets break this down a little.</p>

<p>Hopefully, if you read <a href="http://developingwithstyle.com/articles/2009/05/20/10-reasons-why-ruby-is-better-than-php-reason-1.html">reason #1</a> you will now know that <code>99</code> is an object, which has a method called <code>downto</code>. It's pretty obvious that this method simply counts down from 99 to 1, and iterates through each number. It serves roughly the same purpose as the <code>for</code> construct in our PHP example. The odd looking bit between the curly braces, with the goalposts, is the block.</p>

<p>There are many similarities between the Ruby block and the PHP <code>for</code> loop. This is because the Ruby block is actually just a function in another form. A block is a function without a name, or an anonymous function. Yes I know PHP 5.3 will include some sort of support for anonymous functions, but again, it's an afterthought.</p>

<p>A Ruby block can receive parameters in much the same way a method or PHP function can, but they are placed within the goalposts of the block. In our case, we place the number (<code>num</code>) of kids between the goal posts, and this becomes our one and only parameter. We can pass more parameters to the block, by simply separating them with a comma. If we don't want to pass any parameters, then we leave off the goalposts completely. The rest of the block is executable code, just like any other Ruby method.</p>

<p>Every method in Ruby, whether it be a built-in one, or one that you create, can be passed a block. And that one simple fact is what makes blocks so powerful. In fact, if the <code>downto</code> method were written in pure ruby, it could look something like this:</p>

{% codeblock ruby %}
class Integer
  def downto(value, &block)
    n = self
    while n >= value
      block.call n
      n -= 1
    end
    return self
  end
end
{% endcodeblock %}

<p>So we <a href="http://developingwithstyle.com/articles/2009/05/21/10-reasons-why-ruby-is-better-than-php-reason-2.html">reopen</a> the <code>Integer</code> class, and redeclare the <code>downto</code> method. We then pass two parameters to that method. Pay particular attention to the second parameter: <code>&block</code>, as it is very important.</p>

<p>When a block is passed to a Ruby method, it can be captured in a variable. In fact, the code that we pass within the block to <code>downto</code> is converted into an object, and then stored inside a variable. The ampersand <code>&block</code> tells Ruby to store this block in a variable called <code>block</code>. The keyword <code>self</code> in this example refers to the object itself, which in this case is the integer <code>99</code>.</p>

<p>Still with me? Good! Lets take our earlier example again, and apply it to the <code>downto</code> method that we just created:</p>

{% codeblock ruby %}
99.downto(1) do |num|
  puts "There are now #{$num} kids in my family"
end
{% endcodeblock %}

<p>Hold a second, the above code is different to our first example isn't it? Yes it is, well spotted! Just as in everything in Ruby, you don't need the curly braces. The use of the <code>do</code> keyword is usually used for larger blocks, that need to span multiple lines. But it does exactly the same thing.</p>

<p>When the <code>downto</code> method is called, it receives two parameters: <code>value</code> contains the number of kids we have, and <code>block</code> contains the block of code that will be run on each iteration.</p>

<p>The inside of our <code>downto</code> method should look familiar to you, as it is effectively doing the same thing as our PHP <code>for</code> loop. It just counts down from 99 to 1, using a <code>while</code> loop. Then on each iteration of the <code>while</code> loop, it yields control to the code that is passed in the <code>block</code> variable, by calling the <code>block.call</code> method. Any parameters passed to <code>block.call</code>, are passed in the same way to the goalposts in the block.</p>

<p>A little confusing I know, but I really wanted to explain how blocks work as well as I could, as they are becoming ever more useful to me, the more that I develop with Ruby.</p>

<p>To finish off, I really want to show you an awesome way that Ruby's blocks are used. I won't go into it too much though, as it leads on to another of my reasons. There is a Ruby library (Gem) called <em><a href="http://www.thoughtbot.com/projects/shoulda/">Shoulda</a></em> which improves the <em>Test:Unit</em> unit testing library that is supported as standard in Ruby on Rails. Shoulda improves the language of your unit tests, and turns them into an almost human readable form. So here we have a test:</p>

{% codeblock ruby %}
context "a User instance" do
  should "return its full name"
    assert_equal 'John Doe', user.full_name
  end
end
{% endcodeblock %}

<p>Now start from the beginning of that code and just read it out load. It may end up something like this "<em>a User instance should return its full name</em>". Of course there is more in between, but what I am trying to convey is how expressive and readable the above code is. And that is because of the power of blocks.</p>

<p>Hope that helps a little. Keep the comments coming guys, and thanks for reading.</p>
