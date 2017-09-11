AIDE is a host-based intrusion detection system (HIDS) for checking the integrity of files. It does this by creating a baseline database of files on an initial run, and then checks this database against the system on subsequent runs. File properties that can be checked against include inode, permissions, modification time, file contents, etc.

AIDE only does file integrity checks. It does not check for rootkits or parse logfiles for suspicious activity, like some other [HIDS](/index.php/List_of_applications/Security#Threat_and_vulnerability_detection "List of applications/Security") (such as OSSEC) do. For these features, you can use an additional HIDS ([see here](http://www.la-samhna.de/library/scanners.html) for a possibly biased comparison), or use standalone rootkit scanners (rkhunter, chkrootkit) and log monitoring solutions ([logwatch](/index.php/Logwatch "Logwatch"), logcheck).

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Usage](#Usage)
    *   [3.1 Cron](#Cron)
    *   [3.2 Security](#Security)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [aide](https://www.archlinux.org/packages/?name=aide) package.

## Configuration

The default config file at `/etc/aide.conf` has pretty sane defaults and is heavily commented. If you want to change the rules, see `man aide.conf` and the [AIDE Manual](http://aide.sourceforge.net/stable/manual.html) for documentation.

## Usage

To check your configuration, use `aide -D`.

To initialize the database, use `aide -i` or `aideinit`. Depending on your configuration and system, this command can take a while to complete.

You can check the system against the baseline database using `aide -C`, or update the baseline db using `aide -u`.

For more info, see [aide(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/aide.1).

### Cron

AIDE can be run manually if desired, but you may want to run it automatically instead. How you set this up will depend on your [cron](/index.php/Cron "Cron") daemon and MUA (if email notification is desired).

If cron is set up to automatically mail all job output, it can be as simple as

```
#!/bin/bash -e

# these should be the same as what's defined in /etc/aide.conf
database=/var/lib/aide/aide.db.gz
database_out=/var/lib/aide/aide.db.new.gz

if [ ! -f "$database" ]; then
        echo "$database not found" >&2
        exit 1
fi

aide -u || true

mv $database $database.back
mv $database_out $database

```

For examples of more complicated cron scripts see [here](https://sources.gentoo.org/cgi-bin/viewvc.cgi/gentoo-x86/app-forensics/aide/files/aide.cron) or [here](https://rfxn.com/downloads/cron.aide).

### Security

Since the database is stored on the root filesystem, attackers can easily modify it to cover their tracks if they compromise your system. You may want to copy the database to offline, read-only media and perform checks against this copy periodically.

## See also

*   [AIDE manual](http://aide.sourceforge.net/stable/manual.html)
*   [Gentoo Docs - Intrusion detection](https://wiki.gentoo.org/wiki/Security_Handbook?part=1&chap=13#doc_chap1)
*   [Samhain Labs - file integrity checkers](http://www.la-samhna.de/library/scanners.html)