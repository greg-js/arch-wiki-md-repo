Related articles

*   [Active Directory Integration](/index.php/Active_Directory_Integration "Active Directory Integration")

[Kerberos](https://en.wikipedia.org/wiki/Kerberos_(protocol) is a network authentication system. See [krb5 documentation](https://web.mit.edu/kerberos/krb5-1.12/doc/admin/index.html).

## Contents

*   [1 Installation](#Installation)
*   [2 Server configuration](#Server_configuration)
    *   [2.1 Domain creation](#Domain_creation)
    *   [2.2 Add principals](#Add_principals)
*   [3 Client configuration](#Client_configuration)
    *   [3.1 Join the domain](#Join_the_domain)
    *   [3.2 Create client principals](#Create_client_principals)
*   [4 Advanced configuration](#Advanced_configuration)
    *   [4.1 DNS records](#DNS_records)
    *   [4.2 Firewall](#Firewall)
    *   [4.3 Configuring kadmin ACL](#Configuring_kadmin_ACL)
*   [5 SSH Authentication](#SSH_Authentication)
*   [6 NFS](#NFS)
    *   [6.1 Create service principals](#Create_service_principals)
    *   [6.2 NFS Server](#NFS_Server)
    *   [6.3 NFS Client](#NFS_Client)
*   [7 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [krb5](https://www.archlinux.org/packages/?name=krb5) package on your clients and server.

It is **highly** recommended to use a [time sync daemon](/index.php/Time#Time_synchronization "Time") to keep client/server clocks in sync.

If hostname resolution has not been configured, you can manually add your clients and server to the [hosts(5)](http://man7.org/linux/man-pages/man5/hosts.5.html) file of each machine.

## Server configuration

### Domain creation

Edit `/etc/krb5.conf` to configure your domain:

 `/etc/krb5.conf` 
```
[libdefaults]
    default_realm = EXAMPLE.COM

[realms]
# use "kdc = ..." if real admins haven't put SRV records int DNS
    EXAMPLE.COM = {
        admin_server = kbserver.example.com
        kdc = kbserver.example.com
    }

[domain_realm]
    example.com = EXAMPLE.COM
    .example.com = EXAMPLE.COM

[logging]
    kdc          = CONSOLE
    admin_server = CONSOLE
    default      = CONSOLE

```

This file's format is described in the MIT Kerberos [documentation](https://web.mit.edu/kerberos/krb5-1.12/doc/admin/conf_files/krb5_conf.html)

Create the database:

 `# kdb5_util -r EXAMPLE.COM create -s` 
```
Loading random data                                                             
Initializing database '/var/lib/krb5kdc/principal' for realm 'EXAMPLE.COM',                  
master key name 'K/M@EXAMPLE.COM'
You will be prompted for the database Master Password.                          
It is important that you NOT FORGET this password.                              
Enter KDC database master key: ***
Re-enter KDC database master key to verify: ***

```

Finally, enable and start the Kerberos services:

```
# systemctl enable krb5-kdc krb5-kadmind
# systemctl start krb5-kdc krb5-kadmind

```

### Add principals

Start the Kerberos administration tool:

 `# kadmin.local` 
```
Authenticating as principal root/admin@EXAMPLE.COM with password.
kadmin.local:
```

Add the admin user to the Kerberos database:

 `kadmin.local: addprinc root/admin` 
```
WARNING: no policy specified for root/admin@EXAMPLE.COM; defaulting to no policy
Enter password for principal "root/admin@EXAMPLE.COM": ***
Re-enter password for principal "root/admin@EXAMPLE.COM": ***
Principal "root/admin@EXAMPLE.COM" created.

```

Add a user to the Kerberos database:

 `kadmin.local:  addprinc myuser@EXAMPLE.COM` 
```
WARNING: no policy specified for myuser@EXAMPLE.COM; defaulting to no policy
Enter password for principal "myuser@EXAMPLE.COM": ***
Re-enter password for principal "myuser@EXAMPLE.COM": ***
Principal "myuser@EXAMPLE.COM" created.

```

Add the KDC to the Kerberos database:

 `kadmin.local: addprinc -randkey host/kbserver.example.com` 
```
WARNING: no policy specified for host/kbserver.example.com@EXAMPLE.COM; defaulting to no policy
Principal "host/kbserver.example.com@EXAMPLE.COM" created.

```

Finally, Add the KDC to the Kerberos keytab:

 `kadmin.local:  ktadd host/kbserver.example.com` 
```
Entry for principal host/kbserver.example.com with kvno 2, encryption type aes256-cts-hmac-sha1-96 added to keytab FILE:/etc/krb5.keytab.
Entry for principal host/kbserver.example.com with kvno 2, encryption type aes128-cts-hmac-sha1-96 added to keytab FILE:/etc/krb5.keytab.

```

You should now be able to get a Kerberos ticket:

 `$ kinit` 
```
Password for myuser@EXAMPLE.COM: ***

```
 `$ klist` 
```
Ticket cache: FILE:/tmp/krb5cc_1000
Default principal: myuser@EXAMPLE.COM

Valid starting       Expires              Service principal
08/30/2017 14:26:09  08/31/2017 14:26:09  krbtgt/EXAMPLE.COM@EXAMPLE.COM

```

## Client configuration

### Join the domain

Edit `/etc/krb5.conf` to match your server's configuration. You can simply copy this file from the server.

### Create client principals

Start the Kerberos administration tool on the Kerberos server:

 `# kadmin.local` 
```
Authenticating as principal root/admin@EXAMPLE.COM with password.

```

Add the client to the Kerberos database:

 `kadmin.local: addprinc -randkey host/kbclient.example.com` 
```
WARNING: no policy specified for host/kbclient.example.com@EXAMPLE.COM; defaulting to no policy
Principal "host/kbclient.example.com@EXAMPLE.COM" created.

```

Finally, add the client to the Kerberos keytab:

 `kadmin.local:  ktadd host/kbclient.example.com` 
```
Entry for principal host/kbclient.example.com with kvno 2, encryption type aes256-cts-hmac-sha1-96 added to keytab FILE:/etc/krb5.keytab.
Entry for principal host/kbclient.example.com with kvno 2, encryption type aes128-cts-hmac-sha1-96 added to keytab FILE:/etc/krb5.keytab.

```

Finally, copy `/etc/krb5.keytab` from the server to the client:

```
# scp kbserver.example.com:/etc/krb5.keytab /etc/krb5.keytab
# chmod 600 /etc/krb5.keytab
```

You should now be able to get a Kerberos ticket on the client:

 `$ kinit` 
```
Password for myuser@EXAMPLE.COM: ***

```
 `$ klist` 
```
Ticket cache: FILE:/tmp/krb5cc_1000
Default principal: myuser@EXAMPLE.COM

Valid starting       Expires              Service principal
08/30/2017 15:36:10  08/31/2017 15:36:10  krbtgt/EXAMPLE.COM@EXAMPLE.COM

```

## Advanced configuration

### DNS records

 `db.example.com` 
```
kerberos           A   1.2.3.4
_kerberos          TXT "EXAMPLE.COM"
_kerberos._udp     SRV 0 0  88 kerberos.example.com.
_kerberos-adm._udp SRV 0 0 750 kerberos.example.com.

```

Do not forget reverse DNS.

### Firewall

Add ALLOW rules to your firewall for both tcp and udp on ports 88 and 750.

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

Modify your [SSH](/index.php/SSH "SSH") server configuration to enable GSSAPI authentication:

 `/etc/ssh/sshd_config` 
```
# GSSAPI Options
GSSAPIAuthentication yes
GSSAPICleanupCredentials yes

```

And modify your client configuration to send GSSAPI requests:

 `/etc/ssh/ssh_config` 
```
Host *
  GSSAPIAuthentication yes
  GSSAPIDelegateCredentials yes

```

Get a ticket-granting ticket on the client before using ssh:

 `$ kinit myuser@EXAMPLE.COM`  `Password for myuser@EXAMPLE.COM: ***` 

Pass the -v option to ssh to make sure it works:

 `$ ssh kbserver.example.com -v` 
```
debug1: Authentications that can continue: publickey,gssapi-with-mic,password
debug1: Next authentication method: gssapi-with-mic
debug1: Delegating credentials
debug1: Delegating credentials
debug1: Authentication succeeded (gssapi-with-mic).
Authenticated to krb5-server ([192.168.100.136]:22).
debug1: channel 0: new [client-session]
debug1: Requesting no-more-sessions@openssh.com
debug1: Entering interactive session.
debug1: pledge: network
debug1: client_input_global_request: rtype hostkeys-00@openssh.com want_reply 0
Last login: Wed Aug 30 15:52:41 2017 from 192.168.100.1

```

You should now see a host ticket on the client:

 `$ klist` 
```
Ticket cache: FILE:/tmp/krb5cc_1000
Default principal: myuser@EXAMPLE.COM

Valid starting       Expires              Service principal
08/30/2017 15:37:40  08/31/2017 15:37:40  krbtgt/EXAMPLE.COM@EXAMPLE.COM
08/30/2017 15:53:04  08/31/2017 15:37:40  host/krb5-server.example.com@EXAMPLE.COM

```

## NFS

### Create service principals

Create service principals for **both** your NFS client and your NFS server on the KDC:

 `kadmin.local: addprinc -randkey nfs/nfsclient.example.com` 
```
WARNING: no policy specified for nfs/nfsclient.example.com@EXAMPLE.COM; defaulting to no policy
Principal "nfs/nfsclient.example.com@EXAMPLE.COM" created.

```

And add to the keytab:

 `kadmin.local: ktadd nfs/nfsclient.example.com` 
```
Entry for principal nfs/nfsclient.example.com with kvno 2, encryption type aes256-cts-hmac-sha1-96 added to keytab FILE:/etc/krb5.keytab.
Entry for principal nfs/nfsclient.example.com with kvno 2, encryption type aes128-cts-hmac-sha1-96 added to keytab FILE:/etc/krb5.keytab.

```

Then distribute `/etc/krb5.keytab` to your NFS clients and server.

### NFS Server

Add the Kerberos export option:

 `/etc/exports` 
```
/srv/export *(rw,async,no_subtree_check,no_root_squash,sec=krb5)

```

And reload the server:

```
# exportfs -ra

```

### NFS Client

Mount the server by passing the sec=krb5 mount option:

```
# mount -o sec=krb5 nfsserver:/srv/export /mnt/

```

Check that it worked with the `mount` command:

 `mount | grep krb5` 
```
nfsserver:/srv/export on /mnt type nfs4 (rw,relatime,vers=4.1,rsize=131072,wsize=131072,namlen=255,hard,proto=tcp,port=0,timeo=600,retrans=2,sec=krb5,clientaddr=192.168.100.139,local_lock=none,addr=192.168.100.136)

```

## See also

*   [RHEL7: Configure a Kerberos KDC](https://www.certdepot.net/rhel7-configure-kerberos-kdc/)
*   [RHEL7: Configure a system to authenticate using Kerberos](https://www.certdepot.net/rhel7-configure-system-authenticate-using-kerberos/)