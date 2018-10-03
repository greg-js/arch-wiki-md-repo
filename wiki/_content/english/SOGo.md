Related articles

*   [Apache HTTP Server](/index.php/Apache_HTTP_Server "Apache HTTP Server")
*   [Dovecot](/index.php/Dovecot "Dovecot")
*   [MySQL](/index.php/MySQL "MySQL")
*   [Nginx](/index.php/Nginx "Nginx")
*   [OpenLDAP](/index.php/OpenLDAP "OpenLDAP")
*   [Postfix](/index.php/Postfix "Postfix")
*   [PostgreSQL](/index.php/PostgreSQL "PostgreSQL")
*   [Samba/Active Directory domain controller](/index.php/Samba/Active_Directory_domain_controller "Samba/Active Directory domain controller")
*   [Virtual user mail system](/index.php/Virtual_user_mail_system "Virtual user mail system")

[SOGo](http://www.sogo.nu/) provides a rich AJAX-based Web interface and supports multiple native clients through the use of standard protocols such as CalDAV, CardDAV and GroupDAV, as well as Microsoft ActiveSync. This article explains how to setup a groupware server using SOGo.

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
        *   [4.2.1 Prerequisites](#Prerequisites_2)
        *   [4.2.2 Creation of the sogo_users table](#Creation_of_the_sogo_users_table)
        *   [4.2.3 Modify SOGo config file](#Modify_SOGo_config_file)
    *   [4.3 OpenLDAP](#OpenLDAP)
    *   [4.4 PostgreSQL](#PostgreSQL_2)
*   [5 Dovecot configurtion](#Dovecot_configurtion)
    *   [5.1 Basic configuration](#Basic_configuration)
    *   [5.2 User sources](#User_sources)
        *   [5.2.1 Active Directory](#Active_Directory_2)
        *   [5.2.2 Maria DB](#Maria_DB)
        *   [5.2.3 OpenLDAP](#OpenLDAP_2)
        *   [5.2.4 PostgreSQL](#PostgreSQL_3)
    *   [5.3 Testing Dovecot authentication](#Testing_Dovecot_authentication)
    *   [5.4 LMTP configuration](#LMTP_configuration)
    *   [5.5 TLS configuration](#TLS_configuration)
    *   [5.6 Sieve configuration](#Sieve_configuration)
*   [6 Postfix configuration](#Postfix_configuration)
    *   [6.1 Basic configuration](#Basic_configuration_2)
    *   [6.2 User sources](#User_sources_2)
        *   [6.2.1 Active Directory](#Active_Directory_3)
        *   [6.2.2 Maria DB](#Maria_DB_2)
        *   [6.2.3 OpenLDAP](#OpenLDAP_3)
        *   [6.2.4 PostgreSQL](#PostgreSQL_4)
    *   [6.3 SASL configuration](#SASL_configuration)
    *   [6.4 LMTP configuration](#LMTP_configuration_2)
    *   [6.5 TLS configuration](#TLS_configuration_2)
    *   [6.6 Testing the Postfix SASL configuration](#Testing_the_Postfix_SASL_configuration)
*   [7 SOGo configuration](#SOGo_configuration)
    *   [7.1 Basic configuration](#Basic_configuration_3)
    *   [7.2 SOGo user sources](#SOGo_user_sources)
        *   [7.2.1 Active Directory](#Active_Directory_4)
        *   [7.2.2 Maria DB](#Maria_DB_3)
        *   [7.2.3 OpenLDAP](#OpenLDAP_4)
        *   [7.2.4 PostgreSQL](#PostgreSQL_5)
    *   [7.3 Completing configuration](#Completing_configuration)
*   [8 Web server final configuration](#Web_server_final_configuration)
    *   [8.1 Apache](#Apache_2)
    *   [8.2 nginx](#nginx_2)
*   [9 ActiveSync configuration](#ActiveSync_configuration)
    *   [9.1 Apache](#Apache_3)
    *   [9.2 nginx](#nginx_3)
    *   [9.3 SOGo](#SOGo)

## Installation

### Considerations

SOGo can use many different sources for user authentication including, but not limited to, Active Directory, OpenLDAP, MySQL/MariaDB, PostgreSQL, and probably many others if you include PAM. This article will focus on using a centrally managed user database (following on from the [Samba/Active Directory domain controller](/index.php/Samba/Active_Directory_domain_controller "Samba/Active Directory domain controller") article initially -- hopefully others will contribute OpenLDAP/MySQL/PostgreSQL user configs) for both authentication, and to provide a global address list.

Additionally, either [mariadb](https://www.archlinux.org/packages/?name=mariadb) or [postgresql](https://www.archlinux.org/packages/?name=postgresql) must be used to store the users' calendars and address books. As of this writing, the SOGo documentation has a clear preference for MariaDB (or MySQL), but if you have an existing PostgreSQL installation, it might make sense to use it. Other SQL implementations might also be supported, but are not currently covered.

Finally, there are currently two versions of SOGo that are being actively maintained. SOGo-2.x is uses a look and feel that is similar to a desktop client, while SOGo-3.x uses a more modern interface, taking cues from Google using AngularJS. Instructions and configuration are interchangeable between the two versions.

### Prerequisites

[Install](/index.php/Install "Install") [sogo](https://aur.archlinux.org/packages/sogo/) or [sogo2](https://aur.archlinux.org/packages/sogo2/).

*   For a local database install [MySQL](/index.php/MySQL "MySQL") or [PostgreSQL](/index.php/PostgreSQL "PostgreSQL").
*   For a local mail server install [Dovecot](/index.php/Dovecot "Dovecot") and [Postfix](/index.php/Postfix "Postfix").
*   For a local web server install [Apache](/index.php/Apache "Apache") or [nginx](/index.php/Nginx "Nginx").

## Initial web server configuration

### Apache

If using [Apache](/index.php/Apache "Apache") for the web server, add SOGo to the Apache configuration appending the following lines at the end of `/etc/httpd/conf/httpd.conf`:

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

If using [nginx](/index.php/Nginx "Nginx") for the web server, you will only configure on 443, SSL certificates must be in place prior to configuration. Add the following to `/etc/nginx/nginx.conf`:

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

Open a browser and go to http://**mail.domain.tld**/SOGo/ for Apache, or https://**mail.domain.tld**/SOGo/ for nginx. Do not try to login just yet, just verify that you can connect and get the login screen as authentication sources have not been setup yet.

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

If using Active Directory for user authentication, whether using Samba (following the [Samba/Active Directory domain controller](/index.php/Samba/Active_Directory_domain_controller "Samba/Active Directory domain controller") article) or using a Microsoft server, the needed attributes for mail users are already present in the default schema. Users, however, need to have both *mail* and *proxyAddresses* attributes set. The *proxyAddress* attribute labeled **SMTP** (as opposed to smtp) is the default mail address. If using internal and external domains, you will need to set SMTP to the user's external address as this will be the SMTP from address and envelope sender in outgoing messages. Additionally, the *mail* attribute must also be set to the user's external email address.

For Samba, you can use the *ldbedit* command to edit users. In this example, we'll modify the "Administrator" user and add aliases for postmaster, as well as internal and external email addresses. Replace *vim* in the following command with your preferred editor:

```
# LDB_MODULES_PATH="/usr/lib/samba/ldb" ldbedit -e *vim* -H /var/lib/samba/private/sam.ldb '(samaccountname=**administrator**)'

```

It is important to change both the **mail** attribute (this is what will be used for group expansion and global address list functionality), and the primary **SMTP** address. The **smtp** entries for proxyAddresses act as aliases. Add the following attributes (again, substitute appropriate values for **internal**.**domain**.**tld** and **domain**.**tld**):

```
...
mail: administrator@**domain**.**tld**
proxyAddresses: SMTP:administrator@**domain**.**tld**
proxyAddresses: smtp:postmaster@**internal**.**domain**.**tld**
proxyAddresses: smtp:postmaster@**domain**.**tld**
proxyAddresses: smtp:administrator@**internal**.**domain**.**tld**
...
```

If using Microsoft's Active Directory Users and Computers MMC snap-in to edit users, you'll need to enable "Show Advanced Features" from the Tools menu, and use the Attribute Editor tab.

Next, allow daemons to lookup users in the directory using LDAP. To do this, create an unprivileged user to use for LDAP lookups and optionally (recommended), set the password not to expire. If using Samba, execute the following commands. Be certain to set a suitably strong password:

```
# samba-tool user create ldap --description="Unprivileged user for LDAP lookups"
# samba-tool user setexpiry ldap --noexpiry

```

Finally, with Samba after 4.3.8 or 4.2.2, non-encrypted communication is disabled by default. Add the following configuration item to the [global] section of `/etc/samba/smb.conf` if you are not in a position to enable TLS or StartTLS:

 `        ldap server require strong auth = no` 

### MySQL/MariaDB

Following procedure is valid for mariadb 10.1.25-1 but should also work for MySQL. For debugging purposes, enable all debugging switches, so problems can be identified. In */etc/sogo/sogo.conf* set

```
 /* Debug */
 SOGoDebugRequests = YES;
 SoDebugBaseURL = YES;  
 ImapDebugEnabled = YES;
 LDAPDebugEnabled = YES;
 PGDebugEnabled = YES;
 MySQL4DebugEnabled = YES;
 SOGoUIxDebugEnabled = YES;
 WODontZipResponse = YES;
 WOLogFile = /var/log/sogo/sogo.log;

```

If problems occure, check via *journalctl -xe*

#### Prerequisites

1.  Ensure the sogo user is created in the database (see [#MySQL/MariaDB](#MySQL.2FMariaDB)).
2.  Ensure that there is a database named sogo with the database scheme utf8 (and not utf8mb4). This is necessary because the automatic creation of the *sogo_sessions_folder* table will fail otherwise:

```
 SQL: SELECT count(*) FROM sogo_sessions_folder;
 ERROR: Table 'sogo.sogo_sessions_folder' doesn't exist
 SQL: CREATE TABLE sogo_sessions_folder ( c_id VARCHAR(255) PRIMARY KEY, c_value VARCHAR(255) NOT NULL, c_creationdate INT NOT NULL, c_lastseen INT NOT NULL);
 ERROR: Specified key was too long; max key length is 767 bytes          <-- This happens because VARCHAR(255) is too big as primary key for utf8mb4

```

Scheme can be altered via

```
 ALTER SCHEMA `sogo`  DEFAULT CHARACTER SET utf8

```

Update: There seems to be a way around this and utf8mb4 could be used. Check page 33 ff of SOGo installation guide pdf.

#### Creation of the sogo_users table

The *sogo_users* table has to be created manually:

Change user and create table with comments, explaining what each column is (see [https://sogo.nu/files/docs/SOGoInstallationGuide.html#_authentication_using_sql](https://sogo.nu/files/docs/SOGoInstallationGuide.html#_authentication_using_sql))

```
 USE sogo;
 CREATE TABLE `sogo`.`sogo_users` (
 `c_uid` VARCHAR(128) NOT NULL COMMENT 'c_uid: will be used for authentication - it’s a username or username@domain.tld',  
 `c_name` VARCHAR(128) NOT NULL COMMENT 'c_name: will be used to uniquely identify entries - which can be identical to c_uid',
 `c_password` VARCHAR(128) NOT NULL COMMENT 'c_password: password of the user, plain text, crypt, md5 or sha encoded',
 `c_cn` VARCHAR(128) NULL COMMENT 'c_cn: the user’s common name',
 `mail` VARCHAR(128) NOT NULL COMMENT 'mail: the user’s email address',  PRIMARY KEY (`c_uid`));

```

Create a user

*   Generate the MD5 sum of the password (MD5 is still safe for password checking as of August 2017\. On top of that, webaccess should be done via SSL anyways).

```
 echo -n 'mypassword' | md5sum
 34819d7beeabb9260a5c854bc85b3e44  -

```

*   Create the entry for this user

```
 INSERT INTO `sogo`.`sogo_users` (`c_uid`, `c_name`, `c_password`, `c_cn`, `mail`) VALUES ('username', 'username', '34819d7beeabb9260a5c854bc85b3e44', 'Archie Username', 'archie@example.com');

```

#### Modify SOGo config file

Insert or modify in */etc/sogo/sogo.conf* (change the password to the chosen password for the sogo mysql user):

```
  SOGoUserSources =
    (
      {
        type = sql;
        id = directory;
        viewURL = "mysql://sogo:**yoursogopassword**@127.0.0.1:3306/sogo/sogo_users";
        canAuthenticate = YES;
        isAddressBook = YES;
        userPasswordAlgorithm = md5;
      }
    );

```

Alternatively, a view can be used instead of the table directly. More information about which values are available for *SOGoUserSources* can be found here: [https://sogo.nu/files/docs/SOGoInstallationGuide.html#_authentication_using_sql](https://sogo.nu/files/docs/SOGoInstallationGuide.html#_authentication_using_sql)

### OpenLDAP

To be added...

### PostgreSQL

To be added...

## Dovecot configurtion

### Basic configuration

Create a very basic dovecot configuration:

```
# cp /etc/dovecot/dovecot.conf{.sample,}
# chown root:root /etc/dovecot/dovecot.conf

```

Then create the file `/etc/dovecot/conf.d/local.conf` with this content:

```
auth_mechanisms = plain login
disable_plaintext_auth = no
ssl = no
auth_username_format = %n
mail_location = /home/vmail/%Lu/Maildir

```

Enable and start `dovecot`.

### User sources

#### Active Directory

Add the LDAP lookup configuation `/etc/dovecot/conf.d/ldap.conf`:

```
passdb ldap {
    driver = ldap
    args = /etc/dovecot/dovecot-ldap-passdb.conf
}
userdb ldap {
    driver = ldap
    args = /etc/dovecot/dovecot-ldap-userdb.conf
}

```

Set permissions:

```
# chmod 0644 /etc/dovecot/conf.d/ldap.conf
# chown root:root /etc/dovecot/conf.d/ldap.conf

```

Create the LDAP user and password configuration files (replace dc=**internal**,dc=**domain**,dc=**tld**, **INTERNAL**, and **ldapPW** with appropriate values). Remove the tls lines below if you haven't enabled the TLS configuration in your directory:

`/etc/dovecot/dovecot-ldap-passdb.conf`

```
hosts = localhost
auth_bind = yes
auth_bind_userdn = **INTERNAL**\%u
ldap_version = 3
tls = yes
base = dc=**internal**,dc=**domain**,dc=**tld**
scope = subtree
deref = never
pass_filter = (&(objectClass=person)(sAMAccountName=%u)(mail=*))

```

`/etc/dovecot/dovecot-ldap-userdb.conf`

```
hosts = localhost
dn = cn=ldap,cn=Users,dc=**internal**,dc=**domain**,dc=**tld**
dnpass = **ldapPW**
ldap_version = 3
tls = yes
base = cn=Users,dc=**internal**,dc=**domain**,dc=**tld**
user_attrs = =uid=5000,=gid=5000,=home=/home/vmail/%Lu,=mail=maildir:/home/vmail/%Lu/Maildir/
user_filter = (&(objectClass=person)(sAMAccountName=%u)(mail=*))

# Attributes and filter to get a list of all users
iterate_attrs = sAMAccountName=user
iterate_filter = (objectClass=person)

```

Set permissions:

```
# chown root:root /etc/dovecot/dovecot-ldap-{pass,user}db.conf
# chmod 0600 /etc/dovecot/dovecot-ldap-userdb.conf
# chmod 0644 /etc/dovecot/dovecot-ldap-passdb.conf

```

Create the SASL configuation `/etc/dovecot/conf.d/sasl.conf`:

```
service auth {
    unix_listener /var/spool/postfix/private/auth {
        mode = 0660
        user = postfix
        group = postfix
     }
}

```

Set permissions:

```
# chmod 0644 /etc/dovecot/conf.d/sasl.conf
# chown root:root /etc/dovecot/conf.d/sasl.conf

```

Reload Dovecot for the configuration to take effect:

```
# dovecot reload

```

#### Maria DB

To be added...

#### OpenLDAP

To be added...

#### PostgreSQL

To be added...

### Testing Dovecot authentication

Create the vmail user and group:

```
# groupadd -g 5000 vmail
# useradd -u 5000 -g vmail -s /usr/bin/nologin -d /home/vmail -m vmail
# chmod 750 /home/vmail

```

Open a *telnet* session and test (commands you enter are in bold, replace *Administrator* with a valid user account and *UserPass* with your real password):

```
**telnet localhost 143**
Trying 127.0.0.1...
Connected to localhost.
Escape character is '^]'.
* OK [CAPABILITY IMAP4rev1 LITERAL+ SASL-IR LOGIN-REFERRALS ID ENABLE IDLE AUTH=PLAIN AUTH=LOGIN] Dovecot ready.
**a LOGIN Administrator UserPass**
. OK [CAPABILITY IMAP4rev1 LITERAL+ SASL-IR LOGIN-REFERRALS ID ENABLE IDLE SORT SORT=DISPLAY THREAD=REFERENCES THREAD=REFS THREAD=ORDEREDSUBJECT MULTIAPPEND  URL-PARTIAL CATENATE UNSELECT CHILDREN NAMESPACE UIDPLUS LIST-EXTENDED I18NLEVEL=1 CONDSTORE QRESYNC ESEARCH ESORT SEARCHRES WITHIN CONTEXT=SEARCH LIST-STATUS SPECIAL-USE BINARY MOVE] Logged in
**a LOGOUT**
* BYE Logging out
. OK Logout completed.
Connection closed by foreign host.

```

If anything other than OK is returned, go back and double check the configuration before continuing.

### LMTP configuration

Create the LMTP configuration file `/etc/dovecot/conf.d/lmtp.conf`:

```
mail_location = /home/vmail/%Lu/Maildir
service lmtp {
  unix_listener /var/spool/postfix/private/dovecot-lmtp {
    mode = 0600
    user = postfix
    group = postfix
  }
  user = vmail
}

protocol lmtp {
  postmaster_address = postmaster@**domain**.**tld**
}

```

```
# chmod 0644 /etc/dovecot/conf.d/lmtp.conf
# dovecot reload

```

### TLS configuration

Put your certificates into place and create the TLS configuration file `/etc/dovecot/conf.d/tls.conf` (adjust paths and names as necessary). The keyfile should be owned by root with 0400 permissions. Any intermediate certificates should be concatenated after the public cert:

```
ssl = yes
ssl_cert = </etc/dovecot/ssl/**host**.**domain**.**tld**.pem
ssl_key = </etc/dovecot/ssl/**host**.**domain**.**tld**.key

```

```
# chmod 644 /etc/dovecot/conf.d/tls.conf
# chmod 600 /etc/dovecot/ssl/**host**.**domain**.**tld**.key

```

Remove the earlier explicitly defined values from `local.conf` and reload Dovecot:

```
# sed -e '/^ssl/d' -e '/disable_plaintext/s/no/yes/' \
      -i /etc/dovecot/conf.d/local.conf
# dovecot reload

```

### Sieve configuration

Edit `/etc/dovecot/dovecot.conf`, uncomment the protocols line and add sieve as a service (remove pop3 as well if you do not intend to provide pop access):

```
protocols = imap lmtp sieve

```

Append the following to `/etc/dovecot/conf.d/local.conf`:

```
...
plugin {
   sieve_before = /home/vmail/sieve/spam-global.sieve
   sieve=/home/vmail/%Lu/dovecot.sieve
   sieve_dir=/home/vmail/%Lu/sieve
}

```

Create the global sieve directory:

```
mkdir -p /home/vmail/sieve/

```

Create the `/home/vmail/sieve/spam-global.sieve` file with the following contents:

```
require "fileinto";
if header :contains "X-Spam-Flag" "YES" {
  fileinto "Spam";
}

```

Set permissions on the directory (and file):

```
chown -R vmail:vmail /home/vmail/sieve

```

Modify the `/etc/dovecot/conf.d/lmtp.conf` file, adding the bold text below:

```
mail_location = /home/vmail/%Lu/Maildir
service lmtp {
  unix_listener /var/spool/postfix/private/dovecot-lmtp {
    mode = 0600
    user = postfix
    group = postfix
  }
  user = vmail
}

protocol lmtp {
  postmaster_address = postmaster@domain.tld
  **mail_plugins = sieve**
}

**plugin {**
  **sieve_before = /home/vmail/sieve/spam-global.sieve**
  **sieve = /home/vmail/%Lu/dovecot.sieve**
  **sieve_dir = /home/vmail/%Lu/sieve**
**}**

```

Reload dovecot

## Postfix configuration

### Basic configuration

Create a minimal Postfix configuration. Replace **server**.**internal**.**domain.tld** with a valid internal FQDN):

```
# postconf -e myhostname=**server**.**internal**.**domain.tld**
# postconf -e mydestination=localhost

```

If this server will be accessible from the internet, set the HELO/EHLO values to match the FQDN as seen from the internet (replace **mail**.**domain**.**tld**):

```
# postconf -e smtp_helo_name=**mail**.**domain**.**tld**
# postconf -e smtpd_banner='$smtp_helo_name ESMTP $mail_name'

```

Enable and start `postfix`.

Configure Postfix to use the vmail user and group:

```
# postconf -e virtual_minimum_uid=5000
# postconf -e virtual_uid_maps=static:5000
# postconf -e virtual_gid_maps=static:5000
# postconf -e virtual_mailbox_base=/home/vmail
# postfix reload

```

### User sources

#### Active Directory

Now, create a LDAP alias and group maps for Postfix by pasting the following lines in the file `/etc/postfix/ldap-alias.cf` as root (replace dc=**internal**,dc=**domain**,dc=**tld** with appropriate values and **ldapPW** with the password of the ldap user). If TLS has not been configured for your directory, remove the start_tls line:

```
# Directory settings
server_host = 127.0.0.1
search_base = dc=**internal**,dc=**domain**,dc=**tld**
scope = sub
version = 3
start_tls = yes

# User Binding
bind = yes
bind_dn = cn=ldap,cn=users,dc=**internal**,dc=**domain**,dc=**tld**
bind_pw = **ldapPW**

# Filter
query_filter = (&(objectclass=person)(proxyAddresses=smtp:%s))
result_attribute = samaccountname
result_format = %s@**internal**.**domain**.**tld**

```

Create the group map:

```
# sed -e '/^query/d' \
      -e '/^result/d' \
      /etc/postfix/ldap-alias.cf > /etc/postfix/ldap-group.cf

```

Append the following lines to the newly created `/etc/postfix/ldap-group.cf` (in the #Filter secton):

```
query_filter = (&(objectclass=group)(mail=%s))
special_result_attribute = member
leaf_result_attribute = mail

```

Set the permissions:

```
# chmod 0600 /etc/postfix/ldap-{alias,group}.cf

```

Next test our lookup maps for users (groups have not yet been created) (substitute **internal.domain.tld**):

```
# postmap -q administrator@**domain.tld** ldap:/etc/postfix/ldap-alias.cf
# postmap -q administrator@**internal.domain.tld** ldap:/etc/postfix/ldap-alias.cf

```

The following output should be displayed for both commands:

```
Administrator@internal.domain.tld

```

Append any other hosted domains to the first command below, add the maps, and then reload the Postfix configuration (again replacing domain values):

```
# postconf -e virtual_mailbox_domains="**domain.tld**, **internal.domain.tld**"
# postconf -e virtual_alias_maps="ldap:/etc/postfix/ldap-alias.cf, ldap:/etc/postfix/ldap-group.cf"
# postfix reload

```

#### Maria DB

To be added...

#### OpenLDAP

To be added...

#### PostgreSQL

To be added...

### SASL configuration

Modify the default smtpd instance:

```
# postconf -e smtpd_sasl_type=dovecot
# postconf -e smtpd_sasl_path=private/auth
# postconf -e smtpd_sasl_auth_enable=yes
# postconf -e smtpd_relay_restrictions="permit_mynetworks, permit_sasl_authenticated, reject_unauth_destination"

```

### LMTP configuration

Use dovecot LMTP for delivery:

```
# postconf -e virtual_transport=lmtp:unix:private/dovecot-lmtp

```

### TLS configuration

If you intend to use STARTTLS (as you should), enable the mail submission port and restrict to authenticated clients. Edit the following lines in `/etc/postfix/master.cf`:

```
submission inet n       -       n       -       -       smtpd
  -o syslog_name=postfix/submission
  -o smtpd_tls_security_level=encrypt
  -o smtpd_sasl_auth_enable=yes
  -o smtpd_sasl_type=dovecot
  -o smtpd_sasl_path=private/auth
  -o smtpd_sasl_security_options=noanonymous
  -o smtpd_client_restrictions=permit_sasl_authenticated,reject
  -o smtpd_sender_login_maps=ldap:/etc/postfix/ldap-sender.cf
  -o smtpd_sender_restrictions=reject_sender_login_mismatch
  -o smtpd_recipient_restrictions=reject_non_fqdn_recipient,reject_unknown_recipient_domain,permit_sasl_authenticated,reject

```

Add SSL certificates. If you intend to put Postfix in a chroot jail (not discussed in this guide), these need to be placed in the Postfix configuration directory as opposed to the default /etc/ssl/private directory. Additionally, any intermediate certs should be concatenated with the public cert being first in the chain, and the key file should be owned by root with 0400 permission mode (replace **mail.domain.tld**):

```
# postconf -e smtpd_tls_key_file=/etc/postfix/ssl/**mail.domain.tld.key**
# postconf -e smtpd_tls_cert_file=/etc/postfix/ssl/**mail.domain.tld.pem**

```

Create a map to verify addresses to authenticated users `/etc/postfix/ldap-sender.cf`:

```
# Directory settings
server_host = localhost
search_base = dc=**internal**,dc=**domain**,dc=**tld**
version = 3
scope = sub

# User Binding
bind = yes
bind_dn = cn=ldap,cn=Users,dc=**internal**,dc=**domain**,dc=**tld**
bind_pw = **ldapPW**

# Filter
query_filter = (&(objectclass=person)(proxyAddresses=smtp:%s))
leaf_result_attribute = proxyAddresses
result_attribute = sAMAccountName

```

Set permissions:

```
# chown root:root /etc/postfix/ldap-sender.cf
# chmod 0640 /etc/postfix/ldap-sender.cf

```

If you would like to enable TLS on the default SMTP port, you should make it optional. If you make it required, you will not be able to receive mail from many hosts on the internet.

```
# postconf -e smtpd_tls_security_level=may

```

Reload postfix to apply the configuration changes:

```
# postfix reload

```

### Testing the Postfix SASL configuration

Begin by getting a base64 encoded version of the username and password (replace **Administrator** with a valid username and **UserPass** with your real password):

```
$ echo -ne '\000**Administrator**\000**UserPass'** | openssl base64

```

You should receive output similar to the following:

```
AEFkbWluaXN0cmF0b3IAVXNlclBhc3M=

```

Now, open a *telnet* session and test (commands you enter are in bold, replace **host.domain.tld** with the real external FQDN and **AEFkbWluaXN0cmF0b3IAVXNlclBhc3M=** with the result of the previous command):

```
$ **telnet localhost 25**
Trying 127.0.0.1...
Connected to localhost.
Escape character is '^]'.
220 host.domain.tld ESMTP Postfix
**ehlo host.domain.tld**
250-mail.lucasit.com
250-PIPELINING
250-SIZE 10240000
250-VRFY
250-ETRN
250-STARTTLS
250-AUTH PLAIN LOGIN
250-ENHANCEDSTATUSCODES
250-8BITMIME
250 DSN
**AUTH PLAIN AEFkbWluaXN0cmF0b3IAVXNlclBhc3M=**
235 2.7.0 Authentication successful
**quit**
221 2.0.0 Bye
Connection closed by foreign host.

```

If anything other than a 235 message is returned, something is wrong and you should troubleshoot now rather than later.

## SOGo configuration

### Basic configuration

Edit the SOGo http configuration file, `/etc/httpd/conf/extra/SOGo.conf`, and comment out the following lines for testing (until SSL certs are in place and configuration is complete):

```
## adjust the following to your configuration
#  RequestHeader set "x-webobjects-server-port" "443"
#  RequestHeader set "x-webobjects-server-name" "yourhostname"
#  RequestHeader set "x-webobjects-server-url" "https://yourhostname"

```

Create a suitable SOGo configuration file in `/etc/sogo/sogo.conf` (replace items in bold with appropriate values). If using PostgreSQL, replace the "mysql:" lines with the appropriate "postgresql:" lines (as above):

```
{
    /* Database Configuration */
    SOGoProfileURL = "mysql://sogo:**SogoPW**@localhost/sogo/sogo_user_profile";
    OCSFolderInfoURL = "mysql://sogo:**SogoPW**@localhost/sogo/sogo_folder_info";
    OCSSessionsFolderURL = "mysql://sogo:**SogoPW**@localhost/sogo/sogo_sessions_folder";

    /* Mail */
    SOGoDraftsFolderName = Drafts;
    SOGoSentFolderName = Sent;
    SOGoTrashFolderName = Trash;
    SOGoIMAPServer = localhost;
    SOGoSieveServer = sieve://127.0.0.1:4190;
    SOGoSMTPServer = 127.0.0.1;
    SOGoMailDomain = **internal**.**domain**.**tld**;
    SOGoMailingMechanism = smtp;
    SOGoForceExternalLoginWithEmail = NO;
    SOGoMailSpoolPath = /var/spool/sogo;
    NGImap4ConnectionStringSeparator = "/";

    /* Notifications */
    SOGoAppointmentSendEMailNotifications = YES;
    SOGoACLsSendEMailNotifications = NO;
    SOGoFoldersSendEMailNotifications = NO;

    /* Authentication */
    SOGoPasswordChangeEnabled = YES;

    /* Web Interface */
    SOGoPageTitle = SOGo;
    SOGoVacationEnabled = YES;
    SOGoForwardEnabled = YES;
    SOGoSieveScriptsEnabled = YES;
    SOGoMailAuxiliaryUserAccountsEnabled = YES;
    SOGoTrustProxyAuthentication = NO;

    /* General */
    SOGoLanguage = **English**;
    SOGoTimeZone = **America/Chicago**;
    SOGoCalendarDefaultRoles = (
        PublicDAndTViewer,
        ConfidentialDAndTViewer
    );
    SOGoSuperUsernames = (**administrator**);
    SxVMemLimit = 384;
    //WOPidFile = "/var/run/sogo/sogo.pid";
    SOGoMemcachedHost = "**127.0.0.1**";

    /* Debug */
    //SOGoDebugRequests = YES;
    //SoDebugBaseURL = YES;
    //ImapDebugEnabled = YES;
    //LDAPDebugEnabled = YES;
    //PGDebugEnabled = YES;
    //MySQL4DebugEnabled = YES;
    //SOGoUIxDebugEnabled = YES;
    //WODontZipResponse = YES;
    //WOLogFile = /var/log/sogo/sogo.log;

}

```

Then issue the following commands:

```
# chown sogo:sogo /etc/sogo/sogo.conf
# chmod 0600 /etc/sogo/sogo.conf
# mkdir /var/spool/sogo
# chown sogo:sogo /var/spool/sogo
# chmod 700 /var/spool/sogo

```

### SOGo user sources

#### Active Directory

Modify the `/etc/sogo/sogo.conf` file and add the LDAP user sources (and global address list). Place the following contents before the *Web Interface* section. If TLS is not configured for your Directory, exclude the "**/????!StartTLS**" strings at the end of the LDAP URIs:

```
    /* User Authentication */
    SOGoUserSources = (
     {
        id = directory;
        displayName = "Active Directory";
        canAuthenticate = YES;
        type = ldap;
        CNFieldName = cn;
        IDFieldName = sAMAccountName;
        UIDFieldName = sAMAccountName;
        baseDN = "dc=**internal**,dc=**domain**,dc=**tld**";
        bindDN = "cn=ldap,cn=Users,dc=**internal**,dc=**domain**,dc=**tld**";
        bindFields = (sAMAccountName);
        bindPassword = **ldapPW**;
        hostname = ldap://**server**.**internal**.**domain**.**tld**:389/????!StartTLS;
      },
      {
        id = sambaShared;
        displayName = "Shared Addressbook";
        canAuthenticate = NO;
        isAddressBook = YES;
        type = ldap;
        CNFieldName = cn;
        IDFieldName = mail;
        UIDFieldName = mail;
        hostname = ldap://**server**.**internal**.**domain**.**tld**:389/????!StartTLS;
        baseDN = "dc=**internal**,dc=**domain**,dc=**tld**";
        bindDN = "cn=ldap,cn=Users,dc=**internal**,dc=**domain**,dc=**tld**";
        bindPassword = **ldapPW**;
        filter = "((NOT isCriticalSystemObject='TRUE') AND (mail=\'*\') AND (NOT objectClass=contact))";
        //Uncomment to list local users in WebUI without searching (small directories only)
        //listRequiresDot = NO;
      },
      {
        id = sambaContacts;
        displayName = "Shared Contacts";
        canAuthenticate = NO;
        isAddressBook = YES;
        type = ldap;
        CNFieldName = cn;
        IDFieldName = mail;
        UIDFieldName = mail;
        hostname = ldap://**server**.**internal**.**domain**.**tld**:389/????!StartTLS;
        baseDN = "dc=**internal**,dc=**domain**,dc=**tld**";
        bindDN = "cn=ldap,cn=Users,dc=**internal**,dc=**domain**,dc=**tld**";
        bindPassword = **ldapPW**;
        filter = "((((objectClass=person) AND (objectClass=contact) AND ((uidNumber>=2000) OR (mail='*')))
                 AND (NOT isCriticalSystemObject='TRUE') AND (NOT showInAdvancedViewOnly='TRUE') AND (NOT uid=Guest))
                 OR (((objectClass=group) AND (gidNumber>=2000)) AND (NOT isCriticalSystemObject='TRUE') AND (NOT showInAdvancedViewOnly='TRUE')))";
        mapping = {
            displayname = ("cn");
        //Uncomment to list contacts in WebUI without searching (few contacts only)
        //listRequiresDot = NO;
        };
      }
    );

```

#### Maria DB

To be added...

#### OpenLDAP

To be added...

#### PostgreSQL

To be added...

### Completing configuration

Now enable and start the `memcached` service and restart the `sogo` service. Test by visiting http://**server.internal.domain.tld**/SOGo/ .

## Web server final configuration

### Apache

If all is well with SOGo without SSL, go ahead and enable SSL in httpd if using Apache (modify paths and filenames as necessary):

```
# sed -e '/httpd-ssl.conf/s/#//' \
      -e '/modules\/mod_ssl.so/s/#//' \
      -e '/mod_socache_shmcb/s/#//' \
      -i /etc/httpd/conf/httpd.conf
# sed -e '/^SSLCertificateFile/s@/etc/httpd/conf/server.crt@/etc/httpd/ssl/**mail**.**domain**.**tld**.pem@' \
         -e '/^SSLCertificateKeyFile/s@/etc/httpd/conf/server.key@/etc/httpd/ssl/**mail**.**domain**.**tld**.key@' \
         -i /etc/httpd/conf/extra/httpd-ssl.conf

```

Now go ahead and edit the `/etc/httpd/conf/extra/SOGo.conf` file and uncomment the following lines, edit to suit your site:

```
## adjust the following to your configuration
RequestHeader set "x-webobjects-server-port" "443"
RequestHeader set "x-webobjects-server-name" "**mail**.**domain**.**tld**"
RequestHeader set "x-webobjects-server-url" "https://**mail**.**domain**.**tld**"

```

Restart `httpd` service for the changes to take effect.

Go ahead and go to the regular http page and it should redirect you to the https site.

### nginx

Since the nginx configuration was already setup for SSL, nothing more need be done.

## ActiveSync configuration

### Apache

To add ActiveSync support, simply uncomment the following lines in `/etc/httpd/conf/extra/SOGo.conf`:

```
...
ProxyPass /Microsoft-Server-ActiveSync \
 http://127.0.0.1:20000/SOGo/Microsoft-Server-ActiveSync \
 retry=60 connectiontimeout=5 timeout=3600
...

```

This will result in extended locking delays if you have more than a handful of users, so some tuning is required. You may notice that the above line was changed from 360 seconds to 3600 seconds (or one hour). This is because EAS devices need to keep their HTTP connections open for very long times (up to one hour). Because of this, you will need to tell SOGo (see below) to honor that timeout.

### nginx

Add the following to your server definition for SOGo in `/etc/nginx/nginx.com`:

```
...
        location ^~ /Microsoft-Server-ActiveSync {
                proxy_pass http://127.0.0.1:20000/SOGo/Microsoft-Server-ActiveSync;
                proxy_redirect http://127.0.0.1:20000/Microsoft-Server-ActiveSync /;
        }

        location ^~ /SOGo/Microsoft-Server-ActiveSync {
                proxy_pass http://127.0.0.1:20000/SOGo/Microsoft-Server-ActiveSync;
                proxy_redirect http://127.0.0.1:20000/SOGo/Microsoft-Server-ActiveSync /;
        }
...

```

Additional tuning may be required for the parameters in the SOGo section below (timeout, retry, and next host values, specifically).

### SOGo

As stated above for the listed HTTP servers, some tuning is required to use EAS. While the timeouts below (59 minutes) are appropriate for the HTTP session timeout set above, the number of workers is dependent on the number of simultaneous EAS clients you must support. In short, you will always need more workers than EAS clients to allow start of another worker for push operations. Additionally, the sync interval will allow you to reduce the load on the server so that less delay is generated, and this dependent on the total number of clients. The SOGo configuration guide, available at [http://sogo.nu/files/docs/SOGoInstallationGuide.pdf](http://sogo.nu/files/docs/SOGoInstallationGuide.pdf), lists two example configurations. The 100 user with 10 EAS users example was chosen for this article. Append the following lines to `/etc/sogo/sogo.conf` making sure that they are placed before the closing brace ("}") character:

```
  /* ActiveSync */
  WOWorkersCount = 15;
  SOGoMaximumPingInterval = 3540;
  SOGoMaximumSyncInterval = 3540;
  SOGoInternalSyncInterval = 30;

```