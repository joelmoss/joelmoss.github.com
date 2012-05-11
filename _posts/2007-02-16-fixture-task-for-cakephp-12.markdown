--- 
layout: post
title: Fixture Task for CakePHP 1.2
categories: articles
---
As <a href="http://joelmoss.info/switchboard/blog/2284:Migrations_Task_for_CakePHP_12">previously mentioned</a>, I have split out the Fixture part of my migrations script and placed it in its own bake2 task.

The script below is pretty much the same as the previous version of fixtures. Just run the following:

<pre><code>php bake2.php fixture app users</code></pre>

Replace "app" with your applications alias (as defined in the apps.ini file). And "users" is the name of the table that you want to run the fixture for.

<pre><code>/**
 * The FixtureTask runs a specified database fixture.
 *
 * PHP versions 4 and 5
 *
 * Licensed under The MIT License
 * Redistributions of files must retain the above copyright notice.
 *
 * @filesource
 * @copyright       Copyright 2006-2007, Joel Moss
 * @link                http://joelmoss.info
 * @package         cake
 * @subpackage      cake.cake.scripts.bake
 * @since           CakePHP(tm) v 1.2
 * @version         $Version: 3.0 $
 * @modifiedby      $LastChangedBy: joelmoss $
 * @lastmodified    $Date: 2007-02-16 09:09:45 +0000 (Fri, 16 Feb 2007) $
 * @license         http://www.opensource.org/licenses/mit-license.php The MIT License
 */

uses('file', 'folder');

class FixtureTask extends BakeTask
{

    function execute($params)
    {
        $this-&gt;welcome();

        if ($params[0] == 'help')
        {
            $this-&gt;help();
            exit;
        }

        $this-&gt;initDatabase();
        $this-&gt;initApp();

        if (count($params) &gt; 0)
        {
            define('FIXTURES_PATH', APP_PATH .DS. 'config' .DS. 'fixtures');

            $this-&gt;fixture = $params[0];
            $this-&gt;fixtures();
            exit;
        }
        else
        {
            $this-&gt;err('Table name not specified.');
        }

        $this-&gt;help();
    }

    function fixtures()
    {
        if (!file_exists(FIXTURES_PATH)) $folder = new Folder(FIXTURES_PATH, true, 0777);
        $tables = $this-&gt;_db-&gt;listTables();
        if (!count($tables))
            $this-&gt;err('Database contains no tables. Please run your migrations before your fixtures.');

        if (!file_exists(FIXTURES_PATH .DS. $this-&gt;fixture .'.yml'))
        {
            $this-&gt;err('Fixture does not exist for table ''.$this-&gt;fixture.''.');
        }

        $this-&gt;out('');
        $this-&gt;out("  Running fixture for '".$this-&gt;fixture."' ... ", false);
        $this-&gt;startFixture($this-&gt;fixture);
        $this-&gt;out('Fixture completed.');
        $this-&gt;hr();
    }

    function startFixture($name)
    {
        $file = FIXTURES_PATH .DS. $name .'.yml';

        if (function_exists('syck_load'))
        {
            $yml = file_get_contents($file);
            $data = @syck_load($yml);
        }
        else
        {
            vendor('Spyc');
            $data = Spyc::YAMLLoad($file);
        }

        if (!is_array($data) || !count($data))
            $this-&gt;err("Unable to parse YAML Fixture file: '$file'");

        $res = $this-&gt;_db-&gt;query("DELETE FROM `$name`");
        if (PEAR::isError($res)) $this-&gt;err($res-&gt;getDebugInfo());

        $count = 0;
        foreach($data as $ri=&gt;$r)
        {
            #if (!in_array('created', $r)) $data[$ri]['created'] = date('Y-m-d H:i:s');
            foreach($r as $fi=&gt;$f)
                if ($f == 'NOW') $data[$ri][$fi] = date('Y-m-d H:i:s');
            $res = $this-&gt;_db-&gt;autoExecute($name, $data[$ri], MDB2_AUTOQUERY_INSERT);
            if (PEAR::isError($res)) $this-&gt;err($res-&gt;getDebugInfo());
            $count = $count+$res;
        }
        $this-&gt;out("($count rows) ... ", false);
    }

    function initApp()
    {
        $this-&gt;out("Application: '".APP_DIR."' (".APP_PATH.")");
        $this-&gt;hr();
    }

    function initDatabase()
    {
        if (!@include_once('MDB2.php'))
        {
            echo "nnTask Error: Unable to include PEAR.php and MDB2.phpnn";
            exit;
        }

        if(!file_exists(APP_PATH.'config'.DS.'database.php'))
        {
            $this-&gt;out('** Checking for database configuration ... NOT FOUND! **');
            $this-&gt;out();
            $this-&gt;out('IMPORTANT!');
            $this-&gt;out('Your database configuration ('.APP_PATH.'config'.DS.'database.php) was not found. Please');
            $this-&gt;out('take a moment to create one by running the 'dbconfig' task:');
            $this-&gt;out('');
            $this-&gt;out('  php bake2.php dbconfig [...]');
            $this-&gt;hr();
            exit;
        }

        require_once (APP_PATH . 'config' .DS. 'database.php');

        $ds = new DATABASE_CONFIG();
        $config = $ds-&gt;default;
        $dsn = array(
            'phptype'   =&gt;  $config['driver'],
            'username'  =&gt;  $config['login'],
            'password'  =&gt;  $config['password'],
            'hostspec'  =&gt;  $config['host'],
            'database'  =&gt;  $config['database']
        );
        $options = array(
            'debug'         =&gt;  DEBUG,
            'portability'   =&gt;  DB_PORTABILITY_ALL
        );
        $this-&gt;_db = &amp;MDB2::connect($dsn, $options);
        if (PEAR::isError($this-&gt;_db)) $this-&gt;err($this-&gt;_db-&gt;getDebugInfo());
        $this-&gt;_db-&gt;setFetchMode(MDB2_FETCHMODE_ASSOC);
        $this-&gt;_db-&gt;loadModule('Manager');
        $this-&gt;_db-&gt;loadModule('Extended');
        $this-&gt;_db-&gt;loadModule('Reverse');
    }

    function help()
    {
        echo "This task inserts database fixtures.n";
        echo "Usage: bake2 fixture app_alias [table_name]n";
    }

    function out($str='', $newline=true)
    {
        $nl = $newline ? "n" : "";
        echo "  $str$nl";
    }
    function hr()
    {
        echo "n  ----------------------------------------------------------------------------n";
    }
    function err($str)
    {
        $this-&gt;out('');
        $this-&gt;out('  ** '.$str.' **');
        $this-&gt;hr();
        exit;
    }
    function welcome()
    {
        $this-&gt;out('');
        $this-&gt;hr();
    $this-&gt;out(' __  __  _  _  __  __  _  _  __     __      ___      _   __  _ ');
    $this-&gt;out('|   |__| |_/  |__ |__] |__| |__]   |_  | /  |  | | |_] |__ [_ ');
    $this-&gt;out('|__ |  | | _ |__ |    |  | |      |   | /  |  |_| |  |__  _]');
        $this-&gt;hr();
        $this-&gt;out('');
    }

}
</code></pre>

That is pretty much it.
