**Secure Shell** (**SSH**) is a network protocol that allows data to be exchanged over a secure channel between two computers. Encryption provides confidentiality and integrity of data. SSH uses public-key cryptography to authenticate the remote computer and allow the remote computer to authenticate the user, if necessary.

SSH is typically used to log into a remote machine and execute commands, but it also supports tunneling, forwarding arbitrary TCP ports and X11 connections; file transfer can be accomplished using the associated SFTP or SCP protocols.

An SSH server, by default, listens on the standard TCP port 22\. An SSH client program is typically used for establishing connections to an _sshd_ daemon accepting remote connections. Both are commonly present on most modern operating systems, including Mac OS X, GNU/Linux, Solaris and OpenVMS. Proprietary, freeware and open source versions of various levels of complexity and completeness exist.

(Source: [Wikipedia:Secure Shell](https://en.wikipedia.org/wiki/Secure_Shell "wikipedia:Secure Shell"))

## Contents

*   [1 OpenSSH](#OpenSSH)
    *   [1.1 Installing OpenSSH](#Installing_OpenSSH)
    *   [1.2 Configuring SSH](#Configuring_SSH)
        *   [1.2.1 Client](#Client)
        *   [1.2.2 Daemon](#Daemon)
    *   [1.3 Managing SSHD Daemon](#Managing_SSHD_Daemon)
    *   [1.4 Connecting to the server](#Connecting_to_the_server)
*   [2 Tips and Tricks](#Tips_and_Tricks)
    *   [2.1 Encrypted Socks Tunnel](#Encrypted_Socks_Tunnel)
        *   [2.1.1 Step 1: Start the Connection](#Step_1:_Start_the_Connection)
        *   [2.1.2 Step 2: Configure your Browser (or other programs)](#Step_2:_Configure_your_Browser_.28or_other_programs.29)
    *   [2.2 X11 Forwarding](#X11_Forwarding)
    *   [2.3 Forwarding Other Ports](#Forwarding_Other_Ports)
    *   [2.4 Speed up SSH](#Speed_up_SSH)
        *   [2.4.1 Troubleshooting](#Troubleshooting)
    *   [2.5 Mounting a Remote Filesystem with SSHFS](#Mounting_a_Remote_Filesystem_with_SSHFS)
    *   [2.6 Keep Alive](#Keep_Alive)
    *   [2.7 Save connection data in ssh config](#Save_connection_data_in_ssh_config)
    *   [2.8 Change bash prompt when logged over ssh](#Change_bash_prompt_when_logged_over_ssh)
    *   [2.9 Automatically logout all ssh users when the sshd server is shutdown](#Automatically_logout_all_ssh_users_when_the_sshd_server_is_shutdown)
*   [3 Troubleshooting](#Troubleshooting_2)
    *   [3.1 Connection Refused or Timeout Problem](#Connection_Refused_or_Timeout_Problem)
        *   [3.1.1 Is SSH running and listening?](#Is_SSH_running_and_listening.3F)
        *   [3.1.2 Are there firewall rules blocking the connection?](#Are_there_firewall_rules_blocking_the_connection.3F)
        *   [3.1.3 Is the traffic even getting to your computer?](#Is_the_traffic_even_getting_to_your_computer.3F)
        *   [3.1.4 Read from socket failed: Connection reset by peer](#Read_from_socket_failed:_Connection_reset_by_peer)
    *   [3.2 "[your shell]: No such file or directory" / ssh_exchange_identification Problem](#.22.5Byour_shell.5D:_No_such_file_or_directory.22_.2F_ssh_exchange_identification_Problem)
*   [4 See Also](#See_Also)
*   [5 Links & References](#Links_.26_References)

## OpenSSH

OpenSSH (OpenBSD Secure Shell) is a set of computer programs providing encrypted communication sessions over a computer network using the ssh protocol. It was created as an open source alternative to the proprietary Secure Shell software suite offered by SSH Communications Security. OpenSSH is developed as part of the OpenBSD project, which is led by Theo de Raadt.

OpenSSH is occasionally confused with the similarly-named OpenSSL; however, the projects have different purposes and are developed by different teams, the similar name is drawn only from similar goals.

### Installing OpenSSH

```
# pacman -S openssh

```

### Configuring SSH

#### Client

The SSH client configuration file can be found and edited in `/etc/ssh/ssh_config`.

An example configuration:

 `/etc/ssh/ssh_config` 

```
#	$OpenBSD: ssh_config,v 1.26 2010/01/11 01:39:46 dtucker Exp $

# This is the ssh client system-wide configuration file.  See
# ssh_config(5) for more information.  This file provides defaults for
# users, and the values can be changed in per-user configuration files
# or on the command line.

# Configuration data is parsed as follows:
#  1\. command line options
#  2\. user-specific file
#  3\. system-wide file
# Any configuration value is only changed the first time it is set.
# Thus, host-specific definitions should be at the beginning of the
# configuration file, and defaults at the end.

# Site-wide defaults for some commonly used options.  For a comprehensive
# list of available options, their meanings and defaults, please see the
# ssh_config(5) man page.

# Host *
#   ForwardAgent no
#   ForwardX11 no
#   RhostsRSAAuthentication no
#   RSAAuthentication yes
#   PasswordAuthentication yes
#   HostbasedAuthentication no
#   GSSAPIAuthentication no
#   GSSAPIDelegateCredentials no
#   BatchMode no
#   CheckHostIP yes
#   AddressFamily any
#   ConnectTimeout 0
#   StrictHostKeyChecking ask
#   IdentityFile ~/.ssh/identity
#   IdentityFile ~/.ssh/id_rsa
#   IdentityFile ~/.ssh/id_dsa
#   Port 22
#   Protocol 2,1
#   Cipher 3des
#   Ciphers aes128-ctr,aes192-ctr,aes256-ctr,arcfour256,arcfour128,aes128-cbc,3des-cbc
#   MACs hmac-md5,hmac-sha1,umac-64@openssh.com,hmac-ripemd160
#   EscapeChar ~
#   Tunnel no
#   TunnelDevice any:any
#   PermitLocalCommand no
#   VisualHostKey no
#   ProxyCommand ssh -q -W %h:%p gateway.example.com

```

It is recommended to change the Protocol line into this:

```
Protocol 2

```

That means that only Protocol 2 will be used, since Protocol 1 is considered somewhat insecure.

#### Daemon

The SSH daemon configuration file can be found and edited in `/etc/ssh/ssh**d**_config`.

An example configuration:

 `/etc/ssh/sshd_config` 

```
#	$OpenBSD: sshd_config,v 1.82 2010/09/06 17:10:19 naddy Exp $

# This is the sshd server system-wide configuration file.  See
# sshd_config(5) for more information.

# This sshd was compiled with PATH=/usr/bin:/bin:/usr/sbin:/sbin

# The strategy used for options in the default sshd_config shipped with
# OpenSSH is to specify options with their default value where
# possible, but leave them commented.  Uncommented options change a
# default value.

#Port 22
#AddressFamily any
#ListenAddress 0.0.0.0
#ListenAddress ::

# The default requires explicit activation of protocol 1
#Protocol 2

# HostKey for protocol version 1
#HostKey /etc/ssh/ssh_host_key
# HostKeys for protocol version 2
#HostKey /etc/ssh/ssh_host_rsa_key
#HostKey /etc/ssh/ssh_host_dsa_key
#HostKey /etc/ssh/ssh_host_ecdsa_key

# Lifetime and size of ephemeral version 1 server key
#KeyRegenerationInterval 1h
#ServerKeyBits 1024

# Logging
# obsoletes QuietMode and FascistLogging
#SyslogFacility AUTH
#LogLevel INFO

# Authentication:

#LoginGraceTime 2m
#PermitRootLogin yes
#StrictModes yes
#MaxAuthTries 6
#MaxSessions 10

#RSAAuthentication yes
#PubkeyAuthentication yes
#AuthorizedKeysFile	.ssh/authorized_keys

# For this to work you will also need host keys in /etc/ssh/ssh_known_hosts
#RhostsRSAAuthentication no
# similar for protocol version 2
#HostbasedAuthentication no
# Change to yes if you do not trust ~/.ssh/known_hosts for
# RhostsRSAAuthentication and HostbasedAuthentication
#IgnoreUserKnownHosts no
# Don't read the user's ~/.rhosts and ~/.shosts files
#IgnoreRhosts yes

# To disable tunneled clear text passwords, change to no here!
#PasswordAuthentication yes
#PermitEmptyPasswords no

# Change to no to disable s/key passwords
ChallengeResponseAuthentication no

# Kerberos options
#KerberosAuthentication no
#KerberosOrLocalPasswd yes
#KerberosTicketCleanup yes
#KerberosGetAFSToken no

# GSSAPI options
#GSSAPIAuthentication no
#GSSAPICleanupCredentials yes

# Set this to 'yes' to enable PAM authentication, account processing, 
# and session processing. If this is enabled, PAM authentication will 
# be allowed through the ChallengeResponseAuthentication and
# PasswordAuthentication.  Depending on your PAM configuration,
# PAM authentication via ChallengeResponseAuthentication may bypass
# the setting of "PermitRootLogin without-password".
# If you just want the PAM account and session checks to run without
# PAM authentication, then enable this but set PasswordAuthentication
# and ChallengeResponseAuthentication to 'no'.
UsePAM yes

#AllowAgentForwarding yes
#AllowTcpForwarding yes
#GatewayPorts no
#X11Forwarding no
#X11DisplayOffset 10
#X11UseLocalhost yes
#PrintMotd yes
#PrintLastLog yes
#TCPKeepAlive yes
#UseLogin no
#UsePrivilegeSeparation yes
#PermitUserEnvironment no
#Compression delayed
#ClientAliveInterval 0
#ClientAliveCountMax 3
#UseDNS yes
#PidFile /var/run/sshd.pid
#MaxStartups 10
#PermitTunnel no
#ChrootDirectory none

# no default banner path
#Banner none

# override default of no subsystems
Subsystem	sftp	/usr/lib/ssh/sftp-server

# Example of overriding settings on a per-user basis
#Match User anoncvs
#	X11Forwarding no
#	AllowTcpForwarding no
#	ForceCommand cvs server
```

To allow access only for some users add this line:

```
AllowUsers    user1 user2

```

To disable root login over SSH, add the following:

```
PermitRootLogin no

```

You could also uncomment the BANNER option and edit `/etc/issue` for a nice welcome message.

**Tip:** You may want to change the default port from 22 to any higher port (see [security through obscurity](http://en.wikipedia.org/wiki/Security_through_obscurity)).

Even though the port ssh is running on could be detected by using a port-scanner like nmap, changing it will reduce the number of log entries caused by automated authentication attempts. To help select a port review the [list of TCP and UDP port numbers](https://en.wikipedia.org/wiki/List_of_TCP_and_UDP_port_numbers "wikipedia:List of TCP and UDP port numbers").

**Tip:** Disabling password logins entirely will greatly increase security, see [Using SSH Keys](/index.php/Using_SSH_Keys "Using SSH Keys") for more information.

### Managing SSHD Daemon

Just add sshd to the "DAEMONS" array of your `/etc/[rc.conf](/index.php/Rc.conf "Rc.conf")`:

```
DAEMONS=(... ... **sshd** ... ...)

```

To start/restart/stop the daemon, use the following:

```
# rc.d {start|stop|restart} sshd

```

Or

```
# systemctl start sshd

```

### Connecting to the server

To connect to a server, run:

```
$ ssh -p port user@server-address

```

## Tips and Tricks

### Encrypted Socks Tunnel

This is highly useful for laptop users connected to various unsafe wireless connections. The only thing you need is an SSH server running at a somewhat secure location, like your home or at work. It might be useful to use a dynamic DNS service like [DynDNS](http://www.dyndns.org/) so you do not have to remember your IP-address.

#### Step 1: Start the Connection

You only have to execute this single command in your favorite terminal to start the connection:

```
$ ssh -ND 4711 user@host

```

where `"user"` is your username at the SSH server running at the `"host"`. It will ask for your password, and then you're connected! The `"N"` flag disables the interactive prompt, and the `"D"` flag specifies the local port on which to listen on (you can choose any port number if you want).

One way to make this easier is to put an alias line in your `~/.bashrc` file as following:

```
alias sshtunnel="ssh -ND 4711 -v user@host"

```

It's nice to add the verbose `"-v"` flag, because then you can verify that it's actually connected from that output. Now you just have to execute the `"sshtunnel"` command :)

#### Step 2: Configure your Browser (or other programs)

The above step is completely useless if you do not configure your web browser (or other programs) to use this newly created socks tunnel. Since the current version of SSH supports both SOCKS4 and SOCKS5, you can use either of them.

*   For Firefox: _Edit → Preferences → Advanced → Network → Connection → Setting_:

	Check the _"Manual proxy configuration"_ radio button, and enter "localhost" in the _"SOCKS host"_ text field, and then enter your port number in the next text field (I used 4711 above).

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

### X11 Forwarding

To run graphical programs through a SSH connection you can enable X11 forwarding. An option needs to be set in the configuration files on the server and client (here "client" means your (desktop) machine your X11 Server runs on, and you will run X applications on the "server").

Install xorg-xauth on the server:

```
# pacman -S xorg-xauth

```

*   Enable the **AllowTcpForwarding** option in `ssh**d**_config` on the **server**.
*   Enable the **X11Forwarding** option in `ssh**d**_config` on the **server**.
*   Set the **X11DisplayOffset** option in `ssh**d**_config` on the **server** to 10.
*   Enable the **X11UseLocalhost** option in `ssh**d**_config` on the **server**.

Also:

*   Enable the **ForwardX11** option in `ssh_config` on the **client**.

Enable the **ForwardX11Trusted** can help when gui drawing badly.

To use the forwarding, log on to your server through ssh:

```
$ ssh -X -p port user@server-address

```

If you receive errors trying to run graphical applications try trusted forwarding instead:

```
$ ssh -Y -p port user@server-address

```

You can now start any X program on the remote server, the output will be forwarded to your local session:

```
$ xclock

```

If you get "Cannot open display" errors try the following command as the non root user:

```
$ xhost +

```

the above command will allow anybody to forward X11 applications. To restrict forwarding to a particular host type:

```
$ xhost +hostname

```

where hostname is the name of the particular host you want to forward to. Type "man xhost" for more details.

Be careful with some applications as they check for a running instance on the local machine. Firefox is an example. Either close running Firefox or use the following start parameter to start a remote instance on the local machine

```
$ firefox -no-remote

```

### Forwarding Other Ports

In addition to SSH's built-in support for X11, it can also be used to securely tunnel any TCP connection, by use of local forwarding or remote forwarding.

Local forwarding opens a port on the local machine, connections to which will be forwarded to the remote host and from there on to a given destination. Very often, the forwarding destination will be the same as the remote host, thus providing a secure shell and, e.g. a secure VNC connection, to the same machine. Local forwarding is accomplished by means of the `-L` switch and it's accompanying forwarding specification in the form of `<tunnel port>:<destination address>:<destination port>`.

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

### Speed up SSH

You can make all sessions to the same host use a single connection, which will greatly speed up subsequent logins, by adding these lines under the proper host in `/etc/ssh/ssh_config`:

```
ControlMaster auto
ControlPath ~/.ssh/socket-%r@%h:%p

```

Changing the ciphers used by SSH to less cpu-demanding ones can improve speed. In this aspect, the best choices are arcfour and blowfish-cbc. **Please do not do this unless you know what you are doing; arcfour has a number of known weaknesses**. To use them, run SSH with the `"c"` flag, like this:

```
$ ssh -c arcfour,blowfish-cbc user@server-address

```

To use them permanently, add this line under the proper host in `/etc/ssh/ssh_config`:

```
Ciphers arcfour,blowfish-cbc

```

Another option to improve speed is to enable compression with the `"C"` flag. A permanent solution is to add this line under the proper host in `/etc/ssh/ssh_config`:

```
Compression yes

```

Login time can be shorten by using the `"4"` flag, which bypasses IPv6 lookup. This can be made permanent by adding this line under the proper host in `/etc/ssh/ssh_config`:

```
AddressFamily inet

```

Another way of making these changes permanent is to create an alias in `~/.bashrc`:

```
alias ssh='ssh -C4c arcfour,blowfish-cbc'

```

#### Troubleshooting

Make sure your DISPLAY string is resolveable on the remote end:

```
$ ssh -X user@server-address
server $ echo $DISPLAY
localhost:10.0
server $ telnet localhost 6010
localhost/6010: lookup failure: Temporary failure in name resolution   

```

can be fixed by adding localhost to `/etc/hosts`.

### Mounting a Remote Filesystem with SSHFS

Install sshfs

```
# pacman -S sshfs

```

Load the Fuse module

```
# modprobe fuse

```

Add fuse to the _modules_ array in `/etc/rc.conf` to load it on each system boot.

Mount the remote folder using sshfs

```
# mkdir ~/remote_folder
# sshfs USER@remote_server:/tmp ~/remote_folder

```

The command above will cause the folder /tmp on the remote server to be mounted as ~/remote_folder on the local machine. Copying any file to this folder will result in transparent copying over the network using SFTP. Same concerns direct file editing, creating or removing.

When we’re done working with the remote filesystem, we can unmount the remote folder by issuing:

```
# fusermount -u ~/remote_folder

```

If we work on this folder on a daily basis, it is wise to add it to the `/etc/fstab` table. This way is can be automatically mounted upon system boot or mounted manually (if `noauto` option is chosen) without the need to specify the remote location each time. Here is a sample entry in the table:

```
sshfs#USER@remote_server:/tmp /full/path/to/directory fuse    defaults,auto,allow_other    0 0

```

### Keep Alive

Your ssh session will automatically log out if it is idle. To keep the connection active (alive) add this to `~/.ssh/config` or to `/etc/ssh/ssh_config` on the client.

```
ServerAliveInterval 120

```

This will send a "keep alive" signal to the server every 120 seconds.

Conversely, to keep incoming connections alive, you can set

```
ClientAliveInterval 120

```

(or some other number greater than 0) in `/etc/ssh/sshd_config` on the server.

### Save connection data in ssh config

Whenever you want to connect to a ssh server, you usually have to type at least its address and the username. To save that typing work for servers you regularly connect to, you can use the personal `$HOME/.ssh/config` or the global `/etc/ssh/ssh_config` files as shown in the following example:

 `$HOME/.ssh/config` 

```
Host myserver
    HostName 123.123.123.123
    Port 12345
    User bob
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

### Change bash prompt when logged over ssh

It can sometimes be useful to be able to make the difference between your local and your remote prompt, in particular when they are both configured in the same way. To do that, just insert this in your bashrc:

 `$HOME/.bashrc` 

```
if [ -n "$SSH_CLIENT" ]; then
        PS1='\[\e[0;33m\]\u@\h:\wSSH$\[\e[m\] '
else
        PS1='\[\e[0;32m\]\u\[\e[m\] \[\e[1;34m\]\w\[\e[m\] \[\e[1;32m\]\$\[\    e[m\] '
fi
```

See [Color Bash Prompt](/index.php/Color_Bash_Prompt "Color Bash Prompt") for more information about the PS1 variable customization.

### Automatically logout all ssh users when the sshd server is shutdown

To automatically log out all remote ssh users when the sshd server system shuts down, for reboot or halt, add this line to /etc/rc.local.shutdown on the sshd server:

```
who | cut -d " " -f1 | uniq | xargs pkill -KILL -u

```

This prevents ssh client terminals from hanging during a lengthy timeout, which eventually ends with:

```
Write failed: Broken pipe

```

## Troubleshooting

### Connection Refused or Timeout Problem

#### Is SSH running and listening?

```
$ ss -tnlp

```

If the above command do not show SSH port is open, SSH is NOT running. Check `/var/log/messages` for errors etc.

#### Are there firewall rules blocking the connection?

Flush your iptables rules to make sure they are not interfering:

```
# rc.d stop iptables

```

or:

```
# iptables -P INPUT ACCEPT
# iptables -P OUTPUT ACCEPT
# iptables -F INPUT
# iptables -F OUTPUT

```

#### Is the traffic even getting to your computer?

Start a traffic dump on the computer you're having problems with:

```
# tcpdump -lnn -i any port ssh and tcp-syn

```

This should show some basic information, then wait for any matching traffic to happen before displaying it. Try your connection now. If you do not see any output when you attempt to connect, then something outside of your computer is blocking the traffic (e. g., hardware firewall, NAT router etc.).

#### Read from socket failed: Connection reset by peer

Recent versions of openssh sometimes fail with the above error message, due to a bug involving elliptic curve cryptography. In that case, edit the file

```
~/.ssh/config

```

or create it, if it doesn't already exist. Add the line

```
HostKeyAlgorithms ssh-rsa-cert-v01@openssh.com,ssh-dss-cert-v01@openssh.com,ssh-rsa-cert-v00@openssh.com,ssh-dss-cert-v00@openssh.com,ecdsa-sha2-nistp256,ecdsa-sha2-nistp384,ecdsa-sha2-nistp521,ssh-rsa,ssh-dss

```

With openssh 5.9, the above fix doesn't work. Instead, put the following lines in ~/.ssh/config

```
Ciphers aes128-ctr,aes192-ctr,aes256-ctr,aes128-cbc,3des-cbc 
MACs hmac-md5,hmac-sha1,hmac-ripemd160

```

See also the [discussion](http://www.gossamer-threads.com/lists/openssh/dev/51339) on the openssh bug forum.

### "[your shell]: No such file or directory" / ssh_exchange_identification Problem

One possible cause for this is the need of certain SSH clients to find an absolute path (one returned by `whereis -b [your shell]`, for instance) in `$SHELL`, even if the shell's binary is located in one of the `$PATH` entries. Another reason can be that the user is no member of the _network_ group.

## See Also

*   [SSH keys](/index.php/SSH_keys "SSH keys")
*   [Pam abl](/index.php/Pam_abl "Pam abl")
*   [fail2ban](/index.php/Fail2ban "Fail2ban")
*   [sshguard](/index.php/Sshguard "Sshguard")
*   [Sshfs](/index.php/Sshfs "Sshfs")

## Links & References

*   [A Cure for the Common SSH Login Attack](http://www.soloport.com/iptables.html)
*   [Defending against brute force ssh attacks](http://www.la-samhna.de/library/brutessh.html)
*   [OpenSSH key management, Part 1](http://www.ibm.com/developerworks/library/l-keyc/index.html) and [Part 2](http://www.ibm.com/developerworks/library/l-keyc2) on IBM developerWorks