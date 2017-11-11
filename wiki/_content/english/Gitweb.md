Gitweb is the default web interface that comes with [Git](/index.php/Git "Git") and is the basis for other Git scripts like [cgit](/index.php/Cgit "Cgit") and [gitosis](/index.php/Gitosis "Gitosis").

Gitweb actually supports FCGI natively, so you do not need to wrap it as a CGI script. [[1]](http://repo.or.cz/w/alt-git.git?a=blob_plain;f=gitweb/INSTALL)[[2]](https://sixohthree.com/1402/running-gitweb-in-fastcgi-mode)

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Apache](#Apache)
    *   [2.2 Lighttpd](#Lighttpd)
    *   [2.3 Nginx](#Nginx)
    *   [2.4 Gitweb config](#Gitweb_config)
    *   [2.5 Syntax highlighting](#Syntax_highlighting)
*   [3 Adding repositories](#Adding_repositories)
*   [4 See also](#See_also)

## Installation

To install gitweb you first have to install [git](https://www.archlinux.org/packages/?name=git) and a webserver. Now, if you want to quickly test it, see the help of `git instaweb`. Otherwise, if you want a comprehensive setup, keep reading.

For this example we use [apache](https://www.archlinux.org/packages/?name=apache) but you can also use [nginx](https://www.archlinux.org/packages/?name=nginx), [lighttpd](https://www.archlinux.org/packages/?name=lighttpd) or others.

For all the examples below, you need to [install](/index.php/Install "Install") the [perl-cgi](https://www.archlinux.org/packages/?name=perl-cgi) package. ([FS#45431](https://bugs.archlinux.org/task/45431))

## Configuration

### Apache

Create `/etc/httpd/conf/extra/gitweb.conf`

 `gitweb.conf` 
```
Alias /gitweb "/usr/share/gitweb"
<Directory "/usr/share/gitweb">
    DirectoryIndex gitweb.cgi
    Options ExecCGI
    Require all granted
    <Files gitweb.cgi>
    SetHandler cgi-script
    </Files>
    SetEnv  GITWEB_CONFIG  /etc/gitweb.conf
</Directory>

```

Add the following line to the end of `/etc/httpd/conf/httpd.conf`

```
# gitweb configuration
Include conf/extra/gitweb.conf

```

If Apache refuses to display gitweb, but prints the plain source code of the perl script instead, it is very likely that `cgi_module` has not been loaded by Apache.

In order to resolve this issue, add the following line to `/etc/httpd/conf/httpd.conf`

```
LoadModule cgi_module modules/mod_cgi.so

```

### Lighttpd

Add the following to `/etc/lighttpd/lighttpd.conf`:

```
server.modules += ( "mod_alias", "mod_cgi", "mod_redirect", "mod_setenv" )
url.redirect += ( "^/gitweb$" => "/gitweb/" )
alias.url += ( "/gitweb/" => "/usr/share/gitweb/" )
$HTTP["url"] =~ "^/gitweb/" {
       setenv.add-environment = (
               "GITWEB_CONFIG" => "/etc/gitweb.conf",
               "PATH" => env.PATH
       )
       cgi.assign = ( ".cgi" => "" )
       server.indexfiles = ( "gitweb.cgi" )
}

```

You may also need to add `".css" => "text/css"` to the `mimetype.assign` line for GitWeb to display properly.

### Nginx

Append this location to your nginx configuration (you might want to change the location):

 `/etc/nginx/nginx.conf` 
```
location /gitweb.cgi {
    include fastcgi_params;
    gzip off;
    fastcgi_param   SCRIPT_FILENAME  /usr/share/gitweb/gitweb.cgi;
    fastcgi_param   GITWEB_CONFIG  /etc/gitweb.conf;
    fastcgi_pass    unix:/var/run/fcgiwrap.sock;
}

location / {
    root /usr/share/gitweb;
    index gitweb.cgi;
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

In the end, [start/enable](/index.php/Start/enable "Start/enable") `fcgiwrap.service`.

### Gitweb config

Next we need to make a gitweb config file. Open (or create if it does not exist) the file `/etc/gitweb.conf` and place this in it:

 `/etc/gitweb.conf` 
```
# The directories where your projects are. Must not end with a slash.
our $projectroot = "/path/to/your/repositories"; 

# Base URLs for links displayed in the web interface.
our @git_base_url_list = qw(git://<your_server> [http://git@](http://git@)<your_server>);
```

To enable "blame" view (showing the author of each line in a source file), add the following line:

```
$feature{'blame'}{'default'} = [1];

```

Now the the configuration is done, restart your webserver.

### Syntax highlighting

To enable syntax highlighting with Gitweb, you have to first install the [highlight](https://www.archlinux.org/packages/?name=highlight) package:

When highlight has been installed, simply add this line to your `gitweb.conf`:

```
$feature{'highlight'}{'default'} = [1];

```

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

## See also

*   [How To Install A Public Git Repository On A Debian Server](https://www.howtoforge.com/how-to-install-a-public-git-repository-on-a-debian-server) — HowtoForge page used as the main source for this article.