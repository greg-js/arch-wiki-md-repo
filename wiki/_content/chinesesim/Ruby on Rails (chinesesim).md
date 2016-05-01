[Ruby on Rails](http://rubyonrails.org/)，通常简写为 Rails 或者 RoR，是一个 Ruby 语言的开源的 web 应用框架。它通常被 web 开发人员使用敏捷开发方法做快速开发使用。

本文档描述如何在Archlinux下建立Ruby on Rails开发环境。

Ruby on Rails 需要首先安装 [Ruby](/index.php/Ruby "Ruby")，所以阅读首先阅读那篇文章查看安装说明。

## Contents

*   [1 选项A：通过RubyGems来安装 (推荐)](#.E9.80.89.E9.A1.B9A.EF.BC.9A.E9.80.9A.E8.BF.87RubyGems.E6.9D.A5.E5.AE.89.E8.A3.85_.28.E6.8E.A8.E8.8D.90.29)
    *   [1.1 更新gems](#.E6.9B.B4.E6.96.B0gems)
*   [2 选项B：通过 AUR 安装](#.E9.80.89.E9.A1.B9B.EF.BC.9A.E9.80.9A.E8.BF.87_AUR_.E5.AE.89.E8.A3.85)
*   [3 配置](#.E9.85.8D.E7.BD.AE)
*   [4 Web 服务器](#Web_.E6.9C.8D.E5.8A.A1.E5.99.A8)
*   [5 Mongrel](#Mongrel)
    *   [5.1 Apache/Nginx (using Phusion Passenger)](#Apache.2FNginx_.28using_Phusion_Passenger.29)
*   [6 数据库](#.E6.95.B0.E6.8D.AE.E5.BA.93)
    *   [6.1 SQLite](#SQLite)
    *   [6.2 PostgreSQL](#PostgreSQL)
    *   [6.3 MySQL](#MySQL)
*   [7 选项C：完美的 Rails 安装](#.E9.80.89.E9.A1.B9C.EF.BC.9A.E5.AE.8C.E7.BE.8E.E7.9A.84_Rails_.E5.AE.89.E8.A3.85)
    *   [7.1 步骤 0: SQLite](#.E6.AD.A5.E9.AA.A4_0:_SQLite)
    *   [7.2 步骤 1: RVM](#.E6.AD.A5.E9.AA.A4_1:_RVM)
    *   [7.3 步骤 2: Rubies](#.E6.AD.A5.E9.AA.A4_2:_Rubies)
        *   [7.3.1 Advice](#Advice)
    *   [7.4 步骤 3: Nginx with Passenger support](#.E6.AD.A5.E9.AA.A4_3:_Nginx_with_Passenger_support)
    *   [7.5 步骤 4: Gemsets and Apps](#.E6.AD.A5.E9.AA.A4_4:_Gemsets_and_Apps)
    *   [7.6 Passenger for Nginx and Passenger Standalone](#Passenger_for_Nginx_and_Passenger_Standalone)
    *   [7.7 步骤 5: .rvmrc 文件和所有者](#.E6.AD.A5.E9.AA.A4_5:_.rvmrc_.E6.96.87.E4.BB.B6.E5.92.8C.E6.89.80.E6.9C.89.E8.80.85)
    *   [7.8 步骤 6: 反向代理](#.E6.AD.A5.E9.AA.A4_6:_.E5.8F.8D.E5.90.91.E4.BB.A3.E7.90.86)
        *   [7.8.1 Launch Passenger Standalone daemons at system start-up](#Launch_Passenger_Standalone_daemons_at_system_start-up)
    *   [7.9 步骤 7: 部署](#.E6.AD.A5.E9.AA.A4_7:_.E9.83.A8.E7.BD.B2)
    *   [7.10 参考文献](#.E5.8F.82.E8.80.83.E6.96.87.E7.8C.AE)
*   [8 参见](#.E5.8F.82.E8.A7.81)
*   [9 参考文献](#.E5.8F.82.E8.80.83.E6.96.87.E7.8C.AE_2)

## 选项A：通过RubyGems来安装 (推荐)

**注意:** 如果这个命令不是用root运行的，那么gem会把它安装到用户的家目录中。

```
# gem install rails

```

创建文档需要一会时间. 如果不想要它,加上 --no-ri --no-rdoc 参数到安装命令中.

```
# gem install rails --no-ri --no-rdoc

```

**注意:** 如果安装完成后提示警告在PATH中没有~/.gem/ruby/2.0.0/bin,gem executables will not run，那么要使用命令export PATH="$PATH:$(ruby -rubygems -e 'puts Gem.user_dir')/bin"将rails加入环境变量，最后可以通过命令rails -v查看安装的rails版本确认rails可用。

### 更新gems

gem 是一个ruby模块包管理器, 类似pacman. 去更新gem, 简单的使用gem命令:

```
# gem update

```

## 选项B：通过 AUR 安装

**Warning:** This is not recommended, as this might not include the latest Rails version, and additional dependencies may be introduced that may require you to run `gem install` anyway.

There is a [rails](https://aur.archlinux.org/packages/rails/) package available in the [AUR](/index.php/AUR "AUR"). Note that this is not in an [official repository](/index.php/Official_repositories "Official repositories"), so you will need to [build it manually](/index.php/AUR#Build_the_package "AUR").

## 配置

Rails 自带了一个基本的HTTP服务器 WeBrick. 你可以创建一个测试应用来测试它. 首先, 创建一个应用使用rails 命令:

```
# rails new testapp_name

```

然后开始Web服务器. 它默认监听3000端口 :

```
# cd testapp_name
# rails server 

```

完成后打开浏览器输入你服务器地址和3000端口. 例如, 如果服务器在本机 :

```
在浏览器地址栏输入http://127.0.0.1:3000/ 

```

你将看到Rails默认欢迎界面 "Welcome aboard".

## Web 服务器

Ruby On Rails 默认HTTP 服务器(WeBrick) 可以方便去测试，但是不推荐在产品中使用。以下是一些合适的选择：

## Mongrel

Mongrel is a drop-in replacement for WeBrick, that can be run in precisely the same way, but offers better performance.

通过gem来安装mongrel:

```
# gem install mongrel

```

然后开始mongrel:

```
# mongrel_rails start

```

Alternatively, you can just run "ruby script/server" again, as it replaces WeBrick by default.

Generally, Mongrel is used in a production environment by running multiple instances of mongrel_rails, which are load-balanced behind an [Nginx](/index.php/Nginx "Nginx") or [Apache](/index.php/Apache "Apache") reverse proxy. However, you might find Phusion Passenger (see below) a much simpler solution for running a production environment.

### Apache/Nginx (using Phusion Passenger)

[Passenger](http://www.modrails.com/) also known as `mod_rails` is a module available for [Nginx](/index.php/Nginx "Nginx") and [Apache](/index.php/Apache "Apache"), that greatly simplifies setting up a Rails server environment.

Start by installing the Passenger gem:

```
# gem install passenger

```

If you are aiming to use [Apache](/index.php/Apache "Apache") with Passenger, run:

```
# passenger-install-apache2-module

```

For [Nginx](/index.php/Nginx "Nginx"):

```
# passenger-install-nginx-module

```

The installer will provide you with any additional information regarding the installation (such as installing additional libraries).

**Note:** See [Nginx#Ruby Integration (Ruby on Rails and Rack-based)](/index.php/Nginx#Ruby_Integration_.28Ruby_on_Rails_and_Rack-based.29 "Nginx") for more information on configuring a Rails Nginx-Passenger web stack.

## 数据库

多数Web应用都需要数据库去保存数据。ActiveRecord (the ORM used by Rails to provide database abstraction) supports several database vendors, the most popular of which are MySQL, SQLite, and PostgreSQL.

### SQLite

SQLite 是Ruby on Rails默认的数据库. 要去激活 SQLite, 安装ruby-sqlite3

```
# pacman -S ruby-sqlite3

```

### PostgreSQL

（待补充） 安装 [postgresql](https://www.archlinux.org/packages/?name=postgresql).

### MySQL

**注意:** 在尝试安装 Ruby MySQL 扩展之前，你必须首先安装带有合适头文件(位于`/usr/include`) 的 [MySQL](/index.php/MySQL "MySQL")(只需要安装 [mysql](https://aur.archlinux.org/packages/mysql/) 就可以了)。

关于如何安装 MySQL 服务器请参考 [MySQL](/index.php/MySQL "MySQL")。

首先安装通过gem安装mysql模块:

```
# gem install mysql

```

你可以创建使用mysql的Rails应用使用 `-d` 参数:

```
$ rails new testapp_name -d mysql

```

然后你需要编辑 config/database.yml. Rails 为production/tests/development使用3种数据库。下面示例使用development数据库. 填写数据库，用户名，密码字段：

```
 development:
   adapter: mysql
   database: my_application_database
   username: development
   password: my_secret_password

```

Note that you do not have to actually create the database using MySQL, as this can be done via Rails with:

```
# rake db:migrate

```

如果没有错误显示, 那么表示建立正确，并且Rails可以和MySQL数据库通信了。

## 选项C：完美的 Rails 安装

*Phusion Passenger running multiple Ruby versions.*

*   [Archlinux](https://www.archlinux.org/): A simple, lightweight distribution. ;)
*   [Nginx](http://www.nginx.org/): A fast and lightweight **web server** with a strong focus on high concurrency, performance and low memory usage.
*   [Passenger](http://www.modrails.com/) (a.k.a. mod_rails or mod_rack): Supports both Apache and Nginx web servers. It makes deployment of Ruby web applications, such as those built on Ruby on Rails web framework, a breeze.
*   [Ruby Enterprise Edition](http://www.rubyenterpriseedition.com/) (REE): Passenger allows Ruby on Rails applications to use about 33% less memory, when used in combination with REE.
*   [Ruby Version Manager](http://rvm.beginrescueend.com/) (RVM): A command-line tool which allows you to easily install, manage, and work with multiple Ruby environments from interpreters to sets of gems. RVM lets you deploy each project with its own completely self-contained and dedicated environment —from the specific version of ruby, all the way down to the precise set of required gems to run your application—.
*   [SQLite](http://sqlite.org/): The default lightweight **database** for Ruby on Rails.

### 步骤 0: SQLite

Easy as:

```
$ sudo pacman -S sqlite

```

**Note:** Of course SQLite is not critical in this setup, you can use MySQL and PostgreSQL as well.

### 步骤 1: RVM

Make a multi-user [RVM](/index.php/RVM "RVM") installation as specified [here](/index.php/RVM#Multi-user_installation "RVM").

In the 'adding users to the rvm group' step, do

```
$ sudo usermod -a -G rvm http
$ sudo usermod -a -G rvm nobody

```

. http and nobody are the users related to Nginx and Passenger, respectively.

**Note:** Maybe adding the 'nodody' user to the 'rvm' group is not necessary.

### 步骤 2: Rubies

Once you have a working RVM installation in your hands, it is time to install the Ruby Enterprise Edition interpreter

```
$ rvm install ree

```

. Also take the chance to include other interpreters you want to use, like the last Ruby version

```
$ rvm install 1.9.3

```

#### Advice

I have found useful to delete the 'global' gemsets of the environments that have web applications. Their gems were somehow interfering with Passenger. Do not do

```
$ rvm ree do gemset delete global
$ rvm 1.9.3 do gemset delete global

```

now, but consider this later if you encounter complications.

### 步骤 3: Nginx with Passenger support

Do not install Nginx via pacman. This web server does not support modules as Apache, so it must be compiled from source with the functionality of *mod_rails* (Passenger). Fortunately this is straightforward thanks to the passenger gem. Get it:

```
$ rvm use ree
$ gem install passenger

```

. The gem will be put into the 'default' gemset. Now execute the following script:

```
$ rvmsudo passenger-install-nginx-module

```

. It will download the sources of Nginx, compile and install it for you. It will guide you through all the process. (The default location for Nginx is /opt/nginx.)

After completion, the script will require you to add two lines into the 'http block' at /opt/nginx/conf/nginx.conf that look like:

```
http { 
  ...
  passenger_root /usr/local/rvm/gems/ree-1.8.7-2011.03/gems/passenger-3.0.9;
  passenger_ruby /usr/local/rvm/wrappers/ree-1.8.7-2011.03/ruby;
  ...
}

```

For everything that is not Ruby, use [Nginx](/index.php/Nginx "Nginx") as usual to serve static pages, PHP and Python. Check the wiki page for more information.

To enable the Nnginx service by default at start-up just add `nginx` to the `DAEMONS` array in `/etc/rc.conf`:

```
DAEMONS=(ntpd syslog-ng ... nginx)

```

**Note:** It is possible that your Nginx installation has not come with an init script; check your /etc/rc.d/ directory for a file called *nginx*, if that is your case manually create it.

### 步骤 4: Gemsets and Apps

For each Rails application you should have a gemset. Suppose that you want to try [RefineryCMS](http://refinerycms.com) against [BrowserCMS](http://www.browsercms.org), two open-source Content Management Systems based on Rails. Then you should do:

```
$ rvm use ree@refinery --create
$ gem install rails -v 3.0.11
$ gem install passenger
$ gem install refinerycms refinerycms-i18n sqlite3

```

Deploy a RefineryCMS instance called *refineria*:

```
$ cd /srv/http/
$ rvmsudo refinerycms refineria

```

Again:

```
$ rvm use 1.9.3@browser --create
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

*   *ree* => for Nginx,
*   *ree@refinery* => Standalone, and
*   *1.9.3@browser* => Standalone.

The strategy is to combine Passenger for Nginx with Passenger Standalone. One must first identify the Ruby environment (interpreter plus gemset) that one uses the most; in this setup the REE interpreter and the default gemset were selected. One then proceeds with setting up Passenger for Nginx to use that environment. All applications that are to use a different Ruby version and/or gemset can be served separately through Passenger Standalone and hook into the main web server via a reverse proxy configuration.

### 步骤 5: .rvmrc 文件和所有者

This step is crucial for the correct behaviour of the setup. RVM seeks for .rvmrc files when changing folders; if it finds one, it reads it. In these files normally one stores a line like

```
rvm <ruby_version>@<gemset_name>

```

so the specified environment is set at the entrance of applications' root folder.

Create /srv/http/refineria/.rvmrc and put

```
sudo sh -c 'echo "rvm ree@refinery" > /srv/http/navegador/.rvmrc'

```

while in /srv/http/navegador/.rvmrc,

```
sudo sh -c 'echo "rvm 1.9.3@browser" > /srv/http/navegador/.rvmrc'

```

You have to enter to both application root folders now, because every first time that RVM finds a .rvmrc it asks you if you trust the given file, consequently you must validate the two files you have just created.

These files aid the programs involved to find the correct gems.

Apart, if applications' files and folders are not owned by the right user you will face database write-access problems. The use of rvmsudo produces *root*-owned archives when generated by Rails; in the other hand, *nobody* is the user for Passenger —if you have not changed it—: who will use and should posses them. Fix this doing

```
$ sudo chown -R nobody.nobody /srv/http/refineria /srv/http/navegador

```

### 步骤 6: 反向代理

You have to start the Passenger Standalone web servers for your applications. So, do

```
$ cd /srv/http/refineria
$ rvmsudo passenger start --socket refineria.socket -d

```

and

```
$ cd /srv/http/navegador
$ rvmsudo passenger start --socket navegador.socket -d

```

. The first time that you run a Passenger Standalone it will perform a minor installation.

Note that you are using *unix domain* sockets instead of the commonly-used *TCP* sockets; it turns out that unix domain are significantly faster than TCP sockets.

#### Launch Passenger Standalone daemons at system start-up

*Coming soon!*

### 步骤 7: 部署

Once again edit /opt/nginx/conf/nginx.conf to include some vital instructions:

```
## RefineryCMS ##

upstream refineria_upstream {
    server unix:/srv/http/refineria/refineria.socket;
}

server {
    server_name refinery.domain.com;
    root /srv/http/refineria/public;
    location / {
        proxy_pass http://refineria_upstream;
        proxy_set_header Host $host;
    }
}

## BrowserCMS ##

upstream navegador_upstream {
    server unix:/srv/http/navegador/navegador.socket;
}

server {
    server_name browser.domain.com;
    root /srv/http/navegador/public;
    location / {
        proxy_pass http://navegador_upstream;
        proxy_set_header Host $host;
    }
}

```

At this point you are in conditions to run Nginx with:

```
$ sudo rc.d start nginx

```

and to access both CMSs through *refinery.domain.com* and *browser.domain.com*.

### 参考文献

*   [http://beginrescueend.com/integration/passenger](http://beginrescueend.com/integration/passenger)
*   [http://blog.phusion.nl/2010/09/21/phusion-passenger-running-multiple-ruby-versions](http://blog.phusion.nl/2010/09/21/phusion-passenger-running-multiple-ruby-versions)

## 参见

*   [Ruby](/index.php/Ruby "Ruby")
*   [Nginx](/index.php/Nginx "Nginx")
*   [LAMP](/index.php/LAMP "LAMP")
*   [MySQL](/index.php/MySQL "MySQL")

## 参考文献

*   Ruby on Rails [http://rubyonrails.org/download](http://rubyonrails.org/download).
*   Mongrel [http://mongrel.rubyforge.org](http://mongrel.rubyforge.org).