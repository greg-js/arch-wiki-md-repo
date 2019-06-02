Related articles

*   [Samba](/index.php/Samba "Samba")
*   [Samba/Active Directory domain controller](/index.php/Samba/Active_Directory_domain_controller "Samba/Active Directory domain controller")
*   [SOGo](/index.php/SOGo "SOGo")

From [Wikipedia](https://en.wikipedia.org/wiki/Active_Directory "w:Active Directory"):

	Active Directory (AD) is a [directory service](https://en.wikipedia.org/wiki/directory_service "wikipedia:directory service") that Microsoft developed for [Windows domain](https://en.wikipedia.org/wiki/Windows_domain "wikipedia:Windows domain") networks.

This article describes how to integrate an Arch Linux system with an existing Windows domain network using [Samba](/index.php/Samba "Samba").

Before continuing, you must have an existing Active Directory domain, and have a user with the appropriate rights within the domain to: query users and add computer accounts (Domain Join).

This document is not an intended as a complete guide to Active Directory nor Samba. Refer to the resources section for additional information.

Active Directory serves as a central location for network administration and security. It is responsible for authenticating and authorizing all users and computers within a Windows domain network, assigning and enforcing security policies for all computers in a network and installing or updating software on network computers. For example, when a user logs into a computer that is part of a Windows domain, it is Active Directory that verifies his or her password and specifies whether he or she is a system administrator or normal user. Server computers on which Active Directory is running are called domain controllers.

Active Directory uses [Lightweight Directory Access Protocol (LDAP)](https://en.wikipedia.org/wiki/Ldap "wikipedia:Ldap") versions 2 and 3, Microsoft's version of [Kerberos](/index.php/Kerberos "Kerberos") and DNS.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Terminology](#Terminology)
*   [2 Active Directory configuration](#Active_Directory_configuration)
    *   [2.1 GPO considerations](#GPO_considerations)
*   [3 Linux host configuration](#Linux_host_configuration)
    *   [3.1 Installation](#Installation)
    *   [3.2 Updating DNS](#Updating_DNS)
    *   [3.3 Configuring NTP](#Configuring_NTP)
    *   [3.4 Kerberos](#Kerberos)
        *   [3.4.1 Creating a Kerberos ticket](#Creating_a_Kerberos_ticket)
        *   [3.4.2 Validating the Ticket](#Validating_the_Ticket)
    *   [3.5 pam_winbind.conf](#pam_winbind.conf)
    *   [3.6 Samba](#Samba)
    *   [3.7 Join the domain](#Join_the_domain)
*   [4 Starting and testing services](#Starting_and_testing_services)
    *   [4.1 Starting Samba](#Starting_Samba)
    *   [4.2 Testing Winbind](#Testing_Winbind)
    *   [4.3 Testing nsswitch](#Testing_nsswitch)
    *   [4.4 Testing Samba commands](#Testing_Samba_commands)
*   [5 Configuring PAM](#Configuring_PAM)
    *   [5.1 system-auth](#system-auth)
        *   [5.1.1 "auth" section](#"auth"_section)
        *   [5.1.2 "account" section](#"account"_section)
        *   [5.1.3 "password" section](#"password"_section)
        *   [5.1.4 "session" section](#"session"_section)
    *   [5.2 passwd](#passwd)
        *   [5.2.1 "password" section](#"password"_section_2)
    *   [5.3 Testing login](#Testing_login)
*   [6 Configuring Shares](#Configuring_Shares)
*   [7 Adding a machine keytab file and activating password-free kerberized ssh to the machine](#Adding_a_machine_keytab_file_and_activating_password-free_kerberized_ssh_to_the_machine)
    *   [7.1 Creating a machine key tab file](#Creating_a_machine_key_tab_file)
    *   [7.2 Enabling keytab authentication](#Enabling_keytab_authentication)
    *   [7.3 Preparing sshd on server](#Preparing_sshd_on_server)
    *   [7.4 Adding necessary options on client](#Adding_necessary_options_on_client)
    *   [7.5 Testing the setup](#Testing_the_setup)
    *   [7.6 Nifty fine-tuning for complete password-free kerberos handling.](#Nifty_fine-tuning_for_complete_password-free_kerberos_handling.)
*   [8 Generating user Keytabs which are accepted by AD](#Generating_user_Keytabs_which_are_accepted_by_AD)
    *   [8.1 Nice to know](#Nice_to_know)
*   [9 See also](#See_also)
    *   [9.1 Commercial Solutions](#Commercial_Solutions)
    *   [9.2 OpenSource version](#OpenSource_version)

## Terminology

If you are not familiar with Active Directory, there are a few keywords that are helpful to know.

*   **Domain** : The name used to group computers and accounts.
*   **SID** : Each computer that joins the domain as a member must have a unique SID or System Identifier.
*   **SMB** : Server Message Block.
*   **NETBIOS**: Network naming protocol used as an alternative to DNS. Mostly legacy, but still used in Windows Networking.
*   **WINS**: Windows Information Naming Service. Used for resolving Netbios names to windows hosts.
*   **Winbind**: Protocol for windows authentication.

## Active Directory configuration

This section works with the default configuration of Windows Server 2012 R2.

### GPO considerations

Digital signing is enabled by default in Windows Server, and must be enabled at both the client and server level. For certain versions of Samba, Linux clients may experience issues connecting to the domain and/or shares. It's recommended you add the following parameters to your `smb.conf` file:

```
client signing = auto 
server signing = auto

```

If that is not successful, you can disable *Digital Sign Communication (Always)* in the AD group policies. In your AD Group Policy editor, locate:

Under *Local policies > Security policies > Microsoft Network Server > Digital sign communication (Always)* activate *define this policy* and use the *disable* radio button.

If you use Windows Server 2008 R2, you need to modify that in *GPO for Default Domain Controller Policy > Computer Setting > Policies > Windows Setting > Security Setting > Local Policies > Security Option > Microsoft network client: Digitally sign communications (always)*.

Please note that disabling this GPO affects the security of all members of the domain.

## Linux host configuration

The next few steps will begin the process of configuring the Host. You will need root or sudo access to complete these steps.

### Installation

[Install](/index.php/Install "Install") the following packages:

*   [samba](https://www.archlinux.org/packages/?name=samba), see also [Samba](/index.php/Samba "Samba")
*   [pam-krb5](https://www.archlinux.org/packages/?name=pam-krb5)
*   [ntp](https://www.archlinux.org/packages/?name=ntp) or [openntpd](https://www.archlinux.org/packages/?name=openntpd), see also [NTPd](/index.php/NTPd "NTPd") or [OpenNTPD](/index.php/OpenNTPD "OpenNTPD")

### Updating DNS

Active Directory is heavily dependent upon DNS. You will need to update `/etc/resolv.conf` to use one or more of the Active Directory domain controllers:

 `/etc/resolv.conf` 
```
nameserver <IP1>
nameserver <IP2>

```

Replacing <IP1> and <IP2> with valid IP addresses for the AD servers. If your AD domains do not permit DNS forwarding or recursion, you may need to add additional resolvers.

**Note:** If your machine dual boots Windows and Linux, you should use a different DNS hostname and netbios name for the linux configuration if both operating systems will be members of the same domain.

### Configuring NTP

Read [System time#Time synchronization](/index.php/System_time#Time_synchronization "System time") to configure an NTP service.

On the NTP servers configuration, use the IP addresses for the AD servers, as they typically run NTP as a service. Alternatively, you can use other known NTP servers provided the Active directory servers sync to the same stratum.

Ensure that the service is configured to sync the time automatically very early on startup.

### Kerberos

Let us assume that your AD is named example.com. Let us further assume your AD is ruled by two domain controllers, the primary and secondary one, which are named PDC and BDC, pdc.example.com and bdc.example.com respectively. Their IP adresses will be 192.168.1.2 and 192.168.1.3 in this example. Take care to watch your syntax; upper-case is very important here.

 `/etc/krb5.conf` 
```
[libdefaults]
        default_realm 	= 	EXAMPLE.COM
	clockskew 	= 	300
	ticket_lifetime	=	1d
        forwardable     =       true
        proxiable       =       true
        dns_lookup_realm =      true
        dns_lookup_kdc  =       true

[realms]
	EXAMPLE.COM = {
		kdc 	= 	PDC.EXAMPLE.COM
                admin_server = PDC.EXAMPLE.COM
		default_domain = EXAMPLE.COM
	}

[domain_realm]
        .kerberos.server = EXAMPLE.COM
	.example.com = EXAMPLE.COM
	example.com = EXAMPLE.COM
	example	= EXAMPLE.COM

[appdefaults]
	pam = {
	ticket_lifetime 	= 1d
	renew_lifetime 		= 1d
	forwardable 		= true
	proxiable 		= false
	retain_after_close 	= false
	minimum_uid 		= 0
	debug 			= false
	}

[logging]
	default 		= FILE:/var/log/krb5libs.log
	kdc 			= FILE:/var/log/kdc.log
        admin_server            = FILE:/var/log/kadmind.log

```

**Note:** Heimdal 1.3.1 deprecated DES encryption which is required for AD authentication before Windows Server 2008\. You will probably have to add `allow_weak_crypto = true` to the `[libdefaults]` section.

#### Creating a Kerberos ticket

**Note:** The keys and commands are user specific: sudo will be root, so your non-elevated account can connect to a different AD user with a separate key. If you only have one domain, it is not necessary to type @EXAMPLE.COM

Now you can query the AD domain controllers and request a kerberos ticket (**uppercase is necessary**):

 `kinit administrator@EXAMPLE.COM` 

You can use any username that has rights as a Domain Administrator.

#### Validating the Ticket

Run **klist** to verify you did receive the token. You should see something similar to:

 `# klist` 
```
 Ticket cache: FILE:/tmp/krb5cc_0
 Default principal: administrator@EXAMPLE.COM

 Valid starting    Expires           Service principal 
 02/04/12 21:27:47 02/05/12 07:27:42 krbtgt/EXAMPLE.COM@EXAMPLE.COM
         renew until 02/05/12 21:27:47

```

### pam_winbind.conf

If you get errors stating that /etc/security/pam_winbind.conf was not found, create the file and add the following:

 `/etc/security/pam_winbind.conf` 
```
[global]
  debug = no
  debug_state = no
  try_first_pass = yes
  krb5_auth = yes
  krb5_ccache_type = FILE
  cached_login = yes
  silent = no
  mkhomedir = yes

```

With this setup, winbind will create user keytabs on the fly (krb5_ccache_type = FILE) at login and maintain them. You can verify this by simply running klist in a shell after logging in as an AD user but without needing to run kinit. You may need to set additional permissions on /etc/krb5.keytab eg 640 instead of 600 to get this to work (see [FS#52621](https://bugs.archlinux.org/task/52621) for example)

### Samba

Samba is a free software re-implementation of the SMB/CIFS networking protocol. It also includes tools for Linux machines to act as Windows networking servers and clients.

**Note:** The configuration can vary greatly depending on how the Windows environment is deployed. Be prepared to troubleshoot and research

In this section, we will focus on getting Authentication to work first by editing the 'Global' section first. Later, we will go back and add shares.

 `/etc/samba/smb.conf` 
```
[Global]
  netbios name = MYARCHLINUX
  workgroup = EXAMPLE
  realm = EXAMPLE.COM
  server string = %h ArchLinux Host
  security = ads
  encrypt passwords = yes
  password server = pdc.example.com
  client signing = auto
  server signing = auto

  idmap config * : backend = tdb
  idmap config * : range = 10000-20000

  winbind use default domain = Yes
  winbind enum users = Yes
  winbind enum groups = Yes
  winbind nested groups = Yes
  winbind separator = +
  winbind refresh tickets = yes
  winbind offline logon = yes
  winbind cache time = 300

  template shell = /bin/bash
  template homedir = /home/%D/%U

  preferred master = no
  dns proxy = no
  wins server = pdc.example.com
  wins proxy = no

  inherit acls = Yes
  map acl inherit = Yes
  acl group control = yes

  load printers = no
  debug level = 3
  use sendfile = no

```

### Join the domain

You need an AD Administrator account to do this. Let us assume this is named Administrator. The command is 'net ads join'

 `# net ads join -U Administrator` 
```
Administrator's password: xxx
Using short domain name -- EXAMPLE
Joined 'MYARCHLINUX' to realm 'EXAMPLE.COM'

```

## Starting and testing services

### Starting Samba

Hopefully, you have not rebooted yet! Fine. If you are in an X-session, quit it, so you can test login into another console, while you are still logged in.

Enable and start the individual Samba daemons `smbd.service`, `nmbd.service`, and `winbindd.service`.

**Note:** In [samba](https://www.archlinux.org/packages/?name=samba) 4.8.0-1, the Samba daemon units have been renamed from `smbd.service`, `nmbd.service`, and `winbindd.service` to `smb.service`, `nmb.service`, and `winbind.service`.

Next we will need to modify the NSSwitch configuration, which tells the Linux host how to retrieve information from various sources and in which order to do so. In this case, we are appending Active Directory as additional sources for Users, Groups, and Hosts.

 `/etc/nsswitch.conf` 
```
 passwd:            files winbind
 shadow:            files winbind
 group:             files winbind 

 hosts:             files dns wins

```

### Testing Winbind

Let us check if winbind is able to query the AD. The following command should return a list of AD users:

 `# wbinfo -u` 
```
administrator
guest
krbtgt
test.user

```

*   Note we created an Active Directory user called 'test.user' on the domain controller

We can do the same for AD groups:

 `# wbinfo -g` 
```
domain computers
domain controllers
schema admins
enterprise admins
cert publishers
domain admins
domain users
domain guests
group policy creator owners
ras and ias servers
allowed rodc password replication group
denied rodc password replication group
read-only domain controllers
enterprise read-only domain controllers
dnsadmins
dnsupdateproxy

```

### Testing nsswitch

To ensure that our host is able to query the domain for users and groups, we test nsswitch settings by issuing the 'getent' command.

If user accounts from your DC are not showing, try adding the following line to your smb.conf file:

 `/etc/samba/smb.conf` 
```
winbind trusted domains only = no

```

The following output shows what a stock ArchLinux install looks like:

 `# getent passwd` 
```
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/bin/false
daemon:x:2:2:daemon:/sbin:/bin/false
mail:x:8:12:mail:/var/spool/mail:/bin/false
ftp:x:14:11:ftp:/srv/ftp:/bin/false
http:x:33:33:http:/srv/http:/bin/false
nobody:x:99:99:nobody:/:/bin/false
dbus:x:81:81:System message bus:/:/bin/false
ntp:x:87:87:Network Time Protocol:/var/empty:/bin/false
avahi:x:84:84:avahi:/:/bin/false
administrator:*:10001:10006:Administrator:/home/EXAMPLE/administrator:/bin/bash
guest:*:10002:10007:Guest:/home/EXAMPLE/guest:/bin/bash
krbtgt:*:10003:10006:krbtgt:/home/EXAMPLE/krbtgt:/bin/bash
test.user:*:10000:10006:Test User:/home/EXAMPLE/test.user:/bin/bash

```

And for groups:

 `# getent group` 
```
root:x:0:root
bin:x:1:root,bin,daemon
daemon:x:2:root,bin,daemon
sys:x:3:root,bin
adm:x:4:root,daemon
tty:x:5:
disk:x:6:root
lp:x:7:daemon
mem:x:8:
kmem:x:9:
wheel:x:10:root
ftp:x:11:
mail:x:12:
uucp:x:14:
log:x:19:root
utmp:x:20:
locate:x:21:
rfkill:x:24:
smmsp:x:25:
http:x:33:
games:x:50:
network:x:90:
video:x:91:
audio:x:92:
optical:x:93:
floppy:x:94:
storage:x:95:
scanner:x:96:
power:x:98:
nobody:x:99:
users:x:100:
dbus:x:81:
ntp:x:87:
avahi:x:84:
domain computers:x:10008:
domain controllers:x:10009:
schema admins:x:10010:administrator
enterprise admins:x:10011:administrator
cert publishers:x:10012:
domain admins:x:10013:test.user,administrator
domain users:x:10006:
domain guests:x:10007:
group policy creator owners:x:10014:administrator
ras and ias servers:x:10015:
allowed rodc password replication group:x:10016:
denied rodc password replication group:x:10017:krbtgt
read-only domain controllers:x:10018:
enterprise read-only domain controllers:x:10019:
dnsadmins:x:10020:
dnsupdateproxy:x:10021:

```

### Testing Samba commands

Try out some net commands to see if Samba can communicate with AD:

 `# net ads info` 
```
[2012/02/05 20:21:36.473559,  0] param/loadparm.c:7599(lp_do_parameter)
  Ignoring unknown parameter "idmapd backend"
LDAP server: 192.168.1.2
LDAP server name: PDC.example.com
Realm: EXAMPLE.COM
Bind Path: dc=EXAMPLE,dc=COM
LDAP port: 389
Server time: Sun, 05 Feb 2012 20:21:33 CST
KDC server: 192.168.1.2
Server time offset: -3

```
 `# net ads lookup` 
```
[2012/02/05 20:22:39.298823,  0] param/loadparm.c:7599(lp_do_parameter)
  Ignoring unknown parameter "idmapd backend"
Information for Domain Controller: 192.168.1.2

Response Type: LOGON_SAM_LOGON_RESPONSE_EX
GUID: 2a098512-4c9f-4fe4-ac22-8f9231fabbad
Flags:
        Is a PDC:                                   yes
        Is a GC of the forest:                      yes
        Is an LDAP server:                          yes
        Supports DS:                                yes
        Is running a KDC:                           yes
        Is running time services:                   yes
        Is the closest DC:                          yes
        Is writable:                                yes
        Has a hardware clock:                       yes
        Is a non-domain NC serviced by LDAP server: no
        Is NT6 DC that has some secrets:            no
        Is NT6 DC that has all secrets:             yes
Forest:                 example.com
Domain:                 example.com
Domain Controller:      PDC.example.com
Pre-Win2k Domain:       EXAMPLE
Pre-Win2k Hostname:     PDC
Server Site Name :              Office
Client Site Name :              Office
NT Version: 5
LMNT Token: ffff
LM20 Token: ffff

```
 `# net ads status -U administrator%password | less` 
```
objectClass: top
objectClass: person
objectClass: organizationalPerson
objectClass: user
objectClass: computer
cn: myarchlinux
distinguishedName: CN=myarchlinux,CN=Computers,DC=leafscale,DC=inc
instanceType: 4
whenCreated: 20120206043413.0Z
whenChanged: 20120206043414.0Z
uSNCreated: 16556
uSNChanged: 16563
name: myarchlinux
objectGUID: 2c24029c-8422-42b2-83b3-a255b9cb41b3
userAccountControl: 69632
badPwdCount: 0
codePage: 0
countryCode: 0
badPasswordTime: 0
lastLogoff: 0
lastLogon: 129729780312632000
localPolicyFlags: 0
pwdLastSet: 129729764538848000
primaryGroupID: 515
objectSid: S-1-5-21-719106045-3766251393-3909931865-1105
...<snip>...

```

## Configuring PAM

Now we will change various rules in PAM to allow Active Directory users to use the system for things like login and sudo access. When changing the rules, note the order of these items and whether they are marked as **required** or **sufficient** is critical to things working as expected. You should not deviate from these rules unless you know how to write PAM rules.

In case of logins, PAM should first ask for AD accounts, and for local accounts if no matching AD account was found. Therefore, we add entries to include `pam_winbind.so` into the authentication process.

The Arch Linux PAM configuration keeps the central auth process in `/etc/pam.d/system-auth`. Starting with the stock configuration from `pambase`, change it like this:

### system-auth

#### "auth" section

Find the line:

```
auth required pam_unix.so ...

```

Delete it, and replace with:

```
auth [success=1 default=ignore] pam_localuser.so
auth [success=2 default=die] pam_winbind.so
auth [success=1 default=die] pam_unix.so nullok
auth requisite pam_deny.so

```

#### "account" section

Find the line:

```
account required pam_unix.so

```

Keep it, and add this below:

```
account [success=1 default=ignore] pam_localuser.so
account required pam_winbind.so

```

#### "password" section

Find the line:

```
password required pam_unix.so ...

```

Delete it, and replace with:

```
password [success=1 default=ignore] pam_localuser.so
password [success=2 default=die] pam_winbind.so
password [success=1 default=die] pam_unix.so sha512 shadow
password requisite pam_deny.so

```

#### "session" section

Find the line:

```
session required pam_unix.so

```

Keep it, and add this line immediately above it:

```
session required pam_mkhomedir.so skel=/etc/skel/ umask=0022

```

Below the pam_unix line, add these:

```
session [success=1 default=ignore] pam_localuser.so
session required pam_winbind.so

```

### passwd

#### "password" section

In order for logged-in Active Directory users to be able to change their passwords with the 'passwd' command, the file `/etc/pam.d/passwd` must include the information from system-auth.

Find the line:

```
password required pam_unix.so sha512 shadow nullok

```

Delete it, and replace with:

```
password include system-auth

```

### Testing login

Now, start a new console session (or ssh) and try to login using the AD credentials. The domain name is optional, as this was set in the Winbind configuration as 'default realm'. Please note that in the case of ssh, you will need to modify the `/etc/ssh/sshd_config` file to allow kerberos authentication `(KerberosAuthentication yes)`.

```
test.user
EXAMPLE+test.user

```

Both should work. You should notice that `/home/example/test.user` will be automatically created. **Log into another session using an linux account. Check that you still be able to log in as root - but keep in mind to be logged in as root in at least one session!**

## Configuring Shares

Earlier we skipped configuration of the shares. Now that things are working, go back to `/etc/samba/smb.conf`, and add the exports for the host that you want available on the windows network.

 `/etc/samba/smb.conf` 
```
[MyShare]
  comment = Example Share
  path = /srv/exports/myshare
  read only = no
  browseable = yes
  valid users = @NETWORK+"Domain Admins" NETWORK+test.user

```

In the above example, the keyword **NETWORK** is to be used. Do not mistakenly substitute this with your domain name. For adding groups, prepend the '@' symbol to the group. Note that `Domain Admins` is encapsulated in quotes so Samba correctly parses it when reading the configuration file.

## Adding a machine keytab file and activating password-free kerberized ssh to the machine

This explains how to generate a machine keytab file which you will need e.g. to enable password-free kerberized ssh to your machine from other machines in the domain. The scenario in mind is that you have a bunch of systems in your domain and you just added a server/workstation using the above description to your domain onto which a lot of users need to ssh in order to work - e.g. GPU workstation or an OpenMP compute node, etc. In this case you might not want to type your password every time you log in. On the other hand the key authentication used by many users in this case can not give you the necessary credentials to e.g. mount kerberized NFSv4 shares. So this will help you to enable password-free logins from your clients to the machine in question using kerberos ticket forwarding.

### Creating a machine key tab file

run 'net ads keytab create -U administrator' as root to create a machine keytab file in /etc/krb5.keytab. It will prompt you with a warning that we need to enable keytab authentication in our configuration file, so we will do that in the next step. In my case it had problems when a key tab file is already in place - the command just did not come back it hang ... In that case you should rename the existing /etc/krb5.keytab and run the command again - it should work now.

 `# net ads keytab create -U administrator` 

verify the content of your keytab by running:

 `# klist -k /etc/krb5.keytab` 
```
Keytab name: FILE:/etc/krb5.keytab
KVNO Principal
---- --------------------------------------------------------------------------
   4 host/myarchlinux.example.com@EXAMPLE.COM
   4 host/myarchlinux.example.com@EXAMPLE.COM
   4 host/myarchlinux.example.com@EXAMPLE.COM
   4 host/myarchlinux.example.com@EXAMPLE.COM
   4 host/myarchlinux.example.com@EXAMPLE.COM
   4 host/MYARCHLINUX@EXAMPLE.COM
   4 host/MYARCHLINUX@EXAMPLE.COM
   4 host/MYARCHLINUX@EXAMPLE.COM
   4 host/MYARCHLINUX@EXAMPLE.COM
   4 host/MYARCHLINUX@EXAMPLE.COM
   4 MYARCHLINUX$@EXAMPLE.COM
   4 MYARCHLINUX$@EXAMPLE.COM
   4 MYARCHLINUX$@EXAMPLE.COM
   4 MYARCHLINUX$@EXAMPLE.COM
   4 MYARCHLINUX$@EXAMPLE.COM

```

### Enabling keytab authentication

Now you need to tell winbind to use the file by adding these lines to the /etc/samba/smb.conf:

```
 kerberos method = secrets and keytab
 dedicated keytab file = /etc/krb5.keytab

```

It should look something like this:

 `/etc/samba/smb.conf` 
```
[Global]
  netbios name = MYARCHLINUX
  workgroup = EXAMPLE
  realm = EXAMPLE.COM
  server string = %h ArchLinux Host
  security = ads
  encrypt passwords = yes
  password server = pdc.example.com
  kerberos method = secrets and keytab
  dedicated keytab file = /etc/krb5.keytab

  idmap config * : backend = tdb
  idmap config * : range = 10000-20000

  winbind use default domain = Yes
  winbind enum users = Yes
  winbind enum groups = Yes
  winbind nested groups = Yes
  winbind separator = +
  winbind refresh tickets = yes

  template shell = /bin/bash
  template homedir = /home/%D/%U

  preferred master = no
  dns proxy = no
  wins server = pdc.example.com
  wins proxy = no

  inherit acls = Yes
  map acl inherit = Yes
  acl group control = yes

  load printers = no
  debug level = 3
  use sendfile = no

```

Restart the winbind daemon using 'systemctl restart winbindd.service' with root privileges.

 `# systemctl restart winbindd.service` 

Check if everything works by getting a machine ticket for your system by running

 `# kinit MYARCHLINUX$ -kt /etc/krb5.keytab` 

This should not give you any feedback but running 'klist' should show you sth like:

 `# klist` 
```
 Ticket cache: FILE:/tmp/krb5cc_0
 Default principal: MYARCHLINUX$@EXAMPLE.COM

 Valid starting    Expires           Service principal 
 02/04/12 21:27:47 02/05/12 07:27:42 krbtgt/EXAMPLE.COM@EXAMPLE.COM
         renew until 02/05/12 21:27:47

```

Some common mistakes here are a) forgetting the trailing $ or b) ignoring case sensitivity - it needs to look exactly like the entry in the keytab (usually you cannot to much wrong with all capital)

### Preparing sshd on server

All we need to do is add some options to our sshd_config and restart the sshd.service.

Edit /etc/ssh/sshd_config to look like this in the appropriate places:

 `# /etc/ssh/sshd_config` 
```

...

# Change to no to disable s/key passwords
ChallengeResponseAuthentication no

# Kerberos options
KerberosAuthentication yes
#KerberosOrLocalPasswd yes
KerberosTicketCleanup yes
KerberosGetAFSToken yes

# GSSAPI options
GSSAPIAuthentication yes
GSSAPICleanupCredentials yes

...

```

Restart the sshd.service using:

 `# systemctl restart sshd.service` 

### Adding necessary options on client

First we need to make sure that the tickets on our client are forwardable. This is usually standard but we better check anyways. You have to look for the forwardable option and set it to 'true' in the Kerberos config file /etc/krb5.conf

 `forwardable     =       true` 

Secondly we need to add the options

```
 GSSAPIAuthentication yes
 GSSAPIDelegateCredentials yes

```

to our .ssh/config file to tell ssh to use this options - alternatively they can be invoked using the -o options directly in the ssh command (see 'man ssh' for help).

### Testing the setup

On Client:

make sure you have a valid ticket - if in doubt run 'kinit'

then use ssh to connect to you machine

 `ssh myarchlinux.example.com ` 

you should get connected without needing to enter your password.

if you have key authentication additionally activated then you should perform

 `ssh -v myarchlinux.example.com ` 

to see which authentication method it actually uses.

For debugging you can enable DEBUG3 on the server and look into the journal using [journalctl](/index.php/Journalctl "Journalctl").

### Nifty fine-tuning for complete password-free kerberos handling.

In case your clients are not using domain accounts on their local machines (for whatever reason) it can be hard to actually teach them to kinit before ssh to the workstation. Therefore I came up with a nice workaround:

## Generating user Keytabs which are accepted by AD

On a system let the user run:

```
ktutil
addent -password -p username@EXAMPLE.COM -k 1 -e RC4-HMAC
- enter password for username -
wkt username.keytab
q

```

Now test the file by invoking:

 `kinit username@EXAMPLE.COM -kt username.keytab` 

It should not promt you to give your password nor should it give any other feedback. If it worked you are basically done - just put the line above into your ~./bashrc - you can now get kerberos tickets without typing a password and with that you can connect to your workstation without typing a password while being completely kerberized and able to authenticate against NFSv4 and CIFS via tickets - pretty neat.

### Nice to know

The file 'username.keytab' is not machinespecific and can therefore be copied around. E.g. we created the files on a linux machine and copied them to our Mac clients as the commands on Macs are different ...

## See also

*   [Wikipedia - Active Directory](https://en.wikipedia.org/wiki/Active_Directory "wikipedia:Active Directory")
*   [Wikipedia - Samba](https://en.wikipedia.org/wiki/Samba_(software) "wikipedia:Samba (software)")
*   [Wikipedia - Kerberos](https://en.wikipedia.org/wiki/Kerberos_(protocol) "wikipedia:Kerberos (protocol)")
*   [Samba - Documentation](http://www.samba.org/samba/docs)
*   [Samba Wiki - Samba & Active Directory](http://wiki.samba.org/index.php/Samba_&_Active_Directory)
*   [`smb.conf(5)` manpage](http://www.samba.org/samba/docs/man/manpages-3/smb.conf.5.html)

### Commercial Solutions

*   Centrify
*   Likewise

### OpenSource version

*   [PowerBroker Identity Services Open](https://github.com/BeyondTrust/pbis-open/): formerly Likewise acquired by BeyondTrust
*   [Centrify Express for Linux](https://www.centrify.com/express/linux/)