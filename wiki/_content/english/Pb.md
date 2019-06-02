Related articles

*   [Copying text from a terminal](/index.php/Copying_text_from_a_terminal "Copying text from a terminal")
*   [Pastebin](/index.php/Pastebin "Pastebin")

[pb](https://github.com/ptpb/pb) is a lightweight pastebin and URL shortener built, written in Python using Flask. The official instance is [https://ptpb.pw/](https://ptpb.pw/).

**Warning:** A pastebin should not be used for sharing confidential or private information.

**Note:** Since 2019-03-08 the [official instance is no longer available](https://github.com/ptpb/pb/issues/246).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 Server](#Server)
    *   [1.2 Client](#Client)
*   [2 Usage](#Usage)
    *   [2.1 pbpst](#pbpst)
    *   [2.2 Expiration](#Expiration)

## Installation

### Server

[Install](/index.php/Install "Install") the [nodejs-grunt](https://aur.archlinux.org/packages/nodejs-grunt/) and [pb-git](https://aur.archlinux.org/packages/pb-git/) packages, and [enable](/index.php/Enable "Enable") `pb.service`.

To configure the server, [edit](/index.php/Textedit "Textedit") the `/etc/uwsgi/pb.ini` file.

### Client

Any [download manager](/index.php/List_of_applications#Download_managers "List of applications") supporting [HTTP POST](https://en.wikipedia.org/wiki/POST_(HTTP) "w:POST (HTTP)") requests may be used, such as [curl](https://www.archlinux.org/packages/?name=curl). Alternatively, a native client may be used:

*   **pbpst** — [https://github.com/HalosGhost/pbpst](https://github.com/HalosGhost/pbpst) pbqst

	A pb client written in C. || [pbpst](https://www.archlinux.org/packages/?name=pbpst) [pbpst-git](https://aur.archlinux.org/packages/pbpst-git/)

## Usage

A paste may be created with a POST request as follows: [[1]](https://curl.haxx.se/docs/httpscripting.html#Forms_explained) [[2]](https://curl.haxx.se/docs/manpage.html#-F)

```
curl -F c=@- *https://ptpb.pw* < *file*

```

See [https://ptpb.pw](https://ptpb.pw) and [API specification](https://ptpb.pw/a) for more information.

**Note:** *pb* also provides an HTML form at the `/f` path, for example [https://ptpb.pw/f](https://ptpb.pw/f).

### pbpst

See [pbpst(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pbpst.1) and [pbpst_db(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pbpst_db.5) for usage details.

**Note:**

*   When taking standard input from a terminal, press `Ctrl+D` twice to process the data. [[3]](https://github.com/HalosGhost/pbpst/issues/32)
*   The provider may be configured with `--provider`. (defaults to [https://ptpb.pw](https://ptpb.pw))
*   By default *pbpst* only prints the URL at which the paste is available. The full output may be retrieved with `--verbose`.

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