# Lighttpd

[Lighttpd](http://www.lighttpd.net/) is "a secure, fast, compliant, and very flexible [web-server](https://en.wikipedia.org/wiki/Web_server "wikipedia:Web server") that has been optimized for high-performance environments. It has a very low memory footprint compared to other webservers and takes care of cpu-load. Its advanced feature-set ([FastCGI](https://en.wikipedia.org/wiki/FastCGI "wikipedia:FastCGI"), [CGI](https://en.wikipedia.org/wiki/Common_Gateway_Interface "wikipedia:Common Gateway Interface"), Auth, Output-Compression, URL-Rewriting and many more) make lighttpd the perfect webserver-software for every server that suffers load problems."

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Basic Setup](#Basic_Setup)
    *   [2.2 CGI](#CGI)
    *   [2.3 FastCGI](#FastCGI)
        *   [2.3.1 PHP](#PHP)
            *   [2.3.1.1 Using php-fpm](#Using_php-fpm)
            *   [2.3.1.2 eAccelerator](#eAccelerator)
            *   [2.3.1.3 Try a php page](#Try_a_php_page)
        *   [2.3.2 Ruby on Rails](#Ruby_on_Rails)
        *   [2.3.3 Python FastCGI](#Python_FastCGI)
    *   [2.4 SSL](#SSL)
        *   [2.4.1 Server Name Indication](#Server_Name_Indication)
        *   [2.4.2 Redirect HTTP requests to HTTPS](#Redirect_HTTP_requests_to_HTTPS)
    *   [2.5 Output Compression](#Output_Compression)
*   [3 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [lighttpd](https://www.archlinux.org/packages/?name=lighttpd) package.

## Configuration

### Basic Setup

The lighttpd configuration file is: `/etc/lighttpd/lighttpd.conf`. By default it should produce a working test page.

To check your `lighttpd.conf` for bugs you can use this command - helps finding misconfigurations very fast:

```
$ lighttpd -t -f /etc/lighttpd/lighttpd.conf

```

The default configuration file specifies `/srv/http/` as the document directory served. To test the installation, create a dummy file:

 `/srv/http/index.html`  `Hello world!` 

Then [start/enable](/index.php/Start/enable "Start/enable") the `lighttpd.service` and point your browser to `localhost`, where you should see the test page.

Example configuration files are available in `/usr/share/doc/lighttpd/`.

### CGI

[Common Gateway Interface](https://en.wikipedia.org/wiki/Common_Gateway_Interface "wikipedia:Common Gateway Interface") (CGI) scripts work with Lighttpd out of box, you just need to enable the CGI module, include the configuration file and make sure your chosen programming language interpreter is installed. (i.e. for python you would install [python](https://www.archlinux.org/packages/?name=python))

Create the file `/etc/lighttpd/conf.d/cgi.conf` Add the following to it:

```
server.modules += ( "mod_cgi" )

cgi.assign                 = ( ".pl"  => "/usr/bin/perl",
                               ".cgi" => "/usr/bin/perl",
                               ".rb"  => "/usr/bin/ruby",
                               ".erb" => "/usr/bin/eruby",
                               ".py"  => "/usr/bin/python",
                               ".php" => "/usr/bin/php-cgi" )

index-file.names           += ( "index.pl",   "default.pl",
                               "index.rb",   "default.rb",
                               "index.erb",  "default.erb",
                               "index.py",   "default.py",
                               "index.php",  "default.php" )

```

For PHP scripts you will need to make sure the following is set in `/etc/php/php.ini`

```
cgi.fix_pathinfo = 1

```

In your Lighttpd configuration file, `/etc/lighttpd/lighttpd.conf` add:

```
include "conf.d/cgi.conf"

```

### FastCGI

Install [fcgi](https://www.archlinux.org/packages/?name=fcgi). Now you have lighttpd with fcgi support. If it was that what you wanted you are all set. People that want Ruby on Rails, PHP or Python should continue.

**Note:** New default user and group: Instead of group `nobody` lighttpd now runs as user/group `http` by default.

First copy the example config file form `/usr/share/doc/lighttpd/config/conf.d/fastcgi.conf` to `/etc/lighttpd/conf.d`

The following needs adding to the config file, `/etc/lighttpd/conf.d/fastcgi.conf`

```
server.modules += ( "mod_fastcgi" )

#server.indexfiles += ( "dispatch.fcgi" ) #this is deprecated
index-file.names += ( "dispatch.fcgi" ) #dispatch.fcgi if rails specified

server.error-handler-404   = "/dispatch.fcgi" #too
fastcgi.server = (
    ".fcgi" => (
      "localhost" => ( 
        "socket" => "/run/lighttpd/rails-fastcgi.sock",
        "bin-path" => "/path/to/rails/application/public/dispatch.fcgi"
      )
    )
)

```

Then in `/etc/lighttpd/lighttpd.conf`:

```
include "conf.d/fastcgi.conf"

```

For PHP or Ruby on Rails see the next sections.

#### PHP

Install [php](https://www.archlinux.org/packages/?name=php) and [php-cgi](https://www.archlinux.org/packages/?name=php-cgi) (see also [PHP](/index.php/PHP "PHP") and [LAMP](/index.php/LAMP "LAMP")).

Check that php-cgi is working `php-cgi --version`

```
PHP 5.4.3 (cgi-fcgi) (built: May  8 2012 17:10:17)
Copyright (c) 1997-2012 The PHP Group
Zend Engine v2.4.0, Copyright (c) 1998-2012 Zend Technologies

```

If you get a similar output then php is installed correctly.

Create a new configuration file:

 `/etc/lighttpd/conf.d/fastcgi.conf` 

```
# Make sure to install php and php-cgi. See:                                                             
# https://wiki.archlinux.org/index.php/Fastcgi_and_lighttpd#PHP

server.modules += ("mod_fastcgi")

# FCGI server
# ===========
#
# Configure a FastCGI server which handles PHP requests.
#
index-file.names += ("index.php")
fastcgi.server = ( 
    # Load-balance requests for this path...
    ".php" => (
        # ... among the following FastCGI servers. The string naming each
        # server is just a label used in the logs to identify the server.
        "localhost" => ( 
            "bin-path" => "/usr/bin/php-cgi",
            "socket" => "/tmp/php-fastcgi.sock",
            # breaks SCRIPT_FILENAME in a way that PHP can extract PATH_INFO
            # from it 
            "broken-scriptfilename" => "enable",
            # Launch (max-procs + (max-procs * PHP_FCGI_CHILDREN)) procs, where
            # max-procs are "watchers" and the rest are "workers". See:
            # https://redmine.lighttpd.net/projects/1/wiki/frequentlyaskedquestions#How-many-php-CGI-processes-will-lighttpd-spawn 
            "max-procs" => 4, # default value
            "bin-environment" => (
                "PHP_FCGI_CHILDREN" => "1" # default value
            )
        )
    )   
)

```

Make lighttpd use the new configuration file:

 `/etc/lighttpd/lighttpd.conf` 

```
include "conf.d/fastcgi.conf"

```

**Note:** Remember that the order in which the modules are loaded is important, the correct order is listed in `/usr/share/doc/lighttpd/config/modules.conf`. Any misconfiguration may cause _lighttpd_ to crash.

[Reload](/index.php/Reload "Reload") lighttpd.

**Note:**

*   If you receive errors like _No input file found_ when attempting to access php files, there are several possible explanations. See [this FAQ](http://redmine.lighttpd.net/projects/1/wiki/frequentlyaskedquestions#I-get-the-error-No-input-file-specified-when-trying-to-use-PHP) for more information.
*   Make sure that no other module (e.g. `mod_cgi`) will try to handle the _.php_ extension.

##### Using php-fpm

There is no adaptive spawning anymore in recent lighttpd releases. For dynamic management of PHP processes, you can install [php-fpm](https://www.archlinux.org/packages/?name=php-fpm) and then [start](/index.php/Start "Start") and enable `php-fpm.service`.

**Note:** You can configure the number of servers in the pool and tweak other configuration options by editing the file `/etc/php/php-fpm.conf`. More details on _php-fpm_ can be found on the [php-fpm website](http://php-fpm.org/). Remember that when you make changes to `/etc/php/php.ini` you will need to restart `php-fpm.service`.

In `/etc/lighttpd/conf.d/fastcgi.conf` add:

```
server.modules += ( "mod_fastcgi" )

index-file.names += ( "index.php" ) 

fastcgi.server = (
    ".php" => (
      "localhost" => ( 
        "socket" => "/run/php-fpm/php-fpm.sock",
        "broken-scriptfilename" => "enable"
      ))
)

```

##### eAccelerator

**Note:** As of November 2014, [eaccelerator](https://aur.archlinux.org/packages/eaccelerator/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/eaccelerator)]</sup> cannot be compiled.

Install [eaccelerator](https://aur.archlinux.org/packages/eaccelerator/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/eaccelerator)]</sup>.

Add own config file for eaccelerator:

 `/etc/php/conf.d/eaccelerator-own.ini` 

```
zlib.output_compression = On
cgi.fix_pathinfo=1
eaccelerator.cache_dir="/home/phpuser/eaccelerator/cache"
```

**Tip:** I additionally set `safe_mod` to `On` in my setup, but this is not required.

##### Try a php page

Create the following php page, name it `index.php`, and place a copy in both `/srv/http/` and `/srv/http-ssl/html/`

```
<?php
phpinfo();
?>

```

Try navigating with a web browser to both the http and https address of your server. You should see the phpinfo page.

Check eaccelerator caching:

```
# ls -l /home/phpuser/eaccelerator/cache

```

If the above command outputs the following:

```
-rw-------  1 phpuser phpuser 456 2005-05-05 14:53 eaccelerator-277.58081
-rw-------  1 phpuser phpuser 452 2005-05-05 14:53 eaccelerator-277.88081

```

Then eaccelerator is happily caching your php scripts to help speed things up.

#### Ruby on Rails

Install and configure FastCGI (see [#FastCGI](#FastCGI) above).

Install [ruby](/index.php/Ruby "Ruby") from [official repositories](/index.php/Official_repositories "Official repositories") and [ruby-fcgi](https://aur.archlinux.org/packages/ruby-fcgi/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/ruby-fcgi)]</sup> from [AUR](/index.php/AUR "AUR").

Follow instructions on [RubyOnRails](/index.php/RubyOnRails "RubyOnRails").

#### Python FastCGI

**Note:** This method will not work with Python 3 because _Flup_ library is only available for Python 2\. If you want to use Python 3, you should refer to [#CGI](#CGI) section.

Install and configure FastCGI (see [#FastCGI](#FastCGI) above).

Install [python2-flup](https://www.archlinux.org/packages/?name=python2-flup).

Configure:

```
fastcgi.server = (
    ".py" =>
    (
        "python-fcgi" =>
        (
        "socket" => "/run/lighttpd/fastcgi.python.socket",
         "bin-path" => "test.py",
         "check-local" => "disable",
         "max-procs" => 1,
        )
    )
)

```

Put the test.py in the root of your server (do not forget to chmod +x it)

```
#!/usr/bin/env python2

def myapp(environ, start_response):
    print 'got request: %s' % environ
    start_response('200 OK', [('Content-Type', 'text/plain')])
    return ['Hello World!']

if __name__ == '__main__':
    from flup.server.fcgi import WSGIServer
    WSGIServer(myapp).run()
```

[Thanks to firecat53 for his explanation](https://bbs.archlinux.org/viewtopic.php?pid=734173#p734173)

### SSL

**Warning:** If you plan on implementing SSL/TLS, know that some variations and implementations are [still](https://weakdh.org/#affected) [vulnerable to attack](https://en.wikipedia.org/wiki/Transport_Layer_Security#Attacks_against_TLS.2FSSL "wikipedia:Transport Layer Security"). For details on these current vulnerabilities within SSL/TLS and how they apply to Lighttpd and other services (such as email) visit [http://disablessl3.com/](http://disablessl3.com/) and [https://weakdh.org/sysadmin.html](https://weakdh.org/sysadmin.html)

Generate an SSL Cert, e.g. like that:

```
# mkdir /etc/lighttpd/certs
# openssl req -x509 -nodes -days 7300 -newkey rsa:2048 -sha256 -keyout /etc/lighttpd/certs/www.example.com.pem -out /etc/lighttpd/certs/www.example.com.pem
# chmod 600 /etc/lighttpd/certs/www.example.com.pem

```

Edit `/etc/lighttpd/lighttpd.conf`. To make lighttpd SSL-only (you probably need to set the server port to 443 as well)

```
ssl.engine = "enable" 
ssl.pemfile = "/etc/lighttpd/certs/www.example.com.pem"

```

To enable SSL in addition to normal HTTP

```
$SERVER["socket"] == ":443" {
    ssl.engine                  = "enable" 
    ssl.pemfile                 = "/etc/lighttpd/certs/www.example.com.pem" 
 }

```

If you want to serve different sites, you can change the document root inside the socket conditional:

```
$SERVER["socket"] == ":443" {
    server.document-root = "/srv/ssl" # use your ssl directory here
    ssl.engine                 = "enable"
    ssl.pemfile                = "/etc/lighttpd/certs/www.example.com.pem"  # use the path where you created your pem file
 }

```

or as alternative you can use the scheme conditional to distinguish between secure and normal requests.

```
$HTTP["scheme"] == "https" {
    server.document-root = "/srv/ssl" # use your ssl directory here
    ssl.engine                 = "enable"
    ssl.pemfile                = "/etc/lighttpd/certs/www.example.com.pem"  # use the path where you created your pem file
 }

```

Note that you cannot use the scheme conditional around ssl.engine above, since lighttpd needs to know on what port to enable SSL.

##### Server Name Indication

To use [SNI](http://en.wikipedia.org/wiki/Server_Name_Indication) with lighttpd, simply put additional ssl.pemfile configuration directives inside host conditionals. A default ssl.pemfile is [still required](https://redmine.lighttpd.net/projects/1/wiki/Docs_SSL#Server-Name-Indication-SNI).

```
$HTTP["host"] == "www.example.org" {
    ssl.pemfile = "/etc/lighttpd/certs/www.example.org.pem" 
}

$HTTP["host"] == "mail.example.org" {
    ssl.pemfile = "/etc/lighttpd/certs/mail.example.org.pem" 
}

```

#### Redirect HTTP requests to HTTPS

You should add `"mod_redirect"` in server.modules array in `/etc/lighttpd/lighttpd.conf`:

```
server.modules += ( "mod_redirect" )

$SERVER["socket"] == ":80" {
  $HTTP["host"] =~ "example.org" {
    url.redirect = ( "^/(.*)" => "https://example.org/$1" )
    server.name                 = "example.org" 
  }
}

$SERVER["socket"] == ":443" {
  ssl.engine = "enable" 
  ssl.pemfile = "/etc/lighttpd/ssl/server.pem" 
  server.document-root = "..." 
}

```

To redirect all hosts to their secure equivalents use the following in place of the socket 80 configuration above:

```
$SERVER["socket"] == ":80" {
  $HTTP["host"] =~ ".*" {
    url.redirect = (".*" => "https://%0$0")
  }
}

```

To redirect all hosts for part of the site (e.g. secure or phpmyadmin):

```
$SERVER["socket"] == ":80" {
  $HTTP["url"] =~ "^/secure" {
    url.redirect = ( "^/(.*)" => "https://example.com/$1" )
  }
}

```

### Output Compression

In `/etc/lighttpd/lighttpd.conf` add

```
var.cache_dir           = "/var/cache/lighttpd"

```

Then create directory for a compressed files:

```
# mkdir /var/cache/lighttpd/compress
# chown http:http /var/cache/lighttpd/compress

```

Copy example configuration file:

```
# mkdir /etc/lighttpd/conf.d
# cp /usr/share/doc/lighttpd/config/conf.d/compress.conf /etc/lighttpd/conf.d/

```

Add following in `/etc/lighttpd/lighttpd.conf`:

```
include "conf.d/compress.conf"

```

**Note:** You can not do this (copy compress.conf) and add a needed content in `/etc/lighttpd/lighttpd.conf` instead.

## See also

*   [Lighttpd wiki](http://redmine.lighttpd.net/projects/lighttpd/wiki)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Lighttpd&oldid=412896](https://wiki.archlinux.org/index.php?title=Lighttpd&oldid=412896)"