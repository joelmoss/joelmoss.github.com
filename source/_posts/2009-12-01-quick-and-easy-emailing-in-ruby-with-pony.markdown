--- 
layout: post
title: Quick and easy emailing in Ruby with Pony
categories: articles
---
<p>I needed to send an email to all the users of Codaset, and wanted a quick and easy way to do so. So I just wrote a quick Rake task that will loop through all the users in the Codaset database, and send each one an email. However, when I was looking at how to send the emails, there didn't seem to be an easy way to do so without having to write several lines of code just to send one email. What I needed was something similar to <a href="http://www.php.net/manual/en/function.mail.php">PHP's mail() function</a> which lets me send an email with one line of code:</p>

{% codeblock php %}
mail('you@example.com', 'My Subject', $message);
{% endcodeblock %}

<p>I don't need to use an SMTP server to send it, as it works just fine with sendmail.</p>

<p>Unfortunately, Ruby and Rails built in mail classes don't offer such simplicity, which is very rare. But then I found <a href="http://github.com/benprew/pony">Pony</a>, which is a Ruby gem that mimics PHP's mail function. Now I can can send an email in Ruby with one short line of code, and no configuration needed:</p>

{% codeblock ruby %}
Pony.mail(:to => 'you@example.com', :from => 'me@example.com', :subject => 'hi', :body => 'Hello there.')
{% endcodeblock %}

<p>Easy peasy!</p>

<p>For those of you who are interested, here is my rake task in its entirety:</p>

{% codeblock ruby %}
require "pony"
require "erb"

desc "Send an email to all users"
task :email_users => :environment do
  raise "No template provided. Please set TEMPLATE=file_name" if ENV['TEMPLATE'].blank?

  template  = File.read ENV['TEMPLATE']
  subject   = ENV['SUBJECT'] || "Hello from Codaset"
  
  if ENV['TEST']
    name = 'Joel Test'
    Pony.mail :to => 'joel@developwithstyle.com', :from => "Codaset <help@codaset.com>", :subject => subject, :body => ERB.new(template).result(binding)
    puts "Email test ('#{subject}') sent to joel@developwithstyle.com"
  else
    User.find_each do |user|
      unless user.email.blank?
        name = user.title
        Pony.mail :to => user.email, :from => "Codaset <help@codaset.com>", :subject => subject, :body => ERB.new(template).result(binding)
        puts "Email ('#{subject}') sent to #{user.email}"
      end
    end
  end
end
{% endcodeblock %}

<p>This simply loops through each user in the database, and sends them an email. The body of the email is built using a templated file, that uses ERB. Which means I can use it as a normal view template. I run it like this:</p>

{% codeblock ruby %}
rake email_users RAILS_ENV=production TEMPLATE=my_email_template.txt SUBJECT='Look at my email i sent ya!'
{% endcodeblock %}