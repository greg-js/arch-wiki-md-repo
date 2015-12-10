# Identd Setup

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

**This article or section needs language, wiki syntax or style improvements.**

**Reason:** Unnecessary use of ordered lists; other style issues, see [Help:Style](/index.php/Help:Style "Help:Style"). (Discuss in [Talk:Identd Setup#](https://wiki.archlinux.org/index.php/Talk:Identd_Setup))

The Ident service as specified by [RFC 1413](//tools.ietf.org/html/rfc1413) is mostly used by various IRC networks and the occasional old FTP server to ask a remote server which user is making a connection. This method is quite untrustworthy, as the remote host can simply choose to lie.

So you have two choices:

1.  Tell the truth (see pidentd below)
2.  Tell a little white lie (see nullidentmod or nullidentd below)

## Contents

*   [1 pIdentd](#pIdentd)
*   [2 nullIdentdMod](#nullIdentdMod)
    *   [2.1 Customization](#Customization)
*   [3 nullIdent](#nullIdent)
    *   [3.1 systemd activation](#systemd_activation)

## pIdentd

Like most people, I prefer to run identd from from inetd instead of as a stand-alone service. For this to work you will need to install two packages: xinetd and pidentd. I tried this with oidentd but it does not seem to work with the latest xinetd.

**1.** Install the [xinetd](https://www.archlinux.org/packages/?name=xinetd) and [pidentd](https://aur.archlinux.org/packages/pidentd/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/pidentd)]</sup> packages.

**2.** Next, you will need to paste the following into a new file and save it as `/etc/xinetd.d/auth`

```
service auth
{
      flags = REUSE
      socket_type = stream
      wait = no
      user = nobody
      server = /usr/bin/identd
      server_args = -m -N
      log_on_failure += USERID
      disable = no
}

```

**3.** After you have saved the new file, start **xinetd** [systemd](/index.php/Systemd "Systemd") service.

If all went well, you should have the auth service running on port 113\. A good way of checking this is by installing [nmap](https://www.archlinux.org/packages/?name=nmap) (if you do not have it already) and typing

```
$ nmap localhost

```

## nullIdentdMod

**1.** [Install](/index.php/Install "Install") the [nullidentdmod-git](https://aur.archlinux.org/packages/nullidentdmod-git/)<sup><small>AUR</small></sup> package.

**2.** [Enable](/index.php/Enable "Enable") `nullidentdmod.socket` on systemd.

**3.** [Start](/index.php/Start "Start") `nullidentdmod.socket` on systemd.

**4.** Check if is working [here](http://acidhub.click/NullidentdMod/).

As is nullidentdmod will return a random userid.

### Customization

**1.** Copy the unit for customization

```
# cp /usr/lib/systemd/system/nullidentdmod@.service /etc/systemd/system/

```

**2.** [Edit](/index.php/Edit "Edit") `/etc/systemd/system/nullidentdmod@.service` At line 6, write desired userid

```
[Unit]                                   
Description=NullidentdMod service        

[Service]                                
User=nobody                              
ExecStart=/usr/bin/nullidentdmod **<userid>**
StandardInput=socket                     
StandardOutput=socket                    

[Install]                                
WantedBy=multi-user.target               

```

Obviously where <userid> you put your custom userid.

**4.** Check if is working [here](http://acidhub.click/NullidentdMod/)

## nullIdent

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

**This article or section is out of date.**

**Reason:** sbin is deprecated in [Arch filesystem hierarchy](/index.php/Arch_filesystem_hierarchy "Arch filesystem hierarchy") (Discuss in [Talk:Identd Setup#](https://wiki.archlinux.org/index.php/Talk:Identd_Setup))

This Ident server is capable of only returning the same name for any query. With a quick change to a single line of code, it can be customized to return any name you can think. One use for such a simple service would be for IRC client connections to ensure a degree of privacy (remote IRC server and users do not know your username) as well as allowing a small degree of 'vanity plating' for use in IRC channels.

The original code suffered link rot, but may now be found on github, at this address [https://github.com/dxtr/nullidentd](https://github.com/dxtr/nullidentd).

**1.** clone the source to a directory of your choice using git.

```
git clone https://github.com/dxtr/nullidentd

```

**2.** Edit line 86 of nullidentd.c to your liking. use any text editor of your choice

example:

```
nano nullidentd.c

```

**3.** Compile the binary.

```
make

```

**4.** Install Binary You can move it to any location of your choice of course, but the FileSystem Hierarchy states the nullidentd binary should live in `/usr/local/sbin`

```
# mv nullidentd /usr/local/sbin

```

### systemd activation

Below are two files you need to create under `/etc/systemd/system/`

**1.** identd@.service

```
[Unit]
Description=per connection null identd

[Service]
User=nobody
ExecStart=/usr/local/sbin/nullidentd
StandardInput=socket
StandardOutput=socket

```

**2.** ident.socket

```
[Unit]
Description=socket for ident

[Socket]
ListenStream=113
Accept=yes

[Install]
WantedBy=sockets.target

```

**3.** inform SystemD of the new files

```
# systemctl daemon-reload

```

**4.** Test that the socket is listening sucessfully

```
$ systemctl status ident.socket

```

this should yield output similar to the below

```
ident.socket - socket for ident
   Loaded: loaded (/etc/systemd/system/ident.socket; enabled)
   Active: active (listening) since Fri 2014-01-24 02:30:53 WST; 30 seconds ago
   Listen: [::]:113 (Stream)
 Accepted: 0; Connected: 0

Jan 24 02:30:53 HOSTNAME systemd[1]: Listening on socket for ident.

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=Identd_Setup&oldid=392251](https://wiki.archlinux.org/index.php?title=Identd_Setup&oldid=392251)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Networking](/index.php/Category:Networking "Category:Networking")