--- 
layout: post
title: Generate Task for CakePHP 1.2
categories: articles
---
Following on from my previous posts announcing CakePHP 1.2 compatible versions of Migrations and Fixtures, below you will find another bake2 task that can very quickly generate your models, controllers, migrations and fixtures.

To generate a model called "User" in your "app" application, simply run:

<pre><code>php bake2.php generate app model User</code></pre>

Use the exact same syntax to generate controllers and migrations.

If you run "php bake2.php generate app fixtures", a fixture will be created for every table in your database, unless of course fixtures already exists.

<pre><code>/**
 * The GenerateTask generates various files as specified.
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
 * @version         $Version: 1.0 $
 * @modifiedby      $LastChangedBy: joelmoss $
 * @lastmodified    $Date: 2007-02-16 09:09:45 +0000 (Fri, 16 Feb 2007) $
 * @license         http://www.opensource.org/licenses/mit-license.php The MIT License
 */ 

uses('file', 'folder', 'inflector');

class GenerateTask extends BakeTask
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

        define('FIXTURES_PATH', APP_PATH .'config' .DS. 'fixtures');
        define('MIGRATIONS_PATH', APP_PATH .'config' .DS. 'migrations');

        if (count($params) &gt; 0)
        {
            if ($params[0] == 'fixtures')
            {
                $this-&gt;fixtures();
                exit;
            }
            elseif ($params[0] == 'migration')
            {
                $this-&gt;migration($params[1]);
                exit;
            }
            elseif ($params[0] == 'model')
            {
                $this-&gt;model($params[1]);
                exit;
            }
            elseif ($params[0] == 'controller')
            {
                $this-&gt;controller($params[1]);
                exit;
            }
        }

        $this-&gt;help();
    }

    function controller($name)
    {
        if (empty($name)) $this-&gt;err('Controller name not specified.');
        if (!preg_match("/^[a-zA-Z]+$/", $name))
            $this-&gt;err('Controller name ('.$name.') is invalid. It must be CamelCased');

        $filename = Inflector::underscore($name) . '_controller.php';
        if (file_exists(CONTROLLERS . $filename)) $this-&gt;err('Controller ('.$name.') already exists.');

        $data = "";
        $file = new File(CONTROLLERS . $filename, true);
        $file-&gt;write($data);

        $this-&gt;out('');
        $this-&gt;out('Generation of controller: ''.$name.'' completed.');
        $this-&gt;out('Please edit ''.CONTROLLERS . $filename . '' to customise your controller.');

        if (!file_exists(VIEWS.Inflector::underscore($name)))
            new Folder(VIEWS.Inflector::underscore($name), true, 0777);

        $this-&gt;hr();
        exit;
    }

    function model($name)
    {
        if (empty($name)) $this-&gt;err('Model name not specified.');
        if (!preg_match("/^[a-zA-Z]+$/", $name))
            $this-&gt;err('Model name ('.$name.') is invalid. It must be CamelCased');

        $filename = Inflector::underscore($name) . '.php';
        if (file_exists(MODELS . $filename)) $this-&gt;err('Model ('.$name.') already exists.');

        $data = "";
        $file = new File(MODELS . $filename, true);
        $file-&gt;write($data);

        $this-&gt;out('');
        $this-&gt;out('Generation of model: ''.$name.'' completed.');
        $this-&gt;out('Please edit ''.MODELS . $filename . '' to customise your model.');

        $this-&gt;migration('create_'.Inflector::tableize($name));
        exit;
    }

    function migration($name)
    {
        if (empty($name)) $this-&gt;err('Migration name not specified.');
        if (!preg_match("/^([a-z0-9]+|_)+$/", $name)) $this-&gt;err('Migration name ('.$name.') is invalid');

        $this-&gt;getMigrations();
        $new_migration_count = $this-&gt;migration_count+1;
        $data = "#n# migration YAML filen#nUP: nullnDOWN: null";
        $file = new File(MIGRATIONS_PATH . DS .$new_migration_count . '_' . $name . '.yml', true);
        $file-&gt;write($data);

        $this-&gt;out('');
        $this-&gt;out('Generation of migration file: ''.$name.'' completed.');
        $this-&gt;out('Please edit ''.MIGRATIONS_PATH . DS .$new_migration_count . '_' . $name . '.yml' to customise your migration.');
        $this-&gt;hr();
        exit;
    }

    function getMigrations()
    {
        $folder = new Folder(MIGRATIONS_PATH, true, 0777);
        $this-&gt;migrations = $folder-&gt;find("[0-9]+_.+.yml");
        usort($this-&gt;migrations, array('GenerateTask', '_upMigrations'));
        $this-&gt;migration_count = count($this-&gt;migrations);
    }

    function _upMigrations($a, $b)
    {
        list($aStr) = explode('_', $a);
        list($bStr) = explode('_', $b);
        $aNum = (int)$aStr;
        $bNum = (int)$bStr;
        if ($aNum == $bNum) {
            return 0;
        }
        return ($aNum &gt; $bNum) ? 1 : -1;
    }

    function fixtures()
    {
        $folder = new Folder(FIXTURES_PATH, true, 0777);
        $tables = $this-&gt;_db-&gt;listTables();
        if (!count($tables))
            $this-&gt;err('Database contains no tables. Please generate and run your migrations before your fixtures.');

        $this-&gt;out();
        $data = "#n# Fixture YAML filen#n#n# Example:-n# -n#  first_name: Bobn#  last_name: Bonesn#n";
        foreach ($tables as $i=&gt;$t)
        {
            if (!file_exists(FIXTURES_PATH .DS. $t . '.yml'))
            {
                $file = new File(FIXTURES_PATH .DS. $t . '.yml', true);
                $file-&gt;write($data);
                $this-&gt;out('  Generating fixture for '.$t.' ... DONE!');
            }
        }
        $this-&gt;out('Generating complete!');
        $this-&gt;hr();
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
            $this-&gt;err('Task Error: Unable to include PEAR.php and MDB2.php');
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
        echo "This task generates database migration and fixture files.n";
        echo "Usage: bake2 generate app_alias fixtures|migration [migration_name]n";
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
    $this-&gt;out(' __  __  _  _  __  __  _  _  __     __   __       __  __   __  ___  __   __ ');
    $this-&gt;out('|   |__| |_/  |__ |__] |__| |__]   | _  |__ | | |__ |__] |__|  |  |  | |__]');
    $this-&gt;out('|__ |  | | _ |__ |    |  | |      |__| |__ | | |__ |   |  |  |  |__| |  ');
        $this-&gt;hr();
        $this-&gt;out('');
    }

}
</code></pre>

Its a great way to easily complete a few mudane tasks.
