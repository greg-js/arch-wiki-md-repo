# Kolab

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [Citadel groupware](/index.php/Citadel_groupware "Citadel groupware")
*   [Open-xchange](/index.php/Open-xchange "Open-xchange")

[Kolab](http://kolab.org) is an unified communication and collaboration system, composed of a server-side daemon which offers storage and synchronization capabilities for contact, calendar, mail and file data. Clients can use several well defined formats like vCard, iCal, XML, IMAP and LDAP to communicate with the Kolab server.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Arch-specific configuration](#Arch-specific_configuration)
    *   [2.2 Kolab configuration](#Kolab_configuration)
*   [3 First steps](#First_steps)
    *   [3.1 Creating a user](#Creating_a_user)
    *   [3.2 Enabling proper TLS](#Enabling_proper_TLS)
*   [4 Frontends](#Frontends)
    *   [4.1 Roundcubemail Plugin](#Roundcubemail_Plugin)
*   [5 Start/stop the services](#Start.2Fstop_the_services)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 PHP Error: required kolabformat module not found](#PHP_Error:_required_kolabformat_module_not_found)
    *   [6.2 Error creating tasks / Tasks are not syncronized with Roundcube](#Error_creating_tasks_.2F_Tasks_are_not_syncronized_with_Roundcube)
    *   [6.3 Web interface is slow when accessing IMAP folders](#Web_interface_is_slow_when_accessing_IMAP_folders)
*   [7 See also](#See_also)

## Installation

Kolab server is available in the [AUR](/index.php/AUR "AUR") via the [kolab](https://aur.archlinux.org/packages/kolab/)<sup><small>AUR</small></sup> meta-package. This package will install all Kolab components, as well as the neccesary external services: [cyrus-imapd](https://aur.archlinux.org/packages/cyrus-imapd/)<sup><small>AUR</small></sup>, [Postfix](/index.php/Postfix "Postfix"), [389-ds-base](https://aur.archlinux.org/packages/389-ds-base/)<sup><small>AUR</small></sup>, [MySQL](/index.php/MySQL "MySQL"), [Amavis](/index.php/Amavis "Amavis"), [ClamAV](/index.php/ClamAV "ClamAV"), [SpamAssassin](/index.php/Postfix#SpamAssassin "Postfix") and [Apache](/index.php/Apache "Apache") with [PHP](/index.php/PHP "PHP") support.

## Configuration

**Warning:** Kolab changes the configuration of many system components. If you use any of the services listed above, you may want to backup your configuration, as the Kolab installation process is likely to overwrite part of it

At first, Kolab requires you to use a FQDN (fully qualified domain name), with at least three dot-separated parts. Therefore adjust and append:

 `/etc/hosts`  `192.168.1.101 kolab.example.org` 

Write the same domain name into _/etc/hostname_. You should also check your DNS settings and reverse DNS resolution.

### Arch-specific configuration

Kolab makes many assumptions about the system it is installing on. The [kolab](https://aur.archlinux.org/packages/kolab/)<sup><small>AUR</small></sup> packages ships with an script that brings the system to a state where the Kolab setup script is useful. Run it as root:

```
# arch-setup-kolab

```

This will:

*   Check your FQDN (can be skipped adding the `--no-fqdn` option)
*   Initialize or update the ClamAV and SpamAssassin databases
*   Initialize the Cyrus IMAP cache directory
*   Create the Postfix aliases database (aliases.db)
*   Configure ClamAV to be able to access Amavis directories
*   Enable the PHP module in Apache
*   Add all Kolab applications to Apache in `/etc/httpd/conf/extra/kolab.conf`
*   Add Roundcube to Apache
*   Enable the required PHP extensions, and condigure the include_path and open_basedir in {{ic|/etc/php/conf.d/kolab.ini)
*   Configure libsasl to use the SASL daemon shipped with Kolab
*   Create a dummy certificate for localhost (`/etc/ssl/private/localhost.pem`) and install it as a trust anchor (`/etc/ca-certificates/trust-source/anchors/localhost.pem`)

### Kolab configuration

Kolab ships with its own configuration script (contained in [pykolab](https://aur.archlinux.org/packages/pykolab/)<sup><small>AUR</small></sup>. Run it as root:

```
# setup-kolab

```

This runs all configurations steps neccesary for Kolab. During the process, multiple questions will be asked, regarding passwords, etc. The defaults are fine for all but two questions:

*   The _password for the LDAP Directory Manager_ is the password you use for logging in to the web administration panel
*   When asked about MySQL, you should select _1: Existing MySQL server_ and then the password for the root MySQL user (by default, empty)

You can also list the steps with `setup-kolab help` and selectively run some of them.

## First steps

### Creating a user

The web admin panel is located at `[http://localhost/kolab-webadmin/](http://localhost/kolab-webadmin/)`. You can login using `cn=Directory Manager` as the user, and the password you chose during the previous step. You can recover the password by running:

```
$ grep ^bind_pw /etc/kolab/kolab.conf

```

You can then create a user and login as him in `[http://localhost/roundcube/](http://localhost/roundcube/)` by using the email address or the UID of the user and the assigned password.

More information in the Kolab documentation: [[1]](http://docs.kolab.org/installation-guide/first-login.html)

### Enabling proper TLS

The default installation creates a dummy localhost certificate, as some parts of Kolab (most notably kolabd) use TLS to communicate with the IMAP daemon. However, this will not work for external clients. In order to install a proper certificate you must edit the following files:

 `/etc/postfix/main.cf` 

```
# TLS
smtpd_tls_cert_file=/etc/ssl/private/localhost.pem
smtpd_tls_key_file=/etc/ssl/private/localhost.pem
```

 `/etc/cyrus/imapd.conf` 

```
tls_cert_file: /etc/ssl/private/localhost.pem
tls_key_file: /etc/ssl/private/localhost.pem
```

The cert_file should point to a PEM file containing your certificate (and intermediate CA certificates if that's the case), and the key_file should contain your PEM-encoded private key.

After that, restart Postfix and Cyrus imapd:

```
# systemctl restart postfix cyrus-master

```

Additionally, you have to change the Roundcube configuration in order to include your domain name instead of localhost. If not, certificate validation will fail (the server is presenting a certificate for the domain and Roundcube expects one for localhost) and the web interface will be unusable. Replace localhost with your domain name in the Roundcube configuration:

 `/etc/webapps/roundcubemail/config/config.inc.php` 

```
// IMAP Server Settings
$config['default_host'] = 'tls://localhost';

// SMTP Server Settings
$config['smtp_server'] = 'tls://localhost';
```

Finally, you can dispose of the temporary dummy certificate generated by the installation process:

```
# rm /etc/ssl/private/localhost.pem
# rm /etc/ca-certificates/trust-source/anchors/localhost.pem
# update-ca-trust

```

If you notice slow performance in roundcube, specially if you are using a big keypair, you may want to [disable TLS for local connections](#Web_interface_is_slow_when_accessing_IMAP_folders).

## Frontends

### Roundcubemail Plugin

Besides the basic [Roundcubemail](/index.php/Roundcubemail "Roundcubemail") installation and configuration, this [roundcubemail-plugins-kolab](https://aur.archlinux.org/packages/roundcubemail-plugins-kolab/)<sup><small>AUR</small></sup> plugin package is needed for advanced groupware functionality.

## Start/stop the services

The installation process should have enable and started all Kolab services. The following services are used by Kolab (and can be managed by systemctl):

*   389-ds-base.target: LDAP directory for configuration and authentication
*   amavisd: Bridge from Postfix to ClamAV and SpamAssassin
*   clamd: Virus scanning
*   cyrus-master: IMAP/PÔP3 server
*   httpd: Apache web server
*   kolabd: Synchronizes LDAP configuration with Cyrus IMAP (list of mailboxes)
*   kolab-saslauthd: Handles SASL auth for Postfix
*   mysqld: Database engine for RoundCube and Kolab components
*   postfix: SMTP server
*   wallace: Scans incoming mail for groupware content

## Troubleshooting

### PHP Error: required kolabformat module not found

Make sure that `/usr/share/php` is in the `include_path` and `open_basedir` variables in the PHP configuration. The most likely cause is that they are overwritten in the Roundcube Apache configuration (`/etc/httpd/conf/extra/roundcube.conf`).

### Error creating tasks / Tasks are not syncronized with Roundcube

The default configuration for the tasklist plugin is to use the database backend to store the tasks. This is usually changed by the arch-setup-kolab script. To do it manually, copy `/usr/share/webapps/roundcubemail/plugins/tasklist/config.inc.php.dist` to `/etc/webapps/roundcubemail/config/tasklist.inc.php`.

### Web interface is slow when accessing IMAP folders

The default configuration uses TLS for all communications with the IMAP server. This can be slow, specially if you are using a large certificate. You can configure Cyrus IMAP server in order to not require tls for localhost. To do so, edit:

 `/etc/cyrus/cyrus.conf` 

```
SERVICES {
    # add or remove based on preferences
    imap                cmd="imapd" listen="yourdomain:imap" prefork=5
    imaps               cmd="imapd -s" listen="imaps" prefork=1
    imapl               cmd="imapd" listen="localhost:imap" prefork=5
```

Add a new service imapl that listens on localhost. We also need to change the imap service to listen only on the external addresses, as otherwise, it will conflict with the newly created service.

Now, add a line to `imapd.conf` to enable plaintext authentication when connection from localhost (using the imapl service).

 `/etc/cyrus/imapd.conf` 

```
allowplaintext: no
imapl_allowplaintext: yes
```

Restart the cyrus services:

```
# systemctl restart postfix cyrus-master

```

Finally, configure roundcube to disable tls. Set the default host to localhost, without any protocol:

 `/etc/webapps/roundcubemail/config/config.inc.php` 

```
// IMAP Server Settings
$config['default_host'] = 'localhost';
```

Changing folders in roundcube should be much faster now, while forcing TLS for remote connections.

## See also

*   [Official homepage](http://kolab.org)
*   [Kolab manuals](http://docs.kolab.org/index.html)
*   [http://hosted.kolabsys.com/~vanmeeuwen/build/html/howtos/build-kolab-from-source.html](http://hosted.kolabsys.com/~vanmeeuwen/build/html/howtos/build-kolab-from-source.html)
*   [http://mirror.kolabsys.com/pub/releases/](http://mirror.kolabsys.com/pub/releases/)
*   [https://obs.kolabsys.com/project/show?project=Kolab%3A3.1](https://obs.kolabsys.com/project/show?project=Kolab%3A3.1)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Kolab&oldid=414171](https://wiki.archlinux.org/index.php?title=Kolab&oldid=414171)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Internet applications](/index.php/Category:Internet_applications "Category:Internet applications")