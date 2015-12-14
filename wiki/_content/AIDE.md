# AIDE

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

AIDE is a host-based intrusion detection system (HIDS) for checking the integrity of files. It does this by creating a baseline database of files on an initial run, and then checks this database against the system on subsequent runs. File properties that can be checked against include inode, permissions, modification time, file contents, etc.

AIDE only does file integrity checks. It does not check for rootkits or parse logfiles for suspicious activity, like some other HIDS (such as OSSEC) do. For these features, you can use an additional HIDS ([see here](http://www.la-samhna.de/library/scanners.html) for a possibly biased comparison), or use standalone rootkit scanners (rkhunter, chkrootkit) and log monitoring solutions ([logwatch](/index.php/Logwatch "Logwatch"), logcheck).

## Contents

*   [1 Setup](#Setup)
    *   [1.1 Installation](#Installation)
    *   [1.2 Configuration](#Configuration)
    *   [1.3 Usage](#Usage)
    *   [1.4 Cron](#Cron)
    *   [1.5 Security](#Security)
*   [2 See also](#See_also)

## Setup

### Installation

[Install](/index.php/Install "Install") [aide](https://www.archlinux.org/packages/?name=aide) from the [official repositories](/index.php/Official_repositories "Official repositories").

### Configuration

The default config file at `/etc/aide.conf` has pretty sane defaults and is heavily commented. If you want to change the rules, see `man aide.conf` and the [AIDE Manual](http://aide.sourceforge.net/stable/manual.html) for documentation.

### Usage

To check your configuration, use `aide -D`.

To initialize the database, use `aide -i` or `aideinit`. Depending on your configuration and system, this command can take a while to complete.

You can check the system against the baseline database using `aide -C`, or update the baseline db using `aide -u`.

For more info, see `man aide`.

### Cron

AIDE can be run manually if desired, but you may want to run it automatically instead. How you set this up will depend on your cron daemon and MUA (if email notification is desired).

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

For examples of more complicated cron scripts see [here](http://sources.gentoo.org/cgi-bin/viewvc.cgi/gentoo-x86/app-forensics/aide/files/aide.cron) or [here](http://rfxn.com/downloads/cron.aide).

### Security

Since the database is stored on the root filesystem, attackers can easily modify it to cover their tracks if they compromise your system. You may want to copy the database to offline, read-only media and perform checks against this copy periodically.

## See also

*   [AIDE manual](http://aide.sourceforge.net/stable/manual.html)
*   [Gentoo Docs - Intrusion detection](http://www.gentoo.org/doc/en/security/security-handbook.xml?part=1&chap=13#doc_chap1)
*   [Samhain Labs - file integrity checkers](http://www.la-samhna.de/library/scanners.html)

Retrieved from "[https://wiki.archlinux.org/index.php?title=AIDE&oldid=412026](https://wiki.archlinux.org/index.php?title=AIDE&oldid=412026)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Security](/index.php/Category:Security "Category:Security")