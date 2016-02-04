# Seafile

Seafile is an open source cloud storage system, with advanced support for file syncing, privacy protection and teamwork.

Collections of files are called libraries, and each library can be synced separately. A library can be encrypted with a user chosen password. This password is not stored on the server, so even the server admin can't view your file contents.

Seafile lets you create groups with file syncing, wiki, and discussion -- enabling easy collaboration around documents within a team.

## Contents

*   [1 Server](#Server)
    *   [1.1 Installation](#Installation)
    *   [1.2 Setup a server instance](#Setup_a_server_instance)
    *   [1.3 Deploy an instance with Nginx](#Deploy_an_instance_with_Nginx)
    *   [1.4 Upgrading](#Upgrading)
    *   [1.5 Running Seafile GC](#Running_Seafile_GC)
*   [2 Sources](#Sources)

## Server

### Installation

Install [seafile-server](https://aur.archlinux.org/packages/seafile-server/) from the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository")

As root, add a new user to run seafile server instances under:

```
# useradd -m -r -d /srv/seafile -s /usr/bin/nologin seafile

```

### Setup a server instance

Change to the user previously setup in [#Installation](#Installation) (following commands are to be executed as that user unless otherwise stated):

```
$ sudo -u seafile -s /bin/sh

```

As that user, create the directory layout for the new seafile server instance and change directory to it:

```
$ mkdir -p $HOME/example.org/seafile-server
$ cd $HOME/example.org

```

_**Note:**_ **Replace every occurence of 'example.org' on this page with the actual domain of your new server instance**

Determine the appropriate seahub version (it will be shown in the format 'x.y.z-r', e.g. 3.0.2):

```
$ pacman -Qi seafile-server | grep Version

```

Set the SEAFILE_SERVER_VERSION variable to the 'x.y.z' retrieved in the previous step:

```
$ SEAFILE_SERVER_VERSION=3.0.3

```

Download seahub and extract it:

```
$ wget -P seafile-server [https://github.com/haiwen/seahub/archive/v$SEAFILE_SERVER_VERSION-server.tar.gz](https://github.com/haiwen/seahub/archive/v$SEAFILE_SERVER_VERSION-server.tar.gz)
$ tar -xz -C seafile-server -f seafile-server/v$SEAFILE_SERVER_VERSION-server.tar.gz

```

Rename the extracted directory:

```
$ mv seafile-server/seahub-$SEAFILE_SERVER_VERSION-server seafile-server/seahub

```

To create the configuration for the seafile server instance choose and follow the 'setup' section of one of the following options shown in the [seafile manual](http://manual.seafile.com/deploy/README.html):

*   [SQLite](http://manual.seafile.com/deploy/using_sqlite.html)
*   [MySQL](http://manual.seafile.com/deploy/using_mysql.html)

Those initial setup steps can be done with the `seafile-admin` command as the seafile user. Be sure to execute them in the correct directory:

```
$ cd $HOME/example.org
$ seafile-admin setup

```

If you wish to have non-english consistent language support you need to compile your language by executing the following command:

```
$ cd $HOME/example.org/seafile-server/seahub/locale/<yourlanguage>/LC_MESSAGES/
$ msgfmt -o django.mo django.po

```

Next we need to add this default language to the settings now:

```
$ echo "LANGUAGE='<yourlanguage>'" >> $HOME/example.org/seahub_settings.py

```

Now, copy the systemd service for seafile 'seafile-server@.service' from /usr/lib/systemd/system/ to /etc/systemd/system and replace the two occurences of '%h' in it with the actual $HOME for the user setup in [#Installation](#Installation).

If you did not yet setup nginx and if you want to test out seafiles own web-frontend-implementation seahub purely, you have to edit the systemd-service file, were you replaced the '%h' with your $HOME, and delete the --fastcgi parameter from the start script, as fastcgi is not supported with seahub-only.

To manually start your new seafile server, run as root:

```
# systemctl start seafile-server@example.org

```

To automatically start your new seafile server at system startup, run as root:

```
# systemctl enable seafile-server@example.org

```

After starting the seafile server daemon, you can create an admin user for your seafile instance:

```
$ cd $HOME/example.org
$ seafile-admin create-admin

```

### Deploy an instance with Nginx

In order to deploy Seafile's webinterface "seahub" with Nginx, you can use an Nginx configuration similar to this:

```
server {
    listen 80;
    server_name www.example.org example.org;
    rewrite ^/(.*) https://$server_name/$1 permanent;   # force redirect http to https
}

server {
    listen 443;
    ssl on;
    ssl_certificate /etc/ssl/certs/example.org.crt;
    ssl_certificate_key /etc/ssl/private/server.key;
    server_name www.example.org example.org;

    location / {
        fastcgi_pass    127.0.0.1:8000;
        fastcgi_param   SCRIPT_FILENAME     $document_root$fastcgi_script_name;
        fastcgi_param   PATH_INFO           $fastcgi_script_name;

        fastcgi_param   SERVER_PROTOCOL     $server_protocol;
        fastcgi_param   QUERY_STRING        $query_string;
        fastcgi_param   REQUEST_METHOD      $request_method;
        fastcgi_param   CONTENT_TYPE        $content_type;
        fastcgi_param   CONTENT_LENGTH      $content_length;
        fastcgi_param   SERVER_ADDR         $server_addr;
        fastcgi_param   SERVER_PORT         $server_port;
        fastcgi_param   SERVER_NAME         $server_name;

        fastcgi_param   HTTPS on;
        fastcgi_param   HTTP_SCHEME https;
    }

    location /seafhttp {
        rewrite ^/seafhttp(.*)$ $1 break;
        proxy_pass http://127.0.0.1:8082;
        client_max_body_size 0;
    }

    location /media {
        root {ABSOLUTE_PATH_TO_SEAFILE_USER'S_HOME}/example.org/seafile-server/seahub;
    }
}

```

### Upgrading

First, stop each of your seafile server instances (repeat for example.org, foo.bar, etc.) as root:

```
# systemctl stop seafile-server@example.org

```

Upgrade [seafile-server](https://aur.archlinux.org/packages/seafile-server/) from the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository").

Become the user the seafile server instances run as (following commands are to be executed as that user unless otherwise stated):

```
$ sudo -u seafile -s

```

Repeat the following for each seafile server instance:

	Change directory to the server instance's 'seafile-server' subdirectory:

```
$ cd /srv/seafile/example.org/seafile-server

```

	Run the preupgrade script (Or do the steps by hand, see [the Seafile wiki](https://github.com/haiwen/seafile/wiki/Build-and-deploy-seafile-server-from-source)):

```
$ seahub-preupgrade

```

	Run the appropriate seafile/seahub upgrade script from the upgrade subdirectory:

	For a minor upgrade (x.y.a to x.y.b with a < b):

```
$ ./upgrade/minor-upgrade.sh

```

	For a major upgrade (x.y.a to z.w.b with x < z || y < w):

```
$ ./upgrade/upgrade_x.y_z.w.sh

```

	Repeat the steps for language mentioned in the installation guide

Lastly, start each of your seafile server instances again (repeat for example.org, foo.bar, etc.) as root:

```
# systemctl start seafile-server@example.org

```

### Running Seafile GC

To release storage space held by unused blocks, you will want to run Seafile's garbage collector.

Specifically, the GC program will remove:

*   blocks belonging to nonexistent libraries
*   out-dated blocks based on that library's history length limits

First, make sure to shutdown the Seafile program on your server. For Professional Edition v.3.1.11 on, online GC operation is supported.

Now, to see how much garbage will be collected before making changes:

```
$ seafserv-gc -c /srv/seafile/example.org/ccnet -d /srv/seafile/example.org/seafile-data --dry-run

```

If the output looks okay, proceed to run the same command without the --dry-run argument.

## Sources

*   [http://manual.seafile.com/deploy/README.html](http://manual.seafile.com/deploy/README.html)
*   [http://manual.seafile.com/deploy/deploy_with_nginx.html](http://manual.seafile.com/deploy/deploy_with_nginx.html)
*   [http://manual.seafile.com/maintain/seafile_gc.html](http://manual.seafile.com/maintain/seafile_gc.html)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Seafile&oldid=400844](https://wiki.archlinux.org/index.php?title=Seafile&oldid=400844)"