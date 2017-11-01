An [electronic identification](https://en.wikipedia.org/wiki/Electronic_identification "w:Electronic identification") ("eID") is an electronic identification solution of citizens or organizations, for example in view to access benefits or services provided by government authorities, banks or other companies. Apart from online authentication many eICs also give users the option to sign electronic documents with a digital signature.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Belgium](#Belgium)
    *   [1.2 Estonia](#Estonia)
    *   [1.3 Sweden](#Sweden)

## Installation

[Install](/index.php/Install "Install") the [ccid](https://www.archlinux.org/packages/?name=ccid) package. [ACS](https://www.acs.com.hk/en/product-lines/2/pc-linked-smart-card-readers/) smart card also require the [acsccid](https://aur.archlinux.org/packages/acsccid/) package. After installation, [enable](/index.php/Enable "Enable") `pcscd.socket`.

### Belgium

[https://eid.belgium.be/en](https://eid.belgium.be/en)

Install the [eid-mw](https://aur.archlinux.org/packages/eid-mw/) package. Before installation, import the (continuous build) keys from [[1]](https://files.eid.belgium.be/). See [makepkg#Signature checking](/index.php/Makepkg#Signature_checking "Makepkg").

There is no plugin for Chrome, but there is one for Firefox. Add the [Firefox plugin](https://addons.mozilla.org/nl/firefox/addon/belgium-eid) to your browser. You should now be able to use your eID reader in Firefox. Try it out using the [test page](http://test.eid.belgium.be)

You may find hints for troubleshooting in the [official documentation (Dutch)](http://faq.eid.belgium.be/nl/index.html) but note that Arch Linux is not officially supported.

### Estonia

Install the [chrome-token-signing](https://aur.archlinux.org/packages/chrome-token-signing/), [qdigidoc](https://aur.archlinux.org/packages/qdigidoc/) and [qesteidutil](https://aur.archlinux.org/packages/qesteidutil/) packages, with dependencies [libdigidoc](https://aur.archlinux.org/packages/libdigidoc/) and [libdigidocpp](https://aur.archlinux.org/packages/libdigidocpp/). These applications will automatically appear in your application menus. You can also start from command line with <tt>qdigidocclient</tt> and <tt>qesteidutil</tt>.

[chrome-token-signing](https://aur.archlinux.org/packages/chrome-token-signing/) contains [Native Messaging](https://developer.mozilla.org/en-US/Add-ons/WebExtensions/Native_messaging) host for Google Chrome/Chromium and Firefox and it is the modern way of doing authentication and digital signatures on the web.

For Google Chrome and Chromium you also will probably want to run [esteid-update-nssdb](https://github.com/open-eid/linux-installer/blob/master/esteid-update-nssdb) script that enables TLS client authentication in the browser.

If you still cannot login from [Firefox](/index.php/Firefox "Firefox") with your ID-card you should install [esteidfirefoxplugin](https://aur.archlinux.org/packages/esteidfirefoxplugin/).

### Sweden

[BankID](https://www.bankid.com/en/om-bankid/detta-ar-bankid) is the leading electronic identification in Sweden. The desktop client is proprietary and only available for Windows and OS X. [[2]](https://install.bankid.com/) The underlying application is [Nexus Personal](https://www.nexusgroup.com/software/nexus-personal-desktop/).

There once was an AUR package but it no longer works, since the `source` isn't available anymore. [[3]](https://github.com/felixonmars/aur3-mirror/blob/master/nexuspersonal/PKGBUILD)

The free implementation of BankID [FriBID](https://fribid.se/index.en.html) also no longer works with the current version of BankID.