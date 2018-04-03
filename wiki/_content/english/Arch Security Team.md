The Arch Security Team is a group of volunteers whose goal is to track security issues with Arch Linux packages. All issues are tracked on the [Arch Linux security tracker](https://security.archlinux.org/). The team was formerly known as the *Arch CVE Monitoring Team*.

## Contents

*   [1 Mission](#Mission)
*   [2 Contribute](#Contribute)
*   [3 Procedure](#Procedure)
    *   [3.1 Information sharing and investigation phase](#Information_sharing_and_investigation_phase)
    *   [3.2 Upstream situation and bug reporting](#Upstream_situation_and_bug_reporting)
    *   [3.3 Tracking and publishing](#Tracking_and_publishing)
*   [4 Resources](#Resources)
    *   [4.1 RSS](#RSS)
    *   [4.2 Mailing lists](#Mailing_lists)
    *   [4.3 Other Distributions](#Other_Distributions)
    *   [4.4 Other](#Other)
    *   [4.5 More](#More)
*   [5 Team Members](#Team_Members)

## Mission

The mission of the Arch Security Team is to contribute to the improvement of the security of Arch Linux.

The most important duty of the team is to find and track issues assigned a [Common Vulnerabilities and Exposure](https://en.wikipedia.org/wiki/Common_Vulnerabilities_and_Exposures "wikipedia:Common Vulnerabilities and Exposures") (CVE). A CVE is public, it is identified by a unique ID of the form *CVE-YYYY-number*.

They publish ASAs (*Arch Linux Security Advisory*) which is an Arch-specific warning disseminated to Arch users. ASAs are scheduled in the tracker for peer-review, and need two acknowledgments from team members before being published.

The *Arch Linux security tracker* is a platform used by the Arch Security Team to track packages, add CVEs and generate advisory text.

**Note:**

*   An *Arch Linux Vulnerability Group* (AVG) is a group of CVEs related to a set of packages within the same *pkgbase*.
*   Packages qualified for an advisory must be part of the *core*, *extra*, *community* or *multilib* repository.

## Contribute

To get involved in the identification of the vulnerabilities, it is recommended to:

*   Follow the [#archlinux-security](irc://irc.freenode.net/archlinux-security) IRC channel. It is the main communication medium for reporting and discussing CVEs, packages affected and first fixed package version.

*   In order to be warned early about new issues, one can monitor the recommended [#Mailing lists](#Mailing_lists) for new CVEs, along with other sources if required.

*   We encourage volunteers to look over the advisories for mistakes, questions, or comments and report in the IRC channel.

*   Subscribe to the mailing lists [arch-security](https://lists.archlinux.org/listinfo/arch-security) and [oss-security](http://oss-security.openwall.org/wiki/mailing-lists/oss-security).

*   Committing code to the [arch-security-tracker (GitHub)](https://github.com/archlinux/arch-security-tracker) project is a great way to contribute to the team.

*   Derivative distributions that rely on Arch Linux package repositories are encouraged to contribute. This helps the security of all the users.

## Procedure

The procedure to follow whenever a security vulnerability has been found in a software packaged within the Arch Linux official repositories is the following:

### Information sharing and investigation phase

*   Reach out an Arch Security Team member via your preferred channel to ensure the issue has been brought to the attention of the team.
*   In order to substantiate the vulnerability, verify the CVE report against the current package version (including possible patches), and collect as much information as possible on the issue, including via search engines. If you need help to investigate the security issue, ask for advice or support on the IRC channel.

### Upstream situation and bug reporting

Two situations may arise:

*   If upstream released a new version that fixes the issue, the Security Team member should flag the package out-of-date.
    *   If the package has not been updated after a long delay, a bug report should be filed about the vulnerability.
    *   If this is a critical security issue, a bug report must be filed immediately after flagging the package out-of-date.
*   If there is no upstream release available, a bug report must be filed including the patches for mitigation. The following information must be provided in the bug report:
    *   Description about the security issue and its impact
    *   Links to the CVE-IDs and (upstream) report
    *   If no release is available, links to the upstream patches (or attachments) that mitigate the issue

### Tracking and publishing

The following tasks must be performed by team members:

*   A team member will create an advisory on the [security tracker](https://security.archlinux.org/) and add the CVEs for tracking.
*   A team member with access to [arch-security](https://lists.archlinux.org/listinfo/arch-security) will generate an ASA from the tracker and publish it.

**Note:** If you have a private bug to report, contact [security@archlinux.org](https://mailman.archlinux.org/pipermail/arch-security/2014-June/000088.html). Please note that the address for private bug reporting is *security*, not *arch-security*. A private bug is one that is too sensitive to post where anyone can read and exploit it, e.g. vulnerabilities in the Arch Linux infrastructure.

## Resources

### RSS

	National Vulnerability Database (NVD)

	All CVE vulnerabilites: [https://nvd.nist.gov/download/nvd-rss.xml](https://nvd.nist.gov/download/nvd-rss.xml)

	All fully analyzed CVE vulnerabilities: [https://nvd.nist.gov/download/nvd-rss-analyzed.xml](https://nvd.nist.gov/download/nvd-rss-analyzed.xml)

### Mailing lists

	oss-sec

	Main list dealing with security of free software, a lot of CVE attributions happen here, required if you wish to follow security news.

	Info: [http://oss-security.openwall.org/wiki/mailing-lists/oss-security](http://oss-security.openwall.org/wiki/mailing-lists/oss-security)

	Subscribe: oss-security-subscribe(at)lists.openwall.com

	Archive: [http://www.openwall.com/lists/oss-security/](http://www.openwall.com/lists/oss-security/)

	BugTraq

	A full disclosure moderated mailing list (noisy).

	Info: [http://www.securityfocus.com/archive/1/description](http://www.securityfocus.com/archive/1/description)

	Subscribe: bugtraq-subscribe(at)securityfocus.com

	Full-disclosure

	Another full-disclosure mailing-list (noisy).

	Info: [http://lists.grok.org.uk/full-disclosure-charter.html](http://lists.grok.org.uk/full-disclosure-charter.html)

	Subscribe: full-disclosure-request(at)lists.grok.org.uk

Also consider following the mailing lists for specific packages, such as LibreOffice, X.org, Puppetlabs, ISC, etc.

### Other Distributions

Resources of other distributions (to look for CVE, patch, comments etc.):

	RedHat and Fedora

	Advisories feed: [https://bodhi.fedoraproject.org/rss/updates/?type=security](https://bodhi.fedoraproject.org/rss/updates/?type=security)

	CVE tracker: [https://access.redhat.com/security/cve/](https://access.redhat.com/security/cve/)<CVE-ID>

	Bug tracker: [https://bugzilla.redhat.com/show_bug.cgi?id=](https://bugzilla.redhat.com/show_bug.cgi?id=)<CVE-ID>

	Ubuntu

	Advisories feed: [https://www.ubuntu.com/usn/atom.xml](https://www.ubuntu.com/usn/atom.xml)

	CVE tracker: [https://people.canonical.com/~ubuntu-security/cve/?cve=](https://people.canonical.com/~ubuntu-security/cve/?cve=)<CVE-ID>

	Database: [https://code.launchpad.net/~ubuntu-security/ubuntu-cve-tracker/master](https://code.launchpad.net/~ubuntu-security/ubuntu-cve-tracker/master)

	Debian

	CVE tracker: [https://security-tracker.debian.org/tracker/](https://security-tracker.debian.org/tracker/)<CVE-ID>/

	Patch tracker: [https://tracker.debian.org/pkg/patch](https://tracker.debian.org/pkg/patch)

	Database: [https://anonscm.debian.org/viewvc/secure-testing/data/](https://anonscm.debian.org/viewvc/secure-testing/data/)

	OpenSUSE

	CVE tracker: [https://www.suse.com/security/cve/](https://www.suse.com/security/cve/)<CVE-ID>/

### Other

	Mitre and NVD links for CVE's

	[https://cve.mitre.org/cgi-bin/cvename.cgi?name=](https://cve.mitre.org/cgi-bin/cvename.cgi?name=)<CVE-ID>

	[https://web.nvd.nist.gov/view/vuln/detail?vulnId=](https://web.nvd.nist.gov/view/vuln/detail?vulnId=)<CVE-ID>

NVD and Mitre do not necessarily fill their CVE entry immediately after attribution, so it is not always relevant for Arch. The CVE-ID and the "Date Entry Created" fields do not have particular meaning. CVE are attributed by CVE Numbering Authorities (CNA), and each CNA obtain CVE blocks from Mitre when needed/asked, so the CVE ID is not linked to the attribution date. The "Date Entry Created" field often only indicates when the CVE block was given to the CNA, nothing more.

	Linux Weekly News

	LWN provides a daily notice of security updates for various distributions.

	[https://lwn.net/headlines/newrss](https://lwn.net/headlines/newrss)

### More

For more resources, please see the OpenWall's [Open Source Software Security Wiki](http://oss-security.openwall.org/wiki/).

## Team Members

The current members of the Arch Security Team are:

*   [Levente Polyak](/index.php/User:Anthraxx "User:Anthraxx")
*   [Remi Gacogne](/index.php/User:Rgacogne "User:Rgacogne")
*   [Christian Rebischke](/index.php/User:Shibumi "User:Shibumi")
*   [Jelle van der Waa](/index.php/User:Jelly "User:Jelly")
*   [Santiago Torres-Arias](/index.php/User:Sangy "User:Sangy")
*   [Jonathan Roemer](/index.php/User:Pid1 "User:Pid1")
*   [Morten Linderud](/index.php/User:Foxboron "User:Foxboron")

**Note:** Run `!pingsec <msg>` in [IRC channels](/index.php/IRC_channels "IRC channels") to highlight all current security team members.