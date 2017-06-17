[Belgian eID](https://eid.belgium.be/en) card reader allow you to read your identity card.

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 Firefox](#Firefox)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Card reader stopped working during session](#Card_reader_stopped_working_during_session)

## Installation

Install the [eid-mw](https://aur.archlinux.org/packages/eid-mw/) package. [eid-viewer](https://aur.archlinux.org/packages/eid-viewer/) is useful to verify a functional setup, before trying to read an eid from within a browser. Before installation, import the (continuous build) keys from [[1]](https://files.eid.belgium.be/). See [makepkg#Signature checking](/index.php/Makepkg#Signature_checking "Makepkg").

As a driver for the card reader hardware is required, install the [ccid](https://www.archlinux.org/packages/?name=ccid) package. In some cases, [acsccid](https://aur.archlinux.org/packages/acsccid/) is needed instead.

After installing the right driver, [start](/index.php/Start "Start") and enable the `pcscd` service.

## Usage

If you have installed eid-viewer, you can open it and (with card reader and your eID plugged in) should be able to see your eID's contents in eid-viewer.

### Firefox

There is no plugin for Chrome, but there is one for Firefox. Add the [Firefox plugin](https://addons.mozilla.org/nl/firefox/addon/belgium-eid) to your browser. You should now be able to use your eID reader in Firefox. Try it out using the [test page](http://test.eid.belgium.be)

## Troubleshooting

You may find hints for troubleshooting in the [official documentation (Dutch)](http://faq.eid.belgium.be/nl/index.html) but note that Arch Linux is not officially supported.

### Card reader stopped working during session

`pcscd` may have crashed (check with `systemctl status pcscd`, restart it:

 `# systemctl restart pcscd`