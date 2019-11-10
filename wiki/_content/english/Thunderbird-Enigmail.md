[Enigmail](https://www.enigmail.net) is a Thunderbird extension that allows writing and receiving email signed and encrypted with the OpenPGP standard. It relies on the [GnuPG](/index.php/GnuPG "GnuPG").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 Sharing the public key](#Sharing_the_public_key)
    *   [2.2 Encrypting emails](#Encrypting_emails)
    *   [2.3 Decrypting emails](#Decrypting_emails)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Blank draft messages](#Blank_draft_messages)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [thunderbird-extension-enigmail](https://www.archlinux.org/packages/?name=thunderbird-extension-enigmail) package.

## Usage

### Sharing the public key

To distribute the public key one may upload it to a [keyserver](https://en.wikipedia.org/wiki/Key_server_(cryptographic) "wikipedia:Key server (cryptographic)").

### Encrypting emails

Encryption does not always work properly with emails containing HTML. It is best to use plain text by choosing *Options* > *Delivery Format* > *Plain Text Only* in the new email window.

Once the email is finished it can be signed through the *OpenPGP* menu.

### Decrypting emails

Assuming that the email was encrypted properly, just trying to open it should result in a pop-up asking to type in the keyphrase.

## Troubleshooting

### Blank draft messages

If after upgrading to [gnupg](https://www.archlinux.org/packages/?name=gnupg) v2.1 your saved draft emails have gone "blank" and show a pink bar displaying:

```
Enigmail Error - no matching private/secret key found to decrypt message; click on 'Details' button for more information

```

or, when you have a "Write" window open you repeatedly see a popup window with:

```
The email address or key ID 0x*key_id* cannot be matched to a valid, not expired OpenPGP key.
Please ensure that you have a valid OpenPGP key, and that your account settings point to that key.

```

and `gpg --list-keys` fails to show some keys that used to be there, see [GnuPG invalid packet workaround](http://jo-ke.name/wp/?p=111).

## See also

[https://addons.mozilla.org/thunderbird/addon/enigmail/](https://addons.mozilla.org/thunderbird/addon/enigmail/)