# Secure Shell

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [SSH keys](/index.php/SSH_keys "SSH keys")
*   [Pam abl](/index.php/Pam_abl "Pam abl")
*   [fail2ban](/index.php/Fail2ban "Fail2ban")
*   [sshguard](/index.php/Sshguard "Sshguard")
*   [Sshfs](/index.php/Sshfs "Sshfs")
*   [Syslog-ng](/index.php/Syslog-ng "Syslog-ng")
*   [SFTP chroot](/index.php/SFTP_chroot "SFTP chroot")

Secure Shell (SSH) is a network protocol that allows data to be exchanged over a secure channel between two computers. Encryption provides confidentiality and integrity of data. SSH uses public-key cryptography to authenticate the remote computer and allow the remote computer to authenticate the user, if necessary.

SSH is typically used to log into a remote machine and execute commands, but it also supports tunneling, forwarding arbitrary TCP ports and X11 connections; file transfer can be accomplished using the associated SFTP or SCP protocols.

An SSH server, by default, listens on the standard TCP port 22\. An SSH client program is typically used for establishing connections to an _sshd_ daemon accepting remote connections. Both are commonly present on most modern operating systems, including Mac OS X, GNU/Linux, Solaris and OpenVMS. Proprietary, freeware and open source versions of various levels of complexity and completeness exist.

## Contents

