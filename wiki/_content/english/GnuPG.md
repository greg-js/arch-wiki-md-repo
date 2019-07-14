Related articles

*   [pacman/Package signing](/index.php/Pacman/Package_signing "Pacman/Package signing")
*   [Disk encryption](/index.php/Disk_encryption "Disk encryption")
*   [List of applications/Security#Encryption, signing, steganography](/index.php/List_of_applications/Security#Encryption,_signing,_steganography "List of applications/Security")

According to the [official website](https://www.gnupg.org/):

	GnuPG is a complete and free implementation of the [OpenPGP](http://openpgp.org/about/) standard as defined by [RFC4880](https://tools.ietf.org/html/rfc4880) (also known as PGP). GnuPG allows you to encrypt and sign your data and communications; it features a versatile key management system, along with access modules for all kinds of public key directories. GnuPG, also known as GPG, is a command line tool with features for easy integration with other applications. A wealth of frontend applications and libraries are available. GnuPG also provides support for S/MIME and Secure Shell (ssh).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Directory location](#Directory_location)
    *   [2.2 Configuration files](#Configuration_files)
    *   [2.3 Default options for new users](#Default_options_for_new_users)
*   [3 Usage](#Usage)
    *   [3.1 Create a key pair](#Create_a_key_pair)
    *   [3.2 Generate a revocation certificate](#Generate_a_revocation_certificate)
    *   [3.3 List keys](#List_keys)
    *   [3.4 Export your public key](#Export_your_public_key)
    *   [3.5 Import a public key](#Import_a_public_key)
    *   [3.6 Use a keyserver](#Use_a_keyserver)
    *   [3.7 Web Key Directory](#Web_Key_Directory)
    *   [3.8 Encrypt and decrypt](#Encrypt_and_decrypt)
        *   [3.8.1 Asymmetric](#Asymmetric)
        *   [3.8.2 Symmetric](#Symmetric)
*   [4 Key maintenance](#Key_maintenance)
    *   [4.1 Backup your private key](#Backup_your_private_key)
    *   [4.2 Edit your key](#Edit_your_key)
    *   [4.3 Exporting subkey](#Exporting_subkey)
    *   [4.4 Extending expiration date](#Extending_expiration_date)
    *   [4.5 Rotating subkeys](#Rotating_subkeys)
    *   [4.6 Revoke a key](#Revoke_a_key)
*   [5 Signatures](#Signatures)
    *   [5.1 Create a signature](#Create_a_signature)
        *   [5.1.1 Sign a file](#Sign_a_file)
        *   [5.1.2 Clearsign a file or message](#Clearsign_a_file_or_message)
        *   [5.1.3 Make a detached signature](#Make_a_detached_signature)
    *   [5.2 Verify a signature](#Verify_a_signature)
*   [6 gpg-agent](#gpg-agent)
    *   [6.1 Configuration](#Configuration_2)
    *   [6.2 Reload the agent](#Reload_the_agent)
    *   [6.3 pinentry](#pinentry)
    *   [6.4 Cache passwords](#Cache_passwords)
    *   [6.5 Unattended passphrase](#Unattended_passphrase)
    *   [6.6 SSH agent](#SSH_agent)
        *   [6.6.1 Set SSH_AUTH_SOCK](#Set_SSH_AUTH_SOCK)
        *   [6.6.2 Configure pinentry to use the correct TTY](#Configure_pinentry_to_use_the_correct_TTY)
        *   [6.6.3 Add SSH keys](#Add_SSH_keys)
        *   [6.6.4 Using a PGP key for SSH authentication](#Using_a_PGP_key_for_SSH_authentication)
*   [7 Smartcards](#Smartcards)
    *   [7.1 GnuPG only setups](#GnuPG_only_setups)
    *   [7.2 GnuPG with pcscd (PCSC Lite)](#GnuPG_with_pcscd_(PCSC_Lite))
        *   [7.2.1 Always use pcscd](#Always_use_pcscd)
        *   [7.2.2 Shared access with pcscd](#Shared_access_with_pcscd)
            *   [7.2.2.1 Multi applet smart cards](#Multi_applet_smart_cards)
*   [8 Tips and tricks](#Tips_and_tricks)
    *   [8.1 Different algorithm](#Different_algorithm)
    *   [8.2 Encrypt a password](#Encrypt_a_password)
    *   [8.3 Revoking a key](#Revoking_a_key)
    *   [8.4 Change trust model](#Change_trust_model)
    *   [8.5 Hide all recipient id's](#Hide_all_recipient_id's)
    *   [8.6 Using caff for keysigning parties](#Using_caff_for_keysigning_parties)
    *   [8.7 Always show long ID's and fingerprints](#Always_show_long_ID's_and_fingerprints)
    *   [8.8 Custom capabilities](#Custom_capabilities)
*   [9 Troubleshooting](#Troubleshooting)
    *   [9.1 Not enough random bytes available](#Not_enough_random_bytes_available)
    *   [9.2 su](#su)
    *   [9.3 Agent complains end of file](#Agent_complains_end_of_file)
    *   [9.4 KGpg configuration permissions](#KGpg_configuration_permissions)
    *   [9.5 GNOME on Wayland overrides SSH agent socket](#GNOME_on_Wayland_overrides_SSH_agent_socket)
    *   [9.6 mutt](#mutt)
    *   [9.7 "Lost" keys, upgrading to gnupg version 2.1](#"Lost"_keys,_upgrading_to_gnupg_version_2.1)
    *   [9.8 gpg hanged for all keyservers (when trying to receive keys)](#gpg_hanged_for_all_keyservers_(when_trying_to_receive_keys))
    *   [9.9 Smartcard not detected](#Smartcard_not_detected)
    *   [9.10 server 'gpg-agent' is older than us (x < y)](#server_'gpg-agent'_is_older_than_us_(x_<_y))
    *   [9.11 IPC connect call failed](#IPC_connect_call_failed)
*   [10 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [gnupg](https://www.archlinux.org/packages/?name=gnupg) package.

This will also install [pinentry](https://www.archlinux.org/packages/?name=pinentry), a collection of simple PIN or passphrase entry dialogs which GnuPG uses for passphrase entry. The shell script `/usr/bin/pinentry` determines which *pinentry* dialog is used, in the order described at [#pinentry](#pinentry).

If you want to use a graphical frontend or program that integrates with GnuPG, see [List of applications/Security#Encryption, signing, steganography](/index.php/List_of_applications/Security#Encryption,_signing,_steganography "List of applications/Security").

## Configuration

### Directory location

`$GNUPGHOME` is used by GnuPG to point to the directory where its configuration files are stored. By default `$GNUPGHOME` is not set and your `$HOME` is used instead; thus, you will find a `~/.gnupg` directory right after installation.

To change the default location, either run gpg this way `$ gpg --homedir *path/to/file*` or set the `GNUPGHOME` [environment variable](/index.php/Environment_variable "Environment variable").

### Configuration files

The default configuration files are `~/.gnupg/gpg.conf` and `~/.gnupg/dirmngr.conf`.

By default, the gnupg directory has its [permissions](/index.php/Permissions "Permissions") set to `700` and the files it contains have their permissions set to `600`. Only the owner of the directory has permission to read, write, and access the files. This is for security purposes and should not be changed. In case this directory or any file inside it does not follow this security measure, you will get warnings about unsafe file and home directory permissions.

Append to these files any long options you want. Do not write the two dashes, but simply the name of the option and required arguments. You will find skeleton files in `/usr/share/doc/gnupg/`. These files are copied to `~/.gnupg` the first time gpg is run if they do not exist there. Other examples are found in [#See also](#See_also).

Additionally, [pacman](/index.php/Pacman "Pacman") uses a different set of configuration files for package signature verification. See [Pacman/Package signing](/index.php/Pacman/Package_signing "Pacman/Package signing") for details.

### Default options for new users

If you want to setup some default options for new users, put configuration files in `/etc/skel/.gnupg/`. When the new user is added in system, files from here will be copied to its GnuPG home directory. There is also a simple script called *addgnupghome* which you can use to create new GnuPG home directories for existing users:

```
# addgnupghome user1 user2

```

This will add the respective `/home/user1/.gnupg/` and `/home/user2/.gnupg/` and copy the files from the skeleton directory to it. Users with existing GnuPG home directory are simply skipped.

## Usage

**Note:** Whenever a *`user-id`* is required in a command, it can be specified with your key ID, fingerprint, a part of your name or email address, etc. GnuPG is flexible on this.

### Create a key pair

Generate a key pair by typing in a terminal:

```
$ gpg --full-gen-key

```

**Tip:** Use the `--expert` option for getting alternative ciphers like [ECC](https://en.wikipedia.org/wiki/Elliptic_curve_cryptography "wikipedia:Elliptic curve cryptography"). [[1]](https://www.gnupg.org/faq/whats-new-in-2.1.html#ecc)

The command will prompt for answers to several questions. For general use most people will want:

*   the RSA (sign only) and a RSA (encrypt only) key.
*   a keysize of the default value (2048). A larger keysize of 4096 "gives us almost nothing, while costing us quite a lot"[[2]](https://www.gnupg.org/faq/gnupg-faq.html#no_default_of_rsa4096).
*   an expiration date. A period of a year is good enough for the average user. This way even if access is lost to the keyring, it will allow others to know that it is no longer valid. Later, if necessary, the expiration date can be extended without having to re-issue a new key.
*   your name and email address. You can add multiple identities to the same key later (*e.g.*, if you have multiple email addresses you want to associate with this key).
*   *no* optional comment. Since the semantics of the comment field are [not well-defined](https://lists.gnupg.org/pipermail/gnupg-devel/2015-July/030150.html), it has limited value for identification.
*   [a secure passphrase](/index.php/Security#Choosing_secure_passwords "Security").

**Note:** The name and email address you enter here will be seen by anybody who imports your key.

### Generate a revocation certificate

After generating your key, one of the first things you should do is create a revocation certificate:

```
$ gpg --gen-revoke --armor --output=*revocation_certificate.asc* *user-id*

```

This certificate can be used to [revoke your key](#Revoke_a_key) if it is ever lost or compromised.

**Warning:** Anyone with access to the revocation certificate can revoke your key. Protect your revocation certificate like you protect your secret keys. Print it out, save it on a disk, and store it safely. It will be short enough that you can type it back in by hand without much effort if you just print it out.

### List keys

To list keys in your public key ring:

```
$ gpg --list-keys

```

To list keys in your secret key ring:

```
$ gpg --list-secret-keys

```

### Export your public key

gpg's main usage is to ensure confidentiality of exchanged messages via public-key cryptography. With it each user distributes the public key of their keyring, which can be used by others to encrypt messages to the user. The private key must *always* be kept private, otherwise confidentiality is broken. See [w:Public-key cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography "w:Public-key cryptography") for examples about the message exchange.

So, in order for others to send encrypted messages to you, they need your public key.

To generate an ASCII version of a user's public key to file `*public.key*` (e.g. to distribute it by e-mail):

```
$ gpg --output *public.key* --armor --export *user-id*

```

Alternatively, or in addition, you can [#Use a keyserver](#Use_a_keyserver) to share your key.

**Tip:** Add `--no-emit-version` to avoid printing the version number, or add the corresponding setting to your configuration file.

### Import a public key

In order to encrypt messages to others, as well as verify their signatures, you need their public key. To import a public key with file name `*public.key*` to your public key ring:

```
$ gpg --import *public.key*

```

Alternatively, [#Use a keyserver](#Use_a_keyserver) to find a public key.

### Use a keyserver

You can register your key with a public PGP key server, so that others can retrieve your key without having to contact you directly:

```
$ gpg --send-keys *key-id*

```

**Warning:** Once a key has been submitted to a keyserver, it cannot be deleted from the server.[[3]](https://pgp.mit.edu/faq.html)

**Tip:** You can access your *key-id* by `$ gpg --list-secret-keys --keyid-format=LONG <email>`. The *key-id* is the hash-key provided in the sec line.

To find out details of a key on the keyserver, without importing it, do:

```
$ gpg --search-keys *user-id*

```

To import a key from a key server:

```
$ gpg --recv-keys *key-id*

```

**Warning:**

*   You should verify the authenticity of the retrieved public key by comparing its fingerprint with one that the owner published on an independent source(s) (e.g., contacting the person directly). See [Wikipedia:Public key fingerprint](https://en.wikipedia.org/wiki/Public_key_fingerprint "wikipedia:Public key fingerprint") for more information.
*   Using a short ID may encounter collisions. All keys will be imported that have the short ID. To avoid this, use the full fingerprint or long key ID when receiving a key.[[4]](https://lkml.org/lkml/2016/8/15/445)

**Tip:**

*   Adding `keyserver-options auto-key-retrieve` to `gpg.conf` will automatically fetch keys from the key server as needed, but this can be considered a **privacy violation**; see "web bug" in [gpg(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/gpg.1).
*   An alternative key server is `pool.sks-keyservers.net` and can be specified with `keyserver` in `dirmngr.conf`; see also [wikipedia:Key server (cryptographic)#Keyserver examples](https://en.wikipedia.org/wiki/Key_server_(cryptographic)#Keyserver_examples "wikipedia:Key server (cryptographic)").
*   If your network blocks ports used for hkp/hkps, you may need to specify port 80, i.e. `pool.sks-keyservers.net:80`
*   If receiving GPG fails with the following error message: `gpg: keyserver receive failed: Connection refused`, please check your DNS servers or use others.
*   You can connect to the keyserver over [Tor](/index.php/Tor "Tor") with [Tor#Torsocks](/index.php/Tor#Torsocks "Tor"). Or using the `--use-tor` command line option. See this [GnuPG blog post](https://gnupg.org/blog/20151224-gnupg-in-november-and-december.html) for more information.
*   You can connect to a keyserver using a proxy by setting the `http_proxy` [environment variable](/index.php/Environment_variable "Environment variable") and setting `honor-http-proxy` in `dirmngr.conf`. Alternatively, set `http-proxy *host[:port]*` in `dirmngr.conf`, overriding the `http_proxy` environment variable. [Restart](/index.php/Restart "Restart") the `dirmngr.service` [user service](/index.php/Systemd/User "Systemd/User") for the changes to take effect.
*   If you wish to import a key ID to install a specific Arch Linux package, see [pacman/Package signing#Managing the keyring](/index.php/Pacman/Package_signing#Managing_the_keyring "Pacman/Package signing") and [Makepkg#Signature checking](/index.php/Makepkg#Signature_checking "Makepkg").

The most common keyservers:

*   [SKS Keyserver Pool](https://sks-keyservers.net): federated, no verification, keys cannot be deleted.
*   [Mailvelope Keyserver](https://keys.mailvelope.com): central, verification of email IDs, keys can be deleted.
*   [keys.openpgp.org](https://keys.openpgp.org): central, verification of email IDs, keys can be deleted, no third-party signatures (i.e. no Web of Trust support).

### Web Key Directory

The Web Key Service (WKS) protocol is a new [standard](https://datatracker.ietf.org/doc/draft-koch-openpgp-webkey-service/) for key distribution, where the email domain provides its own key server called [Web Key Directory (WKD)](https://wiki.gnupg.org/WKD). When encrypting to an email address (e.g. `user@example.com`), GnuPG (>=2.1.16) will query the domain (`example.com`) via HTTPS for the public OpenPGP key if it’s not already in the local keyring. Note that the option `auto-key-locate` must contain `wkd` (which is the default).

```
# gpg --recipient *user@example.org* --auto-key-locate local,wkd --encrypt *doc*

```

See the [GnuPG Wiki](https://wiki.gnupg.org/WKD#Implementations) for a list of email providers that support WKD. If you control the domain of your email address yourself, you can follow [this guide](https://wiki.gnupg.org/WKDHosting) to enable WKD for your domain. To check if your key can be found in the WKD you can use [this webinterface](https://metacode.biz/openpgp/web-key-directory).

### Encrypt and decrypt

#### Asymmetric

You need to [#Import a public key](#Import_a_public_key) of a user before encrypting (options `--encrypt` or `-e`) a file or message to that recipient (options `--recipient` or `-r`). Additionally you need to [#Create a key pair](#Create_a_key_pair) if you have not already done so.

To encrypt a file with the name *doc*, use:

```
$ gpg --recipient *user-id* --encrypt *doc*

```

To decrypt (option `--decrypt` or `-d`) a file with the name *doc*.gpg encrypted with your public key, use:

```
$ gpg --output *doc* --decrypt *doc*.gpg

```

*gpg* will prompt you for your passphrase and then decrypt and write the data from *doc*.gpg to *doc*. If you omit the `-o` (`--output`) option, *gpg* will write the decrypted data to stdout.

**Tip:**

*   Add `--armor` to encrypt a file using ASCII armor (suitable for copying and pasting a message in text format)
*   Use `-R *user-id*` or `--hidden-recipient *user-id*` instead of `-r` to not put the recipient key IDs in the encrypted message. This helps to hide the receivers of the message and is a limited countermeasure against traffic analysis.
*   Add `--no-emit-version` to avoid printing the version number, or add the corresponding setting to your configuration file.
*   You can use gnupg to encrypt your sensitive documents by using your own user-id as recipient or by using the `--default-recipient-self` flag instead; however, you can only do this one file at a time, although you can always tarball various files and then encrypt the tarball. See also [Disk encryption#Available methods](/index.php/Disk_encryption#Available_methods "Disk encryption") if you want to encrypt directories or a whole file-system.

#### Symmetric

Symmetric encryption does not require the generation of a key pair and can be used to simply encrypt data with a passphrase. Simply use `--symmetric` or `-c` to perform symmetic encryption:

```
$ gpg -c *doc*

```

The following example:

*   Encrypts `*doc*` with a symmetric cipher using a passphrase
*   Uses the AES-256 cipher algorithm to encrypt the passphrase
*   Uses the SHA-512 digest algorithm to mangle the passphrase
*   Mangles the passphrase for 65536 iterations

```
$ gpg -c --s2k-cipher-algo AES256 --s2k-digest-algo SHA512 --s2k-count 65536 *doc*

```

To decrypt a symmetrically encrypted `*doc*.gpg` using a passphrase and output decrypted contents into the same directory as `*doc*` do:

```
$ gpg --output *doc* --decrypt *doc*.gpg

```

## Key maintenance

### Backup your private key

To backup your private key do the following:

```
$ gpg --export-secret-keys --armor *<user-id>* > *privkey.asc*

```

Note that *gpg* release 2.1 changed default behaviour so that the above command enforces a passphrase protection, even if you deliberately chose not to use one on key creation. This is because otherwise anyone who gains access to the above exported file would be able to encrypt and sign documents as if they were you *without* needing to know your passphrase.

**Warning:** The passphrase is usually the weakest link in protecting your secret key. Place the private key in a safe place on a different system/device, such as a locked container or encrypted drive. It is the only safety you have to regain control to your keyring in case of, for example, a drive failure, theft or worse.

To import the backup of your private key:

```
$ gpg --import *privkey.asc*

```

**Tip:** [Paperkey](/index.php/Paperkey "Paperkey") can be used to export private keys as human readable text or machine readable barcodes that can be printed on paper and archived.

### Edit your key

Running the `gpg --edit-key *<user-id>*` command will present a menu which enables you to do most of your key management related tasks.

Some useful commands in the edit key sub menu:

```
> passwd       # change the passphrase
> clean        # compact any user ID that is no longer usable (e.g revoked or expired)
> revkey       # revoke a key
> addkey       # add a subkey to this key
> expire       # change the key expiration time
> adduid       # add additional names, comments, and email addresses
> addphoto     # add photo to key (must be JPG, 240x288 recommended, enter full path to image when prompted)

```

Type `help` in the edit key sub menu for more commands.

**Tip:** If you have multiple email accounts you can add each one of them as an identity, using `adduid` command. You can then set your favourite one as `primary`.

### Exporting subkey

If you plan to use the same key across multiple devices, you may want to strip out your master key and only keep the bare minimum encryption subkey on less secure systems.

First, find out which subkey you want to export.

```
$ gpg --list-secret-keys

```

Select only that subkey to export.

```
$ gpg -a --export-secret-subkeys [subkey id]! > /tmp/subkey.gpg

```

**Warning:** If you forget to add the !, all of your subkeys will be exported.

At this point you could stop, but it is most likely a good idea to change the passphrase as well. Import the key into a temporary folder.

```
$ gpg --homedir /tmp/gpg --import /tmp/subkey.gpg
$ gpg --homedir /tmp/gpg --edit-key *<user-id>*
> passwd
> save
$ gpg --homedir /tmp/gpg -a --export-secret-subkeys *[subkey id]*! > /tmp/subkey.altpass.gpg

```

**Note:** You will get a warning that the master key was not available and the password was not changed, but that can safely be ignored as the subkey password was.

At this point, you can now use `/tmp/subkey.altpass.gpg` on your other devices.

### Extending expiration date

**Warning:** **Never** delete your expired or revoked subkeys unless you have a good reason. Doing so will cause you to lose the ability to decrypt files encrypted with the old subkey. Please **only** delete expired or revoked keys from other users to clean your keyring.

It is good practice to set an expiration date on your subkeys, so that if you lose access to the key (e.g. you forget the passphrase) the key will not continue to be used indefinitely by others. When the key expires, it is relatively straight-forward to extend the expiration date:

```
$ gpg --edit-key *<user-id>*
> expire

```

You will be prompted for a new expiration date, as well as the passphrase for your secret key, which is used to sign the new expiration date.

Repeat this for any further subkeys that have expired:

```
> key 1
> expire

```

Finally, save the changes and quit:

```
> save

```

Update it to a keyserver.

```
$ gpg --keyserver pgp.mit.edu --send-keys *<user-id>*

```

Alternatively, if you use this key on multiple computers, you can export the public key (with new signed expiration dates) and import it on those machines:

```
$ gpg --export *<user-id>* > pubkey.gpg
$ gpg --import pubkey.gpg

```

There is no need to re-export your secret key or update your backups: the master secret key itself never expires, and the signature of the expiration date left on the public key and subkeys is all that is needed.

### Rotating subkeys

**Warning:** **Never** delete your expired or revoked subkeys unless you have a good reason. Doing so will cause you to lose the ability to decrypt files encrypted with the old subkey. Please **only** delete expired or revoked keys from other users to clean your keyring.

Alternatively, if you prefer to stop using subkeys entirely once they have expired, you can create new ones. Do this a few weeks in advance to allow others to update their keyring.

**Tip:** You do not need to create a new key simply because it is expired. You can extend the expiration date, see the section [#Extending expiration date](#Extending_expiration_date).

Create new subkey (repeat for both signing and encrypting key)

```
$ gpg --edit-key *<user-id>*
> addkey

```

And answer the following questions it asks (see [#Create a key pair](#Create_a_key_pair) for suggested settings).

Save changes

```
> save

```

Update it to a keyserver.

```
$ gpg --keyserver pgp.mit.edu --send-keys *<user-id>*

```

You will also need to export a fresh copy of your secret keys for backup purposes. See the section [#Backup your private key](#Backup_your_private_key) for details on how to do this.

**Tip:** Revoking expired subkeys is unnecessary and arguably bad form. If you are constantly revoking keys, it may cause others to lack confidence in you.

### Revoke a key

If you lose your secret key or it is compromised, you will want to revoke your key by first [importing your public key](#Import_a_public_key) if you not longer have access to the keypair. Then, you will import your [revocation certificate](#Generate_a_revocation_certificate):

```
$ gpg --import revocation_certificate.asc

```

You now need to make your now-revoked key public. If you used a keyserver, [send the key to the keyserver](#Use_a_keyserver). Otherwise, distribute the revoked key to your colleagues.

## Signatures

Signatures certify and timestamp documents. If the document is modified, verification of the signature will fail. Unlike encryption which uses public keys to encrypt a document, signatures are created with the user's private key. The recipient of a signed document then verifies the signature using the sender's public key.

### Create a signature

#### Sign a file

To sign a file use the `--sign` or `-s` flag:

```
$ gpg --output *doc*.sig --sign *doc*

```

`*doc*.sig` contains both the compressed content of the original file `*doc*` and the signature in a binary format, but the file is not encrypted. However, you can combine signing with [encrypting](#Encrypt_and_decrypt).

#### Clearsign a file or message

To sign a file without compressing it into binary format use:

```
$ gpg --output *doc*.sig --clearsign *doc*

```

Here both the content of the original file `*doc*` and the signature are stored in human-readable form in `*doc*.sig`.

#### Make a detached signature

To create a separate signature file to be distributed separately from the document or file itself, use the `--detach-sig` flag:

```
$ gpg --output *doc*.sig --detach-sig *doc*

```

Here the signature is stored in `*doc*.sig`, but the contents of `*doc*` are not stored in it. This method is often used in distributing software projects to allow users to verify that the program has not been modified by a third party.

### Verify a signature

To verify a signature use the `--verify` flag:

```
$ gpg --verify *doc*.sig

```

where `*doc*.sig` is the signed file containing the signature you wish to verify.

If you are verifying a detached signature, both the signed data file and the signature file must be present when verifying. For example, to verify Arch Linux's latest iso you would do:

```
$ gpg --verify archlinux-*version*.iso.sig

```

where `archlinux-*version*.iso` must be located in the same directory.

You can also specify the signed data file with a second argument:

```
$ gpg --verify archlinux-*version*.iso.sig */path/to/*archlinux-*version*.iso

```

If a file has been encrypted in addition to being signed, simply [decrypt](#Encrypt_and_decrypt) the file and its signature will also be verified.

## gpg-agent

*gpg-agent* is mostly used as daemon to request and cache the password for the keychain. This is useful if GnuPG is used from an external program like a mail client. [gnupg](https://www.archlinux.org/packages/?name=gnupg) comes with [systemd user](/index.php/Systemd/User "Systemd/User") sockets which are enabled by default. These sockets are `gpg-agent.socket`, `gpg-agent-extra.socket`, `gpg-agent-browser.socket`, `gpg-agent-ssh.socket`, and `dirmngr.socket`.

*   The main `gpg-agent.socket` is used by *gpg* to connect to the *gpg-agent* daemon.
*   The intended use for the `gpg-agent-extra.socket` on a local system is to set up a Unix domain socket forwarding from a remote system. This enables to use *gpg* on the remote system without exposing the private keys to the remote system. See [gpg-agent(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/gpg-agent.1) for details.
*   The `gpg-agent-browser.socket` allows web browsers to access the *gpg-agent* daemon.
*   The `gpg-agent-ssh.socket` can be used by [SSH](/index.php/SSH "SSH") to cache [SSH keys](/index.php/SSH_keys "SSH keys") added by the *ssh-add* program. See [#SSH agent](#SSH_agent) for the necessary configuration.
*   The `dirmngr.socket` starts a GnuPG daemon handling connections to keyservers.

**Note:** If you use non-default GnuPG [#Directory location](#Directory_location), you will need to [edit](/index.php/Edit "Edit") all socket files to use the values of `gpgconf --list-dirs`.

### Configuration

gpg-agent can be configured via `~/.gnupg/gpg-agent.conf` file. The configuration options are listed in [gpg-agent(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/gpg-agent.1). For example you can change cache ttl for unused keys:

 `~/.gnupg/gpg-agent.conf` 
```
default-cache-ttl 3600

```

**Tip:** To cache your passphrase for the whole session, please run the following command:
```
$ /usr/lib/gnupg/gpg-preset-passphrase --preset XXXXX

```

where XXXXX is the keygrip. You can get its value when running `gpg --with-keygrip -K`. The passphrase will be stored until `gpg-agent` is restarted. If you set up `default-cache-ttl` value, it will take precedence.

### Reload the agent

After changing the configuration, reload the agent using *gpg-connect-agent*:

```
$ gpg-connect-agent reloadagent /bye

```

The command should print `OK`.

However in some cases only the restart may not be sufficient, like when `keep-screen` has been added to the agent configuration. In this case you firstly need to kill the ongoing gpg-agent process and then you can restart it as was explained above.

### pinentry

`gpg-agent` can be configured via the `pinentry-program` stanza to use a particular [pinentry](https://www.archlinux.org/packages/?name=pinentry) user interface when prompting the user for a passphrase. For example:

 `~/.gnupg/gpg-agent.conf` 
```
pinentry-program /usr/bin/pinentry-curses

```

There are other pinentry programs that you can choose from - see `pacman -Ql pinentry | grep /usr/bin/`.

**Tip:** In order to use `/usr/bin/pinentry-kwallet` you have to install the [kwalletcli](https://aur.archlinux.org/packages/kwalletcli/) package.

Remember to [reload the agent](#Reload_the_agent) after making changes to the configuration.

### Cache passwords

`max-cache-ttl` and `default-cache-ttl` defines how many seconds gpg-agent should cache the passwords. To enter a password once a session, set them to something very high, for instance:

 `gpg-agent.conf` 
```
max-cache-ttl 60480000
default-cache-ttl 60480000

```

For password caching in SSH emulation mode, set `default-cache-ttl-ssh` and `max-cache-ttl-ssh` instead, for example:

 `gpg-agent.conf` 
```
default-cache-ttl-ssh 60480000
max-cache-ttl-ssh 60480000

```

### Unattended passphrase

Starting with GnuPG 2.1.0 the use of gpg-agent and pinentry is required, which may break backwards compatibility for passphrases piped in from STDIN using the `--passphrase-fd 0` commandline option. In order to have the same type of functionality as the older releases two things must be done:

First, edit the gpg-agent configuration to allow *loopback* pinentry mode:

 `~/.gnupg/gpg-agent.conf` 
```
allow-loopback-pinentry

```

[Reload the agent](#Reload_the_agent) if it is running to let the change take effect.

Second, either the application needs to be updated to include a commandline parameter to use loopback mode like so:

```
$ gpg --pinentry-mode loopback ...

```

...or if this is not possible, add the option to the configuration:

 `~/.gnupg/gpg.conf` 
```
pinentry-mode loopback

```

**Note:** The upstream author indicates setting `pinentry-mode loopback` in `gpg.conf` may break other usage, using the commandline option should be preferred if at all possible. [[5]](https://bugs.g10code.com/gnupg/issue1772)

### SSH agent

*gpg-agent* has OpenSSH agent emulation. If you already use the GnuPG suite, you might consider using its agent to also cache your [SSH keys](/index.php/SSH_keys "SSH keys"). Additionally, some users may prefer the PIN entry dialog GnuPG agent provides as part of its passphrase management.

#### Set SSH_AUTH_SOCK

You have to set `SSH_AUTH_SOCK` so that SSH will use *gpg-agent* instead of *ssh-agent*. To make sure each process can find your *gpg-agent* instance regardless of e.g. the type of shell it is child of use [pam_env](/index.php/Environment_variables#Using_pam_env "Environment variables").

 `~/.pam_environment` 
```
SSH_AGENT_PID	DEFAULT=
SSH_AUTH_SOCK	DEFAULT="${XDG_RUNTIME_DIR}/gnupg/S.gpg-agent.ssh"
```

**Note:**

*   If you set your `SSH_AUTH_SOCK` manually (such as in this pam_env example), keep in mind that your socket location may be different if you are using a custom `GNUPGHOME`. You can use the following bash example, or change `SSH_AUTH_SOCK` to the value of `gpgconf --list-dirs agent-ssh-socket`.
*   If GNOME Keyring is installed, it is necessary to [deactivate](/index.php/GNOME/Keyring#Disable_keyring_daemon_components "GNOME/Keyring") its ssh component. Otherwise, it will overwrite `SSH_AUTH_SOCK`.

Alternatively, depend on Bash. This works for non-standard socket locations as well:

 `~/.bashrc` 
```
unset SSH_AGENT_PID
if [ "${gnupg_SSH_AUTH_SOCK_by:-0}" -ne $$ ]; then
  export SSH_AUTH_SOCK="$(gpgconf --list-dirs agent-ssh-socket)"
fi
```

**Note:** The test involving the `gnupg_SSH_AUTH_SOCK_by` variable is for the case where the agent is started as `gpg-agent --daemon /bin/sh`, in which case the shell inherits the `SSH_AUTH_SOCK` variable from the parent, *gpg-agent* [[6]](http://git.gnupg.org/cgi-bin/gitweb.cgi?p=gnupg.git;a=blob;f=agent/gpg-agent.c;hb=7bca3be65e510eda40572327b87922834ebe07eb#l1307).

#### Configure pinentry to use the correct TTY

Also set the GPG_TTY and refresh the TTY in case user has switched into an X session as stated in [gpg-agent(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/gpg-agent.1). For example:

 `~/.bashrc` 
```
export GPG_TTY=$(tty)
gpg-connect-agent updatestartuptty /bye >/dev/null
```

#### Add SSH keys

Once *gpg-agent* is running you can use *ssh-add* to approve keys, following the same steps as for [ssh-agent](/index.php/SSH_keys#ssh-agent "SSH keys"). The list of approved keys is stored in the `~/.gnupg/sshcontrol` file.

Once your key is approved, you will get a *pinentry* dialog every time your passphrase is needed. For password caching see [#Cache passwords](#Cache_passwords).

#### Using a PGP key for SSH authentication

You can also use your PGP key as an SSH key. This requires a key with the `Authentication` capability (see [#Custom capabilities](#Custom_capabilities)). There are various benefits gained by using a PGP key for SSH authentication, including:

*   Reduced key maintenance, as you will no longer need to maintain an SSH key.
*   The ability to store the authentication key on a smartcard. GnuPG will automatically detect the key when the card is available, and add it to the agent (check with `ssh-add -l` or `ssh-add -L`). The comment for the key should be something like: `openpgp:*key-id*` or `cardno:*card-id*`.

To retrieve the public key part of your GPG/SSH key, run `gpg --export-ssh-key *gpg-key*`.

Unless you have your GPG key on a keycard, you need to add your key to `$GNUPGHOME/sshcontrol` to be recognized as a SSH key. If your key is on a keycard, its keygrip is added to `sshcontrol` implicitly. If not, get the keygrip of your key this way:

 `$ gpg --list-keys --with-keygrip` 
```
sub   rsa4096 2018-07-25 [A]
      Keygrip = *1531C8084D16DC4C36911F1585AF0ACE7AAFD7E7*
```

Then edit `sshcontrol` like this. Adding the keygrip is a one-time action; you will not need to edit the file again, unless you are adding additional keys.

 `$GNUPGHOME/sshcontrol` 
```
*1531C8084D16DC4C36911F1585AF0ACE7AAFD7E7*

```

## Smartcards

GnuPG uses *scdaemon* as an interface to your smartcard reader, please refer to the [man page](/index.php/Man_page "Man page") [scdaemon(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/scdaemon.1) for details.

### GnuPG only setups

**Note:** To allow scdaemon direct access to USB smartcard readers the optional dependency [libusb-compat](https://www.archlinux.org/packages/?name=libusb-compat) must be installed

If you do not plan to use other cards but those based on GnuPG, you should check the `reader-port` parameter in `~/.gnupg/scdaemon.conf`. The value '0' refers to the first available serial port reader and a value of '32768' (default) refers to the first USB reader.

### GnuPG with pcscd (PCSC Lite)

[pcscd(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pcscd.8) is a daemon which handles access to smartcard (SCard API). If GnuPG's scdaemon fails to connect the smartcard directly (e.g. by using its integrated CCID support), it will fallback and try to find a smartcard using the PCSC Lite driver.

To use pscsd [install](/index.php/Install "Install") [pcsclite](https://www.archlinux.org/packages/?name=pcsclite) and [ccid](https://www.archlinux.org/packages/?name=ccid). Then [start](/index.php/Start "Start") and/or [enable](/index.php/Enable "Enable") `pcscd.service`. Alternatively start and/or enable `pcscd.socket` to activate the daemon when needed.

#### Always use pcscd

If you are using any smartcard with an opensc driver (e.g.: ID cards from some countries) you should pay some attention to GnuPG configuration. Out of the box you might receive a message like this when using `gpg --card-status`

```
gpg: selecting openpgp failed: ec=6.108

```

By default, scdaemon will try to connect directly to the device. This connection will fail if the reader is being used by another process. For example: the pcscd daemon used by OpenSC. To cope with this situation we should use the same underlying driver as opensc so they can work well together. In order to point scdaemon to use pcscd you should remove `reader-port` from `~/.gnupg/scdaemon.conf`, specify the location to `libpcsclite.so` library and disable ccid so we make sure that we use pcscd:

 `~/.gnupg/scdaemon.conf` 
```
pcsc-driver /usr/lib/libpcsclite.so
card-timeout 5
disable-ccid

```

Please check [scdaemon(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/scdaemon.1) if you do not use OpenSC.

#### Shared access with pcscd

GnuPG `scdaemon` is the only popular `pcscd` client that uses `PCSC_SHARE_EXCLUSIVE` flag when connecting to `pcscd`. Other clients like OpenSC PKCS#11 that are used by browsers and programs listed in [Electronic identification](/index.php/Electronic_identification "Electronic identification") are using `PCSC_SHARE_SHARED` that allows simultaneous access to single smartcard. `pcscd` will not give exclusive access to smartcard while there are other clients connected. This means that to use GnuPG smartcard features you must before have to close all your open browser windows or do some other inconvenient operations. There is a out of tree patch in [GPGTools/MacGPG2](https://github.com/GPGTools/MacGPG2/blob/dev/patches/gnupg/scdaemon_shared-access.patch) git repo that enables `scdaemon` to use shared access but GnuPG developers are against allowing this because when one `pcscd` client authenticates the smartcard then some other malicious `pcscd` clients could do authenticated operations with the card without you knowing. You can read full mailing list thread [here](https://lists.gnupg.org/pipermail/gnupg-devel/2015-September/030247.html).

If you accept the security risk then you can use the patch from [GPGTools/MacGPG2](https://github.com/GPGTools/MacGPG2/blob/dev/patches/gnupg/scdaemon_shared-access.patch) git repo or use [gnupg-scdaemon-shared-access](https://aur.archlinux.org/packages/gnupg-scdaemon-shared-access/) package. After patching your `scdaemon` you can enable shared access by modifying your `scdaemon.conf` file and adding `shared-access` line end of it.

##### Multi applet smart cards

When using [YubiKeys](/index.php/YubiKey "YubiKey") or other multi applet USB dongles with OpenSC PKCS#11 may run into problems where OpenSC switches your Yubikey from OpenPGP to PIV applet, breaking the `scdaemon`.

You can hack around the problem by forcing OpenSC to also use the OpenPGP applet. Open `/etc/opensc.conf` file, search for Yubikey and change the `driver = "PIV-II";` line to `driver = "openpgp";`. If there is no such entry, use `pcsc_scan`. Search for the Answer to Reset `ATR: 12 34 56 78 90 AB CD ...`. Then create a new entry.

 `/etc/opensc.conf` 
```
...
card_atr 12:23:34:45:67:89:ab:cd:... {
    name = "YubiKey Neo";
    driver = "openpgp"
}
...
```

After that you can test with `pkcs11-tool -O --login` that the OpenPGP applet is selected by default. Other PKCS#11 clients like browsers may need to be restarted for that change to be applied.

## Tips and tricks

### Different algorithm

You may want to use stronger algorithms:

 `~/.gnupg/gpg.conf` 
```
...

personal-digest-preferences SHA512
cert-digest-algo SHA512
default-preference-list SHA512 SHA384 SHA256 SHA224 AES256 AES192 AES CAST5 ZLIB BZIP2 ZIP Uncompressed
personal-cipher-preferences TWOFISH CAMELLIA256 AES 3DES

```

In the latest version of GnuPG, the default algorithms used are SHA256 and AES, both of which are secure enough for most people. However, if you are using a version of GnuPG older than 2.1, or if you want an even higher level of security, then you should follow the above step.

### Encrypt a password

It can be useful to encrypt some password, so it will not be written in clear on a configuration file. A good example is your email password.

First create a file with your password. You **need** to leave **one** empty line after the password, otherwise gpg will return an error message when evaluating the file.

Then run:

```
$ gpg -e -a -r *<user-id>* *your_password_file*

```

`-e` is for encrypt, `-a` for armor (ASCII output), `-r` for recipient user ID.

You will be left with a new `*your_password_file*.asc` file.

**Tip:** [pass](/index.php/Pass "Pass") automates this process.

### Revoking a key

**Warning:**

*   Anybody having access to your revocation certificate can revoke your key, rendering it useless.
*   Key revocation should only be performed if your key is compromised or lost, or you forget your passphrase.

Revocation certificates are automatically generated for newly generated keys, although one can be generated manually by the user later. These are located at `~/.gnupg/openpgp-revocs.d/`. The filename of the certificate is the fingerprint of the key it will revoke.

To revoke your key, simply import the revocation certificate:

```
$ gpg --import *<fingerprint>*.rev

```

Then [send the key](#Use_a_keyserver) that was revoked back to your keyserver(s) of choice.

### Change trust model

By default GnuPG uses the [Web of Trust](https://en.wikipedia.org/wiki/Web_of_Trust "wikipedia:Web of Trust") as the trust model. You can change this to [Trust on first use](https://en.wikipedia.org/wiki/Trust_on_first_use "wikipedia:Trust on first use") by adding `--trust-model=tofu` when adding a key or adding this option to your GnuPG configuration file. More details are in [this email to the GnuPG list](https://lists.gnupg.org/pipermail/gnupg-devel/2015-October/030341.html).

### Hide all recipient id's

By default the recipient's key ID is in the encrypted message. This can be removed at encryption time for a recipient by using `hidden-recipient *<user-id>*`. To remove it for all recipients add `throw-keyids` to your configuration file. This helps to hide the receivers of the message and is a limited countermeasure against traffic analysis. (Using a little social engineering anyone who is able to decrypt the message can check whether one of the other recipients is the one he suspects.) On the receiving side, it may slow down the decryption process because all available secret keys must be tried (*e.g.* with `--try-secret-key *<user-id>*`).

### Using caff for keysigning parties

To allow users to validate keys on the keyservers and in their keyrings (i.e. make sure they are from whom they claim to be), PGP/GPG uses the [Web of Trust](https://en.wikipedia.org/wiki/Web_of_Trust "wikipedia:Web of Trust"). Keysigning parties allow users to get together at a physical location to validate keys. The [Zimmermann-Sassaman](https://en.wikipedia.org/wiki/Zimmermann%E2%80%93Sassaman_key-signing_protocol "wikipedia:Zimmermann–Sassaman key-signing protocol") key-signing protocol is a way of making these very effective. [Here](http://www.cryptnet.net/fdp/crypto/keysigning_party/en/keysigning_party.html) you will find a how-to article.

For an easier process of signing keys and sending signatures to the owners after a keysigning party, you can use the tool *caff*. It can be installed from the AUR with the package [caff-git](https://aur.archlinux.org/packages/caff-git/).

To send the signatures to their owners you need a working [MTA](https://en.wikipedia.org/wiki/Message_transfer_agent "wikipedia:Message transfer agent"). If you do not have already one, install [msmtp](/index.php/Msmtp "Msmtp").

### Always show long ID's and fingerprints

To always show long key ID's add `keyid-format 0xlong` to your configuration file. To always show full fingerprints of keys, add `with-fingerprint` to your configuration file.

### Custom capabilities

For further customization also possible to set custom capabilities to your keys. The following capabilities are available:

*   Certify (only for master keys) - allows the key to create subkeys, mandatory for master keys.
*   Sign - allows the key to create cryptographic signatures that others can verify with the public key.
*   Encrypt - allows anyone to encrypt data with the public key, that only the private key can decrypt.
*   Authenticate - allows the key to authenticate with various non-GnuPG programs. The key can be used as e.g. an SSH key.

It's possible to specify the capabilities of the master key, by running:

```
$ gpg --full-generate-key --expert

```

And select an option that allows you to set your own capabilities.

Comparably, to specify custom capabilities for subkeys, add the `--expert` flag to `gpg --edit-key`, see [#Edit your key](#Edit_your_key) for more information.

## Troubleshooting

### Not enough random bytes available

When generating a key, gpg can run into this error:

```
Not enough random bytes available. Please do some other work to give the OS a chance to collect more entropy!

```

To check the available entropy, check the kernel parameters:

```
$ cat /proc/sys/kernel/random/entropy_avail

```

A healthy Linux system with a lot of entropy available will have return close to the full 4,096 bits of entropy. If the value returned is less than 200, the system is running low on entropy.

To solve it, remember you do not often need to create keys and best just do what the message suggests (e.g. create disk activity, move the mouse, edit the wiki - all will create entropy). If that does not help, check which service is using up the entropy and consider stopping it for the time. If that is no alternative, see [Random number generation#Alternatives](/index.php/Random_number_generation#Alternatives "Random number generation").

### su

When using `pinentry`, you must have the proper permissions of the terminal device (e.g. `/dev/tty1`) in use. However, with *su* (or *sudo*), the ownership stays with the original user, not the new one. This means that pinentry will fail, even as root. The fix is to change the permissions of the device at some point before the use of pinentry (i.e. using gpg with an agent). If doing gpg as root, simply change the ownership to root right before using gpg:

```
# chown root /dev/ttyN  # where N is the current tty

```

and then change it back after using gpg the first time. The equivalent is likely to be true with `/dev/pts/`.

**Note:** The owner of tty *must* match with the user for which pinentry is running. Being part of the group `tty` **is not** enough.

**Tip:** If you run gpg with `script` it will use a new tty with the correct ownership:
```
# script -q -c "gpg --gen-key" /dev/null

```

### Agent complains end of file

The default pinentry program is `/usr/bin/pinentry-gnome3`, which needs a DBus session bus to run properly. See [General troubleshooting#Session permissions](/index.php/General_troubleshooting#Session_permissions "General troubleshooting") for details.

Alternatively, you can use a variety of different options described in [#pinentry](#pinentry).

### KGpg configuration permissions

There have been issues with [kgpg](https://www.archlinux.org/packages/?name=kgpg) being able to access the `~/.gnupg/` options. One issue might be a result of a deprecated *options* file, see the [bug](https://bugs.kde.org/show_bug.cgi?id=290221) report.

### GNOME on Wayland overrides SSH agent socket

For Wayland sessions, `gnome-session` sets `SSH_AUTH_SOCK` to the standard gnome-keyring socket, `$XDG_RUNTIME_DIR/keyring/ssh`. This overrides any value set in `~/.pam_environmment` or systemd unit files.

See [GNOME/Keyring#Disable keyring daemon components](/index.php/GNOME/Keyring#Disable_keyring_daemon_components "GNOME/Keyring") on how to disable this behavior.

### mutt

Mutt might not use *gpg-agent* correctly, you need to set an [environment variable](/index.php/Environment_variable "Environment variable") `GPG_AGENT_INFO` (the content does not matter) when running mutt. Be also sure to enable password caching correctly, see [#Cache passwords](#Cache_passwords).

See [this forum thread](https://bbs.archlinux.org/viewtopic.php?pid=1490821#p1490821)

### "Lost" keys, upgrading to gnupg version 2.1

When `gpg --list-keys` fails to show keys that used to be there, and applications complain about missing or invalid keys, some keys may not have been migrated to the new format.

Please read [GnuPG invalid packet workaround](http://jo-ke.name/wp/?p=111). Basically, it says that there is a bug with keys in the old `pubring.gpg` and `secring.gpg` files, which have now been superseded by the new `pubring.kbx` file and the `private-keys-v1.d/` subdirectory and files. Your missing keys can be recovered with the following commands:

```
$ cd
$ cp -r .gnupg gnupgOLD
$ gpg --export-ownertrust > otrust.txt
$ gpg --import .gnupg/pubring.gpg
$ gpg --import-ownertrust otrust.txt
$ gpg --list-keys

```

### gpg hanged for all keyservers (when trying to receive keys)

If gpg hanged with a certain keyserver when trying to receive keys, you might need to kill dirmngr in order to get access to other keyservers which are actually working, otherwise it might keeping hanging for all of them.

### Smartcard not detected

Your user might not have the permission to access the smartcard which results in a `card error` to be thrown, even though the card is correctly set up and inserted.

One possible solution is to add a new group `scard` including the users who need access to the smartcard.

Then use [udev rules](/index.php/Udev_rules "Udev rules"), similar to the following:

 `/etc/udev/rules.d/71-gnupg-ccid.rules` 
```
ACTION=="add", SUBSYSTEM=="usb", ENV{ID_VENDOR_ID}=="1050", ENV{ID_MODEL_ID}=="0116|0111", MODE="660", GROUP="scard"

```

One needs to adapt VENDOR and MODEL according to the `lsusb` output, the above example is for a YubikeyNEO.

### server 'gpg-agent' is older than us (x < y)

This warning appears if `gnupg` is upgraded and the old gpg-agent is still running. [Restart](/index.php/Restart "Restart") the *user'*s `gpg-agent.socket` (i.e., use the `--user` flag when restarting).

### IPC connect call failed

Make sure `gpg-agent` and `dirmngr` are not running with `killall gpg-agent dirmngr` and the `$GNUPGHOME/crls.d/` folder has permission set to `700`.

If your keyring is stored on a vFat filesystem (e.g. a USB drive), `gpg-agent` will fail to create the required sockets (vFat does not support sockets), you can create redirects to a location that handles sockets, e.g. `/dev/shm`:

```
# export GNUPGHOME=/custom/gpg/home
# printf '%%Assuan%%
socket=/dev/shm/S.gpg-agent
' > $GNUPGHOME/S.gpg-agent
# printf '%%Assuan%%
socket=/dev/shm/S.gpg-agent.browser
' > $GNUPGHOME/S.gpg-agent.browser
# printf '%%Assuan%%
socket=/dev/shm/S.gpg-agent.extra
' > $GNUPGHOME/S.gpg-agent.extra
# printf '%%Assuan%%
socket=/dev/shm/S.gpg-agent.ssh
' > $GNUPGHOME/S.gpg-agent.ssh

```

Test that gpg-agent starts successfully with `gpg-agent --daemon`.

## See also

*   [GNU Privacy Guard Homepage](https://gnupg.org/)
*   [Alan Eliasen's GPG Tutorial](https://futureboy.us/pgp.html)
*   [RFC4880 "OpenPGP Message Format"](https://tools.ietf.org/html/rfc4880)
*   [gpg.conf recommendations and best practices](https://help.riseup.net/en/security/message-security/openpgp/gpg-best-practices)
*   [Creating GPG Keys (Fedora)](https://fedoraproject.org/wiki/Creating_GPG_Keys)
*   [OpenPGP subkeys in Debian](https://wiki.debian.org/Subkeys)
*   [Protecting code integrity with PGP](https://github.com/lfit/itpol/blob/master/protecting-code-integrity.md)
*   [A more comprehensive gpg Tutorial](https://sanctum.geek.nz/arabesque/series/gnu-linux-crypto/)
*   [/r/GPGpractice - a subreddit to practice using GnuPG.](https://www.reddit.com/r/GPGpractice/)