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