*   [1 OpenSSH](#OpenSSH)
    *   [1.1 Installation](#Installation)
    *   [1.2 Client usage](#Client_usage)
    *   [1.3 Server usage](#Server_usage)
        *   [1.3.1 Configuration](#Configuration)
        *   [1.3.2 Daemon management](#Daemon_management)
        *   [1.3.3 Protection](#Protection)
            *   [1.3.3.1 Force public key authentication](#Force_public_key_authentication)
            *   [1.3.3.2 Two-factor authentication and public keys](#Two-factor_authentication_and_public_keys)
            *   [1.3.3.3 Protecting against brute force attacks](#Protecting_against_brute_force_attacks)
                *   [1.3.3.3.1 Using Iptabels](#Using_Iptabels)
                *   [1.3.3.3.2 Anti-Brute-Force Tools](#Anti-Brute-Force_Tools)
            *   [1.3.3.4 Limit root login](#Limit_root_login)
                *   [1.3.3.4.1 Deny](#Deny)
                *   [1.3.3.4.2 Restrict](#Restrict)
            *   [1.3.3.5 Securing the authorized_keys file](#Securing_the_authorized_keys_file)
*   [2 Other SSH clients and servers](#Other_SSH_clients_and_servers)
    *   [2.1 Dropbear](#Dropbear)
    *   [2.2 Mosh: Mobile Shell](#Mosh:_Mobile_Shell)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Encrypted SOCKS tunnel](#Encrypted_SOCKS_tunnel)
        *   [3.1.1 Step 1: start the connection](#Step_1:_start_the_connection)
        *   [3.1.2 Step 2: configure your browser (or other programs)](#Step_2:_configure_your_browser_.28or_other_programs.29)
    *   [3.2 X11 forwarding](#X11_forwarding)
        *   [3.2.1 Setup](#Setup)
        *   [3.2.2 Usage](#Usage)
    *   [3.3 Forwarding other ports](#Forwarding_other_ports)
    *   [3.4 Multiplexing](#Multiplexing)
    *   [3.5 Speeding up SSH](#Speeding_up_SSH)
    *   [3.6 Mounting a remote filesystem with SSHFS](#Mounting_a_remote_filesystem_with_SSHFS)
    *   [3.7 Keep alive](#Keep_alive)
    *   [3.8 Saving connection data in ssh config](#Saving_connection_data_in_ssh_config)
    *   [3.9 Automatically restart SSH tunnels with systemd](#Automatically_restart_SSH_tunnels_with_systemd)
    *   [3.10 Autossh - automatically restarts SSH sessions and tunnels](#Autossh_-_automatically_restarts_SSH_sessions_and_tunnels)
        *   [3.10.1 Run Autossh automatically at boot via systemd](#Run_Autossh_automatically_at_boot_via_systemd)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Checklist](#Checklist)
        *   [4.1.1 Verify SSH settings](#Verify_SSH_settings)
        *   [4.1.2 Restart SSH + Relogin Users](#Restart_SSH_.2B_Relogin_Users)
        *   [4.1.3 Cleanup outdated keys (optional)](#Cleanup_outdated_keys_.28optional.29)
        *   [4.1.4 Recommendations](#Recommendations)
    *   [4.2 SSH connection left hanging after poweroff/reboot](#SSH_connection_left_hanging_after_poweroff.2Freboot)
    *   [4.3 Connection refused or timeout problem](#Connection_refused_or_timeout_problem)
        *   [4.3.1 Is your router doing port forwarding?](#Is_your_router_doing_port_forwarding.3F)
        *   [4.3.2 Is SSH running and listening?](#Is_SSH_running_and_listening.3F)
        *   [4.3.3 Are there firewall rules blocking the connection?](#Are_there_firewall_rules_blocking_the_connection.3F)
        *   [4.3.4 Is the traffic even getting to your computer?](#Is_the_traffic_even_getting_to_your_computer.3F)
        *   [4.3.5 Your ISP or a third party blocking default port?](#Your_ISP_or_a_third_party_blocking_default_port.3F)
            *   [4.3.5.1 Diagnosis](#Diagnosis)
            *   [4.3.5.2 Possible solution](#Possible_solution)
        *   [4.3.6 Read from socket failed: connection reset by peer](#Read_from_socket_failed:_connection_reset_by_peer)
    *   [4.4 "[your shell]: No such file or directory" / ssh_exchange_identification problem](#.22.5Byour_shell.5D:_No_such_file_or_directory.22_.2F_ssh_exchange_identification_problem)
    *   [4.5 "Terminal unknown" or "Error opening terminal" error message](#.22Terminal_unknown.22_or_.22Error_opening_terminal.22_error_message)
        *   [4.5.1 Workaround by setting the $TERM variable](#Workaround_by_setting_the_.24TERM_variable)
        *   [4.5.2 Solution using terminfo file](#Solution_using_terminfo_file)
    *   [4.6 Connection closed by x.x.x.x [preauth]](#Connection_closed_by_x.x.x.x_.5Bpreauth.5D)
    *   [4.7 id_dsa refused by OpenSSH 7.0](#id_dsa_refused_by_OpenSSH_7.0)
    *   [4.8 no matching key exchange method found by OpenSSH 7.0](#no_matching_key_exchange_method_found_by_OpenSSH_7.0)
*   [5 See also](#See_also)

## OpenSSH

OpenSSH (OpenBSD Secure Shell) is a set of computer programs providing encrypted communication sessions over a computer network using the ssh protocol. It was created as an open source alternative to the proprietary Secure Shell software suite offered by SSH Communications Security. OpenSSH is developed as part of the OpenBSD project, which is led by Theo de Raadt.

OpenSSH is occasionally confused with the similarly-named OpenSSL; however, the projects have different purposes and are developed by different teams, the similar name is drawn only from similar goals.

### Installation

[Install](/index.php/Install "Install") the [openssh](https://www.archlinux.org/packages/?name=openssh) package.

### Client usage

To connect to a server, run:

```
$ ssh -p port user@server-address

```

If the server only allows public-key authentication, follow [SSH keys](/index.php/SSH_keys "SSH keys").

### Server usage

#### Configuration

The SSH daemon configuration file can be found and edited in `/etc/ssh/ssh**d**_config`.

To allow access only for some users add this line:

```
AllowUsers    user1 user2

```

To allow access only for some groups:

```
AllowGroups   group1 group2

```

To disable root login over SSH, change the PermitRootLogin line into this:

```
PermitRootLogin no

```

**Note:** `PermitRootLogin prohibit-password` is the default since version 7.0p1\. See `man sshd_config`.

To add a nice welcome message (e.g. from the `/etc/issue` file), configure the `Banner` option:

```
Banner /etc/issue

```

Host keys will be generated automatically by the sshd Systemd service. If you want sshd to use a particular key which you have provided, you can configure it manually:

```
HostKey /etc/ssh/ssh_host_rsa_key

```

If the server is to be exposed to the WAN, it is recommended to change the default port from 22 to a random higher one like this:

```
Port 39901

```

For a discussion, see [security through obscurity](https://en.wikipedia.org/wiki/Security_through_obscurity "wikipedia:Security through obscurity"). Even though the port ssh is running on could be detected by using a port-scanner like [nmap](https://www.archlinux.org/packages/?name=nmap), changing it will reduce the number of log entries caused by automated authentication attempts. To help select a port review the [list of TCP and UDP port numbers](https://en.wikipedia.org/wiki/List_of_TCP_and_UDP_port_numbers "wikipedia:List of TCP and UDP port numbers"). You can also find port information locally in `/etc/services`. Select an alternative port that is **not** already assigned to a common service to prevent conflicts.

**Note:** OpenSSH can also listen on multiple ports simply by having multiple **Port x** lines in the config file.

It is also recommended to disable password logins entirely. This will greatly increase security, see [#Disabling password logins](#Disabling_password_logins) for more information.

#### Daemon management

[openssh](https://www.archlinux.org/packages/?name=openssh) comes with two kinds of [systemd](/index.php/Systemd "Systemd") service files:

1.  `sshd.service`, which will keep the SSH daemon permanently active and fork for each incoming connection.[[1]](https://projects.archlinux.org/svntogit/packages.git/tree/trunk/sshd.service?h=packages/openssh#n16) It is especially suitable for systems with a large amount of SSH traffic.[[2]](https://projects.archlinux.org/svntogit/packages.git/tree/trunk/sshd.service?h=packages/openssh&id=4cadf5dff444e4b7265f8918652f4e6dff733812#n15)
2.  `sshd.socket` + `sshd@.service`, which spawn on-demand instances of the SSH daemon per connection. Using it implies that _systemd_ listens on the SSH socket and will only start the daemon process for an incoming connection. It is the recommended way to run `sshd` in almost all cases.[[3]](https://projects.archlinux.org/svntogit/packages.git/tree/trunk/sshd.service?h=packages/openssh&id=4cadf5dff444e4b7265f8918652f4e6dff733812#n18)[[4]](http://lists.freedesktop.org/archives/systemd-devel/2011-January/001107.html)[[5]](http://0pointer.de/blog/projects/inetd.html)

You can [start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") either `sshd.service` **or** `sshd.socket` to begin using the daemon.

If using the socket service, you will need to [edit](/index.php/Systemd#Editing_provided_units "Systemd") the unit file if you want it to listen on a port other than the default 22:

 `# systemctl edit sshd.socket` 

```
[Socket]
ListenStream=
ListenStream=12345

```

**Warning:** Using `sshd.socket` negates the `ListenAddress` setting, so it will allow connections over any address. To achieve the effect of setting `ListenAddress`, you must specify the port _and_ IP for `ListenStream` (e.g. `ListenStream=192.168.1.100:22`). You must also add `FreeBind=true` under `[Socket]` or else setting the IP address will have the same drawback as setting `ListenAddress`: the socket will fail to start if the network is not up in time.

**Tip:** When using socket activation neither `sshd.socket` nor the daemon's regular `sshd.service` allow to monitor connection attempts in the log, but executing `# journalctl /usr/bin/sshd` does.

#### Protection

Allowing remote log-on through SSH is good for administrative purposes, but can pose a threat to your server's security. Often the target of brute force attacks, SSH access needs to be limited properly to prevent third parties gaining access to your server.

Several other good guides are available on the topic, for example:

*   [Article by Mozilla Infosec Team](https://wiki.mozilla.org/Security/Guidelines/OpenSSH)
*   [Secure sshd](https://stribika.github.io/2015/01/04/secure-secure-shell.html)

##### Force public key authentication

If a client cannot authenticate through a public key, by default the SSH server falls back to password authentication, thus allowing a malicious user to attempt to gain access by [brute-forcing](#Protecting_against_brute_force_attacks) the password. One of the most effective ways to protect against this attack is to disable password logins entirely, and force the use of [SSH keys](/index.php/SSH_keys "SSH keys"). This can be accomplished by disabling the following options in `sshd_config`:

```
PasswordAuthentication no
ChallengeResponseAuthentication no

```

**Warning:** Before adding this to your configuration, make sure that all accounts which require SSH access have public-key authentication set up in the corresponding `authorized_keys` files. See [SSH keys#Copying the public key to the remote server](/index.php/SSH_keys#Copying_the_public_key_to_the_remote_server "SSH keys") for more information.

##### Two-factor authentication and public keys

Since OpenSSH 6.2, you can add your own chain to authenticate with using the `AuthenticationMethods` option. This enables you to use public keys as well as a two-factor authorization.

See [Google Authenticator](/index.php/Google_Authenticator "Google Authenticator") to set up Google Authenticator.

To use PAM with OpenSSH, edit the following files:

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
AuthenticationMethods publickey,keyboard-interactive:pam

```

##### Protecting against brute force attacks

Brute forcing is a simple concept: One continuously tries to log in to a webpage or server log-in prompt like SSH with a high number of random username and password combinations.

###### Using Iptabels

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**This article or section is a candidate for merging with [Simple_stateful_firewall#Bruteforce_attacks](/index.php/Simple_stateful_firewall#Bruteforce_attacks "Simple stateful firewall").**

**Notes:** Out of scope, same technique as already described in the SSF. (Discuss in [Talk:Secure Shell#](https://wiki.archlinux.org/index.php/Talk:Secure_Shell))

If you are already using iptables you can easily protect SSH against brute force attacks by using the following rules.

**Note:** In this example the SSH port was changed to port 42660 TCP.

Before the following rules can be used we create a new rule chain to log and drop to many connection attempts:

```
$IPT -N LOG_AND_DROP

```

The first rule will be applied to packets that signal the start of new connections headed for TCP port 42660

```
iptables -A INPUT -p tcp -m tcp --dport 42660 -m state --state NEW -m recent --set --name DEFAULT --rsource

```

The next rule tells iptables to look for packets that match the previous rule's parameters, and which also come from hosts already added to the watch list.

```
iptables -A INPUT -p tcp -m tcp --dport 42660 -m state --state NEW -m recent --update --seconds 90 --hitcount 4 --name DEFAULT --rsource -j LOG_AND_DROP

```

Now iptables decides what to do with TCP traffic to port 42660 which does not match the previous rule.

```
iptables -A INPUT -p tcp -m tcp --dport 42660 -j ACCEPT

```

We are appending this rule to the LOG_AND_DROP table, and we use the -j (jump) operator to pass the packet's information to the logging facility

```
iptables -A LOG_AND_DROP -j LOG --log-prefix "iptables deny: " --log-level 7

```

After they are logged by the first rule, all packets are then dropped

```
iptables -A LOG_AND_DROP -j DROP

```

###### Anti-Brute-Force Tools

You can protect yourself from brute force attacks by using an automated script that blocks anybody trying to brute force their way in, for example [fail2ban](/index.php/Fail2ban "Fail2ban") or [sshguard](/index.php/Sshguard "Sshguard").

*   Only allow incoming SSH connections from trusted locations
*   Use [fail2ban](/index.php/Fail2ban "Fail2ban") or [sshguard](/index.php/Sshguard "Sshguard") to automatically block IP addresses that fail password authentication too many times.
*   Use [pam_shield](https://github.com/jtniehof/pam_shield) to block IP addresses that perform too many login attempts within a certain period of time. In contrast to [fail2ban](/index.php/Fail2ban "Fail2ban") or [sshguard](/index.php/Sshguard "Sshguard"), this program does not take login success or failure into account.

##### Limit root login

It is generally considered bad practice to allow the root user to log in without restraint over SSH. There are two methods by which SSH root access can be restricted for increased security.

###### Deny

Sudo selectively provides root rights for actions requiring these without requiring authenticating against the root account. This allows locking the root account against access via SSH and potentially functions as a security measure against brute force attacks, since now an attacker must guess the account name in addition to the password.

SSH can be configured to deny remote logins with the root user by editing the "Authentication" section in `/etc/ssh/sshd_config`. Simply change `#PermitRootLogin yes` to `no` and uncomment the line:

 `/etc/ssh/sshd_config` 

```
PermitRootLogin no
...

```

Next, [restart](/index.php/Restart "Restart") the SSH daemon.

You will now be unable to log in through SSH under root, but will still be able to log in with your normal user and use [su](/index.php/Su "Su") or [sudo](/index.php/Sudo "Sudo") to do system administration.

###### Restrict

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
PermitRootLogin without-password

```

##### Securing the authorized_keys file

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

[Dropbear](https://en.wikipedia.org/wiki/Dropbear_(software) "wikipedia:Dropbear (software)") is a SSH-2 client and server. [dropbear](https://www.archlinux.org/packages/?name=dropbear) is available in the [official repositories](/index.php/Official_repositories "Official repositories").

The command-line ssh client is named dbclient.

### Mosh: Mobile Shell

From the Mosh [website](http://mosh.mit.edu/):

Remote terminal application that allows roaming, supports intermittent connectivity, and provides intelligent local echo and line editing of user keystrokes. Mosh is a replacement for SSH. It is more robust and responsive, especially over slow connections such as Wi-Fi, cellular, and long-distance.

[Install](/index.php/Install "Install") the [mosh](https://www.archlinux.org/packages/?name=mosh) package, or [mosh-git](https://aur.archlinux.org/packages/mosh-git/)<sup><small>AUR</small></sup> for the latest revision.

Mosh has an undocumented command line option `--predict=experimental` which produces more aggressive echoing of local keystrokes. Users interested in low-latency visual confirmation of keyboard input may prefer this prediction mode.

**Tip:** Since Mosh, by design, does not let you access session history, consider installing a terminal multiplexer such as [tmux](/index.php/Tmux "Tmux") or [screen](/index.php/Screen "Screen").

## Tips and tricks

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

**The factual accuracy of this article or section is disputed.**

**Reason:** According to the current layout, this section seems rather generic, but in fact most of the offered tips work only in _openssh_. For example _dropbear_ (listed in [#Other SSH clients and servers](#Other_SSH_clients_and_servers)) does not support SOCKS proxy.[[6]](https://en.wikipedia.org/wiki/Comparison_of_SSH_clients#Technical) (Discuss in [Talk:Secure Shell#](https://wiki.archlinux.org/index.php/Talk:Secure_Shell))

### Encrypted SOCKS tunnel

This is highly useful for laptop users connected to various unsafe wireless connections. The only thing you need is an SSH server running at a somewhat secure location, like your home or at work. It might be useful to use a dynamic DNS service like [DynDNS](http://www.dyndns.org/) so you do not have to remember your IP-address.

#### Step 1: start the connection

You only have to execute this single command to start the connection:

```
$ ssh -TND 4711 _user_@_host_

```

where `_user_` is your username at the SSH server running at the `_host_`. It will ask for your password, and then you are connected! The `N` flag disables the interactive prompt, and the `D` flag specifies the local port on which to listen on (you can choose any port number if you want). The `T` flag disables pseudo-tty allocation.

It is nice to add the verbose (`-v`) flag, because then you can verify that it is actually connected from that output.

#### Step 2: configure your browser (or other programs)

The above step is completely useless if you do not configure your web browser (or other programs) to use this newly created socks tunnel. Since the current version of SSH supports both SOCKS4 and SOCKS5, you can use either of them.

*   For Firefox: _Edit > Preferences > Advanced > Network > Connection > Setting_:  
    Check the _Manual proxy configuration_ radio button, and enter `localhost` in the _SOCKS host_ text field, and then enter your port number in the next text field (`4711` in the example above).

Firefox does not automatically make DNS requests through the socks tunnel. This potential privacy concern can be mitigated by the following steps:

1.  Type about:config into the Firefox location bar.
2.  Search for network.proxy.socks_remote_dns
3.  Set the value to true.
4.  Restart the browser.

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

X11 forwarding is a mechanism that allows graphical interfaces of X11 programs running on a remote system to be displayed on a local client machine. For X11 forwarding the remote host does not need to have a full X11 system installed, however it needs at least to have _xauth_ installed. _xauth_ is a utility that maintains `Xauthority` configurations used by server and client for authentication of X11 session ([source](http://xmodulo.com/2012/11/how-to-enable-x11-forwarding-using-ssh.html)).

**Warning:** X11 forwarding has important security implications which should be at least acknowledged by reading relevant sections of `ssh`, `sshd_config` and `ssh_config` manual pages. See also [a short writeup](https://security.stackexchange.com/questions/14815/security-concerns-with-x11-forwarding)

#### Setup

On the remote system:

*   [install](/index.php/Pacman#Installing_specific_packages "Pacman") [xorg-xauth](https://www.archlinux.org/packages/?name=xorg-xauth) and [xorg-xhost](https://www.archlinux.org/packages/?name=xorg-xhost) from the [official repositories](/index.php/Official_repositories "Official repositories")
*   in `/etc/ssh/ssh**d**_config`:
    *   verify that `AllowTcpForwarding` and `X11UseLocalhost` options are set to _yes_, and that `X11DisplayOffset` is set to _10_ (those are the default values if nothing has been changed, see `man sshd_config`)
    *   set `X11Forwarding` to _yes_
*   then [restart](/index.php/Restart "Restart") the [_sshd_ daemon](#Managing_the_sshd_daemon).

On the client's side, enable the `ForwardX11` option by either specifying the `-X` switch on the command line for opportunistic connections, or by setting `ForwardX11` to _yes_ in [openSSH client's configuration file](#Client).

**Tip:** You can enable the `ForwardX11Trusted` option (`-Y` switch on the command line) if GUI is drawing badly or you receive errors; this will prevent X11 forwardings from being subjected to the [X11 SECURITY extension](http://www.x.org/wiki/Development/Documentation/Security/) controls. Be sure you have read [the warning](#X11_forwarding) at the beginning of this section if you do so.

#### Usage

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

**The factual accuracy of this article or section is disputed.**

**Reason:** `xhost` is [generally not needed](http://unix.stackexchange.com/questions/12755/how-to-forward-x-over-ssh-from-ubuntu-machine#comment-17148) (Discuss in [Talk:Secure Shell#](https://wiki.archlinux.org/index.php/Talk:Secure_Shell))

[Log on to the remote machine](#Connecting_to_the_server) normally, specifying the `-X` switch if _ForwardX11_ was not enabled in the client's configuration file:

```
$ ssh -X _user@host_

```

If you receive errors trying to run graphical applications, try _ForwardX11Trusted_ instead:

```
$ ssh -Y _user@host_

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

where hostname is the name of the particular host you want to forward to. See `man xhost` for more details.

Be careful with some applications as they check for a running instance on the local machine. [Firefox](/index.php/Firefox "Firefox") is an example: either close the running Firefox instance or use the following start parameter to start a remote instance on the local machine:

```
$ firefox --no-remote

```

If you get "X11 forwarding request failed on channel 0" when you connect (and the server `/var/log/errors.log` shows "Failed to allocate internet-domain X11 display socket"), make sure package [xorg-xauth](https://www.archlinux.org/packages/?name=xorg-xauth) is installed. If its installation is not working, try to either:

*   enable the `AddressFamily any` option in `ssh**d**_config` on the _server_, or
*   set the `AddressFamily` option in `ssh**d**_config` on the _server_ to inet.

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

will use SSH to login to and open a shell on 192.168.0.100, and will also create a tunnel from the local machine's TCP port 1000 to mail.google.com on port 25\. Once established, connections to localhost:1000 will connect to the Gmail SMTP port. To Google, it will appear that any such connection (though not necessarily the data conveyed over the connection) originated from 192.168.0.100, and such data will be secure as between the local machine and 192.168.0.100, but not between 192.168.0.100, unless other measures are taken.

Similarly:

```
$ ssh -L 2000:192.168.0.100:6001 192.168.0.100

```

will allow connections to localhost:2000 which will be transparently sent to the remote host on port 6001\. The preceding example is useful for VNC connections using the vncserver utility--part of the tightvnc package--which, though very useful, is explicit about its lack of security.

Remote forwarding allows the remote host to connect to an arbitrary host via the SSH tunnel and the local machine, providing a functional reversal of local forwarding, and is useful for situations where, e.g., the remote host has limited connectivity due to firewalling. It is enabled with the `-R` switch and a forwarding specification in the form of `<tunnel port>:<destination address>:<destination port>`.

Thus:

```
$ ssh -R 3000:irc.freenode.net:6667 192.168.0.200

```

will bring up a shell on 192.168.0.200, and connections from 192.168.0.200 to itself on port 3000 (remotely speaking, localhost:3000) will be sent over the tunnel to the local machine and then on to irc.freenode.net on port 6667, thus, in this example, allowing the use of IRC programs on the remote host to be used, even if port 6667 would normally be blocked to it.

Both local and remote forwarding can be used to provide a secure "gateway," allowing other computers to take advantage of an SSH tunnel, without actually running SSH or the SSH daemon by providing a bind-address for the start of the tunnel as part of the forwarding specification, e.g. `<tunnel address>:<tunnel port>:<destination address>:<destination port>`. The `<tunnel address>` can be any address on the machine at the start of the tunnel, `localhost`, `*` (or blank), which, respectively, allow connections via the given address, via the loopback interface, or via any interface. By default, forwarding is limited to connections from the machine at the "beginning" of the tunnel, i.e. the `<tunnel address>` is set to `localhost`. Local forwarding requires no additional configuration, however remote forwarding is limited by the remote server's SSH daemon configuration. See the `GatewayPorts` option in `sshd_config(5)` for more information.

### Multiplexing

The SSH daemon usually listens on port 22\. However, it is common practice for many public internet hotspots to block all traffic that is not on the regular HTTP/S ports (80 and 443, respectively), thus effectively blocking SSH connections. The immediate solution for this is to have `sshd` listen additionally on one of the whitelisted ports:

 `/etc/ssh/sshd_config` 

```
Port 22
Port 443

```

However, it is likely that port 443 is already in use by a web server serving HTTPS content, in which case it is possible to use a multiplexer, such as [sslh](https://www.archlinux.org/packages/?name=sslh), which listens on the multiplexed port and can intelligently forward packets to many services.

### Speeding up SSH

**Note:** If you intend to use SSH for SFTP or SCP, installing [openssh-hpn-git](https://aur.archlinux.org/packages/openssh-hpn-git/)<sup><small>AUR</small></sup> can significantly increase throughput.[[7]](https://www.psc.edu/index.php/hpn-ssh)

You can make all sessions to the same host use a single connection, which will greatly speed up subsequent logins, by adding these lines under the proper host in `/etc/ssh/ssh_config` or `$HOME/.ssh/config`:

```
Host examplehost.com
  ControlMaster auto
  ControlPersist yes
  ControlPath ~/.ssh/socket-%r@%h:%p

```

**Tip:** To make it a global setting, you can create a `~/.ssh/sockets/` folder and use the following: `~/.ssh/config` 

```
Host *
  ControlPath ~/.ssh/sockets/%r@%h-%p

```

See the `ssh_config(5)` manual page for full description of these options.

Another option to improve speed is to enable compression with the `-C` flag. A permanent solution is to add this line under the proper host in `/etc/ssh/ssh_config` or `$HOME/.ssh/config`:

```
Compression yes

```

**Warning:** `man ssh` states that "_Compression is desirable on modem lines and other slow connections, but will only slow down things on fast networks_". This tip might be counterproductive depending on your network configuration.

Login time can be shortened by using the `-4` flag, which bypasses IPv6 lookup. This can be made permanent by adding this line under the proper host in `/etc/ssh/ssh_config`:

```
AddressFamily inet

```

### Mounting a remote filesystem with SSHFS

Please refer to the [Sshfs](/index.php/Sshfs "Sshfs") article to use sshfs to mount a remote system - accessible via SSH - to a local folder, so you will be able to do any operation on the mounted files with any tool (copy, rename, edit with vim, etc.). Using sshfs instead of shfs is generally preferred as a new version of shfs has not been released since 2004.

### Keep alive

Your ssh session will automatically log out if it is idle. To keep the connection active (alive) add this to `~/.ssh/config` or to `/etc/ssh/ssh_config` on the client.

```
ServerAliveInterval 120

```

This will send a "keep alive" signal to the server every 120 seconds.

See also the `ServerAliveCountMax` and `TCPKeepAlive` options.

Conversely, to keep incoming connections alive, you can set

```
ClientAliveInterval 120

```

(or some other number greater than 0) in `/etc/ssh/sshd_config` on the server.

### Saving connection data in ssh config

Whenever you want to connect to a ssh server, you usually have to type at least its address and the username. To save that typing work for servers you regularly connect to, you can use the personal `~/.ssh/config` or the global `/etc/ssh/ssh_config` files as shown in the following example:

 `~/.ssh/config` 

```
Host myserver
    HostName 123.123.123.123
    Port 12345
    User bob
    IdentityFile ~/.ssh/some_key_file
Host other_server
    HostName test.something.org
    User alice
    CheckHostIP no
    Cipher blowfish

```

Now you can simply connect to the server by using the name you specified:

```
$ ssh myserver

```

To see a complete list of the possible options, check out ssh_config's manpage on your system or the [ssh_config documentation](http://www.openbsd.org/cgi-bin/man.cgi?query=ssh_config) on the official website.

### Automatically restart SSH tunnels with systemd

[systemd](/index.php/Systemd "Systemd") can automatically start SSH connections on boot/login _and_ restart them when they fail. This makes it a useful tool for maintaining SSH tunnels.

The following service can start an SSH tunnel on login using the connection settings in your [ssh config](#Saving_connection_data_in_ssh_config). If the connection closes for any reason, it waits 10 seconds before restarting it:

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

When a session or tunnel cannot be kept alive, for example due to bad network conditions causing client disconnections, you can use [Autossh](http://www.harding.motd.ca/autossh/) to automatically restart them. Autossh can be installed from the [official repositories](/index.php/Official_repositories "Official repositories").

Usage examples:

```
$ autossh -M 0 -o "ServerAliveInterval 45" -o "ServerAliveCountMax 2" username@example.com

```

Combined with [sshfs](/index.php/Sshfs "Sshfs") :

```
$ sshfs -o reconnect,compression=yes,transform_symlinks,ServerAliveInterval=45,ServerAliveCountMax=2,ssh_command='autossh -M 0' username@example.com: /mnt/example 

```

Connecting through a SOCKS-proxy set by [Proxy_settings](/index.php/Proxy_settings "Proxy settings") :

```
$ autossh -M 0 -o "ServerAliveInterval 45" -o "ServerAliveCountMax 2" -NCD 8080 username@example.com 

```

With the `-f` option autossh can be made to run as a background process. Running it this way however means the passphrase cannot be entered interactively.

The session will end once you type `exit` in the session, or the autossh process receives a SIGTERM, SIGINT of SIGKILL signal.

#### Run Autossh automatically at boot via systemd

If you want to automatically start autossh, it is now easy to get systemd to manage this for you. For example, you could create a systemd unit file like this:

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

Then place this in, for example, /etc/systemd/system/autossh.service. Afterwards, you can then start and/or [enable](/index.php/Enable "Enable") your autossh tunnels by enabling the `autossh` service (or whatever you called the service file).

It is also easy to maintain several autossh processes, to keep several tunnels alive. Just create multiple .service files with different names.

## Troubleshooting

### Checklist

This is a first-steps troubleshooting checklist. It is recommended to check these issues before you look any further.

#### Verify SSH settings

1\. The client and server `~/.ssh` folder and its content should be accessible by its user:

```
  $ chmod 700 /home/USER/.ssh
  $ chmod 600 /home/USER/.ssh/*

```

2\. Check that all files within client's and server's `~/.ssh` folder are owned by its user:

```
  $ chown -R USER: /home/USER/.ssh

```

3\. Check that the client's public key in e.g. `id_rsa.pub` is in the server's `authorized_keys` file in the user's `~/.ssh/` folder.

4\. Check that you did not limit SSH access with `AllowUsers or AllowGroups` options in `/etc/ssh/sshd_config` (space separated).

5\. Check if the user has set a password. Sometimes new users are added and do not have a password set nor were logged in once.

#### Restart SSH + Relogin Users

6\. [Restart](/index.php/Restart "Restart") `sshd` (server).

7\. Relogin the user (shell) on both systems (client, host)

#### Cleanup outdated keys (optional)

8\. Delete old/invalid key rows in server's `~/.ssh/authorized_keys` file.

9\. Delete old/invalid private and public keys within the clients `~/.ssh` folder.

#### Recommendations

10\. Keep as few keys as possible in user's `~/.ssh/authorized_keys` file on the server.

11\. Secure server's `/home/USER/.ssh/authorized_keys` file against manipulation:

```
  $ chmod 400 /home/USER/.ssh/authorized_keys

```

### SSH connection left hanging after poweroff/reboot

SSH connection hangs after poweroff or reboot if systemd stop network before sshd. To fix that problem, comment and change the `After` statement:

 `/usr/lib/systemd/system/systemd-user-sessions.service` 

```
#After=remote-fs.target
After=network.target
```

### Connection refused or timeout problem

#### Is your router doing port forwarding?

SKIP THIS STEP IF YOU ARE NOT BEHIND A NAT MODEM/ROUTER (eg, a VPS or otherwise publicly addressed host). Most home and small businesses will have a NAT modem/router.

The first thing is to make sure that your router knows to forward any incoming ssh connection to your machine. Your external IP is given to you by your ISP, and it is associated with any requests coming out of your router. So your router needs to know that any incoming ssh connection to your external IP needs to be forwarded to your machine running sshd.

Find your internal network address.

```
ip a

```

Find your interface device and look for the inet field. Then access your router's configuration web interface, using your router's IP (find this on the web). Tell your router to forward it to your inet IP. Go to [[8]](http://portforward.com/) for more instructions on how to do so for your particular router.

#### Is SSH running and listening?

```
$ ss -tnlp

```

If the above command do not show SSH port is open, SSH is NOT running. Check `/var/log/messages` for errors etc.

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
# tcpdump -ni _interface_ "port 22"

```

For Wireshark:

```
$ tshark -f "tcp port 22" -i _interface_

```

where `_interface_` is the network interface for a WAN connection (see `ip a` to check). If you are not receiving any packets while trying to connect remotely, you can be very sure that your ISP is blocking the incoming traffic on port 22.

##### Possible solution

The solution is just to use some other port that the ISP is not blocking. Open the `/etc/ssh/sshd_config` and configure the file to use different ports. For example, add:

```
Port 22
Port 1234

```

Also make sure that other "Port" configuration lines in the file are commented out. Just commenting "Port 22" and putting "Port 1234" will not solve the issue because then sshd will only listen on port 1234\. Use both lines to run the SSH server on both ports.

[Restart](/index.php/Restart "Restart") the server `sshd.service` and you are almost done. You still have to configure your client(s) to use the other port instead of the default port. There are numerous solutions to that problem, but let us cover two of them here.

#### Read from socket failed: connection reset by peer

Recent versions of openssh sometimes fail with the above error message, due to a bug involving elliptic curve cryptography. In that case add the following line to `~/.ssh/config`:

```
HostKeyAlgorithms ssh-rsa-cert-v01@openssh.com,ssh-dss-cert-v01@openssh.com,ssh-rsa-cert-v00@openssh.com,ssh-dss-cert-v00@openssh.com,ecdsa-sha2-nistp256,ecdsa-sha2-nistp384,ecdsa-sha2-nistp521,ssh-rsa,ssh-dss

```

With openssh 5.9, the above fix does not work. Instead, put the following lines in `~/.ssh/config`:

```
Ciphers aes128-ctr,aes192-ctr,aes256-ctr,aes128-cbc,3des-cbc 
MACs hmac-md5,hmac-sha1,hmac-ripemd160

```

See also the [discussion](http://www.gossamer-threads.com/lists/openssh/dev/51339) on the openssh bug forum.

### "[your shell]: No such file or directory" / ssh_exchange_identification problem

One possible cause for this is the need of certain SSH clients to find an absolute path (one returned by `whereis -b [your shell]`, for instance) in `$SHELL`, even if the shell's binary is located in one of the `$PATH` entries.

### "Terminal unknown" or "Error opening terminal" error message

With ssh it is possible to receive errors like "Terminal unknown" upon logging in. Starting ncurses applications like nano fails with the message "Error opening terminal". There are two methods to this problem, a quick one using the $TERM variable and a profound one using the terminfo file.

#### Workaround by setting the $TERM variable

After connecting to the remote server set the $TERM variable to "xterm" with the following command.

`TERM=xterm`

This method is a workaround and should be used on ssh servers you do seldomly connect to, because it can have unwanted side effects. Also you have to repeat the command after every connection, or alternatively set it in ~.bashrc .

#### Solution using terminfo file

A profound solution is transferring the terminfo file of the terminal on your client computer to the ssh server. In this example we cover how to setup the terminfo file for the "rxvt-unicode-256color" terminal. Create the directory containing the terminfo files on the ssh server, while you are logged in to the server issue this command:

`mkdir -p ~/.terminfo/r/`

Now copy the terminfo file of your terminal to the new directory. Replace `rxvt-unicode-256color` with your client's terminal in the following command and `ssh-server` with the relevant user and server adress.

`$ scp /usr/share/terminfo/r/_rxvt-unicode-256color_ ssh-server:~/.terminfo/r/`

After logging in and out from the ssh server the problem should be fixed.

### Connection closed by x.x.x.x [preauth]

If you are seeing this error in your sshd logs, make sure you have set a valid HostKey

```
HostKey /etc/ssh/ssh_host_rsa_key

```

### id_dsa refused by OpenSSH 7.0

OpenSSH 7.0 deprecated ssh-dss and [http://www.openssh.com/legacy.html](http://www.openssh.com/legacy.html) does not document how to reach server if id_dsa keys are used:

```
PubkeyAcceptedKeyTypes +ssh-dss

```

While this can be added a per host basis or with -o, to make sure "ProxyCommand ssh" still works, add it to ssh_config.

### no matching key exchange method found by OpenSSH 7.0

OpenSSH 7.0 also deprecated the key algorithm diffie-hellman-group1-sha1, as we could see in [http://www.openssh.com/legacy.html](http://www.openssh.com/legacy.html).

If the client and server are unable to agree on a mutual set of parameters then the connection will fail. OpenSSH (7.0 and greater) will produce an error message like this:

```
 Unable to negotiate with 127.0.0.1: no matching key exchange method found.
 Their offer: diffie-hellman-group1-sha1

```

In this case, the client and server were unable to agree on the key exchange algorithm. The server offered only a single method diffie-hellman-group1-sha1\. OpenSSH supports this method, but does not enable it by default because is weak and within theoretical range of the so-called Logjam attack.

The best resolution for these failures is to upgrade the software at the other end. OpenSSH only disables algorithms that we actively recommend against using because they are known to be weak. In some cases, this might not be immediately possible so you may need to temporarily re-enable the weak algorithms to retain access.

For the case of the above error message, OpenSSH can be configured to enable the diffie-hellman-group1-sha1 key exchange algorithm (or any other that is disabled by default) using the KexAlgorithm option - either on the command-line:

```
 ssh -oKexAlgorithms=+diffie-hellman-group1-sha1 user@127.0.0.1

```

or in the ~/.ssh/config file:

```
 Host somehost.example.org
 	KexAlgorithms +diffie-hellman-group1-sha1

```

## See also

*   [Wikipedia:Secure Shell](https://en.wikipedia.org/wiki/Secure_Shell "wikipedia:Secure Shell")
*   [Defending against brute force ssh attacks](http://www.la-samhna.de/library/brutessh.html)
*   [OpenSSH key management, Part 1](http://www.ibm.com/developerworks/library/l-keyc/index.html) and [Part 2](http://www.ibm.com/developerworks/library/l-keyc2) on IBM developerWorks
*   [Secure Secure Shell](https://stribika.github.io/2015/01/04/secure-secure-shell.html)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Secure_Shell&oldid=414783](https://wiki.archlinux.org/index.php?title=Secure_Shell&oldid=414783)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Secure Shell](/index.php/Category:Secure_Shell "Category:Secure Shell")