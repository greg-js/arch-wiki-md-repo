[Ruby on Rails](https://rubyonrails.org/), often shortened to Rails or RoR, is an open source web application framework for the [Ruby](/index.php/Ruby "Ruby") programming language. It is intended to be used with an Agile development methodology that is used by web developers for rapid development.

This document describes how to set up the Ruby on Rails Framework on an Arch Linux system.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 RubyGems](#RubyGems)
    *   [1.2 Pacman](#Pacman)
    *   [1.3 Quarry binary repository](#Quarry_binary_repository)
*   [2 Configuration](#Configuration)
*   [3 Application servers](#Application_servers)
    *   [3.1 Thin](#Thin)
    *   [3.2 Unicorn](#Unicorn)
        *   [3.2.1 Systemd service](#Systemd_service)
        *   [3.2.2 Nginx Configuration](#Nginx_Configuration)
    *   [3.3 Apache/Nginx (using Phusion Passenger)](#Apache/Nginx_(using_Phusion_Passenger))
    *   [3.4 Puma (with Nginx as reverse proxy server)](#Puma_(with_Nginx_as_reverse_proxy_server))
        *   [3.4.1 Option A: With config file](#Option_A:_With_config_file)
        *   [3.4.2 Option 2: by systemd](#Option_2:_by_systemd)
*   [4 Databases](#Databases)
    *   [4.1 SQLite](#SQLite)
    *   [4.2 PostgreSQL](#PostgreSQL)
    *   [4.3 MySQL](#MySQL)
    *   [4.4 Database Access Configuration](#Database_Access_Configuration)
    *   [4.5 Create the databases from Rails](#Create_the_databases_from_Rails)
*   [5 The Perfect Rails Setup](#The_Perfect_Rails_Setup)
    *   [5.1 Step 0: SQLite](#Step_0:_SQLite)
    *   [5.2 Step 1: RVM](#Step_1:_RVM)
    *   [5.3 Step 2: Rubies](#Step_2:_Rubies)
    *   [5.4 Step 3: Nginx with Passenger support](#Step_3:_Nginx_with_Passenger_support)
    *   [5.5 Step 4: Gemsets and Apps](#Step_4:_Gemsets_and_Apps)
    *   [5.6 Passenger for Nginx and Passenger Standalone](#Passenger_for_Nginx_and_Passenger_Standalone)
    *   [5.7 Step 5: .rvmrc files and ownerships](#Step_5:_.rvmrc_files_and_ownerships)
    *   [5.8 Step 6: Reverse proxies](#Step_6:_Reverse_proxies)
        *   [5.8.1 Launch Passenger Standalone daemons at system start-up](#Launch_Passenger_Standalone_daemons_at_system_start-up)
    *   [5.9 Step 7: Deployment](#Step_7:_Deployment)
        *   [5.9.1 With subdomains](#With_subdomains)
        *   [5.9.2 Without subdomains](#Without_subdomains)
    *   [5.10 References](#References)
*   [6 See also](#See_also)
*   [7 References](#References_2)

## Installation

Ruby on Rails requires [Ruby](/index.php/Ruby "Ruby") to be installed, so read that article first for installation instructions. The [nodejs](https://www.archlinux.org/packages/?name=nodejs) package is also required if using uglifier (Ruby wrapper for [UglifyJS JavaScript compressor](https://github.com/mishoo/UglifyJS2), optional) The Rails framework is linked to a version of Ruby (or the system Ruby installation). Ruby version(s) installed can be from system or from rbenv or from rvm (Ruby Version Manager).

### RubyGems

**Note:** You can also install Rails system-wide using Gems. To do this, run the following commands as root and append them with `--no-user-install`. Please read [Ruby#Installing gems per-user or system-wide](/index.php/Ruby#Installing_gems_per-user_or_system-wide "Ruby") for possible dangers of using RubyGem in this way.

The following command will install Rails for the current user:

```
$ gem install rails

```

Building the documentation takes a while. If you want to skip it, append `--no-document` to the install command.

```
$ gem install rails --no-document

```

gem is a package manager for Ruby modules, somewhat like pacman is to Arch Linux. To update your gems, simply run:

```
$ gem update

```

### Pacman

[Install](/index.php/Install "Install") the [ruby-rails](https://aur.archlinux.org/packages/ruby-rails/) package. Alternatively, see [Ruby#Managing RubyGems using pacman](/index.php/Ruby#Managing_RubyGems_using_pacman "Ruby").

### Quarry binary repository

Install *ruby-rails* from the unofficial [quarry](/index.php/Unofficial_user_repositories#quarry "Unofficial user repositories") repository.

## Configuration

Rails is bundled with a basic HTTP server called WeBrick. You can create a test application to test it. First, create an application with the rails command:

```
$ rails new testapp_name

```

**Note:** If you get an error like `Errno::ENOENT: No such file or directory (...) An error occurred while installing x, and Bundler cannot continue.`, you might have to configure [Bundler](/index.php/Ruby#Bundler "Ruby") so that it installs gems per-user and not system-wide. Alternatively, run `# rails new testapp_name` once as root. If it has completed successfully, delete `testapp_name/` and run `$ rails new testapp_name` again as a regular user.

This creates a new folder inside your current working directory.

```
$ cd testapp_name

```

Next start the web server. It listens on port 3000 by default:

```
$ rails server

```

Now visit the testapp_name website on your local machine by opening http://localhost:3000 in your browser

**Note:** If Ruby complains about not being able to find a JavaScript runtime, install [nodejs](https://www.archlinux.org/packages/?name=nodejs).

A test-page should be shown greeting you "Welcome aboard".

## Application servers

The built-in Ruby On Rails HTTP server (WeBrick for version 4.X of Rails, and Puma for version 5.X) is convenient for basic development, but it is not recommended for production use. Instead, you should use an application server such as [#Thin](#Thin), [#Unicorn](#Unicorn) or [Phusion Passenger](#Apache/Nginx_(using_Phusion_Passenger)).

### Thin

[Thin](http://code.macournoyer.com/thin/) is a fast and very simple Ruby web server.

First install thin gem:

```
$ gem install thin

```

Then start it using:

```
$ thin start

```

### Unicorn

[Unicorn](http://unicorn.bogomips.org/) is an application server that cannot talk directly to clients. Instead, a web server must sit between clients and Unicorn, proxying requests as needed. Unicorn is loosely based on Mongrel. It is used by Github, and it uses an architecture that tries hard to find the best child for handling a request. [Explanation of differences between Unicorn and Mongrel](https://github.com/blog/517-unicorn).

Install the Unicorn gem:

```
# gem install unicorn

```

Then create a configuration file for your application in `/etc/unicorn/`. For example; here is a configuration example (Based on [[1]](http://www.warden.pl/2011/01/07/running-redmine-under-unicorn-in-debian/)) for Redmine:

 `/etc/unicorn/redmine.ru` 
```
working_directory "/srv/http/redmine"
pid "/tmp/redmine.pid"

preload_app true
timeout 60
worker_processes 4
listen 4000
stderr_path('/var/log/unicorn.log')

GC.respond_to?(:copy_on_write_friendly=) and GC.copy_on_write_friendly = true

after_fork do |server, worker|
	#start the worker on port 4000, 4001, 4002 etc...
	addr = "0.0.0.0:#{4000 + worker.nr}"
	# infinite tries to start the worker
	server.listen(addr, :tries => -1, :delay => -1, :backlog => 128)

	#Drop privileges if running as root
	worker.user('nobody', 'nobody') if Process.euid == 0
end

```

Start it using:

```
# /usr/bin/unicorn -D -E production -c /etc/unicorn/redmine.ru

```

#### Systemd service

Put the following contents in `/etc/systemd/system/unicorn.service`:

 `/etc/systemd/system/unicorn.service` 
```
[Unit]
Description=Unicorn application server
After=network.target

[Service]
Type=forking
User=redmine
ExecStart=/usr/bin/unicorn -D -E production -c /etc/unicorn/redmine.ru

[Install]
WantedBy=multi-user.target
```

You can now easily start and stop unicorn using systemctl

#### Nginx Configuration

After setting up [Nginx](/index.php/Nginx "Nginx"), configure unicorn as an upstream server using something like this (Warning: this is a stripped example. It probably does not work without additional configuration):

```
http {
	upstream unicorn {
		server 127.0.0.1:4000 fail_timeout=0;
		server 127.0.0.1:4001 fail_timeout=0;
		server 127.0.0.1:4002 fail_timeout=0;
		server 127.0.0.1:4003 fail_timeout=0;
	}

	server {
		listen		80 default;
		server_name	YOURHOSTNAMEHERE;

		location / {
			root			/srv/http/redmine/public;
			proxy_set_header	X-Forwarded-For $proxy_add_x_forwarded_for;
			proxy_set_header Host   $http_host;
			proxy_redirect		off;
			proxy_pass		[http://unicorn](http://unicorn);
		}
	}
}
```

### Apache/Nginx (using Phusion Passenger)

[Passenger](http://www.modrails.com/) also known as `mod_rails` is a module available for [Nginx](/index.php/Nginx "Nginx") and [Apache](/index.php/Apache "Apache"), that greatly simplifies setting up a Rails server environment. Nginx does not support modules as Apache and has to be compiled with `mod_rails` in order to support Passenger; let Passenger compile it for you. As for Apache, let Passenger set up the module for you.

Two differents choices (one or the other, not both in same time):

1/ Archlinux now has packages officialy support server modules to be compiled with passenger:

```
 # pacman -Syu passenger

```

2/ Start by installing the 'passenger' gem from any version of ruby (user setting):

```
# gem install passenger

```

If you are aiming to use [Apache](/index.php/Apache "Apache"), run:

```
# pacman -Syu mod_passenger (if passenger is not installed from gem)
# passenger-install-apache2-module

```

In case a rails application is deployed with a sub-URI, like [http://example.com/yourapplication](http://example.com/yourapplication), some additional configuration is required, see [the modrails documentation](http://www.modrails.com/documentation/Users%20guide%20Apache.html#deploying_rails_to_sub_uri)

For [Nginx](/index.php/Nginx "Nginx"):

```
# pacman -Syu nginx-mod-passenger (if passenger is not installed from gem)
# passenger-install-nginx-module

```

The installer will provide you with any additional information regarding the installation (such as installing additional libraries).

To serve an application with Nginx, configure it as follows:

```
server {
    server_name app.example.org;
    root path_to_app/public; # Be sure to point to 'public' folder!
    passenger_enabled on;
    rails_env development; # Rails environment.
}

```

### Puma (with Nginx as reverse proxy server)

[Puma](http://puma.io/) ([Github Page](https://github.com/puma/puma)) is a simple, fast, threaded, and highly concurrent HTTP 1.1 server for Ruby/Rack applications, and is considered the replacement for Webrick and Mongrel. It was designed to be the go-to server for Rubinius, but also works well with JRuby and MRI. While reverse proxy server would acts as a load balancer that routes all external requests to a pool of web apps.

For a webserver it is better to use a server user and group, check [Users and groups#Example adding a user](/index.php/Users_and_groups#Example_adding_a_user "Users and groups"), below use `rails` as user name and `server` as group name, also `my_app` as rails app name.

Start by copying your app to /var/www/my_app. And set new ownership with

```
# cd /var/www/
# chown -R rails:server my_app

```

and permission for user with

```
# chmod -R 775 my_app

```

Then add `puma gem` in the Gemfile and install with

```
$ cd my_app 
$ bundle install

```

Also install `nginx` by pacman.

Under your app folder, create sockets, pid and log folder with

```
$ mkdir -p shared/pids shared/sockets shared/log

```

Backup nginx.conf with

```
# cp /etc/nginx/nginx.conf /etc/nginx/nginx.conf.backup

```

Then create a new nginx.conf file with your favorite editor, copy codes below and modify as you like:

```
#user html;
worker_processes  1; # this may connect with the worker numbers puma can use.

#error_log  logs/error.log;
#error_log  logs/error.log  notice;
#error_log  logs/error.log  info;

#pid        logs/nginx.pid;

events {
    worker_connections  1024;
}

http {
	upstream app {
	    # Path to Puma SOCK file, as defined previously
 	    server unix:/var/www/my_app/shared/sockets/puma.sock;
	}

	server {
	    listen 80;
	    server_name localhost; # or your server name

	    root /var/www/my_app/public;

	    try_files $uri/index.html $uri @app;

	    location @app {
		proxy_pass http://app;
		proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
		proxy_set_header Host $http_host;
		proxy_redirect off;
	    }

	    error_page 500 502 503 504 /500.html;
	    client_max_body_size 4G;
	    keepalive_timeout 10;
	}
}
```

[Start](/index.php/Start "Start") the `nginx` service.

There are several ways to start puma server, two ways are recommended below:

In common create file `config/puma.rb`, copy codes below and modify as you like:

```
# Change to match your CPU core count
# You can check available worker numbers with $ grep -c processor /proc/cpuinfo
# also see the comment in the nginx.conf
workers 2

# Min and Max threads per worker
#threads 1, 6

app_dir = File.expand_path("../..", __FILE__)
shared_dir = "#{app_dir}/shared"

# Default to production
#rails_env = ENV['RAILS_ENV'] || "production"
#environment rails_env

# Set up socket location
bind "unix://#{shared_dir}/sockets/puma.sock"

# Logging
#stdout_redirect "#{shared_dir}/log/puma.stdout.log", "#{shared_dir}/log/puma.stderr.log", true

# Set master PID and state locations
pidfile "#{shared_dir}/pids/puma.pid"
#state_path "#{shared_dir}/pids/puma.state"
#activate_control_app

#on_worker_boot do
#  require "active_record"
#  ActiveRecord::Base.connection.disconnect! rescue ActiveRecord::ConnectionNotEstablished
#  ActiveRecord::Base.establish_connection(YAML.load_file("#{app_dir}/config/database.yml")[rails_env])
#end
```

#### Option A: With config file

Start server with

```
$ bundle exec puma -C config/puma.rb

```

You can also run it in background with parameter `-d` and check with

```
$ pgrep puma

```

when you want to `kill` it.

If you want to keep it after you log out, you can use

```
$ nohup bundle exec puma -C config/puma.rb &

```

But if the system reboot, the process will still get lost.

#### Option 2: by systemd

Create a new systemd unit `puma.service` under ~/.config/systemd/user/ and copy codes below

```
[Unit]
Description=Puma application server
After=network.target

[Service]
WorkingDirectory=/var/www/my_app
#Environment=RAILS_ENV=production
PIDFile=/var/www/my_app/shared/pids/puma.pid
ExecStart=/home/rails/.gem/ruby/2.2.0/bin/bundle exec \
	 /home/rails/.gem/ruby/2.2.0/bin/puma \
	 -C /var/www/my_app/config/puma.rb

[Install]
WantedBy=default.target
```

Hint: For ExecStart, if you've installed gem globally, you can change routes to /usr/local/bin/ in ExecStart.

Then start puma with

```
$ systemctl --user start puma

```

To enable puma system-widely: You need to store `puma.service` in /etc/systemd/system/ and modify it as below:

```
[Unit]
Description=Puma application server
After=network.target

[Service]
WorkingDirectory=/var/www/my_app
#Environment=RAILS_ENV=production
User=rails
PIDFile=/var/www/my_app/shared/pids/puma.pid
ExecStart=/home/rails/.gem/ruby/2.2.0/bin/bundle exec \
	 /home/rails/.gem/ruby/2.2.0/bin/puma \
	 -C /var/www/my_app/config/puma.rb

[Install]
WantedBy=multi-user.target
```

For further reading take a look at [#References](#References). Also, for easily deploying app in production mode, you can try [capistrano](https://github.com/capistrano/capistrano)

## Databases

Most web applications will need to interact with some sort of database. ActiveRecord (the ORM used by Rails to provide database abstraction) supports several database vendors, the most popular of which are MySQL, SQLite, and PostgreSQL. And then you will have next to configure the file "config/database.yml" for Rails application web site able to connect on your database.

### SQLite

SQLite is the default lightweight database for Ruby on Rails. To enable SQLite, simply install [sqlite](https://www.archlinux.org/packages/?name=sqlite).

### PostgreSQL

Install [postgresql](https://www.archlinux.org/packages/?name=postgresql).

Install for Rails:

```
# gem install pg

```

Or add the gem inside your Gemfile of your project, then use bundle.

create a new Rails web site:

```
# rails new my_web_site -d postgresql

```

### MySQL

First, install and configure a MySQL server. Please refer to [MySQL](/index.php/MySQL "MySQL") on how to do this.

A gem with some native extensions is required, probably best installed as root:

```
# gem install mysql

```

You can generate a rails application configured for MySQL by using the `-d` parameter:

```
$ rails new testapp_name -d mysql

```

### Database Access Configuration

What ever Database (MySQL or Postgresql or SQlite (the default one) you use, you then need to edit `config/database.yml`. Rails uses different databases for development, testing, production and other environments. Here is an example development configuration for MySQL running on localhost:

```
 default:
   adapter: mysql (or postgresql or sqlite)
   username: my_user_name_access
   password: my_secret_password

```

For safety reasons, it is a good practice to not directly put password (who will be no more secret) as clear text in a text file. Instead you can replace "my_secret_password' by "'<%= ENV["MYSQL_PASSWD"] %>'" where MYSQL_PASSWD can be an environment variable exported from the user environment the server use (~/.profile or ~/.bashrc or ~/.zshrc depend of your choice and utility). Surrounding <%= ENV.... %> by "'" searve in case of your password has some special chars like # or !, etc...

### Create the databases from Rails

Note that you do not have to actually create the database using MySQL or Postgresql or Sqlite, as this can be done via Rails directly with:

For rails-4.X version:

```
# rake db:create

```

For rails-5.X version:

```
# rails db:create (for version of Rails-5.X)

```

If no errors are shown, then your database has been created and Rails can talk to your MySQL database.

## The Perfect Rails Setup

*Phusion Passenger running multiple Ruby versions.*

*   [Arch Linux](https://www.archlinux.org/): A simple, lightweight distribution. ;)
*   [Nginx](http://www.nginx.org/): A fast and lightweight **web server** with a strong focus on high concurrency, performance and low memory usage.
*   [Passenger](http://www.modrails.com/) (a.k.a. mod_rails or mod_rack): Supports both Apache and Nginx web servers. It makes deployment of Ruby web applications, such as those built on Ruby on Rails web framework, a breeze.
*   [Ruby Version Manager](https://rvm.io/) (RVM): A command-line tool which allows you to easily install, manage, and work with multiple Ruby environments from interpreters to sets of gems. RVM lets you deploy each project with its own completely self-contained and dedicated environment —from the specific version of ruby, all the way down to the precise set of required gems to run your application—.
*   [SQLite](http://sqlite.org/): The default lightweight **database** for Ruby on Rails.

### Step 0: SQLite

Install [sqlite](https://www.archlinux.org/packages/?name=sqlite).

**Note:** Of course SQLite is not critical in this setup, you can use MySQL and PostgreSQL as well.

### Step 1: RVM

Make a multi-user [RVM](/index.php/RVM "RVM") installation as specified [here](/index.php/RVM#Multi-user_installation "RVM").

In the 'adding users to the rvm group' step, do

```
# usermod -a -G rvm http
# usermod -a -G rvm nobody

```

`http` and `nobody` are the users related to Nginx and Passenger, respectively.

**Note:** Maybe adding the 'nobody' user to the 'rvm' group is not necessary.

### Step 2: Rubies

Once you have a working RVM installation in your hands, it is time to install the latest Ruby interpreter

**Note:** During the installation of Ruby patches will be applied. Consider installing the `base-devel` group beforehand.

```
$ rvm install 2.0.0

```

**Note:** It may be useful to delete the 'global' gemsets of the environments that have web applications. Their gems might somehow interfere with Passenger. In that case, a `rvm 2.0.0 do gemset delete global` is sufficient.

### Step 3: Nginx with Passenger support

Run the following to allow passenger install nginx:

```
$ rvm use 2.0.0 
$ gem install passenger
$ rvmsudo passenger-install-nginx-module

```

The passenger gem will be put into the *default* gemset.

This will download the sources of Nginx, compile and install it for you. It will guide you through all the process. Note that the default location for Nginx will be `/opt/nginx`.

**Note:** If you encounter a compilation error regarding Boost threads, see [this](https://bbs.archlinux.org/viewtopic.php?id=139164) article.

After completion, add the following two lines into the 'http block' at `/opt/nginx/conf/nginx.conf` that look like:

```
http { 
  ...
  passenger_root /usr/local/rvm/gems/ruby-2.0.0-p353/gems/passenger-3.0.9;
  passenger_ruby /usr/local/rvm/wrappers/ruby-2.0.0-p353/ruby;
  ...
}

```

**Note:** This step is currently being done automatically by the installer script.

### Step 4: Gemsets and Apps

For each Rails application you should have a gemset. Suppose that you want to try [RefineryCMS](http://refinerycms.com) against [BrowserCMS](http://www.browsercms.org), two open-source Content Management Systems based on Rails.

Install RefineryCMS first:

```
$ rvm use 2.0.0@refinery --create
$ gem install rails -v 4.0.1
$ gem install passenger
$ gem install refinerycms refinerycms-i18n sqlite3

```

Deploy a RefineryCMS instance called *refineria*:

```
$ cd /srv/http/
$ rvmsudo refinerycms refineria

```

Install BrowserCMS in a different gemset:

```
$ rvm use 2.0.0@browser --create
$ gem install rails -v 4.0.1
$ gem install passenger
$ gem install browsercms sqlite3

```

Deploy a BrowserCMS instance called *navegador*:

```
$ cd /srv/http/
$ rvmsudo browsercms demo navegador
$ cd /srv/http/navegador
$ rvmsudo rake db:install

```

### Passenger for Nginx and Passenger Standalone

Observe that the passenger gem was installed three times and with different intentions; in the environments

*   *2.0.0* => for Nginx,
*   *2.0.0@refinery* => Standalone
*   *2.0.0@browser* => Standalone

The strategy is to combine Passenger for Nginx with Passenger Standalone. One must first identify the Ruby environment (interpreter plus gemset) that one uses the most; in this setup the Ruby interpreter and the default gemset were selected. One then proceeds with setting up Passenger for Nginx to use that environment (step 3).

*   Applications within the chosen environment can be served as in [Apache/Nginx (using Phusion Passenger)](#Apache.2FNginx_.28using_Phusion_Passenger.29), page up in this article.
*   All applications that are to use a different Ruby version and/or gemset can be served separately through Passenger Standalone and hook into the main web server via a reverse proxy configuration (step 6).

### Step 5: .rvmrc files and ownerships

This step is crucial for the correct behaviour of the setup. RVM seeks for .rvmrc files when changing folders; if it finds one, it reads it. In these files normally one stores a line like

```
rvm <ruby_version>@<gemset_name>

```

so the specified environment is set at the entrance of applications' root folder.

Create /srv/http/refineria/.rvmrc doing

```
# echo "rvm ree@refinery" > /srv/http/refineria/.rvmrc

```

, and /srv/http/navegador/.rvmrc with

```
# echo "rvm 2.0.0@browser" > /srv/http/navegador/.rvmrc

```

You have to enter to both application root folders now, because every first time that RVM finds a .rvmrc it asks you if you trust the given file, consequently you must validate the two files you have just created.

These files aid the programs involved to find the correct gems.

Apart, if applications' files and folders are not owned by the right user you will face database write-access problems. The use of rvmsudo produces *root*-owned archives when generated by Rails; in the other hand, *nobody* is the user for Passenger —if you have not changed it—: who will use and should posses them. Fix this doing

```
# chown -R nobody.nobody /srv/http/refineria /srv/http/navegador

```

### Step 6: Reverse proxies

You have to start the Passenger Standalone web servers for your applications. So, do

```
$ cd /srv/http/refineria
$ rvmsudo passenger start --socket tmp/sockets/passenger.socket -d

```

and

```
$ cd /srv/http/navegador
$ rvmsudo passenger start --socket tmp/sockets/passenger.socket -d

```

. The first time that you run a Passenger Standalone it will perform a minor installation.

Note that you are using *unix domain* sockets instead of the commonly-used *TCP* sockets; it turns out that unix domain are significantly faster than TCP sockets.

**Note:** If you are experimenting trouble with unix sockets, changing to TCP should work:
```
rvmsudo passenger start -a 127.0.0.1 -p 3000 -d

```

#### Launch Passenger Standalone daemons at system start-up

*Do you have a script? Please post it here.*

The systemd script below was made for a Typo blog I host at /srv/http/typo. It is located at /etc/systemd/system/passenger_typo.service. I set the Environment= tags (see "man systemd.exec") from the output of "rvm env". The only exception was PATH=, which I had to combine from my regular PATH and the output of rvm env.

Note: If you do not set the "WorkingDirectory=" variable to your application folder, passenger will fail to find your app and will subsequently shut itself down.

```
[Unit]
Description=Passenger Standalone Script for Typo
After=network.target

[Service]
Type=forking
WorkingDirectory=/srv/http/typo
PIDFile=/srv/http/typo/tmp/pids/passenger.pid

Environment=PATH=/usr/local/rvm/gems/ruby-2.0.0-p0@typo/bin:/usr/local/rvm/gems/ruby-2.0.0-p0@global/bin:/usr/local/rvm/rubies/ruby-2.0.0-p0/bin:/usr/local/rvm/bin:/usr/local/bin:/usr/bin:/bin:/usr/local/sbin:/usr/sbin:/sbin:/usr/bin/core_perl
Environment=rvm_env_string=ruby-2.0.0-p0@typo
Environment=rvm_path=/usr/local/rvm
Environment=rvm_ruby_string=ruby-2.0.0-p0
Environment=rvm_gemset_name=typo
Environment=RUBY_VERSION=ruby-2.0.0-p0
Environment=GEM_HOME=/usr/local/rvm/gems/ruby-2.0.0-p0@typo
Environment=GEM_PATH=/usr/local/rvm/gems/ruby-2.0.0-p0@typo:/usr/local/rvm/gems/ruby-2.0.0-p0@global
Environment=MY_RUBY_HOME=/usr/local/rvm/rubies/ruby-2.0.0-p0
Environment=IRBRC=/usr/local/rvm/rubies/ruby-2.0.0-p0/.irbrc

ExecStart=/bin/bash -c "rvmsudo passenger start --socket /srv/http/typo/tmp/sockets/passenger.socket -d"

[Install]
WantedBy=multi-user.target

```

### Step 7: Deployment

#### With subdomains

Once again edit /opt/nginx/conf/nginx.conf to include some vital instructions:

```
## RefineryCMS ##

server {
    server_name refinery.domain.com;
    root /srv/http/refineria/public;
    location / {
        proxy_pass http://unix:/srv/http/refineria/tmp/sockets/passenger.socket;
        proxy_set_header Host $host;
    }
}

## BrowserCMS ##

server {
    server_name browser.domain.com;
    root /srv/http/navegador/public;
    location / {
        proxy_pass http://unix:/srv/http/navegador/tmp/sockets/passenger.socket;
        proxy_set_header Host $host;
    }
}

```

**Note:** Or if using TCP sockets, configure the *proxy_pass* directive like `proxy_pass http://127.0.0.1:3000;` 

#### Without subdomains

If you for some reason do not want to host each application on its own subdomain but rather in a url like: `site.com/railsapp` then you could do something like this in your config:

```
server {
    server_name site.com;
    #Base for the html files etc
    root /srv/http/;

    #First application you want hosted under domain site.com/railsapp
    location /railsapp {
        root /srv/http/railsapp/public;
        #you may need to change passenger_base_uri to be the uri you want to point at, ie:
        #passenger_base_uri /railsapp;
        #but probably only if you are using the other solution with passenger phusion
        proxy_pass http://unix:/srv/http/railsapp/tmp/sockets/passenger.socket;
        proxy_set_header Host $host;
    }

    #Second applicatino you want hosted under domain site.com/anotherapp
    location /anotherapp {
        root /srv/http/anotherapp/public;
        #same thing about the passenger_base_uri here, but with value /anotherapp instead
        proxy_pass http://unix:/srv/http/anotherapp/tmp/sockets/passenger.socket;
        proxy_set_header Host $host;
    }
}

```

At this point you are in conditions to [start](/index.php/Start "Start") the `nginx` service and to access both CMSs through *refinery.domain.com* and *browser.domain.com*.

### References

*   [http://beginrescueend.com/integration/passenger](http://beginrescueend.com/integration/passenger)
*   [http://blog.phusion.nl/2010/09/21/phusion-passenger-running-multiple-ruby-versions](http://blog.phusion.nl/2010/09/21/phusion-passenger-running-multiple-ruby-versions)
*   [http://www.ruby-journal.com/how-to-setup-rails-app-with-puma-and-nginx/](http://www.ruby-journal.com/how-to-setup-rails-app-with-puma-and-nginx/)
*   [https://www.digitalocean.com/community/tutorials/how-to-deploy-a-rails-app-with-puma-and-nginx-on-ubuntu-14-04](https://www.digitalocean.com/community/tutorials/how-to-deploy-a-rails-app-with-puma-and-nginx-on-ubuntu-14-04)

## See also

*   [Ruby](/index.php/Ruby "Ruby")
*   [Nginx](/index.php/Nginx "Nginx")
*   [LAMP](/index.php/LAMP "LAMP")
*   [MySQL](/index.php/MySQL "MySQL")

## References

*   Ruby on Rails [http://rubyonrails.org/download](http://rubyonrails.org/download).
*   Mongrel [http://mongrel.rubyforge.org](http://mongrel.rubyforge.org).