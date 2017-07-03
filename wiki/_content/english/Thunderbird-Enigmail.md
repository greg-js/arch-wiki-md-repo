[Enigmail](https://www.enigmail.net) is a [Thunderbird](/index.php/Thunderbird "Thunderbird") [extension](https://addons.mozilla.org/thunderbird/addon/enigmail/) that allows writing and receiving email signed and/or encrypted with the OpenPGP standard. It relies on the [GnuPG](/index.php/GnuPG "GnuPG").

Common packages include: [thunderbird-enigmail](https://aur.archlinux.org/packages/thunderbird-enigmail/) and [thunderbird-enigmail-bin](https://aur.archlinux.org/packages/thunderbird-enigmail-bin/).

## Contents

*   [1 Usage](#Usage)
    *   [1.1 Sharing the public key](#Sharing_the_public_key)
    *   [1.2 Encrypting emails](#Encrypting_emails)
    *   [1.3 Decrypting emails](#Decrypting_emails)
*   [2 Troubleshooting](#Troubleshooting)
    *   [2.1 Blank draft messages](#Blank_draft_messages)

## Usage

### Sharing the public key

To distribute the public key one may upload it to a [keyserver](https://en.wikipedia.org/wiki/Key_server_(cryptographic) "wikipedia:Key server (cryptographic)").

### Encrypting emails

Encryption does not always work properly with emails containing HTML. It is best to use plain text by choosing *Options > Delivery Format > Plain Text Only* in the new email window.

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