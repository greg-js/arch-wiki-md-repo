# Apache and FastCGI

## Contents

*   [1 Installation](#Installation)
*   [2 mod_fastcgi](#mod_fastcgi)
*   [3 mod_fcgid](#mod_fcgid)
*   [4 Troubleshooting](#Troubleshooting)
*   [5 See also](#See_also)

## Installation

There are two FastCGI modules for Apache:

*   [mod_fastcgi](http://www.fastcgi.com/mod_fastcgi/docs/mod_fastcgi.html)
*   [mod_fcgid](http://fastcgi.coremail.cn/index.htm)

They both have permissive licenses (custom for mod_fastcgi and GPL for mod_fcgid) and they are both available in the [official repositories](/index.php/Official_repositories "Official repositories").

Apache 2.4 (available in the [official repositories](/index.php/Official_repositories "Official repositories") as [apache](https://www.archlinux.org/packages/?name=apache)) now provides an official module, [mod_proxy_fcgi](http://httpd.apache.org/docs/2.4/mod/mod_proxy_fcgi.html). See [configuration example for php-fpm](http://wiki.apache.org/httpd/PHP-FPM).

## mod_fastcgi

[Install](/index.php/Install "Install") [mod_fastcgi](https://www.archlinux.org/packages/?name=mod_fastcgi) from the official repositories.

First you need to load the fastcgi module. Make sure that the following is **present** and **uncommented** in your `httpd.conf`:

```
LoadModule fastcgi_module modules/mod_fastcgi.so

```

Then you need to tell Apache when to use FastCGI.

For example you can ask Apache to treat all .fcgi files as fastcgi applications:

```
<IfModule fastcgi_module>
  AddHandler fastcgi-script .fcgi # you can put whatever extension you want
</IfModule>

```

Remember that standard CGI restrictions apply, files must be in an ExecCGI enabled directory to execute.

## mod_fcgid

Install [mod_fcgid](https://www.archlinux.org/packages/?name=mod_fcgid) from the official repositories.

First you need to load the fastcgi module. Make sure that the following is **present** and **uncommented** in your `httpd.conf`:

```
LoadModule fcgid_module modules/mod_fcgid.so

```

Then you need to tell Apache when to use FastCGI.

For example you can ask Apache to treat all .fcgi files as fastcgi applications:

```
<IfModule fcgid_module>
  AddHandler fcgid-script .fcgi # you can put whatever extension you want
</IfModule>

```

Remember that standard CGI restrictions apply, files must be in an ExecCGI enabled directory to execute.

## Troubleshooting

It doesn't work? Apache error log (`/var/log/httpd/error_log`) should help you find the problem.

## See also

*   [lighttpd#FastCGI](/index.php/Lighttpd#FastCGI "Lighttpd")

Retrieved from "[https://wiki.archlinux.org/index.php?title=Apache_and_FastCGI&oldid=412040](https://wiki.archlinux.org/index.php?title=Apache_and_FastCGI&oldid=412040)"