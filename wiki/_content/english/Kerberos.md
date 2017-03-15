[Kerberos](https://en.wikipedia.org/wiki/Kerberos_(protocol) is a network authentication system.

[krb5 documentation](https://web.mit.edu/kerberos/krb5-1.12/doc/admin/index.html)

## Server

Install the [krb5](https://www.archlinux.org/packages/?name=krb5) package, if it isn't already installed, and configure it to your needs. Ex:

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

Add DNS records:

 `db.example.com` 
```
kerberos           A   1.2.3.4
_kerberos          TXT "EXAMPLE.COM"
_kerberos._udp     SRV 0 0  88 kerberos.example.com.
_kerberos-adm._udp SRV 0 0 750 kerberos.example.com.

```

Don't forget reverse DNS!

Add ALLOW rules to your firewall for both tcp and udp on ports 88 and 750 (krb5 documentation says tcp is used on both, though mine isn't listening for tcp on 750)

Create the database:

 `# krb5_util -r EXAMPLE.COM create -s` 

Enable and start the krb5-kdc service.

Start kadmin, using the local root user instead of kerberos authentication:

 `# kadmin.local` 
```
Authenticating as principal root/admin@EXAMPLE.COM with password.
kadmin.local:
```

You can do most things

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

## SSH Authentication

Make sure both your ssh server and ssh client configurations include this line, then restart the server

 `GSSAPIAuthentication yes` 

Generate a service principal

 `kadmin.local:  add_principal -randkey host/someserver.example.com@EXAMPLE.COM` 

Generate the keytab for the server

 `kadmin.local:  ktadd -keytab /root/someserver.krb5.keytab` 
```
# scp kerberos.example.com:/root/someserver.krb5.keytab /etc/krb5.keytab
# chmod 600 /etc/krb5.keytab
```

Get a ticket-granting ticket on the ssh client

 `$ kinit myuser@EXAMPLE.COM`  `Password for myuser@EXAMPLE.COM: ***` 

Debug with

 `$ ssh someserver.example.com -v`