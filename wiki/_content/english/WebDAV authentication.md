This article outlines how to use simple authentication with [WebDAV](/index.php/WebDAV "WebDAV").

### Required packages

*   apache
*   cadaver (for testing)

## WebDav Configuration

1) Edit `/etc/httpd/conf/httpd.conf`:

```
DAVLockDB /var/log/httpd/DavLock/DavLockDB
<Location /dav>
DAV On
AuthType Digest
AuthName "WebDAV"
AuthUserFile /etc/httpd/conf/passwd
Require user foo
</Location>

```

2) Create needed directories and assign permissions

```
# mkdir -p /var/log/httpd/DavLock
# touch /var/log/httpd/DavLock/DavLockDB
# chown -R nobody.nobody /var/log/httpd/DavLock
# mkdir -p /home/httpd/html/dav
# chown -R nobody.nobody /home/httpd/html/dav

```

3) Authentication

There are numerous different protocols you can use:

*   plain
*   digest
*   others

This is an example for using digest (make sure it is enabled in httpd.conf)

 `htdigest -c /etc/httpd/conf/passwd WebDAV foo` 

Please make sure that the path is identical to the one you entered in your httpd.conf. Also when using digest you have to enter the AuthName from httpd.conf. For plain authentication you would not need this.

With the above setup the user *foo* is required for everything.

If you want to permit everybody to read, you could use this in your httpd.conf

```
<Location /dav>
DAV On
AuthType Digest
AuthName "WebDAV"
AuthUserFile /etc/httpd/conf/passwd
<LimitExcept GET HEAD OPTIONS PROPFIND>
require user foo
</LimitExcept>
</Location>

```

4) Restart apache (`httpd.service`) to apply the changes.