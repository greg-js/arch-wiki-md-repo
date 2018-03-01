[vsftpd](https://security.appspot.com/vsftpd.html) (*Very Secure FTP Daemon*) is a lightweight, stable and secure FTP server for UNIX-like systems.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Enabling uploading](#Enabling_uploading)
    *   [2.2 Local user login](#Local_user_login)
    *   [2.3 Anonymous login](#Anonymous_login)
    *   [2.4 Chroot jail](#Chroot_jail)
    *   [2.5 Limiting user login](#Limiting_user_login)
    *   [2.6 Limiting connections](#Limiting_connections)
    *   [2.7 Using xinetd](#Using_xinetd)
    *   [2.8 Using SSL/TLS to secure FTP](#Using_SSL.2FTLS_to_secure_FTP)
    *   [2.9 Resolve hostname in passive mode](#Resolve_hostname_in_passive_mode)
    *   [2.10 Port configurations](#Port_configurations)
    *   [2.11 Configuring iptables](#Configuring_iptables)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 PAM with virtual users](#PAM_with_virtual_users)
        *   [3.1.1 Adding private folders for the virtual users](#Adding_private_folders_for_the_virtual_users)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 vsftpd: no connection (Error 500) with recent kernels (3.5 and newer) and .service](#vsftpd:_no_connection_.28Error_500.29_with_recent_kernels_.283.5_and_newer.29_and_.service)
    *   [4.2 vsftpd: refusing to run with writable root inside chroot()](#vsftpd:_refusing_to_run_with_writable_root_inside_chroot.28.29)
    *   [4.3 FileZilla Client: GnuTLS error -8 -15 -110 when connecting via SSL](#FileZilla_Client:_GnuTLS_error_-8_-15_-110_when_connecting_via_SSL)
    *   [4.4 vsftpd.service fails to run on boot](#vsftpd.service_fails_to_run_on_boot)
    *   [4.5 ipv6 only fails with: 500 OOPS: run two copies of vsftpd for IPv4 and IPv6](#ipv6_only_fails_with:_500_OOPS:_run_two_copies_of_vsftpd_for_IPv4_and_IPv6)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") [vsftpd](https://www.archlinux.org/packages/?name=vsftpd) and [start/enable](/index.php/Start/enable "Start/enable") the `vsftpd.service` daemon.

To use [xinetd](https://en.wikipedia.org/wiki/xinetd "wikipedia:xinetd") for monitoring and controlling vsftpd connections, see [#Using xinetd](#Using_xinetd).

## Configuration

Most of the settings in vsftpd are done by editing the file `/etc/vsftpd.conf`. The file itself is well-documented, so this section only highlights some important changes you may want to modify. For all available options and documentation, see the [vsftpd.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/vsftpd.conf.5) man page. Files are served by default from `/srv/ftp`.

Enable connections `/etc/hosts.allow`:

```
# Allow all connections
vsftpd: ALL
# IP address range
vsftpd: 10.0.0.0/255.255.255.0

```

### Enabling uploading

The `WRITE_ENABLE` flag must be set to YES in `/etc/vsftpd.conf` in order to allow changes to the filesystem, such as uploading:

```
write_enable=YES

```

### Local user login

One must set the line `local_enable` in `/etc/vsftpd.conf` to `YES` in order to allow users in `/etc/passwd` to login:

```
local_enable=YES

```

### Anonymous login

These lines controls whether anonymous users can login. By default, anonymous logins are enabled for download only from `/srv/ftp`:

 `/etc/vsftpd.conf` 
```
...
# Allow anonymous FTP? (Beware - allowed by default if you comment this out).
anonymous_enable=YES
...
# Uncomment this to allow the anonymous FTP user to upload files. This only
# has an effect if the above global write enable is activated. Also, you will
# obviously need to create a directory writable by the FTP user.
#anon_upload_enable=YES
#
# Uncomment this if you want the anonymous FTP user to be able to create
# new directories.
#anon_mkdir_write_enable=YES
...
```

You may also add e.g. the following options (see [vsftpd.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/vsftpd.conf.5) for more):

 `/etc/vsftpd.conf` 
```
# No password is required for an anonymous login          
no_anon_password=YES

# Maximum transfer rate for an anonymous client in Bytes/second          
anon_max_rate=30000

# Directory to be used for an anonymous login  
anon_root=/example/directory/
```

### Chroot jail

A chroot environment that prevents the user from leaving its home directory can be set up. To enable this, add the following lines to `/etc/vsftpd.conf`:

```
chroot_list_enable=YES
chroot_list_file=/etc/vsftpd.chroot_list

```

The `chroot_list_file` variable specifies the file which contains users that are jailed.

For a more restricted environment, specify the line:

```
chroot_local_user=YES

```

This will make local users jailed by default. In this case, the file specified by `chroot_list_file` lists users that are **not** in a chroot jail.

### Limiting user login

It's possible to prevent users from logging into the FTP server by adding two lines to `/etc/vsftpd.conf`:

```
userlist_enable=YES
userlist_file=/etc/vsftpd.user_list

```

`userlist_file` now specifies the file which lists users that are not able to login.

If you only want to allow certain users to login, add the line:

```
userlist_deny=NO

```

The file specified by `userlist_file` will now contain users that are able to login.

### Limiting connections

The data transfer rate, i.e. number of clients and connections per IP for local users can be limited by adding the information in `/etc/vsftpd.conf`:

```
local_max_rate=1000000 # Maximum data transfer rate in bytes per second
max_clients=50         # Maximum number of clients that may be connected
max_per_ip=2           # Maximum connections per IP

```

### Using xinetd

Xinetd provides enhanced capabilities for monitoring and controlling connections. It is not necessary though for a basic good working vsftpd-server.

Installation of vsftpd will add a necessary service file, `/etc/xinetd.d/vsftpd`. By default services are disabled. Enable the ftp service:

```
service ftp
{
        socket_type             = stream
        wait                    = no
        user                    = root
        server                  = /usr/bin/vsftpd
        log_on_success  += HOST DURATION
        log_on_failure  += HOST
        disable                 = no
}

```

If you have set the vsftpd daemon to run in standalone mode make the following change in `/etc/vsftpd.conf`:

```
listen=NO

```

Otherwise connection will fail:

```
500 OOPS: could not bind listening IPv4 socket

```

Instead of starting the vsftpd daemon start and [enable](/index.php/Enable "Enable") `xinetd.service`.

### Using SSL/TLS to secure FTP

First, you need a *X.509 SSL/TLS* certificate to use TLS. If you do not have one, you can easily generate a self-signed certificate as follows:

```
# cd /etc/ssl/certs
# openssl req -x509 -nodes -days 7300 -newkey rsa:2048 -keyout vsftpd.pem -out vsftpd.pem
# chmod 600 vsftpd.pem

```

You will be asked questions about your company, etc. As your certificate is not a trusted one, it does not really matter what is filled in, it will just be used for encryption. To use a trusted certificate, you can get one from a certificate authority like [Let's Encrypt](/index.php/Let%27s_Encrypt "Let's Encrypt").

Then, edit the configuration file:

 `/etc/vsftpd.conf` 
```
ssl_enable=YES

# if you accept anonymous connections, you may want to enable this setting
#allow_anon_ssl=NO

# by default all non anonymous logins and forced to use SSL to send and receive password and data, set to NO to allow non secure connections
force_local_logins_ssl=NO
force_local_data_ssl=NO

# TLS v1 protocol connections are preferred and this mode is enabled by default while SSL v2 and v3 are disabled
# the settings below are the default ones and do not need to be changed unless you specifically need SSL
#ssl_tlsv1=YES
#ssl_sslv2=NO
#ssl_sslv3=NO

# provide the path of your certificate and of your private key
# note that both can be contained in the same file or in different files
rsa_cert_file=/etc/ssl/certs/vsftpd.pem
rsa_private_key_file=/etc/ssl/certs/vsftpd.pem

# this setting is set to YES by default and requires all data connections exhibit session reuse which proves they know the secret of the control channel.
# this is more secure but is not supported by many FTP clients, set to NO for better compatibility
require_ssl_reuse=NO
```

### Resolve hostname in passive mode

To override the IP address vsftpd advertises in passive mode by the hostname of your server and have it DNS resolved at startup, add the following two lines in `/etc/vsftpd.conf`:

```
pasv_addr_resolve=YES
pasv_address=*yourdomain.org*

```

**Note:**

*   For dynamic DNS, it is **not** necessary to periodically update *pasv_address* and restart the server as it can sometimes be read.
*   You may not be able to connect in passive mode via LAN anymore, in this case try the active mode instead from the LAN clients.

### Port configurations

It may be necessary to adjust the default FTP listening port and the passive mode data ports:

*   For FTP servers exposed to the web, to reduce the likelihood of the server being attacked, the listening port can be changed to something other than the standard port 21\.
*   To limit the passive mode ports to open ports, a range can be provided.

The ports can be defined in the configuration file as illustrated below:

 `/etc/vsftpd.conf` 
```
listen_port=2211

pasv_min_port=5000
pasv_max_port=5003
```

### Configuring iptables

Often the server running the FTP daemon is protected by an [iptables](/index.php/Iptables "Iptables") firewall. To allow access to the FTP server the corresponding port needs to be opened using something like

```
# iptables -A INPUT -m state --state NEW -m tcp -p tcp --dport 21 -j ACCEPT

```

This article won't provide any instruction on how to set up iptables but here is an example: [Simple stateful firewall](/index.php/Simple_stateful_firewall "Simple stateful firewall").

There are some kernel modules needed for proper FTP connection handling by iptables that should be referenced here. Among those especially *nf_conntrack_ftp*. It is needed as FTP uses the given *listen_port* (21 by default) for commands only; all the data transfer is done over different ports. These ports are chosen by the FTP daemon at random and for each session (also depending on whether active or passive mode is used). To tell iptables that packets on ports should be accepted, *nf_conntrack_ftp* is required. To load it automatically on boot create a new file in `/etc/modules-load.d` e.g.:

```
# echo nf_conntrack_ftp > /etc/modules-load.d/nf_conntrack_ftp.conf

```

If the kernel >= 4.7 you either need to set *net.netfilter.nf_conntrack_helper=1* via *sysctl* e.g.

```
# echo net.netfilter.nf_conntrack_helper=1 > /etc/sysctl.d/70-conntrack.conf

```

or use

```
# iptables -A PREROUTING -t raw -p tcp --dport 21 -j CT --helper ftp

```

## Tips and tricks

### PAM with virtual users

Since [PAM](/index.php/PAM "PAM") no longer provides `pam_userdb.so` another easy method is to use [libpam_pwdfile](https://aur.archlinux.org/packages/libpam_pwdfile/). For environments with many users another option could be [pam_mysql](https://aur.archlinux.org/packages/pam_mysql/). This section is however limited to explain how to configure a chroot environment and authentication by `pam_pwdfile.so`.

In this example we create the directory `vsftpd`:

```
# mkdir /etc/vsftpd

```

One option to create and store user names and passwords is to use the Apache generator htpasswd:

```
# htpasswd -c /etc/vsftpd/.passwd

```

A problem with the above command is that vsftpd might not be able to read the generated MD5 hashed password. If running the same command with the -d switch, crypt() encryption, password become readable by vsftpd, but the downside of this is less security and a password limited to 8 characters. Openssl could be used to produce a MD5 based BSD password with algorithm 1:

```
# openssl passwd -1

```

Whatever solution the produced `/etc/vsftpd/.passwd` should look like this:

```
username1:hashed_password1
username2:hashed_password2
...

```

Next you need to create a PAM service using `pam_pwdfile.so` and the generated `/etc/vsftpd/.passwd` file. In this example we create a PAM policy for *vsftpd* with the following content:

 `/etc/pam.d/vsftpd` 
```
auth required pam_pwdfile.so pwdfile /etc/vsftpd/.passwd
account required pam_permit.so
```

Now it is time to create a home for the virtual users. In the example `/srv/ftp` is decided to host data for virtual users, which also reflects the default directory structure of Arch. First create the general user virtual and make `/srv/ftp` its home:

```
# useradd -d /srv/ftp virtual

```

Make virtual the owner:

```
# chown virtual:virtual /srv/ftp

```

A basic `/etc/vsftpd.conf` with no private folders configured, which will default to the home folder of the virtual user:

```
# pointing to the correct PAM service file
pam_service_name=vsftpd
write_enable=YES
hide_ids=YES
listen=YES
connect_from_port_20=YES
anonymous_enable=NO
local_enable=YES
dirmessage_enable=YES
xferlog_enable=YES
chroot_local_user=YES
guest_enable=YES
guest_username=virtual
virtual_use_local_privs=YES

```

Some parameters might not be necessary for your own setup. If you want the chroot environment to be writable you will need to add the following to the configuration file:

```
allow_writeable_chroot=YES

```

Otherwise vsftpd because of default security settings will complain if it detects that chroot is writable.

[Start](/index.php/Start "Start") `vsftpd.service`.

You should now be able to login from a ftp-client with any of the users and passwords stored in `/etc/vsftpd/.passwd`.

#### Adding private folders for the virtual users

First create directories for users:

```
# mkdir /srv/ftp/user1
# mkdir /srv/ftp/user2
# chown virtual:virtual /srv/ftp/user?/

```

Then, add the following lines to `/etc/vsftpd.conf`:

```
local_root=/srv/ftp/$USER
user_sub_token=$USER

```

## Troubleshooting

### vsftpd: no connection (Error 500) with recent kernels (3.5 and newer) and .service

add this to your /etc/vsftpd.conf

```
seccomp_sandbox=NO

```

### vsftpd: refusing to run with writable root inside chroot()

As of vsftpd 2.3.5, the chroot directory that users are locked to must not be writable. This is in order to prevent a security vulnerabilty.

The safe way to allow upload is to keep chroot enabled, and configure your FTP directories.

```
local_root=/srv/ftp/user

```

```
# mkdir -p /srv/ftp/user/upload
#
# chmod 550 /srv/ftp/user
# chmod 750 /srv/ftp/user/upload

```

If you must:

You can put this into your `/etc/vsftpd.conf` to workaround this security enhancement (since vsftpd 3.0.0; from [Fixing 500 OOPS: vsftpd: refusing to run with writable root inside chroot ()](http://www.benscobie.com/fixing-500-oops-vsftpd-refusing-to-run-with-writable-root-inside-chroot/)):

```
allow_writeable_chroot=YES

```

or alternative:

Install [vsftpd-ext](https://aur.archlinux.org/packages/vsftpd-ext/) and set in the conf file allow_writable_root=YES

### FileZilla Client: GnuTLS error -8 -15 -110 when connecting via SSL

vsftpd tries to display plain-text error messages in the SSL session. In order to debug this, temporarily disable encryption and you will see the correct error message.[[1]](http://ramblings.linkerror.com/?p=45) [[2]](https://serverfault.com/questions/772494/vsftpd-list-causes-gnutls-error-15)

### vsftpd.service fails to run on boot

If you have enabled `vsftpd.service` and it fails to run on boot, make sure it is set to load after `network.target` in the service file:

 `/usr/lib/systemd/system/vsftpd.service` 
```
[Unit]
Description=vsftpd daemon
After=network.target
```

### ipv6 only fails with: 500 OOPS: run two copies of vsftpd for IPv4 and IPv6

you most likely have commented out the line

```
# When "listen" directive is enabled, vsftpd runs in standalone mode and
# listens on IPv4 sockets. This directive cannot be used in conjunction
# with the listen_ipv6 directive.
#listen=YES
#
# This directive enables listening on IPv6 sockets. To listen on IPv4 and IPv6
# sockets, you must run two copies of vsftpd with two configuration files.
# Make sure, that one of the listen options is commented !!
listen_ipv6=YES

```

instead of setting

```
# When "listen" directive is enabled, vsftpd runs in standalone mode and
# listens on IPv4 sockets. This directive cannot be used in conjunction
# with the listen_ipv6 directive.
listen=NO

```

## See also

*   [vsftpd official homepage](http://vsftpd.beasts.org/)
*   [vsftpd.conf man page](http://vsftpd.beasts.org/vsftpd_conf.html)