[Open-Xchange](http://ox.io) is a groupware solution providing Mail facilities, Calendaring, shared Contacts and Google-Docs-like text editing.

## Contents

*   [1 Prerequisites](#Prerequisites)
*   [2 Installation](#Installation)
    *   [2.1 From the custom repository](#From_the_custom_repository)
*   [3 Configuration](#Configuration)
    *   [3.1 Initialize the configdb](#Initialize_the_configdb)
    *   [3.2 Initialize the server](#Initialize_the_server)
    *   [3.3 Initialize the first server instance](#Initialize_the_first_server_instance)
    *   [3.4 Create the file store for OX Drive](#Create_the_file_store_for_OX_Drive)
    *   [3.5 Register the Database and Filestore with the server](#Register_the_Database_and_Filestore_with_the_server)
    *   [3.6 Webserver configuration](#Webserver_configuration)
        *   [3.6.1 Apache](#Apache)
            *   [3.6.1.1 Modules](#Modules)
            *   [3.6.1.2 Create the config files by hand](#Create_the_config_files_by_hand)
            *   [3.6.1.3 Install config files from repository](#Install_config_files_from_repository)
            *   [3.6.1.4 Start the Webserver](#Start_the_Webserver)
        *   [3.6.2 nginx](#nginx)
    *   [3.7 Create default context](#Create_default_context)
    *   [3.8 Create your first user](#Create_your_first_user)
    *   [3.9 Restart Open-Xchange](#Restart_Open-Xchange)
    *   [3.10 First login](#First_login)
    *   [3.11 Enable Open-Xchange to run at startup](#Enable_Open-Xchange_to_run_at_startup)
*   [4 Additional Modules](#Additional_Modules)
    *   [4.1 Sieve/Mailfilter](#Sieve.2FMailfilter)
    *   [4.2 Caldav/Carddav](#Caldav.2FCarddav)
    *   [4.3 Text/Spreadsheet](#Text.2FSpreadsheet)
        *   [4.3.1 Spellchecking](#Spellchecking)
    *   [4.4 Document templates](#Document_templates)
*   [5 Troubleshooting](#Troubleshooting)
*   [6 Package origin](#Package_origin)
*   [7 See also](#See_also)

## Prerequisites

In order to use Open-Xchange, you need an empty, configured [MySQL](/index.php/MySQL "MySQL") installation as well as a configured instance of [Postfix](/index.php/Postfix "Postfix"), [Dovecot](/index.php/Dovecot "Dovecot") and [Apache](/index.php/Apache "Apache"). Additionally, Open-Xchange does currently not work with OpenJDK. You will need oracles [jre](https://aur.archlinux.org/packages/jre/) from the [AUR](/index.php/AUR "AUR").

## Installation

Open-Xchange is available in the [AUR](/index.php/AUR "AUR"). Right now, no meta-package exists. Alternatively, it can be installed from the custom repository of the current maintainer. Taking the AUR approach is highly recommended. Package names are the same as upstream, and the same between the custom repo and the AUR.

[Install](/index.php/Install "Install") the following packages: [open-xchange](https://aur.archlinux.org/packages/open-xchange/) [open-xchange-authentication-database](https://aur.archlinux.org/packages/open-xchange-authentication-database/) [open-xchange-grizzly](https://aur.archlinux.org/packages/open-xchange-grizzly/) [open-xchange-admin](https://aur.archlinux.org/packages/open-xchange-admin/) [open-xchange-appsuite](https://aur.archlinux.org/packages/open-xchange-appsuite/) [open-xchange-appsuite-backend](https://aur.archlinux.org/packages/open-xchange-appsuite-backend/) [open-xchange-appsuite-manifest](https://aur.archlinux.org/packages/open-xchange-appsuite-manifest/)

### From the custom repository

Add the following lines to your pacman.conf:

 `/etc/pacman.conf` 

```
[ox]
Server = http://repo.lynxcore.org/ox/
```

## Configuration

### Initialize the configdb

For some reason, Open-Xchange expects an MySQL-Server without a set root password. So reset the password in your MySQL instance before continuing. The initconfigdb script does not set a new root password, so you are good to set a new one after the installation has finished.

```
# /opt/open-xchange/sbin/initconfigdb --configdb-pass=YOUR-DB-PASSWORD -a

```

### Initialize the server

`MAX_MEMORY_FOR_JAVAVM` as a rule of thumb for simple installations should be half available system memory. The value must be in MB. For example "1024" for 1GB .

```
# /opt/open-xchange/sbin/oxinstaller --add-license=YOUR-OX-LICENSE-CODE --servername=oxserver --configdb-pass=YOUR-DB-PASSWORD --master-pass=YOUR-ADMIN-MASTER-PASSWORD --network-listener-host=localhost --servermemory MAX_MEMORY_FOR_JAVAVM
# systemctl start open-xchange

```

### Initialize the first server instance

```
# /opt/open-xchange/sbin/registerserver -n oxserver -A oxadminmaster -P YOUR-ADMIN-MASTER-PASSWORD

```

### Create the file store for OX Drive

You can modify the folder that's used for this.

```
# mkdir /var/opt/filestore
# chown open-xchange:open-xchange /var/opt/filestore

```

### Register the Database and Filestore with the server

```
# /opt/open-xchange/sbin/registerfilestore -A oxadminmaster -P YOUR-ADMIN-MASTER-PASSWORD -t file:/var/opt/filestore -s 1000000
# /opt/open-xchange/sbin/registerdatabase -A oxadminmaster -P YOUR-ADMIN-MASTER-PASSWORD -n oxdatabase -p YOUR-DB-PASSWORD -m true

```

### Webserver configuration

#### Apache

##### Modules

Make sure to enable the following modules in /etc/httpd/conf/httpd.conf:

```
proxy proxy_http proxy_balancer expires deflate headers rewrite mime setenvif lbmethod_byrequests

```

Add the following includes to `/etc/http/conf/httpd.conf`:

```
Include conf/extra/proxy_http.conf
Include conf/extra/ox.conf

```

##### Create the config files by hand

Create the following two files:

 `/etc/httpd/conf/extra/proxy_http.conf` 

```
LoadModule proxy_http_module modules/mod_proxy_http.so

<IfModule mod_proxy_http.c>
   ProxyRequests Off
   ProxyStatus On
   # When enabled, this option will pass the Host: line from the incoming request to the proxied host.
   ProxyPreserveHost On
   # Please note that the servlet path to the soap API has changed:
   <Location /webservices>
       # restrict access to the soap provisioning API
       Order Deny,Allow
       Deny from all
       Allow from 127.0.0.1
       # you might add more ip addresses / networks here
       # Allow from 192.168 10 172.16
   </Location>

   # The old path is kept for compatibility reasons
   <Location /servlet/axis2/services>
       Order Deny,Allow
       Deny from all
       Allow from 127.0.0.1
   </Location>

   # Enable the balancer manager mentioned in
   # http://oxpedia.org/wiki/index.php?title=AppSuite:Running_a_cluster#Updating_a_Cluster
   <IfModule mod_status.c>
     <Location /balancer-manager>
       SetHandler balancer-manager
       Order Deny,Allow
       Deny from all
       Allow from 127.0.0.1
     </Location>
   </IfModule>

   <Proxy balancer://oxcluster>
       Order deny,allow
       Allow from all
       # multiple server setups need to have the hostname inserted instead localhost
       BalancerMember http://localhost:8009 timeout=100 smax=0 ttl=60 retry=60 loadfactor=50 route=APP1
       # Enable and maybe add additional hosts running OX here
       # BalancerMember http://oxhost2:8009 timeout=100 smax=0 ttl=60 retry=60 loadfactor=50 route=APP2
      ProxySet stickysession=JSESSIONID|jsessionid scolonpathdelim=On
      SetEnv proxy-initial-not-pooled
      SetEnv proxy-sendchunked
   </Proxy>

   # The standalone documentconverter(s) within your setup (if installed)
   # Make sure to restrict access to backends only
   # See: http://httpd.apache.org/docs/$YOUR_VERSION/mod/mod_authz_host.html#allow for more infos
   #<Proxy balancer://oxcluster_docs>
   #    Order Deny,Allow
   #    Deny from all
   #    Allow from backend1IP
   #    BalancerMember http://converter_host:8009 timeout=100 smax=0 ttl=60 retry=60 loadfactor=50 keepalive=On route=APP3
   #    ProxySet stickysession=JSESSIONID|jsessionid scolonpathdelim=On
   #	   SetEnv proxy-initial-not-pooled
   #    SetEnv proxy-sendchunked
   #</Proxy>
   # Define another Proxy Container with different timeout for the sync clients. Microsoft recommends a minimum value of 15 minutes.
   # Setting the value lower than the one defined as com.openexchange.usm.eas.ping.max_heartbeat in eas.properties will lead to connection
   # timeouts for clients.  See http://support.microsoft.com/?kbid=905013 for additional information.
   #
   # NOTE for Apache versions < 2.4:
   # When using a single node system or using BalancerMembers that are assigned to other balancers please add a second hostname for that
   # BalancerMember's IP so Apache can treat it as additional BalancerMember with a different timeout.
   #
   # Example from /etc/hosts: 127.0.0.1	localhost localhost_sync
   #
   # Alternatively select one or more hosts of your cluster to be restricted to handle only eas/usm requests
   <Proxy balancer://eas_oxcluster>
      Order deny,allow
      Allow from all
      # multiple server setups need to have the hostname inserted instead localhost
      BalancerMember http://localhost_sync:8009 timeout=1900 smax=0 ttl=60 retry=60 loadfactor=50 route=APP1
      # Enable and maybe add additional hosts running OX here
      # BalancerMember http://oxhost2:8009 timeout=1900  smax=0 ttl=60 retry=60 loadfactor=50 route=APP2
      ProxySet stickysession=JSESSIONID|jsessionid scolonpathdelim=On
      SetEnv proxy-initial-not-pooled
      SetEnv proxy-sendchunked
   </Proxy>

   # When specifying additional mappings via the ProxyPass directive be aware that the first matching rule wins. Overlapping urls of
   # mappings have to be ordered from longest URL to shortest URL.
   # 
   # Example:
   #   ProxyPass /ajax      balancer://oxcluster_with_100s_timeout/ajax
   #   ProxyPass /ajax/test balancer://oxcluster_with_200s_timeout/ajax/test
   #
   # Requests to /ajax/test would have a timeout of 100s instead of 200s 
   #   
   # See:
   # - http://httpd.apache.org/docs/current/mod/mod_proxy.html#proxypass Ordering ProxyPass Directives
   # - http://httpd.apache.org/docs/current/mod/mod_proxy.html#workers Worker Sharing
   ProxyPass /ajax balancer://oxcluster/ajax
   ProxyPass /appsuite/api balancer://oxcluster/ajax
   ProxyPass /drive balancer://oxcluster/drive
   ProxyPass /infostore balancer://oxcluster/infostore
   ProxyPass /publications balancer://oxcluster/publications
   ProxyPass /realtime balancer://oxcluster/realtime
   ProxyPass /servlet balancer://oxcluster/servlet
   ProxyPass /webservices balancer://oxcluster/webservices

   #ProxyPass /documentconverterws balancer://oxcluster_docs/documentconverterws

   ProxyPass /usm-json balancer://eas_oxcluster/usm-json
   ProxyPass /Microsoft-Server-ActiveSync balancer://eas_oxcluster/Microsoft-Server-ActiveSync

</IfModule>
```

 `/etc/httpd/conf/extra/ox.conf` 

```
<VirtualHost *:80>
       ServerAdmin webmaster@localhost

       DocumentRoot /var/www/html
       <Directory /var/www/html>
               Options Indexes FollowSymLinks MultiViews
               AllowOverride None
               Order allow,deny
               allow from all
               Require all granted
               RedirectMatch ^/$ /appsuite/
       </Directory>

       <Directory /var/www/html/appsuite>
               Options None +SymLinksIfOwnerMatch
               Require all granted
               AllowOverride Indexes FileInfo
       </Directory>
</VirtualHost>
```

##### Install config files from repository

Alternatively, you can install the config files from the custom repository:

```
# pacman -S open-xchange-apache-conf

```

##### Start the Webserver

```
# systemctl start httpd

```

#### nginx

[nginx](/index.php/Nginx "Nginx") is not currently supported. If you absolutely MUST use nginx, configure apache to listen on some other port and let nginx proxy requests to apache. Edit `/etc/http/conf/httpd.conf`:

```
# Listen: Allows you to bind Apache to specific IP addresses and/or
# ports, instead of the default. See also the <VirtualHost>
# directive.
#
# Change this to Listen on specific IP addresses as shown below to
# prevent Apache from glomming onto all bound IP addresses.
#
#Listen 80
Listen 127.0.0.1:8080

```

This will make apache listen on port 8080 and only for connections from localhost. Next, add a new server block to your `/etc/nginx/nginx.conf`:

```
server {
    listen       80;
    server_name  your.domain.tld;
    [...]
    location / {
        proxy_pass [http://localhost:8080](http://localhost:8080);
    }
}

```

Not the nicest solution, but the only one possible at the moment.

### Create default context

```
# /opt/open-xchange/sbin/createcontext -A oxadminmaster -P YOUR-ADMIN-MASTER-PASSWORD -c 1 -u oxadmin -d "Context Admin" -g Admin -s User -p YOUR-ADMIN-PASSWORD -L defaultcontext -e oxadmin@YOURDOMAIN.tld -q 1024 --access-combination-name=groupware_standard

```

### Create your first user

```
# /opt/open-xchange/sbin/createuser -c 1 -A oxadmin -P YOUR-ADMIN-PASSWORD -u USERNAME -d "DISPLAYNAME" -g GIVENNAME -s SURNAME -p YOUR-USER-PASSWORD -e EMAIL@YOURDOMAIN.TLD --imaplogin IMAPSERVER-USERNAME --imapserver IMAPSERVER --smtpserver SMTPSERVER

```

### Restart Open-Xchange

```
# systemctl restart open-xchange

```

### First login

Navigate your Browser to http://your.domain.tld Log in with the credentials of the testuser you just created.

### Enable Open-Xchange to run at startup

```
# systemctl enable httpd mysqld open-xchange

```

## Additional Modules

### Sieve/Mailfilter

If you have [Sieve](/index.php/Dovecot#Sieve "Dovecot") configured, you can add the [b]mailfilter[/b] module to edit your sieve rules from within Open-Xchange.

Install [open-xchange-mailfilter](https://aur.archlinux.org/packages/open-xchange-mailfilter/) and edit /opt/open-xchange/eetc/mailfilter.properties from

 `/opt/open-xchange/etc/mailfilter.properties`  `SIEVE_CREDSRC=session` 

to

 `/opt/open-xchange/etc/mailfilter.properties` 

```
#SIEVE_CREDSRC=session
SIEVE_CREDSRC=imapLogin
```

Afterwards, restart Open-Xchange:

```
# systemctl restart open-xchange

```

### Caldav/Carddav

Install [open-xchange-dav](https://aur.archlinux.org/packages/open-xchange-dav/) from the [AUR](/index.php/AUR "AUR") or from the unofficial repository.

Edit /opt/open-xchange/etc/caldav.properties:

 `/opt/open-xchange/etc/caldav.properties`  `com.openexchange.caldav.enabled=true` 

Edit /opt/open-xchange/etc/groupware/carddav.properties:

 `/opt/open-xchange/etc/groupware/carddav.properties`  `com.openexchange.carddav.enabled=true` 

Edit `/etc/httpd/conf/extra/ox.conf` and insert the following before </VirtualHost>:

```
RewriteEngine On
RewriteCond %{HTTP_USER_AGENT}      Calendar           [OR]
RewriteCond %{HTTP_USER_AGENT}      Reminders          [OR]
RewriteCond %{HTTP_USER_AGENT}      DataAccess         [OR]
RewriteCond %{HTTP_USER_AGENT}      DAVKit             [OR]
RewriteCond %{HTTP_USER_AGENT}      Lightning          [OR]
RewriteCond %{HTTP_USER_AGENT}      Adresboek          [OR]
RewriteCond %{HTTP_USER_AGENT}      dataaccessd        [OR]
RewriteCond %{HTTP_USER_AGENT}      Preferences        [OR]
RewriteCond %{HTTP_USER_AGENT}      Adressbuch         [OR]
RewriteCond %{HTTP_USER_AGENT}      AddressBook        [OR]
RewriteCond %{HTTP_USER_AGENT}      Address\ Book      [OR]
RewriteCond %{HTTP_USER_AGENT}      CalendarStore      [OR]
RewriteCond %{HTTP_USER_AGENT}      CalendarAgent      [OR]
RewriteCond %{HTTP_USER_AGENT}      accountsd          [OR]
RewriteCond %{HTTP_USER_AGENT}      eM\ Client         [OR]
RewriteCond %{HTTP_USER_AGENT}      CoreDAV
RewriteRule (.*)                  [http://localhost:8009/servlet/dav$1](http://localhost:8009/servlet/dav$1)     [P] # for grizzly http service

```

Note that this isn't the cleanest solution, but I haven't gotten the cleaner one (two VirtualHosts) to work yet.

Restart open-xchange:

```
# systemctl restart open-xchange

```

### Text/Spreadsheet

Get the following packages from the [AUR](/index.php/AUR "AUR") or from the custom repository: [open-xchange-documents-backend](https://aur.archlinux.org/packages/open-xchange-documents-backend/) [open-xchange-documents-ui](https://aur.archlinux.org/packages/open-xchange-documents-ui/) [open-xchange-documents-ui-static](https://aur.archlinux.org/packages/open-xchange-documents-ui-static/) [open-xchange-documents-ui-common](https://aur.archlinux.org/packages/open-xchange-documents-ui-common/) [open-xchange-documents-ui-editors](https://aur.archlinux.org/packages/open-xchange-documents-ui-editors/) [calcengine](https://aur.archlinux.org/packages/calcengine/)

Edit /opt/open-xchange/etc/documents.properties:

 `/opt/open-xchange/etc/documents.properties` 

```
# Enables or disables the "text" module capability globally.
com.openexchange.capability.text=true

# Enables or disables the "spreadsheet" module capability globally.
com.openexchange.capability.spreadsheet=true
```

Edit /opt/open-xchange/etc/permissions.properties

 `/opt/open-xchange/etc/permissions.properties`  `permissions=..,text,spreadsheet,..` 

Edit /opt/open-xchange/etc/calcengine.properties:

 `/opt/open-xchange/etc/calcengine.properties`  `calcengine.mode=local` 

Restart open-xchange:

```
# systemctl restart open-xchange

```

#### Spellchecking

You will need [hunspell](https://www.archlinux.org/packages/?name=hunspell) and an appropriate language pack for it. For example:

```
# pacman -S hunspell hunspell-en

```

### Document templates

Install [open-xchange-documents-templates](https://aur.archlinux.org/packages/open-xchange-documents-templates/) fromt he [AUR](/index.php/AUR "AUR")

Restart open-xchange:

```
# systemctl restart open-xchange

```

## Troubleshooting

Open-Xchange logs extensively to `/var/log/open-xchange`. Most errors occur because conflicting modules have been installed.

## Package origin

Since the AUR packages have been built from the Debian 8 packages, every link to Documentation will pertain to the Debian 8 version of the documentation.

## See also

*   [Official homepage](http://ox.io)
*   [Installation Guide for Debian 8](http://oxpedia.org/wiki/index.php?title=AppSuite:Open-Xchange_Installation_Guide_for_Debian_8.0)
*   [Archlinux Forums Thread](https://bbs.archlinux.org/viewforum.php?id=38)