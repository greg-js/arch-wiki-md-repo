This article describes how [Yubico](https://yubico.com)'s [YubiKey](https://en.wikipedia.org/wiki/YubiKey "wikipedia:YubiKey") works and how you can use it.

**Note:** Before you overwrite the initial configuration of slot 1, please be aware of the warning under [#Initial configuration](#Initial_configuration).

## Contents

*   [1 Introduction](#Introduction)
    *   [1.1 Installation](#Installation)
    *   [1.2 Understanding the YubiKey](#Understanding_the_YubiKey)
        *   [1.2.1 Inputs](#Inputs)
        *   [1.2.2 Outputs](#Outputs)
    *   [1.3 The button](#The_button)
    *   [1.4 USB connection modes](#USB_connection_modes)
        *   [1.4.1 What does a mode do ?](#What_does_a_mode_do_?)
        *   [1.4.2 Which mode is used?](#Which_mode_is_used?)
        *   [1.4.3 Get enabled modes](#Get_enabled_modes)
        *   [1.4.4 Set the enabled modes](#Set_the_enabled_modes)
    *   [1.5 Two Slots](#Two_Slots)
        *   [1.5.1 Configuration of the slots](#Configuration_of_the_slots)
    *   [1.6 The LED](#The_LED)
    *   [1.7 Initial configuration](#Initial_configuration)
    *   [1.8 Limitations of the passwords typed by YubiKey via USB-keyboard -- or "Why do my password look so weak ?"](#Limitations_of_the_passwords_typed_by_YubiKey_via_USB-keyboard_--_or_"Why_do_my_password_look_so_weak_?")
*   [2 One-time password](#One-time_password)
    *   [2.1 Yubico OTP mode](#Yubico_OTP_mode)
        *   [2.1.1 How does it work](#How_does_it_work)
        *   [2.1.2 Security risks](#Security_risks)
            *   [2.1.2.1 AES key compromise](#AES_key_compromise)
            *   [2.1.2.2 Validation requests/responses tampering](#Validation_requests/responses_tampering)
        *   [2.1.3 YubiCloud and validation servers](#YubiCloud_and_validation_servers)
    *   [2.2 OATH-HOTP mode (RFC 4226)](#OATH-HOTP_mode_(RFC_4226))
*   [3 Challenge-Response](#Challenge-Response)
    *   [3.1 Function and Application of Challenge-Response](#Function_and_Application_of_Challenge-Response)
    *   [3.2 Setup the slot](#Setup_the_slot)
    *   [3.3 Use the slot - get a response for a challenge](#Use_the_slot_-_get_a_response_for_a_challenge)
*   [4 U2F](#U2F)
    *   [4.1 Enabling U2F in the browser](#Enabling_U2F_in_the_browser)
        *   [4.1.1 Chromium/Chrome](#Chromium/Chrome)
        *   [4.1.2 Firefox](#Firefox)
*   [5 CCID Smartcard](#CCID_Smartcard)
    *   [5.1 Enable the CCID mode](#Enable_the_CCID_mode)
    *   [5.2 Use OpenPGP smartcard mode](#Use_OpenPGP_smartcard_mode)
*   [6 Tips and tricks](#Tips_and_tricks)
    *   [6.1 YubiKey and LUKS encrypted partition/disk](#YubiKey_and_LUKS_encrypted_partition/disk)
    *   [6.2 Yubikey and KeePass](#Yubikey_and_KeePass)
        *   [6.2.1 keepassx2](#keepassx2)
        *   [6.2.2 KeePassXC](#KeePassXC)
    *   [6.3 Two-factor authentication with SSH](#Two-factor_authentication_with_SSH)
        *   [6.3.1 Prerequisites](#Prerequisites)
        *   [6.3.2 Configuration](#Configuration)
            *   [6.3.2.1 Authorization Mapping Files](#Authorization_Mapping_Files)
                *   [6.3.2.1.1 Central authorization mapping](#Central_authorization_mapping)
                *   [6.3.2.1.2 Per-user authorization mapping](#Per-user_authorization_mapping)
                *   [6.3.2.1.3 Obtaining the YubiKey token ID (a.k.a. public ID)](#Obtaining_the_YubiKey_token_ID_(a.k.a._public_ID))
            *   [6.3.2.2 PAM configuration](#PAM_configuration)
                *   [6.3.2.2.1 The default way](#The_default_way)
                *   [6.3.2.2.2 Using pure HMAC to authenticate the validation server](#Using_pure_HMAC_to_authenticate_the_validation_server)
                *   [6.3.2.2.3 Using pure HTTPS to authenticate the validation server](#Using_pure_HTTPS_to_authenticate_the_validation_server)
            *   [6.3.2.3 SSHD configuration](#SSHD_configuration)
        *   [6.3.3 That is it!](#That_is_it!)
        *   [6.3.4 Explanation](#Explanation)
*   [7 Maintenance / Upgrades](#Maintenance_/_Upgrades)
    *   [7.1 Installing the OATH Applet for a YubiKey NEO](#Installing_the_OATH_Applet_for_a_YubiKey_NEO)
        *   [7.1.1 Configure the NEO as a CCID Device](#Configure_the_NEO_as_a_CCID_Device)
        *   [7.1.2 Install the Applet](#Install_the_Applet)
        *   [7.1.3 (Optional) Install the Yubico Authenticator Desktop client](#(Optional)_Install_the_Yubico_Authenticator_Desktop_client)
*   [8 Troubleshooting](#Troubleshooting)
    *   [8.1 YubiKey not acting as HID device](#YubiKey_not_acting_as_HID_device)
    *   [8.2 ykman fails to connect to the YubiKey](#ykman_fails_to_connect_to_the_YubiKey)
    *   [8.3 YubiKey fails to bind within a guest VM](#YubiKey_fails_to_bind_within_a_guest_VM)
    *   [8.4 Error: [key] could not be locally signed or gpg: No default secret key: No public key](#Error:_[key]_could_not_be_locally_signed_or_gpg:_No_default_secret_key:_No_public_key)

## Introduction

The YubiKey is a small [USB Security token](https://en.wikipedia.org/wiki/Security_token "wikipedia:Security token") that supports:

*   generating [one-time passwords](https://en.wikipedia.org/wiki/One-time_password "wikipedia:One-time password") (OTP) - using either AES based Yubico OTP algorithm or OATH-HOTP following RFC 4226
*   outputting a up to 63 char long static password
*   handling [challenge-response requests](https://en.wikipedia.org/wiki/Challenge%E2%80%93response_authentication "wikipedia:Challenge–response authentication"), using either Yubico OTP mode or HMAC-SHA1 mode
*   handling [Universal 2nd Factor](https://en.wikipedia.org/wiki/Universal_2nd_Factor "wikipedia:Universal 2nd Factor") (U2F) requests (YubiKey 4 and YubiKey NEO)
*   acting as smartcard (using the [CCID protocol](https://en.wikipedia.org/wiki/CCID_(protocol) "wikipedia:CCID (protocol)")) (YubiKey 4 and YubiKey NEO) - allowing storage of signing, encrypting, authenticating (RSA) keys to be used for instance for SSH login (authentication), Email signature/encryption, git commit signature, etc.

It is manufactured by [Yubico](http://www.yubico.com/).

One of its strengths is that it emulates a USB keyboard to send the OTP as text, and thus requires only USB HID drivers found on practically all desktop computers.

### Installation

There are several packages available:

*   **Yubico PAM** — Module to integrate the YubiKey into [PAM](/index.php/PAM "PAM").

	[https://developers.yubico.com/yubico-pam/](https://developers.yubico.com/yubico-pam/) || [yubico-pam](https://www.archlinux.org/packages/?name=yubico-pam)

*   **YubiKey Manager** — Python library and command-line tool (`ykman`) for configuring a YubiKey over all USB connections. Has optional GUI.

	[https://developers.yubico.com/yubikey-manager/](https://developers.yubico.com/yubikey-manager/) || [yubikey-manager](https://www.archlinux.org/packages/?name=yubikey-manager), [yubikey-manager-qt](https://www.archlinux.org/packages/?name=yubikey-manager-qt)

*   **Yubikey Personalization** — Library and tool to configure slot features over the OTP USB connection. Has optional GUI.

	[https://developers.yubico.com/yubikey-personalization/](https://developers.yubico.com/yubikey-personalization/) || [yubikey-personalization](https://www.archlinux.org/packages/?name=yubikey-personalization), [yubikey-personalization-gui](https://www.archlinux.org/packages/?name=yubikey-personalization-gui)

### Understanding the YubiKey

The YubiKey is a small USB dongle with one button and an LED to communicate with you.

One of its strengths is that it can emulate a USB keyboard to send a password (OTP or static password) as text, and thus requires only USB HID drivers found on practically all computers (desktop, mobile, tablet).

This also makes it vulnerable to keyloggers if the `static password` functionality is used, which is why if possible one should avoid it and try to only use the one-time password (OTP), Challenge-Response and CCID Smartcard functionality.

#### Inputs

The YubiKey takes inputs in the form of:

*   API calls sent to it via the USB interface.
*   short button press
*   long button press

#### Outputs

The YubiKey transforms these inputs into outputs in the form of:

*   Sending keystroke keycodes (emulating a USB keyboard and typing for you)
    This is used to:
    *   type the static password
    *   type the OTP

*   Sending back a Response via the API (over the USB interface).
    This is used to send back:
    *   the response of a Challenge-Response request (calculated using either Yubico OTP mode or HMAC-SHA1 mode)
    *   the response of a U2F Challenge-Response request
    *   the response of a CCID Smartcard related request

### The button

The button activates by slightly touching it. Sometimes it even reacts when you are very close but are not touching it yet.

Depending on the context, touching the button does one of these things:

*   triggering a function (like triggering the output of a static password or of a one-time password (OTP))
*   confirming / allowing a function or access
*   inserting / ejecting the smartcard

In the OTP mode a short press yields slot 1 and a long press yields slot 2.

### USB connection modes

Think of these modes as different subsystems on the key that handle different parts of the keys functionality.

YubiKeys support up to 3 different USB connection/transport modes (depending on model):

	U2F mode

	This subsystem only supports the U2F protocol. It comes fully configured when you buy a YubiKey. It does neither need, nor support any configuration. It can only be enabled / disabled by setting the mode.

	OTP mode

	This subsystem is responsible for OTP, Challenge-Response, Static Passwords. If the transport mode OTP is enabled, the two YubiKey Slots, long press and short press, can be configured and used. These slots can have one of the following credentials configured: a [Yubico OTP](https://developers.yubico.com/OTP/) (which is what comes preconfigured in the short press slot on a new key), a static password, a challenge-response credential, an OATH-HOTP credential. All this functionality is found in the `ykman slot` commands.

	CCID mode

	This is the subsystem allowing the key to act as a Smartcard (using CCID protocol).

**Note:** See [#The LED](#The_LED) about CCID related blinking.

#### What does a mode do ?

A mode defines:

*   how the YubiKey is accessed (e.g. if the CCID mode is activated, then `ykman` will access the YubiKey in CCID mode, meaning if you do not have `pcscd` running, then even a `ykman info` will fail) and
*   what functionality is available or not (e.g. if you deactivate the U2F mode, then your YubiKey will not handle any U2F requests anymore)

These modes can be activated/deactivated independently from each other.

#### Which mode is used?

Only one connection mode will be used at any given point in time to communicate with the YubiKey.

When you plug in your YubiKey one, connection mode will be chosen. The order of preference (TODO:verify) is:

*   If the **CCID mode** is activated, this mode will be chosen.
*   Otherwise (so CCID deactivated and) if the **U2F mode** is activated, this mode will be chosen.
*   Otherwise (so CCID and U2F deactivated and) if the **OTP mode** is activated, this mode will be chosen.

#### Get enabled modes

`ykman mode` will tell you what modes are currently activated/enabled/available. This could output something like

 `Current connection mode is: OTP+U2F+CCID` 

Meaning that currently the OTP, U2F and CCID subsystem of the key are enabled .

#### Set the enabled modes

`ykman mode <MODE>` will allow you to define which modes should be activated/enabled/available.

*   `<MODE>` can be a string, such as `OTP+U2F+CCID`, or a shortened form `o+u+c`.
    With "+" you can combine multiple modes that you wish to be enabled.
*   `<MODE>` can be a mode-number, which is one number that encodes several enabled modes (like flags) into one value.
    The only valid modes when using numbers is 0 - 6 ([see here](https://github.com/Yubico/yubikey-manager/blob/master/ykman/util.py#L94)). The extra flags are not part of the mode in that sense, they just need to be set at the same time as the mode is set.

Usually what you want is to make all functionality available (you will still need to potentially configure stuff, see functionality sections below for more details). In order to do so you can use:

`ykman mode c+u+o` or `ykman mode 6`

**Note:** Using the "80" mode-number or the corresponding `--touch-eject` parameter of `ykman mode` can only be used when the device is *only* in CCID mode (by running `ykman mode ccid --touch-eject` for instance).

Once the `--touch-eject` flag is set, you should be able to eject/insert the smartcard by pressing the button. The LED should indicate if the card is inserted or not as well.

**Warning:** But using the 80 mode-number or the corresponding `--touch-eject` is not recommend as it would prevent you from using the U2F and OTP features of the YubiKey.

**Note:** The often seen:

`ykman mode c+u+o --touch-eject` or `ykman mode 86`

will ignore the `--touch-eject` and be identical to the above recommended `ykman mode 6`.

86 is not a valid mode. It might be a bug that the tool accepts higher values ([see here](https://github.com/Yubico/yubikey-manager/issues/20#issuecomment-326496204)).

### Two Slots

Only if the OTP mode is activated (see Modes of the YubiKey below), the Yubikey provides 2 slots.

If the transport mode OTP is enabled, the two YubiKey Slots, long press and short press, can be configured and used.

#### Configuration of the slots

These slots can have one of the following credentials configured: a [Yubico OTP](https://developers.yubico.com/OTP/) (which is what comes preconfigured in the short press slot on a new key), a static password, a challenge-response credential, an OATH-HOTP credential. All this functionality is found in the `ykman slot` commands.

**Note:** A slot has either a Yubico OTP or a challenge-response credential configured. More general: One, and only one, type of the above listed possible credential per slot.

There are several flags that can be set during the configuration of the slots. These flags /cannot/ be read from the device once written. However, the behaviour of the device should change when the flags are set ;)

**Note:** Actually most of (all of??) the parameters and details you use during configuration of the slots, cannot be read back, once written to the YubiKey.

### The LED

The YubiKey has a small green LED able to communicate with you. Its message to you actually depends on the currently used [#USB connection modes](#USB_connection_modes) of your YubiKey.

The possible messages are:

*   *steady on*: Press now, to allow access. (typically (TODO exclusively?) U2F mode)
*   *slow blinking*: Power/setting up/ready for use (TODO explain)
*   *rapid blinking*: Error, configuring driver (TODO explain)

**Note:** If the CCID mode is turned on, then the LED of the key is always shortly flashing every two-three seconds once inserted.
You can turn the blinking off by disabling the CCID mode. This slow blinking just shows that the device has power, alternatively it shows a need for a button press. On Windows this behavior will typically stop once drivers are installed and it is ready for use. Mac and Linux systems will keep blinking; here [the best current workaround](https://github.com/Yubico/yubikey-manager/issues/20#issuecomment-326496204) to get the LED to blink less is to disable CCID.

### Initial configuration

On a new YubiKey the Yubico OTP is preconfigured on slot 1\.

**Warning:** Before you overwrite your slot 1, please be aware that one is not able to reconfigure the same trust level [see here](https://forum.yubico.com/viewtopic.php?f%3D16&t%3D1960). Meaning:

One could think that it is a good idea to reset configuration slot 1 to a new OTP. But then a "VV" prefix in your credentials must be used. Whereas the factory credentials on your Yubikey use a "CC" prefix. You can upload a "VV" credential using the Yubico personalization tool GUI or manually upload the new AES key to the [yubico.com website](https://upload.yubico.com/) in order to regain the same functionality than with the original factory configuration. VV credentials are not less secure than CC. However some services may only trust CC credentials as they believe that the user process is more prone to security vulnerabilities. This is because you could have malware on your machine or someone intercepting your key when sending it to the YubiCloud.

### Limitations of the passwords typed by YubiKey via USB-keyboard -- or "Why do my password look so weak ?"

The YubiKey can type passwords (OTP or Static Password) for you by acting as USB keyboard and sending scan-codes like if you would type.

A limitation of the YubiKey, however, prevents you from choosing characters that require a modifier key other than Shift. And in order for the YubiKey to work with all possible keyboard layouts (e.g. the `Z` on a German keyboard has a different scan-code than the `Z` on a US keyboard) it is necessary to limit the characters used by YubiKey passwords to the ModHex alphabet + Digits (0-9) (+ optionally "!" as the only available Symbol in static passwords).

The 16 characters used in the ModHex alphabet are: `c,b,d,e,f,g,h,i,j,k,l,n,r,t,u,v`. These characters share a property that makes them very valuable to a YubiKey: They use the same scan codes across a very large number of keyboard layouts. In other words, the scan code 0x06 maps to the character c for English, Swedish, German, French, and many others.

[See here for full info](https://www.yubico.com/wp-content/uploads/2015/11/Yubico_WhitePaper_Static_Password_Function.pdf)

## One-time password

### Yubico OTP mode

The Yubico OTP mode is AES symmetric key based. On a new YubiKey the Yubico OTP is preconfigured on slot 1\. This initial AES symmetric key is stored in the YubiKey and the same AES key is already stored on the Yubico Authentication server. This allows validating against YubiCloud, meaning the use of Yubico OTP in combination with the Yubico Forum website for instance or on [https://demo.yubico.com](https://demo.yubico.com)).

The initial configuration and AES key stored in slot 1 can of course be overwritten.

**Warning:** Please read [#Initial configuration](#Initial_configuration) before you overwrite the intial configuration of slot 1 that your YubiKey comes shipped with.

#### How does it work

Yubikey's authentication protocol is based on [symmetric cryptography](https://en.wikipedia.org/wiki/Symmetric_cryptography "wikipedia:Symmetric cryptography"). More specifically, each YubiKey contains a 128-bit [AES](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard "wikipedia:Advanced Encryption Standard") key unique to that device. It is used to encrypt a token made of different fields such as the ID of the key, a counter, a random number, etc. The OTP is made from concatenating the ID of the key with this encrypted token.

This OTP is sent to the target system to which we want to authenticate. This target system asks a validation server if the OTP is good. The validation server has a mapping of YubiKey IDs -> AES key. Using the key ID in the OTP, it can thus retrieve the AES key and decrypt the other part of the OTP. If it looks OK (plain-text ID and encrypted ID are the same, the counter is bigger than the last seen one to prevent [replay attacks](https://en.wikipedia.org/wiki/Replay_attack "wikipedia:Replay attack"), then authentication is successful.

The validation server sends that authentication status back to the target system, which grants access or not based on that response.

#### Security risks

##### AES key compromise

As you can imagine, the AES key should be kept secret. It cannot be retrieved from the YubiKey itself (or it should not, at least not with software). It is present in the validation server though, so the security of this server is very important.

##### Validation requests/responses tampering

Since the target system relies on the ruling of the validation server, a trivial attack would be to impersonate the validation server. The target system thus needs to authenticate the validation server. 2 methods are available :

*   **HMAC**: This is also symmetric cryptography, the target server and validation server share a key that is used to sign requests and responses.
*   **TLS**: Requests and responses travel via HTTP, so TLS (HTTPS) can be used to authenticate and encrypt the connection.

#### YubiCloud and validation servers

When you buy a YubiKey, it is preloaded with an AES key that is known only to Yubico. They will not even communicate it to you. Yubico provides a validation server with free unlimited access (YubiCloud). It also offers open-source implementations of the server.

So you can either:

*   choose to use your YubiKey with its preloaded AES key and validate against Yubico's validation server ;
*   or load a new AES key in your YubiKey and run your own validation server.

**Note:** To authenticate the Yubico validation server, you can:

*   **with HMAC**: use [https://upgrade.yubico.com/getapikey/](https://upgrade.yubico.com/getapikey/) to get an HMAC key and ID
*   **with HTTPS**: the validation server's certificate is signed by GoDaddy, and is thus trusted by default in Arch installs (at least if you have package ca-certificates)

### OATH-HOTP mode (RFC 4226)

## Challenge-Response

### Function and Application of Challenge-Response

This technique can be used to authenticate.

A challenge is sent to the YubiKey and a response is (auto-magically) calculated and send back. This calculation needs a secret (e.g. an AES key in case of the Yubico OTP mode) The same challenge always results in the same response. Without the secret this calculation is not meant to be feasable. Even if in the possession of many challenge-response pairs.

This can be used for:

*   true 2-factor (possession and knowledge) authentication:
    If you combine the response (possession factor) with a password (knowledge factor) and to authenticate you need to present the triple (challenge,response, password) to 3rd party. In which case the challenge and the corresponding response can be (publicly) send to a 3rd party to authenticate the possession factor, by redoing basically the same (auto-magical) calculation. The needed secret needs to be shared with 3rd party to allow an authentication.

*   semi 2-factor (possession and knowledge) authentication:
    The challenge can be public. Only with the possession of the YubiKey hardware the response can be generated. This can be used to create a "sort-of" 2-factor authentication (possession and knowledge): If you combine the response (possession factor) with a password (knowledge factor) and use the result for instance as passphrase for cryptsetup.

This functionality will consume one slot. And it is used via API calls to the YubiKey. So you usually use some tool to communicate the challenge to your YubiKey and get back the response.

There are two Challenge-Response modes:

*   Yubico OTP mode
*   HMAC-SHA1 mode

### Setup the slot

In order to setup slot `2` in challenge-response mode you may run:

 `ykpersonalize -v -2 -ochal-resp -ochal-hmac -ohmac-lt64 -oserial-api-visible -ochal-btn-trig` 

Above arguments mean:

*   Verbose output (`-v`)
*   Use slot 2 (`-2`)
*   Set challenge-response mode (`-ochal-resp`)
*   Generate HMAC-SHA1 challenge responses (`-ochal-hmac`)
*   Calculate HMAC on less than 64 bytes input (`-ohmac-lt64`)
*   Allow Yubikey serial number to be read using an API call (`-oserial-api-visible`)
*   Require touching Yubikey before issue response (`-ochal-btn-trig`)

You may also enable challenge-response mode using graphical interface through [yubikey-personalization-gui](https://www.archlinux.org/packages/?name=yubikey-personalization-gui)

**Note:** Before you overwrite the initial configuration of slot 1, please be aware of the **Warning** under [#Initial configuration](#Initial_configuration).

### Use the slot - get a response for a challenge

To use a Challenge-Response slot (no matter which mode):

 `ykchalresp -2 <CHALLENGE>` 

## U2F

### Enabling U2F in the browser

#### Chromium/Chrome

[Chromium/Tips and tricks#U2F authentication](/index.php/Chromium/Tips_and_tricks#U2F_authentication "Chromium/Tips and tricks")

#### Firefox

[Firefox/Tweaks#Fido U2F authentication](/index.php/Firefox/Tweaks#Fido_U2F_authentication "Firefox/Tweaks")

## CCID Smartcard

### Enable the CCID mode

Please see [#Set the enabled modes](#Set_the_enabled_modes). Enable at least the CCID mode. CCID mode should be enabled by default on all YubiKeys shipped since November 2015 [[1]](https://www.yubico.com/support/knowledge-base/categories/articles/use-yubikey-yubikey-windows-hello-app/).

### Use OpenPGP smartcard mode

See [GnuPG#Smartcards](/index.php/GnuPG#Smartcards "GnuPG")

## Tips and tricks

### YubiKey and LUKS encrypted partition/disk

YubiKey can be used to strengthen the security of your [LUKS](/index.php/LUKS "LUKS") encrypted partition/disk.

One way to achieve it is to use a Challenge-Response mode for creating strong LUKS passphrases. [yubikey-full-disk-encryption](https://github.com/agherzan/yubikey-full-disk-encryption) is a robust and comfortable to use implementation of an [initramfs](/index.php/Initramfs "Initramfs") hook and on-demand scripts to create/open LUKS encrypted partitions/disks using a stored or manually provided challenge.

Another way of using YubiKey for full disk encryption is to utilize its OpenPGP applet to decrypt the LUKS keyfile during boot. [initramfs-scencrypt](https://github.com/fuhry/initramfs-scencrypt) is a set of hooks for initramfs that automate this process.

### Yubikey and KeePass

Yubikey can be integrated with [KeePass](/index.php/KeePass "KeePass") using [plugins](/index.php/KeePass#Yubikey "KeePass").

For a native open-source implementation of KeePass have a look at:

#### keepassx2

[keepassx2](https://www.archlinux.org/packages/?name=keepassx2) ([see keepassx.org](https://keepassx.org/)) a keepass QT FOSS reimplementation, extremely stable and available for Windows, MacOSX and Linux.

#### KeePassXC

[keepassxc](https://www.archlinux.org/packages/?name=keepassxc) ([see keepassxc.org](https://keepassxc.org/)) a KeePassX fork that integrated YubiKey into KeePassX v2.
The integration covers Challenge-Response as security factor to open the database, but also the generation of OTP using the YubiKey.

In order to have a KeePassXC database work on Android (using the [Keepass2Android app](https://play.google.com/store/apps/details?id=keepass2android.keepass2android)), you need to use version 1.06 ([currently in beta](https://play.google.com/apps/testing/keepass2android.keepass2android); 1.06b) of the app. You also need to save the database file in the KDBX 4 format, since Keepass2Android do not support the KDBX 3 format.

YubiKey support in Keepass2Android (which is compatible with KeePassXC) is tracked [on GitHub](https://github.com/PhilippC/keepass2android/issues/4).

### Two-factor authentication with SSH

**Note:** See also: [https://developers.yubico.com/yubico-pam/Yubikey_and_SSH_via_PAM.html](https://developers.yubico.com/yubico-pam/Yubikey_and_SSH_via_PAM.html)

This details how to use a Yubikey to have [two-factor authentication](https://en.wikipedia.org/wiki/Two-factor_authentication "wikipedia:Two-factor authentication") with SSH, that is, to use both a password and a Yubikey-generated OTP.

#### Prerequisites

Install [yubico-pam](https://www.archlinux.org/packages/?name=yubico-pam).

**Note:** If you are configuring a distant server to use Yubikey, you should open at least one additional, rescue SSH session, so that you are not locked out of your server if the configuration does not work and you exit your main session inadvertently

**Note:** The following assumes you are using the default Yubico servers. See the [yubico-pam documentation](https://github.com/Yubico/yubico-pam) for options relevant to using your own server.

#### Configuration

##### Authorization Mapping Files

A mapping must be made between the YubiKey token ID and the user ID it is attached to. There are two ways to do this, either centrally in one file, or individually, where users can create the mapping in their home directories. If the central authorization mapping file is being used, user home directory mappings will not be used and vice versa.

###### Central authorization mapping

Create a file `/etc/yubico/authorized_yubikeys`, the file must contain a user name and the Yubikey token ID separated by colons (same format as the passwd file) for each user you want to allow onto the system using a Yubikey.

The mappings should look like this, one per line:

```
<first user name>:<Yubikey token ID1>:<Yubikey token ID2>:...
<second user name>:<Yubikey token ID3>:<Yubikey token ID4>:...

```

You can specify multiple key tokens to correspond to one user, but only one is required.

###### Per-user authorization mapping

Each user creates a `~/.yubico/authorized_yubikeys` file inside of their home directory and places the mapping in that file, the file must have only one line:

```
<user name>:<Yubikey token ID1>:<Yubikey token ID2>

```

This is much the same concept as the SSH authorized_keys file.

Note that this file must be readable by the `pam_yubico` module when the user is authenticated, otherwise login will fail. If this is not possible or desired, use the global mapping file instead.

###### Obtaining the YubiKey token ID (a.k.a. public ID)

You can obtain the YubiKey token ID in several ways. One is by removing the last 32 characters of any OTP (One Time Password) generated with your YubiKey. Another is by using the [modhex calculator](http://demo.yubico.com/php-yubico/Modhex_Calculator.php).

Enter your YubiKey OTP and convert it, your Yubikey token ID is 12 characters and listed as:

```
Modhex encoded: XXXXXXX

```

##### PAM configuration

Having set up the `pam_yubico` module, you next need to tell PAM to use it when logging in via SSH. There are several ways of doing this.

###### The default way

Obtain HMAC credentials from Yubico as described in [#YubiCloud and validation servers](#YubiCloud_and_validation_servers). You will receive a Client ID and a secret key.

Add one of the two following lines to the beginnning of `/etc/pam.d/sshd`:

```
auth            required      pam_yubico.so id=CLIENTID authfile=/etc/yubico/authorized_yubikeys

```

if you are using a central authorization mapping file, or

```
auth            required      pam_yubico.so id=CLIENTID

```

if you are using per-user authorization mapping, where `CLIENTID`} is your Client ID. This method utilizes your ID and the server's certificate to authenticate the connection.

**Note:** This will authenticate via Yubico's free YubiCloud servers. If you want to use a different server, add it via the `urllist` parameter.

###### Using pure HMAC to authenticate the validation server

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

###### Using pure HTTPS to authenticate the validation server

**Warning:** While this "old" method of using a dummy id still works, it is unknown how secure and/or future-proof it is, as Yubico no longer describes it in their documentation. Proceed at your own risk. At the very least you should ensure that only HTTPS servers with valid certificates are used for authentication.

If you do not want to use HMAC credentials from Yubico, it is still possible to authenticate via the Yubico server by setting `CLIENTID=1` instead of your own ID. Although `pam_yubico`'s default server uses HTTPS already, for security reasons you should specify it manually via the `urllist` parameter, as the servers certificate is the only way in which the connection is authenticated. You can find the keyserver URL by adding the `debug` parameter to the `auth` line.

##### SSHD configuration

You should check that `/etc/ssh/sshd_config` contains these lines and that they are not commented. The `sshd_config` shipped with [openssh](https://www.archlinux.org/packages/?name=openssh) has these set correctly by default.

```
ChallengeResponseAuthentication no
UsePAM yes

```

#### That is it!

You should not need to restart anything if you did not change the SSHD config file.

To log in, at the `Password:` prompt of SSH, you have to type your password **without pressing enter** and touch the Yubikey's button. The Yubikey should send a return at the end of the OTP so you do not need to touch the enter key at all.

You can display information about the login data generated by `pam_yubico` by adding the `debug` option to the auth line in`/etc/pam.d/sshd`. However, if you are using a central authorization file, you should remove that option once finished testing, as it causes `pam_yubico` to display the entire content of the central file to every user who logs in using a Yubikey.

#### Explanation

This works because the prompt is `pam_yubico.so`'s one, since this module is before `pam_unix.so`, which normally does basic password authentication. So, you are giving a string that is the concatenation of your password and the OTP to `pam_yubico.so`. Since the OTPs have a fixed length (let us call this size N), it just has to get the last N characters to retrieve the OTP, and it assumes that the other characters at the start are the password. It tries to validate the OTP, and in case of success, sends the password to the next PAM module. In Archlinux' default PAM stack, the authenticator `pam_unix.so` is instructed to try receiving a password from the previous module with `try_first_pass`, so it automatically uses the password sent by `pam_yubico.so`.

## Maintenance / Upgrades

### Installing the OATH Applet for a YubiKey NEO

These steps will allow you to install the OATH applet onto your YubiKey NEO. This allows the use of Yubico Authenticator in the Google Play Store.

**Note:** These steps are only for NEOs with a firmware version <= 3.1.2\. The current generation NEOs (with U2F) come with the OpenPGP applet already installed)

#### Configure the NEO as a CCID Device

1.  Install [yubikey-personalization-gui](https://www.archlinux.org/packages/?name=yubikey-personalization-gui) ([yubikey-personalization-gui-git](https://aur.archlinux.org/packages/yubikey-personalization-gui-git/)).
2.  Add the udev rules and reboot so you can manage the YubiKey without needing to be root
3.  Run `ykpersonalize -m82`, enter `y`, and hit enter.

#### Install the Applet

1.  Install [gpshell](https://aur.archlinux.org/packages/gpshell/), [gppcscconnectionplugin](https://aur.archlinux.org/packages/gppcscconnectionplugin/), [globalplatform](https://aur.archlinux.org/packages/globalplatform/), and [pcsclite](https://www.archlinux.org/packages/?name=pcsclite).
2.  [Start](/index.php/Start "Start") `pcscd.service`.
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

#### (Optional) Install the Yubico Authenticator Desktop client

You can get the desktop version of the Yubico Authenticator by installing [yubico-yubioath-desktop](https://aur.archlinux.org/packages/yubico-yubioath-desktop/) or [yubico-yubioath-desktop-git](https://aur.archlinux.org/packages/yubico-yubioath-desktop-git/).

While `pcscd.service` is running, run `yubioath-gui` and insert your Yubikey when prompted.

## Troubleshooting

Restart, especially if you have completed updates since your Yubikey last worked. Do this even if some functions appear to be functioning.

### YubiKey not acting as HID device

Add udev rule as described in [this article](https://michaelheap.com/yubikey-on-arch/):

 `/etc/udev/rules.d/10-security-key.rules`  `KERNEL=="hidraw*", SUBSYSTEM=="hidraw", MODE="0664", GROUP="users", ATTRS{idVendor}=="2581", ATTRS{idProduct}=="f1d0"` 

Run `udevadm trigger` afterwards.

You may also need to [install](/index.php/Install "Install") the package [libu2f-host](https://www.archlinux.org/packages/?name=libu2f-host) if you want support in chrome.

### ykman fails to connect to the YubiKey

If the manager fails to connect to the YubiKey, make sure you have started `pcscd.service` or `pcscd.socket`.

### YubiKey fails to bind within a guest VM

Assuming the Yubikey is available to the guest, the issue results from a driver binding to the device on the host. To unbind the device, the bus and port information is needed from `dmesg` on the host:

```
$ dmesg | grep -B1 Yubico | tail -n 2 | head -n 1 | sed -E 's/^\[[^]]+\] usb ([^:]*):.*/\1/'

```

The resulting USB id should be of the form `X-Y.Z` or `X-Y`. Then, on the host, use `find` to search `/sys/bus/usb/drivers` for which driver the Yubikey is binded to (e.g. `usbhid` or `usbfs`).

```
$ find /sys/bus/usb/drivers -name "*X-Y.Z*"

```

To unbind the device, use the result from the previous command (i.e. `/sys/bus/usb/drivers/<DRIVER>/X-Y.Z:1.0`):

```
# echo 'X-Y.Z:1.0' > /sys/bus/usb/drivers/<DRIVER>/unbind

```

### Error: [key] could not be locally signed or gpg: No default secret key: No public key

Occurs when attempting to sign keys on a non-standard keyring while a YubiKey is plugged in, e.g. as [Pacman](/index.php/Pacman/Package_signing "Pacman/Package signing") does in `pacman-key --populate archlinux`. The solution is to remove the offending YubiKey and start over.