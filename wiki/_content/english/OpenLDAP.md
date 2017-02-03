OpenLDAP is an open-source implementation of the LDAP protocol. An LDAP server basically is a non-relational database which is optimised for accessing, but not writing, data. It is mainly used as an address book (for e.g. email clients) or authentication backend to various services (such as Samba, where it is used to emulate a domain controller, or [Linux system authentication](/index.php/LDAP_authentication "LDAP authentication"), where it replaces `/etc/passwd`) and basically holds the user data.

**Note:** Commands related to OpenLDAP that begin with `ldap` (like `ldapsearch`) are client-side utilities, while commands that begin with `slap` (like `slapcat`) are server-side.

This page is a starting point for a basic OpenLDAP installation and a sanity check.

**Tip:** Directory services are an enormous topic. Configuration can therefore be complex. If you are totally new to those concepts, [this](http://www.brennan.id.au/20-Shared_Address_Book_LDAP.html) is an good introduction that is easy to understand and that will get you started, even if you are new to everything LDAP.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 The server](#The_server)
    *   [2.2 The client](#The_client)
    *   [2.3 Create initial entry](#Create_initial_entry)
    *   [2.4 Test your new OpenLDAP installation](#Test_your_new_OpenLDAP_installation)
    *   [2.5 OpenLDAP over TLS](#OpenLDAP_over_TLS)
        *   [2.5.1 Create a self-signed certificate](#Create_a_self-signed_certificate)
        *   [2.5.2 Configure slapd for SSL](#Configure_slapd_for_SSL)
        *   [2.5.3 Start slapd with SSL](#Start_slapd_with_SSL)
*   [3 Next steps](#Next_steps)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Client authentication checking](#Client_authentication_checking)
    *   [4.2 LDAP server stops suddenly](#LDAP_server_stops_suddenly)
    *   [4.3 LDAP server does not start](#LDAP_server_does_not_start)
*   [5 See also](#See_also)

## Installation

OpenLDAP contains both a LDAP server and client. [Install](/index.php/Install "Install") it with the package [openldap](https://www.archlinux.org/packages/?name=openldap).

## Configuration

### The server

**Note:** If you already have an OpenLDAP database on your machine, remove it by deleting everything inside `/var/lib/openldap/openldap-data/`.

The server configuration file is located at `/etc/openldap/slapd.conf`.

Edit the suffix and rootdn. The suffix typically is your domain name but it does not have to be. It depends on how you use your directory. We will use *example* for the domain name, and *com* for the tld. The rootdn is your LDAP administrator's name (we will use *root* here).

```
suffix     "dc=example,dc=com"
rootdn     "cn=root,dc=example,dc=com"

```

Now we delete the default root password and create a strong one:

```
# sed -i "/rootpw/ d" /etc/openldap/slapd.conf #find the line with rootpw and delete it
# echo "rootpw    $(slappasswd)" >> /etc/openldap/slapd.conf  #add a line which includes the hashed password output from slappasswd

```

You will likely want to add some typically used [schemas](http://www.openldap.org/doc/admin24/schema.html) to the top of `slapd.conf`:

**Note:** currently missing: cp /usr/share/doc/samba/examples/LDAP/samba.schema /etc/openldap/schema

```
include         /etc/openldap/schema/cosine.schema
include         /etc/openldap/schema/inetorgperson.schema
include         /etc/openldap/schema/nis.schema
#include         /etc/openldap/schema/samba.schema

```

You will likely want to add some typically used [indexes](http://www.openldap.org/doc/admin24/tuning.html#Indexes) to the bottom of `slapd.conf`:

```
index   uid             pres,eq
index   mail            pres,sub,eq
index   cn              pres,sub,eq
index   sn              pres,sub,eq
index   dc              eq

```

If you plan to use your LDAP server for authentication, you might want to check access control configuration in [LDAP authentication#LDAP Server Setup](/index.php/LDAP_authentication#LDAP_Server_Setup "LDAP authentication").

Now prepare the database directory. You will need to rename the default config:

```
# cp /var/lib/openldap/openldap-data/DB_CONFIG.example /var/lib/openldap/openldap-data/DB_CONFIG

```

**Note:** With OpenLDAP 2.4 the configuration of `slapd.conf` is deprecated. From this version on all configuration settings are stored in `/etc/openldap/slapd.d/`.

To store the recent changes in `slapd.conf` to the new `/etc/openldap/slapd.d/` configuration settings, we have to delete the old configuration files first, do this every time you change the configuration:

```
# rm -rf /etc/openldap/slapd.d/*

```

(if you do not have a database yet, you might need to create one by starting and stopping the `slapd.service` [using systemd](/index.php/Systemd#Using_units "Systemd") )

Then we generate the new configuration with:

```
# slaptest -f /etc/openldap/slapd.conf -F /etc/openldap/slapd.d/

```

The above command has to be run every time you change `slapd.conf`. Check if everything succeeded. Ignore message "bdb_monitor_db_open: monitoring disabled; configure monitor database to enable".

Change ownership recursively on the new files and directory in /etc/openldap/slapd.d:

```
# chown -R ldap:ldap /etc/openldap/slapd.d

```

**Note:** Index the directory after you populate it. You should stop slapd before doing this.
```
# slapindex
# chown ldap:ldap /var/lib/openldap/openldap-data/*

```

or just

```
$ sudo -u ldap slapindex

```

Finally, start the slapd daemon with `slapd.service` using systemd.

### The client

The client config file is located at `/etc/openldap/ldap.conf`.

It is quite simple: you will only have to alter `BASE` to reflect the suffix of the server, and `URI` to reflect the address of the server, like:

 `/etc/openldap/ldap.conf` 
```
BASE            dc=example,dc=com
URI             ldap://localhost
```

If you decide to use SSL:

*   The protocol (ldap or ldaps) in the `URI` entry has to conform with the slapd configuration
*   If you decide to use self-signed certificates, add a `TLS_REQCERT allow` line to `ldap.conf`
*   If you use a signed certificate from a CA, add the line `TLS_CACERTDIR /usr/share/ca-certificates/trust-source` in `ldap.conf`.

### Create initial entry

Once your client is configured, you probably want to create the root entry, and an entry for the root role:

```
$ ldapadd -x -D 'cn=root,dc=example,dc=com' -W
dn: dc=example,dc=com
objectClass: dcObject
objectClass: organization
dc: example
o: Example
description: Example directory

dn: cn=root,dc=example,dc=com
objectClass: organizationalRole
cn: root
description: Directory Manager
^D

```

The text after the first line is entered on stdin, or could be read from a file either with the -f option or a file redirect.

### Test your new OpenLDAP installation

This is easy, just run the command below:

```
$ ldapsearch -x '(objectclass=*)'

```

Or authenticating as the rootdn (replacing `-x` by `-D <user> -W`), using the example configuration we had above:

```
$ ldapsearch -D "cn=root,dc=example,dc=com" -W '(objectclass=*)'

```

Now you should see some information about your database.

### OpenLDAP over TLS

**Note:** [upstream documentation](http://www.openldap.org/doc/admin24/) is much more useful/complete than this section

If you access the OpenLDAP server over the network and especially if you have sensitive data stored on the server you run the risk of someone sniffing your data which is sent clear-text. The next part will guide you on how to setup an SSL connection between the LDAP server and the client so the data will be sent encrypted.

In order to use TLS, you must have a certificate. For testing purposes, a *self-signed* certificate will suffice. To learn more about certificates, see [OpenSSL](/index.php/OpenSSL "OpenSSL").

**Warning:** OpenLDAP cannot use a certificate that has a password associated to it.

#### Create a self-signed certificate

To create a *self-signed* certificate, type the following:

```
$ openssl req -new -x509 -nodes -out slapdcert.pem -keyout slapdkey.pem -days 365

```

You will be prompted for information about your LDAP server. Much of the information can be left blank. The most important information is the common name. This must be set to the DNS name of your LDAP server. If your LDAP server's IP address resolves to example.org but its server certificate shows a CN of bad.example.org, LDAP clients will reject the certificate and will be unable to negotiate TLS connections (apparently the results are wholly unpredictable).

Now that the certificate files have been created copy them to `/etc/openldap/ssl/` (create this directory if it does not exist) and secure them. `slapdcert.pem` must be world readable because it contains the public key. `slapdkey.pem` on the other hand should only be readable for the ldap user for security reasons:

```
# mv slapdcert.pem slapdkey.pem /etc/openldap/ssl/
# chmod -R 755 /etc/openldap/ssl/
# chmod 400 /etc/openldap/ssl/slapdkey.pem
# chmod 444 /etc/openldap/ssl/slapdcert.pem
# chown ldap /etc/openldap/ssl/slapdkey.pem

```

#### Configure slapd for SSL

Edit the daemon configuration file (`/etc/openldap/slapd.conf`) to tell LDAP where the certificate files reside by adding the following lines:

```
# Certificate/SSL Section
TLSCipherSuite DEFAULT
TLSCertificateFile /etc/openldap/ssl/slapdcert.pem
TLSCertificateKeyFile /etc/openldap/ssl/slapdkey.pem

```

If you are using a signed SSL Certificate from a certification authority such as [Let’s Encrypt](/index.php/Let%E2%80%99s_Encrypt "Let’s Encrypt"), you will also need to specify the path to the root certificates database and your intermediary certificate. You will also need to change ownership of the `.pem` files and intermediary directories to make them readable to the user `ldap`:

```
# Certificate/SSL Section
TLSCipherSuite DEFAULT
TLSCertificateFile /etc/letsencrypt/live/ldap.my-domain.com/cert.pem
TLSCertificateKeyFile /etc/letsencrypt/live/ldap.my-domain.com/privkey.pem
TLSCACertificateFile /etc/letsencrypt/live/ldap.my-domain.com/chain.pem
TLSCACertificatePath /usr/share/ca-certificates/trust-source

```

The TLSCipherSuite specifies a list of OpenSSL ciphers from which slapd will choose when negotiating TLS connections, in decreasing order of preference. In addition to those specific ciphers, you can use any of the wildcards supported by OpenSSL. **NOTE:** DEFAULT is a wildcard. See `man ciphers` for description of ciphers, wildcards and options supported.

**Note:** To see which ciphers are supported by your local OpenSSL installation, type the following: `openssl ciphers -v ALL:COMPLEMENTOFALL`. Always test which ciphers will actually be enabled by TLSCipherSuite by providing it to OpenSSL command, like this: `openssl ciphers -v 'DEFAULT'`

Regenerate the configuration directory:

```
# rm -rf /etc/openldap/slapd.d/*                                  # erase old config settings
# slaptest -f /etc/openldap/slapd.conf -F /etc/openldap/slapd.d/  # generate new config directory from config file
# chown -R ldap:ldap /etc/openldap/slapd.d                        # Change ownership recursively to ldap on the config directory

```

#### Start slapd with SSL

You will have to edit `slapd.service` to change to protocol slapd listens on.

Create the override unit:

 `systemctl edit slapd.service` 
```
[Service]
ExecStart=
ExecStart=/usr/bin/slapd -u ldap -g ldap -h "ldaps:///"
```

Localhost connections do not need to use SSL. So, if you want to access the server locally you should change the `ExecStart` line to:

```
ExecStart=/usr/bin/slapd -u ldap -g ldap -h "ldap://127.0.0.1 ldaps:///"

```

Then [restart](/index.php/Restart "Restart") `slapd.service`. If it was enabled before, reenable it now.

**Note:** If you created a self-signed certificate above, be sure to add `TLS_REQCERT allow` to `/etc/openldap/ldap.conf` on the client, or it will not be able connect to the server.

## Next steps

You now have a basic LDAP installation. The next step is to design your directory. The design is heavily dependent on what you are using it for. If you are new to LDAP, consider starting with a directory design recommended by the specific client services that will use the directory ([PAM](/index.php/PAM "PAM"), [Postfix](/index.php/Postfix "Postfix"), etc).

A directory for system authentication is the [LDAP authentication](/index.php/LDAP_authentication "LDAP authentication") article.

A nice web frontend is [phpLDAPadmin](/index.php/PhpLDAPadmin "PhpLDAPadmin").

## Troubleshooting

### Client authentication checking

If you cannot connect to your server for non-secure authentication

```
$ ldapsearch -x -H ldap://ldaservername:389 -D cn=Manager,dc=example,dc=exampledomain

```

and for TLS secured authentication with:

```
$ ldapsearch -x -H ldaps://ldaservername:636 -D cn=Manager,dc=example,dc=exampledomain

```

### LDAP server stops suddenly

If you notice that slapd seems to start but then stops, try running:

```
# chown ldap:ldap /var/lib/openldap/openldap-data/*

```

to allow slapd write access to its data directory as the user "ldap".

### LDAP server does not start

Try starting the server from the command line with debugging output enabled:

```
# slapd -u ldap -g ldap -h ldaps://ldaservername:636 -d Config,Stats

```

## See also

*   [Official OpenLDAP Software 2.4 Administrator's Guide](http://www.openldap.org/doc/admin24/)
*   [phpLDAPadmin](/index.php/PhpLDAPadmin "PhpLDAPadmin") is a web interface tool in the style of phpMyAdmin.
*   [LDAP authentication](/index.php/LDAP_authentication "LDAP authentication")
*   [apachedirectorystudio](https://aur.archlinux.org/packages/apachedirectorystudio/) from the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") is an Eclipse-based LDAP viewer. Works perfect with OpenLDAP installations.