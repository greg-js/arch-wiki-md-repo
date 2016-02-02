# WebDAV authentication

## Contents

*   [1 Goals](#Goals)
    *   [1.1 Required packages](#Required_packages)
*   [2 WebDav Configuration](#WebDav_Configuration)
    *   [2.1 Step 1: Edit /etc/httpd/conf/httpd.conf](#Step_1:_Edit_.2Fetc.2Fhttpd.2Fconf.2Fhttpd.conf)
    *   [2.2 Step 2: Create needed directories and assign permissions](#Step_2:_Create_needed_directories_and_assign_permissions)
    *   [2.3 Step 3: Authentication](#Step_3:_Authentication)
    *   [2.4 Step 4: Restart apache](#Step_4:_Restart_apache)

## Goals

The goal of this how to use simple authentication with WebDAV. Please refer to [WebDav](/index.php?title=WebDav&action=edit&redlink=1 "WebDav (page does not exist)") on setting up WebDAV.

### Required packages

*   apache
*   cadaver (for testing)

## WebDav Configuration

### Step 1: Edit /etc/httpd/conf/httpd.conf

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

### Step 2: Create needed directories and assign permissions

```
# mkdir -p /var/log/httpd/DavLock
# touch /var/log/httpd/DavLock/DavLockDB
# chown -R nobody.nobody /var/log/httpd/DavLock
# mkdir -p /home/httpd/html/dav
# chown -R nobody.nobody /home/httpd/html/dav

```

### Step 3: Authentication

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

### Step 4: Restart apache

Restart `httpd.service` to apply any changes.

Retrieved from "[https://wiki.archlinux.org/index.php?title=WebDAV_authentication&oldid=376281](https://wiki.archlinux.org/index.php?title=WebDAV_authentication&oldid=376281)"