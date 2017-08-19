The [Mooltipass](https://www.themooltipass.com/) is an open hardware and open software, hardware password keeper in which users store their credentials for authenticating against web application, [PAM](/index.php/PAM "PAM") session, and password protected applications.

The device can be used with any USB compatible system that supports HID class devices.

As a daily based user, one is able to interact directly with the device by using a clickable scroll-wheel or is free to use one of the available browser extensions/applications.

## Contents

*   [1 Introduction](#Introduction)
*   [2 Password storing](#Password_storing)
*   [3 Firmware upgrade](#Firmware_upgrade)
*   [4 Additional features](#Additional_features)
*   [5 Udev rules](#Udev_rules)
*   [6 Usage](#Usage)
    *   [6.1 Chromium](#Chromium)
    *   [6.2 Firefox](#Firefox)
    *   [6.3 Moolticute](#Moolticute)
        *   [6.3.1 Moolticute-CLI](#Moolticute-CLI)
        *   [6.3.2 Moolticute_ssh-agent](#Moolticute_ssh-agent)
    *   [6.4 Mooltipy](#Mooltipy)
*   [7 See also](#See_also)

## Introduction

The team behind Mooltipass was faced with the great complexity of password based authentication which require a strict policy including:

*   A unique password for every usage;
*   A hardly-guessable password;

In order to combine security of such policy and usability people came with software [password managers](/index.php/Password_manager "Password manager") like [KeePass](/index.php/KeePass "KeePass"). Unfortunately, such solution implies that all credentials remains in computer memory, so it could eventually be stolen by a malicious software.

Mooltipass is an external device, on which credential are stored encrypted using [AES](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard "wikipedia:Advanced Encryption Standard")-[CTR](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#Counter_.28CTR.29 "wikipedia:Block cipher mode of operation") and a key of 256 bits stored on an pin-locked smartcard. When plugged, the Mooltipass emulates an HID device and will act like a keyboard to send your credentials information to the targeted application. Even if an attacker is able to sniff at some point the communication between the device and the host it is likely that he will not be able to gather all credentials nor to inject its own data.

## Password storing

The smartcard previously introduced is used to identify an user. Note that multiple user must have different smartcards, but can use the same mooltipass.

Credentials are stored on the device flash memory with the following information: domain, username, password, comments.

**Note:** Out all of this fields only the password is stored encrypted (and salted).

The following list limits of the storing capabilities:

*   The flash memory is of 8Mb;
*   One password can be up to 32 characters long;

**Warning:** Entering a wrong PIN 4 times will block and destroy the smartcard.

## Firmware upgrade

The upgrade of the firmware is made with a signed bundle. Every device gets a dedicated AES key fused into the board by the main developer.

## Additional features

In addition, the mooltipass benefits from the [ATMega32u4](http://www.atmel.com/devices/ATMEGA32U4.aspx) and exposes a custom Random Number Generator that is used to generate random passwords.

## Udev rules

[mooltipass-udev](https://aur.archlinux.org/packages/mooltipass-udev/) provide udev rules that allow access to the device for every classical user from a session or using libusb.

## Usage

Mooltipass has been designed to be easy to use for everyone. The main way of interacting with it is through browser application and/or extension.

### Chromium

[Chromium](/index.php/Chromium "Chromium") was the first target for Mooltipass, the team created one application [chromium-app-mooltipass](https://aur.archlinux.org/packages/chromium-app-mooltipass/) for easily managing the password database, backups and device settings.

Also there is an extension, [chromium-extension-mooltipass](https://aur.archlinux.org/packages/chromium-extension-mooltipass/) that detects login forms on web page and selects the right credential for you on the device. The user only has to check on the Mooltipass screen that the request is legitimate and to approve/deny using the hardware scroll-wheel.

**Note:** Both the [extension](https://github.com/limpkin/mooltipass/tree/master/chrome_extension) and the [application](https://github.com/limpkin/mooltipass/tree/master/chrome_app) are open source.

### Firefox

Like Chromium, [Firefox](/index.php/Firefox "Firefox") users can use [firefox-extension-mooltipass](https://aur.archlinux.org/packages/firefox-extension-mooltipass/) for easy interaction between web sites and credentials stored on the device.

### Moolticute

[moolticute](https://aur.archlinux.org/packages/moolticute/) is an effort to build a cross-platform application that could interact with the mooltipass outside of a browser. The application is based on C++/Qt and provide both a daemon that will handle every operation with the device and an GUI application, that could replace the chrome app.

**Note:** The daemon expose a web socket interface so anyone could build tools for its own needs.

#### Moolticute-CLI

For scripting purpose there is [moolticute-cli](https://aur.archlinux.org/packages/moolticute-cli/) which allow one to interact with the Mooltipass through moolticuted from the command line.

#### Moolticute_ssh-agent

[moolticute_ssh-agent](https://aur.archlinux.org/packages/moolticute_ssh-agent/) benefit from the filesystem support of Mooltipass so users are able to store their (unencrypted) [SSH keys](/index.php/SSH_keys "SSH keys"). Moolticute_ssh-agent implement an SSH agent that allows to load the key from the device.

### Mooltipy

Last client implementation is [mooltipy](https://github.com/osquat/mooltipy) that implement both some CLI tools and an Python module that could be used for scripting.

## See also

*   [The making of a secure open source password keeper (FOSDEM 2017)](https://fosdem.org/2017/schedule/event/password_keeper/)
*   [Mooltipass repository](https://github.com/limpkin/mooltipass)
*   [Moolticute repository](https://github.com/raoulh/moolticute)
*   [Mooltipass mini teardown](https://fry.blueblue.fr/mpm/teardown/)
*   [Mooltipass mini user manual](https://github.com/limpkin/mooltipass/raw/master/user_manual_mini.pdf)
*   [Mooltipass mini datasheets](https://github.com/limpkin/mooltipass/tree/master/datasheets/mini)
*   [Mooltipass mini firmware code](https://github.com/limpkin/mooltipass/tree/master/source_code)