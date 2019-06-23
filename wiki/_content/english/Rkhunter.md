Related articles

*   [Security](/index.php/Security "Security")
*   [List of applications/Security](/index.php/List_of_applications/Security "List of applications/Security")
*   [AIDE](/index.php/AIDE "AIDE")

**rkhunter** (Rootkit Hunter) is a security monitoring tool for POSIX compliant systems. It scans for rootkits, and other possible vulnerabilities. It does so by searching for the default directories (of rootkits), misconfigured permissions, hidden files, kernel modules containing suspicious strings, and comparing hashes of important files with known good ones.

It is written in [Bash](/index.php/Bash "Bash"), to allow for portability, and can run on most UNIX-based systems.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Initial setup](#Initial_setup)
    *   [2.2 Important files](#Important_files)
*   [3 Usage](#Usage)
    *   [3.1 Basic commands](#Basic_commands)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 False positives](#False_positives)
*   [5 See also](#See_also)
    *   [5.1 External documentation](#External_documentation)
    *   [5.2 Related Wikipedia pages](#Related_Wikipedia_pages)

## Installation

[Install](/index.php/Install "Install") the [rkhunter](https://www.archlinux.org/packages/?name=rkhunter) package.

## Configuration

### Initial setup

Prior to running rkhunter for the first time, update the *file properties database*:

```
# rkhunter --propupd

```

### Important files

The main configuration file is located at `/etc/rkhunter.conf`.

By default, a log of the last system check will be placed at `/var/log/rkhunter.log`.

## Usage

See [rkhunter(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/rkhunter.8) for full details.

### Basic commands

To update the file properties database:

```
# rkhunter --propupd

```

To run a system check:

```
# rkhunter --check

```

To validate the configuration file(s):

```
# rkhunter --config-check

```

## Troubleshooting

### False positives

Out of the box, Rootkit Hunter will throw up some false warnings during the file properties check. This is because, a few of the core utilities have been replaced by scripts. These warnings can be muted through white-listing.

 `/etc/rkhunter.conf` 
```
SCRIPTWHITELIST=/usr/bin/egrep
SCRIPTWHITELIST=/usr/bin/fgrep
SCRIPTWHITELIST=/usr/bin/ldd
```

## See also

### External documentation

*   [Rootkit Hunter Homepage](http://rkhunter.sourceforge.net/)
*   [Rootkit Hunter README](https://sourceforge.net/p/rkhunter/rkh_code/ci/master/tree/files/README)

### Related Wikipedia pages

*   [rkhunter](https://en.wikipedia.org/wiki/rkhunter "wikipedia:rkhunter")
*   [Host-based intrusion detection system (HIDS)](https://en.wikipedia.org/wiki/Host-based_intrusion_detection_system "wikipedia:Host-based intrusion detection system")
*   [Intrusion detection system (IDS)](https://en.wikipedia.org/wiki/Intrusion_detection_system "wikipedia:Intrusion detection system")