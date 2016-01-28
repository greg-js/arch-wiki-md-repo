# CurlFtpFS

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** please use the first argument of the template to provide a brief explanation. (Discuss in [Talk:CurlFtpFS#](https://wiki.archlinux.org/index.php/Talk:CurlFtpFS))

Related articles

*   [List of applications/Internet#FTP clients](/index.php/List_of_applications/Internet#FTP_clients "List of applications/Internet")

**Note:** As of February 2015, curlftpfs is reported to be extremely slow, see for example [a Ubuntu bug report](https://bugs.launchpad.net/ubuntu/+source/curlftpfs/+bug/1267749) and a [stackoverflow.com question](http://stackoverflow.com/questions/24360479/ftp-with-curlftpfs-is-extremely-slow-to-the-point-it-is-impossible-to-work-with).

## Installation

[Install](/index.php/Install "Install") [curlftpfs](https://www.archlinux.org/packages/?name=curlftpfs) from the [official repositories](/index.php/Official_repositories "Official repositories")

If needed, make sure that fuse has been started.

```
# modprobe fuse

```

## Mount FTP folder as root

Create the mount point and then mount the FTP folder.

```
# mkdir /mnt/ftp
# curlftpfs ftp.yourserver.com /mnt/ftp/ -o user=username:password

```

If you want to give other (regular) users access right, use the `allow_other` option:

```
# curlftpfs ftp.yourserver.com /mnt/ftp/ -o user=username:password,allow_other

```

Do not add space after the comma or the `allow_other` argument will not be recognized.

To use FTP in active mode add the option 'ftp_port=-':

```
# curlftpfs ftp.yourserver.com /mnt/ftp/ -o user=username:password,allow_other,ftp_port=-

```

You can add this line to /etc/fstab to mount automatically.

```
curlftpfs#USER:PASSWORD@ftp.domain.org /mnt/mydomainorg fuse auto,user,uid=1000,allow_other,_netdev 0 0

```

**Tip:** You can use codepage="_string_" when having problems with non-US English characters on servers that do not support UTF8, e.g. codepage="iso8859-1"

To prevent the password to be shown in the process list, create a `.netrc` file in the home directory of the user running curlftpfs and `chmod 600` with the following content:

```
machine ftp.yourserver.com
login username
password mypassword

```

## Mount FTP folder as normal user

You can also mount as normal user (always use the `.netrc` file for the credentials and ssl encryption!):

```
$ mkdir ~/my-server
$ curlftpfs -o ssl,utf8 ftp://my-server.tld/ ~/my-server

```

if the answer is

```
Error connecting to ftp: QUOT command failed with 500

```

then the server does not support the `utf8` option. Leave it out and all will be fine.

**Tip:** If need be try setting the encoding with for example -o codepage="iso8859-1"

To unmount:

```
$ fusermount -u ~/my-server

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=CurlFtpFS&oldid=371494](https://wiki.archlinux.org/index.php?title=CurlFtpFS&oldid=371494)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [File systems](/index.php/Category:File_systems "Category:File systems")
*   [File Transfer Protocol](/index.php/Category:File_Transfer_Protocol "Category:File Transfer Protocol")

Hidden category:

*   [Pages or sections flagged with Template:Expansion](/index.php/Category:Pages_or_sections_flagged_with_Template:Expansion "Category:Pages or sections flagged with Template:Expansion")