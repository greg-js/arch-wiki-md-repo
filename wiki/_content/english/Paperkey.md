Related articles

*   [GnuPG](/index.php/GnuPG "GnuPG")

[Paperkey](http://www.jabberwocky.com/software/paperkey/) is a command line tool to export GnuPG keys on paper. It reduces the size of the exported key, by removing the public key parts from the private key. Paperkey also includes CRC-24 checksums in the key to allow the user to check whether their private key has been restored correctly.

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 Backup](#Backup)
    *   [2.2 Restore secret key](#Restore_secret_key)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Print secret key directly](#Print_secret_key_directly)

## Installation

Install [paperkey](https://aur.archlinux.org/packages/paperkey/) from the [AUR](/index.php/AUR "AUR").

## Usage

### Backup

**Warning:** You need to have the public key available when restoring the paperkey backup! Since it's safe to have your public key available publicly, consider uploading it to a [keyserver](/index.php/GnuPG#Use_a_keyserver "GnuPG").

To create a backup of your GnuPG key, pipe the private key to paperkey:

```
$ gpg --export-secret-key *key-id* | paperkey --output *paperkey.asc*

```

### Restore secret key

To restore the secret key you need to have a file with the paperkey data and the public key. Then run the following command to import the private key to `~/.gnupg`:

```
$ paperkey --pubring *public-key.asc* --secrets *secret-key-paper.asc* | gpg --import

```

Alternatively, restore the private key to a file:

```
$ paperkey --pubring *public-key.asc* --secrets *secret-key-paper.asc* --output *secret-key.asc*

```

## Tips and tricks

### Print secret key directly

If no `--output` argument is given, paperkey will print it's output to `stdout`. It's possible to print the key directly without intermediate file, which might have security implications. To do so, install [CUPS](/index.php/CUPS "CUPS"), and pipe to `lpr`:

```
$ gpg --export-secret-key *key-id* | paperkey | lpr

```