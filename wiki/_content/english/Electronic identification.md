Related articles

*   [Common Access Card](/index.php/Common_Access_Card "Common Access Card")
*   [Smartcards](/index.php/Smartcards "Smartcards")

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

There is no plugin for Chrome, but there is one for Firefox. Add the [Firefox plugin](https://addons.mozilla.org/nl/firefox/addon/belgium-eid) to your browser. In recent versions, you'll need to manually [add the eID module](https://eid.belgium.be/nl/aanmelden-met-eid#7504) to the Firefox security devices configuration. Your module path might be different than the one in the guide. List the different devices by doing:

```
# p11tool --list-tokens

```

Here you'll see the module, which might be beidpkcs11.so. Now to find the full path you do:

```
# find /usr/lib --name beidpkcs11.so

```

You should now be able to use your eID reader in Firefox. Try it out using the [test page](http://test.eid.belgium.be)

You may find hints for troubleshooting in the [official documentation (Dutch)](http://faq.eid.belgium.be/nl/index.html) but note that Arch Linux is not officially supported.

### Estonia

[https://www.id.ee/?lang=en](https://www.id.ee/?lang=en)

Install the [chrome-token-signing](https://aur.archlinux.org/packages/chrome-token-signing/), [qdigidoc](https://aur.archlinux.org/packages/qdigidoc/) and [qesteidutil](https://aur.archlinux.org/packages/qesteidutil/) packages, with dependencies [libdigidoc](https://aur.archlinux.org/packages/libdigidoc/) and [libdigidocpp](https://aur.archlinux.org/packages/libdigidocpp/). These applications will automatically appear in your application menus. You can also start from command line with <tt>qdigidocclient</tt> and <tt>qesteidutil</tt>.

[chrome-token-signing](https://aur.archlinux.org/packages/chrome-token-signing/) contains [Native Messaging](https://developer.mozilla.org/en-US/Add-ons/WebExtensions/Native_messaging) host for Google Chrome/Chromium and Firefox and it is the modern way of doing authentication and digital signatures on the web.

For Google Chrome and Chromium you also will probably want to run [esteid-update-nssdb](https://github.com/open-eid/linux-installer/blob/master/esteid-update-nssdb) script that enables TLS client authentication in the browser.

Some recent versions of [Firefox](/index.php/Firefox "Firefox") seem to have problems recognizing opensc, see [Smartcards#Mozilla Firefox](/index.php/Smartcards#Mozilla_Firefox "Smartcards"). If you still cannot login from [Firefox](/index.php/Firefox "Firefox") with your ID-card you should install [esteidfirefoxplugin](https://aur.archlinux.org/packages/esteidfirefoxplugin/).

If you updated your certificates due to [https://www.id.ee/?lang=en&id=38241](https://www.id.ee/?lang=en&id=38241), then for signing you need to use a patched version of opensc (see [https://github.com/OpenSC/OpenSC/issues/1176](https://github.com/OpenSC/OpenSC/issues/1176)). Consider [opensc-esteid](https://aur.archlinux.org/packages/opensc-esteid/).

### Sweden

[BankID](https://www.bankid.com/en/om-bankid/detta-ar-bankid) is the leading electronic identification in Sweden.