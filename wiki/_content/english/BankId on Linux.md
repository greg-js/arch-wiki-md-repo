Despite being required by a number a state organizations, BankId is based on a proprietary protocol and implementation. This pages summarizes the possibilities to run it on Linux. It complements [the pages in Swedish by the Ubuntu Sweden Team](https://wiki.ubuntu.com/SwedishTeam/Support/E-legitimation).

## Contents

*   [1  Direct execution on Linux](#.C2.A0Direct_execution_on_Linux)
*   [2  Execution in virtual machines](#.C2.A0Execution_in_virtual_machines)
*   [3  Obsolete solutions](#.C2.A0Obsolete_solutions)
*   [4  Impossible solutions](#.C2.A0Impossible_solutions)
*   [5  Support for other platforms](#.C2.A0Support_for_other_platforms)

##  Direct execution on Linux

No solution for the latest version of the protocol.

##  Execution in virtual machines

*   The Windows desktop client works well in a virtual machine (eg VirtualBox). It requires a physical card reader (ask it to your bank), and to redirect the corresponding USB device in the VirtualBox configuration.
*   The mobile client for Android has been reported to work in RemixOS running in a virtual box, but this does not seem to work anymore.

##  Obsolete solutions

*   At some point, one could run the Android client in Chrome using ARC Welder / ARChon
*   There once was an AUR package but it no longer works, since the `source` isn't available anymore. [[1]](https://github.com/felixonmars/aur3-mirror/blob/master/nexuspersonal/PKGBUILD)
*   The free implementation of BankID [FriBID](https://fribid.se/index.en.html) also no longer works with the current version of BankID.

##  Impossible solutions

*   The Windows client does not work in a Wine emulator.
*   Mobilt does not work in a standard Android emulator

##  Support for other platforms

*   mobile client for Android, called Mobilt BankId
*   mobile client for iOS, called Mobilt BankId
*   desktop client for Windows [[2]](https://install.bankid.com/) The underlying application is [Nexus Personal](https://www.nexusgroup.com/software/nexus-personal-desktop/).
*   desktop client for OS X [[3]](https://install.bankid.com/).