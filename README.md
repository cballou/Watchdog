About Watchdog
--------------

Watchdog is a PHP class implementing inotify which watches for changes to files in
any given number of directories specified in the input. It will not
recursively check directories, so you must implicitely specify each directory
you want watched.

Although it was developed for the purpose of monitoring dynamic css files for
changes and auto-regenerating their output, it can easily be transformed into
a watchdog for just about anything. 

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

Each of these applications have their own set of dependencies.

* SASS - Requires Ruby and RubyGems
* LESS - Requires nodejs and npm
* Stylus - Requires nodejs and npm

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

"stylus: command not found"
---------------------

If you are receiving the error "stylus: command not found", you will need to
ensure you have the stylus npm module installed globally:

```bash
sudo npm install -g stylus
```

Otherwise, you are left with modules installed to your base installation directory.

I'm still getting command not found
---------------------
For Node.JS NPM modules (stylus and less), ensure you have the NODE_PATH variable
appropriately set:

```bash
echo 'export NODE_PATH=/usr/local/lib/node_modules' >> ~/.profile
source ~/.profile
```
