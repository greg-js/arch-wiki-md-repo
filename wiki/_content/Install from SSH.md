# Install from SSH

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

This article is intended to show users how to install Arch remotely via an [SSH](/index.php/SSH "SSH") connection. Consider this approach over the standard one in scenarios such as the following:

*   HTPC without a proper monitor (e.g. an SDTV);
*   PC located in another city, state, country (friend's house, parent's house, etc.);
*   PC that you would rather setup remotely, for example from the comfort of one's own workstation with copy/paste abilities from the ArchWiki.

## On the remote (target) machine

**Note:** These steps require physical access to the machine. Obviously, if physically located elsewhere, this will need to be coordinated with another person.

Boot the target machine into a live Arch environment via the [Live CD/USB image](/index.php/Category:Getting_and_installing_Arch "Category:Getting and installing Arch"): this will log the user in as root.

At this point, setup the network on the target machine as for example suggested in [Installation guide#Connect to the Internet](/index.php/Installation_guide#Connect_to_the_Internet "Installation guide").

Secondly, setup a root password which is needed for an SSH connection, since the default Arch password for root is empty:

```
# passwd

```

Now add `PermitRootLogin yes` to `/etc/ssh/sshd_config` to allow root login with password authentification on the SSH server.

**Note:** If the target machine is behind a NAT router, the SSH port (22 by default) will obviously need to be forwarded to the target machine's LAN IP address. The use of port forwarding is not covered in this guide.

Finally, [start](/index.php/Start "Start") the openssh daemon with `sshd.service`, which is included by default on the live CD.

## On the local machine

On the local machine, connect to the target machine via SSH with the following command:

```
$ ssh root@_ip.address.of.target_

```

From here one is presented with the live environment's welcome message and is able to administer the target machine as if sitting at the physical keyboard. At this point, if the intent is to simply install Arch from the live media, follow the guide at [Installation guide](/index.php/Installation_guide "Installation guide"). If the intent is to edit an existing Linux install that got broken, follow the [Install from existing Linux](/index.php/Install_from_existing_Linux "Install from existing Linux") wiki article.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Install_from_SSH&oldid=410450](https://wiki.archlinux.org/index.php?title=Install_from_SSH&oldid=410450)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Getting and installing Arch](/index.php/Category:Getting_and_installing_Arch "Category:Getting and installing Arch")
*   [Secure Shell](/index.php/Category:Secure_Shell "Category:Secure Shell")