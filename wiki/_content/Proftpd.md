# Proftpd

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-document-new.png](/images/f/f0/Tango-document-new.png)](/index.php/File:Tango-document-new.png)

[![Tango-document-new.png](/images/f/f0/Tango-document-new.png)](/index.php/File:Tango-document-new.png)

**This article is a stub.**

**Notes:** please use the first argument of the template to provide more detailed indications. (Discuss in [Talk:Proftpd#](https://wiki.archlinux.org/index.php/Talk:Proftpd))

[proFtpd](http://proftpd.org/) (Pro FTP daemon) is a highly feature rich FTP server, exposing large amount of configuration options to the user.

## Contents

*   [1 Installation](#Installation)
*   [2 Troubleshooting](#Troubleshooting)
    *   [2.1 Anonymous access](#Anonymous_access)
*   [3 See also](#See_also)

## Installation

[proftpd](https://aur.archlinux.org/packages/proftpd/)<sup><small>AUR</small></sup> is available in the AUR. [Enable](/index.php/Enable "Enable") and start `proftpd.service`.

## Troubleshooting

### Anonymous access

To head off a common problem, for anonymous access to work with /bin/false as the shell for the ftp user (the default configuration), you must add the line `RequireValidShell off` to `/etc/proftpd.conf`. Otherwise anonymous logins will receive a 530 error.

## See also

*   [BLFS: ProFTPD](http://www.linuxfromscratch.org/blfs/view/7.6/server/proftpd.html)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Proftpd&oldid=414869](https://wiki.archlinux.org/index.php?title=Proftpd&oldid=414869)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [File Transfer Protocol](/index.php/Category:File_Transfer_Protocol "Category:File Transfer Protocol")