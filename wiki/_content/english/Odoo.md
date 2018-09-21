[Odoo](https://www.odoo.com) (formerly known as OpenERP and before that, TinyERP) is a suite of open-source enterprise management applications. Targeting companies of all sizes, the application suite includes billing, accounting, manufacturing, purchasing, warehouse management, and project management.

Odoo features an application server which uses PostgreSQL as database back-end, with a web-based client. Odoo is written in Python, with a highly modular design which allows rapid development of new modules through Open Object RAD. Odoo developers have a strong commitment to free software.

A thriving support and development community has grown up around Odoo, providing free technical support, bug-fixing, new development, and support services. Odoo provides extensive documentation in various electronic formats, as well as hardcopy. The company responsible for development of Odoo earns profits through partnership services with Odoo consultants, and by providing support, training, hosting services, software development, and software quality testing and verification.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Installing Odoo](#Installing_Odoo)
    *   [1.2 Configuring PostgreSQL to run with Odoo](#Configuring_PostgreSQL_to_run_with_Odoo)
    *   [1.3 Configuring Odoo to run with PostgreSQL](#Configuring_Odoo_to_run_with_PostgreSQL)
    *   [1.4 Starting the server](#Starting_the_server)
    *   [1.5 Logging in](#Logging_in)
*   [2 Running Odoo behind a reverse proxy](#Running_Odoo_behind_a_reverse_proxy)
    *   [2.1 Using Nginx](#Using_Nginx)
*   [3 Additional documentation](#Additional_documentation)

## Installation

### Installing Odoo

Install the [odoo](https://aur.archlinux.org/packages/odoo/) package. Please note that the Odoo package comes with a bunch of Python packages available in the [AUR](/index.php/AUR "AUR"). These dependencies and the size of Odoo require much disk space to be used (multiple GBs). If you are building manually in the current directory, please make sure your current directory is on a device with enough free space.

### Configuring PostgreSQL to run with Odoo

Odoo uses PostgreSQL as the database backend. The latter should have been installed with the odoo package as [postgresql](https://www.archlinux.org/packages/?name=postgresql) comes as a dependency.

It is necessary to create a new PostgreSQL user for Odoo. For that log in as the default PostgreSQL superuser, 'postgres', by executing the following command:

*   If you have [sudo](https://www.archlinux.org/packages/?name=sudo) and your username is in `sudoers`:

	 `$ sudo -i -u postgres` 

*   Otherwise:

```
$ su
# su - postgres

```

If the PostgreSQL instance has not been initialized yet, please follow first the [PostgreSQL install process](/index.php/PostgreSQL#Installation "PostgreSQL").

Once logged as the 'postgres' user, create the database user (called *role* in the PostgreSQL ) *odoo* with the command that follows.

*   where *--interactive* is used to prompt for missing role name and attributes rather than using defaults
*   and *--pwprompt'* is used to assign a password to the new role

You will first be asked for a password. For highly secure yet easy to remember passwords, consider using a [Diceware Passphrase](http://world.std.com/~reinhold/diceware.html). Re-enter the password as requested. The next three questions should be answered in sequence with n, y, and n.

```
$ createuser odoo --interactive --pwprompt
Enter password for new role: 
Enter it again: 
Shall the new role be a superuser? (y/n) n
Shall the new role be allowed to create databases? (y/n) y
Shall the new role be allowed to create more new roles? (y/n) n

```

You can also use the following command line to specify the options to skip the interactive questions:

```
[postgres]$ createuser *odoo* --createdb --login --no-superuser --no-createrole --pwprompt

```

Once you are finished answering these questions, type `exit` to return to your regular user.

This completes the required installation and setup of PostgreSQL for use with Odoo under Arch Linux. Additional detailed information about PostgreSQL configuration can be found in the [PostgreSQL](/index.php/PostgreSQL "PostgreSQL") article. By default, PostgreSQL only accepts connections from the local machine. If you plan to run PostgreSQL and Odoo on two different machines, you will need to follow [PostgreSQL#Configure PostgreSQL to be accessible from remote hosts](/index.php/PostgreSQL#Configure_PostgreSQL_to_be_accessible_from_remote_hosts "PostgreSQL").

### Configuring Odoo to run with PostgreSQL

The configuration file of Odoo is located at `/etc/odoo/odoo.conf`. Specify the `db_user` and `db_password` according to the username and password you specified at previous step. If the PostgreSQL server is on a different machine, also edit `db_host`.

```
[options]
; This is the password that allows database operations:
; admin_passwd = admin
db_host = False
db_port = False
db_user = odoo
db_password = False

```

### Starting the server

Ensure PostgreSQL is running and enabled first before running the following commands.

Use the command below to start odoo automatically at boot:

```
# systemctl enable odoo.service

```

Use the command below to start odoo:

```
# systemctl start odoo.service

```

### Logging in

Go to [http://localhost:8069](http://localhost:8069) in your web browser to access the Odoo login page.

## Running Odoo behind a reverse proxy

You can run odoo behind a web server such as [Apache](/index.php/Apache "Apache") or [Nginx](/index.php/Nginx "Nginx") in reverse proxy mode. This is useful for making odoo available in a local network, under a domaine name such as `odoo.mydomain.local`. It is also useful to enable caching for static resources, and reduce the load on your odoo application.

For this to work, you need to make sure that your local DNS-server (such as [BIND](/index.php/BIND "BIND") or [dnsmasq](/index.php/Dnsmasq "Dnsmasq")) resolves the domain name you choose to the web server's IP address. If running on your local machine, you could simply add an entry to `/etc/hosts` like this:

```
127.0.0.1 odoo.mydomain.local

```

### Using Nginx

Refer to [this guide](/index.php/Nginx#Managing_server_entries "Nginx") for how to create virtual hosts in Nginx.

Assuming your local domain is called `mydomain.local`, and odoo is hosted on the same machine as your Nginx server, create a file inside the `servers-available` directory that contains this server block:

 `/etc/nginx/servers-available/odoo` 
```
upstream odoo {
    server 127.0.0.1:8069;
}

server {
    listen 80;
    server_name odoo.mydomain.local;
    root        /usr/share/nginx/html;
    index       index.html index.htm;
    access_log  /var/log/nginx/odoo-mydomain-local.access.log;
    error_log   /var/log/nginx/odoo-mydomain-local.error.log;

    location / {
        proxy_pass  http://odoo;
        # force timeouts if the backend dies
        proxy_next_upstream error timeout invalid_header http_500 http_502 http_503 http_504;
        proxy_redirect off;

        # set headers
        proxy_set_header    Host            $host;
        proxy_set_header    X-Real-IP       $remote_addr;
        proxy_set_header    X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header    X-Forwarded-Proto https;
    }

    # cache some static data in memory for 60mins
    location ~* /web/static/ {
        proxy_cache_valid 200 60m;
        proxy_buffering on;
        expires 864000;
        proxy_pass http://odoo;
    }
}

```

To enable, simple create a symlink:

```
# ln -s /etc/nginx/servers-available/odoo /etc/nginx/servers-enabled/odoo

```

Reload or restart `nginx` service to enable the new configuration.

```
# systemctl restart nginx.service

```

## Additional documentation

As Odoo is a complete enterprise solution, it might be rather complex to use for newcomers. Therefore, reading the [Odoo User Documentation](https://www.odoo.com/documentation/user/9.0/) and [Odoo technical documentation](https://www.odoo.com/documentation/9.0/) is highly advised.