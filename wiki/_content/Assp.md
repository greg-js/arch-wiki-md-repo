# Assp

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

**This article or section is out of date.**

**Reason:** rc.conf references (Discuss in [Talk:Assp#](https://wiki.archlinux.org/index.php/Talk:Assp))

The Anti-Spam SMTP Proxy (ASSP) Server project aims to create an open source platform-independent SMTP Proxy server which implements auto-whitelists, self learning Bayesian, Greylisting, DNSBL, DNSWL, URIBL, SPF, SRS, Backscatter, Virus scanning, attachment blocking, Senderbase and multiple other filter methods. This page shows how to install ASSP on a [TrimSlice](http://trimslice.com/web/)

## Contents

*   [1 Features](#Features)
*   [2 Installation](#Installation)
    *   [2.1 Basic](#Basic)
    *   [2.2 Download ASSP](#Download_ASSP)
    *   [2.3 Create necessary directories](#Create_necessary_directories)
    *   [2.4 Install files in place](#Install_files_in_place)
    *   [2.5 CPAN](#CPAN)
*   [3 Configuration](#Configuration)
    *   [3.1 Start script](#Start_script)
*   [4 Start ASSP](#Start_ASSP)
    *   [4.1 Manually](#Manually)
    *   [4.2 Daemon](#Daemon)

## Features

*   Multiple Weighted DNSBLs
*   Multiple Weighted URIBLs
*   Greylisting
*   Weighted Regular Expression Filtering
*   Bayesian
*   Penalty Box
*   SenderBase
*   SSL/TLS
*   SPF/SRS
*   Attachment Blocking
*   ClamAV and FileScan
*   Blocking Reporting
*   LDAP support
*   Backscatter Detection
*   V2 - recipient replacement / GUI user access rights management
*   V2 - MIME charset conversion / DKIM check and signing
*   V2 - DB support for all hashes / level based open plugin support
*   V2 - transparent proxy support / BATV check and signing
*   V2 - Plugins: archive, full attachment check and replacement, OCR
*   V2 - damping (steal spammers time)
*   V2 - AUTH to relay host / POP3 collector
*   V2 - configuration value and file synchronization
*   V2 - Block Reports design could be customized
*   V2 - Razor2 and DCC support via Plugin
*   V2 - SNMP support (monitoring, configuring, controll-API)
*   V2 - user group import (file or LDAP or command based)
*   V2 - automatic crash analyzer Hidden Markov Model
*   V2 - IPv6 socket support
*   V2 - word stemming (several languages) for Bayesian analyzer
*   V2 - Perl module autoupdate via PPM or CPAN
*   V2 - Hidden Markov Model spam detection engine
*   V2 - full unicode support

## Installation

### Basic

Install Perl Modules and there dependencies [perl-mail-spf-query](https://www.archlinux.org/packages/?name=perl-mail-spf-query), [perl-email-mime](https://www.archlinux.org/packages/?name=perl-email-mime), [perl-net-dns](https://www.archlinux.org/packages/?name=perl-net-dns), [perl-email-send](https://www.archlinux.org/packages/?name=perl-email-send), [perl-io-socket-ssl](https://www.archlinux.org/packages/?name=perl-io-socket-ssl), [perl-io-socket-inet6](https://www.archlinux.org/packages/?name=perl-io-socket-inet6), [perl-authen-sasl](https://www.archlinux.org/packages/?name=perl-authen-sasl), [perl-berkeleydb](https://www.archlinux.org/packages/?name=perl-berkeleydb), [perl-net-cidr-lite](https://www.archlinux.org/packages/?name=perl-net-cidr-lite) available in the [Official repositories](/index.php/Official_repositories "Official repositories").

Install [unzip](https://www.archlinux.org/packages/?name=unzip), [net-snmp](https://www.archlinux.org/packages/?name=net-snmp) and [clamav](https://www.archlinux.org/packages/?name=clamav) available in the [Official repositories](/index.php/Official_repositories "Official repositories").

### Download ASSP

[here](http://sourceforge.net/project/showfiles.php?group_id=69172)

### Create necessary directories

```
# mkdir -p /usr/share/assp/{spam,notspam,errors/{spam,notspam}}

```

### Install files in place

```
# cd /usr/share/
# unzip /path/to/ASSP_<version>_<build>_install.zip
# rm *.txt

```

### CPAN

Install Perl Modules via CPAN

```
# perl -MCPAN -e shell
cpan> test File::Scan::ClamAV
cpan> look File::Scan::ClamAV

```

edit `clamav.conf`

```
Foreground **true**
ScanArchive **true**

```

 `[root@trim File-Scan-ClamAV-1.91-VHJd1I]# make install` 

```
Installing /usr/share/perl5/site_perl/File/Scan/ClamAV.pm
Installing /usr/share/man/man3/File::Scan::ClamAV.3pm
Appending installation info to /usr/lib/perl5/core_perl/perllocal.pod

```

 `[root@trim File-Scan-ClamAV-1.91-VHJd1I]# exit` 

```
exit

```

 `cpan> exit` 

```
Terminal does not support GetHistory.
Lockfile removed.

```

```
# perl -MCPAN -e 'install HTML::Entities'
# perl -MCPAN -e 'install Email::Valid'
# perl -MCPAN -e 'install Lingua::Stem::Snowball'
# perl -MCPAN -e 'install Sys::MemInfo'
# perl -MCPAN -e 'install Net::SMTP::TLS'
# perl -MCPAN -e 'install Convert::TNEF'
# perl -MCPAN -e 'install Compress::Zlib'
# perl -MCPAN -e 'install Net::IP::Match::Regexp'
# perl -MCPAN -e 'install Net::SenderBase'
# perl -MCPAN -e 'install Tie::RDBM'
# perl -MCPAN -e 'install Net::Syslog'
# perl -MCPAN -e 'install Time::HiRes'
# perl -MCPAN -e 'install File::ReadBackwards'
# perl -MCPAN -e 'install Email::MIME::Modifier'
# perl -MCPAN -e 'install Mail::SRS'
# perl -MCPAN -e 'install Sys::Syslog'
# perl -MCPAN -e 'install Net::LDAP'
# perl -MCPAN -e 'install Unicode::GCString'
# perl -MCPAN -e 'install Thread::State'
# perl -MCPAN -e 'install Schedule::Cron'

```

## Configuration

### Start script

 `/etc/rc.d/assp` 

```

#!/bin/bash

. /etc/rc.conf
. /etc/rc.d/functions

PATH=/bin:/usr/bin:/sbin:/usr/sbin

case "$1" in

        start)
                stat_busy 'Starting the Anti-Spam SMTP Proxy'
                cd /usr/share/assp
                perl assp.pl 2>&1 > /dev/null &
                if [[ $? -gt 0 ]]; then
                        stat_fail
                else
                        add_daemon assp
                        stat_done
                fi
        ;;

        stop)
                stat_busy 'Stopping the Anti-Spam SMTP Proxy'
                kill -9 `pidof perl assp.pl`
                if [[ $? -gt 0 ]]; then
                        stat_fail
                else
                        rm_daemon assp
                        stat_done
                fi
        ;;

        restart)
                $0 stop || true
                $0 start
        ;;

        *)
                echo "Usage: $0 {start|stop|restart}"
                exit 1
        ;;

esac
exit 0

```

## Start ASSP

### Manually

```
# cd /usr/share/assp/
# perl assp.pl

```

You can access the ASSP web interface via [http://localhost:55555](http://localhost:55555) with username "root" and password "nospam4me".

After successful login at web interface stop the ASSP with `Ctrl+c`. Please check `/usr/share/assp/moduleLoadErrors.txt` for

### Daemon

To start/stop/restart the Daemon manually, please read [Performing daemons actions manually](/index.php/Daemon#Performing_daemon_actions_manually "Daemon"), to start at Boot please read [Starting on Boot](/index.php/Daemon#Starting_on_Boot "Daemon").

Retrieved from "[https://wiki.archlinux.org/index.php?title=Assp&oldid=388071](https://wiki.archlinux.org/index.php?title=Assp&oldid=388071)"