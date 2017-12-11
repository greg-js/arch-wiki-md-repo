[WebDAV](https://en.wikipedia.org/wiki/WebDAV "wikipedia:WebDAV") *(Web Distributed Authoring and Versioning)* is an extension of HTTP 1.1 and therefore can be considered to be a procotol. It contains a set of concepts and accompanying extension methods to allow read and write across the HTTP 1.1 protocol. Instead of using [NFS](/index.php/NFS "NFS") or [SMB](/index.php/SMB "SMB"), WebDAV offers file transfers via HTTP.

The goal of this how to is to setup a simple WebDAV configuration using a [web server](/index.php/Category:Web_server "Category:Web server").

## Contents

*   [1 Server](#Server)
    *   [1.1 Apache](#Apache)
    *   [1.2 Nginx](#Nginx)
*   [2 Client](#Client)
    *   [2.1 Cadaver](#Cadaver)
    *   [2.2 Thunar](#Thunar)
*   [3 Authentication](#Authentication)
    *   [3.1 Apache](#Apache_2)

## Server

### Apache

Install the [Apache HTTP Server](/index.php/Apache_HTTP_Server "Apache HTTP Server").

Uncomment the modules for DAV:

```
LoadModule dav_module modules/mod_dav.so
LoadModule dav_fs_module modules/mod_dav_fs.so
LoadModule dav_lock_module modules/mod_dav_lock.so

```

Add the following line to `/etc/httpd/conf/httpd.conf`.

```
DAVLockDB /home/httpd/DAV/DAVLock

```

Make sure you add it outside of any other directives, for instance right under the `DocumentRoot` definition.

Next, add the following (also outside of any directives):

```
Alias /dav "/home/httpd/html/dav"

<Directory "/home/httpd/html/dav">
  DAV On
  AllowOverride None
  Options Indexes FollowSymLinks
  Require all granted
</Directory>

```

Create the directory:

```
# mkdir -p /home/httpd/DAV

```

Check the permissions of DavLockDB's directory and ensure it is writable by the webserver [user](/index.php/User "User") `http`:

```
# chown -R http:http /home/httpd/DAV
# mkdir -p /home/httpd/html/dav
# chown -R http:http /home/httpd/html/dav

```

### Nginx

Install the mainline variant of [nginx](/index.php/Nginx "Nginx") and [nginx-mainline-mod-dav-ext](https://aur.archlinux.org/packages/nginx-mainline-mod-dav-ext/).

At the top of your `/etc/nginx/nginx.conf` and outside any blocks, add

```
load_module /usr/lib/nginx/modules/ngx_http_dav_ext_module.so;

```

Add a new `location` for WebDAV to your `server` block, for example:

```
location /dav {
    root   /srv/http;

    dav_methods PUT DELETE MKCOL COPY MOVE;
    dav_ext_methods PROPFIND OPTIONS;

    # Adjust as desired:
    dav_access all:rw;
    client_max_body_size 0;
    create_full_put_path on;
    client_body_temp_path /srv/client-temp;
    autoindex on;

    allow 192.168.178.0/24;
    deny all;
}

```

The above example requires the directories `/srv/http/dav` and `/srv/client-temp` to exist.

You may want to use bind mounts to make other directories accessible via WebDAV.

## Client

### Cadaver

[Install](/index.php/Install "Install") the package [cadaver](https://www.archlinux.org/packages/?name=cadaver).

After installation, test the WebDAV server:

```
# cadaver [http://localhost/dav](http://localhost/dav)
dav:/dav/> mkcol test
Creating `test': succeeded.
dav:/dav/> ls
Listing collection `/dav/': succeeded.
Coll: test

```

### Thunar

In [Thunar](/index.php/Thunar "Thunar") just press `Ctrl+l` and enter the address with *dav* or *davs* protocol specified:

```
davs://webdav.yandex.ru

```

## Authentication

There are numerous different protocols you can use:

*   plain
*   digest
*   others

### Apache

Using digest:

```
# basic form: htdigest -c /path/to/file AuthName username
htdigest -c /etc/httpd/conf/passwd WebDAV **username**

```

**Note:** Make sure digest authentication is enabled in `httpd.conf` by the presence of this entry: `LoadModule auth_digest_module modules/mod_auth_digest.so`

Using plain:

```
# basic form: htpasswd -c /path/to/file username
htpasswd -c /etc/httpd/conf/passwd **username**

```

Next, `httpd.conf` must be edited to enable authentication. One method would be to require the user `foo` for everything:

```
<Directory "/home/httpd/html/dav">
  DAV On
  AllowOverride None
  Options Indexes FollowSymLinks
  AuthType Digest # substitute "Basic" for "Digest" if you used htpasswd above
  AuthName "WebDAV"
  AuthUserFile /etc/httpd/conf/passwd
  Require user foo
</Directory>

```

**Note:** `AuthName` must match the name passed when using the `htdigest` command for digest authentication. For basic/plain authentication, this line may be removed. Also, make sure that the `AuthUserFile` path matches that used with the `htdigest` or `htpasswd` commands above

If you want to permit everybody to read, you could use this in your httpd.conf

```
<Directory "/home/httpd/html/dav">
  DAV On
  AllowOverride None
  Options Indexes FollowSymLinks
  AuthType Digest # substitute "Basic" for "Digest" if you used htpasswd above
  AuthName "WebDAV"
  AuthUserFile /etc/httpd/conf/passwd
  Require all granted
  <LimitExcept GET HEAD OPTIONS PROPFIND>
    Require user foo
  </LimitExcept>
</Directory>

```

Do not forget to restart apache after making changes!

```
# systemctl restart httpd

```