This article introduces the Arch CVE Monitoring Team (ACMT) and describes best practices for contributing.

## Contents

*   [1 Introduction](#Introduction)
*   [2 Joining the ACMT](#Joining_the_ACMT)
*   [3 Participation Guidelines](#Participation_Guidelines)
*   [4 Procedure](#Procedure)
    *   [4.1 Bug Report Template](#Bug_Report_Template)
*   [5 Resources](#Resources)
    *   [5.1 RSS](#RSS)
    *   [5.2 Mailing Lists](#Mailing_Lists)
    *   [5.3 Other Distributions](#Other_Distributions)
    *   [5.4 Other](#Other)
    *   [5.5 More](#More)
*   [6 Package Categories and Team Members](#Package_Categories_and_Team_Members)

## Introduction

Arch Linux is a community-driven distribution. It relies upon the efforts of volunteers to maintain and improve the distribution itself and to support fellow community members.

The importance of software security cannot be overstated. Today's society relies upon computer technology for everything from amusement to indispensable national and local infrastructure. Many rely upon Arch Linux to provide these.

On March 9, 2014, Allan McRae [called](https://mailman.archlinux.org/pipermail/arch-dev-public/2014-March/025952.html) upon our community to assist in securing Arch Linux by monitoring any and all relevant resources for announced [Common Vulnerabilities and Exposures](https://en.wikipedia.org/wiki/Common_Vulnerabilities_and_Exposures "wikipedia:Common Vulnerabilities and Exposures") (CVE's). In contrast to security issues which can be fixed by updating, CVE's require patches to be backported. As such, Arch developers must be notified that this is the case. This is where the ACMT comes in.

The ACMT should embody the efforts of the "security-conscious" part of the Arch users population. Server owners, maintainers of workstations in production environments as well as concerned personal users would gain the benefit of relatively prompt security updates. The ACMT should help alleviate two important problems: finding bugs, communicating with developers.

The Team is a volunteer maintained service. Volunteers are welcome to help identify and notify packages with security vulnerabilities.

## Joining the ACMT

Joining is as simple as helping. Firstly, join the [Arch Security mailing list](https://mailman.archlinux.org/mailman/listinfo/arch-security) and/or IRC chan [#archlinux-security](irc://irc.freenode.net/archlinux-security). Secondly, consider the area where you would like to help. It would be ideal to have team members' labor divided across the software ecosystem as equally as possible. This helps the Team to quickly and efficiently find and report CVE's. Software categories are listed [below](#Package_Categories_and_Team_Members). However, it is not required that those who wish to volunteer restrict their monitoring in any way. "Global" and multiple-category volunteers are needed and encouraged.

It is recommended that interested parties please consider monitoring those categories for which there are fewer volunteers. However, it is fully recognized that volunteers contribute best in areas in which they are most interested. Please consider both of these factors when selecting where your primary efforts will be placed. However, please note that it is not required that you restrict your monitoring to any one particular category. *The goal of the ACMT is to simply keep Arch Linux secure. Any and all efforts are more than welcome and unreservedly appreciated.*

If you would like to join the Team, please edit this page to include your name in the [Package Categories and Team Members](#Package_Categories_and_Team_Members) section below. Please place your name beneath the package category for which you will be monitoring. If you do not care to monitor specific categories and you would like to contribute any and all, please place your name in the "Global" category. *These options are not mutually exclusive.*

## Participation Guidelines

ACMT monitors all packages within the following repositories:

*   *core*
*   *extra*
*   *community*

Follow mailing lists (both development and user), security advisories (if any) and bug trackers on a regular basis. A few resources are listed below. You will quickly learn the different kind of vulnerabilities if you are unfamiliar. For those who will monitor languages, it is ideal to be able to operate at both the interpreter level (often written in C) and the language level.

Everyone should file bug reports. If you are unsure how to file a bug report, please refer to the [Reporting bug guidelines](/index.php/Reporting_bug_guidelines "Reporting bug guidelines").

People with the technical ability are encouraged to not only file bug reports about CVE's, but write/comment patches, test, communicate with upstream developers, among other things.

## Procedure

A security vulnerability has been found in a software package within the Arch Linux official repositories. An ACMT member picks up this information from some mailing list he/she is following.

*   In order to assure vulnerability, verify the report against the current package version (including possible patches) and collect as much information (also via search engines) as possible.
*   If upstream released a new version that corrects the issue, the ACMT member should flag the package out-of-date.
    *   If the package has not been updated after a too long delay, a bug report should be filed about the security issue.
    *   If this is an important (critical) security issue, a bug report must be filed immediately after flagging the package out-of-date.
    *   If there is no upstream release available, a but report must be filed including the patches for mitigation.
*   If a bug report has been created, the following informations are mandatory:
    *   Description about the security issue and its impact
    *   Links to the CVE-IDs and (upstream) report
    *   If no release is available, links to the upstream patches (or attachments) that mitigate the issue
*   Add the issue to a new row at the top of the [CVE Tracking](/index.php/CVE "CVE") page (provide a wiki change summary including package name and some information)

If you have a private bug to report, [then use security@archlinux.org](https://mailman.archlinux.org/pipermail/arch-security/2014-June/000088.html). Please note that the address for private bugs reporting is *security*, not *arch-security*. A private bug is one that is too sensitive to post where anyone can read and exploit it, e.g. vulnerabilities in Arch Linux infrastructure.

### Bug Report Template

```
Title : [<pkg-name>] <CVE-ID> vulnerability-types
Description:
Quick description of the issue (or copy/paste from oss-sec, upstream bug reports, etc.)
upstream bug report [0]

Resolution:
patch [1] 

Resources:
[0] links to upstream bug report
[1] link to patch

```

The criticality of the bug report should be set to either Critical or High, depending on the severity of the issue. Some updates will be much more critical than others. However, updates are always recommended in the case of any vulnerability.

Once this process is complete, please add the CVE and later the [ASA](/index.php/Security_Advisories "Security Advisories") to the [CVE](/index.php/CVE "CVE") Documented Resolved CVE table.

## Resources

### RSS

	National Vulnerability Database (NVD)

	All CVE vulnerabilites: [http://nvd.nist.gov/download/nvd-rss.xml](http://nvd.nist.gov/download/nvd-rss.xml)

	All fully analyzed CVE vulnerabilities: [http://nvd.nist.gov/download/nvd-rss-analyzed.xml](http://nvd.nist.gov/download/nvd-rss-analyzed.xml)

### Mailing Lists

	oss-sec

	main list dealing with security of free software, a lot of CVE attributions happen here, required if you wish to follow security news.

	info: [http://oss-security.openwall.org/wiki/mailing-lists/oss-security](http://oss-security.openwall.org/wiki/mailing-lists/oss-security)

	subscribe: oss-security-subscribe(at)lists.openwall.com

	archive: [http://www.openwall.com/lists/oss-security/](http://www.openwall.com/lists/oss-security/)

	bugtraq

	a full disclosure moderated mailing list (noisy)

	info: [http://www.securityfocus.com/archive/1/description](http://www.securityfocus.com/archive/1/description)

	subscribe: bugtraq-subscribe(at)securityfocus.com

	full-disclosure

	another full-disclosure mailing-list (noisy)

	info: [http://lists.grok.org.uk/full-disclosure-charter.html](http://lists.grok.org.uk/full-disclosure-charter.html)

	subscribe: full-disclosure-request(at)lists.grok.org.uk

Also consider following the mailing lists for specific packages, such as LibreOffice, X.org, Puppetlabs, ISC, etc.

### Other Distributions

Resources of other distributions (to look for CVE, patch, comments etc.):

	RedHat and Fedora

	rss advisories: [https://admin.fedoraproject.org/updates/rss/rss2.0?type=security](https://admin.fedoraproject.org/updates/rss/rss2.0?type=security)

	CVE tracker: [https://access.redhat.com/security/cve/](https://access.redhat.com/security/cve/)<CVE-id>

	bug tracker: [https://bugzilla.redhat.com/show_bug.cgi?id=](https://bugzilla.redhat.com/show_bug.cgi?id=)<CVE-id>

	Ubuntu

	advisories: [http://www.ubuntu.com/usn/atom.xml](http://www.ubuntu.com/usn/atom.xml)

	CVE tracker: [http://people.canonical.com/~ubuntu-security/cve/?cve=](http://people.canonical.com/~ubuntu-security/cve/?cve=)<CVE-id>

	database: [https://code.launchpad.net/~ubuntu-security/ubuntu-cve-tracker/master](https://code.launchpad.net/~ubuntu-security/ubuntu-cve-tracker/master)

	Debian

	CVE tracker: [http://security-tracker.debian.org/tracker/](http://security-tracker.debian.org/tracker/)<CVE-id>

	patch-tracker: [http://patch-tracker.debian.org/](http://patch-tracker.debian.org/)

	database: [http://anonscm.debian.org/viewvc/secure-testing/data/](http://anonscm.debian.org/viewvc/secure-testing/data/)

	OpenSUSE

	CVE tracker: [http://support.novell.com/security/cve/](http://support.novell.com/security/cve/)<CVE-id>.html

### Other

	Mitre and NVD links for CVE's

	[http://cve.mitre.org/cgi-bin/cvename.cgi?name=](http://cve.mitre.org/cgi-bin/cvename.cgi?name=)<CVE-id>

	[http://web.nvd.nist.gov/view/vuln/detail?vulnId=](http://web.nvd.nist.gov/view/vuln/detail?vulnId=)<CVE-id>

NVD and Mitre do not necessarily fill their CVE entry immediately after attribution, so it is not always relevant for Arch. The CVE-id and the "Date Entry Created" fields do not have particular meaning. CVE are attributed by CVE Numbering Authorities (CNA), and each CNA obtain CVE blocks from Mitre when needed/asked, so the CVE ID is not linked to the attribution date. The "Date Entry Created" field often only indicates when the CVE block was given to the CNA, nothing more.

	Linux Weekly News

	LWN provides a daily notice of security updates for various distributions

	[http://lwn.net/headlines/newrss](http://lwn.net/headlines/newrss)

### More

For more resources, please see the OpenWall's [Open Source Software Security Wiki](http://oss-security.openwall.org/wiki/).

## Package Categories and Team Members

Below is a list of general package categories. Should you like, you are welcome to add a new category. Please remember the KISS philosophy when editing the list.

*   Global

	[Billy Wayne McCann](/index.php/User:Bwayne "User:Bwayne")

	[HegemoOn](/index.php/User:Netmonk "User:Netmonk")

	[Timothée Ravier](/index.php/User:Siosm "User:Siosm")

	[Remi Gacogne](/index.php/User:Rgacogne "User:Rgacogne")

	[Levente Polyak](/index.php/User:Anthraxx "User:Anthraxx")

	[Christian Rebischke](/index.php/User:Shibumi "User:Shibumi")

	[Santiago Torres-Arias](/index.php/User:Sangy "User:Sangy")

	[Your Name Here]

*   Kernel

	Mark Lee

*   Filesystems

	[Your Name Here]

*   GNU userland

	[Your Name Here]

*   Xorg

	[Your Name Here]

*   Systemd

	[Your Name Here]

*   Perl and associated software

	[Your Name Here]

*   Python and associated software

	[Scott Lawrence](/index.php/User:Srl "User:Srl")

	[Your Name Here]

*   Java and associated software

	[Your Name Here]

*   Ruby and associated software

	[Your Name Here]

*   Gtk/Gnome and associated software

	[Your Name Here]

*   QT/KDE and associated software

	[Billy Wayne McCann](/index.php/User:Bwayne "User:Bwayne") (KDE)

	[Your Name Here]

*   Various Windows Managers (please include which WM along with your name)

	[Your Name Here]