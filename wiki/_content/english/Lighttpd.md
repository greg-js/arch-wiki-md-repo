[Lighttpd](https://www.lighttpd.net/) is "a secure, fast, compliant, and very flexible [web-server](https://en.wikipedia.org/wiki/Web_server "wikipedia:Web server") that has been optimized for high-performance environments. It has a very low memory footprint compared to other webservers and takes care of cpu-load. Its advanced feature-set ([FastCGI](https://en.wikipedia.org/wiki/FastCGI "wikipedia:FastCGI"), [CGI](https://en.wikipedia.org/wiki/Common_Gateway_Interface "wikipedia:Common Gateway Interface"), Auth, Output-Compression, URL-Rewriting and many more) make lighttpd the perfect webserver-software for every server that suffers load problems."

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Basic setup](#Basic_setup)
        *   [2.1.1 Basic logging](#Basic_logging)
        *   [2.1.2 Enabling https via SSL](#Enabling_https_via_SSL)
            *   [2.1.2.1 Self-signed](#Self-signed)
            *   [2.1.2.2 Let's Encrypt](#Let.27s_Encrypt)
        *   [2.1.3 Password protecting a directory](#Password_protecting_a_directory)
    *   [2.2 CGI](#CGI)
    *   [2.3 FastCGI](#FastCGI)
        *   [2.3.1 PHP](#PHP)
            *   [2.3.1.1 Using php-cgi](#Using_php-cgi)
            *   [2.3.1.2 Using php-fpm](#Using_php-fpm)
        *   [2.3.2 Python FastCGI](#Python_FastCGI)
            *   [2.3.2.1 Server name indication](#Server_name_indication)
        *   [2.3.3 Redirect http requests to https](#Redirect_http_requests_to_https)
    *   [2.4 Output compression](#Output_compression)
*   [3 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [lighttpd](https://www.archlinux.org/packages/?name=lighttpd) package.

## Configuration

### Basic setup

The lighttpd configuration file is: `/etc/lighttpd/lighttpd.conf`. By default it should produce a working test page.

To check your `lighttpd.conf` for bugs you can use this command (helps finding misconfigurations very quickly):

```
$ lighttpd -t -f /etc/lighttpd/lighttpd.conf

```

A more thorough preflight check is also available:

```
$ lighttpd -tt -f /etc/lighttpd/lighttpd.conf

```

The default configuration file specifies `/srv/http/` as the document directory served. To test the installation, create a dummy file:

 `/srv/http/index.html`  `Hello world!` 

Then [start/enable](/index.php/Start/enable "Start/enable") the `lighttpd.service` and point your browser to `localhost`, where you should see the test page.

Example configuration files are available in `/usr/share/doc/lighttpd/`.

#### Basic logging

Lighttpd can write out both errors and access to log files. To enable both of the logging options, edit `/etc/lighttpd/lighttpd.conf` as follows:

```
server.modules += (
   "mod_access",
   "mod_accesslog",
)

server.errorlog   = "/var/log/lighttpd/error.log"
accesslog.filename = "/var/log/lighttpd/access.log"

```

#### Enabling https via SSL

**Warning:** Users planning to implementing SSL/TLS, should know that some variations and implementations are vulnerable to attack. See the [OpenSSL](/index.php/OpenSSL "OpenSSL") article for details.

**Tip:**

*   Mozilla has an SSL [configuration generator](https://mozilla.github.io/server-side-tls/ssl-config-generator/) that can be used with lighttpd.
*   After setting up SSL, you can use Qualys SSL Labs' [SSL Server Check](https://www.ssllabs.com/ssltest/index.html) to check your configuration.

##### Self-signed

Self-signed SSL Certificates can be generated assuming [openssl](https://www.archlinux.org/packages/?name=openssl) is installed on the system as follows:

```
# mkdir /etc/lighttpd/certs
# openssl req -x509 -nodes -days 7300 -newkey rsa:2048 -sha256 -keyout /etc/lighttpd/certs/server.pem -out /etc/lighttpd/certs/server.pem
# chmod 600 /etc/lighttpd/certs/server.pem

```

Modify `/etc/lighttpd/lighttpd.conf` adding the following lines to enable https:

```
$SERVER["socket"] == ":443" {
    ssl.engine                  = "enable" 
    ssl.pemfile                 = "/etc/lighttpd/certs/server.pem" 
 }

```

##### Let's Encrypt

Alternatively, generate a certificate signed by [Let's Encrypt](/index.php/Let%27s_Encrypt "Let's Encrypt"). After following the instruction for manual certificate generation, combine the generated `privkey.pem` and `cert.pem` into one file:

```
# cat /etc/letsencrypt/live/*domain*/{privkey.pem,cert.pem} > /etc/letsencrypt/live/*domain*/combined.pem

```

[Edit](/index.php/Edit "Edit") `/etc/lighttpd/lighttpd.conf` by adding the following lines:

```
$SERVER["socket"] == ":443" {
    ssl.engine                  = "enable" 
    ssl.pemfile                 = "/etc/letsencrypt/live/*domain*/combined.pem"
    ssl.ca-file                 = "/etc/letsencrypt/live/*domain*/chain.pem"
}

```

#### Password protecting a directory

Note that this module requires [libmariadbclient](https://www.archlinux.org/packages/?name=libmariadbclient) to be installed. A passwd file which is lighttpd's equivalent to the system's `/etc/passwd` is needed for user authentication. The setup requires a specific format and md5sum hashed password but users can quickly and easily create an entry using the following as an example:

```
$ user=foo
$ password=b@R102
$ realm='Password Required'
$ hash=`echo -n "$user:$realm:$pass" | md5sum | cut -b -32`

# echo "$user:$realm:$hash" >> /etc/lighttpd/lighttpd.user

```

Modify `/etc/lighttpd/lighttpd.conf` adding the following lines to enable the directory protection:

```
server.modules = (
   "mod_auth",
 )

auth.debug = 2
auth.backend                = "htdigest"
auth.backend.htdigest.userfile = "/etc/lighttpd/lighttpd.user"

# note this entry is relative to the server.document-root
auth.require = ( "/secret" =>
   (
    "method" => "basic",
    "realm" => "Password Required",
    "require" => "user=foo"
   )
)

```

**Note:** The realm and user entered into `/etc/lighttpd/lighttpd.conf` must match the values chosen in `/etc/lighttpd/lighttpd.user` for authentication to work.

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

##### Using php-cgi

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

Make lighttpd use the new configuration file by appending the following line to your lighttpd configuration file:

 `/etc/lighttpd/lighttpd.conf` 
```
include "conf.d/fastcgi.conf"

```

**Note:** Remember that the order in which the modules are loaded is important, the correct order is listed in `/usr/share/doc/lighttpd/config/modules.conf`.

[Reload](/index.php/Reload "Reload") lighttpd.

**Note:**

*   If you receive errors like *No input file found* when attempting to access php files, there are several possible explanations. See [this FAQ](https://redmine.lighttpd.net/projects/1/wiki/frequentlyaskedquestions#I-get-the-error-No-input-file-specified-when-trying-to-use-PHP) for more information.
*   Make sure that no other module (e.g. `mod_cgi`) will try to handle the *.php* extension.

##### Using php-fpm

There is no adaptive spawning anymore in recent lighttpd releases. For dynamic management of PHP processes, you can install [php-fpm](https://www.archlinux.org/packages/?name=php-fpm) and then [start](/index.php/Start "Start") and enable `php-fpm.service`.

**Note:** You can configure the number of servers in the pool and tweak other configuration options by editing the file `/etc/php/php-fpm.conf`. More details on *php-fpm* can be found on the [php-fpm website](http://php-fpm.org/). Remember that when you make changes to `/etc/php/php.ini` you will need to restart `php-fpm.service`.

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

#### Python FastCGI

**Note:**

*   lighttpd supports Python WSGI protocol: [HowToPythonWSGI](https://redmine.lighttpd.net/projects/lighttpd/wiki/HowToPythonWSGI).
*   The following method will not work with Python 3 because *Flup* library is only available for Python 2\. If you want to use Python 3, you should refer to [#CGI](#CGI) section.

Install and configure FastCGI (see [#FastCGI](#FastCGI) above).

Install [python2-flup](https://aur.archlinux.org/packages/python2-flup/).

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

##### Server name indication

To use [SNI](https://en.wikipedia.org/wiki/Server_Name_Indication "wikipedia:Server Name Indication") with lighttpd, simply put additional ssl.pemfile configuration directives inside host conditionals. A default ssl.pemfile is [still required](https://redmine.lighttpd.net/projects/1/wiki/Docs_SSL#Server-Name-Indication-SNI).

```
$HTTP["host"] == "www.example.org" {
    ssl.pemfile = "/etc/lighttpd/certs/www.example.org.pem" 
}

$HTTP["host"] == "mail.example.org" {
    ssl.pemfile = "/etc/lighttpd/certs/mail.example.org.pem" 
}

```

#### Redirect http requests to https

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
  ssl.pemfile = "/etc/lighttpd/certs/server.pem" 
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

### Output compression

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

*   [Lighttpd wiki](https://redmine.lighttpd.net/projects/lighttpd/wiki)