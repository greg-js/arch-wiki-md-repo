## Contents

*   [1 Core signoffs](#Core_signoffs)
    *   [1.1 Process](#Process)
    *   [1.2 Caveats](#Caveats)
*   [2 Extra signoffs](#Extra_signoffs)
    *   [2.1 Process](#Process_2)
    *   [2.2 Caveats](#Caveats_2)
*   [3 Patching](#Patching)
    *   [3.1 Vanilla Packages](#Vanilla_Packages)
    *   [3.2 When is patching acceptable?](#When_is_patching_acceptable.3F)
    *   [3.3 When is patching discouraged?](#When_is_patching_discouraged.3F)
*   [4 Adding packages to extra](#Adding_packages_to_extra)
    *   [4.1 Ask First](#Ask_First)
*   [5 Bash coding style](#Bash_coding_style)

## Core signoffs

This policy is intended to ensure the [core](/index.php/Core "Core") repository, and thus the core of Arch Linux, is as functional as possible at all times. Packages can be tested by developers, Trusted Users and testers which all have access to archweb.

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

## Extra signoffs

### Process

The process is simple:

*   If you need to test a package from the [extra] repository, you can add it to [testing]
*   When a [extra] package is placed in [testing] an email **SHOULD** be sent to the arch-dev-public mailing list with the subject "[signoff] [extra] foobar-1.0-1", where *foobar-1.0-1* is the package name and version.
*   In the email the maintainer has to say the reasons why that package went to [testing]
*   All developers are encouraged to test this package.
*   If a package works fine, a reply **SHOULD** be sent, telling the maintainer it worked, and on which architecture.
*   When a package receives 2 signoffs for each architecture, it can be moved from [testing] to [extra].
*   A maintainer is free to leave a package in [testing] for further testing or signoffs, but should make this intention known in the signoff email.

### Caveats

The maintainer himself *DOES* count as a signoff. We are working under the assumption that the maintainer did test the package before pushing it to [testing]. Thus, a package may only need one signoff if the original maintainer tested it on both architectures before uploading.

## Patching

This policy is intended to *suggest*, not to enforce.

### Vanilla Packages

Arch tries, as much as possible, to ship packages as the original author of the software intended. This means that every time we add a patch, we take one more step away from their intent. Additionally, patches can be hard to maintain when we're talking hundreds of packages.

### When is patching acceptable?

It's inevitable that some software will need modifications to work.

*   Patches to the *build system* are pretty much always allowed. This is usually needed when Arch's tools are too new for shipped scripts, and things do not work right (libtool is a known offender here).

*   Patches due to a *too new* compiler are usually allowed. GCC releases tend to be more and more strict, disallowing things that were once allowed. Fixing compiler errors so that the source builds under Arch are common and allowable.

*   When a *major feature* doesn't work in the app, bug fix patches are allowed. To explain 'major feature', think of an app that burns DVDs - if it doesn't burn DVDs due to a bug, well, that's a major feature. If the 'Help' menu doesn't work, well, that's a minor feature.

### When is patching discouraged?

*   Fixing minor features is not our job and patches should not be applied to fix things not directly related to the app's functionality. Patches to fix typos or images are discouraged.

*   Additional features should *NOT* be added by Arch. Patches that add completely new features should be sent to upstream. As said before - we ship packages as the ORIGINAL AUTHORS intended them. Not as WE intend them.

*   Features denied by upstream. If a patch was sent and the original developers denied it, we should *NEVER* apply that patch, no matter how opinionated we are. You are welcome to fork the app and supply a package for your own app.

## Adding packages to extra

Because we have limited man power, and limited mirror space, it is important that we keep the packages in the [extra] repository under control. Packages can always go into community as opposed to extra.

### Ask First

The policy here is very simple. Ask the other devs.

*   Send a short mail to the arch-dev-public list with your intent to add a new package to [extra]
*   Wait for a few replies to see if anyone takes issue with it. Generally, it's probably good to wait a few hours, as timezones differ between the team quite a bit.
*   Assuming no one takes issue with the package, add it to extra.

## Bash coding style

*   encoding is utf-8
*   use `#!/bin/bash`
*   indent with tabs
*   tabs have 8 characters
*   do not use more than 132 columns
*   opening braces are top right, closing are bottom left:

```
foo() {
        echo bar
}

```

*   `if` and `for` statements are like this:

```
if true; then
        do something
else
        do something else
fi

```

```
for i in a b c; do
        echo $i
done

```

*   use single quotes if a string does not contain parseable content
*   use `source` instead of `.`
*   use `$()` instead of ````