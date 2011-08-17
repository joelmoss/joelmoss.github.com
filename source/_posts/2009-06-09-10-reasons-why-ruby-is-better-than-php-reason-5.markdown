--- 
layout: post
title: "10 Reasons why Ruby is better than PHP - Reason #5"
categories: articles
---
<p>It's been a while I know, and I am aware that some of you are chomping at the bit to read reason #5. Apologies for the wait, but some of us have work to do, and a <a href="http://codaset.com">mammoth side project</a> to complete, which by the way, is coming along nicely.</p>

<p>Before I start on reason #5, I want to mention a couple of posts in a similar vein to my series.</p>

<p>Andy Jeffries "<a href="http://andyjeffries.co.uk/articles/4-reasons-why-ruby-syntax-is-better-than-phps-">4 Reasons why Ruby syntax is better than PHP's</a>" is a straight to the point article all about the strengths of Ruby's syntax over PHP. If after reading his post, you still think syntax doesn't matter, then you are a lost cause, and beyond help of any kind!</p>

<p>Another post I actually read a while ago, but forgot all about until I was <a href="http://twitter.com/m3nt0r/status/2091044381">pleasantly reminded of</a>, is Bitcetera's "<a href="http://www.bitcetera.com/en/techblog/2009/04/07/10-reasons-why-php-is-still-better-than-ruby-/">10 Reasons why PHP is still better than Ruby</a>". Read it carefully all the way through, as it is a great read.</p>

<p>Now, we get to Modules in Ruby, again, a feature that has no direct equivalent in PHP. Modules are very similar to classes, in fact they are written in much the same way:</p>

{% codeblock ruby %}
module Animal
  def name
    "Dog"
  end
end
{% endcodeblock %}

<p>So what are they used for? Well, modules are generally used for two purposes; creating namespaces and mixins. I'm sure (and I hope) that you all know what namespaces are. But you probably have no idea what a mixin is. Well I'll get to that in a bit. Let's quickly talk about how Ruby uses namespaces.</p>

<p>Let us imagine that we have been charged with cleaning up and re-organizing our code, and we have a lot of it. Normally in PHP you might simply stick this code in a file and include it wherever you need it, but what if you have two methods or constants that are named the same? Some developers have worked around this by separating different class package names with underscores. This solution solves the immediate problem and also works conveniently with autoloading in PHP. It can, however, leave us with some really long class names.</p>

<p>Let's imagine we have two classes that define a <code>Document</code> class. In PHP we would probably prefix each class name with the document type:</p>

{% codeblock php %}
class XML_Document {
  public function __construct() {
    print "new xml document\n";
  }
}
class PDF_Document {
  public function __construct() {
    print "new pdf document\n";
  }
}
$xml = new XML_Document; 
$pdf = new PDF_Document;
{% endcodeblock %}

<p>Ruby would achieve the same thing like this:</p>

{% codeblock ruby %}
module XML 
  class Document 
    def initialize 
      puts 'new xml document' 
    end 
  end 
end 
module PDF 
  class Document 
    def initialize 
      puts 'new pdf document' 
    end 
  end 
end 
xml = XML::Document.new 
pdf = PDF::Document.new
{% endcodeblock %}

<p>Now I know that the as-yet-to-be-released PHP 5.3 will introduce namespaces, but come on! <a href="http://php.net/manual/language.namespaces.rationale.php">Have you actually seen how PHP namespaces are created and written?!</a> WTF!? Using slashes just looks wrong! Slashes are used in directory paths, and that is where they should stay. And why should I have to declare my namespace at the very top of the file and no where else?</p>

<p>But the best thing about Ruby's modules, is the ability to mix them into my classes, as if it was part of the original class code. Think of it as inheritance, but better. Everyone knows that in PHP and Ruby, a class can only inherit from one class at a time. To inherit from another class would involve you having to create a complicated chain of inheritance. Mixins eliminate that need. Just create a class, inherit from another class, and then mixin as many modules as you want.</p>

{% codeblock ruby %}
module Movement 
  def run 
    puts "I'm running!" 
  end 
  def walk 
    puts "I'm walking a bit briskly!" 
  end 
  def crawl 
    puts "I'm so slowwww!" 
  end 
end

class Man 
  include Movement 
  def jump 
    puts "I'm bipedal and I can jump like a fool!" 
  end 
end

class Sloth 
  include Movement 
  def flop 
    puts "It's all a lie...all I can do is flop around." 
  end 
end

mister_man = Man.new 
mister_man.run 
?  I'm running!

mister_slothy = Sloth.new 
mister_slothy.flop 
?  It's all a lie...all I can do is flop around.
{% endcodeblock %}

<p>As you can see, this mechanism is very similar to inheritance in that you can use all of the mixin's code.  To use a mixin, simply define a module and then use the include keyword followed by the module's name (note I said module; the include keyword has nothing to do with files or libraries like in PHP); from then on the class has access to all of that module's constants and methods.</p>

<p>The above example really doesn't do mixins justice, but it's a very simple example to help demonstrate how they work. Modules are a very versatile tool in Ruby and allow us to extract and share common behavior in objects, and are another reason why Ruby is better than PHP (in my opinion).</p>
