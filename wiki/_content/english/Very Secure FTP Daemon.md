**vsftpd** (Very Secure FTP Daemon) is a lightweight, stable and secure FTP server for UNIX-like systems.

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
    *   [2.8 Using SSL to Secure FTP](#Using_SSL_to_Secure_FTP)
    *   [2.9 Dynamic DNS](#Dynamic_DNS)
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

[Install](/index.php/Install "Install") [vsftpd](https://www.archlinux.org/packages/?name=vsftpd).

[Start/Enable](/index.php/Systemd#Using_units "Systemd") the `vsftpd.service` daemon.

See the [#Using xinetd](#Using_xinetd) for procedures to use vsftpd with xinetd.

## Configuration

Most of the settings in vsftpd are done by editing the file `/etc/vsftpd.conf`. The file itself is well-documented, so this section only highlights some important changes you may want to modify. For all available options and documentation, see the man page for vsftpd.conf (5), or [view it online](https://security.appspot.com/vsftpd/vsftpd_conf.html). Files are served by default from `/srv/ftp`.

### Enabling uploading

The `WRITE_ENABLE` flag must be set to YES in `/etc/vsftpd.conf` in order to allow changes to the filesystem, such as uploading:

```
write_enable=YES

```

### Local user login

One must set the line to `/etc/vsftpd.conf` to allow users in `/etc/passwd` to login:

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

You may also add e.g. the following options (see `[man](/index.php/Man "Man") vsftp.conf` for more):

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

### Using SSL to Secure FTP

Generate an SSL Cert, e.g. like that:

```
# cd /etc/ssl/certs
# openssl req -x509 -nodes -days 7300 -newkey rsa:2048 -keyout /etc/ssl/certs/vsftpd.pem -out /etc/ssl/certs/vsftpd.pem
# chmod 600 /etc/ssl/certs/vsftpd.pem

```

You will be asked a lot of Questions about your Company etc., as your Certificate is not a trusted one it doesn't really matter what you fill in. You will use this for encryption! If you plan to use this in a matter of trust get one from a CA like thawte, verisign etc.

edit your configuration `/etc/vsftpd.conf`

```
#this is important
ssl_enable=YES

#choose what you like, if you accept anon-connections
# you may want to enable this
# allow_anon_ssl=NO

#choose what you like,
# it's a matter of performance i guess
# force_local_data_ssl=NO

#choose what you like
force_local_logins_ssl=YES

#you should at least enable this if you enable ssl...
ssl_tlsv1=YES
#choose what you like
ssl_sslv2=YES
#choose what you like
ssl_sslv3=YES
#give the correct path to your currently generated *.pem file
rsa_cert_file=/etc/ssl/certs/vsftpd.pem
#the *.pem file contains both the key and cert
rsa_private_key_file=/etc/ssl/certs/vsftpd.pem

```

### Dynamic DNS

Make sure you put the following two lines in `/etc/vsftpd.conf`:

```
pasv_addr_resolve=YES
pasv_address=yourdomain.noip.info

```

It is **not** necessary to use a script that updates pasv_address periodically and restarts the server, as it can be found elsewhere!

**Note:** You won't be able to connect in passive mode via LAN anymore. Try the active mode on your LAN PC's FTP client.

### Port configurations

Especially for private FTP servers that are exposed to the web it's recommended to change the listening port to something other than the standard port 21\. This can be done using the following lines in `/etc/vsftpd.conf`:

```
listen_port=2211

```

Furthermore a custom passive port range can be given by:

```
pasv_min_port=49152
pasv_max_port=65534

```

### Configuring iptables

Often the server running the FTP daemon is protected by an [iptables](/index.php/Iptables "Iptables") firewall. To allow access to the FTP server the corresponding port needs to be opened using something like

```
# iptables -A INPUT -m state --state NEW -m tcp -p tcp --dport 2211 -j ACCEPT

```

This article won't provide any instruction on how to set up iptables but here is an example: [Simple stateful firewall](/index.php/Simple_stateful_firewall "Simple stateful firewall").

There are some kernel modules needed for proper FTP connection handling by iptables that should be referenced here. Among those especially *ip_conntrack_ftp*. It is needed as FTP uses the given *listen_port* (21 by default) for commands only; all the data transfer is done over different ports. These ports are chosen by the FTP daemon at random and for each session (also depending on whether active or passive mode is used). To tell iptables that packets on ports should be accepted, *ip_conntrack_ftp* is required. To load it automatically on boot create a new file in `/etc/modules-load.d` e.g.:

```
# echo nf_conntrack_ftp > /etc/modules-load.d/nf_conntrack_ftp.conf

```

If you changed the *listen_port* you also need to configure the conntrack module accordingly:

 `/etc/modprobe.d/ip_conntrack_ftp.conf` 
```
options nf_conntrack_ftp ports=2211

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

If you have enabled the vsftpd service and it fails to run on boot, make sure it is set to load after network.target in the service file:

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