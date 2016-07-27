# Core Signoffs

This policy is intended to ensure the [core] repository, and thus the core of Arch Linux, is as functional as possible at all times. Packages can be tested by developers, Trusted Users and testers which all have access to archweb.

Testing a package can range from a simple "does it start/run?" test to more complex ones. Normally checking if the software still works for some simple example (for example, "does the new linux kernel still boot" or "does perl still run some perl script I have?") is sufficient. The main goal is to catch very badly broken packages before they can hit a large number of users.

### Process

The process is simple:

*   All [core] packages **MUST** go to [testing] first.
*   Archweb automatically picks up the new package and allows developers and testers to signoff on [this page](https://www.archlinux.org/packages/signoffs/).
*   If a package works fine, the tester should signoff via archweb.
*   If it does not work, a bug report and/or email to the maintainer should be created/sent ASAP.
*   When a package receives 2 signoffs for each architecture, it can be moved from [testing] to [core].
*   A maintainer is free to leave a package in [testing] for further testing or signoffs.

### Caveats

The maintainer himself *DOES* count as a signoff. We are working under the assumption that the maintainer did test the package before pushing it to [testing]. Thus, a package may only need one signoff if the original maintainer tested it on both architectures before uploading.