--- 
layout: post
title: Cake's global CSS, Javascript and images
categories: articles
---
Just perusing through cake's webroot, I noticed a PHP file in the <em>js</em> directory called <em>vendors.php</em>. It seems its idea is to allow you to keep a global repository of javascript files in cake's main vendors directory. This is a great idea for those of us who develop multiple apps with one cake install.

So I had a little think and realised I could do the same thing with my CSS files and images. So I set to work modifying this vendors.php file. So now if I want to include a link to a global javascript file located in cake's <em>vendors</em> directory, I simply do this in my view:

{% codeblock %}
$javascript->link('vendors/myjs');
{% endcodeblock %}

Adding <em>vendors/</em> before the filename simply tells the javascript helper that it should look in the global vendors directory for the file. Of course it works normally if <em>vendors/</em> is not prepended and includes files from your webroot.

I can do the same thing with CSS:

{% codeblock %}
$html->css('vendors/mycss');
{% endcodeblock %}

<h4>So how did I do this?</h4>
Simply edit the vendors.php file in your <em>webroot/js</em> directory (or create it if it doesn't exist) and add the following code:

{% codeblock %}
/**
 * This file includes js vendor-files from /vendor/ directory if they need to
 * be accessible to the public.
 */
$file = $_GET['file'];
if(is_file('../../../../vendors/js/'.$file))
{
    readfile('../../../../vendors/js/'.$file);
}
else
{
    header('HTTP/1.1 404 Not Found');
}
{% endcodeblock %}

Now you just need to create an .htaccess file in your <em>webroot/js</em> directory with the following content:

{% codeblock %}
<ifmodule>
    RewriteEngine On
    RewriteCond %{REQUEST_FILENAME} !-d
    RewriteCond %{REQUEST_FILENAME} !-f
    RewriteRule ^vendors/(.*)$ vendors.php?file=$1 [QSA,L]
</ifmodule>
{% endcodeblock %}

This is required, so this whole thing will obviously only work if you have apache's mod_rewrite enabled.

Now just create a directory called <em>js</em> in your global <em>vendors</em> directory and place your javascript files into it. Now you can include your javascript files from a central repository shared by all your apps.

Just rinse and repeat for your CSS and images directories. Not forgetting to edit the file paths, etc.
