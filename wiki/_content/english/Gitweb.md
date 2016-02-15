Gitweb is the default web interface provided with [git](/index.php/Git "Git") itself and is the basis for other git scripts like [cgit](/index.php/Cgit "Cgit"), [gitosis](/index.php/Gitosis "Gitosis") and others.

Gitweb actually supports fcgi natively, so you do not need to wrap it as a cgi script. [[1]](http://repo.or.cz/w/alt-git.git?a=blob_plain;f=gitweb/INSTALL)[[2]](https://sixohthree.com/1402/running-gitweb-in-fastcgi-mode)

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Apache 2.2](#Apache_2.2)
        *   [2.1.1 Apache 2.4](#Apache_2.4)
    *   [2.2 Lighttpd](#Lighttpd)
    *   [2.3 Nginx](#Nginx)
    *   [2.4 Gitweb config](#Gitweb_config)
    *   [2.5 Syntax highlighting](#Syntax_highlighting)
*   [3 Adding repositories](#Adding_repositories)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 "An error occurred while reading CGI reply (no response received)" in browser](#.22An_error_occurred_while_reading_CGI_reply_.28no_response_received.29.22_in_browser)
*   [5 See also](#See_also)

## Installation

To install gitweb you first have to install [git](https://www.archlinux.org/packages/?name=git) and a webserver. Now, if you want to quickly test it, see the help of `git instaweb`. Otherwise, if you want a comprehensive setup, keep reading.

For this example we use [apache](https://www.archlinux.org/packages/?name=apache) but you can also use [nginx](https://www.archlinux.org/packages/?name=nginx), [lighttpd](https://www.archlinux.org/packages/?name=lighttpd) or others.

Next you need to link the current gitweb default to your webserver location. In this example the default folder locations are used:

```
# ln -s /usr/share/gitweb /srv/http/gitweb

```

**Note:** You may want to double check the server directory to make sure the symbolic links were made.

## Configuration

### Apache 2.2

Add the following to the end of your `/etc/httpd/conf/httpd.conf`

```
<Directory "/srv/http/gitweb">
   DirectoryIndex gitweb.cgi
   Allow from all
   AllowOverride all
   Order allow,deny
   Options ExecCGI
   <Files gitweb.cgi>
   SetHandler cgi-script
   </Files>
   SetEnv  GITWEB_CONFIG  /etc/conf.d/gitweb.conf
</Directory>

```

If using a virtualhosts configuration, add this to `/etc/httpd/conf/extra/httpd-vhosts.conf`

```
<VirtualHost *:80>
    ServerName gitserver
    DocumentRoot /var/www/gitweb
    <Directory /var/www/gitweb>
       Options ExecCGI +FollowSymLinks +SymLinksIfOwnerMatch
       AllowOverride All
       order allow,deny
       Allow from all
       AddHandler cgi-script cgi
       DirectoryIndex gitweb.cgi
   </Directory>
</VirtualHost>

```

You could also put the configuration in its own config file in `/etc/httpd/conf/extra/` but that is up to you to decide.

#### Apache 2.4

For Apache 2.4 you need to install [mod_perl](https://aur.archlinux.org/packages/mod_perl/) along with [git](https://www.archlinux.org/packages/?name=git) and [apache](https://www.archlinux.org/packages/?name=apache).

Create `/etc/httpd/conf/extra/httpd-gitweb.conf`

```
<IfModule mod_perl.c>
    Alias /gitweb "/usr/share/gitweb"
    <Directory "/usr/share/gitweb">
        DirectoryIndex gitweb.cgi
        Require all granted
        Options ExecCGI
        AddHandler perl-script .cgi
        PerlResponseHandler ModPerl::Registry
        PerlOptions +ParseHeaders
        SetEnv  GITWEB_CONFIG  /etc/conf.d/gitweb.conf
    </Directory>
</IfModule>

```

Add the following line to the modules section of `/etc/httpd/conf/httpd.conf`

```
LoadModule perl_module modules/mod_perl.so

```

Add the following line to the end of `/etc/httpd/conf/httpd.conf`

```
# gitweb configuration
Include conf/extra/httpd-gitweb.conf

```

### Lighttpd

Add the following to `/etc/lighttpd/lighttpd.conf`:

```
server.modules += ( "mod_alias", "mod_cgi", "mod_redirect", "mod_setenv" )
setenv.add-environment = ( "GITWEB_CONFIG" => "/etc/conf.d/gitweb.conf" )
url.redirect += ( "^/gitweb$" => "/gitweb/" )
alias.url += ( "/gitweb/" => "/usr/share/gitweb/" )
$HTTP["url"] =~ "^/gitweb/" {
       cgi.assign = ( ".cgi" => "" )
       server.indexfiles = ( "gitweb.cgi" )
}

```

You may also need to add `".css" => "text/css"` to the `mimetype.assign` line for GitWeb to display properly.

### Nginx

Consider you have symlinked `ln -s /usr/share/gitweb /srv/http`, append this location to your nginx configuration:

 `/etc/nginx/nginx.conf` 

```
location /gitweb/ {
        index gitweb.cgi;
        include fastcgi_params;
        gzip off;
        fastcgi_param   GITWEB_CONFIG  /etc/conf.d/gitweb.conf;
        if ($uri ~ "/gitweb/gitweb.cgi") {
                fastcgi_pass    unix:/var/run/fcgiwrap.sock;
        }
}

```

If you follow [Nginx#CGI implementation](/index.php/Nginx#CGI_implementation "Nginx"), try replacing `include fastcgi_params;` with `include fastcgi.conf;`.

Additionally, we have to install [fcgiwrap](https://www.archlinux.org/packages/?name=fcgiwrap) and [spawn-fcgi](https://www.archlinux.org/packages/?name=spawn-fcgi) and modify the fcgiwrap service file:

 `/usr/lib/systemd/system/fcgiwrap.service` 

```
[Unit]
Description=Simple server for running CGI applications over FastCGI
After=syslog.target network.target

[Service]
Type=forking
Restart=on-abort
PIDFile=/var/run/fcgiwrap.pid
ExecStart=/usr/bin/spawn-fcgi -s /var/run/fcgiwrap.sock -P /var/run/fcgiwrap.pid -u http -g http -- /usr/sbin/fcgiwrap
ExecStop=/usr/bin/kill -15 $MAINPID

[Install]
WantedBy=multi-user.target

```

In the end, enable and restart the services:

```
systemctl enable nginx fcgiwrap
systemctl start nginx fcgiwrap
```

### Gitweb config

Next we need to make a gitweb config file. Open (or create if it does not exist) the file `/etc/conf.d/gitweb.conf` and place this in it:

 `/etc/conf.d/gitweb.conf` 

```
our $git_temp = "/tmp";

# The directories where your projects are. Must not end with a slash.
our $projectroot = "/path/to/your/repositories"; 

# Base URLs for links displayed in the web interface.
our @git_base_url_list = qw(git://<your_server> http://git@<your_server>); 

```

To enable "blame" view (showing the author of each line in a source file), add the following line:

```
$feature{'blame'}{'default'} = [1];

```

Now the the configuration is done, please restart your webserver. For apache:

```
systemctl restart httpd 

```

Or for lighttpd:

```
systemctl restart lighttpd

```

### Syntax highlighting

To enable syntax highlighting with Gitweb, you have to first install the [highlight](https://www.archlinux.org/packages/?name=highlight) package:

When highlight has been installed, simply add this line to your `gitweb.conf`:

 `$feature{'highlight'}{'default'} = [1];` 

Save the file and highlighting should now be enabled.

## Adding repositories

To add a repository go to your repository folder, make your repository like so:

```
mkdir my_repository.git
git init --bare my_repository.git/
cd my_repository.git/
touch git-daemon-export-ok
echo "Short project's description" > description

```

Next open the `config` file and add this:

```
[gitweb]
        owner = Your Name

```

This will fill in the "Owner" field in gitweb. It is not required.

This assumes that you want to have this repository as "central" repository storage where you push your commits to so the git-daemon-export-ok and --bare are here to have minimal overhead and to allow the git daemon to be used on it.

That is all for making a repository. You can now see it on your [http://localhost/gitweb](http://localhost/gitweb) (assuming everything went fine). You do not need to restart apache for new repositories since the gitweb cgi script simply reads your repository folder.

## Troubleshooting

### "An error occurred while reading CGI reply (no response received)" in browser

When browsing [http://localhost/gitweb](http://localhost/gitweb), there is only a one-line message as title. By running `gitweb.cgi` in command line as follows, we can get the complete error message (assuming you have symlinked `ln -s /usr/share/gitweb /srv/http`):

 `$ perl /srv/http/gitweb/gitweb.cgi` 

```
Can't locate CGI.pm in @INC (you may need to install the CGI module) (@INC contains: /usr/lib/perl5/site_perl
 /usr/share/perl5/site_perl /usr/lib/perl5/vendor_perl /usr/share/perl5/vendor_perl /usr/lib/perl5/core_perl 
/usr/share/perl5/core_perl .) at gitweb/gitweb.cgi line 13.

```

To solve this issue, just install [perl-cgi](https://www.archlinux.org/packages/?name=perl-cgi). There is also a bug report: [FS#45431](https://bugs.archlinux.org/task/45431).

## See also

*   [How To Install A Public Git Repository On A Debian Server](http://www.howtoforge.com/how-to-install-a-public-git-repository-on-a-debian-server) — HowtoForge page used as the main source for this article.