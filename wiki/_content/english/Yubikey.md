The Yubikey is a small [USB token](https://en.wikipedia.org/wiki/Security_token "wikipedia:Security token") that generates [One-Time Passwords](https://en.wikipedia.org/wiki/One-time_password "wikipedia:One-time password") (OTP). It is manufactured by [Yubico](http://www.yubico.com/).

A small section of this article also works for *Fido U2F* USB keys : [#Enabling U2F in the browser](#Enabling_U2F_in_the_browser)

One of its strengths is that it emulates a USB keyboard to send the OTP as text, and thus requires only USB HID drivers found on practically all desktop computers.

## Contents

*   [1 Introduction](#Introduction)
    *   [1.1 How does it work](#How_does_it_work)
    *   [1.2 Security risks](#Security_risks)
        *   [1.2.1 AES key compromise](#AES_key_compromise)
        *   [1.2.2 Validation requests/responses tampering](#Validation_requests.2Fresponses_tampering)
    *   [1.3 YubiCloud and validation servers](#YubiCloud_and_validation_servers)
*   [2 Two-factor authentication with SSH](#Two-factor_authentication_with_SSH)
    *   [2.1 Prerequisites](#Prerequisites)
    *   [2.2 Configuration](#Configuration)
        *   [2.2.1 Authorization Mapping Files](#Authorization_Mapping_Files)
            *   [2.2.1.1 Central authorization mapping](#Central_authorization_mapping)
            *   [2.2.1.2 Per-user authorization mapping](#Per-user_authorization_mapping)
            *   [2.2.1.3 Obtaining the Yubikey token ID (a.k.a. public ID)](#Obtaining_the_Yubikey_token_ID_.28a.k.a._public_ID.29)
        *   [2.2.2 PAM configuration](#PAM_configuration)
            *   [2.2.2.1 The default way](#The_default_way)
            *   [2.2.2.2 Using pure HMAC to authenticate the validation server](#Using_pure_HMAC_to_authenticate_the_validation_server)
            *   [2.2.2.3 Using pure HTTPS to authenticate the validation server](#Using_pure_HTTPS_to_authenticate_the_validation_server)
        *   [2.2.3 SSHD configuration](#SSHD_configuration)
    *   [2.3 That is it!](#That_is_it.21)
    *   [2.4 Explanation](#Explanation)
*   [3 Installing the OATH Applet for a Yubikey NEO](#Installing_the_OATH_Applet_for_a_Yubikey_NEO)
    *   [3.1 Configure the NEO as a CCID Device](#Configure_the_NEO_as_a_CCID_Device)
    *   [3.2 Install the Applet](#Install_the_Applet)
    *   [3.3 (Optional) Install the Yubico Authenticator Desktop client](#.28Optional.29_Install_the_Yubico_Authenticator_Desktop_client)
*   [4 Enabling U2F in the browser](#Enabling_U2F_in_the_browser)
    *   [4.1 Chromium/Chrome](#Chromium.2FChrome)
    *   [4.2 Firefox](#Firefox)
*   [5 Enabling OpenPGP smartcard mode](#Enabling_OpenPGP_smartcard_mode)
*   [6 Yubikey and KeePass](#Yubikey_and_KeePass)
*   [7 Troubleshooting](#Troubleshooting)
    *   [7.1 Yubikey not acting as HID device](#Yubikey_not_acting_as_HID_device)

## Introduction

### How does it work

Yubikey's authentication protocol is based on [symmetric cryptography](https://en.wikipedia.org/wiki/Symmetric_cryptography "wikipedia:Symmetric cryptography"). More specifically, each Yubikey contains a 128-bit [AES](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard "wikipedia:Advanced Encryption Standard") key unique to that device. It is used to encrypt a token made of different fields such as the ID of the key, a counter, a random number, etc. The OTP is made from concatenating the ID of the key with this encrypted token.

This OTP is sent to the target system, to which we want to authenticate. This target system asks a validation server if the OTP is good. The validation server has a mapping of Yubikey IDs -> AES key. Using the key ID in the OTP, it can thus retrieve the AES key and decrypt the other part of the OTP. If it looks OK (plain-text ID and encrypted ID are the same, the counter is bigger than the last seen one to prevent [replay attacks](https://en.wikipedia.org/wiki/Replay_attack "wikipedia:Replay attack")...), then authentication is successful.

The validation server sends that authentication status back to the target system, which grants access or not based on that response.

### Security risks

#### AES key compromise

As you can imagine, the AES key should be kept secret. It cannot be retrieved from the Yubikey itself (or it should not, at least not with software). It is present in the validation server though, so the security of this server is very important.

#### Validation requests/responses tampering

Since the target system relies on the ruling of the validation server, a trivial attack would be to impersonate the validation server. The target system thus needs to authenticate the validation server. 2 methods are available :

*   **HMAC**: This is also symmetric crypto, the target server and validation server share a key that is used to sign requests and responses.
*   **TLS**: Requests and responses travel via HTTP, so TLS (HTTPS) can be used to authenticate and encrypt the connection.

### YubiCloud and validation servers

When you buy a Yubikey, it is preloaded with an AES key that is known only to Yubico. They will not even communicate it to you. Yubico provides a validation server with free unlimited access (YubiCloud). It also offers open-source implementations of the server.

So you can either:

*   choose to use your Yubikey with its preloaded AES key and validate against Yubico's validation server ;
*   or load a new AES key in your Yubikey and run your own validation server.

**Note:** To authenticate the Yubico validation server, you can:

*   **with HMAC**: use [https://upgrade.yubico.com/getapikey/](https://upgrade.yubico.com/getapikey/) to get an HMAC key and ID
*   **with HTTPS**: the validation server's certificate is signed by GoDaddy, and is thus trusted by default in Arch installs (at least if you have package ca-certificates)

## Two-factor authentication with SSH

**Note:** See also: [https://developers.yubico.com/yubico-pam/Yubikey_and_SSH_via_PAM.html](https://developers.yubico.com/yubico-pam/Yubikey_and_SSH_via_PAM.html)

This details how to use a Yubikey to have [two-factor authentication](https://en.wikipedia.org/wiki/Two-factor_authentication "wikipedia:Two-factor authentication") with SSH, that is, to use both a password and a Yubikey-generated OTP.

### Prerequisites

Install [yubico-pam](https://www.archlinux.org/packages/?name=yubico-pam).

**Note:** If you are configuring a distant server to use Yubikey, you should open at least one additional, rescue SSH session, so that you are not locked out of your server if the configuration does not work and you exit your main session inadvertently

**Note:** The following assumes you're using the default Yubico servers. See the [yubico-pam documentation](https://github.com/Yubico/yubico-pam) for options relevant to using your own server.

### Configuration

#### Authorization Mapping Files

A mapping must be made between the YubiKey token ID and the user ID it is attached to. There are two ways to do this, either centrally in one file, or individually, where users can create the mapping in their home directories. If the central authorization mapping file is being used, user home directory mappings will not be used and vice versa.

##### Central authorization mapping

Create a file `/etc/yubico/authorized_yubikeys`, the file must contain a user name and the Yubikey token ID separated by colons (same format as the passwd file) for each user you want to allow onto the system using a Yubikey.

The mappings should look like this, one per line:

```
<first user name>:<Yubikey token ID1>:<Yubikey token ID2>:...
<second user name>:<Yubikey token ID3>:<Yubikey token ID4>:...

```

You can specify multiple key tokens to correspond to one user, but only one is required.

##### Per-user authorization mapping

Each user creates a `~/.yubico/authorized_yubikeys` file inside of their home directory and places the mapping in that file, the file must have only one line:

```
<user name>:<Yubikey token ID1>:<Yubikey token ID2>

```

This is much the same concept as the SSH authorized_keys file.

Note that this file must be readable by the `pam_yubico` module when the user is authenticated, otherwise login will fail. If this is not possible or desired, use the global mapping file instead.

##### Obtaining the Yubikey token ID (a.k.a. public ID)

You can obtain the Yubikey token ID in several ways. One is by removing the last 32 characters of any OTP (One Time Password) generated with your Yubikey. Another is by using the [modhex calculator](http://demo.yubico.com/php-yubico/Modhex_Calculator.php).

Enter your Yubikey OTP and convert it, your Yubikey token ID is 12 characters and listed as:

```
Modhex encoded: XXXXXXX

```

#### PAM configuration

Having set up the `pam_yubico` module, you next need to tell PAM to use it when logging in via SSH. There are several ways of doing this.

##### The default way

Obtain HMAC credentials from Yubico as described in [#YubiCloud and validation servers](#YubiCloud_and_validation_servers). You will receive a Client ID and a secret key.

Add one of the two following lines to the beginnning of `/etc/pam.d/sshd`:

```
auth            required      pam_yubico.so id=CLIENTID authfile=/etc/yubico/authorized_yubikeys

```

if you're using a central authorization mapping file, or

```
auth            required      pam_yubico.so id=CLIENTID

```

if you're using per-user authorization mapping, where `CLIENTID`} is your Client ID. This method utilizes your ID and the server's certificate to authenticate the connection.

**Note:** This will authenticate via Yubico's free YubiCloud servers. If you want to use a different server, add it via the `urllist` parameter.

##### Using pure HMAC to authenticate the validation server

Add `key` to the above lines in `/etc/pam.d/sshd`:

```
auth            required      pam_yubico.so id=CLIENTID key=SECRETKEY ...

```

where `CLIENTID` and `SECRETKEY` are your HMAC ID and key.

You should also disallow unprivileged users to read the file to prevent them from seeing the HMAC credentials:

```
# chmod o-r /etc/pam.d/sshd

```

**Note:** HMAC credentials should be unique to a single target server. That way, if an attacker finds them, he will not be able to craft responses to authenticate to other target servers you own

##### Using pure HTTPS to authenticate the validation server

**Warning:** While this "old" method of using a dummy id still works, it is unknown how secure and/or future-proof it is, as Yubico no longer describes it in their documentation. Proceed at your own risk. At the very least you should ensure that only HTTPS servers with valid certificates are used for authentication.

If you do not want to use HMAC credentials from Yubico, it is still possible to authenticate via the Yubico server by setting `CLIENTID=1` instead of your own ID. Although `pam_yubico`'s default server uses HTTPS already, for security reasons you should specify it manually via the `urllist` parameter, as the servers certificate is the only way in which the connection is authenticated. You can find the keyserver URL by adding the `debug` parameter to the `auth` line.

#### SSHD configuration

You should check that `/etc/ssh/sshd_config` contains these lines and that they are not commented. The `sshd_config` shipped with [openssh](https://www.archlinux.org/packages/?name=openssh) has these set correctly by default.

```
ChallengeResponseAuthentication no
UsePAM yes

```

### That is it!

You should not need to restart anything if you did not change the SSHD config file.

To log in, at the `Password:` prompt of SSH, you have to type your password **without pressing enter** and touch the Yubikey's button. The Yubikey should send a return at the end of the OTP so you do not need to touch the enter key at all.

You can display information about the login data generated by `pam_yubico` by adding the `debug` option to the auth line in`/etc/pam.d/sshd`. However, if you're using a central authorization file, you should remove that option once finished testing, as it causes `pam_yubico` to display the entire content of the central file to every user who logs in using a Yubikey.

### Explanation

This works because the prompt is `pam_yubico.so`'s one, since this module is before `pam_unix.so`, which normally does basic password authentication. So, you are giving a string that is the concatenation of your password and the OTP to `pam_yubico.so`. Since the OTPs have a fixed length (let us call this size N), it just has to get the last N characters to retrieve the OTP, and it assumes that the other characters at the start are the password. It tries to validate the OTP, and in case of success, sends the password to the next PAM module. In Archlinux' default PAM stack, the authenticator `pam_unix.so` is instructed to try receiving a password from the previous module with `try_first_pass`, so it automatically uses the password sent by `pam_yubico.so`.

## Installing the OATH Applet for a Yubikey NEO

These steps will allow you to install the OATH applet onto your Yubikey NEO. This allows the use of Yubico Authenticator in the Google Play Store.

**Note:** These steps are only for NEOs with a firmware version <= 3.1.2\. The current generation NEOs (with U2F) come with the OpenPGP applet already installed)

### Configure the NEO as a CCID Device

1.  Install [yubikey-personalization-gui](https://www.archlinux.org/packages/?name=yubikey-personalization-gui) ([yubikey-personalization-gui-git](https://aur.archlinux.org/packages/yubikey-personalization-gui-git/)).
2.  Add the udev rules and reboot so you can manage the YubiKey without needing to be root
3.  Run `ykpersonalize -m82`, enter `y`, and hit enter.

### Install the Applet

1.  Install [gpshell](https://aur.archlinux.org/packages/gpshell/), [gppcscconnectionplugin](https://aur.archlinux.org/packages/gppcscconnectionplugin/), [globalplatform](https://aur.archlinux.org/packages/globalplatform/), and [pcsclite](https://www.archlinux.org/packages/?name=pcsclite).
2.  Start `pcscd` with `sudo systemctl start pcscd.service`.
3.  Download the most recent CAP file from the [ykneo-oath](http://opensource.yubico.com/ykneo-oath/releases.html) site.
4.  Download `gpinstall.txt` from [GitHub](https://github.com/Yubico/ykneo-oath/blob/master/gpinstall.txt).
5.  Edit the line in gpinstall.txt beginning with `install -file` to reflect the path where the CAP file is located.
6.  Open a terminal and run `gpshell <location of gpinstall.txt>`
7.  Ideally, a bunch of text will scroll by and it ends saying something like

```
 Command --> 80E88013D7C000C400BE00C700CA00CA00B400BE00CE00D200D500D700B000DB00C700DF00BEFFFF00BE00E400AC00AE00AE00DB00E700A
A00EA00ED00ED00ED00BE00EF00F100F400F100F700FA00FF00BE00F700AA01010103010700CA00C400B400AA00F700B400AA00B600C7010C
010C00AA0140012001B0056810B0013005600000056810E0011006B4B44304B44404B44106B44B4405B443400343B002410636810E06B4B44
407326810B004B43103441003334002B102B404B3B403BB4003B440076820A4100221024405B4341008B44600000231066820A100
Wrapped command --> 84E88013DFC000C400BE00C700CA00CA00B400BE00CE00D200D500D700B000DB00C700DF00BEFFFF00BE00E400AC00AE00AE00DB00E700A
A00EA00ED00ED00ED00BE00EF00F100F400F100F700FA00FF00BE00F700AA01010103010700CA00C400B400AA00F700B400AA00B600C7010C
010C00AA0140012001B0056810B0013005600000056810E0011006B4B44304B44404B44106B44B4405B443400343B002410636810E06B4B44
407326810B004B43103441003334002B102B404B3B403BB4003B440076820A4100221024405B4341008B44600000231066820A15D848CB77
27D0EDA00
Response <-- 009000
Command --> 80E60C002107A000000527210108A00000052721010108A000000527210101010003C901000000
Wrapped command --> 84E60C002907A000000527210108A00000052721010108A000000527210101010003C9010000B4648127914A4C7C00
Response <-- 009000
card_disconnect
release_context
```

1.  Unplug the NEO and try it with the Yubico Authenticator app

### (Optional) Install the Yubico Authenticator Desktop client

You can get the desktop version of the Yubico Authenticator by installing [yubico-yubioath-desktop](https://aur.archlinux.org/packages/yubico-yubioath-desktop/) or [yubico-yubioath-desktop-git](https://aur.archlinux.org/packages/yubico-yubioath-desktop-git/).

While `pcscd.service` is running, run `yubioath-gui` and insert your Yubikey when prompted.

## Enabling U2F in the browser

### Chromium/Chrome

In order for the U2F functionality to work with Chromium you need to install the [libu2f-host](https://www.archlinux.org/packages/?name=libu2f-host) library. This provides the [udev rules](https://github.com/Yubico/libu2f-host/blob/master/70-u2f.rules) required to enable access to the Yubikey as a user. Yubikey is by default only accessible by root, and without these rules Chromium will give an error.

### Firefox

To enable U2F support in Firefox, you need to install [this addon](https://github.com/prefiks/u2f4moz). Native support is currently [work in progress](https://bugzilla.mozilla.org/show_bug.cgi?id=1065729).

## Enabling OpenPGP smartcard mode

These steps will allow you to use the OpenPGP functionality of your YubiKey.

1.  Configure your YubiKey as a CCID device as mentioned above.
2.  Install [pcsc-tools](https://www.archlinux.org/packages/?name=pcsc-tools),[ccid](https://www.archlinux.org/packages/?name=ccid) and [libusb-compat](https://www.archlinux.org/packages/?name=libusb-compat)
3.  Enable and start `pcscd` with `sudo systemctl enable pcscd.service`and `sudo systemctl start pcscd.service`
4.  To verify that your YubiKey is ready to be used run `pcsc_scan` which will provide some informations about the connected device. Further you can use `gpg --card-status` to verify that GPG can interact with the card.

## Yubikey and KeePass

Yubikey can be integrated with [KeePass](/index.php/KeePass "KeePass") using [plugins](/index.php/KeePass#Yubikey "KeePass").

## Troubleshooting

Restart, especially if you have completed updates since your Yubikey last worked. Do this even if some functions appear to be functioning.

### Yubikey not acting as HID device

Add udev rule as described in [this article](https://michaelheap.com/yubikey-on-arch/):

```
$ sudo echo 'KERNEL=="hidraw*", SUBSYSTEM=="hidraw", MODE="0664", GROUP="users", ATTRS{idVendor}=="2581", ATTRS{idProduct}=="f1d0"' | sudo tee /etc/udev/rules.d/10-security-key.rules
$ udevadm trigger

```

You may also need to [install](/index.php/Install "Install") the package [libu2f-host](https://www.archlinux.org/packages/?name=libu2f-host) if you want support in chrome.