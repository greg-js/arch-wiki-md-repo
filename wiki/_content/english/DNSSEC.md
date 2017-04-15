## Contents

*   [1 DNSSEC Packages](#DNSSEC_Packages)
*   [2 Howto enable DNSSEC in specific software](#Howto_enable_DNSSEC_in_specific_software)
    *   [2.1 OpenSSH (fixes only weak point in SSH design)](#OpenSSH_.28fixes_only_weak_point_in_SSH_design.29)
    *   [2.2 Firefox (secure browsing - enhancement of HTTPS)](#Firefox_.28secure_browsing_-_enhancement_of_HTTPS.29)
    *   [2.3 Chromium/~~Google Chrome~~ (secure browsing - enhancement of HTTPS)](#Chromium.2FGoogle_Chrome_.28secure_browsing_-_enhancement_of_HTTPS.29)
    *   [2.4 BIND (serving signed DNS zones)](#BIND_.28serving_signed_DNS_zones.29)
    *   [2.5 Postfix (fight spam and frauds)](#Postfix_.28fight_spam_and_frauds.29)
    *   [2.6 jabberd (fight spam and frauds)](#jabberd_.28fight_spam_and_frauds.29)
    *   [2.7 Thunderbird (secure logins)](#Thunderbird_.28secure_logins.29)
    *   [2.8 lftp (secure downloads and logins)](#lftp_.28secure_downloads_and_logins.29)
    *   [2.9 wget (secure downloads)](#wget_.28secure_downloads.29)
    *   [2.10 proftpd](#proftpd)
    *   [2.11 Sendmail (fight spam and frauds)](#Sendmail_.28fight_spam_and_frauds.29)
    *   [2.12 LibSPF](#LibSPF)
    *   [2.13 ncftp (secure downloads and logins)](#ncftp_.28secure_downloads_and_logins.29)
    *   [2.14 libpurple (pidgin + finch -> secure messaging)](#libpurple_.28pidgin_.2B_finch_-.3E_secure_messaging.29)
*   [3 DNSSEC Hardware](#DNSSEC_Hardware)
*   [4 See Also](#See_Also)

## DNSSEC Packages

*   [dnssec-anchors](https://www.archlinux.org/packages/?name=dnssec-anchors)
    *   essential package contains keys to internet from [IANA](https://www.iana.org/dnssec/) stored in /usr/share/dnssec-trust-anchors/
    *   VERY important!
*   [ldns](https://www.archlinux.org/packages/?name=ldns)
    *   DNS(SEC) library **libldns**
    *   drill tool (like dig with DNSSEC support)
        *   can be used for basic DNSSEC validation. eg.:
            *   Should success *(return 0)*:
                *   **drill -TD nic.cz** *#valid DNSSEC key*
                *   **drill -TD google.com** *#not signed domain*
            *   Should fail *(simulating fraudent DNS records)*:
                *   **drill -TD rhybar.cz**
                *   **drill -TD badsign-a.test.dnssec-tools.org**
            *   to use root-zone trust anchor add option **-k /usr/share/dnssec-trust-anchors/root-anchor.key**
*   [dnssec-tools](https://www.archlinux.org/packages/?name=dnssec-tools) *(package is very experimental and volatile right now)*
    *   [https://www.dnssec-tools.org/](https://www.dnssec-tools.org/)
    *   another good library **libval** which can add DNSSEC support to lots of programs
        *   [https://www.dnssec-tools.org/wiki/index.php/DNSSEC_Applications](https://www.dnssec-tools.org/wiki/index.php/DNSSEC_Applications)
    *   some tools [https://www.dnssec-tools.org/wiki/index.php/DNSSEC-Tools_Components](https://www.dnssec-tools.org/wiki/index.php/DNSSEC-Tools_Components)
        *   [https://www.dnssec-tools.org/wiki/index.php/Applications](https://www.dnssec-tools.org/wiki/index.php/Applications)
    *   **libval-shim** LD_PRELOAD library to enable DNSSEC for lots of DNSSEC unaware programs [http://www.dnssec-tools.org/docs/tool-description/libval_shim.html](http://www.dnssec-tools.org/docs/tool-description/libval_shim.html)
    *   PERL API
*   [sshfp](https://aur.archlinux.org/packages/sshfp/)
    *   Generates DNS SSHFP-type records from SSH public keys from public keys from a known_hosts file or from scanning the host's sshd daemon.
    *   not directly related to DNSSEC, but i guess this will become very popular because of DNSSEC
*   [opendnssec](https://aur.archlinux.org/packages/opendnssec/)
    *   Signs DNS zones to be later published by a DNS server (bind, nsd, etc.)
    *   Automates refreshing signatures, key rollovers

## Howto enable DNSSEC in specific software

If you want full support of DNSSEC, you need each single application to use DNSSEC validation. It can be done using several ways:

*   patches
    *   [https://www.dnssec-tools.org/wiki/index.php/DNSSEC_Applications](https://www.dnssec-tools.org/wiki/index.php/DNSSEC_Applications)
    *   [https://www.dnssec-tools.org/wiki/index.php/DNSSEC_Application_Development](https://www.dnssec-tools.org/wiki/index.php/DNSSEC_Application_Development)
*   plugins, extensions, wrappers
*   universal LD_PRELOAD wrapper
    *   overriding calls to: gethostbyname(3), gethostbyaddr(3), getnameinfo(3), getaddrinfo(3), res_query(3)
    *   libval-shim from dnssec-tools: [http://www.dnssec-tools.org/docs/tool-description/libval_shim.html](http://www.dnssec-tools.org/docs/tool-description/libval_shim.html)
*   DNS proxy

### [OpenSSH](/index.php/OpenSSH "OpenSSH") (fixes only weak point in SSH design)

*   dnssec-tools + patch: [https://www.dnssec-tools.org/wiki/index.php/Ssh](https://www.dnssec-tools.org/wiki/index.php/Ssh)
    *   [http://www.dnssec-tools.org/readme/README.ssh](http://www.dnssec-tools.org/readme/README.ssh)

### [Firefox](/index.php/Firefox "Firefox") (secure browsing - enhancement of HTTPS)

*   DNSSEC Validator plugin [https://addons.mozilla.org/en-US/firefox/addon/64247/](https://addons.mozilla.org/en-US/firefox/addon/64247/)
*   DNSSEC Drill plugin [http://nlnetlabs.nl/projects/drill/drill_extension.html](http://nlnetlabs.nl/projects/drill/drill_extension.html)
    *   you need ldns and dnssec-root-zone-trust-anchors packages for this plugin
*   dnssec-tools + firefox patch: [https://www.dnssec-tools.org/wiki/index.php/Firefox](https://www.dnssec-tools.org/wiki/index.php/Firefox)

### [Chromium](/index.php/Chromium "Chromium")/~~Google Chrome~~ (secure browsing - enhancement of HTTPS)

*   Vote for [#50874](http://code.google.com/p/chromium/issues/detail?id=50874)
    *   Patches not yet...
    *   [DNSSEC Drill extension](http://chromium.googlecode.com/issues/attachment?aid=-8803347052009476090&name=chromium-drill-dnssec-validator.zip&token=6e3489c4e5c62bfaae02516be442d7da) (EXPERIMENTAL!)
        *   you need ldns and dnssec-root-zone-trust-anchors packages for this plugin

### BIND (serving signed DNS zones)

*   See [BIND](/index.php/BIND "BIND") for more information on BIND
*   [http://www.dnssec.net/practical-documents](http://www.dnssec.net/practical-documents)
    *   [http://www.cymru.com/Documents/secure-bind-template.html](http://www.cymru.com/Documents/secure-bind-template.html) **(configuration template!)**
    *   [http://www.bind9.net/manuals](http://www.bind9.net/manuals)
    *   [http://www.bind9.net/BIND-FAQ](http://www.bind9.net/BIND-FAQ)
*   [http://blog.techscrawl.com/2009/01/13/enabling-dnssec-on-bind/](http://blog.techscrawl.com/2009/01/13/enabling-dnssec-on-bind/)
*   Or use an external mechanisms such as OpenDNSSEC (fully-automatic key rollover)

### [Postfix](/index.php/Postfix "Postfix") (fight spam and frauds)

*   dnssec-tools + patch

### jabberd (fight spam and frauds)

*   dnssec-tools + patch

### [Thunderbird](/index.php/Thunderbird "Thunderbird") (secure logins)

*   dnssec-tools + patch

### lftp (secure downloads and logins)

*   dnssec-tools + patch

### [wget](/index.php/Wget "Wget") (secure downloads)

*   dnssec-tools + patch

### [proftpd](/index.php/Proftpd "Proftpd")

*   dnssec-tools + patch

### [Sendmail](/index.php/Sendmail "Sendmail") (fight spam and frauds)

*   dnssec-tools + patch

### LibSPF

*   dnssec-tools + patch

### ncftp (secure downloads and logins)

*   dnssec-tools + patch

### libpurple ([pidgin](/index.php/Pidgin "Pidgin") + finch -> secure messaging)

*   no patches yet

*   Vote for [#12413](http://developer.pidgin.im/ticket/12413)

## DNSSEC Hardware

You can check if your router, modem, AP, etc. supports DNSSEC (many different features) using [dnssec-tester](http://www.dnssec-tester.cz/) (Python and GTK+ based app) to know if it is DNSSEC-compatible, and using this tool you can also upload gathered data to a server, so other users and manufacturers can be informed about compatibility of their devices and eventualy fix the firmware (they will be probably urged to do so). (Before running dnssec-tester please make sure, that you do not have any other nameservers in `/etc/resolv.conf`). You can also find the results of performed tests on the [dnssec-tester](http://www.dnssec-tester.cz/) website.

## See Also

*   [AppArmor](/index.php/AppArmor "AppArmor")
*   [Wikipedia:Domain Name System Security Extensions](https://en.wikipedia.org/wiki/Domain_Name_System_Security_Extensions "wikipedia:Domain Name System Security Extensions")
*   [http://www.dnssec.net/](http://www.dnssec.net/)
    *   [http://www.dnssec.net/practical-documents](http://www.dnssec.net/practical-documents)
    *   [http://www.dnssec.net/rfc](http://www.dnssec.net/rfc)
*   [https://www.iana.org/dnssec/](https://www.iana.org/dnssec/)
*   [https://www.dnssec-tools.org/](https://www.dnssec-tools.org/)
*   [http://linux.die.net/man/1/sshfp](http://linux.die.net/man/1/sshfp)
*   [https://bugs.archlinux.org/task/20325](https://bugs.archlinux.org/task/20325) - [DNSSEC] Add DNS validation support to ArchLinux
*   [DNSSEC Visualizer](http://dnsviz.net)