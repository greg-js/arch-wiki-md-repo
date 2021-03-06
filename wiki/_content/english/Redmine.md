Related articles

*   [Ruby on Rails](/index.php/Ruby_on_Rails "Ruby on Rails")
*   [RVM](/index.php/RVM "RVM")
*   [MariaDB](/index.php/MariaDB "MariaDB")
*   [Apache](/index.php/Apache "Apache")
*   [Nginx](/index.php/Nginx "Nginx")

[Redmine](https://www.redmine.org/) is a [free and open source](https://en.wikipedia.org/wiki/free_and_open_source_software "wikipedia:free and open source software"), web-based [project management](https://en.wikipedia.org/wiki/project_management "wikipedia:project management") and [issue tracking](https://en.wikipedia.org/wiki/Issue_tracking_system "wikipedia:Issue tracking system") tool. It handles multiple projects and subprojects. It [features](http://www.redmine.org/projects/redmine/wiki/Features) per project wikis and forums, time tracking, and flexible role based access control. It includes a [calendar](https://en.wikipedia.org/wiki/calendar "wikipedia:calendar") and [Gantt charts](https://en.wikipedia.org/wiki/Gantt_chart "wikipedia:Gantt chart") to aid visual representation of projects and their [deadlines](https://en.wikipedia.org/wiki/time_limit "wikipedia:time limit"). Redmine integrates with various [version control](https://en.wikipedia.org/wiki/version_control "wikipedia:version control") systems and includes a repository browser and diff viewer.

Redmine is written using the [Ruby on Rails](/index.php/Ruby_on_Rails "Ruby on Rails") framework. It is cross-platform and cross-[database](https://en.wikipedia.org/wiki/database "wikipedia:database") and supports 34 languages.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Prerequisites](#Prerequisites)
    *   [1.1 Ruby](#Ruby)
    *   [1.2 Database](#Database)
        *   [1.2.1 MariaDB 5.0 or higher (recommended)](#MariaDB_5.0_or_higher_(recommended))
        *   [1.2.2 MySQL 5.5 - 5.7](#MySQL_5.5_-_5.7)
        *   [1.2.3 PostgreSQL 9.2 or higher](#PostgreSQL_9.2_or_higher)
        *   [1.2.4 Microsoft SQL Server 2012 or higher](#Microsoft_SQL_Server_2012_or_higher)
        *   [1.2.5 SQLite 3](#SQLite_3)
    *   [1.3 Web Server](#Web_Server)
        *   [1.3.1 Apache](#Apache)
        *   [1.3.2 Unicorn](#Unicorn)
        *   [1.3.3 Nginx](#Nginx)
        *   [1.3.4 Apache Tomcat](#Apache_Tomcat)
*   [2 Optional Prerequisites](#Optional_Prerequisites)
    *   [2.1 SCM (Source Code Management)](#SCM_(Source_Code_Management))
    *   [2.2 ImageMagick (recommended)](#ImageMagick_(recommended))
    *   [2.3 Ruby OpenID Library](#Ruby_OpenID_Library)
*   [3 Installation](#Installation)
    *   [3.1 Build and Installation](#Build_and_Installation)
    *   [3.2 Database Configuration](#Database_Configuration)
        *   [3.2.1 Database Creation](#Database_Creation)
        *   [3.2.2 Database Access Configuration](#Database_Access_Configuration)
    *   [3.3 Ruby gems](#Ruby_gems)
        *   [3.3.1 Adding Additional Gems (Optional)](#Adding_Additional_Gems_(Optional))
        *   [3.3.2 Check previously installed gems](#Check_previously_installed_gems)
        *   [3.3.3 Gems Installation](#Gems_Installation)
    *   [3.4 Session Store Secret Generation](#Session_Store_Secret_Generation)
    *   [3.5 Database Structure Creation](#Database_Structure_Creation)
    *   [3.6 Database Population with Default Data](#Database_Population_with_Default_Data)
    *   [3.7 File System Permissions](#File_System_Permissions)
    *   [3.8 Test the installation](#Test_the_installation)
    *   [3.9 Configure the production server](#Configure_the_production_server)
*   [4 Updating](#Updating)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 RMagick gem without support for High Dynamic Range in ImageMagick](#RMagick_gem_without_support_for_High_Dynamic_Range_in_ImageMagick)
    *   [5.2 Runtime error complaining that RMagick was configured with older version](#Runtime_error_complaining_that_RMagick_was_configured_with_older_version)
    *   [5.3 OpenSSL error about "SSLv3_client"](#OpenSSL_error_about_"SSLv3_client")
    *   [5.4 Error when installing gems: Cannot load such file -- mysql2/mysql2](#Error_when_installing_gems:_Cannot_load_such_file_--_mysql2/mysql2)
    *   [5.5 Apache 2.4 Updating](#Apache_2.4_Updating)
    *   [5.6 Checkout SVN Source](#Checkout_SVN_Source)
    *   [5.7 Automating The Update Process](#Automating_The_Update_Process)
    *   [5.8 Creating a Systemd Unit](#Creating_a_Systemd_Unit)
    *   [5.9 Complaints about psych](#Complaints_about_psych)
*   [6 See also](#See_also)

## Prerequisites

This document will guide you through the installation process of Redmine and all of its prerequisites, including the optional ones. If desired, however, you may install Redmine and its prerequisites separately, simply referring to the relevant sections below.

Although this guide will go through the entire installation process, this is not a one way path. Redmine can use different versions of the requisite software. For example the database requirement can be provided by mariaDB, mySQL, postgreSQL, etc.

**Note:** This guide is a default suggestion, feel free to substitute any of the prerequisites mentioned on this page.

### Ruby

| Redmine version | Supported Ruby Versions | Rails version used |
| 3.0.2 | **ruby** 1.9.3, 2.0.0, 2.1, 2.2 | **Rails** 4.2 |
| 3.4 | **ruby** 1.9.3, 2.0.0, 2.1, 2.2, 2.3, 2.4 | **Rails** 4.2 |
| 4.0 | **ruby** 2.2, 2.3, 2.4, 2.5, 2.6 | **Rails** 5.2 |
| 4.1 | **ruby** 2.3, 2.4, 2.5, 2.6 | **Rails** 5.2 |

There are two simple ways to install Ruby: installing the [ruby](https://www.archlinux.org/packages/?name=ruby) package as described in [ruby](/index.php/Ruby "Ruby") or installing RVM as described in [RVM](/index.php/RVM "RVM") **(recommended)**.

**Note:**  Rails 4.2.1 has non ASCII URL issue on MinGW Ruby ([Windows-based installer](http://rubyinstaller.org/)) thin and puma ([#19321](http://www.redmine.org/issues/19321), [#19374](http://www.redmine.org/issues/19374))

**Note:**  MinGW Ruby 2.2 has nokogiri issue ([#19419](http://www.redmine.org/issues/19419)).

**Note:**  As of 2013-03-19, SQL Server support is reported broken with **ruby 2.0.0 under Windows** because of a [database adapter gem incompatibility](https://github.com/rails-sqlserver/tiny_tds/issues/110)

**Note:**  MRI 1.9.3p327 contains a [bug](http://bugs.ruby-lang.org/issues/7374) breaking plugin loading under Windows which 1.9.3p194 or 1.9.3p392 haven't.

**Warning:** If you use RVM, pay attention to the single and multiple user differences! If you are not creating a hosting service, the multiple user (available for all users on the machine) should be the choice for simpler debuging.

**Note:**  Redmine prior to 4.0.6 supports Ruby >= 2.2.2\. Redmine 4.0.6 and later don't support Ruby 2.2 ([see Redmine installation page](https://redmine.org/projects/redmine/wiki/RedmineInstall))

### Database

Redmine [supports many different databases](http://www.redmine.org/projects/redmine/wiki/RedmineInstall#Database).

#### MariaDB 5.0 or higher (recommended)

*   MariaDB is a drop-in replacement for MySQL, in fact it was a fork of it and maintain binary compatibility. It is also [Arch Linux's default implementation of MySQL](https://www.archlinux.org/news/mariadb-replaces-mysql-in-repositories/).
*   MariaDB has known issues ([#19344](https://www.redmine.org/issues/19344), [#19395](https://www.redmine.org/issues/19395), [#17460](https://www.redmine.org/issues/17460)).

To install [mariadb](https://www.archlinux.org/packages/?name=mariadb) simply refer to [MySQL](/index.php/MySQL "MySQL").

#### MySQL 5.5 - 5.7

*   [Oracle MySQL was dropped](https://www.archlinux.org/news/mariadb-replaces-mysql-in-repositories/) to the [AUR](/index.php/AUR "AUR"). [mysql](https://aur.archlinux.org/packages/mysql/) in the [AUR](/index.php/AUR "AUR").
*   MySQL 5.6 or higher has known issues ([#19344](https://www.redmine.org/issues/19344), [#19395](https://www.redmine.org/issues/19395), [#17460](https://www.redmine.org/issues/17460)).
*   Redmine 3.x also supports MySQL 5.0 and 5.1

#### PostgreSQL 9.2 or higher

*   To install [postgresql](https://www.archlinux.org/packages/?name=postgresql) simply refer to [PostgreSQL](/index.php/PostgreSQL "PostgreSQL").

*   Make sure your database datestyle is set to ISO (Postgresql default setting). You can set it using:

 `ALTER DATABASE "redmine_db" SET datestyle="ISO,MDY";` 

*   Redmine 3.x also supports PostgreSQL 8.3 - 9.1.

**Note:** Some bugs in PostgreSQL 8.4.0 and 8.4.1 affect Redmine behavior ([#4259](http://www.redmine.org/issues/4259), [#4314](http://www.redmine.org/issues/4314)), they are fixed in PostgreSQL 8.4.2

#### Microsoft SQL Server [2012 or higher](https://github.com/rails-sqlserver/activerecord-sqlserver-adapter/blob/v4.2.3/README.md#activerecord-sql-server-adapter-for-sql-server-2012-and-higher)

**Warning:** Support is temporarily broken (with ruby 2.0.0 under Windows because of [database adapter gem incompatibility](https://github.com/rails-sqlserver/tiny_tds/issues/110)).

#### SQLite 3

Not supported for multi-user production use. So, it will not be detailed how to install and configure it for use with Redmine. See [upstream document](http://www.redmine.org/projects/redmine/wiki/RedmineInstall#Supported-database-back-ends) for more info.

### Web Server

#### Apache

To install [apache](https://www.archlinux.org/packages/?name=apache) simply refer to [Apache](/index.php/Apache "Apache").

#### Unicorn

To install Unicorn server (ruby gem) simply refer to [Ruby on Rails#Unicorn](/index.php/Ruby_on_Rails#Unicorn "Ruby on Rails").

#### Nginx

To install [nginx](https://www.archlinux.org/packages/?name=nginx) simply refer to [Nginx](/index.php/Nginx "Nginx").

#### Apache Tomcat

To install [tomcat8](https://www.archlinux.org/packages/?name=tomcat8) or [tomcat7](https://www.archlinux.org/packages/?name=tomcat7) simply refer to [Tomcat](/index.php/Tomcat "Tomcat").

## Optional Prerequisites

### SCM (Source Code Management)

| SCM | Supported versions | Comments |
| [Git](http://git-scm.com) | 1.5.4.2 to 2.11.0 |
| [Subversion](http://subversion.apache.org) | 1.3 to 1.9.7 | 1.3 or higher required.

Does not support Ruby Bindings for Subversion.

Subversion 1.7.0 and 1.7.1 contains bugs [#9541](http://www.redmine.org/issues/9541) |
| [Mercurial](http://www.selenic.com/mercurial) | 1.2 to 4.3.1 | Support bellow version 1.6 is droped as seen in [#9465](http://www.redmine.org/issues/9465). |
| [Bazaar](http://bazaar-vcs.org) | 1.0.0.candidate.1 to 2.7.0 |
| [Darcs](http://darcs.net) | >=1.0.7 |
| [CVS](http://www.nongnu.org/cvs) | 1.12.12, 1.12.13 | 1.12 required.
Will not work with CVSNT. |

More information can be read at [Redmine Repositories Wiki](http://www.redmine.org/projects/redmine/wiki/RedmineRepositories).

### ImageMagick (recommended)

[ImageMagick](http://www.imagemagick.org) is necessary to enable Gantt export to a [PNG](https://en.wikipedia.org/wiki/Portable_Network_Graphics "wikipedia:Portable Network Graphics") file and thumbnails generation.

To install [imagemagick](https://www.archlinux.org/packages/?name=imagemagick) simply:

```
# pacman -S imagemagick

```

### Ruby OpenID Library

To enable [OpenID](http://janrain.com/openid-enabled) support, is required a version >= 2 of the library.

The current version (as of 14th January 2020) is 0.9.4, which supports Redmine 4.

## Installation

### Build and Installation

Download, build and install the [redmine](https://www.archlinux.org/packages/?name=redmine) package.

**Note:** Detailed build instructions are in [Arch User Repository#Build and install the package](/index.php/Arch_User_Repository#Build_and_install_the_package "Arch User Repository"). It is **HIGHLY** recommended to read the [AUR](/index.php/AUR "AUR") page to understand what are you doing.

### Database Configuration

Now, we will need to create the database that the Redmine will use to store your data. For now on, the database and its user will be named `redmine`. But this names can be changed to anything else.

**Note:** The configuration for [MariaDB](/index.php/MariaDB "MariaDB") and [MySQL](/index.php/MySQL "MySQL") will be the same since both are binary compatible.

#### Database Creation

To create the database, the user and set privileges (MariaDB and MySQL >= 5.0.2):

 `# mysql -u root -p` 
```
CREATE DATABASE redmine CHARACTER SET UTF8;
CREATE USER 'redmine'@'localhost' IDENTIFIED BY 'my_password';
GRANT ALL PRIVILEGES ON redmine.* TO 'redmine'@'localhost';
```

For versions of MariaDB and MySQL prior to 5.0.2:

 `# mysql -u root -p` 
```
CREATE DATABASE redmine CHARACTER SET UTF8;
GRANT ALL PRIVILEGES ON redmine.* TO'redmine'@'localhost' IDENTIFIED BY 'my_password';
```

For PostgreSQL:

```
CREATE ROLE redmine LOGIN ENCRYPTED PASSWORD 'my_password' NOINHERIT VALID UNTIL 'infinity';
CREATE DATABASE redmine WITH ENCODING='UTF8' OWNER=redmine;
```

For SQLServer:

Although the database, login and user can be created within SQL Server Management Studio with a few clicks, you can always use the command line with `SQLCMD`:

```
USE [master]
GO
-- Very basic DB creation
CREATE DATABASE [REDMINE]
GO
-- Creation of a login with SQL Server login/password authentication and no password expiration policy
CREATE LOGIN [REDMINE] WITH PASSWORD=N'redminepassword', DEFAULT_DATABASE=[REDMINE], CHECK_EXPIRATION=OFF, CHECK_POLICY=OFF
GO
-- User creation using previously created login authentication
USE [REDMINE]
GO
CREATE USER [REDMINE] FOR LOGIN [REDMINE]
GO
-- User permissions set via roles
EXEC sp_addrolemember N'db_datareader', N'REDMINE'
GO
EXEC sp_addrolemember N'db_datawriter', N'REDMINE'
GO
```

**Note:** If you want to use additional environments, you must create separate databases for each one (for example: *development* and *test*).

#### Database Access Configuration

Now you need to configure Redmine to access the database we just created. To do that you have to copy `/usr/share/webapps/redmine/config/database.yml.example` to `database.yml`:

```
# cd /usr/share/webapps/redmine/config
# cp database.yml.example database.yml

```

And then edit this file in order to configure your database settings for "production" environment (you can configure for the "development" and "test" environments too, just change the appropriate sections).

Example for MariaDB and MySQL database:

 `nano database.yml` 
```
production:
  adapter: mysql2
  database: redmine
  host: localhost
  port: 3307   **#If your server is not running on the standard port (3306), set it here, otherwise this line is unnecessary.**
  username: redmine
  password: my_password
```

**Note:** For ruby1.9 the "adapter" value must be set to `mysql2`, and for ruby1.8 or jruby, it must be set to `mysql`.

Example for PostgreSQL database:

 `nano database.yml` 
```
production:
  adapter: postgresql
  database: redmine
  host: localhost
  username: redmine
  password: my_password
  encoding: utf8
  schema_search_path: <database_schema> (default - public)
```

Example for a SQL Server database:

 `nano database.yml` 
```
production:
  adapter: sqlserver
  database: redmine
  host: localhost **#Set not default host (localhost) here, otherwise this line is unnecessary.**
  port: 1433 **#Set not standard port (1433) here, otherwise this line is unnecessary.**
  username: redmine
  password: my_password

```

### Ruby gems

Redmine requires some [RubyGems](/index.php/RubyGems "RubyGems") to be installed and there are multiple ways of installing them (as listed on the referenced page).

*   prototype-rails
*   unicorn (an application-server)
*   mysql2 (high-performance Ruby bindings for MySQL)
*   coderay
*   erubis
*   fastercsv
*   rdoc
*   net-ldap
*   rack-openid

Obviously, if you choose a different database-server, or want to use a different application-server you should replace *mysql2* and *unicorn* to your liking.

#### Adding Additional Gems (Optional)

If you need to load gems that are not required by Redmine core (eg. Puma, fcgi), create a file named `Gemfile.local` at the root of your redmine directory. It will be loaded automatically when running `bundle install`:

 `# nano Gemfile.local`  `gem 'puma'` 

#### Check previously installed gems

The Redmine devs included Bundler in Redmine, which can manage Gems just like pacman manages packages. Run the following command to assure that all Redmine dependencies are met:

```
# bundle install --without development test

```

This should output a list of gems Redmine needs.

#### Gems Installation

**Note:** If you prefer, you can install all the gems as pacman packages. You have only to search for the gem package and install them as usual. As of using Ruby gem is much simpler to manage and maintain up to date gems, this will be preferable and used as default bellow.

Redmine uses Bundler to manage gems dependencies. So, you need to install Bundler first:

```
# gem install bundler

```

Then you can install all the gems required by Redmine using the following command:

```
# cd /usr/share/webapps/redmine
# bundle install

```

To install without the ruby *development* and *test* environments use this instead of the last command:

```
# bundle install --without development test

```

**Note:** You can include/exclude environments using the above syntax.

Although [imagemagick](https://www.archlinux.org/packages/?name=imagemagick) is highly [recommended](#ImageMagick_.28recommended.29), if you do not use it, you should skip the installation of the `rmagick` gem using:

```
# bundle install --without rmagick

```

**Note:** Only the gems that are needed by the adapters you have specified in your database configuration file are actually installed (eg. if your `config/database.yml` uses the *mysql2* adapter, then only the mysql2 gem will be installed). Do not forget to re-run `bundle install` when you change or add adapters in this file.

### Session Store Secret Generation

Now you must generate a random key that will be used by Rails to encode cookies that stores session data thus preventing their tampering:

```
# bundle exec rake generate_secret_token

```

**Note:** For Redmine prior to 2.x this step is done by executing `# bundle exec rake generate_session_store`.

**Warning:** Generating a new secret token invalidates all existing sessions after restart.

### Database Structure Creation

With the database created and the access configured for Redmine, now it is time to create the database structure. This is done by running the following command under the application root directory:

```
# cd /usr/share/webapps/redmine
# RAILS_ENV=production bundle exec rake db:migrate

```

These command will create tables by running all migrations one by one then create the set of the permissions and the application administrator account, named admin.

### Database Population with Default Data

Now you may want to insert the default configuration data in database, like basic types of task, task states, groups, etc. To do so execute the following:

```
# RAILS_ENV=production bundle exec rake redmine:load_default_data

```

Redmine will prompt for the data set language that should be loaded; you can also define the REDMINE_LANG environment variable before running the command to a value which will be automatically and silently picked up by the task:

```
# RAILS_ENV=production REDMINE_LANG=pt-BR bundle exec rake redmine:load_default_data

```

**Note:** This step is not mandatory, but it certainly will save you a lot of work to start using Redmine. And for a first time it can be very instructive.

### File System Permissions

The user account running the application **must** have write permission on the following subdirectories:

```
**files**: storage of attachments.
**log**: application log file production.log.
**tmp** and **tmp/pdf**: used to generate PDF documents among other things (create these ones if not present).

```

Assuming you run the application with a the default Apache user `http` account:

```
# mkdir tmp tmp/pdf public/plugin_assets
# chown -R http:http files log tmp public/plugin_assets
# chmod -R 755 files log tmp tmp/pdf public/plugin_assets

```

### Test the installation

To test your new installation using WEBrick web server run the following in the Redmine folder:

```
# ruby bin/rails server webrick -e production

```

Once WEBrick has started, point your browser to **[http://localhost:3000/](http://localhost:3000/)**. You should now see the application welcome page. Use default administrator account to log in: ***admin***/***admin***. You can go to Administration menu and choose Settings to modify most of the application settings.

**Warning:** Webrick is not suitable for production use, please only use webrick for testing that the installation up to this point is functional. Use one of the many other guides in this wiki to setup redmine to use either Passenger (aka mod_rails), FCGI or a Rack server (Unicorn, Thin, Puma or hellip) to serve up your redmine.

### Configure the production server

For Apache and Nginx, it is recommended to use Phusion Passenger. [Passenger](http://www.modrails.com/), also known as `mod_rails`, is a module available for [Nginx](/index.php/Nginx "Nginx") and [Apache](/index.php/Apache "Apache").

Start by installing the 'passenger' gem:

```
# gem install passenger

```

Now you have to look at your passenger gem installation directory to continue. If you do not known where it is, type:

```
# gem env

```

And look at the `GEM PATHS` to find where the gems are installed. If you followed this guide and installed [RVM](/index.php/RVM "RVM"), you can have more than one path, look at the one you are using.

For this guide so far, the gem path is `/usr/local/rvm/gems/ruby-2.0.0-p247@global`.

```
# cd /usr/local/rvm/gems/ruby-2.0.0-p247@global/gems/passenger-4.0.23

```

If you are aiming to use [Apache](/index.php/Apache "Apache"), run:

```
# passenger-install-apache2-module

```

In case a rails application is deployed with a sub-URI, like [http://example.com/yourapplication](http://example.com/yourapplication), some additional configuration is required, see [the modrails documentation](http://www.modrails.com/documentation/Users%20guide%20Apache.html#deploying_rails_to_sub_uri)

For [Nginx](/index.php/Nginx "Nginx"):

```
# passenger-install-nginx-module

```

And finally, the installer will provide you with further information regarding the installation (such as installing additional libraries). So, to setup your server, simply follow the output from the passenger installer.

## Updating

Backup the files used in Redmine:

```
# tar czvf ~/redmine_files.tar.gz -C /usr/share/webapps/redmine/ files

```

Backup the plugins installed in Redmine:

```
# tar czvf ~/redmine_plugins.tar.gz -C /usr/share/webapps/redmine/ plugins

```

Backup the database:

```
# mysqldump -u root -p <redmine_database> | gzip > ~/redmine_db.sql.gz

```

Update the package as normal (through [AUR](/index.php/AUR "AUR")):

```
# wget [https://aur.archlinux.org/packages/re/redmine/redmine.tar.gz](https://aur.archlinux.org/packages/re/redmine/redmine.tar.gz)
# tar -zxpvf redmine.tar.gz
# cd redmine

```

Inspect the downloaded files, mainly the [PKGBUILD](/index.php/PKGBUILD "PKGBUILD"), and then build:

```
# makepkg -s
# pacman -U redmine-2.3.0-2-any.pkg.tar.gz

```

Update the gems requirements:

```
#  bundle update

```

For a clean gems environment, you may want to remove all the gems and reinstall them. To go through this, do:

```
# for x in `gem list --no-versions`; do gem uninstall $x -a -x -I; done

```

**Warning:** The command above will delete ALL the gems in your system or user, depending of what type of Ruby installation you did in the prerequisites step. You must take care or you can stop working another applications that rely on Ruby gems.

If you did the last step and removed all the gems, now you will need to reinstall them all:

```
# gem install bundler
# bundle install --without development test

```

**Note:** If you removed ALL the gems as above, and used a server that uses a gem, remember to reinstall the server gem: passenger (for Apache and Nginx), Mongrel or Unicorn. To do this, just follow the steps in the installation tutorial above.

Copy the saved files:

```
# tar xzvf ~/redmine_files.tar.gz -C /usr/share/webapps/redmine/

```

Copy the installed plugins:

```
# tar xzvf ~/redmine_plugins.tar.gz -C /usr/share/webapps/redmine/

```

Regenerate the secret token:

```
# cd /usr/share/webapps/redmine
# bundle exec rake generate_secret_token

```

Check for any themes that you may have installed in the `public/themes` directory. You can copy them over but checking for updated version is ideal.

**Warning:** Do NOT overwrite config/settings.yml with the old one.

Update the database. This step is the one that could change the contents of your database. Go to your new redmine directory, then migrate your database:

```
# RAILS_ENV=production REDMINE_LANG=pt-BR bundle exec rake db:migrate

```

If you have installed any plugins, you should also run their database migrations:

```
# RAILS_ENV=production REDMINE_LANG=pt-BR bundle exec rake redmine:plugins:migrate

```

Now, it is time to clean the cache and the existing sessions:

```
# RAILS_ENV=production bundle exec rake tmp:cache:clear tmp:sessions:clear

```

Restart the application server (e.g. puma, thin, passenger, etc). And finally go to "Admin -> Roles & permissions" to check/set permissions for the new features, if any.

## Troubleshooting

### RMagick gem without support for High Dynamic Range in ImageMagick

As of ImageMagick 6.8.6.8-1, it is built with HDRI (High Dynamic Range Image) support, and this breaks the RMagick gem as seen in [FS#36518](https://bugs.archlinux.org/task/36518).

The github [rmagick](https://github.com/rmagick/rmagick) is already patched, but the mantainer did not packed it for rubygems yet.

To install this patched version download the git repository:

```
# git clone [https://github.com/rmagick/rmagick.git](https://github.com/rmagick/rmagick.git)

```

Then, you need to build the gem:

```
# cd rmagick
# gem build rmagick.gemspec

```

And finally install it:

```
# gem install rmagick-2.13.2.gem

```

**Note:** It will show some complains like `unable to convert "\xE0" from ASCII-8BIT to UTF-8 for ext/RMagick/RMagick2.so, skipping`, but you can safelly ignore it.

### Runtime error complaining that RMagick was configured with older version

If you get the following runtime error after upgrading ImageMagick `This installation of RMagick was configured with ImageMagick 6.8.7 but ImageMagick 6.8.8-1 is in use.` then you only need to reinstall (or rebuild as shown above if is the case).

**Note:** This is due to that when you install the RMagick gem it compiles some native extensions and they may need to be rebuilt after some ImageMagick upgrades.

### OpenSSL error about "SSLv3_client"

After thel latest OpenSSL release (version 1.0.2.g-3) the ruby stop to work and you cannot build some ruby versions. You have two way to fix it:

1\. Use ruby-head (if using RVM) or 2.3.0or above (if using Arch package).

2\. Use this patch as noted in [Issue 3529](https://github.com/rvm/rvm/issues/3529#issuecomment-157205030) and [Issue 3548](https://github.com/rvm/rvm/issues/3548)

```
# curl [https://github.com/ruby/ruby/commit/801e1fe46d83c856844ba18ae4751478c59af0d1.diff](https://github.com/ruby/ruby/commit/801e1fe46d83c856844ba18ae4751478c59af0d1.diff) > openssl.patch
# rvm install --patch ./openssl.patch 2.0.0 /*or another ruby version*/

```

### Error when installing gems: Cannot load such file -- mysql2/mysql2

If you see an error like `cannot load such file -- mysql2/mysql2`, you are having a problem with the installation of the database gem. Probably a misconfiguration in the [Database Access Configuration](#Database_Access_Configuration) step. In this case you should verify the `database.yml` file.

If no success, you can manually install the database gem by:

```
# gem install mysql2

```

In last case, as suggested by [Bobdog](/index.php?title=User:Bobdog&action=edit&redlink=1 "User:Bobdog (page does not exist)"), you can try to comment the line of the database gem and add a new one as bellow:

 `<path-to-mysql2-gem-directory>/lib/mysql2/mysql2.rb` 
```

 # require 'mysql2/mysql2'
 require '<path-to-mysql2-gem-directory>/lib/mysql2/mysql2.so'
```

### Apache 2.4 Updating

When updating to Apache 2.4 will be necessary to remove and install all your gems to make sure all of them that need to build native extensions will be rebuilt against the new Apache server.

So, for a clean gems environment, remove all the gems:

```
# for x in `gem list --no-versions`; do gem uninstall $x -a -x -I; done

```

To reinstall the gems:

```
# cd /usr/share/webapps/redmine
# gem install bundler
# bundle install --without development test

```

Remember to reinstall the RMagick gem as describe above in [RMagick gem without support for High Dynamic Range in ImageMagick](#RMagick_gem_without_support_for_High_Dynamic_Range_in_ImageMagick).

And if you are using Passenger to serve your apps through Apache you will need to reinstall it as described above in [Configure the production server](#Configure_the_production_server).

### Checkout SVN Source

Get the Redmine source ([Download instructions](http://www.redmine.org/projects/redmine/wiki/Download)). Here is method of installing Redmine directly from subversion in /srv/http/redmine/

```
# useradd -d /srv/http/redmine -s /bin/false redmine
# mkdir -p /srv/http/redmine
# svn checkout [http://svn.redmine.org/redmine/branches/2.1-stable](http://svn.redmine.org/redmine/branches/2.1-stable) /srv/http/redmine
# chown -R redmine: /srv/http/redmine

```

### Automating The Update Process

Example of an after-update script:

```
#!/usr/bin/bash
export RAILS_ENV=production
grep -E "^gem 'thin'" Gemfile || echo "gem 'thin'" >> Gemfile
bundle update && bundle exec rake generate_secret_token db:migrate redmine:plugins:migrate tmp:cache:clear tmp:sessions:clear

```

**Note:** Note that this script uses Thin as application server, so you must change it to your needs.

### Creating a Systemd Unit

If you want to automatic run you application server when system starts, you need to create a systemd unit file.

**Note:** This is not needed if you use [apache](https://www.archlinux.org/packages/?name=apache) or [nginx](https://www.archlinux.org/packages/?name=nginx) with Passenger gem. Those servers already have their own unit file, so you have only to enable it.
 `/etc/systemd/system/redmine.service` 
```
[Unit]
Description=Redmine server
After=syslog.target
After=network.target

[Service]
Type=simple
User=redmine2
Group=redmine2
Environment=GEM_HOME=/home/redmine2/.gem/
ExecStart=/usr/bin/ruby /usr/share/webapps/redmine/bin/rails server webrick -e production

# Give a reasonable amount of time for the server to start up/shut down
TimeoutSec=300

[Install]
WantedBy=multi-user.target

```

### Complaints about psych

Like that:

```
/usr/lib/ruby/2.1.0/psych/parser.rb:33:in `<class:Parser>': superclass mismatch for class Mark (TypeError)
from /usr/lib/ruby/2.1.0/psych/parser.rb:32:in `<module:Psych>'
from /usr/lib/ruby/2.1.0/psych/parser.rb:1:in `<top (required)>'
from /usr/lib/ruby/2.1.0/psych.rb:7:in `require'

```

[according to that](http://www.redmine.org/boards/2/topics/36728) that is a bundler issue, and you have to add

```
gem 'psych'

```

to your Gemfile.local

## See also

*   [Redmine Official Site](http://www.redmine.org/)
*   [Redmine Features](http://www.redmine.org/projects/redmine/wiki/Features)
*   [Official install guide from Redmine Wiki](http://www.redmine.org/projects/redmine/wiki/RedmineInstall)