Related articles

*   [List of applications/Internet#FTP clients](/index.php/List_of_applications/Internet#FTP_clients "List of applications/Internet")

**Note:** As of February 2015, curlftpfs is reported to be extremely slow, see for example [a Ubuntu bug report](https://bugs.launchpad.net/ubuntu/+source/curlftpfs/+bug/1267749) and a [stackoverflow.com question](http://stackoverflow.com/questions/24360479/ftp-with-curlftpfs-is-extremely-slow-to-the-point-it-is-impossible-to-work-with).

[CurlFtpFS](http://curlftpfs.sourceforge.net/) is a filesystem for accessing FTP hosts based on [FUSE](/index.php/FUSE "FUSE") and libcurl.

## Contents

*   [1 Installation](#Installation)
*   [2 Mount FTP folder as root](#Mount_FTP_folder_as_root)
*   [3 Mount FTP folder as normal user](#Mount_FTP_folder_as_normal_user)
*   [4 Connect to encrypted server](#Connect_to_encrypted_server)

## Installation

[Install](/index.php/Install "Install") the [curlftpfs](https://www.archlinux.org/packages/?name=curlftpfs) package.

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

**Tip:** You can use codepage="*string*" when having problems with non-US English characters on servers that do not support UTF8, e.g. codepage="iso8859-1"

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

## Connect to encrypted server

In it's default settings, CurlFtpFS will authenticate in cleartext when connecting to a non encrypted connection port. If the remote server is configured to refuse non encrypted authentification method / force encrypted authentification, CurlFtpFS will return a

```
# Error connecting to ftp: Access denied: 530

```

To authenticate to the ftp server using explicit encrypted authentification, you must specify the ssl or tsl option.

```
# curlftpfs ftp.yourserver.com /mnt/ftp/ -o ssl,user=username:password

```

If your server uses a self-generated certificate not thrusted by your computer, you can specify to ignore it

```
# curlftpfs ftp.yourserver.com /mnt/ftp/ -o ssl,no_verify_peer,no_verify_hostname,user=username:password

```

An implicit tsl mode is also available. For more details, check the manual page.