Related articles

*   [Active Directory Integration](/index.php/Active_Directory_Integration "Active Directory Integration")

[Kerberos](https://en.wikipedia.org/wiki/Kerberos_(protocol) is a network authentication system. See [krb5 documentation](https://web.mit.edu/kerberos/krb5-latest/doc/).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Server configuration](#Server_configuration)
    *   [2.1 Domain creation](#Domain_creation)
    *   [2.2 Add principals](#Add_principals)
    *   [2.3 Firewall](#Firewall)
    *   [2.4 DNS records](#DNS_records)
*   [3 Client configuration](#Client_configuration)
    *   [3.1 Testing](#Testing)
*   [4 Configuring kadmin](#Configuring_kadmin)
    *   [4.1 Configuring kadmin ACL](#Configuring_kadmin_ACL)
*   [5 Service principals and keytabs](#Service_principals_and_keytabs)
    *   [5.1 With remote kadmin](#With_remote_kadmin)
    *   [5.2 Without remote kadmin](#Without_remote_kadmin)
*   [6 Cross-Realm Trust](#Cross-Realm_Trust)
*   [7 SSH Authentication](#SSH_Authentication)
    *   [7.1 Authorize other principals](#Authorize_other_principals)
*   [8 NFS Security](#NFS_Security)
    *   [8.1 NFS Server](#NFS_Server)
    *   [8.2 NFS Client](#NFS_Client)
*   [9 Browsers](#Browsers)
    *   [9.1 Chromium](#Chromium)
    *   [9.2 Firefox](#Firefox)
*   [10 Troubleshooting](#Troubleshooting)
    *   [10.1 Cannot set GSSAPI authentication names](#Cannot_set_GSSAPI_authentication_names)
*   [11 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [krb5](https://www.archlinux.org/packages/?name=krb5) package on your clients and server.

It is **highly** recommended to use a [time synchronization](/index.php/Time_synchronization "Time synchronization") daemon to keep client/server clocks in sync.

If hostname resolution has not been configured, you can manually add your clients and server to the [hosts(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hosts.5) file of each machine. Note that the FQDN (myclient.example.com) must be the first hostname after the IP address in the hosts file.

## Server configuration

### Domain creation

Edit `/etc/krb5.conf` to configure your domain:

 `/etc/krb5.conf` 
```
[libdefaults]
    default_realm = EXAMPLE.COM

[realms]
    EXAMPLE.COM = {
        admin_server = kerberos.example.com
        # use "kdc = ..." if the kerberos SRV records aren't in DNS (see Advanced section)
        kdc = kerberos.example.com
        # This breaks krb4 compatibility but increases security
        default_principal_flags = +preauth
    }

[domain_realm]
    example.com  = EXAMPLE.COM
    .example.com = EXAMPLE.COM

[logging]
    kdc          = SYSLOG:NOTICE
    admin_server = SYSLOG:NOTICE
    default      = SYSLOG:NOTICE

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
# systemctl enable --now krb5-kdc krb5-kadmind

```

### Add principals

Start the Kerberos administration tool, using local authentication

 `# kadmin.local` 
```
Authenticating as principal root/admin@EXAMPLE.COM with password.
kadmin.local:
```

Add a user principal to the Kerberos database:

 `kadmin.local: addprinc myuser@EXAMPLE.COM` 
```
WARNING: no policy specified for myuser@EXAMPLE.COM; defaulting to no policy
Enter password for principal "myuser@EXAMPLE.COM": ***
Re-enter password for principal "myuser@EXAMPLE.COM": ***
Principal "myuser@EXAMPLE.COM" created.

```

Add the KDC principal to the Kerberos database:

 `kadmin.local: addprinc -randkey host/kerberos.example.com` 
```
WARNING: no policy specified for host/kerberos.example.com@EXAMPLE.COM; defaulting to no policy
Principal "host/kerberos.example.com@EXAMPLE.COM" created.

```

Finally, Add the KDC principal to the server's keytab:

 `kadmin.local: ktadd host/kerberos.example.com` 
```
Entry for principal host/kerberos.example.com with kvno 2, encryption type aes256-cts-hmac-sha1-96 added to keytab FILE:/etc/krb5.keytab.
Entry for principal host/kerberos.example.com with kvno 2, encryption type aes128-cts-hmac-sha1-96 added to keytab FILE:/etc/krb5.keytab.

```

Quit the Kerberos administration tool:

```
kadmin.local: quit

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

### Firewall

Add ALLOW rules to your firewall for any applicable ports/protocols:

*   88, TCP and UDP for Kerberos v5
*   749, TCP and UDP for kadmin if you plan to configure it
*   750, TCP and UDP for Kerberos v4 if you need backwards compatibility

### DNS records

This isn't necessary if you specify the kerberos and kadmin server in each machine's krb5.conf

 `db.example.com` 
```
kerberos.example.com.           A     1.2.3.4
_kerberos.example.com.          TXT   "EXAMPLE.COM"
_kerberos._udp.example.com.     SRV   0 0  88 kerberos.example.com.
_kerberos-adm._udp.example.com. SRV   0 0 749 kerberos.example.com.

```

Do not forget reverse DNS.

## Client configuration

Edit the client's `/etc/krb5.conf` to match your server's configuration. You can copy this file from the server, or just set the required realm information.

### Testing

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

## Configuring kadmin

You'll need /etc/krb5.conf configured on the kadmin client, and the server's firewall configured for kadmin.

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

## Service principals and keytabs

First, ensure you've configured krb5.conf on all involved machines.

A kerberos principal has three components, formatted as `primary/instance@REALM`. For user principals, the primary is your username and the instance is omitted or is a role (eg. "admin"): `myuser@EXAMPLE.COM` or `myuser/admin@EXAMPLE.COM`. For hosts, the primary is "host" and the instance is the server FQDN: `host/myserver.example.com@EXAMPLE.COM`. For services, the primary is the service abbreviation and the instance is the FQDN: `nfs/myserver.example.com@EXAMPLE.COM`. The realm can often be omitted, the local computer's default realm is usually assumed.

### With remote kadmin

This is the easier method, but requires you to have configured [kadmin](#Configuring_kadmin).

Open kadmin as root (so we can write the keytab) on the client, authenticating with your admin principal:

 `client# kadmin -p myuser/admin` 
```
Authenticating as principal myuser/admin with password.
Password for myuser/admin@EXAMPLE.COM:
kadmin:

```

Add a principal for any services you will be using, eg. "host" for SSH authentication or "nfs" for NFS:

 `kadmin: addprinc -randkey host/kbclient.example.com` 
```
WARNING: no policy specified for host/kbclient.example.com@EXAMPLE.COM; defaulting to no policy
Principal "host/kbclient.example.com@EXAMPLE.COM" created.
```

Save each key to the local keytab:

 `kadmin: ktadd host/kbclient.example.com` 
```
Entry for principal host/kbclient.example.com with kvno 2, encryption type aes256-cts-hmac-sha1-96 added to keytab FILE:/etc/krb5.keytab.
Entry for principal host/kbclient.example.com with kvno 2, encryption type aes128-cts-hmac-sha1-96 added to keytab FILE:/etc/krb5.keytab.

```

### Without remote kadmin

Start kadmin on the Kerberos server, using either unix or kerberos authentication:

 `# kadmin.local` 
```
Authenticating as principal root/admin@EXAMPLE.COM with password.
kadmin.local:

```

Add a principal for any services you will be using, eg. "host" for SSH authentication or "nfs" for NFS:

 `kadmin.local: addprinc -randkey host/kbclient.example.com` 
```
WARNING: no policy specified for host/kbclient.example.com@EXAMPLE.COM; defaulting to no policy
Principal "host/kbclient.example.com@EXAMPLE.COM" created.

```

Save each key to a new keytab to be transferred to the client:

 `kadmin.local: ktadd -k kbclient.keytab host/kbclient.example.com` 
```
Entry for principal host/kbclient.example.com with kvno 2, encryption type aes256-cts-hmac-sha1-96 added to keytab FILE:/etc/krb5.keytab.
Entry for principal host/kbclient.example.com with kvno 2, encryption type aes128-cts-hmac-sha1-96 added to keytab FILE:/etc/krb5.keytab.

```

Finally, copy `kbclient.keytab` from the server to the client using SCP or similar, then put it in place with correct permissions:

 `# install -b -o root -g root -m 600 kbclient.keytab /etc/krb5.keytab` 

Finally, delete kbclient.keytab from the server and client.

## Cross-Realm Trust

Set up a second server as shown above, then create the cross-realm principal on both KDCs. Cross-realm principals must be created with strong passwords, not `-randkey`, and the same password must be used on both KDCs. The principal must have the same key version number (kvno) in both KDCs.

To grant EXAMPLE.COM principals access to EXAMPLE.ORG resources, you would use the following principal:

```
kadmin# addprinc krbtgt/EXAMPLE.ORG@EXAMPLE.COM

```

The `[capaths]` section of `krb5.conf` can be used to further control cross-realm trust relationships.

## SSH Authentication

Use the instructions in [Service principals and keytabs](#Service_principals_and_keytabs) to create a principal for the "host" service for both client and server, then put the client's keys in the client's keytab and the server's keys in the server's keytab.

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

Pass the -v option to ssh to watch what's happening:

 `$ ssh sshserver.example.com -v` 
```
debug1: Authentications that can continue: publickey,gssapi-with-mic,password
debug1: Next authentication method: gssapi-with-mic
debug1: Delegating credentials
debug1: Delegating credentials
debug1: Authentication succeeded (gssapi-with-mic).
Authenticated to sshserver.example.com ([192.168.100.136]:22).
debug1: channel 0: new [client-session]
debug1: Requesting no-more-sessions@openssh.com
debug1: Entering interactive session.
debug1: pledge: network
debug1: client_input_global_request: rtype hostkeys-00@openssh.com want_reply 0
Last login: Wed Aug 30 15:52:41 2017 from 192.168.100.1

```

And you should now see a host ticket on the client:

 `client$ klist` 
```
Ticket cache: FILE:/tmp/krb5cc_1000
Default principal: myuser@EXAMPLE.COM

Valid starting       Expires              Service principal
08/30/2017 15:37:40  08/31/2017 15:37:40  krbtgt/EXAMPLE.COM@EXAMPLE.COM
08/30/2017 15:53:04  08/31/2017 15:37:40  host/sshserver.example.com@EXAMPLE.COM

```

### Authorize other principals

To allow a different kerberos principal to authenticate to a user account, add the principal name to the target account's `.k5login` file. For example, to allow `robert@EXAMPLE.COM` to SSH to alice's account:

 `/home/alice/.k5login` 
```
robert@EXAMPLE.COM

```

## NFS Security

First, configure your [NFS server](/index.php/NFS#Server "NFS") server. Also see [NFS Troubleshooting](/index.php/NFS_Troubleshooting "NFS Troubleshooting"). Configuring a [time synchronization](/index.php/Time_synchronization "Time synchronization") daemon on both the clients and the server is strongly recommended. Clock drift will cause this to break, and the error message will not be helpful.

Use the instructions in [Service principals and keytabs](#Service_principals_and_keytabs) to create a principal for the "nfs" service for both client and server, then put the client's keys in the client's keytab and the server's keys in the server's keytab.

### NFS Server

Add a Kerberos export option:

*   sec=krb5 uses kerberos for authentication only, and transmits the data unauthenticated and unencrypted.
*   sec=krb5i uses kerberos for authentication and integrity checking, but still transmits data unencrypted.
*   sec=krb5p uses kerberos for authentication and encryption.

 `/etc/exports` 
```
/srv/export *(rw,async,no_subtree_check,no_root_squash,sec=krb5p)

```

And reload the exports:

```
# exportfs -arv

```

### NFS Client

Mount the exported directory:

```
# mount nfsserver:/srv/export /mnt/

```

You can add -vv for verbose information, and may need -t nfs4 and -o sec=krb5p or your chosen security option.

Check that it worked with the `mount` command:

 `mount | grep krb5` 
```
nfsserver:/srv/export on /mnt type nfs4 (rw,relatime,vers=4.1,rsize=131072,wsize=131072,namlen=255,hard,proto=tcp,port=0,timeo=600,retrans=2,sec=krb5,clientaddr=192.168.100.139,local_lock=none,addr=192.168.100.136)

```

## Browsers

Some browsers have support for Kerberos protocol but disable it by default. Here are the instructions how to enable it:

### Chromium

Chromium needs to be run with a command line parameter that specifies a list of sites where Kerberos authentication is allowed. The easiest way is to add persistent flag to the config file:

 `~/.config/chromium-flags.conf` 
```
--auth-server-whitelist='*.foo.com'

```

### Firefox

To configure Firefox with trusted sites visit `about:config` and set `network.negotiate-auth.trusted-uris` property to FOO.COM (Note: for Firefox there is no "*."; for Chrome, there is).

## Troubleshooting

### Cannot set GSSAPI authentication names

```
Cannot set GSSAPI authentication names, aborting

```

Your realm is missing either the `kadmin/admin` or `kadmin/changepw` principal.

For clients, invalid arguments/options may happen on first setup if rpc-gssd is not loaded. Loading it is usually acomplished by [enabling](/index.php/Enabling "Enabling") and [starting](/index.php/Starting "Starting") `nfs-client.target`, but after first setup this target will need a [restart](/index.php/Restart "Restart").

## See also

*   [RHEL7: Configure a Kerberos KDC](https://www.certdepot.net/rhel7-configure-kerberos-kdc/)
*   [RHEL7: Configure a system to authenticate using Kerberos](https://www.certdepot.net/rhel7-configure-system-authenticate-using-kerberos/)