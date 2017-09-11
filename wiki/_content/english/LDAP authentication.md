Related articles

*   [OpenLDAP](/index.php/OpenLDAP "OpenLDAP")
*   [LDAP Hosts](/index.php/LDAP_Hosts "LDAP Hosts")

## Contents

*   [1 Introduction and Concepts](#Introduction_and_Concepts)
    *   [1.1 NSS and PAM](#NSS_and_PAM)
*   [2 LDAP Server Setup](#LDAP_Server_Setup)
    *   [2.1 Installation](#Installation)
    *   [2.2 Set up access controls](#Set_up_access_controls)
    *   [2.3 Populate LDAP Tree with Base Data](#Populate_LDAP_Tree_with_Base_Data)
    *   [2.4 Adding users](#Adding_users)
*   [3 Client Setup](#Client_Setup)
    *   [3.1 NSS Configuration](#NSS_Configuration)
    *   [3.2 PAM Configuration](#PAM_Configuration)
        *   [3.2.1 Create home folders at login](#Create_home_folders_at_login)
        *   [3.2.2 Enable sudo](#Enable_sudo)
*   [4 Online and Offline Authentication with SSSD](#Online_and_Offline_Authentication_with_SSSD)
    *   [4.1 General Package Details](#General_Package_Details)
    *   [4.2 How to enable SSSD for basic Authentication](#How_to_enable_SSSD_for_basic_Authentication)
        *   [4.2.1 1\. SSSD Configuration](#1._SSSD_Configuration)
        *   [4.2.2 2\. NSCD Configuration](#2._NSCD_Configuration)
        *   [4.2.3 3\. NSS Configuration](#3._NSS_Configuration)
        *   [4.2.4 4\. PAM Configuration](#4._PAM_Configuration)
            *   [4.2.4.1 1\. SUDO Configuration](#1._SUDO_Configuration)
            *   [4.2.4.2 2\. Password Management](#2._Password_Management)
*   [5 Resources](#Resources)

## Introduction and Concepts

This is a guide on how to configure an Arch Linux installation to authenticate against an LDAP directory. This LDAP directory can be either local (installed on the same computer) or network (e.g. in a lab environment where central authentication is desired).

The guide is divided into two parts. The first part deals with how to setup an [OpenLDAP](/index.php/OpenLDAP "OpenLDAP") server that hosts the authentication directory. The second part deals with how to setup the NSS and PAM modules that are required for the authentication scheme to work on the client computers. If you just want to configure Arch to authenticate against an already existing LDAP server, you can skip to the [second part](#Client_Setup).

### NSS and PAM

NSS (which stands for Name Service Switch) is a system mechanism to configure different sources for common configuration databases. For example, `/etc/passwd` is a `file` type source for the `passwd` database.

[PAM](/index.php/PAM "PAM") (which stands for Pluggable Authentication Modules) is a mechanism used by Linux (and most *nixes) to extend its authentication schemes based on different plugins.

So to summarize, we need to configure NSS to use the OpenLDAP server as a source for the `passwd`, `shadow` and other configuration databases and then configure PAM to use these sources to authenticate its users.

## LDAP Server Setup

### Installation

You can read about installation and basic configuration in the [OpenLDAP](/index.php/OpenLDAP "OpenLDAP") article. After you have completed that, return here.

### Set up access controls

To make sure that no-one can read the (encrypted) passwords from the LDAP server, but still allowing users to edit some of their own select attributes (such as own password and photo), add the following to `/etc/openldap/slapd.conf` and restart `slapd.service` afterwards:

**Note:** If you have a different domain name then alter "example" and "org" to your needs
 `slapd.conf` 
```
access to attrs=userPassword,givenName,sn,photo
        by self write
        by anonymous auth
        by dn.base="cn=Manager,dc=example,dc=org" write
        by * none

access to *
        by self read       
        by dn.base="cn=Manager,dc=example,dc=org" write
        by * read
```

### Populate LDAP Tree with Base Data

Create a temporarily file called `base.ldif` with the following text.

 `base.ldif` 
```
# example.org
dn: dc=example,dc=org
dc: example
o: Example Organization
objectClass: dcObject
objectClass: organization

# Manager, example.org
dn: cn=Manager,dc=example,dc=org
cn: Manager
description: LDAP administrator
objectClass: organizationalRole
objectClass: top
roleOccupant: dc=example,dc=org

# People, example.org
dn: ou=People,dc=example,dc=org
ou: People
objectClass: top
objectClass: organizationalUnit

# Groups, example.org
dn: ou=Group,dc=example,dc=org
ou: Group
objectClass: top
objectClass: organizationalUnit

```

Add it to your OpenLDAP Tree:

```
$ ldapadd -D "cn=Manager,dc=example,dc=org" -W -f base.ldif

```

Test to make sure the data was imported:

```
$ ldapsearch -x -b 'dc=example,dc=org' '(objectclass=*)'

```

### Adding users

To manually add a user, create an `.ldif` file like this:

 `user_joe.ldif` 
```
dn: uid=johndoe,ou=People,dc=example,dc=org
objectClass: top
objectClass: person
objectClass: organizationalPerson
objectClass: inetOrgPerson
objectClass: posixAccount
objectClass: shadowAccount
uid: johndoe
cn: John Doe
sn: Doe
givenName: John
title: Guinea Pig
telephoneNumber: +0 000 000 0000
mobile: +0 000 000 0000
postalAddress: AddressLine1$AddressLine2$AddressLine3
userPassword: {CRYPT}xxxxxxxxxx
labeledURI: https://archlinux.org/
loginShell: /bin/bash
uidNumber: 9999
gidNumber: 9999
homeDirectory: /home/johndoe/
description: This is an example user

```

The `xxxxxxxxxx` in the `userPassword` entry should be replaced with the value in `/etc/shadow` or use the `slappasswd` command. Now add the user:

```
$ ldapadd -D "cn=Manager,dc=example,dc=org" -W -f user_joe.ldif

```

**Note:** You can automatically migrate all of your local accounts (and groups, etc.) to the LDAP directory using PADL Software's [Migration Tools](http://www.padl.com/OSS/MigrationTools.html).

## Client Setup

Install the OpenLDAP client as described in [OpenLDAP](/index.php/OpenLDAP "OpenLDAP"). Make sure you can query the server with `ldapsearch`.

Next, [install](/index.php/Install "Install") the [nss-pam-ldapd](https://www.archlinux.org/packages/?name=nss-pam-ldapd) package.

### NSS Configuration

NSS is a system facility which manages different sources as configuration databases. For example, `/etc/passwd` is a `file` type source for the `passwd` database, which stores the user accounts.

Edit `/etc/nsswitch.conf` which is the central configuration file for NSS. It tells NSS which sources to use for which system databases. We need to add the `ldap` directive to the `passwd`, `group` and `shadow` databases, so be sure your file looks like this:

```
passwd: files ldap
group: files ldap
shadow: files ldap

```

Edit `/etc/nslcd.conf` and change the `base` and `uri` lines to fit your ldap server setup.

Start `nslcd.service` using systemd.

You now should see your LDAP users when running `getent passwd` on the client.

### PAM Configuration

The basic rule of thumb for PAM configuration is to include `pam_ldap.so` wherever `pam_unix.so` is included. Arch moving to [pambase](https://www.archlinux.org/packages/?name=pambase) has helped decrease the amount of edits required. For more details about configuring pam, the [RedHat Documentation](https://access.redhat.com/site/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Managing_Smart_Cards/PAM_Configuration_Files.html) is quite good. You might also want the upstream documentation for [nss-pam-ldapd](http://arthurdejong.org/nss-pam-ldapd).

**Tip:** If you want to prevent UID clashes with local users on your system, you might want to include `minimum_uid=10000` or similar on the end of the `pam_ldap.so` lines. You will have to make sure the LDAP server returns uidNumber fields that match the restriction.

**Note:** Each facility (auth, session, password, account) forms a separate chain and the order matters. Sufficient lines will sometimes "short circuit" and skip the rest of the section, so the rule of thumb for *auth*, *password*, and *account* is *sufficient* lines before *required*, but after required lines for the *session* section; *optional* can almost always go at the end. When adding your `pam_ldap.so` lines, do not change the relative order of the other lines without good reason! Simply insert LDAP within the chain.

First edit `/etc/pam.d/system-auth`. This file is included in most of the other files in `pam.d`, so changes here propagate nicely. Updates to [pambase](https://www.archlinux.org/packages/?name=pambase) may change this file.

Make `pam_ldap.so` sufficient at the top of each section, except in the *session* section, where we make it optional.

 `/etc/pam.d/system-auth` 
```
**auth      sufficient pam_ldap.so**
auth      required  pam_unix.so     try_first_pass nullok
auth      optional  pam_permit.so
auth      required  pam_env.so

**account   sufficient pam_ldap.so**
account   required  pam_unix.so
account   optional  pam_permit.so
account   required  pam_time.so

**password  sufficient pam_ldap.so**
password  required  pam_unix.so     try_first_pass nullok sha512 shadow
password  optional  pam_permit.so

session   required  pam_limits.so
session   required  pam_unix.so
**session   optional  pam_ldap.so**
session   optional  pam_permit.so

```

Then edit both `/etc/pam.d/su` and `/etc/pam.d/su-l` identically. The `su-l` file is used when the user runs `su --login`.

Make `pam_ldap.so` sufficient at the top of each section, and add `use_first_pass` to `pam_unix` in the *auth* section.

 `/etc/pam.d/su` 
```
#%PAM-1.0
**auth      sufficient    pam_ldap.so**
auth      sufficient    pam_rootok.so
# Uncomment the following line to implicitly trust users in the "wheel" group.
#auth     sufficient    pam_wheel.so trust use_uid
# Uncomment the following line to require a user to be in the "wheel" group.
#auth     required      pam_wheel.so use_uid
auth      required	pam_unix.so **use_first_pass**
**account   sufficient    pam_ldap.so**
account   required	pam_unix.so
**session   sufficient    pam_ldap.so**
session   required	pam_unix.so

```

To enable users to edit their password, edit `/etc/pam.d/passwd`:

 `/etc/pam.d/passwd` 
```
#%PAM-1.0
**password        sufficient      pam_ldap.so**
#password       required        pam_cracklib.so difok=2 minlen=8 dcredit=2 ocredit=2 retry=3
#password       required        pam_unix.so sha512 shadow use_authtok
password        required        pam_unix.so sha512 shadow nullok
```

#### Create home folders at login

If you want home folders to be created at login (eg: if you are not using NFS to store home folders), edit `/etc/pam.d/system-login` and add `pam_mkhomedir.so` to the *session* section above any "sufficient" items. This will cause home folder creation when logging in at a tty, from ssh, xdm, kdm, gdm, etc. You might choose to edit additional files in the same way, such as `/etc/pam.d/su` and `/etc/pam.d/su-l` to enable it for `su` and `su --login`. If you do not want to do this for ssh logins, edit `system-local-login` instead of `system-login`, etc.

 `/etc/pam.d/system-login` 
```
...top of file not shown...
session    optional   pam_loginuid.so
session    include    system-auth
session    optional   pam_motd.so          motd=/etc/motd
session    optional   pam_mail.so          dir=/var/spool/mail standard quiet
-session   optional   pam_systemd.so
session    required   pam_env.so
**session    required   pam_mkhomedir.so skel=/etc/skel umask=0022**

```
 `/etc/pam.d/su-l` 
```
...top of file not shown...
**session         required        pam_mkhomedir.so skel=/etc/skel umask=0022**
session         sufficient      pam_ldap.so
session         required        pam_unix.so

```

#### Enable sudo

To enable sudo from an LDAP user, edit `/etc/pam.d/sudo`. You will also need to modify sudoers accordingly.

 `/etc/pam.d/sudo` 
```
#%PAM-1.0
**auth      sufficient    pam_ldap.so**
auth      required      pam_unix.so  **try_first_pass**
auth      required      pam_nologin.so

```

You will also need to add in `/etc/openldap/ldap.conf` the following.

 `/etc/openldap/ldap.conf`  `sudoers_base ou=sudoers,dc=AFOLA` 

## Online and Offline Authentication with SSSD

SSSD is a system daemon. Its primary function is to provide access to identity and authentication remote resource through a common framework that can provide caching and offline support to the system. It provides PAM and NSS modules, and in the future will D-BUS based interfaces for extended user information. It provides also a better database to store local users as well as extended user data.

### General Package Details

[Install](/index.php/Install "Install") the [sssd](https://www.archlinux.org/packages/?name=sssd) package.

### How to enable SSSD for basic Authentication

#### 1\. SSSD Configuration

If it does not exist create `/etc/sssd/sssd.conf`.

 `/etc/sssd/sssd.conf` 
```
[sssd]
config_file_version = 2
services = nss, pam
domains = LDAP

[domain/LDAP]
cache_credentials = true

id_provider = ldap
auth_provider = ldap

ldap_uri = ldap://server1.example.org, ldap://server2.example.org
ldap_search_base = dc=example,dc=org
ldap_id_use_start_tls = true
ldap_tls_reqcert = demand
ldap_tls_cacert = /etc/openldap/certs/cacerts.pem
chpass_provider = ldap
ldap_chpass_uri = ldap://server1.example.org
entry_cache_timeout = 600
ldap_network_timeout = 2
ldap_group_member = uniquemember
```

The above is an example only. See [sssd.conf(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/sssd.conf.5) for the full details.

Finally set the file permissions `chmod 600 /etc/sssd/sssd.conf` otherwise sssd will fail to start.

#### 2\. NSCD Configuration

Disable caching for both the passwd and group entries in `/etc/nscd.conf` as it will interfere with sssd caching.

#### 3\. NSS Configuration

Edit `/etc/nsswitch.conf` as follows.

 `/etc/nsswitch.conf` 
```
# Begin /etc/nsswitch.conf

passwd: files **sss**
group: files **sss**
shadow: files **sss**
**sudoers: files sss**

publickey: files

hosts: files dns myhostname
networks: files

protocols: files
services: files
ethers: files
rpc: files

netgroup: files

# End /etc/nsswitch.conf

```

#### 4\. PAM Configuration

The first step is to edit `/etc/pam.d/system-auth` as follows.

 `/etc/pam.d/system-auth` 
```
#%PAM-1.0

**auth sufficient pam_sss.so forward_pass**
auth required pam_unix.so try_first_pass nullok
auth optional pam_permit.so
auth required pam_env.so

**account [default=bad success=ok user_unknown=ignore authinfo_unavail=ignore] pam_sss.so**
account required pam_unix.so
account optional pam_permit.so
account required pam_time.so

**password sufficient pam_sss.so use_authtok**
password required pam_unix.so try_first_pass nullok sha512 shadow
password optional pam_permit.so

**session     required      pam_mkhomedir.so skel=/etc/skel/ umask=0077**
session required pam_limits.so
session required pam_unix.so
**session optional pam_sss.so**
session optional pam_permit.so
```

##### 1\. SUDO Configuration

Edit `/etc/pam.d/sudo` as follows.

 `/etc/pam.d/sudo` 
```
#%PAM-1.0
**auth           sufficient      pam_sss.so**
auth           required        pam_unix.so try_first_pass
auth           required        pam_nologin.so

```

##### 2\. Password Management

In order to enable users to change their passwords using `passwd` edit `/etc/pam.d/passwd` as follows.

 `/etc/pam.d/passwd` 
```
#%PAM-1.0
**password        sufficient      pam_sss.so**
#password       required        pam_cracklib.so difok=2 minlen=8 dcredit=2 ocredit=2 retry=3
#password       required        pam_unix.so sha512 shadow use_authtok
password        required        pam_unix.so sha512 shadow nullok
```

[Start/enable](/index.php/Start/enable "Start/enable") the `sssd.service` systemd unit.

You should now be able to see details of your ldap users with `getent passwd <username>` or `id <username>`.

Once you have logged in with a user the credentials will be cached and you will be able to login using the cached credentials when the ldap server is offline or unavailable.

## Resources

*   [The official page of the nss-pam-ldapd packet](http://arthurdejong.org/nss-pam-ldapd/setup)
*   The PAM and NSS page at the Debian Wiki [1](http://wiki.debian.org/LDAP/NSS) [2](http://wiki.debian.org/LDAP/PAM)
*   [Using LDAP for single authentication](https://www.fatofthelan.com/technical/using-ldap-for-single-authentication/)
*   [Heterogeneous Network Authentication Introduction](http://www.cs.dixie.edu/ldap/)
*   [Discussion on suse's mailing lists about nss-pam-ldapd](http://readlist.com/lists/suse.com/suse-linux-e/36/182642.html)
*   [Fedora's SSSD User Guide](https://docs.fedoraproject.org/en-US/Fedora/15/html/Deployment_Guide/chap-SSSD_User_Guide-Introduction.html)