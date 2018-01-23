[Cgit](http://git.zx2c4.com/cgit/) is an attempt to create a fast web interface for the [git](/index.php/Git "Git") version control system, using a built in cache to decrease pressure on the git server.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration of web server](#Configuration_of_web_server)
    *   [2.1 Apache](#Apache)
    *   [2.2 Lighttpd](#Lighttpd)
        *   [2.2.1 Lighttpd sub-domain](#Lighttpd_sub-domain)
    *   [2.3 Nginx](#Nginx)
        *   [2.3.1 Using fcgiwrap](#Using_fcgiwrap)
        *   [2.3.2 Using uwsgi](#Using_uwsgi)
*   [3 Configuration of cgit](#Configuration_of_cgit)
    *   [3.1 Basic Configuration](#Basic_Configuration)
    *   [3.2 Adding repositories](#Adding_repositories)
    *   [3.3 Syntax highlighting](#Syntax_highlighting)
        *   [3.3.1 Using python-pygments](#Using_python-pygments)
        *   [3.3.2 Using highlight](#Using_highlight)
*   [4 Integration](#Integration)
    *   [4.1 Gitosis](#Gitosis)
    *   [4.2 Gitolite](#Gitolite)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 *snapshots* does not show properly](#snapshots_does_not_show_properly)
    *   [5.2 *source-filter* does not work properly](#source-filter_does_not_work_properly)
*   [6 References](#References)

## Installation

Install the [cgit](https://www.archlinux.org/packages/?name=cgit) package.

To use cgit a [web server](/index.php/Category:Web_server "Category:Web server") must be installed on the system, such as [Apache](/index.php/Apache "Apache").

## Configuration of web server

### Apache

You may add the following either to the end of your `/etc/httpd/conf/httpd.conf` file or place it in a separate file inside the `/etc/httpd/conf/extra/` directory.

```
ScriptAlias /cgit "/usr/lib/cgit/cgit.cgi/"
Alias /cgit-css "/usr/share/webapps/cgit/"
<Directory "/usr/share/webapps/cgit/">
   AllowOverride None
   Options None
   Require all granted
</Directory>
<Directory "/usr/lib/cgit/">
   AllowOverride None
   Options ExecCGI FollowSymlinks
   Require all granted
</Directory>

```

Make sure that the cgi module is being loaded in the `httpd.conf` by uncommenting this line:

```
LoadModule cgi_module modules/mod_cgi.so

```

and restart `httpd.service` to apply the changes.

### Lighttpd

The following configuration will let you access cgit through [http://your.server.com/git](http://your.server.com/git) or [http://your.server.com/cgit](http://your.server.com/cgit). The cgit url is not perfect (for example you will see "cgit.cgi" in all repos' url) but works.

Create the file `/etc/lighttpd/conf.d/cgit.conf`:

```
server.modules += ( "mod_cgi", "mod_alias" )

$HTTP["url"] =~ "^/cgit" {
    server.document-root = "/usr/share/webapps/"
    server.indexfiles = ("cgit.cgi")
    cgi.assign = ("cgit.cgi" => "")
    mimetype.assign = ( ".css" => "text/css" )
}

alias.url += (
    "/git" => "/usr/share/webapps/cgit/cgit.cgi",
)
$HTTP["url"] =~ "^/git" {
    cgi.assign = ( "" => "" )
}

```

And include this file in `/etc/lighttpd/lighttpd.conf`:

```
include "conf.d/cgit.conf"

```

and restart lighttpd.

#### Lighttpd sub-domain

This alternative lighttpd configuration will serve Cgit on a sub-domain like git.example.com with optional SSL support, and rewrites creating nice permalinks:

```
   # GIT repository browser
   #$SERVER["socket"] == "127.0.0.1:443" {
   $SERVER["socket"] == "127.0.0.1:80" {
     #ssl.engine                    = "enable"
     #ssl.pemfile                   = "/etc/lighttpd/ssl/git.example.com.pem"

     server.name          = "git.example.com"
     server.document-root = "/usr/share/webapps/cgit"

     index-file.names     = ( "cgit.cgi" )
     cgi.assign           = ( "cgit.cgi" => "/usr/share/webapps/cgit/cgit.cgi" )
     url.rewrite-once     = (
       "^/([^?/]+/[^?]*)?(?:\?(.*))?$"   => "/cgit.cgi?url=$1&$2",
     )
   }

```

### Nginx

#### Using fcgiwrap

The following configuration uses [fcgiwrap](https://www.archlinux.org/packages/?name=fcgiwrap) and will serve Cgit on a subdomain like `git.example.com`.

[Start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") `fcgiwrap.socket`. Then, configure Nginx:

 `/etc/nginx/nginx.conf` 
```
worker_processes          1;

events {
  worker_connections      1024;
}

http {
  include                 mime.types;
  default_type            application/octet-stream;
  sendfile                on;
  keepalive_timeout       65;
  gzip                    on;

  # Cgit
  server {
    listen                80;
    server_name           *git.example.com;*
    root                  /usr/share/webapps/cgit;
    try_files             $uri @cgit;

    location @cgit {
      include             fastcgi_params;
      fastcgi_param       SCRIPT_FILENAME $document_root/cgit.cgi;
      fastcgi_param       PATH_INFO       $uri;
      fastcgi_param       QUERY_STRING    $args;
      fastcgi_param       HTTP_HOST       $server_name;
      fastcgi_pass        unix:/run/fcgiwrap.sock;
    }
  }
}
```

#### Using uwsgi

The following example will setup cgit using the native cgi plugin for uwsgi.

First, install [uwsgi](https://www.archlinux.org/packages/?name=uwsgi) and [uwsgi-plugin-cgi](https://www.archlinux.org/packages/?name=uwsgi-plugin-cgi).

Add below server block to your configuration:

 `/etc/nginx/nginx.conf` 
```
server {
  listen 80;
  server_name git.example.com;
  root /usr/share/webapps/cgit;

  # Serve static files with nginx
  location ~* ^.+(cgit.(css|png)|favicon.ico|robots.txt) {
    root /usr/share/webapps/cgit;
    expires 30d;
  }
  location / {
    try_files $uri @cgit;
  }
  location @cgit {
    gzip off;
    include uwsgi_params;
    uwsgi_modifier1 9;
    uwsgi_pass unix:/run/uwsgi/cgit.sock;
  }
} 

```

Add a uwsgi configuration for cgit.

 `/etc/uwsgi/cgit.ini` 
```
[uwsgi]
master = true
plugins = cgi
socket = /run/uwsgi/%n.sock
uid = http
gid = http
procname-master = uwsgi cgit
processes = 1
threads = 2
cgi = /usr/lib/cgit/cgit.cgi
```

[Enable](/index.php/Enable "Enable") and [start](/index.php/Start "Start") the corresponding socket `uwsgi@cgit.socket`.

## Configuration of cgit

### Basic Configuration

Before you can start adding repositories you will first have to create the basic cgit configuration file at `/etc/cgitrc`.

```
#
# cgit config
#

css=/cgit.css
logo=/cgit.png

# Following lines work with the above Apache config
#css=/cgit-css/cgit.css
#logo=/cgit-css/cgit.png

# Following lines work with the above Lighttpd config
#css=/cgit/cgit.css
#logo=/cgit/cgit.png

# if you do not want that webcrawler (like google) index your site
robots=noindex, nofollow

# if cgit messes up links, use a virtual-root. For example has cgit.example.org/ this value:
virtual-root=/

```

### Adding repositories

Now you can add your repos:

```
#
# List of repositories.
# This list could be kept in a different file (e.g. '/etc/cgitrepos')
# and included like this:
#   include=/etc/cgitrepos
#

repo.url=MyRepo
repo.path=/srv/git/MyRepo.git
repo.desc=This is my git repository

# For a non-bare repository
repo.url=MyOtherRepo
repo.path=/srv/git/MyOtherRepo/.git
repo.desc=That's my other git repository

```

Or else, it is also possible to configure cgit to automatically search for the repo:

```
scan-path=/srv/git/

```

If you use the method above, add the descriptions to `.git/description` file and add the following lines to show the author:

 `.git/config` 
```
[gitweb]
        owner = John Cena <john@riseup.net>
```

If you are coming from gitweb and want to keep the descriptions and owner information, then use:

```
enable-git-config=1

```

For detailed documentation about the available settings in this configuration file, please see the manpage ([cgitrc(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/cgitrc.5)).

### Syntax highlighting

Cgit supports syntax highlighting when viewing blobs. To enable syntax highlighting, you have several options.

#### Using python-pygments

Install [python-pygments](https://www.archlinux.org/packages/?name=python-pygments) and add the filter in `/etc/cgitrc`

```
source-filter=/usr/lib/cgit/filters/syntax-highlighting.py

```

To change the coloring style, modify the `style` argument that is passed to `HtmlFormatter` in the `syntax-highlighting.py` file. For instance, to change the coloring style to 'tango':

```
 formatter = HtmlFormatter(encoding='utf-8', style='tango')

```

To get a list of all coloring styles that are available, do:

```
 $ python
 >>> from pygments.styles import get_all_styles
 >>> list(get_all_styles())
 ['manni', 'igor', 'xcode', 'vim', 'autumn', 'vs', 'rrt', 'native', 'perldoc', 'borland', 'tango', 'emacs', 'friendly', 'monokai', 'paraiso-dark', 'colorful', 'murphy', 'bw', 'pastie', 'paraiso-light', 'trac', 'default', 'fruity']

```

#### Using highlight

Install the [highlight](https://www.archlinux.org/packages/?name=highlight) package.

Copy `/usr/lib/cgit/filters/syntax-highlighting.sh` to `/usr/lib/cgit/filters/syntax-highlighting-edited.sh`. Then, in the copied file, comment out version 2 and comment in version 3. You may want to add `--inline-css` to the options of highlight for a more colorful output without editing cgit's css file.

```
 # This is for version 2
 #exec highlight --force -f -I -X -S "$EXTENSION" 2>/dev/null

 # This is for version 3
 exec highlight --force --inline-css -f -I -O xhtml -S "$EXTENSION" 2>/dev/null

```

Enable the filter in `/etc/cgitrc`

```
source-filter=/usr/lib/cgit/filters/syntax-highlighting-edited.sh

```

**Note:** Editing `/usr/lib/cgit/filters/syntax-highlighting.sh` directly would lose all the modifications as soon as [cgit](https://www.archlinux.org/packages/?name=cgit) is updated.

## Integration

### Gitosis

If you want to integrate with [gitosis](/index.php/Gitosis "Gitosis") you will have to run two commands to give apache permission to look though the folder.

```
# chgrp http /srv/gitosis
# chmod a+rx /srv/gitosis

```

### Gitolite

If you added repositories managed by [gitolite](/index.php/Gitolite "Gitolite") you have to change the permissions, so the web server can access the files.

*   Add the *http* user to the *gitolite* group:
    *   `# usermod -aG gitolite http`
*   Change permission for future repositories:
    *   Edit `/var/lib/gitolite/.gitolite.rc`. Change the `UMASK` to `0027`
    *   See also: [http://gitolite.com/gitolite/gitolite.html#umask](http://gitolite.com/gitolite/gitolite.html#umask)
*   Change permission for the *gitolite* home directory, and existing repositories. Run the following two commands:
    *   `# chmod g+rX /var/lib/gitolite`
    *   `# chmod -R g+rX /var/lib/gitolite/repositories`

## Troubleshooting

### *snapshots* does not show properly

If you have enabled *scan-path* as well as *snapshots*, the order in cgitrc matters. According to [cgit mailing list](http://comments.gmane.org/gmane.comp.version-control.cgit/917), *snapshots* should be specified before *scan-path*

```
snapshots=tar.gz tar.bz2 zip
scan-path=/path/to/your/repositories

```

### *source-filter* does not work properly

If you have enabled *scan-path*, again, the order in cgitrc matters. *source-filter* should be specified before *scan-path*, otherwise it will have no effect.

## References

*   [http://git.zx2c4.com/cgit/](http://git.zx2c4.com/cgit/)
*   [http://git.zx2c4.com/cgit/about/](http://git.zx2c4.com/cgit/about/)
*   [http://git.zx2c4.com/cgit/tree/README](http://git.zx2c4.com/cgit/tree/README)
*   [http://git.zx2c4.com/cgit/tree/cgitrc.5.txt](http://git.zx2c4.com/cgit/tree/cgitrc.5.txt)