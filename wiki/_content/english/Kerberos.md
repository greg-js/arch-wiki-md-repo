[Kerberos](https://en.wikipedia.org/wiki/Kerberos_(protocol) is a network authentication system. See [krb5 documentation](https://web.mit.edu/kerberos/krb5-1.12/doc/admin/index.html).

## Contents

*   [1 Server](#Server)
    *   [1.1 Basic Commands](#Basic_Commands)
    *   [1.2 Configuring kadmin ACL](#Configuring_kadmin_ACL)
*   [2 SSH Authentication](#SSH_Authentication)

## Server

Install the [krb5](https://www.archlinux.org/packages/?name=krb5) package, if it is not already installed, and configure it to your needs. For example:

 `/etc/krb5.conf` 
```
[libdefaults]
    default_realm = EXAMPLE.COM
    permitted_enctypes = aes256-cts-hmac-sha1-96 aes128-cts-hmac-sha1-96 camellia256-cts-cmac camellia128-cts-cmac

[realms]
    EXAMPLE.COM = {
        admin_server = kerberos.example.com
        supported_enctypes = aes256-cts-hmac-sha1-96 aes128-cts-hmac-sha1-96 camellia256-cts-cmac camellia128-cts-cmac
    }

[domain_realm]
    example.com = EXAMPLE.COM
    .example.com = EXAMPLE.COM

[logging]
    kdc          = SYSLOG:NOTICE
    admin_server = SYSLOG:NOTICE
    default      = SYSLOG:NOTICE

```

This file's format is described in the MIT Kerberos [documentation](https://web.mit.edu/kerberos/krb5-1.12/doc/admin/conf_files/krb5_conf.html)

Add DNS records:

 `db.example.com` 
```
kerberos           A   1.2.3.4
_kerberos          TXT "EXAMPLE.COM"
_kerberos._udp     SRV 0 0  88 kerberos.example.com.
_kerberos-adm._udp SRV 0 0 750 kerberos.example.com.

```

Do not forget reverse DNS.

Add ALLOW rules to your firewall for both tcp and udp on ports 88 and 750.

Create the database:

```
# kdb5_util -r EXAMPLE.COM create -s

```

Enable and start the krb5-kdc service.

Start kadmin, using the local root user instead of kerberos authentication:

 `# kadmin.local` 
```
Authenticating as principal root/admin@EXAMPLE.COM with password.
kadmin.local:
```

### Basic Commands

Add a human principal (user):

 `kadmin.local:  add_principal myuser@EXAMPLE.COM` 
```
WARNING: no policy specified for myuser@EXAMPLE.COM; defaulting to no policy
Enter password for principal "myuser@EXAMPLE.COM": ***
Re-enter password for principal "myuser@EXAMPLE.COM": ***
Principal "myuser@EXAMPLE.COM" created.

```

Add a service principal:

 `kadmin.local:  add_principal -randkey nfs/someserver.example.com@EXAMPLE.COM` 

### Configuring kadmin ACL

Create a principal for administration:

 `kadmin.local:  add_principal myuser/admin@EXAMPLE.COM` 
```
WARNING: no policy specified for myuser/admin@EXAMPLE.COM; defaulting to no policy
Enter password for principal "myuser/admin@EXAMPLE.COM": ***
Re-enter password for principal "myuser/admin@EXAMPLE.COM": ***
Principal "myuser/admin@EXAMPLE.COM" created.

```

Add the user to the kadmin ACL file:

 `/var/lib/krb5kdc/kadm5.acl`  `myuser/admin@EXAMPLE.COM *` 

This file's format is described in the MIT Kerberos [documentation](https://web.mit.edu/kerberos/krb5-1.12/doc/admin/conf_files/kadm5_acl.html)

Configure kdc.conf:

 `/var/lib/krb5kdc/kdc.conf` 
```
[kdcdefaults]
    kdc_ports = 750,88

[realms]
    EXAMPLE.COM = {
        database_name = /var/lib/krb5kdc/principal
        acl_file = /var/lib/krb5kdc/kadm5.acl
        key_stash_file = /var/lib/krb5kdc/.k5.EXAMPLE.COM
        kdc_ports = 750,88
        max_life = 10h 0m 0s
        max_renewable_life = 7d 0h 0m 0s
    }

```

This file's format is described in the MIT Kerberos [documentation](https://web.mit.edu/kerberos/krb5-1.12/doc/admin/conf_files/kdc_conf.html)

Restart the kdc and kadmin daemons:

 `sudo systemctl restart krb5-kdc krb5-kadmind` 

You can now use kadmin as your own user, authenticating with kerberos:

 `$ kadmin` 
```
Authenticating as principal myuser/admin@EXAMPLE.COM with password.
Password for myuser/admin@EXAMPLE.COM: ***
kadmin:

```

## SSH Authentication

Make sure both your [SSH](/index.php/SSH "SSH") server and client configurations include this line, then restart the server:

 `GSSAPIAuthentication yes` 

Generate a service principal:

 `kadmin.local:  add_principal -randkey host/someserver.example.com@EXAMPLE.COM` 

Generate the keytab for the server:

 `kadmin.local:  ktadd -keytab /root/someserver.krb5.keytab host/someserver.example.com@EXAMPLE.COM` 
```
# scp kerberos.example.com:/root/someserver.krb5.keytab /etc/krb5.keytab
# chmod 600 /etc/krb5.keytab
```

Get a ticket-granting ticket on the ssh client:

 `$ kinit myuser@EXAMPLE.COM`  `Password for myuser@EXAMPLE.COM: ***` 

Debug with:

 `$ ssh someserver.example.com -v`