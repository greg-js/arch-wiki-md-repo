**OSH** (Oil Shell) is a Bash-compatible UNIX [command-line shell](/index.php/Command-line_shell "Command-line shell"). OSH can be run on most UNIX-like operating systems, including GNU/Linux. It is written in Python (v2.7), but ships with a native executable. The dialect of Bash recognized by OSH is called the OSH language.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Smoke Test](#Smoke_Test)
    *   [1.2 Making OSH your default shell](#Making_OSH_your_default_shell)
*   [2 Uninstallation](#Uninstallation)

## Installation

[Install](/index.php/Install "Install") the [osh](https://aur.archlinux.org/packages/osh/) package.

### Smoke Test

Make sure that OSH has been installed correctly by running the following in a terminal:

```
$> osh

```

This will start an OSH session and change the shell prompt to:

```
osh$

```

Identify an installed binary and attempt to invoke it in the OSH session to confirm that the output is correct.

For example:

```
osh$ ls
...

```

### Making OSH your default shell

See [Command-line shell#Changing your default shell](/index.php/Command-line_shell#Changing_your_default_shell "Command-line shell").

## Uninstallation

Change the default shell before removing the [osh](https://aur.archlinux.org/packages/osh/) package.

**Warning:** Failure to follow the below procedure may result in users no longer having access to a working shell.

Run following command:

```
$ chsh -s /bin/bash *user*

```

Use it for every user with *osh* set as their login shell (including root if needed). When completed, the [osh](https://aur.archlinux.org/packages/osh/) package can be removed.

Alternatively, change the default shell back to Bash by editing `/etc/passwd` as root.

**Warning:** It is strongly recommended to use `vipw` when editing `/etc/passwd` as it helps prevent invalid entries and/or syntax errors.

For example, change the following:

```
*username*:x:1000:1000:*Full Name*,,,:/home/*username*:/bin/osh

```

To this:

```
*username*:x:1000:1000:*Full Name*,,,:/home/*username*:/bin/bash

```