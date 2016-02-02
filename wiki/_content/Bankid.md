# Bankid

This page is about the digital id software [Bankid](http://www.bankid.com/en/What-is-BankID/) or **BankID**. The underlaying application of Bankid is Nexus Personal ([http://www.nexusgroup.com](http://www.nexusgroup.com/en/solutions/Identity-Federation/nexus-personal-security-client/)), so the tips here is probably helpful for anyone trying to run other versions of Nexus Personal as well.

## Installation

Install the [nexuspersonal](https://aur.archlinux.org/packages/nexuspersonal/) package from the [AUR](/index.php/AUR "AUR").

## Open source alternatives

The open source program Fribid is available in the [AUR](/index.php/AUR "AUR"): [fribid](https://aur.archlinux.org/packages/fribid/).

## Running Bankid in a virtual machine running Windows

If no other solution works, you can always install for example [VirtualBox](/index.php/VirtualBox "VirtualBox") and run Bankid on a Windows virtual machine. It should work fairly out of the box with Windows XP on the guest. If you want to use a card-reader you have to add the user that runs Virtualbox (usually you) to the group `vboxusers` to be able to access the usb-connected card-reader. You can then add a usb-filter in the Virtualbox settings for the machine, so that the machine captures the card-reader automatically.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Bankid&oldid=391954](https://wiki.archlinux.org/index.php?title=Bankid&oldid=391954)"