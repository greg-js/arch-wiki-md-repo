[BankID](https://www.bankid.com/en/om-bankid/detta-ar-bankid) is the leading electronic identification in Sweden. The desktop client is proprietary and only available for Windows and OS X. [[1]](https://install.bankid.com/) The underlying application is [Nexus Personal](https://www.nexusgroup.com/software/nexus-personal-desktop/).

There once was an AUR package but it no longer works. [[2]](https://github.com/felixonmars/aur3-mirror/blob/master/nexuspersonal/PKGBUILD)

The free implementation of BankID [FriBID](https://fribid.se/index.en.html) also no longer works with the current version of BankID.

## Running BankID in a virtual Windows machine

Install [VirtualBox](/index.php/VirtualBox "VirtualBox"), download a Windows ISO, setup the machine and install BankID. If you want to use a card-reader you have to add your user to the group `vboxusers` to be able to access the usb-connected card-reader. You can then add a usb-filter in the Virtualbox settings for the machine, so that the machine recognizes the card-reader automatically.