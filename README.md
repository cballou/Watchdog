About Watchdog
--------------

Watchdog is a PHP class implementing inotify which watches for changes to files in
any given number of directories specified in the input. It will not
recursively check directories, so you must implicitely specify each directory
you want watched.

Although it was developed for the purpose of monitoring dynamic css files for
changes and auto-regenerating their output, it can easily be transformed into
a watchdog for just about anything. 

Watchdog currently supports compilation of Stylus, SASS, LESS, Jade, and HAML.
If you have anything else you'd like added to the list, let me know!

Usage 
-----

```bash
./watchdog --types styl --watch /path/to/public/css/
./watchdog --types styl,sass,scss,less,jade,haml --watch /path/to/public/css/
./watchdog --types styl,less --watch /path/to/public/css/ --ignore mixins.less 
./watchdog --types less --watch /path/to/public/css/less/ --ignore mixins.less --
./watchdog --config /path/to/config
./watchdog --help
```

Example Config File (written in PHP, requires return):

```php
<?php
return array(
    'types' => array('sass', 'scss', 'less', 'styl', 'jade', 'haml'),
    'watch' => array(
        '/path/to/public/css',
        '/path/to/alternate/css'
    ),
    'minify' => true,
    'ignore' => array()
);
```

Example Config File demonstrating all settings:

```php
<?php
return array(
    'types' => array('sass', 'scss', 'less', 'styl', 'jade', 'haml'),
    'watch' => array(
        // key => val equivalent to input file for compilation => output file (result of compiling)
        '/path/to/public/css/dynamic/' => '/path/to/public/css/',
        // assume the input path and output path are the same
        '/path/to/alternate/css',
        // watch a specific file
        '/path/to/public/html/view.jade'
    ),
    'minify' => true,
    'ignore' => array(
        'mixins.less'
    )
);
```

Settings
--------

The configuration file is slightly more customizable than specifying arguments via the command line.
For starters, you can specify both the input file/directory and output file/directory of watched files/directories
which comes in handy if you store your files in two separate directories.

Requirements
------------

Watchdog requires you to have the PHP PEAR library inotify installed. If you have
PEAR installed, you may run the following from the command line to install inotify:

```bash
sudo pecl install inotify
```

Prerequisites
-------------

Watchdog is merely an intermediary between you and your dynamic CSS files. It
does not handle any form of parsing internally, and subsequently passes off
proper executable commands to the command line for compiling. For these reasons,
watchdog assumes that you have one or more of the following modules installed
(depending on your particular necessities):

* SASS
* LESS
* Stylus
* Jade
* HAML

Each of these applications have their own set of dependencies.

* SASS - Requires Ruby and RubyGems
* LESS - Requires nodejs and npm
* Stylus - Requires nodejs and npm
* Jade - Requires nodejs and npm
* HAML - Requires Ruby and RubyGems

"sass: command not found"
---------------------

If you are receiving the error "sass: command not found", you will need to
ensure you have the SASS ruby gem installed:

```bash
sudo gem install sass`
```

"lessc: command not found"
---------------------

If you are receiving the error "lessc: command not found", you will need to
ensure you have the LESS npm module installed globally:

```bash
sudo npm install -g less
```

We specify the global option because you would otherwise be left with modules installed to your base installation directory.

"stylus: command not found"
---------------------

If you are receiving the error "stylus: command not found", you will need to
ensure you have the stylus npm module installed globally:

```bash
sudo npm install -g stylus
```

We specify the global option because you would otherwise be left with modules installed to your base installation directory.

"jade: command not found"
---------------------

If you are receiving the error "jade: command not found", you will need to
ensure you have the Jade npm module installed globally:

```bash
sudo npm install -g jade`
```

"haml: command not found"
---------------------

If you are receiving the error "haml: command not found", you will need to
ensure you have the HAML ruby gem installed:

```bash
sudo gem install haml-edge`
```

We specify the global option because you would otherwise be left with modules installed to your base installation directory.

I'm still getting command not found
---------------------
For Node.JS NPM modules (stylus, less, and jade), ensure you have the NODE_PATH variable
appropriately set:

```bash
echo 'export NODE_PATH=/usr/local/lib/node_modules' >> ~/.profile
source ~/.profile
```
