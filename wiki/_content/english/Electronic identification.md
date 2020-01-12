Related articles

*   [Common Access Card](/index.php/Common_Access_Card "Common Access Card")
*   [Smartcards](/index.php/Smartcards "Smartcards")

An [electronic identification](https://en.wikipedia.org/wiki/Electronic_identification "w:Electronic identification") ("eID") is an electronic identification solution of citizens or organizations, for example in view to access benefits or services provided by government authorities, banks or other companies. Apart from online authentication many eICs also give users the option to sign electronic documents with a digital signature.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Setup per country](#Setup_per_country)
    *   [2.1 Belgium](#Belgium)
    *   [2.2 Estonia](#Estonia)
        *   [2.2.1 DigiDoc](#DigiDoc)
        *   [2.2.2 Chromium](#Chromium)
        *   [2.2.3 Firefox](#Firefox)
        *   [2.2.4 For new cards issued since December 2018](#For_new_cards_issued_since_December_2018)
    *   [2.3 Germany](#Germany)
        *   [2.3.1 ReinerSCT devices](#ReinerSCT_devices)
    *   [2.4 Sweden](#Sweden)

## Installation

a All types of electronic identification **require** installing the [ccid](https://www.archlinux.org/packages/?name=ccid) package. After installation, [enable](/index.php/Enable "Enable"), and [start](/index.php/Start "Start") `pcscd.socket`. In addition, [ACS](https://www.acs.com.hk/en/product-lines/2/pc-linked-smart-card-readers/) smart cards also require the [acsccid](https://www.archlinux.org/packages/?name=acsccid) package.

[pcsc-tools](https://www.archlinux.org/packages/?name=pcsc-tools) contains `pcsc_scan` program that can be used to check smart card detection [Smartcards#Scan for card reader](/index.php/Smartcards#Scan_for_card_reader "Smartcards").

## Setup per country

### Belgium

[https://eid.belgium.be/en](https://eid.belgium.be/en)

Install the [eid-mw](https://aur.archlinux.org/packages/eid-mw/) package. Before installation, import the (continuous build) keys from [[1]](https://files.eid.belgium.be/). See [makepkg#Signature checking](/index.php/Makepkg#Signature_checking "Makepkg").

There is no plugin for Chrome, but there is one for Firefox. Add the [Firefox plugin](https://addons.mozilla.org/nl/firefox/addon/belgium-eid) to your browser. In recent versions, you'll need to manually [add the eID module](https://eid.belgium.be/en/log-eid#7507) to the Firefox security devices configuration. Your module path might be different than the one in the guide. List the different devices by doing:

```
# p11tool --list-tokens

```

Here you'll see the module, which might be beidpkcs11.so. Now to find the full path you do:

```
# find /usr/lib -name beidpkcs11.so

```

You should now be able to use your eID reader in Firefox. Try it out using the [test page](https://iamapps.belgium.be/tma/?lang=en).

You may find hints for troubleshooting in the [official documentation](http://faq.eid.belgium.be/nl/index.html) but keep in mind that Arch Linux is not officially supported.

### Estonia

See [https://www.id.ee/?lang=en](https://www.id.ee/?lang=en)

#### DigiDoc

Once [ccid](https://www.archlinux.org/packages/?name=ccid) is installed and `pcscd.socket` is [started](/index.php/Start "Start"), install [qdigidoc4](https://aur.archlinux.org/packages/qdigidoc4/). One of the dependency [xml-security-c](https://aur.archlinux.org/packages/xml-security-c/) is [verified with a signature](/index.php/Makepkg#Signature_checking "Makepkg") that you have to import to your GnuPG keyring.

DigiDoc4 has an optional [GNOME/Files](/index.php/GNOME/Files "GNOME/Files") right click menu integration. Install [python2-nautilus](https://aur.archlinux.org/packages/python2-nautilus/) and restart Gnome Files using the command `pkill nautilus`.

**Note:** [chrome-token-signing](https://aur.archlinux.org/packages/chrome-token-signing/) contains the "Token signing" extension that allows digital signatures on the web for both Google Chrome/Chromium and Firefox.

#### Chromium

After installing [chrome-token-signing](https://aur.archlinux.org/packages/chrome-token-signing/), enable the PIN 1 authentication in [Google Chrome](/index.php/Google_Chrome "Google Chrome") and [Chromium](/index.php/Chromium "Chromium") by running the following command (taken from the [open-eid repo](https://github.com/open-eid/linux-installer/blob/master/esteid-update-nssdb)).

```
 modutil -dbdir sql:$HOME/.pki/nssdb -add opensc-pkcs11 -libfile onepin-opensc-pkcs11.so -mechanisms FRIENDLY

```

#### Firefox

To enable PIN 1 authentication in [Firefox](/index.php/Firefox "Firefox") you should install [esteidpkcs11loader](https://aur.archlinux.org/packages/esteidpkcs11loader/) and [chrome-token-signing](https://aur.archlinux.org/packages/chrome-token-signing/). After restarting the browser make sure that "Firefox PKCS11 loader" extension is enabled. You can also follow manual instructions at [Smartcards#Mozilla Firefox](/index.php/Smartcards#Mozilla_Firefox "Smartcards").

For [firefox-esr52](https://aur.archlinux.org/packages/firefox-esr52/) and other other Firefox forks you can use [esteidfirefoxplugin](https://aur.archlinux.org/packages/esteidfirefoxplugin/).

#### For new cards issued since December 2018

The [opensc-git](https://aur.archlinux.org/packages/opensc-git/) package provides drivers for EstEID 2018+ [[2]](https://github.com/OpenSC/OpenSC/pull/1635).

**Note:** qdigidoc4 requires opensc but you need to remove it before installing opensc-git. To work around this, just force remove opensc with `pacman -Rdd opensc`.

Currently the default pkcs11 provider for Chrome is unsuitable (it asks PIN2 on authentication) (see [[3]](https://github.com/OpenSC/OpenSC/issues/1818)). Fix it by

1.  deleting `~/.pki/nssdb/pkcs11.txt`
2.  running `/usr/bin/pkcs11-register -m /usr/lib/onepin-opensc-pkcs11.so`
3.  and appending `-m /usr/lib/onepin-opensc-pkcs11.so` to the `Exec` line of `/etc/xdg/autostart/pkcs11-register.desktop`.

### Germany

#### ReinerSCT devices

Install [pcsc-cyberjack](https://aur.archlinux.org/packages/pcsc-cyberjack/) and copy the default configuration file `/etc/pcsc-cyberjack/cyberjack.conf.default` to the same folder, without default. Restart `pcsc.service` and apps like [ausweisapp2](https://aur.archlinux.org/packages/ausweisapp2/) should recognize the scanner. The ReinerSCT RFID will blink its LED, which it does not when the driver is not installed correctly.

### Sweden

[BankID](https://www.bankid.com/en/om-bankid/detta-ar-bankid) is the leading electronic identification in Sweden.