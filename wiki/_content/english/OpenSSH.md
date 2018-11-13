Related articles

*   [SSH keys](/index.php/SSH_keys "SSH keys")
*   [Pam abl](/index.php/Pam_abl "Pam abl")
*   [fail2ban](/index.php/Fail2ban "Fail2ban")
*   [sshguard](/index.php/Sshguard "Sshguard")
*   [Sshfs](/index.php/Sshfs "Sshfs")
*   [Syslog-ng](/index.php/Syslog-ng "Syslog-ng")
*   [SFTP chroot](/index.php/SFTP_chroot "SFTP chroot")
*   [SCP and SFTP](/index.php/SCP_and_SFTP "SCP and SFTP")

[OpenSSH](https://en.wikipedia.org/wiki/OpenSSH "wikipedia:OpenSSH") (OpenBSD Secure Shell) is a set of computer programs providing encrypted communication sessions over a computer network using the [Secure Shell](https://en.wikipedia.org/wiki/Secure_Shell "wikipedia:Secure Shell") (SSH) protocol. It was created as an open source alternative to the proprietary Secure Shell software suite offered by SSH Communications Security. OpenSSH is developed as part of the OpenBSD project, which is led by Theo de Raadt.

OpenSSH is occasionally confused with the similarly-named OpenSSL; however, the projects have different purposes and are developed by different teams, the similar name is drawn only from similar goals.

An SSH server, by default, listens on the standard TCP port 22\. An SSH client program is typically used for establishing connections to an *sshd* daemon accepting remote connections. Both are commonly present on most modern operating systems, including macOS, GNU/Linux, Solaris and OpenVMS. Proprietary, freeware and open source versions of various levels of complexity and completeness exist.

## Contents

*   [1 Installation](#Installation)
*   [2 Client usage](#Client_usage)
    *   [2.1 Configuration](#Configuration)
*   [3 Server usage](#Server_usage)
    *   [3.1 Configuration](#Configuration_2)
    *   [3.2 Daemon management](#Daemon_management)
    *   [3.3 Protection](#Protection)
        *   [3.3.1 Force public key authentication](#Force_public_key_authentication)
        *   [3.3.2 Two-factor authentication and public keys](#Two-factor_authentication_and_public_keys)
        *   [3.3.3 Protecting against brute force attacks](#Protecting_against_brute_force_attacks)
            *   [3.3.3.1 Using ufw](#Using_ufw)
            *   [3.3.3.2 Using iptables](#Using_iptables)
            *   [3.3.3.3 Anti-brute-force tools](#Anti-brute-force_tools)
        *   [3.3.4 Limit root login](#Limit_root_login)
            *   [3.3.4.1 Deny](#Deny)
            *   [3.3.4.2 Restrict](#Restrict)
        *   [3.3.5 Securing the authorized_keys file](#Securing_the_authorized_keys_file)
*   [4 Other SSH clients and servers](#Other_SSH_clients_and_servers)
    *   [4.1 Dropbear](#Dropbear)
    *   [4.2 Mosh](#Mosh)
*   [5 Tips and tricks](#Tips_and_tricks)
    *   [5.1 Encrypted SOCKS tunnel](#Encrypted_SOCKS_tunnel)
        *   [5.1.1 Step 1: start the connection](#Step_1:_start_the_connection)
        *   [5.1.2 Step 2: configure your browser (or other programs)](#Step_2:_configure_your_browser_(or_other_programs))
    *   [5.2 X11 forwarding](#X11_forwarding)
        *   [5.2.1 Setup](#Setup)
        *   [5.2.2 Usage](#Usage)
    *   [5.3 Forwarding other ports](#Forwarding_other_ports)
    *   [5.4 Jump hosts](#Jump_hosts)
    *   [5.5 Reverse SSH through a relay](#Reverse_SSH_through_a_relay)
    *   [5.6 Multiplexing](#Multiplexing)
    *   [5.7 Speeding up SSH](#Speeding_up_SSH)
    *   [5.8 Mounting a remote filesystem with SSHFS](#Mounting_a_remote_filesystem_with_SSHFS)
    *   [5.9 Keep alive](#Keep_alive)
    *   [5.10 Automatically restart SSH tunnels with systemd](#Automatically_restart_SSH_tunnels_with_systemd)
    *   [5.11 Autossh - automatically restarts SSH sessions and tunnels](#Autossh_-_automatically_restarts_SSH_sessions_and_tunnels)
        *   [5.11.1 Run autossh automatically at boot via systemd](#Run_autossh_automatically_at_boot_via_systemd)
    *   [5.12 Alternative service should SSH daemon fail](#Alternative_service_should_SSH_daemon_fail)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 Checklist](#Checklist)
    *   [6.2 Connection refused or timeout problem](#Connection_refused_or_timeout_problem)
        *   [6.2.1 Port forwarding](#Port_forwarding)
        *   [6.2.2 Is SSH running and listening?](#Is_SSH_running_and_listening?)
        *   [6.2.3 Are there firewall rules blocking the connection?](#Are_there_firewall_rules_blocking_the_connection?)
        *   [6.2.4 Is the traffic even getting to your computer?](#Is_the_traffic_even_getting_to_your_computer?)
        *   [6.2.5 Your ISP or a third party blocking default port?](#Your_ISP_or_a_third_party_blocking_default_port?)
            *   [6.2.5.1 Diagnosis](#Diagnosis)
            *   [6.2.5.2 Possible solution](#Possible_solution)
        *   [6.2.6 Read from socket failed: connection reset by peer](#Read_from_socket_failed:_connection_reset_by_peer)
    *   [6.3 "[your shell]: No such file or directory" / ssh_exchange_identification problem](#"[your_shell]:_No_such_file_or_directory"_/_ssh_exchange_identification_problem)
    *   [6.4 "Terminal unknown" or "Error opening terminal" error message](#"Terminal_unknown"_or_"Error_opening_terminal"_error_message)
        *   [6.4.1 TERM hack](#TERM_hack)
    *   [6.5 Connection closed by x.x.x.x [preauth]](#Connection_closed_by_x.x.x.x_[preauth])
    *   [6.6 id_dsa refused by OpenSSH 7.0](#id_dsa_refused_by_OpenSSH_7.0)
    *   [6.7 No matching key exchange method found by OpenSSH 7.0](#No_matching_key_exchange_method_found_by_OpenSSH_7.0)
    *   [6.8 tmux/screen session killed when disconnecting from SSH](#tmux/screen_session_killed_when_disconnecting_from_SSH)
    *   [6.9 SSH session stops responding](#SSH_session_stops_responding)
    *   [6.10 Broken pipe](#Broken_pipe)
*   [7 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [openssh](https://www.archlinux.org/packages/?name=openssh) package.

## Client usage

To connect to a server, run:

```
$ ssh -p *port* *user*@*server-address*

```

If the server only allows public-key authentication, follow [SSH keys](/index.php/SSH_keys "SSH keys").

### Configuration

The client can be configured to store common options and hosts. All options can be declared globally or restricted to specific hosts. For example:

 `~/.ssh/config` 
```
# global options
User *user*

# host-specific options
Host *myserver*
    HostName *server-address*
    Port     *port*

```

With such a configuration, the following commands are equivalent

```
$ ssh -p *port* *user*@*server-address*
$ ssh *myserver*

```

See [ssh_config(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ssh_config.5) for more information.

Some options do not have command line switch equivalents, but you can specify config options on the command line with `-o`. For example `-oKexAlgorithms=+diffie-hellman-group1-sha1`.

## Server usage

### Configuration

The SSH daemon configuration file can be found and edited in `/etc/ssh/ssh**d**_config`.

To allow access only for some users add this line:

```
AllowUsers    *user1 user2*

```

To allow access only for some groups:

```
AllowGroups   *group1 group2*

```

To add a nice welcome message (e.g. from the `/etc/issue` file), configure the `Banner` option:

```
Banner /etc/issue

```

Public and private host keys are automatically generated in `/etc/ssh` by the *sshd* [service files](#Daemon_management) on the first run after installation. Four key pairs are provided based on the algorithms [dsa, rsa, ecdsa and ed25519](/index.php/SSH_keys#Choosing_the_authentication_key_type "SSH keys"). To have sshd use a particular key, specify the following option:

```
HostKey /etc/ssh/ssh_host_rsa_key

```

If the server is to be exposed to the WAN, it is recommended to change the default port from 22 to a random higher one like this:

```
Port 39901

```

**Tip:**

*   To help select an alternative port that is not already assigned to a common service, review the [list of TCP and UDP port numbers](https://en.wikipedia.org/wiki/List_of_TCP_and_UDP_port_numbers "wikipedia:List of TCP and UDP port numbers"). You can also find port information locally in `/etc/services`. A port change from default port 22 will reduce the number of log entries caused by automated authentication attempts but will not eliminate them. See [Port knocking](/index.php/Port_knocking "Port knocking") for related information.
*   It is recommended to disable password logins entirely. This will greatly increase security, see [#Force public key authentication](#Force_public_key_authentication) for more information. See [#Protection](#Protection) for more recommend security methods.
*   OpenSSH can listen to multiple ports simply by having multiple `Port *port_number*` lines in the config file.

### Daemon management

[openssh](https://www.archlinux.org/packages/?name=openssh) comes with two kinds of [systemd](/index.php/Systemd "Systemd") service files:

1.  `sshd.service`, which will keep the SSH daemon permanently active and fork for each incoming connection.[[1]](https://projects.archlinux.org/svntogit/packages.git/tree/trunk/sshd.service?h=packages/openssh#n16) It is especially suitable for systems with a large amount of SSH traffic.[[2]](https://projects.archlinux.org/svntogit/packages.git/tree/trunk/sshd.service?h=packages/openssh&id=4cadf5dff444e4b7265f8918652f4e6dff733812#n15)
2.  `sshd.socket` + `sshd@.service`, which spawn on-demand instances of the SSH daemon per connection. Using it implies that *systemd* listens on the SSH socket and will only start the daemon process for an incoming connection. It is the recommended way to run `sshd` in almost all cases.[[3]](https://projects.archlinux.org/svntogit/packages.git/tree/trunk/sshd.service?h=packages/openssh&id=4cadf5dff444e4b7265f8918652f4e6dff733812#n18)[[4]](http://lists.freedesktop.org/archives/systemd-devel/2011-January/001107.html)[[5]](http://0pointer.de/blog/projects/inetd.html)

You can [start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") either `sshd.service` **or** `sshd.socket` to begin using the daemon.

If using the socket service, you will need to [edit](/index.php/Edit "Edit") the unit file if you want it to listen on a port other than the default 22:

 `# systemctl edit sshd.socket` 
```
[Socket]
ListenStream=
ListenStream=12345

```

**Warning:** Using `sshd.socket` negates the `ListenAddress` setting, so it will allow connections over any address. To achieve the effect of setting `ListenAddress`, you must specify the port *and* IP for `ListenStream` (e.g. `ListenStream=192.168.1.100:22`). You must also add `FreeBind=true` under `[Socket]` or else setting the IP address will have the same drawback as setting `ListenAddress`: the socket will fail to start if the network is not up in time.

**Tip:** When using socket activation a transient instance of `sshd@.service` will be started for each connection (with different instance names). Therefore, neither `sshd.socket` nor the daemon's regular `sshd.service` allow to monitor connection attempts in the log. The logs of socket-activated instances of SSH can be seen with `journalctl -u "sshd@*"` or with `journalctl /usr/bin/sshd`.

### Protection

Allowing remote log-on through SSH is good for administrative purposes, but can pose a threat to your server's security. Often the target of brute force attacks, SSH access needs to be limited properly to prevent third parties gaining access to your server.

Several other good guides are available on the topic, for example:

*   [Article by Mozilla Infosec Team](https://wiki.mozilla.org/Security/Guidelines/OpenSSH "mozillawiki:Security/Guidelines/OpenSSH")
*   [Secure sshd](https://stribika.github.io/2015/01/04/secure-secure-shell.html)

#### Force public key authentication

If a client cannot authenticate through a public key, by default the SSH server falls back to password authentication, thus allowing a malicious user to attempt to gain access by [brute-forcing](#Protecting_against_brute_force_attacks) the password. One of the most effective ways to protect against this attack is to disable password logins entirely, and force the use of [SSH keys](/index.php/SSH_keys "SSH keys"). This can be accomplished by disabling the following options in the daemon configuration file:

 `/etc/ssh/sshd_config`  `PasswordAuthentication no` 
**Warning:** Before adding this to your configuration, make sure that all accounts which require SSH access have public-key authentication set up in the corresponding `authorized_keys` files. See [SSH keys#Copying the public key to the remote server](/index.php/SSH_keys#Copying_the_public_key_to_the_remote_server "SSH keys") for more information.

#### Two-factor authentication and public keys

SSH can be set up to require multiple ways of authentication, you can tell which authentication methods are required using the `AuthenticationMethods` option. This enables you to use public keys as well as a two-factor authorization.

See [Google Authenticator](/index.php/Google_Authenticator "Google Authenticator") to set up Google Authenticator.

To use [PAM](/index.php/PAM "PAM") with OpenSSH, edit the following files:

 `/etc/ssh/sshd_config` 
```
ChallengeResponseAuthentication yes
AuthenticationMethods publickey keyboard-interactive:pam

```

Then you can log in with either a publickey **or** the user authentication as required by your PAM setup.

If, on the other hand, you want to authenticate the user on both a publickey **and** the user authentication as required by your PAM setup, use a comma instead of a space to separate the AuthenticationMethods:

 `/etc/ssh/sshd_config` 
```
ChallengeResponseAuthentication yes
AuthenticationMethods publickey**,**keyboard-interactive:pam

```

With required pubkey **and** pam authentication you may wish to disable the password requirement:

 `/etc/pam.d/sshd` 
```
auth      required  pam_securetty.so     #disable remote root
#Require google authenticator
auth      required  pam_google_authenticator.so
#But not password
#auth      include   system-remote-login
account   include   system-remote-login
password  include   system-remote-login
session   include   system-remote-login

```

#### Protecting against brute force attacks

Brute forcing is a simple concept: One continuously tries to log in to a webpage or server log-in prompt like SSH with a high number of random username and password combinations.

##### Using ufw

See [ufw#Rate limiting with ufw](/index.php/Ufw#Rate_limiting_with_ufw "Ufw").

##### Using iptables

If you are already using iptables you can easily protect SSH against brute force attacks by using the following rules.

**Note:** In this example the SSH port was changed to port 42660 TCP.

Before the following rules can be used we create a new rule chain to log and drop too many connection attempts:

```
# iptables -N LOG_AND_DROP

```

The first rule will be applied to packets that signal the start of new connections headed for TCP port 42660

```
# iptables -A INPUT -p tcp -m tcp --dport 42660 -m state --state NEW -m recent --set --name DEFAULT --rsource

```

The next rule tells iptables to look for packets that match the previous rule's parameters, and which also come from hosts already added to the watch list.

```
# iptables -A INPUT -p tcp -m tcp --dport 42660 -m state --state NEW -m recent --update --seconds 90 --hitcount 4 --name DEFAULT --rsource -j LOG_AND_DROP

```

Now iptables decides what to do with TCP traffic to port 42660 which does not match the previous rule.

```
# iptables -A INPUT -p tcp -m tcp --dport 42660 -j ACCEPT

```

We are appending this rule to the LOG_AND_DROP table, and we use the -j (jump) operator to pass the packet's information to the logging facility

```
# iptables -A LOG_AND_DROP -j LOG --log-prefix "iptables deny: " --log-level 7

```

After they are logged by the first rule, all packets are then dropped

```
# iptables -A LOG_AND_DROP -j DROP

```

##### Anti-brute-force tools

You can protect yourself from brute force attacks by using an automated script that blocks anybody trying to brute force their way in, for example [fail2ban](/index.php/Fail2ban "Fail2ban") or [sshguard](/index.php/Sshguard "Sshguard").

*   Only allow incoming SSH connections from trusted locations
*   Use [fail2ban](/index.php/Fail2ban "Fail2ban") or [sshguard](/index.php/Sshguard "Sshguard") to automatically block IP addresses that fail password authentication too many times.
*   Use [pam_shield](https://github.com/jtniehof/pam_shield) to block IP addresses that perform too many login attempts within a certain period of time. In contrast to [fail2ban](/index.php/Fail2ban "Fail2ban") or [sshguard](/index.php/Sshguard "Sshguard"), this program does not take login success or failure into account.

#### Limit root login

It is generally considered bad practice to allow the root user to log in without restraint over SSH. There are two methods by which SSH root access can be restricted for increased security.

##### Deny

Sudo selectively provides root rights for actions requiring these without requiring authenticating against the root account. This allows locking the root account against access via SSH and potentially functions as a security measure against brute force attacks, since now an attacker must guess the account name in addition to the password.

SSH can be configured to deny remote logins with the root user by editing the "Authentication" section in the daemon configuration file. Simply set `PermitRootLogin` to `no`:

 `/etc/ssh/sshd_config`  `PermitRootLogin no` 

Next, [restart](/index.php/Restart "Restart") the SSH daemon.

You will now be unable to log in through SSH under root, but will still be able to log in with your normal user and use [su](/index.php/Su "Su") or [sudo](/index.php/Sudo "Sudo") to do system administration.

##### Restrict

Some automated tasks such as remote, full-system backup require full root access. To allow these in a secure way, instead of disabling root login via SSH, it is possible to only allow root logins for selected commands. This can be achieved by editing `~root/.ssh/authorized_keys`, by prefixing the desired key, e.g. as follows:

```
command="/usr/lib/rsync/rrsync -ro /" ssh-rsa …

```

This will allow any login with this specific key only to execute the command specified between the quotes.

The increased attack surface created by exposing the root user name at login can be compensated by adding the following to `sshd_config`:

```
PermitRootLogin forced-commands-only

```

This setting will not only restrict the commands which root may execute via SSH, but it will also disable the use of passwords, forcing use of public key authentication for the root account.

A slightly less restrictive alternative will allow any command for root, but makes brute force attacks infeasible by enforcing public key authentication. For this option, set:

```
PermitRootLogin prohibit-password

```

#### Securing the authorized_keys file

For additional protection, you can prevent users from adding new public keys and connecting from them.

In the server, make the `authorized_keys` file read-only for the user and deny all other permissions:

```
$ chmod 400 ~/.ssh/authorized_keys

```

To keep the user from simply changing the permissions back, [set the immutable bit](/index.php/File_permissions_and_attributes#chattr_and_lsattr "File permissions and attributes") on the `authorized_keys` file. After that the user could rename the `~/.ssh` directory to something else and create a new `~/.ssh` directory and `authorized_keys` file. To prevent this, set the immutable bit on the `~/.ssh` directory too.

**Note:** If you find yourself needing to add a new key, you will first have to remove the immutable bit from `authorized_keys` and make it writable. Follow the steps above to secure it again.

## Other SSH clients and servers

Apart from OpenSSH, there are many SSH [clients](https://en.wikipedia.org/wiki/Comparison_of_SSH_clients "wikipedia:Comparison of SSH clients") and [servers](https://en.wikipedia.org/wiki/Comparison_of_SSH_servers "wikipedia:Comparison of SSH servers") available.

### Dropbear

[Dropbear](https://en.wikipedia.org/wiki/Dropbear_(software) is a SSH-2 client and server. [dropbear](https://www.archlinux.org/packages/?name=dropbear) is available in the [official repositories](/index.php/Official_repositories "Official repositories").

The command-line ssh client is named dbclient.

### Mosh

From the Mosh [website](http://mosh.mit.edu/):

	Remote terminal application that allows roaming, supports intermittent connectivity, and provides intelligent local echo and line editing of user keystrokes. Mosh is a replacement for SSH. It is more robust and responsive, especially over slow connections such as Wi-Fi, cellular, and long-distance.

[Install](/index.php/Install "Install") the [mosh](https://www.archlinux.org/packages/?name=mosh) package, or [mosh-git](https://aur.archlinux.org/packages/mosh-git/) for the latest revision.

Mosh has an undocumented command line option `--predict=experimental` which produces more aggressive echoing of local keystrokes. Users interested in low-latency visual confirmation of keyboard input may prefer this prediction mode.

**Note:** Mosh by design does not let you access session history, consider installing a terminal multiplexer such as [tmux](/index.php/Tmux "Tmux") or [GNU Screen](/index.php/GNU_Screen "GNU Screen").

## Tips and tricks

### Encrypted SOCKS tunnel

This is highly useful for laptop users connected to various unsafe wireless connections. The only thing you need is an SSH server running at a somewhat secure location, like your home or at work. It might be useful to use a dynamic DNS service like [DynDNS](http://www.dyndns.org/) so you do not have to remember your IP-address.

#### Step 1: start the connection

You only have to execute this single command to start the connection:

```
$ ssh -TND 4711 *user*@*host*

```

where `*user*` is your username at the SSH server running at the `*host*`. It will ask for your password, and then you are connected. The `N` flag disables the interactive prompt, and the `D` flag specifies the local port on which to listen on (you can choose any port number if you want). The `T` flag disables pseudo-tty allocation.

It is nice to add the verbose (`-v`) flag, because then you can verify that it is actually connected from that output.

#### Step 2: configure your browser (or other programs)

The above step is useful only in combination with a web browser or another program that uses this newly created SOCKS tunnel. Since SSH currently supports both SOCKS4 and SOCKS5, you can use either of them.

*   For Firefox: *Preferences > General > Network Proxy > Manual proxy*, and enter `localhost` in the *SOCKS host* text field, and the port number in the next text field (`4711` in the example above).

Firefox does not automatically make DNS requests through the socks tunnel. This potential privacy concern can be mitigated by the following steps:

1.  Type `about:config` into the Firefox location bar
2.  Set `network.proxy.socks_remote_dns` to `true`
3.  Restart Firefox

*   For Chromium: You can set the SOCKS settings as environment variables or as command line options. I recommend to add one of the following functions to your `.bashrc`:

```
function secure_chromium {
    port=4711
    export SOCKS_SERVER=localhost:$port
    export SOCKS_VERSION=5
    chromium &
    exit
}

```

OR

```
function secure_chromium {
    port=4711
    chromium --proxy-server="socks://localhost:$port" &
    exit
}

```

Now open a terminal and just do:

```
$ secure_chromium

```

Enjoy your secure tunnel!

### X11 forwarding

X11 forwarding is a mechanism that allows graphical interfaces of X11 programs running on a remote system to be displayed on a local client machine. For X11 forwarding the remote host does not need to have a full X11 system installed, however it needs at least to have *xauth* installed. *xauth* is a utility that maintains `Xauthority` configurations used by server and client for authentication of X11 session ([source](http://xmodulo.com/2012/11/how-to-enable-x11-forwarding-using-ssh.html)).

**Warning:** X11 forwarding has important security implications which should be at least acknowledged by reading relevant sections of [ssh(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ssh.1), [sshd_config(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sshd_config.5), and [ssh_config(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ssh_config.5) manual pages. See also [this StackExchange question.](https://security.stackexchange.com/questions/14815/security-concerns-with-x11-forwarding)

#### Setup

On the remote system:

*   [install](/index.php/Install "Install") the [xorg-xauth](https://www.archlinux.org/packages/?name=xorg-xauth) and [xorg-xhost](https://www.archlinux.org/packages/?name=xorg-xhost) packages
*   in `/etc/ssh/ssh**d**_config`:
    *   verify that `AllowTcpForwarding` and `X11UseLocalhost` options are set to *yes*, and that `X11DisplayOffset` is set to *10* (those are the default values if nothing has been changed, see [sshd_config(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sshd_config.5))
    *   set `X11Forwarding` to *yes*
*   then [restart](/index.php/Restart "Restart") the [*sshd* daemon](#Daemon_management).

On the client side, enable the `ForwardX11` option by either specifying the `-X` switch on the command line for opportunistic connections, or by setting `ForwardX11` to *yes* in the [client's configuration](#Configuration).

**Tip:** You can enable the `ForwardX11Trusted` option (`-Y` switch on the command line) if GUI is drawing badly or you receive errors; this will prevent X11 forwardings from being subjected to the [X11 SECURITY extension](http://www.x.org/wiki/Development/Documentation/Security/) controls. Be sure you have read [the warning](#X11_forwarding) at the beginning of this section if you do so.

#### Usage

Log on to the remote machine normally, specifying the `-X` switch if *ForwardX11* was not enabled in the client's configuration file:

```
$ ssh -X *user@host*

```

If you receive errors trying to run graphical applications, try *ForwardX11Trusted* instead:

```
$ ssh -Y *user@host*

```

You can now start any X program on the remote server, the output will be forwarded to your local session:

```
$ xclock

```

If you get "Cannot open display" errors try the following command as the non root user:

```
$ xhost +

```

The above command will allow anybody to forward X11 applications. To restrict forwarding to a particular host type:

```
$ xhost +hostname

```

where hostname is the name of the particular host you want to forward to. See [xhost(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xhost.1) for more details.

Be careful with some applications as they check for a running instance on the local machine. [Firefox](/index.php/Firefox "Firefox") is an example: either close the running Firefox instance or use the following start parameter to start a remote instance on the local machine:

```
$ firefox --no-remote

```

If you get "X11 forwarding request failed on channel 0" when you connect (and the server `/var/log/errors.log` shows "Failed to allocate internet-domain X11 display socket"), make sure package [xorg-xauth](https://www.archlinux.org/packages/?name=xorg-xauth) is installed. If its installation is not working, try to either:

*   enable the `AddressFamily any` option in `ssh**d**_config` on the *server*, or
*   set the `AddressFamily` option in `ssh**d**_config` on the *server* to inet.

Setting it to inet may fix problems with Ubuntu clients on IPv4.

For running X applications as other user on the SSH server you need to `xauth add` the authentication line taken from `xauth list` of the SSH logged in user.

**Tip:** [Here](http://unix.stackexchange.com/a/12772/29867) are [some](http://unix.stackexchange.com/a/46748/29867) useful [links](http://superuser.com/a/805060/185665) for troubleshooting `X11 Forwarding` issues.

### Forwarding other ports

In addition to SSH's built-in support for X11, it can also be used to securely tunnel any TCP connection, by use of local forwarding or remote forwarding.

Local forwarding opens a port on the local machine, connections to which will be forwarded to the remote host and from there on to a given destination. Very often, the forwarding destination will be the same as the remote host, thus providing a secure shell and, e.g. a secure VNC connection, to the same machine. Local forwarding is accomplished by means of the `-L` switch and it is accompanying forwarding specification in the form of `<tunnel port>:<destination address>:<destination port>`.

Thus:

```
$ ssh -L 1000:mail.google.com:25 192.168.0.100

```

will use SSH to login to and open a shell on `192.168.0.100`, and will also create a tunnel from the local machine's TCP port 1000 to mail.google.com on port 25\. Once established, connections to `localhost:1000` will connect to the Gmail SMTP port. To Google, it will appear that any such connection (though not necessarily the data conveyed over the connection) originated from `192.168.0.100`, and such data will be secure between the local machine and 192.168.0.100, but not between `192.168.0.100` and Google, unless other measures are taken.

Similarly:

```
$ ssh -L 2000:192.168.0.100:6001 192.168.0.100

```

will allow connections to `localhost:2000` which will be transparently sent to the remote host on port 6001\. The preceding example is useful for VNC connections using the vncserver utility--part of the tightvnc package--which, though very useful, is explicit about its lack of security.

Remote forwarding allows the remote host to connect to an arbitrary host via the SSH tunnel and the local machine, providing a functional reversal of local forwarding, and is useful for situations where, e.g., the remote host has limited connectivity due to firewalling. It is enabled with the `-R` switch and a forwarding specification in the form of `<tunnel port>:<destination address>:<destination port>`.

Thus:

```
$ ssh -R 3000:irc.freenode.net:6667 192.168.0.200

```

will bring up a shell on `192.168.0.200`, and connections from `192.168.0.200` to itself on port 3000 (the remote host's `localhost:3000`) will be sent over the tunnel to the local machine and then on to irc.freenode.net on port 6667, thus, in this example, allowing the use of IRC programs on the remote host to be used, even if port 6667 would normally be blocked to it.

Both local and remote forwarding can be used to provide a secure "gateway", allowing other computers to take advantage of an SSH tunnel, without actually running SSH or the SSH daemon by providing a bind-address for the start of the tunnel as part of the forwarding specification, e.g. `<tunnel address>:<tunnel port>:<destination address>:<destination port>`. The `<tunnel address>` can be any address on the machine at the start of the tunnel. The address `localhost` allows connections via the `localhost` or loopback interface, and an empty address or `*` allow connections via any interface. By default, forwarding is limited to connections from the machine at the "beginning" of the tunnel, i.e. the `<tunnel address>` is set to `localhost`. Local forwarding requires no additional configuration, however remote forwarding is limited by the remote server's SSH daemon configuration. See the `GatewayPorts` option in [sshd_config(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sshd_config.5) and `-L address` option in [ssh(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ssh.1) for more information about remote forwarding and local forwarding, respectively.

### Jump hosts

In certain scenarios, there might not be a direct connection to your target SSH daemon, and the use of a jump server (or bastion server) is required. Thus, we attempt to connect together two or more SSH tunnels, and assuming your local keys are authorized against each server in the chain. This is possible using SSH agent forwarding (`-A`) and pseudo-terminal allocation (`-t`) which forwards your local key with the following syntax:

```
$ ssh -A -t -l user1 bastion1 \
  ssh -A -t -l user2 intermediate2 \
  ssh -A -t -l user3 target

```

An easier way to do this is using the `-J` flag:

```
$ ssh -J user1@bastion1,user2@intermediate2 user3@target

```

Multiple hosts in the `-J` directive can be separted with a comma, they will be connected to in the order listed. The `user...@` part is not required, but can be used. The host specifications for `-J` use the ssh configuration file, so specific per-host options can be set there, if needed.

### Reverse SSH through a relay

The idea is that client connects to the server via another relay, while the server is connected to the same relay using a reverse SSH tunnel. This is for example useful when the server is behind a NAT and relay is a publicly accessible SSH server used as a proxy to which the user has access. So the prerequisite is that client's keys are authorized against both the relay and the server and server's need to be authorized against the relay as well for the reverse SSH connection.

The following configuration example assumes that user1 is the user account used on client, user2 on relay and user3 on server. First the server needs to establish the reverse tunnel with:

```
ssh -R 2222:localhost:22 -N user2@relay

```

Which can also be automated with a startup script, systemd service or [autossh](https://www.archlinux.org/packages/?name=autossh).

At the client side the connection is established with:

```
ssh user2@relay ssh user3@localhost -p 2222

```

The remote command to establish the connection to reverse tunnel can also be defined in relay's `~/.ssh/authorized_keys` by including the `command` field as follows:

```
command="ssh user3@localhost -p 2222" ssh-rsa KEY2 user1@client

```

In this case the connection is established with:

```
ssh user2@relay

```

Note that SCP's autocomplete function in client's terminal is not working and even the SCP transfers themselves are not working under some configurations.

### Multiplexing

The SSH daemon usually listens on port 22\. However, it is common practice for many public internet hotspots to block all traffic that is not on the regular HTTP/S ports (80 and 443, respectively), thus effectively blocking SSH connections. The immediate solution for this is to have `sshd` listen additionally on one of the whitelisted ports:

 `/etc/ssh/sshd_config` 
```
Port 22
Port 443

```

However, it is likely that port 443 is already in use by a web server serving HTTPS content, in which case it is possible to use a multiplexer, such as [sslh](https://www.archlinux.org/packages/?name=sslh), which listens on the multiplexed port and can intelligently forward packets to many services.

### Speeding up SSH

There are several [client configuration](#Configuration) options which can speed up connections either globally or for specific hosts. See [ssh_config(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ssh_config.5) for full descriptions of these options.

*   You can make all sessions to the same host share a single connection using these options:
    ```
    ControlMaster auto
    ControlPersist yes
    ControlPath ~/.ssh/sockets/socket-%r@%h:%p

    ```

	where `~/.ssh/sockets` can be any directory not writable by other users.

*   `ControlPersist` specifies how long the master should wait in the background for new clients after the initial client connection has been closed. Possible values are either:
    *   `no` to close the connection immediately after the last client disconnects,
    *   a time in seconds,
    *   `yes` to wait forever, the connection will never be closed automatically.

*   Compression can increase speed on slow connections, it is enabled with the `Compression yes` option or the `-C` flag. However the compression algorithm used is the relatively slow [gzip(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/gzip.1) which becomes the bottleneck on fast networks. In order to speed up the connection one should use the `Compression no` option on local or fast networks.

*   Login time can be shortened by bypassing IPv6 lookup using the `AddressFamily inet` option or `-4` flag.

*   Last, if you intend to use SSH for SFTP or SCP, [High Performance SSH/SCP](https://www.psc.edu/index.php/hpn-ssh) can significantly increase throughput by raising dynamically the SSH buffer sizes. Install the package [openssh-hpn-git](https://aur.archlinux.org/packages/openssh-hpn-git/) to use a patched version of OpenSSH with this enhancement.

### Mounting a remote filesystem with SSHFS

Please refer to the [SSHFS](/index.php/SSHFS "SSHFS") article to mount a SSH-accessible remote system to a local folder, so you will be able to do any operation on the mounted files with any tool (copy, rename, edit with vim, etc.). *sshfs* is generally preferred over *shfs*, the latter has not been updated since 2004.

**Tip:** There is a package [autosshfs-git](https://aur.archlinux.org/packages/autosshfs-git/) that can be used to run autosshfs automatically at login.

### Keep alive

By default, the SSH session automatically logs out if it has been idle for a certain time. To keep the session up, the client can send a keep-alive signal to the server if no data has been received for some time, or symmetrically the server can send messages at regular intervals if it has not heard from the client.

*   On the **server** side, `ClientAliveInterval` sets the timeout in seconds after which if no data has been received from the client, *sshd* will send a request for response. The default is 0, no message is sent. For example to request a response every 60 seconds from the client, set the `ClientAliveInterval 60` option in your [server configuration](#Configuration_2). See also the `ClientAliveCountMax` and `TCPKeepAlive` options.
*   On the **client** side, `ServerAliveInterval` controls the interval between the requests for response sent from the client to the server. For example to request a response every 120 seconds from the server, add the `ServerAliveInterval 120` option to your [client configuration](#Configuration). See also the `ServerAliveCountMax` and `TCPKeepAlive` options.

**Note:** To ensure a session is kept alive, only one of either the client or the server needs to send keep alive requests. If ones control both the servers and the clients, a reasonable choice is to only configure the clients that require a persistent session with a positive `ServerAliveInterval` and leave other clients and servers in their default configuration.

### Automatically restart SSH tunnels with systemd

[systemd](/index.php/Systemd "Systemd") can automatically start SSH connections on boot/login *and* restart them when they fail. This makes it a useful tool for maintaining SSH tunnels.

The following service can start an SSH tunnel on login using the connection settings in your [ssh configuration](#Configuration). If the connection closes for any reason, it waits 10 seconds before restarting it:

 `~/.config/systemd/user/tunnel.service` 
```
[Unit]
Description=SSH tunnel to myserver

[Service]
Type=simple
Restart=always
RestartSec=10
ExecStart=/usr/bin/ssh -F %h/.ssh/config -N myserver

```

Then [enable](/index.php/Enable "Enable") and [start](/index.php/Start "Start") the user service. See [#Keep alive](#Keep_alive) for how to prevent the tunnel from timing out. If you wish to start the tunnel on boot, you will need to rewrite the unit as a system service.

### Autossh - automatically restarts SSH sessions and tunnels

When a session or tunnel cannot be kept alive, for example due to bad network conditions causing client disconnections, you can use [autossh](https://www.archlinux.org/packages/?name=autossh) to automatically restart them.

Usage examples:

```
$ autossh -M 0 -o "ServerAliveInterval 45" -o "ServerAliveCountMax 2" username@example.com

```

Combined with [SSHFS](/index.php/SSHFS "SSHFS"):

```
$ sshfs -o reconnect,compression=yes,transform_symlinks,ServerAliveInterval=45,ServerAliveCountMax=2,ssh_command='autossh -M 0' username@example.com: /mnt/example 

```

Connecting through a SOCKS-proxy set by [Proxy settings](/index.php/Proxy_settings "Proxy settings"):

```
$ autossh -M 0 -o "ServerAliveInterval 45" -o "ServerAliveCountMax 2" -NCD 8080 username@example.com 

```

With the `-f` option autossh can be made to run as a background process. Running it this way however means the passphrase cannot be entered interactively.

The session will end once you type `exit` in the session, or the autossh process receives a SIGTERM, SIGINT of SIGKILL signal.

#### Run autossh automatically at boot via systemd

If you want to automatically start autossh, you can create a systemd unit file:

 `/etc/systemd/system/autossh.service` 
```
[Unit]
Description=AutoSSH service for port 2222
After=network.target

[Service]
Environment="AUTOSSH_GATETIME=0"
ExecStart=/usr/bin/autossh -M 0 -NL 2222:localhost:2222 -o TCPKeepAlive=yes foo@bar.com

[Install]
WantedBy=multi-user.target
```

Here `AUTOSSH_GATETIME=0` is an environment variable specifying how long ssh must be up before autossh considers it a successful connection, setting it to 0 autossh also ignores the first run failure of ssh. This may be useful when running autossh at boot. Other environment variables are available on the manpage. Of course, you can make this unit more complex if necessary (see the systemd documentation for details), and obviously you can use your own options for autossh, but note that the `-f` implying `AUTOSSH_GATETIME=0` does not work with systemd.

Remember to [start](/index.php/Start "Start") and/or [enable](/index.php/Enable "Enable") the service afterwards.

You may also need to disable ControlMaster e.g.

```
ExecStart=/usr/bin/autossh -M 0 -o ControlMaster=no -NL 2222:localhost:2222 -o TCPKeepAlive=yes foo@bar.com

```

**Tip:** It is also easy to maintain several autossh processes, to keep several tunnels alive. Just create multiple service files with different names.

### Alternative service should SSH daemon fail

For remote or headless servers which rely exclusively on SSH, a failure to start the SSH daemon (e.g., after a system upgrade) may prevent administration access. [systemd](/index.php/Systemd "Systemd") offers a simple solution via `OnFailure` option.

Let us suppose the server runs `sshd` and [telnet](/index.php/Telnet "Telnet") is the fail-safe alternative of choice. Create a file as follows. Do **not** [enable](/index.php/Enable "Enable") telnet.socket!

 `/etc/systemd/system/sshd.service.d/override.conf` 
```
[Unit]
OnFailure=telnet.socket
```

That's it. Telnet is not available when `sshd` is running. Should `sshd` fail to start, a telnet session can be opened for recovery.

## Troubleshooting

### Checklist

Check these simple issues before you look any further.

1.  The config directory `~/.ssh` and its contents should be accessible only by your user (check this on both the client and the server):
    ```
    $ chmod 700 ~/.ssh
    $ chmod 600 ~/.ssh/*
    $ chown -R $USER ~/.ssh

    ```

2.  Check that the client's public key (e.g. `id_rsa.pub`) is in `~/.ssh/authorized_keys` on the server.
3.  Check that you did not limit SSH access with `AllowUsers` or `AllowGroups` in the [server config](#Configuration_2).
4.  Check if the user has set a password. Sometimes new users who have not yet logged in to the server do not have a password.
5.  [Append](/index.php/Append "Append") `LogLevel DEBUG` to `/etc/ssh/sshd_config`.
6.  Use `journalctl -xe` for possible (error) messages.
7.  [Restart](/index.php/Restart "Restart") `sshd` and logout/login on both client and server.

### Connection refused or timeout problem

#### Port forwarding

If you are behind a NAT mode/router (which is likely unless you are on a VPS or publicly addressed host), make sure that your router is forwarding incoming ssh connections to your machine. Find the server's internal IP address with `$ ip addr` and set up your router to forward TCP on your SSH port to that IP. [portforward.com](http://portforward.com) can help with that.

#### Is SSH running and listening?

The [ss](/index.php/Ss "Ss") utility shows all the processes listening to a TCP port with the following command line:

```
$ ss --tcp --listening

```

If the above command do not show the system is listening to the port `ssh`, then SSH is NOT running: check `/var/log/messages` for errors etc.

#### Are there firewall rules blocking the connection?

[Iptables](/index.php/Iptables "Iptables") may be blocking connections on port `22`. Check this with:

 `# iptables -nvL` 

and look for rules that might be dropping packets on the `INPUT` chain. Then, if necessary, unblock the port with a command like:

```
# iptables -I INPUT 1 -p tcp --dport 22 -j ACCEPT

```

For more help configuring firewalls, see [firewalls](/index.php/Firewalls "Firewalls").

#### Is the traffic even getting to your computer?

Start a traffic dump on the computer you are having problems with:

```
# tcpdump -lnn -i any port ssh and tcp-syn

```

This should show some basic information, then wait for any matching traffic to happen before displaying it. Try your connection now. If you do not see any output when you attempt to connect, then something outside of your computer is blocking the traffic (e. g., hardware firewall, NAT router etc.).

#### Your ISP or a third party blocking default port?

**Note:** Try this step if you **know** you are not running any firewalls and you know you have configured the router for DMZ or have forwarded the port to your computer and it still does not work. Here you will find diagnostic steps and a possible solution.

In some cases, your ISP might block the default port (SSH port 22) so whatever you try (opening ports, hardening the stack, defending against flood attacks, et al) ends up useless. To confirm this, create a server on all interfaces (0.0.0.0) and connect remotely.

If you get an error message comparable to this:

```
ssh: connect to host www.inet.hr port 22: Connection refused

```

That means the port is **not** being blocked by the ISP, but the server does not run SSH on that port (See [security through obscurity](https://en.wikipedia.org/wiki/Security_through_obscurity "wikipedia:Security through obscurity")).

However, if you get an error message comparable to this:

```
ssh: connect to host 111.222.333.444 port 22: Operation timed out 

```

That means that something is rejecting your TCP traffic on port 22\. Basically that port is stealth, either by your firewall or 3rd party intervention (like an ISP blocking and/or rejecting incoming traffic on port 22). If you know you are not running any firewall on your computer, and you know that Gremlins are not growing in your routers and switches, then your ISP is blocking the traffic.

To double check, you can run Wireshark on your server and listen to traffic on port 22\. Since Wireshark is a Layer 2 Packet Sniffing utility, and TCP/UDP are Layer 3 and above (see [IP Network stack](https://en.wikipedia.org/wiki/Internet_protocol_suite "wikipedia:Internet protocol suite")), if you do not receive anything while connecting remotely, a third party is most likely to be blocking the traffic on that port to your server.

##### Diagnosis

[Install](/index.php/Install "Install") either [tcpdump](https://www.archlinux.org/packages/?name=tcpdump) or Wireshark with the [wireshark-cli](https://www.archlinux.org/packages/?name=wireshark-cli) package.

For tcpdump:

```
# tcpdump -ni *interface* "port 22"

```

For Wireshark:

```
$ tshark -f "tcp port 22" -i *interface*

```

where `*interface*` is the network interface for a WAN connection (see `ip a` to check). If you are not receiving any packets while trying to connect remotely, you can be very sure that your ISP is blocking the incoming traffic on port 22.

##### Possible solution

The solution is just to use some other port that the ISP is not blocking. Open the `/etc/ssh/sshd_config` and configure the file to use different ports. For example, add:

```
Port 22
Port 1234

```

Also make sure that other "Port" configuration lines in the file are commented out. Just commenting "Port 22" and putting "Port 1234" will not solve the issue because then sshd will only listen on port 1234\. Use both lines to run the SSH server on both ports.

[Restart](/index.php/Restart "Restart") the server `sshd.service` and you are almost done. You still have to configure your client(s) to use the other port instead of the default port. There are numerous solutions to that problem, but let us cover two of them here.

#### Read from socket failed: connection reset by peer

Recent versions of openssh sometimes fail with the above error message when connecting to older ssh servers. This can be worked around by setting various [client options](#Configuration) for that host. See [ssh_config(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ssh_config.5) for more information about the following options.

The problem could be the `ecdsa-sha2-nistp*-cert-v01@openssh` elliptical host key algorithms. These can be disabled by setting `HostKeyAlgorithms` to a list excluding those algorithms.

If that does not work, it could be that the list of ciphers is too long. Set the `Ciphers` option to a shorter list (fewer than 80 characters should be enough). Similarly, you can also try shortening the list of `MACs`.

See also the [discussion](http://www.gossamer-threads.com/lists/openssh/dev/51339) on the openssh bug forum.

### "[your shell]: No such file or directory" / ssh_exchange_identification problem

One possible cause for this is the need of certain SSH clients to find an absolute path (one returned by `whereis -b [your shell]`, for instance) in `$SHELL`, even if the shell's binary is located in one of the `$PATH` entries.

### "Terminal unknown" or "Error opening terminal" error message

If you receive the above errors upon logging in, this means the server does not recognize your terminal. Ncurses applications like nano may fail with the message "Error opening terminal".

The correct solution is to install the client terminal's terminfo file on the server. This tells console programs on the server how to correctly interact with your terminal. You can get info about current terminfo using `$ infocmp` and then find out [which package owns it](/index.php/Pacman#Querying_package_databases "Pacman").

If you cannot [install](/index.php/Install "Install") it normally, you can copy your terminfo to your home directory on the server:

```
$ ssh myserver mkdir -p  ~/.terminfo/${TERM:0:1}
$ scp /usr/share/terminfo/${TERM:0:1}/$TERM myserver:~/.terminfo/${TERM:0:1}/

```

After logging in and out from the server the problem should be fixed.

#### TERM hack

**Note:** This should only be used as a last resort.

Alternatively, you can simply set `TERM=xterm` in your environment on the server (e.g. in `.bash_profile`). This will silence the error and allow ncurses applications to run again, but you may experience strange behavior and graphical glitches unless your terminal's control sequences exactly match xterm's.

### Connection closed by x.x.x.x [preauth]

If you are seeing this error in your sshd logs, make sure you have set a valid HostKey

```
HostKey /etc/ssh/ssh_host_rsa_key

```

### id_dsa refused by OpenSSH 7.0

OpenSSH 7.0 deprecated DSA public keys for security reasons. If you absolutely must enable them, set the [config](#Configuration) option `PubkeyAcceptedKeyTypes +ssh-dss` ([http://www.openssh.com/legacy.html](http://www.openssh.com/legacy.html) does not mention this).

### No matching key exchange method found by OpenSSH 7.0

OpenSSH 7.0 deprecated the diffie-hellman-group1-sha1 key algorithm because it is weak and within theoretical range of the so-called Logjam attack (see [http://www.openssh.com/legacy.html](http://www.openssh.com/legacy.html)). If the key algorithm is needed for a particular host, ssh will produce an error message like this:

```
Unable to negotiate with 127.0.0.1: no matching key exchange method found.
Their offer: diffie-hellman-group1-sha1

```

The best resolution for these failures is to upgrade/configure the server to not use deprecated algorithms. If that is not possible, you can force the client to reenable the algorithm with the [client option](#Configuration) `KexAlgorithms +diffie-hellman-group1-sha1`.

### tmux/screen session killed when disconnecting from SSH

If your processes get killed at the end of the session, it is possible that you are using socket activation and it gets killed by [systemd](https://www.archlinux.org/packages/?name=systemd) when it notices that the SSH session process exited. In that case there are two solutions. One is to avoid using socket activation by using `ssh.service` instead of `ssh.socket`. The other is to set `KillMode=process` in the Service section of `ssh@.service`.

The `KillMode=process` setting may also be useful with the classic `ssh.service`, as it avoids killing the SSH session process or the [screen](https://www.archlinux.org/packages/?name=screen) or [tmux](https://www.archlinux.org/packages/?name=tmux) processes when the server gets stopped or restarted.

### SSH session stops responding

SSH responds to [flow control commands](https://en.wikipedia.org/wiki/Software_flow_control "wikipedia:Software flow control") `XON` and `XOFF`. It will freeze/hang/stop responding when you hit `Ctrl+s`. Use `Ctrl+q` to resume your session.

### Broken pipe

If you attempt to create a connection which results in a `Broken pipe` response for `packet_write_wait`, you should reattempt the connection in debug mode and see if the output ends in error:

```
debug3: send packet: type 1
packet_write_wait: Connection to A.B.C.D port 22: Broken pipe
```

The `send packet` line above indicates that the reply packet was never received. So, it follows that this is a *QoS* issue. To decrease the likely-hood of a packet being dropped, set `IPQoS`:

 `/etc/ssh/ssh_config` 
```
Host *
    IPQoS reliability
```

The `reliability` (`0x04`) type-of-service should resolve the issue, as well as `0x00` and `throughput` (`0x08`).

## See also

*   [Defending against brute force ssh attacks](http://www.la-samhna.de/library/brutessh.html)
*   [OpenSSH key management, Part 1](http://www.ibm.com/developerworks/library/l-keyc/index.html) and [Part 2](http://www.ibm.com/developerworks/library/l-keyc2) on IBM developerWorks
*   [Secure Secure Shell](https://stribika.github.io/2015/01/04/secure-secure-shell.html)