# Belgian eID card reader

[![Tango-go-next.png](/images/f/f0/Tango-go-next.png)](/index.php/File:Tango-go-next.png)

[![Tango-go-next.png](/images/f/f0/Tango-go-next.png)](/index.php/File:Tango-go-next.png)

**This article or section is a candidate for moving to [eID card](/index.php?title=EID_card&action=edit&redlink=1 "EID card (page does not exist)").**

**Notes:** Shared instructions amongst different eID cards (card readers, pcsc), different mostly in middleware and browser plugins. Merge with [Estonian ID-card](/index.php/Estonian_ID-card "Estonian ID-card"). (Discuss in [Talk:Belgian eID card reader#](https://wiki.archlinux.org/index.php/Talk:Belgian_eID_card_reader))

[Belgian eID](http://eid.belgium.be/en%7C) card reader allow you to read your identity card.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Import public keys](#Import_public_keys)
*   [2 Usage](#Usage)
    *   [2.1 Firefox](#Firefox)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Card reader stopped working during session](#Card_reader_stopped_working_during_session)

## Installation

Install the [eid-mw](https://aur.archlinux.org/packages/eid-mw/)<sup><small>AUR</small></sup> package. [eid-viewer](https://aur.archlinux.org/packages/eid-viewer/)<sup><small>AUR</small></sup> is useful to verify a functional setup, before trying to read an eid from within a browser.

As a driver for the card reader hardware is required, install the [ccid](https://www.archlinux.org/packages/?name=ccid) package. In some cases, [acsccid](https://aur.archlinux.org/packages/acsccid/)<sup><small>AUR</small></sup> is needed instead.

After installing the right driver, [start](/index.php/Start "Start") and enable the `pcscd` service.

### Import public keys

[![Tango-user-trash-full.png](/images/e/ee/Tango-user-trash-full.png)](/index.php/File:Tango-user-trash-full.png)

[![Tango-user-trash-full.png](/images/e/ee/Tango-user-trash-full.png)](/index.php/File:Tango-user-trash-full.png)

**This article or section is being considered for deletion.**

**Reason:** Duplicates [makepkg#Signature checking](/index.php/Makepkg#Signature_checking "Makepkg") (Discuss in [Talk:Belgian eID card reader#](https://wiki.archlinux.org/index.php/Talk:Belgian_eID_card_reader))

To install [eid-mw](https://aur.archlinux.org/packages/eid-mw/)<sup><small>AUR</small></sup>, you will need to import the public keys listed [here](http://files.eid.belgium.be/%7C), i.e. each (or at least the continuous build key) of the `*.asc` files, like so:

 `# gpg --import *.asc ` 

## Usage

If you have installed eid-viewer, you can open it and (with card reader and your eID plugged in) should be able to see your eID's contents in eid-viewer.

### Firefox

There is no plugin for Chrome, but there is one for Firefox. Add the [Firefox plugin](https://addons.mozilla.org/nl/firefox/addon/belgium-eid/%7C) to your browser. You should now be able to use your eID reader in Firefox. Try it out using the [test page](http://test.eid.belgium.be/%7C)

## Troubleshooting

You may find hints for troubleshooting in the [official documentation (Dutch)](http://faq.eid.belgium.be/nl/index.html%7C) but note that Arch Linux is not officially supported.

### Card reader stopped working during session

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

**This article or section needs language, wiki syntax or style improvements.**

**Reason:** "Hello, IT, have you tried turning it off and on again" (Discuss in [Talk:Belgian eID card reader#](https://wiki.archlinux.org/index.php/Talk:Belgian_eID_card_reader))

`pcscd` may have crashed (check with `systemctl status pcscd`, restart it:

 `# systemctl restart pcscd` 

Retrieved from "[https://wiki.archlinux.org/index.php?title=Belgian_eID_card_reader&oldid=411837](https://wiki.archlinux.org/index.php?title=Belgian_eID_card_reader&oldid=411837)"