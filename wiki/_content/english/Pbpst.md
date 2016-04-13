A command-line tool to interact with pb instances (eg [ptpb.pw](https://ptpb.pw)).

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Usage](#Usage)
    *   [3.1 Managing pastes](#Managing_pastes)
    *   [3.2 Expiration](#Expiration)
    *   [3.3 Shortening URLs](#Shortening_URLs)
*   [4 Security and privacy](#Security_and_privacy)
    *   [4.1 Signing pastes using GnuPG](#Signing_pastes_using_GnuPG)

## Installation

Install [pbpst](https://www.archlinux.org/packages/?name=pbpst) from the official repositories. Alternatively, a [Git](/index.php/Git "Git") version is available in [AUR](/index.php/Arch_User_Repository "Arch User Repository"): [pbpst-git](https://aur.archlinux.org/packages/pbpst-git/).

## Configuration

For basic use with *ptpb.pw* no additional configuration is required.

## Usage

`pbpst` is a command-line tool, run from a terminal.

To send an output of `command` to a pb instance, use:

```
$ command | pbpst -S

```

**Warning:** This command may send the data, unconditionally, to a public paste service. See [#Security and privacy](#Security_and_privacy) for more information.

To manually input the text to be pasted, `pbpst` may be invoked without the input being redirected from another command:

```
$ pbpst -S
The data to be sent. Line 1.
Line 2.
And other lines!
.
.
.

```

To end input, the stream has to be ended, typically by hitting Ctrl+D.

[xclip](https://www.archlinux.org/packages/?name=xclip) provides means for output the content of the clipboard:

```
$ xclip -o | pbpst -S

```

By default `xclip` uses `PRIMARY` [selection](/index.php/Clipboard#Background "Clipboard") and, only if it's empty, falls back to `SECONDARY` or `CLIPBOARD`. If one needs to select which one should be used, the appropriate `-selection` option should be passed to `xclip`.

To send a file:

```
$ pbpst -Sf path_to_file

```

For all of the commands above a response is received that contains an URL:

 `$ echo 'ArchLinux: livin’ on the edge!' | pbpst -S` 
```
https://ptpb.pw/qJrv

```

In this example, [https://ptpb.pw/qJrv](https://ptpb.pw/qJrv) is the URL at which the paste is available.

Finally, the protocol provides a HTML form for uploading pastes, which is always located at the resource named `/f` in the pb service's directory. For *ptpb.pw* this is [https://ptpb.pw/f](https://ptpb.pw/f).

### Managing pastes

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

### Expiration

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

### Shortening URLs

The `-s` option (*lowercase* `-s`) is used to create short URLs:

```
$ pbpst -s 'https://www.archlinux.org/'
https://ptpb.pw/HnSO

```

## Security and privacy

The pb protocol should never be used for sending confidential or private information unencrypted.

All pastes are public, given one knows their URL. A less-guessable identifier may be obtained from `pbpst` using the `-p` option, but this *does not* provide real security or privacy.

Content of all pastes is always available to the operator of the service, and anyone who can access its servers.

UUID is the only way to authenticate with a pb service. If one loses the UUID, there is no way to manage a paste. If an adversary gets an access to the UUID, they have full access to it.

The pb protocol doesn't allow the recipient to reliably determine who has created a paste.

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