Related articles

*   [Courier MTA](/index.php/Courier_MTA "Courier MTA")
*   [OpenDKIM](/index.php/OpenDKIM "OpenDKIM")
*   [Postfix](/index.php/Postfix "Postfix")
*   [SOGo](/index.php/SOGo "SOGo")

This article describes how to set up a complete virtual user mail system on an Arch Linux system in the simplest manner possible. However, since a mail system consists of many complex components, quite a bit of configuration will still be necessary.

Roughly, the components used in this article are Postfix as the mail server, Dovecot as the IMAP server, Roundcube as the webmail interface and PostfixAdmin as the administration interface to manage it all.

In the end, the provided solution will allow you to use the best currently available security mechanisms, you will be able to send mails using SMTP and SMTPS and receive mails using POP3, POP3S, IMAP and IMAPS. Additionally, configuration will be easy thanks to PostfixAdmin and users will be able to login using Roundcube. What a deal!

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 User](#User)
    *   [2.2 Database](#Database)
        *   [2.2.1 PostfixAdmin](#PostfixAdmin)
    *   [2.3 SSL certificate](#SSL_certificate)
    *   [2.4 Postfix](#Postfix)
        *   [2.4.1 Setting up Postfix](#Setting_up_Postfix)
        *   [2.4.2 Create the file structure](#Create_the_file_structure)
    *   [2.5 Dovecot](#Dovecot)
    *   [2.6 PostfixAdmin](#PostfixAdmin_2)
    *   [2.7 Roundcube](#Roundcube)
        *   [2.7.1 Apache configuration](#Apache_configuration)
        *   [2.7.2 Roundcube: Change Password Plugin](#Roundcube:_Change_Password_Plugin)
*   [3 Fire it up](#Fire_it_up)
*   [4 Testing](#Testing)
    *   [4.1 Error response](#Error_response)
    *   [4.2 See that you have received a email](#See_that_you_have_received_a_email)
*   [5 Optional Items](#Optional_Items)
    *   [5.1 Quota](#Quota)
*   [6 Sidenotes](#Sidenotes)
    *   [6.1 Alternative vmail folder structure](#Alternative_vmail_folder_structure)
*   [7 Troubleshooting](#Troubleshooting)
    *   [7.1 IMAP/POP3 client failing to receive mails](#IMAP.2FPOP3_client_failing_to_receive_mails)
    *   [7.2 Roundcube not able to delete emails or view any 'standard' folders](#Roundcube_not_able_to_delete_emails_or_view_any_.27standard.27_folders)

## Installation

Before you start, you must have both a working MySQL server as described in [MySQL](/index.php/MySQL "MySQL") and a working Postfix server as described in [Postfix](/index.php/Postfix "Postfix").

[Install](/index.php/Install "Install") the [dovecot](https://www.archlinux.org/packages/?name=dovecot) and [roundcubemail](https://www.archlinux.org/packages/?name=roundcubemail) packages.

## Configuration

### User

For security reasons, a new user should be created to store the mails:

```
# groupadd -g 5000 vmail
# useradd -u 5000 -g vmail -s /usr/bin/nologin -d /home/vmail -m vmail

```

A gid and uid of 5000 is used in both cases so that we do not run into conflicts with regular users. All your mail will then be stored in `/home/vmail`. You could change the home directory to something like `/var/mail/vmail` but be careful to change this in any configuration below as well.

### Database

You will need to create an empty database and corresponding user. In this article, the user *postfix_user* will have read/write access to the database *postfix_db* using *hunter2* as password. You are expected to create the database and user yourself, and give the user permission to use the database, as shown in the following code.

 `$ mysql -u root -p` 
```
CREATE DATABASE postfix_db;
GRANT ALL ON postfix_db.* TO 'postfix_user'@'localhost' IDENTIFIED BY 'hunter2';
FLUSH PRIVILEGES;

```

Now you can go to the PostfixAdmin's setup page, let PostfixAdmin create the needed tables and create the users in there.

#### PostfixAdmin

See [Postfix#PostfixAdmin](/index.php/Postfix#PostfixAdmin "Postfix").

### SSL certificate

You will need a SSL certificate for all encrypted mail communications (SMTPS/IMAPS/POP3S). If you do not have one, create one:

```
# cd /etc/ssl/private/
# openssl req -new -x509 -nodes -newkey rsa:4096 -keyout vmail.key -out vmail.crt -days 1460 #days are optional
# chmod 400 vmail.key
# chmod 444 vmail.crt

```

Alternatively, create a free trusted certificate using [Let's Encrypt](/index.php/Let%27s_Encrypt "Let's Encrypt"). The private key will be in `/etc/letsencrypt/live/*yourdomain*/privkey.pem`, the certificate in `/etc/letsencrypt/live/*yourdomain*/fullchain.pem`. Either change the configuration accordingly, or symlink the keys to `/etc/ssl/private`:

```
# ln -s /etc/letsencrypt/live/*yourdomain*/privkey.pem /etc/ssl/private/vmail.key
# ln -s /etc/letsencrypt/live/*yourdomain*/fullchain.pem /etc/ssl/private/vmail.crt

```

### Postfix

Before you copy & paste the configuration below, check if `relay_domains` has already been already set. If you leave more than one active, you will receive warnings during runtime.

**Warning:** `relay_domains` can be dangerous. You usually do not want Postfix to forward mail of strangers. `$mydestination` is a sane default value. Double check its value before running postfix! See [http://www.postfix.org/BASIC_CONFIGURATION_README.html#relay_to](http://www.postfix.org/BASIC_CONFIGURATION_README.html#relay_to)

Also follow [Postfix#Secure SMTP (receiving)](/index.php/Postfix#Secure_SMTP_.28receiving.29 "Postfix") pointing to the files you created in [#SSL certificate](#SSL_certificate).

#### Setting up Postfix

To `/etc/postfix/main.cf` append:

```
relay_domains = $mydestination
virtual_alias_maps = proxy:mysql:/etc/postfix/virtual_alias_maps.cf
virtual_mailbox_domains = proxy:mysql:/etc/postfix/virtual_mailbox_domains.cf
virtual_mailbox_maps = proxy:mysql:/etc/postfix/virtual_mailbox_maps.cf
virtual_mailbox_base = /home/vmail
virtual_mailbox_limit = 512000000
virtual_minimum_uid = 5000
virtual_transport = virtual
virtual_uid_maps = static:5000
virtual_gid_maps = static:5000
local_transport = virtual
local_recipient_maps = $virtual_mailbox_maps
transport_maps = hash:/etc/postfix/transport

smtpd_sasl_auth_enable = yes
smtpd_sasl_type = dovecot
smtpd_sasl_path = /var/run/dovecot/auth-client
smtpd_recipient_restrictions = permit_mynetworks, permit_sasl_authenticated, reject_unauth_destination
smtpd_relay_restrictions = permit_mynetworks, permit_sasl_authenticated, reject_unauth_destination
smtpd_sasl_security_options = noanonymous
smtpd_sasl_tls_security_options = $smtpd_sasl_security_options
smtpd_tls_security_level = may
smtpd_tls_auth_only = yes
smtpd_tls_received_header = yes
smtpd_tls_cert_file = /etc/ssl/private/vmail.crt
smtpd_tls_key_file = /etc/ssl/private/vmail.key
smtpd_sasl_local_domain = $mydomain
broken_sasl_auth_clients = yes
smtpd_tls_loglevel = 1
smtp_tls_security_level = may
smtp_tls_loglevel = 1

```

*   In the configuration above `virtual_mailbox_domains` is a list of the domains that you want to receive mail for. This CANNOT contain the domain that is set in `mydestination`. That is why we left `mydestination` to be localhost only.

*   `virtual_mailbox_maps` will contain the information of virtual users and their mailbox locations. We are using a hash file to store the more permanent maps, and these will then override the forwards in the MySQL database.

*   `virtual_mailbox_base` is the base directory where the virtual mailboxes will be stored.

The `virtual_uid_maps` and `virtual_gid_maps` are the real system user IDs that the virtual mails will be owned by. This is for storage purposes.

**Note:** Since we will be using a web interface (Roundcube), and do not want people accessing this by any other means, we will be creating this account later without providing any login access.

#### Create the file structure

Those new additional settings reference a lot of files that do not even exist yet. We will create them with the following steps.

If you were setting up your database with PostfixAdmin and created the database schema through PostfixAdmin, you can create the following files. Do not forget to change the password:

 `/etc/postfix/virtual_alias_maps.cf` 
```
user = postfix_user
password = hunter2
hosts = localhost
dbname = postfix_db
table = alias
select_field = goto
where_field = address

```
 `/etc/postfix/virtual_mailbox_domains.cf` 
```
user = postfix_user
password = hunter2
hosts = localhost
dbname = postfix_db
table = domain
select_field = domain
where_field = domain

```
 `/etc/postfix/virtual_mailbox_maps.cf` 
```
user = postfix_user
password = hunter2
hosts = localhost
dbname = postfix_db
table = mailbox
select_field = maildir
where_field = username

```

For alias domains functionality adjust the following files:

 `/etc/postfix/main.cf` 
```
virtual_alias_maps = proxy:mysql:/etc/postfix/virtual_alias_maps.cf,proxy:mysql:/etc/postfix/virtual_alias_domains_maps.cf
virtual_alias_domains = proxy:mysql:/etc/postfix/virtual_alias_domains.cf

```
 `/etc/postfix/virtual_alias_domains_maps.cf` 
```
user = postfix_user
password = hunter2
hosts = localhost
dbname = postfix_db
query = SELECT goto FROM alias,alias_domain WHERE alias_domain.alias_domain = '%d' and alias.address = CONCAT('%u', '@', alias_domain.target_domain) AND alias.active = 1 AND alias_domain.active='1'

```
 `/etc/postfix/virtual_alias_domains.cf` 
```
user = postfix_user
password = hunter2
hosts = localhost
dbname = postfix_db
query = SELECT alias_domain FROM alias_domain WHERE alias_domain='%s' AND active = '1'

```

**Note:** For setups without using PostfixAdmin, create the following files.
 `/etc/postfix/virtual_alias_maps.cf` 
```
user = postfix_user
password = hunter2
hosts = localhost
dbname = postfix_db
table = domains
select_field = virtual
where_field = domain

```
 `/etc/postfix/virtual_mailbox_domains.cf` 
```
user = postfix_user
password = hunter2
hosts = localhost
dbname = postfix_db
table = forwardings
select_field = destination
where_field = source

```
 `/etc/postfix/virtual_mailbox_maps.cf` 
```
user = postfix_user
password = hunter2
hosts = localhost
dbname = postfix_db
table = users
select_field = concat(domain,'/',email,'/')
where_field = email

```

Run *postmap* on *transport* to generate its db:

```
# postmap /etc/postfix/transport

```

### Dovecot

Instead of using the provided Dovecot example config file, we'll create our own `/etc/dovecot/dovecot.conf`. Please note that the user and group here might be vmail **instead of postfix**!

 `/etc/dovecot/dovecot.conf` 
```
protocols = imap pop3
auth_mechanisms = plain
passdb {
    driver = sql
    args = /etc/dovecot/dovecot-sql.conf
}
userdb {
    driver = sql
    args = /etc/dovecot/dovecot-sql.conf
}

service auth {
    unix_listener auth-client {
        group = postfix
        mode = 0660
        user = postfix
    }
    user = root
}

mail_home = /home/vmail/%d/%n
mail_location = maildir:~

ssl_cert = </etc/ssl/private/vmail.crt
ssl_key = </etc/ssl/private/vmail.key

```

**Note:** If you instead want to modify `dovecot.conf.sample`, beware that the default configuration file imports the content of `conf.d/*.conf`. Those files call other files that aren't present in our configuration.

Now we create `/etc/dovecot/dovecot-sql.conf`, which we just referenced in the config above. Use the following contents and check if everything is set accordingly to your system's configuration.

If you used PostfixAdmin, then you add the following:

 `/etc/dovecot/dovecot-sql.conf` 
```
driver = mysql
connect = host=localhost dbname=postfix_db user=postfix_user password=hunter2
# It is highly recommended to not use deprecated MD5-CRYPT. Read more at http://wiki2.dovecot.org/Authentication/PasswordSchemes
default_pass_scheme = SHA512-CRYPT
# Get the mailbox
user_query = SELECT '/home/vmail/%d/%n' as home, 'maildir:/home/vmail/%d/%n' as mail, 5000 AS uid, 5000 AS gid, concat('dirsize:storage=',  quota) AS quota FROM mailbox WHERE username = '%u' AND active = '1'
# Get the password
password_query = SELECT username as user, password, '/home/vmail/%d/%n' as userdb_home, 'maildir:/home/vmail/%d/%n' as userdb_mail, 5000 as  userdb_uid, 5000 as userdb_gid FROM mailbox WHERE username = '%u' AND active = '1'
# If using client certificates for authentication, comment the above and uncomment the following
#password_query = SELECT null AS password, ‘%u’ AS user

```

Without having used PostfixAdmin you can use:

 `/etc/dovecot/dovecot-sql.conf` 
```
driver = mysql
connect = host=localhost dbname=postfix_db user=postfix_user password=hunter2
# It is highly recommended to not use deprecated MD5-CRYPT. Read more at http://wiki2.dovecot.org/Authentication/PasswordSchemes
default_pass_scheme = SHA512-CRYPT
# Get the mailbox
user_query = SELECT '/home/vmail/%d/%n' as home, 'maildir:/home/vmail/%d/%n' as mail, 5000 AS uid, 5000 AS gid, concat('dirsize:storage=',  quota) AS quota FROM users WHERE email = '%u'
# Get the password
password_query = SELECT email as user, password, '/home/vmail/%d/%n' as userdb_home, 'maildir:/home/vmail/%d/%n' as userdb_mail, 5000 as  userdb_uid, 5000 as userdb_gid FROM users WHERE email = '%u'
# If using client certificates for authentication, comment the above and uncomment the following
#password_query = SELECT null AS password, ‘%u’ AS user

```

**Tip:** Visit [http://wiki2.dovecot.org/Variables](http://wiki2.dovecot.org/Variables) to learn more about Dovecot variables.

### PostfixAdmin

See [Postfix#PostfixAdmin](/index.php/Postfix#PostfixAdmin "Postfix").

Note: To match the configuration in this file, config.inc.php should contain the following.

```
   # /etc/postfixadmin/config.inc.php
   ...
   $CONF['domain_path'] = 'YES';
   $CONF['domain_in_mailbox'] = 'NO';
   ...

```

### Roundcube

Make sure that both `extension=pdo_mysql` and`
**Template error:** are you trying to use the = sign? Visit [Help:Template#Escape template-breaking characters](/index.php/Help:Template#Escape_template-breaking_characters "Help:Template") for workarounds.
`are uncommented in your `php.ini` file. Also check the `.htaccess` for access restrictions. Assuming that localhost is your current host, navigate a browser to `[http://localhost/roundcube/installer/](http://localhost/roundcube/installer/)` and follow the instructions.

Roundcube needs a separate database to work. You should not use the same database for Roundcube and PostfixAdmin. Create a second database `roundcube_db` and a new user named `roundcube_user`.

While running the installer ...

*   For the address of the IMAP host, use `ssl://localhost/` or `tls://localhost/` and not just `localhost`.
*   Use port `993`. Likewise with SMTP.
*   For the address of the SMTP host, use `tls://localhost/` and port `587` if you used the proper TLS mode.

	(use `ssl://localhost/` with port `465` if you used the wrapper mode)

*   See [#Postfix](#Postfix) for an explanation on that.

The post install process is similar to any other webapp like [PhpMyAdmin](/index.php/PhpMyAdmin "PhpMyAdmin") or PostFixAdmin. The configuration file is in `/etc/webapps/roundcubemail/config/config.inc.php` which works as an override over `default.inc.php`.

#### Apache configuration

If you are using Apache, copy the example configuration file to your webserver configuration directory.

```
# cp /etc/webapps/roundcubemail/apache.conf /etc/httpd/conf/extra/httpd-roundcubemail.conf

```

Add the following line in

 `/etc/httpd/conf/httpd.conf` 
```
Include conf/extra/httpd-roundcubemail.conf

```

#### Roundcube: Change Password Plugin

To let users change their passwords from within Roundcube, do the following:

Enable the password plugin by adding this line to

 `/etc/webapps/roundcubemail/config/config.inc.php` 
```
$config['plugins'] = array('password');

```

Configure the password plugin and make sure you alter the settings accordingly:

 `/usr/share/webapps/roundcubemail/plugins/password/config.inc.php` 
```
$config['password_driver'] = 'sql';
$config['password_db_dsn'] = 'mysql://<postfix_database_user>:<password>@localhost/<postfix_database_name>';
// for dovecot salted passwords only
// $config['password_dovecotpw'] = 'doveadm pw';
// $config['password_dovecotpw_method'] = 'SHA512-CRYPT';
// $config['password_dovecotpw_with_method'] = true;
$config['password_query'] = 'UPDATE mailbox SET password=%c WHERE username=%u';

```

## Fire it up

All necessary daemons should be started in order to test the configuration. [Start](/index.php/Start "Start") both `postfix` and `dovecot`.

Now for testing purposes, create a domain and mail account in PostfixAdmin. Try to login to this account using Roundcube. Now send yourself a mail.

## Testing

Now lets see if Postfix is going to deliver mail for our test user.

```
nc servername 25
helo testmail.org
mail from:<test@testmail.org>
rcpt to:<cactus@virtualdomain.tld>
data
This is a test email.
.
quit

```

### Error response

```
451 4.3.0 <lisi@test.com>:Temporary lookup failure

```

Maybe you have entered the wrong user/password for MySQL or the MySQL socket is not in the right place.

This error will also occur if you neglect to run newaliases at least once before starting postfix. MySQL is not required for local only usage of postfix.

```
550 5.1.1 <email@spam.me>: Recipient address rejected: User unknown in virtual mailbox table.

```

Double check content of mysql_virtual_mailboxes.cf and check the main.cf for mydestination

### See that you have received a email

Now type `$ find /home/vmailer`.

You should see something like the following:

```
/home/vmailer/virtualdomain.tld/cactus@virtualdomain.tld
/home/vmailer/virtualdomain.tld/cactus@virtualdomain.tld/tmp
/home/vmailer/virtualdomain.tld/cactus@virtualdomain.tld/cur
/home/vmailer/virtualdomain.tld/cactus@virtualdomain.tld/new
/home/vmailer/virtualdomain.tld/cactus@virtualdomain.tld/new/1102974226.2704_0.bonk.testmail.org

```

The key is the last entry. This is an actual email, if you see that, it is working.

## Optional Items

Although these items are not required, they definitely add more completeness to your setup

### Quota

To enable mailbox quota support by dovecot, do the following:

*   First add the following lines to /etc/dovecot/dovecot.conf

```
dict {
	quotadict = mysql:/etc/dovecot/dovecot-dict-sql.conf.ext
}
service dict {
	unix_listener dict {
		group = vmail
		mode = 0660
		user = vmail
	}
	user = root
}
service quota-warning {
	executable = script /usr/local/bin/quota-warning.sh
	user = vmail
	unix_listener quota-warning {
		group = vmail
		mode = 0660
		user = vmail
	}
}	
mail_plugins=quota
protocol pop3 {
	 mail_plugins = quota
	 pop3_client_workarounds = outlook-no-nuls oe-ns-eoh
	 pop3_uidl_format = %08Xu%08Xv
}
protocol lda {
	mail_plugins = quota
	postmaster_address = postmaster@yourdomain.com
}
protocol imap {
	mail_plugins = $mail_plugins imap_quota
	mail_plugin_dir = /usr/lib/dovecot/modules
}
plugin {
       quota = dict:User quota::proxy::quotadict
       quota_rule2 = Trash:storage=+10%%
       quota_warning = storage=100%% quota-warning +100 %u
       quota_warning2 = storage=95%% quota-warning +95 %u
       quota_warning3 = storage=80%% quota-warning +80 %u
       quota_warning4 = -storage=100%% quota-warning -100 %u # user is no longer over quota
}

```

*   Create a new file /etc/dovecot/dovecot-dict-sql.conf.ext with the following code:

```
connect = host=localhost dbname=yourdb user=youruser password=yourpassword
map {
	pattern = priv/quota/storage
	table = quota2
	username_field = username
	value_field = bytes
}
map {
	pattern = priv/quota/messages
	table = quota2
	username_field = username
	value_field = messages
}

```

*   Create a warning script /usr/local/bin/quota-warning.sh and make sure it is executable. This warning script works with postfix lmtp configuration as well.

```
 #!/bin/sh
 BOUNDARY="$1"
 USER="$2"
 MSG=""
 if [[ "$BOUNDARY" = "+100" ]]; then
    MSG="Your mailbox is now overfull (>100%). In order for your account to continue functioning properly, you need to remove some emails NOW."
 elif [[ "$BOUNDARY" = "+95" ]]; then
    MSG="Your mailbox is now over 95% full. Please remove some emails ASAP."
 elif [[ "$BOUNDARY" = "+80" ]]; then
    MSG="Your mailbox is now over 80% full. Please consider removing some emails to save space."
 elif [[ "$BOUNDARY" = "-100" ]]; then
    MSG="Your mailbox is now back to normal (<100%)."
 fi

 cat << EOF | /usr/lib/dovecot/dovecot-lda -d $USER -o "plugin/quota=maildir:User quota:noenforcing"
 From: postmaster@yourdomain.com
 Subject: Email Account Quota Warning

 Dear User,

 $MSG

 Best regards,
 Your Mail System
 EOF

```

*   Edit the user_query line and add iterat_query in dovecot-sql.conf as following:

```
 user_query = SELECT '/home/vmail/%d/%n' as home, 'maildir:/home/vmail/%d/%n' as mail, 5000 AS uid, 5000 AS gid, concat('*:bytes=', quota) AS quota_rule FROM mailbox WHERE username = '%u' AND active = '1'
 iterate_query = SELECT username AS user FROM mailbox

```

*   Set up LDA as described above under SpamAssassin. If you're not using SpamAssassin, the pipe should look like this in /etc/postfix/master.cf :

```
 dovecot    unix  -       n       n       -       -       pipe
 flags=DRhu user=vmail:vmail argv=/usr/lib/dovecot/deliver -f ${sender} -d ${recipient}

```

As above activate it in Postfix main.cf

```
 virtual_transport = dovecot

```

*   You can set up quota per each mailbox in postfixadmin. Make sure the relevant lines in config.inc.php look like this:

```
$CONF['quota'] = 'YES';
$CONF['quota_multiplier'] = '1024000';

```

Restart postfix and dovecot services. If things go well, you should be able to list all users' quota and usage by the this command:

```
doveadm quota get -A

```

You should be able to see the quota in roundcube too.

## Sidenotes

### Alternative vmail folder structure

Instead of having a directory structure like `/home/vmail/example.com/user@example.com` you can have cleaner subdirectories (without the additional domain name) by replacing `select_field` and `where_field` with:

 `query = SELECT CONCAT(SUBSTRING_INDEX(email,'@',-1),'/',SUBSTRING_INDEX(email,'@',1),'/') FROM users WHERE email='%s'` 

## Troubleshooting

### IMAP/POP3 client failing to receive mails

If you get similar errors, take a look into `/var/log/mail.log` or use `journalctl -xn --unit postfix.service` to find out more.

It may turn out that the Maildir `/home/vmail/mail@domain.tld` is just being created if there is at least one email waiting. Otherwise there wouldn't be any need for the directory creation before.

### Roundcube not able to delete emails or view any 'standard' folders

Ensure that the Roundcube config.inc.php file contains the following:

```
$rcmail_config['default_imap_folders'] = array('INBOX', 'Drafts', 'Sent', 'Junk', 'Trash');
$rcmail_config['create_default_folders'] = true;
$rcmail_config['protect_default_folders'] = true;
```