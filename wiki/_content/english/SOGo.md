[SOGo](http://www.sogo.nu/) provides a rich AJAX-based Web interface and supports multiple native clients through the use of standard protocols such as CalDAV, CardDAV and GroupDAV, as well as Microsoft ActiveSync.

This article explains how to setup a groupware server using a SOGo backend. While other MTAs and IMAP servers can be used, Postfix is used for the MTA and Dovecot for the IMAP/POP server.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Considerations](#Considerations)
    *   [1.2 Prerequisites](#Prerequisites)
*   [2 Initial web server configuration](#Initial_web_server_configuration)
    *   [2.1 Apache](#Apache)
    *   [2.2 nginx](#nginx)
    *   [2.3 Start and test web access](#Start_and_test_web_access)
*   [3 SOGo database configuration](#SOGo_database_configuration)
    *   [3.1 MySQL/MariaDB](#MySQL.2FMariaDB)
        *   [3.1.1 Migrating from a previous PostgreSQL configuration](#Migrating_from_a_previous_PostgreSQL_configuration)
    *   [3.2 PostgreSQL](#PostgreSQL)
*   [4 Configuring user databases](#Configuring_user_databases)
    *   [4.1 Active Directory](#Active_Directory)
    *   [4.2 MySQL/MariaDB](#MySQL.2FMariaDB_2)
    *   [4.3 OpenLDAP](#OpenLDAP)
    *   [4.4 PostgreSQL](#PostgreSQL_2)
*   [5 Postfix configuration](#Postfix_configuration)
    *   [5.1 Basic configuration](#Basic_configuration)
    *   [5.2 User sources](#User_sources)
        *   [5.2.1 Active Directory](#Active_Directory_2)
        *   [5.2.2 Maria DB](#Maria_DB)
        *   [5.2.3 OpenLDAP](#OpenLDAP_2)
        *   [5.2.4 PostgreSQL](#PostgreSQL_3)
*   [6 Dovecot configurtion](#Dovecot_configurtion)
    *   [6.1 Basic configuration](#Basic_configuration_2)
    *   [6.2 User sources](#User_sources_2)
        *   [6.2.1 Active Directory](#Active_Directory_3)
        *   [6.2.2 Maria DB](#Maria_DB_2)
        *   [6.2.3 OpenLDAP](#OpenLDAP_3)
        *   [6.2.4 PostgreSQL](#PostgreSQL_4)
*   [7 SOGo configuration](#SOGo_configuration)
    *   [7.1 Basic configuration](#Basic_configuration_3)
    *   [7.2 User sources](#User_sources_3)
        *   [7.2.1 Active Directory](#Active_Directory_4)
        *   [7.2.2 Maria DB](#Maria_DB_3)
        *   [7.2.3 OpenLDAP](#OpenLDAP_4)
        *   [7.2.4 PostgreSQL](#PostgreSQL_5)
*   [8 Web server final configuration](#Web_server_final_configuration)
    *   [8.1 Apache](#Apache_2)
    *   [8.2 nginx](#nginx_2)

## Installation

### Considerations

SOGo can use many different sources for user authentication including, but not limited to, Active Directory, OpenLDAP, MySQL/MariaDB, PostgreSQL, and probably many others if you include PAM. This article will focus on using a centrally managed user database (following on from the [Samba 4 Active Directory domain controller](/index.php/Samba_4_Active_Directory_domain_controller "Samba 4 Active Directory domain controller") article initially -- hopefully others will contribute OpenLDAP/MySQL/PostgreSQL user configs) for both authentication, and to provide a global address list.

Additionally, either [mariadb](https://www.archlinux.org/packages/?name=mariadb) or [postgresql](https://www.archlinux.org/packages/?name=postgresql) must be used to store the users' calendars and address books. As of this writing, the SOGo documentation has a clear preference for MariaDB (or MySQL), but if you have an existing PostgreSQL installation, it makes sense to use it. Other SQL implementations might be supported as well, but are not currently covered.

### Prerequisites

[Install](/index.php/Install "Install") the needed prerequisite packages [dovecot](https://www.archlinux.org/packages/?name=dovecot), [mariadb](https://www.archlinux.org/packages/?name=mariadb), [pigeonhole](https://www.archlinux.org/packages/?name=pigeonhole), [postfix](https://www.archlinux.org/packages/?name=postfix), [postgresql](https://www.archlinux.org/packages/?name=postgresql), [mysql-python](https://www.archlinux.org/packages/?name=mysql-python) and either [apache](https://www.archlinux.org/packages/?name=apache) or [nginx](https://www.archlinux.org/packages/?name=nginx) from the [official repositories](/index.php/Official_repositories "Official repositories"), and [python2-sievelib](https://aur.archlinux.org/packages/python2-sievelib/), [sogo](https://aur.archlinux.org/packages/sogo/), and [sope](https://aur.archlinux.org/packages/sope/) from the [AUR](/index.php/AUR "AUR").

## Initial web server configuration

### Apache

If using [Apache](/index.php/Apache_HTTP_Server "Apache HTTP Server") for the web server, add SOGo to the Apache configuration appending the following lines at the end of `/etc/httpd/conf/httpd.conf`:

```
...
# Include SOGo configuration
include conf/extra/SOGo.conf

```

Enable mod_proxy_html in the `/etc/httpd/conf/httpd.conf`:

```
# cp /etc/httpd/conf/httpd.conf{,.bak}
# sed /mod_proxy_html\.so/s/#// -i /etc/httpd/conf/httpd.conf

```

Edit the `/etc/httpd/conf/extra/SOGo.conf` file and modify the following lines (replace **mail.domain.tld**):

```
...
## adjust the following to your configuration
  RequestHeader set "x-webobjects-server-port" "443"
  RequestHeader set "x-webobjects-server-name" "**mail.domain.tld**"
  RequestHeader set "x-webobjects-server-url" "https://**mail.domain.tld**"
...

```

### nginx

If using [nginx](/index.php/Nginx "Nginx") for the web server, add the following to `/etc/nginx/nginx.conf`:

```
   server {
       listen 443;
       root /usr/lib/GNUstep/SOGo/WebServerResources/;
       server_name **mail.domain.tld**
       server_tokens off;
       client_max_body_size 100M;
       index  index.php index.html index.htm;
       autoindex off;
       ssl on;
       ssl_certificate path **/path/to/your/certfile**; #eg. /etc/ssl/certs/keyfile.crt
       ssl_certificate_key **/path/to/your/keyfile**; #eg /etc/ssl/private/keyfile.key
       ssl_ciphers 'AES128+EECDH:AES128+EDH:!aNULL';
       ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
       ssl_session_cache shared:SSL:10m;
       #optional ssl_stapling on;
       #optional ssl_stapling_verify on;
       #optional ssl_trusted_certificate /etc/ssl/private/cacert-stapeling.pem; 
       #optional resolver 8.8.4.4 8.8.8.8 valid=300s;
       #optionalresolver_timeout 10s;
       ssl_prefer_server_ciphers on;
       #optional ssl_dhparam /etc/ssl/certs/dhparam.pem;
       #optional add_header Strict-Transport-Security max-age=63072000;
       #optional add_header X-Frame-Options DENY;
       #optional add_header X-Content-Type-Options nosniff;
       location = / {
               rewrite ^ https://$server_name/SOGo;
               allow all;
       }
       location = /principals/ {
               rewrite ^ https://$server_name/SOGo/dav;
               allow all;
       }
       location ^~/SOGo {
               proxy_pass http://127.0.0.1:20000;
               proxy_redirect http://127.0.0.1:20000 default;
               # forward user's IP address
               proxy_set_header X-Real-IP $remote_addr;
               proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
               proxy_set_header Host $host;
               proxy_set_header x-webobjects-server-protocol HTTP/1.0;
               proxy_set_header x-webobjects-remote-host 127.0.0.1;
               proxy_set_header x-webobjects-server-name $server_name;
               proxy_set_header x-webobjects-server-url $scheme://$host;
               proxy_connect_timeout 90;
               proxy_send_timeout 90;
               proxy_read_timeout 90;
               proxy_buffer_size 4k;
               proxy_buffers 4 32k;
               proxy_busy_buffers_size 64k;
               proxy_temp_file_write_size 64k;
               client_max_body_size 50m;
               client_body_buffer_size 128k;
               break;
       }
       location /SOGo.woa/WebServerResources/ {
               alias /usr/lib/GNUstep/SOGo/WebServerResources/;
               allow all;
       }
       location /SOGo/WebServerResources/ {
               alias /usr/lib/GNUstep/SOGo/WebServerResources/;
               allow all;
       }
       location ^/SOGo/so/ControlPanel/Products/([^/]*)/Resources/(.*)$ {
               alias /usr/lib/GNUstep/SOGo/$1.SOGo/Resources/$2;
       }
       location ^/SOGo/so/ControlPanel/Products/[^/]*UI/Resources/.*\.(jpg|png|gif|css|js)$ {
               alias /usr/lib/GNUstep/SOGo/$1.SOGo/Resources/$2;
       }
   }

```

### Start and test web access

Create the state directory and start services:

```
# mkdir /var/run/sogo
# chown sogo:sogo /var/run/sogo
# chown sogo:sogo /etc/sogo/sogo.conf
# chmod 0644 /etc/sogo/sogo.conf

```

Then enable and start the `sogo` and either `httpd` or `nginx` services.

Open a browser and go to http://**mail.domain.tld**/SOGo/ but do not try to login just yet, just verify that you can connect and get the login screen.

## SOGo database configuration

### MySQL/MariaDB

If you haven't already done so, create the first MySQL database with the following command:

```
# mysql_install_db --user=mysql --basedir=/usr/ --ldata=/var/lib/mysql/

```

Enable and start `mysqld`, then enter the MySQL shell as the root user:

```
# mysql -u root

```

At the mysql prompt, enter the following commands (replace **SogoPW** with a secure password):

```
CREATE DATABASE sogo;
CREATE USER 'sogo'@'localhost' IDENTIFIED BY '**SogoPW'**;
GRANT ALL PRIVILEGES ON `sogo`.* TO 'sogo'@'localhost' WITH GRANT OPTION;
FLUSH PRIVILEGES;

```

#### Migrating from a previous PostgreSQL configuration

If you had previously used PostgreSQL, you can migrate user data to MySQL/MariaDB using sogo-tool to backup and restore. Details are obviously site specific, but this example should work for most. Backup the full sogo-database with the following commands:

```
# mkdir /root/sogo-backup
# sogo-tool backup /root/sogo-backup ALL

```

Now stop the sogo daemon, stop postgresql (if not used for other purposes), and reconfigure sogo (/etc/sogo/sogo.conf) using both the sogo user and sogo database keeping the last path element (see example below).

To restore all user data, run the following commands:

```
# for user in `ls -d /root/sogo-backup/*`
  do
      sogo-tool restore -f /root/sogo-backup $(basename $user)
  done

```

Simply restart sogo to continue using the MySQL/MariaDB.

### PostgreSQL

If you've elected to use PostgreSQL over MySQL/MariaDB, the old instructions have been left for convenience. If this is a new installation, it is recommended that you use only MySQL/MariaDB for sogo/openchange data.

Initialize the default database and start PostgreSQl (be sure to replace **en_US.UTF-8** with the correct locale for your installation):

```
# mkdir -p /var/lib/postgres/data
# chown -R postgres:postgres /var/lib/postgres
# su - postgres -c "initdb --locale **en_US.UTF-8** -D '/var/lib/postgres/data'"

```

Then start and enable `postgresql` service.

Create the sogo user and the sogo DB for PostgreSQL (do not select a strong password for the sogo user, just use "sogo" for simplicity. This is temporary and will be changed later):

```
# su - postgres
$ createuser --no-superuser --no-createdb --no-createrole --encrypted --pwprompt sogo
$ createdb -O sogo sogo

```

Edit the access configuration for the openchange DB:

```
# cp /var/lib/postgres/data/pg_hba.conf{,.bak}
# sed \
      's/D$/D

#Configuration for OpenChange/' \
      -i /var/lib/postgres/data/pg_hba.conf
# sed \
      's/ange$/ange
host\topenchange\topenchange\t127.0.0.1\/32\t\tmd5/' \
      -i /var/lib/postgres/data/pg_hba.conf
# chown postgres:postgres /var/lib/postgres/data/pg_hba.conf{,.bak}

```

Restart the `postgresql` service.

## Configuring user databases

### Active Directory

If using Active Directory for user authentication, whether using Samba (following the [Samba 4 Active Directory domain controller](/index.php/Samba_4_Active_Directory_domain_controller "Samba 4 Active Directory domain controller") article) or using a Microsoft server, the needed attributes for mail users are already present in the default schema. Users, however, need to have both *mail* and *proxyAddresses* attributes set. The *proxyAddress* attribute labeled **SMTP** (as opposed to smtp) is the default mail address. If using internal and external domains, you will need to set SMTP to the user's external address as this will be the SMTP from address and envelope sender in outgoing messages. Additionally, the *mail* attribute must also be set to the user's external email address.

For Samba, you can use the *ldbedit* command to edit users. In this example, we'll modify the "Administrator" user and add aliases for postmaster, as well as internal and external email addresses. Replace *vim* in the following command with your preferred editor:

```
# LDB_MODULES_PATH="/usr/lib/samba/ldb" ldbedit -e *vim* -H /var/lib/samba/private/sam.ldb '(samaccountname=**administrator**)'

```

It is important to change both the **mail** attribute (this is what will be used for group expansion and global address list functionality), and the primary **SMTP** address. The **smtp** entries for proxyAddresses act as aliases. Add the following attributes (again, substitute appropriate values for **internal**.**domain**.**tld** and **domain**.**tld**):

```
...
proxyAddresses: SMTP:administrator@**domain**.**tld**
proxyAddresses: smtp:postmaster@**internal**.**domain**.**tld**
proxyAddresses: smtp:postmaster@**domain**.**tld**
proxyAddresses: smtp:administrator@**internal**.**domain**.**tld**
mail: administrator@**domain**.**tld**
...
```

If using Microsoft's Active Directory Users and Computers MMC snap-in to edit users, you'll need to enable "Show Advanced Features" from the Tools menu, and use the Attribute Editor tab.

### MySQL/MariaDB

To be added...

### OpenLDAP

To be added...

### PostgreSQL

To be added...

## Postfix configuration

### Basic configuration

### User sources

#### Active Directory

#### Maria DB

#### OpenLDAP

#### PostgreSQL

## Dovecot configurtion

### Basic configuration

### User sources

#### Active Directory

#### Maria DB

#### OpenLDAP

#### PostgreSQL

## SOGo configuration

### Basic configuration

### User sources

#### Active Directory

#### Maria DB

#### OpenLDAP

#### PostgreSQL

## Web server final configuration

### Apache

### nginx