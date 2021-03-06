Related articles

*   [pacman/Package signing (简体中文)](/index.php/Pacman/Package_signing_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman/Package signing (简体中文)")
*   [Disk encryption](/index.php/Disk_encryption "Disk encryption")
*   [List of applications/Security#Encryption, signing, steganography](/index.php/List_of_applications/Security#Encryption,_signing,_steganography "List of applications/Security")

**翻译状态：** 本文是英文页面 [GnuPG](/index.php/GnuPG "GnuPG") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-07-27，点击[这里](https://wiki.archlinux.org/index.php?title=GnuPG&diff=0&oldid=441685)可以查看翻译后英文页面的改动。

根据 [官方网站](http://www.gnupg.org):

	GnuPG 是 RFC4880 OpenPGP 标准 PGP 的完整实现，自由软件。GnuPG 可以加密和签名数据和信息传递，包含一个通用的密钥管理系统，包含的访问模块可以访问各种公钥目录。 GnuPG, 简称 GPG, 是命令行工具，很方便和其它程序进行整合，具有很多前端程序和函数库。 GnuPG V2 还支持 S/MIME 和 Secure Shell (ssh).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 安装](#安装)
*   [2 配置](#配置)
    *   [2.1 目录位置](#目录位置)
    *   [2.2 配置文件](#配置文件)
    *   [2.3 新用户的默认选项](#新用户的默认选项)
*   [3 用法](#用法)
    *   [3.1 创建密钥对](#创建密钥对)
    *   [3.2 查看密钥](#查看密钥)
    *   [3.3 导出公钥](#导出公钥)
    *   [3.4 导入公共密钥](#导入公共密钥)
    *   [3.5 使用公钥服务器](#使用公钥服务器)
    *   [3.6 Encrypt and decrypt](#Encrypt_and_decrypt)
*   [4 密钥维护](#密钥维护)
    *   [4.1 Edit your key](#Edit_your_key)
    *   [4.2 Exporting subkey](#Exporting_subkey)
    *   [4.3 Rotating subkeys](#Rotating_subkeys)
*   [5 Signatures](#Signatures)
    *   [5.1 Sign a file](#Sign_a_file)
    *   [5.2 Clearsign a file or message](#Clearsign_a_file_or_message)
    *   [5.3 Make a detached signature](#Make_a_detached_signature)
    *   [5.4 Verify a signature](#Verify_a_signature)
*   [6 gpg-agent](#gpg-agent)
    *   [6.1 Configuration](#Configuration)
    *   [6.2 Reload the agent](#Reload_the_agent)
    *   [6.3 pinentry](#pinentry)
    *   [6.4 Start gpg-agent with systemd user](#Start_gpg-agent_with_systemd_user)
    *   [6.5 Unattended passphrase](#Unattended_passphrase)
    *   [6.6 SSH agent](#SSH_agent)
*   [7 Smartcards](#Smartcards)
    *   [7.1 GnuPG only setups](#GnuPG_only_setups)
    *   [7.2 GnuPG with PSCD-Lite](#GnuPG_with_PSCD-Lite)
        *   [7.2.1 Always use PSCD-Light](#Always_use_PSCD-Light)
*   [8 使用技巧](#使用技巧)
    *   [8.1 Different algorithm](#Different_algorithm)
    *   [8.2 Encrypt a password](#Encrypt_a_password)
    *   [8.3 Revoking a key](#Revoking_a_key)
    *   [8.4 Change trust model](#Change_trust_model)
    *   [8.5 Hide all recipient id's](#Hide_all_recipient_id's)
    *   [8.6 Using caff for keysigning parties](#Using_caff_for_keysigning_parties)
*   [9 Troubleshooting](#Troubleshooting)
    *   [9.1 Not enough random bytes available](#Not_enough_random_bytes_available)
    *   [9.2 su](#su)
    *   [9.3 Agent complains end of file](#Agent_complains_end_of_file)
    *   [9.4 KGpg configuration permissions](#KGpg_configuration_permissions)
    *   [9.5 Conflicts between gnome-keyring and gpg-agent](#Conflicts_between_gnome-keyring_and_gpg-agent)
    *   [9.6 mutt and gpg](#mutt_and_gpg)
    *   [9.7 "Lost" keys, upgrading to gnupg version 2.1](#"Lost"_keys,_upgrading_to_gnupg_version_2.1)
    *   [9.8 gpg hanged for all keyservers (when trying to receive keys)](#gpg_hanged_for_all_keyservers_(when_trying_to_receive_keys))
    *   [9.9 Smartcard not detected](#Smartcard_not_detected)
*   [10 参阅](#参阅)

## 安装

[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") 软件包 [gnupg](https://www.archlinux.org/packages/?name=gnupg).

软件包 [pinentry](https://www.archlinux.org/packages/?name=pinentry) 也会被同时安装，它是一个简单的 PIN 或 passphrase 输入对话框集合，GnuPG 用来输入密码，*pinentry* 的对话框是由软链接`/usr/bin/pinentry` 确定，默认指向 `/usr/bin/pinentry-gtk-2`.

如果要图形界面和 GnuPG 进行整合，请查看 [List of applications/Security#Encryption, signing, steganography](/index.php/List_of_applications/Security#Encryption,_signing,_steganography "List of applications/Security").

## 配置

### 目录位置

GnuPG 用环境变量 `$GNUPGHOME` 定位配置文件的位置，默认情况下此变量并未被设置，会直接使用 `$HOME`，所以默认的配置目录是 `~/.gnupg`。

要改变默认位置，执行 `$ gpg --homedir *path/to/file*` 或在 [startup files](/index.php/Startup_files "Startup files") 中设置 `GNUPGHOME`。

### 配置文件

默认的配置文件是 `~/.gnupg/gpg.conf` 和 `~/.gnupg/dirmngr.conf`.

gnupg 目录的默认 [权限](/index.php/Permissions "Permissions") 是 `700`，其中文件的权限是 `600`. 仅目录的所有者有权读写，访问这些文件。这是基于安全考虑，请不要变更。如果不使用这样的安全权限设置，会收到不安全文件的警告。

在文件中附加需要的文件，`/usr/share/gnupg` 包含基本架构文件. gpg 第一次运行时，如果配置文件不存在，会自动复制文件到 `~/.gnupg`.

此外, [pacman](/index.php/Pacman "Pacman") 使用单独的配置文件进行软件包的权限验证。详情请参考 [Pacman/Package signing](/index.php/Pacman/Package_signing "Pacman/Package signing")。

### 新用户的默认选项

要给新建用户设定一些默认选项，把配置文件放到 `/etc/skel/.gnupg/`. 系统创建新用户时，就会把文件复制到 GnuPG 目录。还有一个 *addgnupghome* 命令可以为已有用户创建新 GnuPG 主目录：

```
# addgnupghome user1 user2

```

此命令会将对检查 `/home/user1/.gnupg` 和 `/home/user2/.gnupg`，如果用户的 GnuPG 主目录不存在，就会从 skeleton 目录复制文件过去。

## 用法

**Note:** 如果命令需要一个 *`<user-id>`*， 可以使用 key ID, 指纹, 用户名和密码对等替代，GnuPG 这的处理很灵活。

### 创建密钥对

用下面命令创建一个密钥对：

```
$ gpg --full-gen-key

```

**Tip:** 使用 `--expert` 选项可以选择其它的 option for getting alternative 密码算法，比如 [ECC](https://en.wikipedia.org/wiki/Elliptic_curve_cryptography "wikipedia:Elliptic curve cryptography").

命令执行后会需要用户回答一些问题，大部分用户应该需要的是：

*   RSA (sign only) 和 a RSA (encrypt only) 密钥.
*   默认的密钥长度 (2048). 增大长度到 4096 "收益不大，但是付出很大"[[1]](https://www.gnupg.org/faq/gnupg-faq.html#no_default_of_rsa4096).
*   过期日期. 大部分用户可以选择一年. 这样即使无法访问 keyring, 用户也知道密钥已经过期。如果需要可以不重新建立密钥就延长过期时间。
*   用户名和电子邮件。可以给同样的密钥不同的身份，比如给同一个密钥关联多个电子邮件。
*   *无* 可选注释，注释字段并没有被[很好的定义](https://lists.gnupg.org/pipermail/gnupg-devel/2015-July/030150.html)，作用有限。
*   [a secure passphrase](/index.php/Security#Choosing_secure_passwords "Security").

**注意:** 任何导入密钥的人都可以看到这里的用户名和电子邮件地址。

### 查看密钥

查看公钥：

```
$ gpg --list-keys

```

查看私钥:

```
$ gpg --list-secret-keys

```

### 导出公钥

gpg's main usage is to ensure confidentiality of exchanged messages via public-key cryptography. With it each user distributes the public key of their keyring, which can be be used by others to encrypt messages to the user. The private key must *always* be kept private, otherwise confidentiality is broken. See [w:Public-key cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography "w:Public-key cryptography") for examples about the message exchange.

所以其他人需要有你的公钥才能给你发加密信息。

要生成公钥的 ASCII 版本，(例如通过电子邮件发布):

```
$ gpg --output *public.key* --armor --export *<user-id>*  

```

此外，还可以通过 [密钥服务器](#使用公钥服务器)分发公钥.

**Tip:** 使用 `--no-emit-version` 可以避免打印版本号，通过配置文件也可以进行此设置。

### 导入公共密钥

要给其他人发送加密信息，或者验证他们的签名，就需要他们的公钥。通过文件 `*public.key*` 导入公钥到密钥环：

```
$ gpg --import *public.key*

```

此外，还可以通过密钥服务器导入公钥。

### 使用公钥服务器

你可以将你的公钥注册到一个公共的密钥服务器，这样其他人不用联系你就能获取到你的公钥：

```
$ gpg --send-keys *<key-id>*

```

要查询公钥的详细信息而不是导入，执行：

```
$ gpg --search-keys *<key-id>*

```

要导入一个公钥：

```
$ gpg --recv-keys *<key-id>*

```

**Warning:** Anyone can send keys to a keyserver, so you should not trust that the key you download actually belongs to the individual listed. You should verify the authenticity of the retrieved public key by comparing its fingerprint with one that the owner published on an independent source, such as their own blog or website, or contacting them by email, over the phone or in person. Using multiple authentication sources will increase the level of trust you can give to the downloaded key. See [Wikipedia:Public key fingerprint](https://en.wikipedia.org/wiki/Public_key_fingerprint "wikipedia:Public key fingerprint") for more information.

**Tip:**

*   Adding `keyserver-options auto-key-retrieve` to `gnupg.conf` will automatically fetch keys from the key server as needed.
*   An alternative key server is `pool.sks-keyservers.net` and can be specified with `keyserver` in `dirmngr.conf`.; see also [wikipedia:Key server (cryptographic)#Keyserver examples](https://en.wikipedia.org/wiki/Key_server_(cryptographic)#Keyserver_examples "wikipedia:Key server (cryptographic)").
*   You can connect to the keyserver over [Tor](/index.php/Tor "Tor") using `--use-tor`. `hkp://jijrk5u4osbsr34t5.onion` is the onion address for the sks-keyservers pool. [See this GnuPG blog post](https://gnupg.org/blog/20151224-gnupg-in-november-and-december.html) for more information.
*   You can connect to a keyserver using a proxy by setting the `http_proxy` environment variable and setting `honor-http-proxy` in `dirmngr.conf`. Alternatively, set `http-proxy *host[:port]*` in `dirmngr.conf`, overriding the `http_proxy` environment variable.

### Encrypt and decrypt

You need to [#Import a public key](#Import_a_public_key) of a user before encrypting (options `--encrypt` or `-e`) a file or message to that recipient (options `--recipient` or `-r`).

To encrypt a file with the name *doc*, use:

```
$ gpg --recipient *<user-id>* --encrypt *doc*

```

To decrypt (option `--decrypt` or `-d`) a file with the name *doc.gpg* encrypted with your public key, use:

```
$ gpg --output *doc* --decrypt *doc.gpg*

```

*gpg* will prompt you for your passphrase and then decrypt and write the data from *doc.gpg* to *doc*. If you omit the `-o` (`--output`) option, *gpg* will write the decrypted data to stdout.

**Tip:**

*   Add `--armor` to encrypt a file using ASCII armor (suitable for copying and pasting a message in text format)
*   Use `-R *<user-id>*` or `--hidden-recipient *<user-id>*` instead of `-r` to not put the recipient key IDs in the encrypted message. This helps to hide the receivers of the message and is a limited countermeasure against traffic analysis.
*   Add `--no-emit-version` to avoid printing the version number, or add the corresponding setting to your configuration file.
*   You can use gnupg to encrypt your sensitive documents by using your own user-id as recipient, but only individual files at a time, though you can always tarball various files and then encrypt the tarball. See also [Disk encryption#Available methods](/index.php/Disk_encryption#Available_methods "Disk encryption") if you want to encrypt directories or a whole file-system.

## 密钥维护

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

**Note:** You do not need to create a new key simply because it is expired. You can extend the expiration date.

Create new subkey (repeat for both signing and encrypting key)

```
$ gpg --edit-key *<user-id>*
> addkey

```

And answer the following questions it asks (see previous section for suggested settings).

Save changes

```
> save

```

Update it to a keyserver.

```
$ gpg --keyserver pgp.mit.edu --send-keys *<user-id>*

```

**Note:** Revoking expired subkeys is unnecessary and arguably bad form. If you are constantly revoking keys, it may cause others to lack confidence in you.

## Signatures

Signatures certify and timestamp documents. If the document is modified, verification of the signature will fail. Unlike encryption which uses public keys to encrypt a document, signatures are created with the user's private key. The recipient of a signed document then verifies the signature using the sender's public key.

### Sign a file

To sign a file use the `--sign` or `-s` flag:

```
 $ gpg --output *doc.sig* --sign *doc*

```

The above also encrypts the file and stores it in binary format.

### Clearsign a file or message

To sign a file without compressing it into binary format use:

```
 $ gpg --clearsign *doc*

```

This wraps the document into an ASCII-armored signature, but does not modify the document.

### Make a detached signature

To create a separate signature file to be distributed separately from the document or file itself, use the `--detach-sig` flag:

```
 $ gpg --output *doc.sig* --detach-sig *doc*

```

This method is often used in distributing software projects to allow users to verify that the program has not been modified by a third part.

### Verify a signature

To verify a signature use the `--verify` flag:

```
 $ gpg --verify *doc.sig*

```

where `*doc.sig*` is the signature you wish to verify.

To verify and decrypt a file at the same time, use the `--decrypt` flag as you normally would in decrypting a file.

If you are verifying a detached signature, both the file and the signature must be present when verifying. For example, to verify Arch Linux's latest iso you would do:

```
 $ gpg --verify *archlinux-<version>-dual.iso.sig*

```

where `*archlinux-<version>-dual.iso*` must be located in the same directory.

## gpg-agent

*gpg-agent* is mostly used as daemon to request and cache the password for the keychain. This is useful if GnuPG is used from an external program like a mail client.

Starting with GnuPG 2.1.0 the use of *gpg-agent* is required. *gpg-agent* is started on-demand by the GnuPG tools, so there is usually no reason to start it manually.

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

### Start gpg-agent with systemd user

It is possible to use the [Systemd/User](/index.php/Systemd/User "Systemd/User") facilities to start the agent.

Create a systemd unit file:

 `~/.config/systemd/user/gpg-agent.service` 
```
[Unit]
Description=GnuPG private key agent
IgnoreOnIsolate=true

[Service]
Type=forking
ExecStart=/usr/bin/gpg-agent --daemon
Restart=on-abort

[Install]
WantedBy=default.target
```

**Note:** If you use non-default value for the [#GNUPGHOME](#GNUPGHOME) environment variable, you need to pass it to the service. See [systemd/User#Environment variables](/index.php/Systemd/User#Environment_variables "Systemd/User") for details.

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
**Note:** The upstream author indicates setting `pinentry-mode loopback` in `gpg.conf` may break other usage, using the commandline option should be preferred if at all possible. [[2]](https://bugs.g10code.com/gnupg/issue1772)

### SSH agent

*gpg-agent* has OpenSSH agent emulation. If you already use the GnuPG suite, you might consider using its agent to also cache your SSH keys. Additionally, some users may prefer the PIN entry dialog GnuPG agent provides as part of its passphrase management.

To start using GnuPG agent for your SSH keys, enable SSH support in the `~/.gnupg/gpg-agent.conf` file:

 `~/.gnupg/gpg-agent.conf` 
```
enable-ssh-support

```

Next, make sure that *gpg-agent* is always started. Either follow [#Start gpg-agent with systemd user](#Start_gpg-agent_with_systemd_user), or add the following to your `.bashrc` file:

 `~/.bashrc` 
```
# Start the gpg-agent if not already running
if ! pgrep -x -u "${USER}" gpg-agent >/dev/null 2>&1; then
  gpg-connect-agent /bye >/dev/null 2>&1
fi

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
*   The test involving the `gnupg_SSH_AUTH_SOCK_by` variable is for the case where the agent is started as `gpg-agent --daemon /bin/sh`, in which case the shell inherits the `SSH_AUTH_SOCK` variable from the parent, *gpg-agent* [[3]](http://git.gnupg.org/cgi-bin/gitweb.cgi?p=gnupg.git;a=blob;f=agent/gpg-agent.c;hb=7bca3be65e510eda40572327b87922834ebe07eb#l1307).

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

```

## Smartcards

GnuPG uses *scdaemon* as an interface to your smartcard reader, please refer to the [man page](/index.php/Man_page "Man page") for details.

### GnuPG only setups

**Note:** To allow scdaemon direct access to USB smarcard readers the optional dependency [libusb-compat](https://www.archlinux.org/packages/?name=libusb-compat) have to be installed

If you do not plan to use other cards but those based on GnuPG, you should check the `reader-port` parameter in `~/.gnupg/scdaemon.conf`. The value '0' refers to the first available serial port reader and a value of '32768' (default) refers to the first USB reader.

### GnuPG with PSCD-Lite

**Note:** [pcsclite](https://www.archlinux.org/packages/?name=pcsclite) and [ccid](https://www.archlinux.org/packages/?name=ccid) have to be installed, and the contained [systemd](/index.php/Systemd#Using_units "Systemd") service `pcscd.service` has to be running, or the socket `pcscd.socket` has to be listening.

PSCD-Lite is a daemon which handles access to smartcard (SCard API). If GnuPG's scdaemon fails to connect the smartcard directly (e.g. by using its integrated CCID support), it will fallback and try to find a smartcard using the PSCD-Lite driver.

#### Always use PSCD-Light

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

## 使用技巧

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
$ gpg --keyserver subkeys.pgp.net --send *<userid>*

```

### Change trust model

By default GnuPG uses the [Web of Trust](https://en.wikipedia.org/wiki/Web_of_Trust "wikipedia:Web of Trust") as the trust model. You can change this to [Trust on First](https://en.wikipedia.org/wiki/Trust_on_First "wikipedia:Trust on First") Use by adding `--trust-model=tofu` when adding a key or adding this option to your GnuPG configuration file. More details are in [this email to the GnuPG list](https://lists.gnupg.org/pipermail/gnupg-devel/2015-October/030341.html).

### Hide all recipient id's

By default the recipient's key ID is in the encrypted message. This can be removed at encryption time for a recipient by using `hidden-recipient *<user-id>*`. To remove it for all recipients add `throw-keyids` to your configuration file. This helps to hide the receivers of the message and is a limited countermeasure against traffic analysis. (Using a little social engineering anyone who is able to decrypt the message can check whether one of the other recipients is the one he suspects.) On the receiving side, it may slow down the decryption process because all available secret keys must be tried (*e.g.* with `--try-secret-key *<user-id>*`).

### Using caff for keysigning parties

To allow users to validate keys on the keyservers and in their keyrings (i.e. make sure they are from whom they claim to be), PGP/GPG uses he [Web of Trust](https://en.wikipedia.org/wiki/Web_of_Trust "wikipedia:Web of Trust"). Keysigning parties allow users to get together in physical location to validate keys. The [Zimmermann-Sassaman](https://en.wikipedia.org/wiki/Zimmermann%E2%80%93Sassaman_key-signing_protocol "wikipedia:Zimmermann–Sassaman key-signing protocol") key-signing protocol is a way of making these very effective. [Here](http://www.cryptnet.net/fdp/crypto/keysigning_party/en/keysigning_party.html) you will find a how-to article.

For an easier process of signing keys and sending signatures to the owners after a keysigning party, you can use the tool *caff*. It can be installed from the AUR with the package [caff-svn](https://aur.archlinux.org/packages/caff-svn/).

To send the signatures to their owners you need a working [MTA](https://en.wikipedia.org/wiki/Message_transfer_agent "wikipedia:Message transfer agent"). If you do not have already one, install [msmtp](/index.php/Msmtp "Msmtp").

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
chown root /dev/ttyN  # where N is the current tty

```

and then change it back after using gpg the first time. The equivalent is likely to be true with `/dev/pts/`.

**Note:** The owner of tty *must* match with the user for which pinentry is running. Being part of the group `tty` **is not** enough.

### Agent complains end of file

The default pinentry program is pinentry-gtk-2, which needs a DBus session bus to run properly. See [General troubleshooting#Session permissions](/index.php/General_troubleshooting#Session_permissions "General troubleshooting") for details.

Alternatively, you can use `pinentry-qt`. See [#pinentry](#pinentry).

### KGpg configuration permissions

There have been issues with [kdeutils-kgpg](https://www.archlinux.org/packages/?name=kdeutils-kgpg) being able to access the `~/.gnupg/` options. One issue might be a result of a deprecated *options* file, see the [bug](https://bugs.kde.org/show_bug.cgi?id=290221) report.

Another user reported that *KGpg* failed to start until the `~/.gnupg` folder is set to `drwxr-xr-x` permissions. If you require this work-around, ensure that the directory contents retain `-rw-------` permissions! Further, report it as a bug to the [developers](https://bugs.kde.org/buglist.cgi?quicksearch=kgpg).

### Conflicts between gnome-keyring and gpg-agent

While the Gnome keyring implements a GPG agent component, as of GnuPG version 2.1, GnuPG ignores the `GPG_AGENT_INFO` environment variable, so that Gnome keyring can no longer be used as a GPG agent.

However, since version 0.9.6 the package [pinentry](https://www.archlinux.org/packages/?name=pinentry) provides the `pinentry-gnome3` program. You may set the following option in your `gpg-agent.conf` file

```
 pinentry-program /usr/bin/pinentry-gnome3

```

in order to make use of that pinentry program.

Since version 0.9.2 all pinentry programs can be configured to optionally save a passphrase with libsecret. For example, when the user is asked for a passphrase via `pinentry-gnome3`, a checkbox is shown whether to save the passphrase using a password manager. Unfortunately, the package [pinentry](https://www.archlinux.org/packages/?name=pinentry) does not have this feature enabled (see [FS#46059](https://bugs.archlinux.org/task/46059) for the reasons). You may use [pinentry-libsecret](https://aur.archlinux.org/packages/pinentry-libsecret/) as a replacement for it, which has support for libsecret enabled.

### mutt and gpg

To be asked for your GnuPG password only once per session as of GnuPG 2.1, see [this forum thread](https://bbs.archlinux.org/viewtopic.php?pid=1490821#p1490821).

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

## 参阅

*   [GNU Privacy Guard Homepage](https://gnupg.org/)
*   [Creating GPG Keys (Fedora)](https://fedoraproject.org/wiki/Creating_GPG_Keys)
*   [OpenPGP subkeys in Debian](https://wiki.debian.org/Subkeys)
*   [A more comprehensive gpg Tutorial](http://blog.sanctum.geek.nz/series/linux-crypto/)
*   [gpg.conf recommendations and best practices](https://help.riseup.net/en/security/message-security/openpgp/gpg-best-practices)
*   [Torbirdy gpg.conf](https://github.com/ioerror/torbirdy/blob/master/gpg.conf)
*   [/r/GPGpractice - a subreddit to practice using GnuPG.](https://www.reddit.com/r/GPGpractice/)