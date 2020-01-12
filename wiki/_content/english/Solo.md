The [Solo](https://solokeys.com/) is an open-source FIDO2 security key. This article describes how to set up and use it.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Introduction](#Introduction)
*   [2 Installation](#Installation)
    *   [2.1 Setting up udev rules](#Setting_up_udev_rules)
    *   [2.2 Upgrading the firmware](#Upgrading_the_firmware)
    *   [2.3 Test the Solo in your browser](#Test_the_Solo_in_your_browser)
*   [3 Authentication for websites](#Authentication_for_websites)
*   [4 Authentication for Arch Linux](#Authentication_for_Arch_Linux)
    *   [4.1 Installing the PAM module](#Installing_the_PAM_module)
    *   [4.2 Adding a key](#Adding_a_key)
    *   [4.3 Passwordless sudo](#Passwordless_sudo)
    *   [4.4 GDM login](#GDM_login)
    *   [4.5 Other authentication methods](#Other_authentication_methods)
    *   [4.6 Troubleshooting](#Troubleshooting)

## Introduction

The Solo (or SoloKey) is a small [USB Security token](https://en.wikipedia.org/wiki/Security_token "wikipedia:Security token") supporting [Universal 2nd Factor](https://en.wikipedia.org/wiki/Universal_2nd_Factor "wikipedia:Universal 2nd Factor") (U2F) requests, thus acting as a second factor for authentication. It also supports the newer [FIDO2](https://en.wikipedia.org/wiki/FIDO2_Project "wikipedia:FIDO2 Project") standard allowing for passwordless logins.

Compared to a [YubiKey](/index.php/YubiKey "YubiKey") it offers less features but supports firmware upgrades to extend the functionality in the future. Both hardware and software are released as open source.

## Installation

Special drivers are not required for the key to work, but you need to setup necessary [udev](/index.php/Udev "Udev") rules. It is also recommended to install the Solo software and upgrade the firmware of your Solo.

### Setting up udev rules

This task is explained in detail in the [official documentation](https://docs.solokeys.io/solo/udev/). As a convenient alternative, the package [solokeys-udev](https://aur.archlinux.org/packages/solokeys-udev/) installs the rules automatically.

### Upgrading the firmware

Managing your Solo, e.g. upgrading the firmware or setting a PIN, requires the [solo-python](https://aur.archlinux.org/packages/solo-python/) package.

**Note:** The current version of solo-python (0.0.20) [does not compile](https://github.com/solokeys/solo-python/issues/49) with the current [python-fido2](https://www.archlinux.org/packages/?name=python-fido2). Until this is resolved, you need either to downgrade python-fido2 to 0.7.1-3 or apply the patch from [the respecting pull request](https://github.com/solokeys/solo-python/pull/47)

After installing the package, first check if your key is detected.

 `$ solo ls` 
```
:: Solos
123456XXXXXX: SoloKeys Solo 3.0.1
```

Then you can use `solo key update` to perform a firmware upgrade and `solo key change-pin` to set a PIN.

### Test the Solo in your browser

Visit the [Webauthn demo](https://webauthn.io/), type in a username and click on "Register". Your Solo's LED will flash until you click it. After that, you can login to the page only using your Solo, no need for username or password.

## Authentication for websites

U2F is supported by major sites like Google, Facebook, Twitter, or GitHub. Check out [twofactorauth.org](https://twofactorauth.org/) or [dongleauth.info](https://www.dongleauth.info/) to find other websites and links to setup documentation.

## Authentication for Arch Linux

Yubico, the company creating the YubiKey, develops an U2F [PAM](/index.php/PAM "PAM") module. It can be used to act as a second factor during login or replace the need for a password entirely.

### Installing the PAM module

The module is part of the package [pam-u2f](https://www.archlinux.org/packages/?name=pam-u2f).

### Adding a key

Keys need to be added with the tool `pamu2fcfg`:

```
$ mkdir ~/.config/Yubico
$ pamu2fcfg -o pam://hostname -i pam://hostname > ~/.config/Yubico/u2f_keys
```

Click the button of your Solo to confirm the key.

**Note:** If the hostname of your system changes, e.g. because of DHCP in different networks, you would be unable to login. In order to prevent that, it is recommended to specify the abovementioned options and replace `hostname` with the actual hostname.

If you own multiple keys, append them with

 `$ pamu2fcfg -o pam://hostname -i pam://hostname >> ~/.config/Yubico/u2f_keys` 

### Passwordless sudo

**Warning:** Before making any changes to your configuration, create a separate terminal window with superuser permissions (`sudo -s`). This way you can revert any changes if something goes wrong.

Open `/etc/pam.d/sudo` and add

 `auth            sufficient      pam_u2f.so origin=pam://hostname appid=pam://hostname` 

as the first line. Be sure to replace the `hostname` as mentioned above. Then create a new terminal and type `sudo ls`. Your Solo's LED should flash and after clicking it the command is executed.

### GDM login

Open `/etc/pam.d/gdm-password` and add

 `auth            required      pam_u2f.so nouserok origin=pam://hostname appid=pam://hostname` 

after the existing `auth` lines. Please note the use of the `nouserok` option which allows the rule to fail if the user did not configure a key. This way setups with multiple users where only some of them use a Solo are supported.

**Note:** This method will not work with encrypted home partitions because the decryption is not done before the login process completed, so the `u2f_keys` file is unavailable. In this case use a central mapping file as explained in the [official documentation of pam-u2f](https://developers.yubico.com/pam-u2f/).

### Other authentication methods

Enable the PAM module for other services like explained above. For example, to secure the screensaver of [Cinnamon](/index.php/Cinnamon "Cinnamon"), edit `/etc/pam.d/cinnamon-screensaver`.

### Troubleshooting

If you managed to lock yourself out of the system, boot into recovery mode or from a USB pen drive. Then revert the changes in the PAM config and reboot.