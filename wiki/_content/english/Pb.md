[pb](https://github.com/ptpb/pb) is a lightweight pastebin and URL shortener built, written in Python using Flask.

## Contents

*   [1 Security and privacy](#Security_and_privacy)
*   [2 Server](#Server)
*   [3 Client](#Client)
    *   [3.1 curl](#curl)
    *   [3.2 pbpst](#pbpst)
        *   [3.2.1 Managing pastes](#Managing_pastes)
        *   [3.2.2 Expiration](#Expiration)
        *   [3.2.3 Shortening URLs](#Shortening_URLs)
    *   [3.3 Signing pastes using GnuPG](#Signing_pastes_using_GnuPG)

## Security and privacy

The pb protocol should never be used for sending confidential or private information unencrypted.

All pastes are public, given one knows their URL. A less-guessable identifier may be obtained from `pbpst` using the `-p` option, but this *does not* provide real security or privacy.

Content of all pastes is always available to the operator of the service, and anyone who can access its servers.

UUID is the only way to authenticate with a pb service. If one loses the UUID, there is no way to manage a paste. If an adversary gets an access to the UUID, they have full access to it.

The pb protocol doesn't allow the recipient to reliably determine who has created a paste.

## Server

[Install](/index.php/Install "Install") the [nodejs-grunt](https://aur.archlinux.org/packages/nodejs-grunt/) and [pb-git](https://aur.archlinux.org/packages/pb-git/) packages, and [enable](/index.php/Enable "Enable") `pb.service`.

To configure the server, [edit](/index.php/Textedit "Textedit") the `/etc/uwsgi/pb.ini` file.

Example: [https://ptpb.pw](https://ptpb.pw)

## Client

For general usage of the command-line, see [Bash](/index.php/Bash "Bash") and [Core utilities](/index.php/Core_utilities "Core utilities").

### curl

The [curl](https://www.archlinux.org/packages/?name=curl) package is available in the [base](https://www.archlinux.org/groups/x86_64/base/) group.

*   [Forms explained](https://curl.haxx.se/docs/httpscripting.html#Forms_explained)
*   [-F/--form](https://curl.haxx.se/docs/manpage.html#-F) This lets curl emulate a filled-in form in which a user has pressed the submit button. The `@` sign forces the "content" part to be a file.
*   [ptpb.pw POST/](https://ptpb.pw/#post)
*   [HTML form](https://ptpb.pw/#get-f) ([https://ptpb.pw/f](https://ptpb.pw/f))

You can access the [ptpb.pw](https://ptpb.pw), [sprunge.us](http://sprunge.us/) and [ix.io](http://ix.io/) pastebins using curl. For example pipe the output of a command to ptpb: `*command* | curl -F c=@- https://ptpb.pw ` or upload a file (including images): `curl -F c=@- https://ptpb.pw < *file*` 

### pbpst

**Note:** Default ptpb.pw, pb instance can be configured

[Install](/index.php/Install "Install") the [pbpst](https://www.archlinux.org/packages/?name=pbpst) package, or [pbpst-git](https://aur.archlinux.org/packages/pbpst-git/) for the development version.

*   `man pbpst`
*   `man pbpst_db`

Pastes are created with `-S`, taking data from [standard input](http://mywiki.wooledge.org/BashGuide/InputAndOutput) by default. As such, shell pipes, [here documents](http://mywiki.wooledge.org/HereDocument) or here strings may be used. For example, to paste the output of the `PRIMARY` (selection) clipboard:

```
$ xclip -o | pbpst -S

```

**Note:** When taking standard input from a terminal, press `Ctrl+D` twice to process the data. [[1]](https://github.com/HalosGhost/pbpst/issues/32)

A file can be uploaded with `-Sf`:

```
$ pbpst -Sf *foo.txt*

```

For all of the commands above a response is received that contains an URL:

 `$ echo 'ArchLinux: livin’ on the edge!' | pbpst -S` 
```
https://ptpb.pw/qJrv

```

In this example, [https://ptpb.pw/qJrv](https://ptpb.pw/qJrv) is the URL at which the paste is available.

#### Managing pastes

To manage a paste, one needs its UUID. These are stored in a local database located in `[$XDG_CONFIG_HOME](/index.php/XDG_Base_Directory_support "XDG Base Directory support")/pbpst/db.json`. Since it's inconvenient to manually search through the database, a descriptive message may be attached to a paste and then searched for from command line. The example below creates a paste containing a random text and then deletes it (`-R` option):

```
$ thePaste="$(cat /dev/urandom | tr -cd [:print:] | head -c 32)"
$ echo "$thePaste"
kzx['{}uOd6olc`(AZXJc*&q\^TH(plx

$ echo "$thePaste" | pbpst -S -m 'A random test message' 
https://ptpb.pw/scrubbed

$ curl 'https://ptpb.pw/scrubbed'
kzx['{}uOd6olc`(AZXJc*&q\^TH(plx

$ pbpst -Dq test
deadbeef-dead-beef-dead-000000000000	https://ptpb.pw/scrubbed	A random test message	N/A

$ pbpst -Ru deadbeef-dead-beef-dead-000000000000
Paste deleted

$ curl 'https://ptpb.pw/scrubbed'
status: not found

$ pbpst -Dq test

```

Note that the paste is also removed from the local database, so `-Dq` can't find it.

One can't manage pastes for which one doesn't have UUID - this includes pastes that are, upon creation, matching already existing ones.

**Tip:** Finding pastes for a given URL

Currently `pbpst` can't search for pastes using their URL directly. However, the identifier from an address may be used to search the database. For an URL in form https://ptpb.pw/**RAs8**, the bold part (`RAs8`) is the identifier. It may be passed to `-Dq` to find matching entries:

```
$ pbpst -Dq RAs8
3bac4f7b-79dd-4eb4-b0d0-42b72f1c681e	https://ptpb.pw/AFUImP5F76wX_ZrottbtWiOfRAs8	-	N/A

```

#### Expiration

By default pastes are created with no expiration time. They'll last as long as the service's operator let them. `-x` option may be used to set the number of seconds after which a paste should be removed:

```
$ thePaste="$(cat /dev/urandom | tr -cd [:print:] | head -c 32)"
$ echo "$thePaste"
cnf[HiC%Ybe't]4aSeIruw5hkB.h~i^B

$ echo "$thePaste" | pbpst -S -m 'A test message that expires after 60s' -x 60
https://ptpb.pw/scrubbed

$ date; curl 'https://ptpb.pw/scrubbed'
Tue Apr 12 19:11:41 CEST 2016
cnf[HiC%Ybe't]4aSeIruw5hkB.h~i^B

$ date; curl 'https://ptpb.pw/scrubbed'
Tue Apr 12 19:13:06 CEST 2016
status: not found

```

The expired pastes, while no longer available from the remote service, are still listed in the local database:

```
$ pbpst -Dq expires
deadbeef-dead-beef-dead-1111111111	https://ptpb.pw/scrubbed	A test message that expires after 60s	1460481140

```

To prune them `-Dy` should be used:

```
$ pbpst -Dy
$ pbpst -Dq expires

```

#### Shortening URLs

The `-s` option (*lowercase* `-s`) is used to create short URLs:

```
$ pbpst -s 'https://www.archlinux.org/'
https://ptpb.pw/HnSO

```

### Signing pastes using GnuPG

Details on setting up and using GnuPG are available on [the relevant Wiki page](/index.php/GnuPG "GnuPG").

Clearsigning the output of a command:

```
$ command | gpg2 --clearsign | pbpst -S
gpg: using "FFFFFFFF" as default secret key for signing
https://ptpb.pw/scrubbed

$ curl 'https://ptpb.pw/scrubbed'
-----BEGIN PGP SIGNED MESSAGE-----
Hash: SHA256

A signed message
-----BEGIN PGP SIGNATURE-----
Version: GnuPG v2

iQEcBAEBCAAGBQJXDaNCAAoJEGEa8/dBnOWlUe4H/iviaH5Y4lx78ch5IyNSkRbp
Wzbk4aJsLYMj4idmE82Ligg4d7lZPK1q+65QZIygSeXm7Vo5/YzP7kztenHzxA0G
SvGuvML3RFwBtFb0AWqLE7Mt9zfq7PLSzhF6Qh87TklMSaluN86f5WSZmXca4SZG
BL6eRJtjy7TEWa7/hJc0b1pn851KTBqjYcX6T79UcyR3eE5KLUrqICrY5lVbq1Qm
UpstZWwgfPcchnoU2DfK3auxVRo37oHDT7N6VjEZyLP5ipbp6YPTLiCJhtjxhbLb
x+nNqFYS1USy8EFo/ftudrQSLfhMRVYuQYFalrNGK3r5dw9dAXv5gdiXIz5rsPI=
=FvyE
-----END PGP SIGNATURE-----

```

Since `gpg2` allows one to input the message to be signed, the following command may be used to manually type data to be sent:

```
$ gpg2 --clearsign | pbpst -S

```

The drawback of using clearsigning is that the process is destructive: GnuPG includes no tool for removing the signature, and the signing may change end-of-line characters. An alternative approach is to use `--sign --armour`

```
$ command | gpg2 --sign --armour | pbpst -S

```

or:

```
$ gpg2 --sign --armour | pbpst -S

```

The signature may then be verified and removed in one step with `--decrypt`:

```
$ echo 'A signed message' | gpg2 --sign --armour | pbpst -S
gpg: using "FFFFFFFF" as default secret key for signing
https://ptpb.pw/scrubbed

$ curl 'https://ptpb.pw/scrubbed' | gpg2 --decrypt
A signed message
gpg: Signature made Wed 13 Apr 2016 04:02:57 AM CEST using RSA key ID FFFFFFFF
gpg: Good signature from "-"

```