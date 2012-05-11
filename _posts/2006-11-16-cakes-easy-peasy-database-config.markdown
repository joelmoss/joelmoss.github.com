--- 
layout: post
title: Cake's easy-peasy database config
categories: articles
---
Like a lot of developers out there, I use Subversion to keep control of my code and projects, and I also use a different database for development and production. But when using Cake this can be a problem when checking out my code from development to production. Unless I edit my database.php with my production config, the production code would have problems, as it would be trying to access data from the development database.

What I needed was an easy-peasy way of being able to check in my code to production without having to edit the ```app/config/database.php``` config file. So what I did was very simple and can be found below:

{% codeblock Database Config - database.php %}
class DATABASE_CONFIG {

    var $development = array(
        'driver' => 'mysql',
        'connect' => 'mysql_connect',
        'host' => 'localhost',
        'login' => 'user',
        'password' => 'passwd',
        'database' => 'app_devel'
    );
    var $production = array(
        'driver' => 'mysql',
        'connect' => 'mysql_connect',
        'host' => 'localhost',
        'login' => 'user',
        'password' => 'passwd',
        'database' => 'app'
    );
    var $test = array(
        'driver' => 'mysql',
        'connect' => 'mysql_connect',
        'host' => 'localhost',
        'login' => 'user',
        'password' => 'passwd',
        'database' => 'app_test'
    );
    var $default = array();

    function __construct()
    {
        $this->default = ($_SERVER['SERVER_ADDR'] == '127.0.0.1') ?
            $this->development : $this->production;
    }
    function DATABASE_CONFIG()
    {
        $this->__construct();
    }
}
{% endcodeblock %}

What you have here are three arrays for each datasource: development, production and test.  Each one defines the database connection variables for each environment. Nothing special there. Directly underneath that is the ```$default``` array, but it is empty. So all we have to do is fill that with the appropriate datasource.

So we set the ```construct``` method for the ```DATABASE_CONFIG``` class and include simply one line of code. What this code does is to set the ```$default``` datasource to the development datasource if the ```SERVER_ADDR``` is a local IP. As most of us develop the code on our local machines and then push it to a production server, this will do nicely, as the ```SERVER_ADDR``` on your production server will not be a local one.

So now I don't have to edit anything when moving my code to production.

Easy-peasy lemon squeasy ;)
