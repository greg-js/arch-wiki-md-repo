Related articles

*   [pacman/Package signing](/index.php/Pacman/Package_signing "Pacman/Package signing")
*   [Disk encryption](/index.php/Disk_encryption "Disk encryption")
*   [List of applications/Security#Encryption, signing, steganography](/index.php/List_of_applications/Security#Encryption.2C_signing.2C_steganography "List of applications/Security")

根據 [official website](https://www.gnupg.org/):

	GnuPG 是根據[OpenPGP](http://openpgp.org/about/)（亦稱作PGP的）所制定之[RFC4880](https://tools.ietf.org/html/rfc4880)標準的一個完整且自由的軟體。

GnuPG讓你可以可以加密及簽署你的檔案及通認資料，其特色在於豐富的金鑰管理系統及多種公鑰連接模組。作為一個命令列工具可輕易的與其他硬用程式整合，因此有豐富的應用程式與函式庫。此外GnuPG第二版更支援S/MIME及Secure Shell（ssh）。

## Contents

*   [1 安裝](#.E5.AE.89.E8.A3.9D)
*   [2 配置](#.E9.85.8D.E7.BD.AE)
    *   [2.1 資料夾位置](#.E8.B3.87.E6.96.99.E5.A4.BE.E4.BD.8D.E7.BD.AE)
    *   [2.2 設定檔](#.E8.A8.AD.E5.AE.9A.E6.AA.94)
    *   [2.3 新使用者的預設參數](#.E6.96.B0.E4.BD.BF.E7.94.A8.E8.80.85.E7.9A.84.E9.A0.90.E8.A8.AD.E5.8F.83.E6.95.B8)
*   [3 使用方法](#.E4.BD.BF.E7.94.A8.E6.96.B9.E6.B3.95)
    *   [3.1 建立鑰匙](#.E5.BB.BA.E7.AB.8B.E9.91.B0.E5.8C.99)
    *   [3.2 List keys](#List_keys)
    *   [3.3 Export your public key](#Export_your_public_key)
    *   [3.4 Import a public key](#Import_a_public_key)
    *   [3.5 Use a keyserver](#Use_a_keyserver)
    *   [3.6 Encrypt and decrypt](#Encrypt_and_decrypt)
        *   [3.6.1 Asymmetric](#Asymmetric)
        *   [3.6.2 Symmetric](#Symmetric)
*   [4 Key maintenance](#Key_maintenance)
    *   [4.1 Backup your private key](#Backup_your_private_key)
    *   [4.2 Edit your key](#Edit_your_key)
    *   [4.3 Exporting subkey](#Exporting_subkey)
    *   [4.4 Rotating subkeys](#Rotating_subkeys)
*   [5 Signatures](#Signatures)
    *   [5.1 Create a signature](#Create_a_signature)
        *   [5.1.1 Sign a file](#Sign_a_file)
        *   [5.1.2 Clearsign a file or message](#Clearsign_a_file_or_message)
        *   [5.1.3 Make a detached signature](#Make_a_detached_signature)
    *   [5.2 Verify a signature](#Verify_a_signature)
*   [6 gpg-agent](#gpg-agent)
    *   [6.1 Configuration](#Configuration)
    *   [6.2 Reload the agent](#Reload_the_agent)
    *   [6.3 pinentry](#pinentry)
    *   [6.4 Unattended passphrase](#Unattended_passphrase)
    *   [6.5 SSH agent](#SSH_agent)
*   [7 Smartcards](#Smartcards)
    *   [7.1 GnuPG only setups](#GnuPG_only_setups)
    *   [7.2 GnuPG with pcscd (PCSC Lite)](#GnuPG_with_pcscd_.28PCSC_Lite.29)
        *   [7.2.1 Always use pcscd](#Always_use_pcscd)
*   [8 Tips and tricks](#Tips_and_tricks)
    *   [8.1 Different algorithm](#Different_algorithm)
    *   [8.2 Encrypt a password](#Encrypt_a_password)
    *   [8.3 Revoking a key](#Revoking_a_key)
    *   [8.4 Change trust model](#Change_trust_model)
    *   [8.5 Hide all recipient id's](#Hide_all_recipient_id.27s)
    *   [8.6 Using caff for keysigning parties](#Using_caff_for_keysigning_parties)
    *   [8.7 Always show long ID's and fingerprints](#Always_show_long_ID.27s_and_fingerprints)
*   [9 Troubleshooting](#Troubleshooting)
    *   [9.1 Not enough random bytes available](#Not_enough_random_bytes_available)
    *   [9.2 su](#su)
    *   [9.3 Agent complains end of file](#Agent_complains_end_of_file)
    *   [9.4 KGpg configuration permissions](#KGpg_configuration_permissions)
    *   [9.5 GNOME on Wayland overrides SSH agent socket](#GNOME_on_Wayland_overrides_SSH_agent_socket)
    *   [9.6 mutt and gpg](#mutt_and_gpg)
    *   [9.7 "Lost" keys, upgrading to gnupg version 2.1](#.22Lost.22_keys.2C_upgrading_to_gnupg_version_2.1)
    *   [9.8 gpg hanged for all keyservers (when trying to receive keys)](#gpg_hanged_for_all_keyservers_.28when_trying_to_receive_keys.29)
    *   [9.9 Smartcard not detected](#Smartcard_not_detected)
    *   [9.10 gpg: WARNING: server 'gpg-agent' is older than us (x < y)](#gpg:_WARNING:_server_.27gpg-agent.27_is_older_than_us_.28x_.3C_y.29)
    *   [9.11 gpg: ..., IPC connect call failed](#gpg:_....2C_IPC_connect_call_failed)
    *   [9.12 Error: [key] could not be locally signed or gpg: No default secret key: No public key](#Error:_.5Bkey.5D_could_not_be_locally_signed_or_gpg:_No_default_secret_key:_No_public_key)
*   [10 參考文件](#.E5.8F.83.E8.80.83.E6.96.87.E4.BB.B6)

## 安裝

[Install](/index.php/Install "Install") the package. 安裝[gnupg](https://www.archlinux.org/packages/?name=gnupg)同時，[pinentry](https://www.archlinux.org/packages/?name=pinentry)也會被一併安裝，pinentry是使用GPG時要求輸入密碼的對話視窗程式，連結為`/usr/bin/pinentry`而預設是`/usr/bin/pinentry-gtk-2`。若你想採用整合GnuPG其他圖形化介面的程式可參考此列表[List of applications/Security#Encryption, signing, steganography](/index.php/List_of_applications/Security#Encryption.2C_signing.2C_steganography "List of applications/Security")。

## 配置

### 資料夾位置

GnuPG的設定檔存於`$GNUPGHOME`，`$GNUPGHOME`並沒有預設路徑，在此情形下則會使用`$HOME`。因此，你在安裝後將會發現`~/.gnupg`這個資料夾。

如果需要修改預設路徑，可以執行`$ gpg --homedir *path/to/file*`，或在[startup files](/index.php/Startup_files "Startup files")設定`GNUPGHOME`。

### 設定檔

`~/.gnupg/gpg.conf`及`~/.gnupg/dirmngr.conf`為預設設定檔。

gnupg資料來預設為`700`權限，而裡面的檔案則為`600`權限。只有該資料夾的擁有者有權讀取、修改、及存取該等檔案。這些權限設定基於安全考量不應輕易修改。如果這些檔案不符合這個安全規範時，gnppg會產生關於檔案或gnupg家目錄不安全權限的警告。

加入的文件雖然可以為任意長度，但不要有兩個破折號（-），建議為選項名稱和使用的參數。你可以在`/usr/share/gnupg`找到一些範例檔案。在gpg第一次執行且沒有檔案時，其亦會將這些範例檔案複製至`~/.gnupg` 。你也可以在[#參考文件](#.E5.8F.83.E8.80.83.E6.96.87.E4.BB.B6)中找到一些範例。

此外，[pacman](/index.php/Pacman "Pacman")採用不同組的設定檔，其用於軟體簽章的驗証。更細節部份可參考[Pacman/Package signing](/index.php/Pacman/Package_signing "Pacman/Package signing")。

### 新使用者的預設參數

如果你想為新使用者設定預設參數，可將設定檔放置於`/etc/skel/.gnupg/`。一旦新使用者加入系統時，該等檔案將會自動地複製到使用者的GnuPG家目錄。此外，*addgnupghome* 這個指令可以協助你為已存在的使用者新增GnuPG家目錄。

```
# addgnupghome user1 user2

```

此指令將會各別生成`/home/user1/.gnupg`和`/home/user2/.gnupg`，並且從樣版資料夾中複製檔案，但若使用者已先產生GnuPG家目錄，則不會有改動。

## 使用方法

**Note:** 無論指令執行時是否可以獲取*`user-id`*，請在指令執行時給予key ID、指紋、你的名字或email，而GnuPG會自動判斷你給的資訊。

### 建立鑰匙

藉由以下指令產生一對鑰匙：

```
$ gpg --full-gen-key

```

**Tip:** 可加入`--expert` 選擇不同的加密方式，例如：[ECC](https://en.wikipedia.org/wiki/Elliptic_curve_cryptography "wikipedia:Elliptic curve cryptography").

這個指令會有一些問題跟提示，大部分的使用者可參考如下設定：

*   RSA (sign only) 或 RSA (encrypt only) key.
*   keysize建議值為2048，4096並不會有額外的好處但卻更耗損資源，請參[[1]](https://www.gnupg.org/faq/gnupg-faq.html#no_default_of_rsa4096)。
*   設定過期時間，建議一年，在屆滿時可以再行延展而不用重新產生鑰匙。
*   你的名字跟email設定，你也可以將多個email綁在同一對鑰匙上。
*   如果需要設定額外註釋請參考[TOFU Design](https://lists.gnupg.org/pipermail/gnupg-devel/2015-July/030150.html)，但並不建議填寫。
*   密碼可參考[a secure passphrase](/index.php/Security#Choosing_secure_passwords "Security").

**Note:** 名字與email將會被人往後匯入你的公鑰的人看到。

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

gpg's main usage is to ensure confidentiality of exchanged messages via public-key cryptography. With it each user distributes the public key of their keyring, which can be be used by others to encrypt messages to the user. The private key must *always* be kept private, otherwise confidentiality is broken. See [w:Public-key cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography "w:Public-key cryptography") for examples about the message exchange.

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
$ gpg --send-keys *user-id*

```

To find out details of a key on the keyserver, without importing it, do:

```
$ gpg --search-keys *user-id*

```

To import a key from a key server:

```
$ gpg --recv-keys *key-id*

```

**Warning:**

*   You should verify the authenticity of the retrieved public key by comparing its fingerprint with one that the owner published on an independent source(s) (i.e., contacting the person directly). See [Wikipedia:Public key fingerprint](https://en.wikipedia.org/wiki/Public_key_fingerprint "wikipedia:Public key fingerprint") for more information.
*   Using a short ID may encounter collisions. All keys will be imported that have the short ID. To avoid this, use the full fingerprint or long key ID when receiving a key.[[2]](https://lkml.org/lkml/2016/8/15/445)

**Tip:**

*   Adding `keyserver-options auto-key-retrieve` to `gpg.conf` will automatically fetch keys from the key server as needed.
*   An alternative key server is `pool.sks-keyservers.net` and can be specified with `keyserver` in `dirmngr.conf`; see also [wikipedia:Key server (cryptographic)#Keyserver examples](https://en.wikipedia.org/wiki/Key_server_(cryptographic)#Keyserver_examples "wikipedia:Key server (cryptographic)").
*   If your network blocks ports used for hkp/hkps, you may need to specify port 80, i.e. `pool.sks-keyservers.net:80`
*   You can connect to the keyserver over [Tor](/index.php/Tor "Tor") using `--use-tor`. See this [GnuPG blog post](https://gnupg.org/blog/20151224-gnupg-in-november-and-december.html) for more information.
*   You can connect to a keyserver using a proxy by setting the `http_proxy` environment variable and setting `honor-http-proxy` in `dirmngr.conf`. Alternatively, set `http-proxy *host[:port]*` in `dirmngr.conf`, overriding the `http_proxy` environment variable.
*   If you wish to import a key ID to install a specific Arch Linux package, see [pacman/Package signing#Managing the keyring](/index.php/Pacman/Package_signing#Managing_the_keyring "Pacman/Package signing") and [Makepkg#Signature checking](/index.php/Makepkg#Signature_checking "Makepkg").

### Encrypt and decrypt

#### Asymmetric

You need to [#Import a public key](#Import_a_public_key) of a user before encrypting (options `--encrypt` or `-e`) a file or message to that recipient (options `--recipient` or `-r`). Additionally you need to [#Create key pair](#Create_key_pair) if you have not already done so.

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

### Edit your key

Running the `gpg --edit-key *<user-id>*` command will present a menu which enables you to do most of your key management related tasks.

Some useful commands in the edit key sub menu:

```
> passwd       # change the passphrase
> clean        # compact any user ID that is no longer usable (e.g revoked or expired)
> revkey       # revoke a key
> addkey       # add a subkey to this key
> expire       # change the key expiration time

```

Type `help` in the edit key sub menu for more commands.

**Tip:** If you have multiple email accounts you can add each one of them as an identity, using `adduid` command. You can then set your favourite one as `primary`.

### Exporting subkey

If you plan to use the same key across multiple devices, you may want to strip out your master key and only keep the bare minimum encryption subkey on less secure systems.

First, find out which subkey you want to export.

```
$ gpg -K

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
$ gpg --homedir /tmp/gpg -a --export-secret-subkeys [subkey id]! > /tmp/subkey.altpass.gpg

```

**Note:** You will get a warning that the master key was not available and the password was not changed, but that can safely be ignored as the subkey password was.

At this point, you can now use `/tmp/subkey.altpass.gpg` on your other devices.

### Rotating subkeys

**Warning:** **Never** delete your expired or revoked subkeys unless you have a good reason. Doing so will cause you to lose the ability to decrypt files encrypted with the old subkey. Please **only** delete expired or revoked keys from other users to clean your keyring.

If you have set your subkeys to expire after a set time, you can create new ones. Do this a few weeks in advance to allow others to update their keyring.

**Tip:** You do not need to create a new key simply because it is expired. You can extend the expiration date.

Create new subkey (repeat for both signing and encrypting key)

```
$ gpg --edit-key *<user-id>*
> addkey

```

And answer the following questions it asks (see [#Create key pair](#Create_key_pair) for suggested settings).

Save changes

```
> save

```

Update it to a keyserver.

```
$ gpg --keyserver pgp.mit.edu --send-keys *<user-id>*

```

**Tip:** Revoking expired subkeys is unnecessary and arguably bad form. If you are constantly revoking keys, it may cause others to lack confidence in you.

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

If a file as been encrypted in addition to being signed, simply [decrypt](#Encrypt_and_decrypt) the file and its signature will also be verified.

## gpg-agent

*gpg-agent* is mostly used as daemon to request and cache the password for the keychain. This is useful if GnuPG is used from an external program like a mail client. [gnupg](https://www.archlinux.org/packages/?name=gnupg) comes with [systemd user](/index.php/Systemd/User "Systemd/User") sockets which are enabled by default. These sockets are `gpg-agent.socket`, `gpg-agent-extra.socket`, `gpg-agent-browser.socket`, `gpg-agent-ssh.socket`, and `dirmngr.socket`.

*   The main `gpg-agent.socket` is used by *gpg* to connect to the *gpg-agent* daemon.
*   The intended use for the `gpg-agent-extra.socket` on a local system is to set up a Unix domain socket forwarding from a remote system. This enables to use *gpg* on the remote system without exposing the private keys to the remote system. See [gpg-agent(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/gpg-agent.1) for details.
*   The `gpg-agent-ssh.socket` can be used by [SSH](/index.php/SSH "SSH") to cache [SSH keys](/index.php/SSH_keys "SSH keys") added by the *ssh-add* program. See [#SSH agent](#SSH_agent) for the necessary configuration.
*   The `dirmngr.socket` starts a GnuPG daemon handling connections to keyservers.

**Note:** If you use non-default GnuPG [#Directory location](#Directory_location), you will need to [edit](/index.php/Edit "Edit") all socket files to use the path in the socket directory that `gpgconf --create-socketdir` creates.

### Configuration

gpg-agent can be configured via `~/.gnupg/gpg-agent.conf` file. The configuration options are listed in [gpg-agent(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/gpg-agent.1). For example you can change cache ttl for unused keys:

 `~/.gnupg/gpg-agent.conf` 
```
default-cache-ttl 3600

```

**Tip:** To cache your passphrase for the whole session, please run the following command:
```
$ /usr/lib/gnupg/gpg-preset-passphrase --preset XXXXXX

```

where XXXX is the keygrip. You can get its value when running `gpg --with-keygrip -K`. Passphrase will be stored until `gpg-agent` is restarted. If you set up `default-cache-ttl` value, it will take precedence.

### Reload the agent

After changing the configuration, reload the agent using *gpg-connect-agent*:

```
$ gpg-connect-agent reloadagent /bye

```

The command should print `OK`.

However in some cases only the restart may not be sufficient, like when `keep-screen` has been added to the agent configuration. In this case you firstly need to kill the ongoing gpg-agent process and then you can restart it as was explained above.

### pinentry

Finally, the agent needs to know how to ask the user for the password. This can be set in the gpg-agent configuration file.

The default uses a gtk dialog. There are other options - see `info pinentry`. To change the dialog implementation set `pinentry-program` configuration option:

 `~/.gnupg/gpg-agent.conf` 
```

# PIN entry program
# pinentry-program /usr/bin/pinentry-curses
# pinentry-program /usr/bin/pinentry-qt
# pinentry-program /usr/bin/pinentry-kwallet

pinentry-program /usr/bin/pinentry-gtk-2

```

**Tip:** For using `/usr/bin/pinentry-kwallet` you have to install the [kwalletcli](https://aur.archlinux.org/packages/kwalletcli/) package.

After making this change, reload the gpg-agent.

### Unattended passphrase

Starting with GnuPG 2.1.0 the use of gpg-agent and pinentry is required, which may break backwards compatibility for passphrases piped in from STDIN using the `--passphrase-fd 0` commandline option. In order to have the same type of functionality as the older releases two things must be done:

First, edit the gpg-agent configuration to allow *loopback* pinentry mode:

 `~/.gnupg/gpg-agent.conf`  `allow-loopback-pinentry` 

Restart the gpg-agent process if it is running to let the change take effect.

Second, either the application needs to be updated to include a commandline parameter to use loopback mode like so:

```
$ gpg --pinentry-mode loopback ...

```

...or if this is not possible, add the option to the configuration:

 `~/.gnupg/gpg.conf`  `pinentry-mode loopback` 
**Note:** The upstream author indicates setting `pinentry-mode loopback` in `gpg.conf` may break other usage, using the commandline option should be preferred if at all possible. [[3]](https://bugs.g10code.com/gnupg/issue1772)

### SSH agent

*gpg-agent* has OpenSSH agent emulation. If you already use the GnuPG suite, you might consider using its agent to also cache your [SSH keys](/index.php/SSH_keys "SSH keys"). Additionally, some users may prefer the PIN entry dialog GnuPG agent provides as part of its passphrase management.

To start using GnuPG agent for your SSH keys, enable SSH support in the `~/.gnupg/gpg-agent.conf` file:

 `~/.gnupg/gpg-agent.conf` 
```
enable-ssh-support

```

Then set `SSH_AUTH_SOCK` so that SSH will use *gpg-agent* instead of *ssh-agent*. To make sure each process can find your *gpg-agent* instance regardless of e.g. the type of shell it is child of use [pam_env](/index.php/Environment_variables#Using_pam_env "Environment variables").

 `~/.pam_environment` 
```
SSH_AGENT_PID	DEFAULT=
SSH_AUTH_SOCK	DEFAULT="${XDG_RUNTIME_DIR}/gnupg/S.gpg-agent.ssh"
```

Alternatively, depend on Bash:

 `~/.bashrc` 
```
# Set SSH to use gpg-agent
unset SSH_AGENT_PID
if [ "${gnupg_SSH_AUTH_SOCK_by:-0}" -ne $$ ]; then
  export SSH_AUTH_SOCK="/run/user/$UID/gnupg/S.gpg-agent.ssh"
fi

```

**Note:**

*   If you use non-default GnuPG [#Directory location](#Directory_location), run `gpgconf --create-socketdir` to create a socket directory under `/run/user/$UID/gnupg/`. Otherwise the socket will be placed in the GnuPG home directory.
*   The test involving the `gnupg_SSH_AUTH_SOCK_by` variable is for the case where the agent is started as `gpg-agent --daemon /bin/sh`, in which case the shell inherits the `SSH_AUTH_SOCK` variable from the parent, *gpg-agent* [[4]](http://git.gnupg.org/cgi-bin/gitweb.cgi?p=gnupg.git;a=blob;f=agent/gpg-agent.c;hb=7bca3be65e510eda40572327b87922834ebe07eb#l1307).

Also set the GPG_TTY and refresh the TTY in case user has switched into an X session as stated in [gpg-agent(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/gpg-agent.1). For example:

 `~/.bashrc` 
```
# Set GPG TTY
export GPG_TTY=$(tty)

# Refresh gpg-agent tty in case user switches into an X session
gpg-connect-agent updatestartuptty /bye >/dev/null

```

Once *gpg-agent* is running you can use *ssh-add* to approve keys, following the same steps as for [ssh-agent](/index.php/SSH_keys#ssh-agent "SSH keys"). The list of approved keys is stored in the `~/.gnupg/sshcontrol` file. Once your key is approved, you will get a *pinentry* dialog every time your passphrase is needed. You can control passphrase caching in the `~/.gnupg/gpg-agent.conf` file. The following example would have *gpg-agent* cache your keys for 3 hours:

 `~/.gnupg/gpg-agent.conf` 
```
default-cache-ttl-ssh 10800
max-cache-ttl-ssh 10800

```

## Smartcards

GnuPG uses *scdaemon* as an interface to your smartcard reader, please refer to the [man page](/index.php/Man_page "Man page") for details.

### GnuPG only setups

**Note:** To allow scdaemon direct access to USB smarcard readers the optional dependency [libusb-compat](https://www.archlinux.org/packages/?name=libusb-compat) have to be installed

If you do not plan to use other cards but those based on GnuPG, you should check the `reader-port` parameter in `~/.gnupg/scdaemon.conf`. The value '0' refers to the first available serial port reader and a value of '32768' (default) refers to the first USB reader.

### GnuPG with pcscd (PCSC Lite)

**Note:** [pcsclite](https://www.archlinux.org/packages/?name=pcsclite) and [ccid](https://www.archlinux.org/packages/?name=ccid) have to be installed, and the contained [systemd](/index.php/Systemd#Using_units "Systemd") service `pcscd.service` has to be running, or the socket `pcscd.socket` has to be listening.

pcscd is a daemon which handles access to smartcard (SCard API). If GnuPG's scdaemon fails to connect the smartcard directly (e.g. by using its integrated CCID support), it will fallback and try to find a smartcard using the PCSC Lite driver.

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

Now update the keyserver:

```
$ gpg --keyserver subkeys.pgp.net --send-keys *<userid>*

```

### Change trust model

By default GnuPG uses the [Web of Trust](https://en.wikipedia.org/wiki/Web_of_Trust "wikipedia:Web of Trust") as the trust model. You can change this to [Trust on first use](https://en.wikipedia.org/wiki/Trust_on_first_use "wikipedia:Trust on first use") by adding `--trust-model=tofu` when adding a key or adding this option to your GnuPG configuration file. More details are in [this email to the GnuPG list](https://lists.gnupg.org/pipermail/gnupg-devel/2015-October/030341.html).

### Hide all recipient id's

By default the recipient's key ID is in the encrypted message. This can be removed at encryption time for a recipient by using `hidden-recipient *<user-id>*`. To remove it for all recipients add `throw-keyids` to your configuration file. This helps to hide the receivers of the message and is a limited countermeasure against traffic analysis. (Using a little social engineering anyone who is able to decrypt the message can check whether one of the other recipients is the one he suspects.) On the receiving side, it may slow down the decryption process because all available secret keys must be tried (*e.g.* with `--try-secret-key *<user-id>*`).

### Using caff for keysigning parties

To allow users to validate keys on the keyservers and in their keyrings (i.e. make sure they are from whom they claim to be), PGP/GPG uses the [Web of Trust](https://en.wikipedia.org/wiki/Web_of_Trust "wikipedia:Web of Trust"). Keysigning parties allow users to get together at a physical location to validate keys. The [Zimmermann-Sassaman](https://en.wikipedia.org/wiki/Zimmermann%E2%80%93Sassaman_key-signing_protocol "wikipedia:Zimmermann–Sassaman key-signing protocol") key-signing protocol is a way of making these very effective. [Here](http://www.cryptnet.net/fdp/crypto/keysigning_party/en/keysigning_party.html) you will find a how-to article.

For an easier process of signing keys and sending signatures to the owners after a keysigning party, you can use the tool *caff*. It can be installed from the AUR with the package [caff-svn](https://aur.archlinux.org/packages/caff-svn/).

To send the signatures to their owners you need a working [MTA](https://en.wikipedia.org/wiki/Message_transfer_agent "wikipedia:Message transfer agent"). If you do not have already one, install [msmtp](/index.php/Msmtp "Msmtp").

### Always show long ID's and fingerprints

To always show long key ID's add `keyid-format 0xlong` to your configuration file. To always show full fingerprints of keys, add `with-fingerprint` to your configuration file.

## Troubleshooting

### Not enough random bytes available

When generating a key, gpg can run into this error:

```
Not enough random bytes available. Please do some other work to give the OS a chance to collect more entropy!

```

To check the available entropy, check the kernel parameters:

```
cat /proc/sys/kernel/random/entropy_avail

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

The default pinentry program is pinentry-gtk-2, which needs a DBus session bus to run properly. See [General troubleshooting#Session permissions](/index.php/General_troubleshooting#Session_permissions "General troubleshooting") for details.

Alternatively, you can use `pinentry-qt`. See [#pinentry](#pinentry).

### KGpg configuration permissions

There have been issues with [kgpg](https://www.archlinux.org/packages/?name=kgpg) being able to access the `~/.gnupg/` options. One issue might be a result of a deprecated *options* file, see the [bug](https://bugs.kde.org/show_bug.cgi?id=290221) report.

### GNOME on Wayland overrides SSH agent socket

For Wayland sessions, `gnome-session` sets `SSH_AUTH_SOCK` to the standard gnome-keyring socket, `$XDG_RUNTIME_DIR/keyring/ssh`. This overrides any value set in `~/.pam_environmment` or systemd unit files.

To disable this behavior, set the `GSM_SKIP_AGENT_WORKAROUND` variable:

 `~/.pam_environment` 
```
SSH_AGENT_PID	DEFAULT=
SSH_AUTH_SOCK	DEFAULT="${XDG_RUNTIME_DIR}/gnupg/S.gpg-agent.ssh"
GSM_SKIP_SSH_AGENT_WORKAROUND	DEFAULT="true"
```

### mutt and gpg

To be asked for your GnuPG password only once per session, see [this forum thread](https://bbs.archlinux.org/viewtopic.php?pid=1490821#p1490821).

### "Lost" keys, upgrading to gnupg version 2.1

When `gpg --list-keys` fails to show keys that used to be there, and applications complain about missing or invalid keys, some keys may not have been migrated to the new format.

Please read [GnuPG invalid packet workaround](http://jo-ke.name/wp/?p=111). Basically, it says that there is a bug with keys in the old `pubring.gpg` and `secring.gpg` files, which have now been superseded by the new `pubring.kbx` file and the `private-keys-v1.d/` subdirectory and files. Your missing keys can be recovered with the following commnads:

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

Then use an [udev](/index.php/Udev#Writing_udev_rules "Udev") rule, similar to the following:

 `/etc/udev/rules.d/71-gnupg-ccid.rules` 
```
ACTION=="add", SUBSYSTEM=="usb", ENV{ID_VENDOR_ID}=="1050", ENV{ID_MODEL_ID}=="0116|0111", MODE="660", GROUP="scard"

```

One needs to adapt VENDOR and MODEL according to the `lsusb` output, the above example is for a YubikeyNEO.

### gpg: WARNING: server 'gpg-agent' is older than us (x < y)

This warning appears if `gnupg` is upgraded and the old gpg-agent is still running. [Restart](/index.php/Restart "Restart") the *user'*s `gpg-agent.socket` (i.e., use the `--user` flag when restarting).

### gpg: ..., IPC connect call failed

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

### Error: [key] could not be locally signed or gpg: No default secret key: No public key

Occurs when attempting to sign keys on a non-standard keyring while a yubikey is plugged in, e.g. as [Pacman](/index.php/Pacman/Package_signing "Pacman/Package signing") does in `pacman-key --populate archlinux`. The solution is to remove the offending yubikey and start over.

## 參考文件

*   [GNU Privacy Guard Homepage](https://gnupg.org/)
*   [RFC4880 "OpenPGP Message Format"](https://tools.ietf.org/html/rfc4880)
*   [Creating GPG Keys (Fedora)](https://fedoraproject.org/wiki/Creating_GPG_Keys)
*   [OpenPGP subkeys in Debian](https://wiki.debian.org/Subkeys)
*   [A more comprehensive gpg Tutorial](https://sanctum.geek.nz/arabesque/series/gnu-linux-crypto/)
*   [gpg.conf recommendations and best practices](https://help.riseup.net/en/security/message-security/openpgp/gpg-best-practices)
*   [Torbirdy gpg.conf](https://github.com/ioerror/torbirdy/blob/master/gpg.conf)
*   [/r/GPGpractice - a subreddit to practice using GnuPG.](https://www.reddit.com/r/GPGpractice/)