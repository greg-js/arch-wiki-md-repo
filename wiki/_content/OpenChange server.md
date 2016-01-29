# OpenChange server

Related articles

*   [Samba 4 Active Directory domain controller](/index.php/Samba_4_Active_Directory_domain_controller "Samba 4 Active Directory domain controller")
*   [Active Directory Integration](/index.php/Active_Directory_Integration "Active Directory Integration")
*   [Samba](/index.php/Samba "Samba")
*   [Samba/Tips and tricks](/index.php/Samba/Tips_and_tricks "Samba/Tips and tricks")

This article explains how to setup a mail server using OpenChange server following on from the [Samba 4 Active Directory domain controller](/index.php/Samba_4_Active_Directory_domain_controller "Samba 4 Active Directory domain controller") article. Postfix is used for the MTA, Dovecot for the IMAP/POP server, and SOGo for the backend with all users stored in Samba's Active Directory (normal Exchange attributes are used throughout).

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Prerequsites](#Prerequsites)
*   [2 Configuration](#Configuration)
    *   [2.1 MySQL/MariaDB](#MySQL.2FMariaDB)
    *   [2.2 Initial OpenChange configuration](#Initial_OpenChange_configuration)
        *   [2.2.1 Samba](#Samba)
        *   [2.2.2 OpenChange](#OpenChange)
    *   [2.3 Initial SOGo configuration](#Initial_SOGo_configuration)
        *   [2.3.1 Apache httpd](#Apache_httpd)
        *   [2.3.2 nginx](#nginx)
        *   [2.3.3 Start and test web access](#Start_and_test_web_access)
        *   [2.3.4 Database Configuration](#Database_Configuration)
            *   [2.3.4.1 MySQL/MariaDB](#MySQL.2FMariaDB_2)
            *   [2.3.4.2 PostgreSQL](#PostgreSQL)
        *   [2.3.5 SOGo](#SOGo)
    *   [2.4 Initial Postfix configuration](#Initial_Postfix_configuration)
        *   [2.4.1 Basic configuratoin](#Basic_configuratoin)
        *   [2.4.2 Virtual user configuration](#Virtual_user_configuration)
        *   [2.4.3 LDAP configuration](#LDAP_configuration)
    *   [2.5 Dovecot configuration](#Dovecot_configuration)
        *   [2.5.1 Basic configuration](#Basic_configuration)
        *   [2.5.2 LDAP configuration](#LDAP_configuration_2)
        *   [2.5.3 Testing Dovecot authentication](#Testing_Dovecot_authentication)
        *   [2.5.4 LMTP configuration](#LMTP_configuration)
        *   [2.5.5 TLS configuration](#TLS_configuration)
        *   [2.5.6 Sieve configuration](#Sieve_configuration)
    *   [2.6 Postfix final configuration](#Postfix_final_configuration)
        *   [2.6.1 SASL configuration](#SASL_configuration)
        *   [2.6.2 LMTP configuration](#LMTP_configuration_2)
        *   [2.6.3 TLS configuration](#TLS_configuration_2)
        *   [2.6.4 Testing the Postfix SASL configuration](#Testing_the_Postfix_SASL_configuration)
    *   [2.7 SOGo final configuration](#SOGo_final_configuration)
        *   [2.7.1 PostgreSQL](#PostgreSQL_2)
        *   [2.7.2 SOGo](#SOGo_2)
        *   [2.7.3 Apache httpd](#Apache_httpd_2)
    *   [2.8 OpenChange final configuration](#OpenChange_final_configuration)
        *   [2.8.1 OCSManager](#OCSManager)
        *   [2.8.2 Adding OpenChange MAPIProxy and OCSManger to Apache httpd](#Adding_OpenChange_MAPIProxy_and_OCSManger_to_Apache_httpd)

## Installation

### Prerequsites

[Install](/index.php/Install "Install") the needed prerequisite packages [dovecot](https://www.archlinux.org/packages/?name=dovecot), [mariadb](https://www.archlinux.org/packages/?name=mariadb), [pigeonhole](https://www.archlinux.org/packages/?name=pigeonhole), [postfix](https://www.archlinux.org/packages/?name=postfix), [postgresql](https://www.archlinux.org/packages/?name=postgresql), [mysql-python](https://www.archlinux.org/packages/?name=mysql-python) and either [apache](https://www.archlinux.org/packages/?name=apache) or [nginx](https://www.archlinux.org/packages/?name=nginx) from the [official repositories](/index.php/Official_repositories "Official repositories").

[Install](/index.php/Install "Install") [openchange](https://aur.archlinux.org/packages/openchange/)<sup><small>AUR</small></sup>, [python2-sievelib](https://aur.archlinux.org/packages/python2-sievelib/)<sup><small>AUR</small></sup>, [sogo](https://aur.archlinux.org/packages/sogo/)<sup><small>AUR</small></sup>, [sogo-openchange](https://aur.archlinux.org/packages/sogo-openchange/)<sup><small>AUR</small></sup>, and [sope](https://aur.archlinux.org/packages/sope/)<sup><small>AUR</small></sup> from the [AUR](/index.php/AUR "AUR").

## Configuration

### MySQL/MariaDB

If you haven't already done so, create the first MySQL database with the following command:

```
# mysql_install_db --user=mysql --basedir=/usr/ --ldata=/var/lib/mysql/

```

Enable and start `mysqld`, then enter the MySQL shell as the root user:

```
# mysql -u root

```

At the mysql prompt, enter the following commands (replace **OpenchangePW** with a secure password):

```
CREATE DATABASE openchange;
CREATE USER 'openchange'@'localhost' IDENTIFIED BY '**OpenchangePW'**;
GRANT ALL PRIVILEGES ON `openchange`.* TO 'openchange'@'localhost' WITH GRANT OPTION;
FLUSH PRIVILEGES;

```

### Initial OpenChange configuration

#### Samba

Make a backup copy of the existing samba configuration:

```
# cp /etc/samba/smb.conf{,.bak}

```

Append the following line to the "[global]" section of the `/etc/samba/smb.conf` file and restart `samba`.

```
dsdb:schema update allowed=true

```

Append the following lines to "[global]" section of the `/etc/samba/smb.conf` file. Be sure to replace **OpenchangePW**:

```
...
# Begin OpenChange Server Configuration
dcerpc endpoint servers = +epmapper, +mapiproxy, +dnsserver
dcerpc_mapiproxy:server = true
dcerpc_mapiproxy:interfaces = exchange_emsmdb, exchange_nsp, exchange_ds_rfr
mapistore:namedproperties = mysql
namedproperties:mysql_user = openchange
namedproperties:mysql_pass = **OpenchangePW**
namedproperties:mysql_host = localhost
namedproperties:mysql_db = openchange
mapistore:indexing_backend = mysql://openchange:**OpenchangePW**@localhost/openchange
mapiproxy:openchangedb = mysql://openchange:**OpenchangePW**@localhost/openchange
# End OpenChange Server Configuration
...

```

#### OpenChange

Next, provision the database and create the openchange DB. Once again, replace **OpenchangePW**:

```
# openchange_provision --standalone
# openchange_provision --openchangedb --openchangedb-uri mysql://openchange:**OpenchangePW**@localhost/openchange

```

Enable mail for the first user (Administrator):

```
# openchange_newuser --create Administrator

```

Restart `samba`.

At this point, verify that all samba services are working as expected. Use the tests in the [Samba 4 Active Directory domain controller](/index.php/Samba_4_Active_Directory_domain_controller#Testing_the_installation "Samba 4 Active Directory domain controller") guide in addition to testing RPC from a windows client (simply connect with RSAT tools or something similar). If all is well, then continue. If not, restore the backup of the `smb.conf` until you can track down the problem.

Finally, verify that user properties can be edited using ldbedit. Relevant attributes are mail and proxyAddresses. The proxyAddress attribute labeled SMTP (as opposed to smtp) is the default mail address. If using internal and external domains, you will need to set SMTP to external address as this will be the SMTP from address and envelope sender in outgoing messages. Replace _vim_ in the following command with your preferred editor:

```
# LDB_MODULES_PATH="/usr/lib/samba/ldb" ldbedit -e _vim_ -H /var/lib/samba/private/sam.ldb '(samaccountname=administrator)'

```

If you first followed the [Samba 4 Active Directory domain controller](/index.php/Samba_4_Active_Directory_domain_controller "Samba 4 Active Directory domain controller") article, you should see text similar to the following in the editor window (substituting **internal**.**domain**.**tld** with your domain's values):

```
...
proxyAddresses: SMTP:Administrator@**internal**.**domain**.**tld**
proxyAddresses: =EX:/o=First Organization/ou=First Administrative Group/cn=Recipients/cn=Administrator
proxyAddresses: X400:c=US;a= ;p=First Organizati;o=First Administrative Group;s=Administrator
proxyAddresses: smtp:postmaster@**internal**.**domain**.**tld**
...
mail: Administrator@**internal**.**domain**.**tld**
...
```

It is important to change both the **mail** attribute (this is what will be used for group expansion), and the primary **SMTP** address. Change it to the following (again, substitute appropriate values for **internal**.**domain**.**tld** and **domain**.**tld**):

```
...
proxyAddresses: SMTP:Administrator@**domain**.**tld**
proxyAddresses: =EX:/o=First Organization/ou=First Administrative Group/cn=Recipients/cn=Administrator
proxyAddresses: X400:c=US;a= ;p=First Organizati;o=Exchange;s=Administrator
proxyAddresses: smtp:postmaster@**internal**.**domain**.**tld**
proxyAddresses: smtp:postmaster@**domain**.**tld**
proxyAddresses: smtp:Administrator@**internal**.**domain**.**tld**
...
mail: Administrator@**domain**.**tld**
...
```

### Initial SOGo configuration

#### Apache httpd

If using Apache for the web server, add SOGo to the Apache configuration appending the following lines at the end of `/etc/httpd/conf/httpd.conf`:

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

#### nginx

If using nginx for the web server, add the following to `/etc/nginx/nginx.conf`:

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

#### Start and test web access

Create the state directory and start services:

```
# mkdir /var/run/sogo
# chown sogo:sogo /var/run/sogo
# chown sogo:sogo /etc/sogo/sogo.conf
# chmod 0644 /etc/sogo/sogo.conf

```

Then enable and start the `sogo` and either `httpd` or `nginx` services.

Open a browser and go to [http://server.internal.domain.tld/SOGo/](http://server.internal.domain.tld/SOGo/) but do not try to login just yet, just verify that you can connect and get the login screen.

#### Database Configuration

##### MySQL/MariaDB

If using MySQL/MariaDB for SOGo, you can use the existing openchange database, no further configuration is necessary.

If you had previously used PostgreSQL, you can migrate user data to MySQL/MariaDB using sogo-tool to backup and restore. Details are obviously site specific, but this example should work for most. Backup the full sogo-database with the following commands:

```
# mkdir /root/sogo-backup
# sogo-tool backup /root/sogo-backup ALL

```

Now stop the sogo daemon, stop postgresql (if not used for other purposes), and reconfigure sogo (/etc/sogo/sogo.conf) using both the openchange user and openchange database keeping the last path element (see example below).

To restore all user data, run the following commands:

```
# for user in `ls -d /root/sogo-backup/*`
  do
      sogo-tool restore -f /root/sogo-backup $(basename $user)
  done

```

Simply restart sogo to continue using the MySQL/MariaDB.

##### PostgreSQL

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
      's/D$/D\n\n#Configuration for OpenChange/' \
      -i /var/lib/postgres/data/pg_hba.conf
# sed \
      's/ange$/ange\nhost\topenchange\topenchange\t127.0.0.1\/32\t\tmd5/' \
      -i /var/lib/postgres/data/pg_hba.conf
# chown postgres:postgres /var/lib/postgres/data/pg_hba.conf{,.bak}

```

Restart the `postgresql` service.

#### SOGo

Configure SOGo defaults with the following commands (be certain to replace **REGION/LOCALITY**, **OpenchangePW**, **SAMBAADMINPASSWORD**, and dc=**internal**,dc=**domain**,dc=**tld** with appropriate values). If using PostgreSQL, be sure to replace all instances of **mysql://openchange:OpenchangePW@localhost/openchange** with **postgresql://sogo:sogo@localhost:5432/sogo**:

```
# su - sogo -s /bin/bash
$ defaults write sogod SOGoTimeZone "**REGION/LOCALITY**"
$ defaults write sogod OCSFolderInfoURL "mysql://openchange:**OpenchangePW**@localhost/openchange/sogo_folder_info"
$ defaults write sogod SOGoProfileURL "mysql://openchange:**OpenchangePW**@localhost/openchange/sogo_user_profile"
$ defaults write sogod OCSSessionsFolderURL "mysql://openchange:**OpenchangePW**@localhost/openchange/sogo_sessions_folder"
$ defaults write sogod OCSEMailAlarmsFolderURL "mysql://openchange:**OpenchangePW**@localhost/openchange/sogo_alarm_folder"
$ defaults write sogod SOGoUserSources '({CNFieldName = displayName; IDFieldName = cn; UIDFieldName = sAMAccountName; IMAPHostFieldName =; baseDN = "cn=Users,dc=**internal**,dc=**domain**,dc=**tld**"; bindDN = "cn=Administrator,cn=Users,dc=**internal**,dc=**domain**,dc=**tld**"; bindPassword = "**SAMBAADMINPASSWORD**"; canAuthenticate = YES; displayName = "Shared Addresses"; hostname = "localhost"; id = public; isAddressBook = YES; port = 389;})'
$ defaults write sogod WONoDetach NO
$ defaults write sogod WOLogFile /var/log/sogo/sogo.log
$ defaults write sogod WOPidFile /var/run/sogo/sogo.pid
$ exit

```

Next, edit the sogo configuration file, `/etc/httpd/conf/extra/SOGo.conf`, and comment out the following lines for testing (until SSL certs are in place and configuration is complete):

```
## adjust the following to your configuration
#  RequestHeader set "x-webobjects-server-port" "443"
#  RequestHeader set "x-webobjects-server-name" "yourhostname"
#  RequestHeader set "x-webobjects-server-url" "https://yourhostname"

```

Give the root user the GNUStep configuration for the sogo user:

```
# ln -s /etc/sogo/GNUstep /root/GNUstep

```

### Initial Postfix configuration

#### Basic configuratoin

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

#### Virtual user configuration

Create a vmail user and set up Postfix to use it:

```
# groupadd -g 5000 vmail
# useradd -u 5000 -g vmail -s /usr/bin/nologin -d /home/vmail -m vmail
# chmod 750 /home/vmail
# postconf -e virtual_minimum_uid=5000
# postconf -e virtual_uid_maps=static:5000
# postconf -e virtual_gid_maps=static:5000
# postconf -e virtual_mailbox_base=/home/vmail
# postfix reload

```

#### LDAP configuration

Next, allow Postfix to lookup users. To do this, create an unprivileged user to use for LDAP lookups (select a suitably strong password, 63 alpha-numeric various case should be good):

```
# samba-tool user create ldap --description="Unprivileged user for LDAP lookups"

```

Since this is a service account, set it to not expire:

```
# samba-tool user setexpiry ldap --noexpiry

```

Now, create a LDAP alias and group maps for Postfix pasting the following lines in the file `/etc/postfix/ldap-alias.cf` as root (replace dc=**internal**,dc=**domain**,dc=**tld** with appropriate values and **axhnTc2LGdnUKQ80cWjWzZBR79SkgAQ1uLxv94M8EDosDoPBqD4bEEvJ1XvpwI7** with a random password of your choosing):

```
# Directory settings
server_host = 127.0.0.1
search_base = dc=**internal**,dc=**domain**,dc=**tld**
scope = sub
version = 3

# User Binding
bind = yes
bind_dn = cn=ldap,cn=users,dc=**internal**,dc=**domain**,dc=**tld**
bind_pw = **axhnTc2LGdnUKQ80cWjWzZBR79SkgAQ1uLxv94M8EDosDoPBqD4bEEvJ1XvpwI7**

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

At this point, Dovecot will need to be configured before completing the Postfix configuration as Dovecot SASL and LMTP will be used for authentication and delivery (respectively).

### Dovecot configuration

#### Basic configuration

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

#### LDAP configuration

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

Create the LDAP user and password configuration files (replace dc=**internal**,dc=**domain**,dc=**tld** and **INTERNAL** with appropropriate values):

`/etc/dovecot/dovecot-ldap-passdb.conf`

```
hosts = localhost
auth_bind = yes
auth_bind_userdn = **INTERNAL**\%u
ldap_version = 3
base = dc=**internal**,dc=**domain**,dc=**tld**
scope = subtree
deref = never
pass_filter = (&(objectClass=person)(sAMAccountName=%u)(mail=*))

```

`/etc/dovecot/dovecot-ldap-userdb.conf`

```
hosts = localhost
dn = cn=ldap,cn=Users,dc=**internal**,dc=**domain**,dc=**tld**
dnpass = **axhnTc2LGdnUKQ80cWjWzZBR79SkgAQ1uLxv94M8EDosDoPBqD4bEEvJ1XvpwI7**
ldap_version = 3
# The base must be cn=Users for OpenChange ATM...future
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

#### Testing Dovecot authentication

Open a _telnet_ session and test (commands you enter are in bold, replace _xxxxxxxx_ with your real password):

```
**telnet localhost 143**
Trying 127.0.0.1...
Connected to localhost.
Escape character is '^]'.
* OK [CAPABILITY IMAP4rev1 LITERAL+ SASL-IR LOGIN-REFERRALS ID ENABLE IDLE AUTH=PLAIN AUTH=LOGIN] Dovecot ready.
**a LOGIN Administrator xxxxxxxx**
. OK [CAPABILITY IMAP4rev1 LITERAL+ SASL-IR LOGIN-REFERRALS ID ENABLE IDLE SORT SORT=DISPLAY THREAD=REFERENCES THREAD=REFS THREAD=ORDEREDSUBJECT MULTIAPPEND  URL-PARTIAL CATENATE UNSELECT CHILDREN NAMESPACE UIDPLUS LIST-EXTENDED I18NLEVEL=1 CONDSTORE QRESYNC ESEARCH ESORT SEARCHRES WITHIN CONTEXT=SEARCH LIST-STATUS SPECIAL-USE BINARY MOVE] Logged in
**a LOGOUT**
* BYE Logging out
. OK Logout completed.
Connection closed by foreign host.

```

If anything other than OK is returned, go back and double check the configuration before continuing.

#### LMTP configuration

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

#### TLS configuration

Put your certificates into place and create the TLS configuration file `/etc/dovecot/conf.d/tls.conf` (adjust paths and names as necessary). The keyfile should be owned by root with 0400 permissions. Any intermediate certificates should be concatenated after the public cert:

```
ssl = yes
ssl_cert = </etc/dovecot/ssl/**host**.**domain**.**tld**.pem
ssl_key = </etc/dovecot/ssl/**host**.**domain**.**tld**.key

```

```
# chmod 644 /etc/dovecot/conf.d/tls.conf

```

Remove the earlier explicitly defined values from `local.conf` and reload Dovecot:

```
# sed -e '/^ssl/d' -e '/disable_plaintext/s/no/yes/' \
      -i /etc/dovecot/conf.d/local.conf
# dovecot reload

```

#### Sieve configuration

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

### Postfix final configuration

#### SASL configuration

Modify the default smtpd instance:

```
# postconf -e smtpd_sasl_type=dovecot
# postconf -e smtpd_sasl_path=private/auth
# postconf -e smtpd_sasl_auth_enable=yes
# postconf -e smtpd_relay_restrictions="permit_mynetworks, permit_sasl_authenticated, reject_unauth_destination"

```

#### LMTP configuration

Use dovecot LMTP for delivery:

```
# postconf -e virtual_transport=lmtp:unix:private/dovecot-lmtp

```

#### TLS configuration

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
bind_pw = **axhnTc2LGdnUKQ80cWjWzZBR79SkgAQ1uLxv94M8EDosDoPBqD4bEEvJ1XvpwI7**

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

#### Testing the Postfix SASL configuration

Begin by getting a base64 encoded version of the username and password (replace **xxxxxxxx** with your real password):

```
$ echo -ne '\000Administrator\000**xxxxxxxx'** | openssl base64

```

You should receive output similar to the following:

```
AEFkbWluaXN0cmF0b3IAeHh4eHh4eHg=

```

Now, open a _telnet_ session and test (commands you enter are in bold, replace **host.domain.tld** with the real external FQDN and **AEFkbWluaXN0cmF0b3IAeHh4eHh4eHg=** with the result of the previous command):

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
**AUTH PLAIN AEFkbWluaXN0cmF0b3IAeHh4eHh4eHg=**
235 2.7.0 Authentication successful
**quit**
221 2.0.0 Bye
Connection closed by foreign host.

```

If anything other than a 235 message is returned, something is wrong and you should troubleshoot now rather than later.

At ths point, you have a fully functional mail server, though you will probably want to lock it down a bit tighter (which is not covered in this article). You could easily stop now and use any mail client you wish, howerver, you would miss out on the fun of Outlook, RPC/HTTPS, calendar, the GAL, and contacts. This additional functionality is provided by SOGo and OpenChange...

### SOGo final configuration

#### PostgreSQL

If using PostgreSQL, you'll need to select a strong password (63 random alphanumeric characters is good) for the sogo user and change it now:

```
# su - postgres
$ psql
ALTER USER sogo WITH PASSWORD 'ZpRTOZuQiaKBma4YhvozRJwXCbLqhnRiurhvidB9A8vbjxEoNNjbAwHSbpBTobT';
\q

```

#### SOGo

Create a suitable SOGo configuration file in `/etc/sogo/sogo.conf` (replace items in bold with appropriate values). If using PostgreSQL, replace the "mysql:" lines with the appropriate "postgresql:" lines (as above):

```
{
    /* Database Configuration */
    SOGoProfileURL = "mysql://openchange:**OpenchangePW**@localhost/openchange/sogo_user_profile";
    OCSFolderInfoURL = "mysql://openchange:**OpenchangePW**@localhost/openchange/sogo_folder_info";
    OCSSessionsFolderURL = "mysql://openchange:**OpenchangePW**@localhost/openchange/sogo_sessions_folder";

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

    /* User Authentication */
    SOGoUserSources = (
     {
        id = directory;
        displayName = "Active Directory";
        canAuthenticate = YES;
        type = ldap;
        CNFieldName = cn;
        IDFieldName = cn;
        UIDFieldName = sAMAccountName;
        baseDN = "dc=**internal**,dc=**domain**,dc=**tld**";
        bindDN = "cn=ldap,cn=Users,dc=**internal**,dc=**domain**,dc=**tld**";
        bindFields = (sAMAccountName);
        bindPassword = **axhnTc2LGdnUKQ80cWjWzZBR79SkgAQ1uLxv94M8EDosDoPBqD4bEEvJ1XvpwI7**;
        hostname = ldap://127.0.0.1:389;
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
        hostname = ldap://127.0.0.1:389;
        baseDN = "dc=**internal**,dc=**domain**,dc=**tld**";
        bindDN = "cn=ldap,cn=Users,dc=**internal**,dc=**domain**,dc=**tld**";
        bindPassword = **axhnTc2LGdnUKQ80cWjWzZBR79SkgAQ1uLxv94M8EDosDoPBqD4bEEvJ1XvpwI7**;
        filter = "((NOT isCriticalSystemObject='TRUE') AND (mail=\'*\') AND (NOT objectClass=contact))";
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
        hostname = ldap://127.0.0.1:389;
        baseDN = "dc=**internal**,dc=**domain**,dc=**tld**";
        bindDN = "cn=ldap,cn=Users,dc=**internal**,dc=**domain**,dc=**tld**";
        bindPassword = **axhnTc2LGdnUKQ80cWjWzZBR79SkgAQ1uLxv94M8EDosDoPBqD4bEEvJ1XvpwI7**;
        filter = "((((objectClass=person) AND (objectClass=contact) AND ((uidNumber>=2000) OR (mail='*')))
                 AND (NOT isCriticalSystemObject='TRUE') AND (NOT showInAdvancedViewOnly='TRUE') AND (NOT uid=Guest))
                 OR (((objectClass=group) AND (gidNumber>=2000)) AND (NOT isCriticalSystemObject='TRUE') AND (NOT showInAdvancedViewOnly='TRUE')))";
        mapping = {
            displayname = ("cn");
        };
      }
    );

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
# rm /etc/sogo/GNUstep/Defaults/sogod.plist
# mkdir /var/spool/sogo
# chown sogo:sogo /var/spool/sogo
# chmod 700 /var/spool/sogo

```

Now enable and start the `memcached` service and restart the `sogo` service. Test by visiting http://**server.internal.domain.tld**/SOGo/ .

#### Apache httpd

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

### OpenChange final configuration

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

**This article or section is out of date.**

**Reason:** Recent versions of Samba have left OCSManager/MAPIProxy in an unusable state. Fortunately, with SOGo-2.2, the new ActiveSync code should eliminate the need for OCSManager with Outlook 2013+. Autodiscover is working as expected now, but free/busy lookups are broken making EWS unusable. (Discuss in [Talk:OpenChange server#](https://wiki.archlinux.org/index.php/Talk:OpenChange_server))

#### OCSManager

OCSManager is a Python-Paste serverlet that listens specifically for autodiscover, EWS, and RPCProxy requests. Create a backup copy of the `/etc/ocsmanager/ocsmanager.ini` file:

```
# mv /etc/ocsmanager/ocsmanager.ini{,.bak}

```

Setup OCSMangaer with the `/etc/ocsmanager/ocsmanager.ini` file (replace the items in bold type with appropriate values):

```
#
# ocsmanager - Pylons configuration
#
# The %(here)s variable will be replaced with the parent directory of this file
#
[DEFAULT]
debug = true
email_to = **postmaster@domain.tld**
smtp_server = localhost
error_email_from = **postmaster@domain.tld**

[main]
auth = ldap
mapistore_root = /var/lib/samba/private
mapistore_data = /var/lib/samba/private/mapistore
debug = yes

[auth:ldap]
host = ldap://**server.domain.tld**
port = 389
bind_dn = **CN=Users,DC=internal,DC=domain,DC=tld**
bind_pw = **axhnTc2LGdnUKQ80cWjWzZBR79SkgAQ1uLxv94M8EDosDoPBqD4bEEvJ1XvpwI7**
basedn = **CN=ldap,CN=Users,DC=internal,DC=domain,DC=tld**
#filter = (cn=%s)
#attrs = userPassword, x-isActive

[server:main]
use = egg:Paste#http
host = **server.internal.domain.tld**
port = 5000
protocol_version = HTTP/1.1

[app:main]
use = egg:ocsmanager
full_stack = true
static_files = true
cache_dir = %(here)s/data
beaker.session.key = ocsmanager
beaker.session.secret = SDyKK3dKyDgW0mlpqttTMGU1f
app_instance_uuid = {ee533ebc-f266-49d1-ae10-d017ee6aa98c}
NTLMAUTHHANDLER_WORKDIR = /var/cache/ntlmauthhandler
SAMBA_HOST = **server.internal.domain.tld**

[rpcproxy:ldap]
host = **server.internal.domain.tld**
port = 389
basedn = **CN=Users,DC=internal,DC=domain,DC=tld**

# WARNING: *THE LINE BELOW MUST BE UNCOMMENTED ON A PRODUCTION ENVIRONMENT*
# Debug mode will enable the interactive debugging tool, allowing ANYONE to
# execute malicious code after an exception is raised.
set debug = false

[autodiscover]
# The client address that is not in these networks have RPC/Proxy
# prioritaised. It only works for Outlook 2010 or higher. Delimiter: ,
# internal_networks = 0.0.0.0/0

[autodiscover:rpcproxy]
# Enabled RPC/Proxy or not
enabled = true
# We assume the autodiscover host and the EWS (Free/Busy) are in the same host
external_hostname = **mail.domain.tld**
# Require SSL to logon. Default value is false
ssl = true

[outofoffice]
# Set the backend.
# Possible backends: file, managesieve
# file makes sieve and OCSManager lives in the same host
# managesieve indicates the server to put/get the sieve script
backend = file

[outofoffice:file]
# Path of the sieve script for the user
#   Expansion variables (example user.name@example.com):
#       $domain   = example.com
#       $user     = user.name
#       $fulluser = user.name@example.com
sieve_script_path = /var/vmail/$user/sieve/sieve-script
# If the sieve script directory hierarchy does not exist, it will be created
sieve_script_path_mkdir = true

[outofoffice:managesieve]
# It requires to have a master password to get into every account
# server = 127.0.0.1
# SSL on/off
# ssl = true
# Master password
# secret = secret

# Logging configuration
[loggers]
keys = root

[handlers]
keys = console

[formatters]
keys = generic

[logger_root]
level = INFO
handlers = console

[handler_console]
class = StreamHandler
args = (sys.stderr,)
level = NOTSET
formatter = generic

[formatter_generic]
format = %(asctime)s %(levelname)-5.5s [%(name)s] [%(threadName)s] %(message)s

```

Create the mapistore and cache directories:

```
# mkdir -p /var/lib/samba/private/mapistore

```

Then start and enable `ocsmanager` service.

#### Adding OpenChange MAPIProxy and OCSManger to Apache httpd

This is the part that glues it all together. Add the following to the end of `/etc/httpd/conf/httpd.conf` file (or virtual host configuration file):

```
LoadModule wsgi_module modules/mod_wsgi.so
include conf/extra/rpcproxy.conf
include conf/extra/ocsmanager-apache.conf

```

Now just restart `httpd` and `samba`. If you have made it this far, and your DNS is configured correctly, you should be able to configure an Outlook client with only an email address, username, and password. For Outlook (or other MAPI clients that support RPC/HTTPS, you need open only port 443, at the edge. Obviously, you still need to consider additional configuration for Postfix (spam and virus filtering, more restrictive use of SMTPD and SMTP, open ports 25 and 587) if you intend to receive mail from the internet. You will probably also want to move the various HTTPD pieces into virtual hosts, provide redirection on 80 for secure services, etc., but those exercises are covered in great detail elsewhere.

Retrieved from "[https://wiki.archlinux.org/index.php?title=OpenChange_server&oldid=411689](https://wiki.archlinux.org/index.php?title=OpenChange_server&oldid=411689)"