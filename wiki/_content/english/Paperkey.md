Related articles

*   [GnuPG](/index.php/GnuPG "GnuPG")

[Paperkey](http://www.jabberwocky.com/software/paperkey/) is a command line tool to export GnuPG keys on paper. It reduces the size of the exported key, by removing the public key parts from the private key. Paperkey also includes CRC-24 checksums in the key to allow the user to check whether their private key has been restored correctly.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 Backup](#Backup)
    *   [2.2 Restore secret key](#Restore_secret_key)
        *   [2.2.1 Error: unable to parse OpenPGP packets (is this armored data?)](#Error:_unable_to_parse_OpenPGP_packets_(is_this_armored_data?))
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Print secret key directly](#Print_secret_key_directly)
    *   [3.2 Encode secret key as QR Code](#Encode_secret_key_as_QR_Code)

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

#### Error: unable to parse OpenPGP packets (is this armored data?)

If you receive this error while restoring your key, you need to dearmor your public key first:

```
$ gpg --dearmor *public-key.asc*

```

## Tips and tricks

### Print secret key directly

If no `--output` argument is given, paperkey will print it's output to `stdout`. It's possible to print the key directly without intermediate file, which might have security implications. To do so, install [CUPS](/index.php/CUPS "CUPS"), and pipe to `lpr`:

```
$ gpg --export-secret-key *key-id* | paperkey | lpr

```

### Encode secret key as QR Code

By default, paperkey will output the secret key as human readable text. While this format guarantees the ability to read and restore the printed information, it is not very convenient. The `--output-type raw` option tells paperkey to output the raw secret key data instead. This enables the use of other encodings, including machine-readable ones such as the [QR code](https://en.wikipedia.org/wiki/QR_code "wikipedia:QR code").

The [qrencode](https://www.archlinux.org/packages/?name=qrencode) program can be used for this:

```
$ gpg --export-secret-key *key-id* | paperkey --output-type raw | qrencode --8bit --output *secret-key.qr.png*

```

It is possible to increase the [error correction level](https://www.qrcode.com/en/about/error_correction.html) to maximum with the `--level H` option. This provides a lost data restoration rate of about 30% at the cost of reduced [capacity](https://www.qrcode.com/en/about/version.html). Should the secret key not fit in the QR code, the lower `Q` and `M` error correction levels are also available and give restoration rates of about 25% and 15% respectively. The default error correction level is `L` which allows restoration of about 7% of lost data.