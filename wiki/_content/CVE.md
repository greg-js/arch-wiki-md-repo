# CVE

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [Arch CVE Monitoring Team](/index.php/Arch_CVE_Monitoring_Team "Arch CVE Monitoring Team")
*   [Security Advisories](/index.php/Security_Advisories "Security Advisories")

This article documents [Common Vulnerabilities and Exposures](https://en.wikipedia.org/wiki/Common_Vulnerabilities_and_Exposures "wikipedia:Common Vulnerabilities and Exposures") (CVE's) that are found and fixed in Arch Linux.

## Contents

*   [1 Introduction](#Introduction)
*   [2 Helping](#Helping)
*   [3 Procedure](#Procedure)
*   [4 Response time](#Response_time)
*   [5 Documented CVE's](#Documented_CVE.27s)

## Introduction

CVE's represent critical security vulnerabilities which must be addressed as quickly as possible.

Once a CVE has been located and fixed, it is added to the CVE documentation table below.

## Helping

This is a community driven project. Please consider joining the [Arch CVE Monitoring Team](/index.php/Arch_CVE_Monitoring_Team "Arch CVE Monitoring Team").

Also, join the [Arch security mailing list](https://mailman.archlinux.org/mailman/listinfo/arch-security). There is an IRC on [irc://irc.freenode.net/archlinux-security](irc://irc.freenode.net/archlinux-security).

## Procedure

When adding a CVE to the table, add it to the TOP of the table. Use Wiki markup to create links in the "CVE-ID", "Package", and "Status" columns. The following template may be used to ease the process of adding CVE entries into the table. The first line, "|-" represents the creation of a new row in the table, while the second line should be modified per CVE:

 `CVE Table Addition Template` 

```
|-
| {{CVE|CVE-2014-????}} || {{Pkg|pkgname}} || Disclosure date || Affected versions || Fixed in version || Arch Linux response time || Status(Fixed|Pending|Invalid) (Bug reports) || {{ASA|ASA-??????-??}}

```

**Note:**

*   If the CVE is not found in [NVD](http://nvd.nist.gov/home.cfm), just include a link to different database in the first column: `[http://link.to.cve CVE-2014-????]`
*   The "Disclosure date" field should be expressed in [ISO 8601 format](https://en.wikipedia.org/wiki/ISO_8601 "wikipedia:ISO 8601") to avoid any confusion. Example: 2014-03-22.
*   The "Arch Linux response time" field corresponds to the time between the public release of a vulnerability and the date the package update fixing the vulnerability is made available in the official stable repositories. The "Time really vulnerable" is potentially much lengthier but is harder to estimate.

The above "CVE-template" should be added after the line:

 `! scope="col" width="125px" data-sort-type="text" | CVE-ID !! Package !! Disclosure date !! Affected versions !! Fixed in version !! Arch Linux response time !! Status (and related bug reports) !! ASA-ID` 

## Response time

The response time is the time taken to get a fixed package to the stable repositories.

## Documented CVE's

**Note:** Refer to the [#Procedure](#Procedure) section when adding new entries.

<table class="wikitable sortable" style="margin: 1em auto 1em auto; text-align: center;" width="100%">

<tbody>

<tr>

<th height="50px" colspan="8" style="font-size: 125%;">**TRACKED CVE's**</th>

</tr>

<tr>

<th scope="col" width="130px" data-sort-type="text">CVE-ID</th>

<th>Package</th>

<th>Disclosure date</th>

<th>Affected versions</th>

<th>Fixed in Arch Linux package version</th>

<th>Arch Linux response time</th>

<th>Status (and related bug reports)</th>

<th>ASA-ID</th>

</tr>

<tr>

<td>[CVE-2015-7201](https://access.redhat.com/security/cve/CVE-2015-7201) [CVE-2015-7205](https://access.redhat.com/security/cve/CVE-2015-7205) [CVE-2015-7212](https://access.redhat.com/security/cve/CVE-2015-7212) [CVE-2015-7213](https://access.redhat.com/security/cve/CVE-2015-7213) [CVE-2015-7214](https://access.redhat.com/security/cve/CVE-2015-7214) [[1]](https://www.mozilla.org/en-US/security/known-vulnerabilities/thunderbird/#thunderbird38.5)</td>

<td>[thunderbird](https://www.archlinux.org/packages/?name=thunderbird)</td>

<td>2015-12-23</td>

<td><= 38.4.0-2</td>

<td>38.5.0-1</td>

<td><1d</td>

<td>Fixed</td>

</tr>

<tr>

<td>[CVE-2015-8612](https://access.redhat.com/security/cve/CVE-2015-8612) [[2]](http://seclists.org/oss-sec/2015/q4/541)</td>

<td>[blueman](https://www.archlinux.org/packages/?name=blueman)</td>

<td>2015-12-18</td>

<td><= 2.0.2-1</td>

<td>**Vulnerable**</td>

</tr>

<tr>

<td>[CVE-2015-8659](https://access.redhat.com/security/cve/CVE-2015-8659) [[3]](http://seclists.org/oss-sec/2015/q4/576)</td>

<td>[nghttp2](https://www.archlinux.org/packages/?name=nghttp2)</td>

<td>2015-12-23</td>

<td><= 1.5.0-2</td>

<td>**Vulnerable**</td>

</tr>

<tr>

<td>[CVE-2015-7555](https://access.redhat.com/security/cve/CVE-2015-7555) [[4]](http://seclists.org/oss-sec/2015/q4/548)</td>

<td>[giflib](https://www.archlinux.org/packages/?name=giflib)</td>

<td>2015-12-21</td>

<td><= 5.1.1-1</td>

<td>**Vulnerable**</td>

</tr>

<tr>

<td>[CVE-2015-7557](https://access.redhat.com/security/cve/CVE-2015-7557) [CVE-2015-7558](https://access.redhat.com/security/cve/CVE-2015-7558) [[5]](http://seclists.org/oss-sec/2015/q4/549)</td>

<td>[librsvg](https://www.archlinux.org/packages/?name=librsvg)</td>

<td>2015-12-21</td>

<td><= 2:2.40.11-1</td>

<td>**Vulnerable**</td>

</tr>

<tr>

<td>[CVE-2015-2141](https://access.redhat.com/security/cve/CVE-2015-2141) [[6]](https://www.cryptopp.com/release563.html)</td>

<td>[crypto++](https://www.archlinux.org/packages/?name=crypto%2B%2B)</td>

<td>2015-12-20</td>

<td><= 5.6.2-4</td>

<td>**Vulnerable**</td>

</tr>

<tr>

<td>[CVE-2015-8622](https://access.redhat.com/security/cve/CVE-2015-8622) [CVE-2015-8623](https://access.redhat.com/security/cve/CVE-2015-8623) [CVE-2015-8624](https://access.redhat.com/security/cve/CVE-2015-8624) [CVE-2015-8625](https://access.redhat.com/security/cve/CVE-2015-8625) [CVE-2015-8626](https://access.redhat.com/security/cve/CVE-2015-8626) [CVE-2015-8627](https://access.redhat.com/security/cve/CVE-2015-8627) [CVE-2015-8628](https://access.redhat.com/security/cve/CVE-2015-8628) [[7]](http://seclists.org/oss-sec/2015/q4/552)</td>

<td>[mediawiki](https://www.archlinux.org/packages/?name=mediawiki)</td>

<td>2015-12-17</td>

<td><= 1.26.0-1</td>

<td>**Vulnerable**</td>

</tr>

<tr>

<td>[CVE-2015-8614](https://access.redhat.com/security/cve/CVE-2015-8614) [[8]](http://www.thewildbeast.co.uk/claws-mail/bugzilla/show_bug.cgi?id=3557)</td>

<td>[claws-mail](https://www.archlinux.org/packages/?name=claws-mail)</td>

<td>2015-12-21</td>

<td><= 3.13.0-1</td>

<td>3.13.1-1</td>

<td>1d</td>

<td>Fixed</td>

<td>[ASA-201512-13](https://lists.archlinux.org/pipermail/arch-security/2015-December/000473.html)</td>

</tr>

<tr>

<td>[CVE-2015-8369](https://access.redhat.com/security/cve/CVE-2015-8369)</td>

<td>[cacti](https://www.archlinux.org/packages/?name=cacti)</td>

<td>2015-12-17</td>

<td><= 0.8.8_f-3</td>

<td>**Vulnerable**</td>

</tr>

<tr>

<td>[[9]](https://blog.fuzzing-project.org/32-Out-of-bounds-read-in-OpenVPN.html)</td>

<td>[openvpn](https://www.archlinux.org/packages/?name=openvpn)</td>

<td>2015-12-18</td>

<td><= 2.3.8-2</td>

<td>**Vulnerable** ([FS#47498](https://bugs.archlinux.org/task/47498))</td>

</tr>

<tr>

<td>[CVE-2015-8549](https://access.redhat.com/security/cve/CVE-2015-8549) [[10]](http://www.ocert.org/advisories/ocert-2015-011.html)</td>

<td>[python2-pyamf](https://www.archlinux.org/packages/?name=python2-pyamf)</td>

<td>2015-12-17</td>

<td><= 0.7.2-1</td>

<td>0.8.0-2</td>

<td><1d</td>

<td>Fixed</td>

<td>[ASA-201512-12](https://lists.archlinux.org/pipermail/arch-security/2015-December/000472.html)</td>

</tr>

<tr>

<td>[CVE-2015-7551](https://access.redhat.com/security/cve/CVE-2015-7551) [[11]](https://www.ruby-lang.org/en/news/2015/12/16/unsafe-tainted-string-usage-in-fiddle-and-dl-cve-2015-7551/)</td>

<td>[ruby](https://www.archlinux.org/packages/?name=ruby)</td>

<td>2015-12-16</td>

<td><= 2.2.3-1</td>

<td>2.2.4-1</td>

<td>1d</td>

<td>Fixed</td>

<td>[ASA-201512-11](https://lists.archlinux.org/pipermail/arch-security/2015-December/000471.html)</td>

</tr>

<tr>

<td>[CVE-2015-7201](https://access.redhat.com/security/cve/CVE-2015-7201) [CVE-2015-7202](https://access.redhat.com/security/cve/CVE-2015-7202) [CVE-2015-7203](https://access.redhat.com/security/cve/CVE-2015-7203) [CVE-2015-7204](https://access.redhat.com/security/cve/CVE-2015-7204) [CVE-2015-7205](https://access.redhat.com/security/cve/CVE-2015-7205) [CVE-2015-7207](https://access.redhat.com/security/cve/CVE-2015-7207) [CVE-2015-7208](https://access.redhat.com/security/cve/CVE-2015-7208) [CVE-2015-7210](https://access.redhat.com/security/cve/CVE-2015-7210) [CVE-2015-7211](https://access.redhat.com/security/cve/CVE-2015-7211) [CVE-2015-7212](https://access.redhat.com/security/cve/CVE-2015-7212) [CVE-2015-7213](https://access.redhat.com/security/cve/CVE-2015-7213) [CVE-2015-7214](https://access.redhat.com/security/cve/CVE-2015-7214) [CVE-2015-7215](https://access.redhat.com/security/cve/CVE-2015-7215) [CVE-2015-7216](https://access.redhat.com/security/cve/CVE-2015-7216) [CVE-2015-7217](https://access.redhat.com/security/cve/CVE-2015-7217) [CVE-2015-7218](https://access.redhat.com/security/cve/CVE-2015-7218) [CVE-2015-7219](https://access.redhat.com/security/cve/CVE-2015-7219) [CVE-2015-7220](https://access.redhat.com/security/cve/CVE-2015-7220) [CVE-2015-7221](https://access.redhat.com/security/cve/CVE-2015-7221) [CVE-2015-7222](https://access.redhat.com/security/cve/CVE-2015-7222) [CVE-2015-7223](https://access.redhat.com/security/cve/CVE-2015-7223) [[12]](https://www.mozilla.org/en-US/security/known-vulnerabilities/firefox/#firefox43)</td>

<td>[firefox](https://www.archlinux.org/packages/?name=firefox)</td>

<td>2015-12-15</td>

<td><= 42.0-3</td>

<td>43.0-1</td>

<td><1d</td>

<td>Fixed</td>

<td>[ASA-201512-9](https://lists.archlinux.org/pipermail/arch-security/2015-December/000467.html)</td>

</tr>

<tr>

<td>[CVE-2015-8000](https://access.redhat.com/security/cve/CVE-2015-8000) [[13]](https://kb.isc.org/article/AA-01317)</td>

<td>[bind](https://www.archlinux.org/packages/?name=bind)</td>

<td>2015-12-15</td>

<td><= 9.10.3-2</td>

<td>9.10.3.P2-1</td>

<td><1d</td>

<td>Fixed</td>

<td>[ASA-201512-10](https://lists.archlinux.org/pipermail/arch-security/2015-December/000468.html)</td>

</tr>

<tr>

<td>[CVE-2015-8370](https://access.redhat.com/security/cve/CVE-2015-8370) [[14]](http://hmarco.org/bugs/CVE-2015-8370-Grub2-authentication-bypass.html#fix)</td>

<td>[grub](https://www.archlinux.org/packages/?name=grub)</td>

<td>2015-12-15</td>

<td><= 1:2.02.beta2-5</td>

<td>**Vulnerable** ([FS#47386](https://bugs.archlinux.org/task/47386))</td>

</tr>

<tr>

<td>[CVE-2015-8378](https://access.redhat.com/security/cve/CVE-2015-8378) [[15]](https://www.keepassx.org/news/2015/12/551)</td>

<td>[keepassx](https://www.archlinux.org/packages/?name=keepassx)</td>

<td>2015-12-08</td>

<td><= 0.4.3-7</td>

<td>0.4.4-1</td>

<td><2d</td>

<td>Fixed</td>

<td>[ASA-201512-8](https://lists.archlinux.org/pipermail/arch-security/2015-December/000466.html)</td>

</tr>

<tr>

<td>[CVE-2015-8045](https://access.redhat.com/security/cve/CVE-2015-8045) [CVE-2015-8047](https://access.redhat.com/security/cve/CVE-2015-8047) [CVE-2015-8048](https://access.redhat.com/security/cve/CVE-2015-8048) [CVE-2015-8049](https://access.redhat.com/security/cve/CVE-2015-8049) [CVE-2015-8050](https://access.redhat.com/security/cve/CVE-2015-8050) [CVE-2015-8055](https://access.redhat.com/security/cve/CVE-2015-8055) [CVE-2015-8056](https://access.redhat.com/security/cve/CVE-2015-8056) [CVE-2015-8057](https://access.redhat.com/security/cve/CVE-2015-8057) [CVE-2015-8058](https://access.redhat.com/security/cve/CVE-2015-8058) [CVE-2015-8059](https://access.redhat.com/security/cve/CVE-2015-8059) [CVE-2015-8060](https://access.redhat.com/security/cve/CVE-2015-8060) [CVE-2015-8061](https://access.redhat.com/security/cve/CVE-2015-8061) [CVE-2015-8062](https://access.redhat.com/security/cve/CVE-2015-8062) [CVE-2015-8063](https://access.redhat.com/security/cve/CVE-2015-8063) [CVE-2015-8064](https://access.redhat.com/security/cve/CVE-2015-8064) [CVE-2015-8065](https://access.redhat.com/security/cve/CVE-2015-8065) [CVE-2015-8066](https://access.redhat.com/security/cve/CVE-2015-8066) [CVE-2015-8067](https://access.redhat.com/security/cve/CVE-2015-8067) [CVE-2015-8068](https://access.redhat.com/security/cve/CVE-2015-8068) [CVE-2015-8069](https://access.redhat.com/security/cve/CVE-2015-8069) [CVE-2015-8070](https://access.redhat.com/security/cve/CVE-2015-8070) [CVE-2015-8071](https://access.redhat.com/security/cve/CVE-2015-8071) [CVE-2015-8401](https://access.redhat.com/security/cve/CVE-2015-8401) [CVE-2015-8402](https://access.redhat.com/security/cve/CVE-2015-8402) [CVE-2015-8403](https://access.redhat.com/security/cve/CVE-2015-8403) [CVE-2015-8404](https://access.redhat.com/security/cve/CVE-2015-8404) [CVE-2015-8405](https://access.redhat.com/security/cve/CVE-2015-8405) [CVE-2015-8406](https://access.redhat.com/security/cve/CVE-2015-8406) [CVE-2015-8407](https://access.redhat.com/security/cve/CVE-2015-8407) [CVE-2015-8408](https://access.redhat.com/security/cve/CVE-2015-8408) [CVE-2015-8409](https://access.redhat.com/security/cve/CVE-2015-8409) [CVE-2015-8410](https://access.redhat.com/security/cve/CVE-2015-8410) [CVE-2015-8411](https://access.redhat.com/security/cve/CVE-2015-8411) [CVE-2015-8412](https://access.redhat.com/security/cve/CVE-2015-8412) [CVE-2015-8413](https://access.redhat.com/security/cve/CVE-2015-8413) [CVE-2015-8414](https://access.redhat.com/security/cve/CVE-2015-8414) [CVE-2015-8415](https://access.redhat.com/security/cve/CVE-2015-8415) [CVE-2015-8416](https://access.redhat.com/security/cve/CVE-2015-8416) [CVE-2015-8417](https://access.redhat.com/security/cve/CVE-2015-8417) [CVE-2015-8418](https://access.redhat.com/security/cve/CVE-2015-8418) [CVE-2015-8419](https://access.redhat.com/security/cve/CVE-2015-8419) [CVE-2015-8420](https://access.redhat.com/security/cve/CVE-2015-8420) [CVE-2015-8421](https://access.redhat.com/security/cve/CVE-2015-8421) [CVE-2015-8422](https://access.redhat.com/security/cve/CVE-2015-8422) [CVE-2015-8423](https://access.redhat.com/security/cve/CVE-2015-8423) [CVE-2015-8424](https://access.redhat.com/security/cve/CVE-2015-8424) [CVE-2015-8425](https://access.redhat.com/security/cve/CVE-2015-8425) [CVE-2015-8426](https://access.redhat.com/security/cve/CVE-2015-8426) [CVE-2015-8427](https://access.redhat.com/security/cve/CVE-2015-8427) [CVE-2015-8428](https://access.redhat.com/security/cve/CVE-2015-8428) [CVE-2015-8429](https://access.redhat.com/security/cve/CVE-2015-8429) [CVE-2015-8430](https://access.redhat.com/security/cve/CVE-2015-8430) [CVE-2015-8431](https://access.redhat.com/security/cve/CVE-2015-8431) [CVE-2015-8432](https://access.redhat.com/security/cve/CVE-2015-8432) [CVE-2015-8433](https://access.redhat.com/security/cve/CVE-2015-8433) [CVE-2015-8434](https://access.redhat.com/security/cve/CVE-2015-8434) [CVE-2015-8435](https://access.redhat.com/security/cve/CVE-2015-8435) [CVE-2015-8436](https://access.redhat.com/security/cve/CVE-2015-8436) [CVE-2015-8437](https://access.redhat.com/security/cve/CVE-2015-8437) [CVE-2015-8438](https://access.redhat.com/security/cve/CVE-2015-8438) [CVE-2015-8439](https://access.redhat.com/security/cve/CVE-2015-8439) [CVE-2015-8440](https://access.redhat.com/security/cve/CVE-2015-8440) [CVE-2015-8441](https://access.redhat.com/security/cve/CVE-2015-8441) [CVE-2015-8442](https://access.redhat.com/security/cve/CVE-2015-8442) [CVE-2015-8443](https://access.redhat.com/security/cve/CVE-2015-8443) [CVE-2015-8444](https://access.redhat.com/security/cve/CVE-2015-8444) [CVE-2015-8445](https://access.redhat.com/security/cve/CVE-2015-8445) [CVE-2015-8446](https://access.redhat.com/security/cve/CVE-2015-8446) [CVE-2015-8447](https://access.redhat.com/security/cve/CVE-2015-8447) [CVE-2015-8448](https://access.redhat.com/security/cve/CVE-2015-8448) [CVE-2015-8449](https://access.redhat.com/security/cve/CVE-2015-8449) [CVE-2015-8450](https://access.redhat.com/security/cve/CVE-2015-8450) [CVE-2015-8451](https://access.redhat.com/security/cve/CVE-2015-8451) [CVE-2015-8452](https://access.redhat.com/security/cve/CVE-2015-8452) [CVE-2015-8453](https://access.redhat.com/security/cve/CVE-2015-8453) [CVE-2015-8454](https://access.redhat.com/security/cve/CVE-2015-8454) [CVE-2015-8455](https://access.redhat.com/security/cve/CVE-2015-8455) [[16]](https://helpx.adobe.com/security/products/flash-player/apsb15-32.html)</td>

<td>[flashplugin](https://www.archlinux.org/packages/?name=flashplugin)</td>

<td>2015-12-08</td>

<td><= 11.2.202.548-1</td>

<td>11.2.202.554-1</td>

<td><1d</td>

<td>Fixed</td>

<td>[ASA-201512-7](https://lists.archlinux.org/pipermail/arch-security/2015-December/000465.html)</td>

</tr>

<tr>

<td>[CVE-2015-6788](https://access.redhat.com/security/cve/CVE-2015-6788) [CVE-2015-6789](https://access.redhat.com/security/cve/CVE-2015-6789) [CVE-2015-6790](https://access.redhat.com/security/cve/CVE-2015-6790) [CVE-2015-6791](https://access.redhat.com/security/cve/CVE-2015-6791) [[17]](http://googlechromereleases.blogspot.fr/2015/12/stable-channel-update_8.html)</td>

<td>[chromium](https://www.archlinux.org/packages/?name=chromium)</td>

<td>2015-12-08</td>

<td><= 47.0.2526.73-1</td>

<td>47.0.2526.80-1</td>

<td><1d</td>

<td>Fixed</td>

<td>[ASA-201512-5](https://lists.archlinux.org/pipermail/arch-security/2015-December/000463.html)</td>

</tr>

<tr>

<td>[CVE-2015-3193](https://access.redhat.com/security/cve/CVE-2015-3193) [CVE-2015-3194](https://access.redhat.com/security/cve/CVE-2015-3194) [CVE-2015-3195](https://access.redhat.com/security/cve/CVE-2015-3195) [CVE-2015-3196](https://access.redhat.com/security/cve/CVE-2015-3196) [CVE-2015-1794](https://access.redhat.com/security/cve/CVE-2015-1794) [[18]](https://www.openssl.org/news/secadv/20151203.txt)</td>

<td>[openssl](https://www.archlinux.org/packages/?name=openssl) [lib32-openssl](https://www.archlinux.org/packages/?name=lib32-openssl)</td>

<td>2015-12-03</td>

<td><= 1.0.2.d-1</td>

<td>1.0.2.e-1</td>

<td><3d</td>

<td>Fixed</td>

<td>[ASA-201512-2](https://lists.archlinux.org/pipermail/arch-security/2015-December/000459.html)</td>

</tr>

<tr>

<td>[CVE-2015-6764](https://access.redhat.com/security/cve/CVE-2015-6764) [CVE-2015-6765](https://access.redhat.com/security/cve/CVE-2015-6765) [CVE-2015-6766](https://access.redhat.com/security/cve/CVE-2015-6766) [CVE-2015-6767](https://access.redhat.com/security/cve/CVE-2015-6767) [CVE-2015-6768](https://access.redhat.com/security/cve/CVE-2015-6768) [CVE-2015-6769](https://access.redhat.com/security/cve/CVE-2015-6769) [CVE-2015-6770](https://access.redhat.com/security/cve/CVE-2015-6770) [CVE-2015-6771](https://access.redhat.com/security/cve/CVE-2015-6771) [CVE-2015-6772](https://access.redhat.com/security/cve/CVE-2015-6772) [CVE-2015-6773](https://access.redhat.com/security/cve/CVE-2015-6773) [CVE-2015-6774](https://access.redhat.com/security/cve/CVE-2015-6774) [CVE-2015-6775](https://access.redhat.com/security/cve/CVE-2015-6775) [CVE-2015-6776](https://access.redhat.com/security/cve/CVE-2015-6776) [CVE-2015-6777](https://access.redhat.com/security/cve/CVE-2015-6777) [CVE-2015-6778](https://access.redhat.com/security/cve/CVE-2015-6778) [CVE-2015-6779](https://access.redhat.com/security/cve/CVE-2015-6779) [CVE-2015-6780](https://access.redhat.com/security/cve/CVE-2015-6780) [CVE-2015-6781](https://access.redhat.com/security/cve/CVE-2015-6781) [CVE-2015-6782](https://access.redhat.com/security/cve/CVE-2015-6782) [CVE-2015-6783](https://access.redhat.com/security/cve/CVE-2015-6783) [CVE-2015-6784](https://access.redhat.com/security/cve/CVE-2015-6784) [CVE-2015-6785](https://access.redhat.com/security/cve/CVE-2015-6785) [CVE-2015-6786](https://access.redhat.com/security/cve/CVE-2015-6786) [CVE-2015-6787](https://access.redhat.com/security/cve/CVE-2015-6787) [[19]](http://googlechromereleases.blogspot.fr/2015/12/stable-channel-update.html)</td>

<td>[chromium](https://www.archlinux.org/packages/?name=chromium)</td>

<td>2015-12-01</td>

<td><= 46.0.2490.86-1</td>

<td>47.0.2526.73-1</td>

<td><1d</td>

<td>Fixed</td>

<td>[ASA-201512-1](https://lists.archlinux.org/pipermail/arch-security/2015-December/000440.html)</td>

</tr>

<tr>

<td>[CVE-2015-6764](https://access.redhat.com/security/cve/CVE-2015-6764) [CVE-2015-8027](https://access.redhat.com/security/cve/CVE-2015-8027) [[20]](https://nodejs.org/en/blog/vulnerability/cve-2015-8027_cve-2015-6764/)</td>

<td>[nodejs](https://www.archlinux.org/packages/?name=nodejs)</td>

<td>2015-11-25</td>

<td><= 5.1.0-1</td>

<td>5.1.1-1</td>

<td>8d</td>

<td>Fixed</td>

<td>[ASA-201512-4](https://lists.archlinux.org/pipermail/arch-security/2015-December/000462.html)</td>

</tr>

<tr>

<td>[CVE-2015-8213](https://access.redhat.com/security/cve/CVE-2015-8213) [templink](https://www.djangoproject.com/weblog/2015/nov/24/security-releases-issued/)</td>

<td>[python-django](https://www.archlinux.org/packages/?name=python-django) [python2-django](https://www.archlinux.org/packages/?name=python2-django)</td>

<td>2015-11-24</td>

<td><= 1.8.6-1</td>

<td>1.8.7-1</td>

<td>5d</td>

<td>Fixed</td>

<td>[ASA-201512-3](https://lists.archlinux.org/pipermail/arch-security/2015-December/000460.html)</td>

</tr>

<tr>

<td>[CVE-2015-1819](https://access.redhat.com/security/cve/CVE-2015-1819) [CVE-2015-5312](https://access.redhat.com/security/cve/CVE-2015-5312) [CVE-2015-7941](https://access.redhat.com/security/cve/CVE-2015-7941) [CVE-2015-7942](https://access.redhat.com/security/cve/CVE-2015-7942) [CVE-2015-7497](https://access.redhat.com/security/cve/CVE-2015-7497) [CVE-2015-7498](https://access.redhat.com/security/cve/CVE-2015-7498) [CVE-2015-7499](https://access.redhat.com/security/cve/CVE-2015-7499) [CVE-2015-7500](https://access.redhat.com/security/cve/CVE-2015-7500) [CVE-2015-8035](https://access.redhat.com/security/cve/CVE-2015-8035) [CVE-2015-8242](https://access.redhat.com/security/cve/CVE-2015-8242) [templink](https://mail.gnome.org/archives/xml/2015-November/msg00012.html)</td>

<td>[libxml2](https://www.archlinux.org/packages/?name=libxml2)</td>

<td>2015-11-20</td>

<td><= 2.9.2-2</td>

<td>2.9.3-1</td>

<td>19d</td>

<td>Fixed ([FS#47095](https://bugs.archlinux.org/task/47095))</td>

<td>[ASA-201512-6](https://lists.archlinux.org/pipermail/arch-security/2015-December/000464.html)</td>

</tr>

<tr>

<td>[CVE-2015-7981](https://access.redhat.com/security/cve/CVE-2015-7981) [CVE-2015-8126](https://access.redhat.com/security/cve/CVE-2015-8126) [templink](http://seclists.org/oss-sec/2015/q4/264) [templink](http://seclists.org/oss-sec/2015/q4/161)</td>

<td>[libpng](https://www.archlinux.org/packages/?name=libpng) [lib32-libpng](https://www.archlinux.org/packages/?name=lib32-libpng)</td>

<td>2015-11-12</td>

<td><= 1.6.18-1</td>

<td>1.6.19-1</td>

<td>5d</td>

<td>Fixed ([FS#47069](https://bugs.archlinux.org/task/47069))</td>

<td>[ASA-201511-9](https://lists.archlinux.org/pipermail/arch-security/2015-November/000437.html) [ASA-201511-10](https://lists.archlinux.org/pipermail/arch-security/2015-November/000438.html)</td>

</tr>

<tr>

<td>[CVE-2015-5309](https://access.redhat.com/security/cve/CVE-2015-5309) [templink](http://www.chiark.greenend.org.uk/~sgtatham/putty/wishlist/vuln-ech-overflow.html)</td>

<td>[putty](https://www.archlinux.org/packages/?name=putty)</td>

<td>2015-11-12</td>

<td><= 0.65-1</td>

<td>0.66-1</td>

<td>1d</td>

<td>Fixed</td>

<td>[ASA-201511-7](https://lists.archlinux.org/pipermail/arch-security/2015-November/000435.html)</td>

</tr>

<tr>

<td>[CVE-2015-7651](https://access.redhat.com/security/cve/CVE-2015-7651) [CVE-2015-7652](https://access.redhat.com/security/cve/CVE-2015-7652) [CVE-2015-7653](https://access.redhat.com/security/cve/CVE-2015-7653) [CVE-2015-7654](https://access.redhat.com/security/cve/CVE-2015-7654) [CVE-2015-7655](https://access.redhat.com/security/cve/CVE-2015-7655) [CVE-2015-7656](https://access.redhat.com/security/cve/CVE-2015-7656) [CVE-2015-7657](https://access.redhat.com/security/cve/CVE-2015-7657) [CVE-2015-7658](https://access.redhat.com/security/cve/CVE-2015-7658) [CVE-2015-7659](https://access.redhat.com/security/cve/CVE-2015-7659) [CVE-2015-7660](https://access.redhat.com/security/cve/CVE-2015-7660) [CVE-2015-7661](https://access.redhat.com/security/cve/CVE-2015-7661) [CVE-2015-7662](https://access.redhat.com/security/cve/CVE-2015-7662) [CVE-2015-7663](https://access.redhat.com/security/cve/CVE-2015-7663) [CVE-2015-8042](https://access.redhat.com/security/cve/CVE-2015-8042) [CVE-2015-8043](https://access.redhat.com/security/cve/CVE-2015-8043) [CVE-2015-8044](https://access.redhat.com/security/cve/CVE-2015-8044) [CVE-2015-8046](https://access.redhat.com/security/cve/CVE-2015-8046) [templink](https://helpx.adobe.com/security/products/flash-player/apsb15-28.html)</td>

<td>[flashplugin](https://www.archlinux.org/packages/?name=flashplugin)</td>

<td>2015-11-10</td>

<td><= 11.2.202.540-1</td>

<td>11.2.202.548-1</td>

<td>1d</td>

<td>Fixed</td>

<td>[ASA-201511-5](https://lists.archlinux.org/pipermail/arch-security/2015-November/000433.html)</td>

</tr>

<tr>

<td>[CVE-2015-1302](https://access.redhat.com/security/cve/CVE-2015-1302) [templink](http://googlechromereleases.blogspot.fr/2015/11/stable-channel-update.html)</td>

<td>[chromium](https://www.archlinux.org/packages/?name=chromium)</td>

<td>2015-11-10</td>

<td><= 46.0.2490.80-2</td>

<td>46.0.2490.86-1</td>

<td>2d</td>

<td>Fixed</td>

<td>[ASA-201511-8](https://lists.archlinux.org/pipermail/arch-security/2015-November/000436.html)</td>

</tr>

<tr>

<td>[CVE-2015-5311](https://access.redhat.com/security/cve/CVE-2015-5311) [templink](https://doc.powerdns.com/md/security/powerdns-advisory-2015-03/)</td>

<td>[powerdns](https://www.archlinux.org/packages/?name=powerdns)</td>

<td>2015-11-09</td>

<td><= 3.4.6-2</td>

<td>3.4.7-1</td>

<td>3d</td>

<td>Fixed ([FS#47014](https://bugs.archlinux.org/task/47014))</td>

<td>[ASA-201511-6](https://lists.archlinux.org/pipermail/arch-security/2015-November/000434.html)</td>

</tr>

<tr>

<td>[CVE-2015-4513](https://access.redhat.com/security/cve/CVE-2015-4513) [CVE-2015-4514](https://access.redhat.com/security/cve/CVE-2015-4514) [CVE-2015-4515](https://access.redhat.com/security/cve/CVE-2015-4515) [CVE-2015-4518](https://access.redhat.com/security/cve/CVE-2015-4518) [CVE-2015-7181](https://access.redhat.com/security/cve/CVE-2015-7181) [CVE-2015-7182](https://access.redhat.com/security/cve/CVE-2015-7182) [CVE-2015-7183](https://access.redhat.com/security/cve/CVE-2015-7183) [CVE-2015-7187](https://access.redhat.com/security/cve/CVE-2015-7187) [CVE-2015-7188](https://access.redhat.com/security/cve/CVE-2015-7188) [CVE-2015-7189](https://access.redhat.com/security/cve/CVE-2015-7189) [CVE-2015-7193](https://access.redhat.com/security/cve/CVE-2015-7193) [CVE-2015-7194](https://access.redhat.com/security/cve/CVE-2015-7194) [CVE-2015-7195](https://access.redhat.com/security/cve/CVE-2015-7195) [CVE-2015-7196](https://access.redhat.com/security/cve/CVE-2015-7196) [CVE-2015-7197](https://access.redhat.com/security/cve/CVE-2015-7197) [CVE-2015-7198](https://access.redhat.com/security/cve/CVE-2015-7198) [CVE-2015-7199](https://access.redhat.com/security/cve/CVE-2015-7199) [CVE-2015-7200](https://access.redhat.com/security/cve/CVE-2015-7200) [templink](https://www.mozilla.org/en-US/security/known-vulnerabilities/firefox/)</td>

<td>[firefox](https://www.archlinux.org/packages/?name=firefox)</td>

<td>2015-11-03</td>

<td><= 41.0.2-2</td>

<td>42.0-1</td>

<td><1d</td>

<td>Fixed</td>

<td>[ASA-201511-2](https://lists.archlinux.org/pipermail/arch-security/2015-November/000430.html)</td>

</tr>

<tr>

<td>[CVE-2015-7183](https://access.redhat.com/security/cve/CVE-2015-7183) [templink](http://www.mail-archive.com/dev-tech-crypto@lists.mozilla.org/msg12386.html)</td>

<td>[nspr](https://www.archlinux.org/packages/?name=nspr)</td>

<td>2015-11-03</td>

<td><= 4.10.9-1</td>

<td>4.10.10-1</td>

<td>1d</td>

<td>Fixed</td>

<td>[ASA-201511-4](https://lists.archlinux.org/pipermail/arch-security/2015-November/000432.html)</td>

</tr>

<tr>

<td>[CVE-2015-7181](https://access.redhat.com/security/cve/CVE-2015-7181) [CVE-2015-7182](https://access.redhat.com/security/cve/CVE-2015-7182) [templink](http://www.mail-archive.com/dev-tech-crypto@lists.mozilla.org/msg12386.html)</td>

<td>[nss](https://www.archlinux.org/packages/?name=nss)</td>

<td>2015-11-03</td>

<td><= 3.20-1</td>

<td>3.20.1-1</td>

<td>1d</td>

<td>Fixed</td>

<td>[ASA-201511-3](https://lists.archlinux.org/pipermail/arch-security/2015-November/000431.html)</td>

</tr>

<tr>

<td>[CVE-2015-7696](https://access.redhat.com/security/cve/CVE-2015-7696) [CVE-2015-7697](https://access.redhat.com/security/cve/CVE-2015-7697) [templink](http://seclists.org/oss-sec/2015/q3/512)</td>

<td>[unzip](https://www.archlinux.org/packages/?name=unzip)</td>

<td>2015-10-30</td>

<td><= 6.0-10</td>

<td>6.0-11</td>

<td>4d</td>

<td>Fixed</td>

<td>[ASA-201511-1](https://lists.archlinux.org/pipermail/arch-security/2015-November/000429.html)</td>

</tr>

<tr>

<td>[CVE-2015-8011](https://access.redhat.com/security/cve/CVE-2015-8011) [CVE-2015-8012](https://access.redhat.com/security/cve/CVE-2015-8012) [templink](http://seclists.org/oss-sec/2015/q4/198)</td>

<td>[lldpd](https://www.archlinux.org/packages/?name=lldpd)</td>

<td>2015-10-17</td>

<td><= 0.7.18-1</td>

<td>0.7.19-1</td>

<td>1d</td>

<td>Fixed</td>

<td>[ASA-201510-25](https://lists.archlinux.org/pipermail/arch-security/2015-October/000427.html)</td>

</tr>

<tr>

<td>[CVE-2015-5714](https://access.redhat.com/security/cve/CVE-2015-5714) [CVE-2015-5715](https://access.redhat.com/security/cve/CVE-2015-5715) [CVE-2015-7989](https://access.redhat.com/security/cve/CVE-2015-7989) [templink](https://codex.wordpress.org/Version_4.3.1)</td>

<td>[wordpress](https://www.archlinux.org/packages/?name=wordpress)</td>

<td>2015-10-18</td>

<td><= 4.3.0-1</td>

<td>4.3.1-1</td>

<td>11d</td>

<td>Fixed</td>

<td>[ASA-201510-24](https://lists.archlinux.org/pipermail/arch-security/2015-October/000426.html)</td>

</tr>

<tr>

<td>[CVE-2015-7873](https://access.redhat.com/security/cve/CVE-2015-7873) [templink](https://www.phpmyadmin.net/security/PMASA-2015-5/)</td>

<td>[phpmyadmin](https://www.archlinux.org/packages/?name=phpmyadmin)</td>

<td>2015-10-23</td>

<td><= 4.5.0-1</td>

<td>4.5.1-1</td>

<td>1d</td>

<td>Fixed</td>

<td>[ASA-201510-23](https://lists.archlinux.org/pipermail/arch-security/2015-October/000425.html)</td>

</tr>

<tr>

<td>[CVE-2015-7995](https://access.redhat.com/security/cve/CVE-2015-7995) [templink](https://bugzilla.redhat.com/show_bug.cgi?id=1257962)</td>

<td>[libxslt](https://www.archlinux.org/packages/?name=libxslt)</td>

<td>2015-10-27</td>

<td><= 1.1.28-3</td>

<td>**Vulnerable**</td>

</tr>

<tr>

<td>[CVE-2015-7943](https://access.redhat.com/security/cve/CVE-2015-7943) [templink](https://www.drupal.org/SA-CORE-2015-004)</td>

<td>[drupal](https://www.archlinux.org/packages/?name=drupal)</td>

<td>2015-10-21</td>

<td><= 7.40-1</td>

<td>7.41-1</td>

<td>1d</td>

<td>Fixed</td>

<td>[ASA-201510-21](https://lists.archlinux.org/pipermail/arch-security/2015-October/000423.html)</td>

</tr>

<tr>

<td>[CVE-2015-4913](https://access.redhat.com/security/cve/CVE-2015-4913) [CVE-2015-4870](https://access.redhat.com/security/cve/CVE-2015-4870) [CVE-2015-4861](https://access.redhat.com/security/cve/CVE-2015-4861) [CVE-2015-4858](https://access.redhat.com/security/cve/CVE-2015-4858) [CVE-2015-4836](https://access.redhat.com/security/cve/CVE-2015-4836) [CVE-2015-4830](https://access.redhat.com/security/cve/CVE-2015-4830) [CVE-2015-4826](https://access.redhat.com/security/cve/CVE-2015-4826) [CVE-2015-4815](https://access.redhat.com/security/cve/CVE-2015-4815) [CVE-2015-4802](https://access.redhat.com/security/cve/CVE-2015-4802) [CVE-2015-4792](https://access.redhat.com/security/cve/CVE-2015-4792)</td>

<td>[mariadb](https://www.archlinux.org/packages/?name=mariadb)</td>

<td>2015-10-22</td>

<td><= 10.0.21-3</td>

<td>10.0.22-1</td>

<td>8d</td>

<td>Fixed</td>

<td>[ASA-201510-26](https://lists.archlinux.org/pipermail/arch-security/2015-October/000428.html)</td>

</tr>

<tr>

<td>[CVE-2015-4734](https://access.redhat.com/security/cve/CVE-2015-4734) [CVE-2015-4803](https://access.redhat.com/security/cve/CVE-2015-4803) [CVE-2015-4805](https://access.redhat.com/security/cve/CVE-2015-4805) [CVE-2015-4806](https://access.redhat.com/security/cve/CVE-2015-4806) [CVE-2015-4810](https://access.redhat.com/security/cve/CVE-2015-4810) [CVE-2015-4835](https://access.redhat.com/security/cve/CVE-2015-4835) [CVE-2015-4840](https://access.redhat.com/security/cve/CVE-2015-4840) [CVE-2015-4842](https://access.redhat.com/security/cve/CVE-2015-4842) [CVE-2015-4843](https://access.redhat.com/security/cve/CVE-2015-4843) [CVE-2015-4844](https://access.redhat.com/security/cve/CVE-2015-4844) [CVE-2015-4860](https://access.redhat.com/security/cve/CVE-2015-4860) [CVE-2015-4868](https://access.redhat.com/security/cve/CVE-2015-4868) [CVE-2015-4872](https://access.redhat.com/security/cve/CVE-2015-4872) [CVE-2015-4881](https://access.redhat.com/security/cve/CVE-2015-4881) [CVE-2015-4882](https://access.redhat.com/security/cve/CVE-2015-4882) [CVE-2015-4883](https://access.redhat.com/security/cve/CVE-2015-4883) [CVE-2015-4893](https://access.redhat.com/security/cve/CVE-2015-4893) [CVE-2015-4901](https://access.redhat.com/security/cve/CVE-2015-4901) [CVE-2015-4902](https://access.redhat.com/security/cve/CVE-2015-4902) [CVE-2015-4903](https://access.redhat.com/security/cve/CVE-2015-4903) [CVE-2015-4906](https://access.redhat.com/security/cve/CVE-2015-4906) [CVE-2015-4908](https://access.redhat.com/security/cve/CVE-2015-4908) [CVE-2015-4911](https://access.redhat.com/security/cve/CVE-2015-4911) [CVE-2015-4916](https://access.redhat.com/security/cve/CVE-2015-4916)</td>

<td>[jdk8-openjdk](https://www.archlinux.org/packages/?name=jdk8-openjdk) [jre8-openjdk](https://www.archlinux.org/packages/?name=jre8-openjdk) [jre8-openjdk-headless](https://www.archlinux.org/packages/?name=jre8-openjdk-headless)</td>

<td>2015-09-22</td>

<td><= 8.u60-1</td>

<td>8.u65-1</td>

<td>1d</td>

<td>Fixed</td>

<td>[ASA-201510-18](https://lists.archlinux.org/pipermail/arch-security/2015-October/000420.html) [ASA-201510-19](https://lists.archlinux.org/pipermail/arch-security/2015-October/000421.html) [ASA-201510-20](https://lists.archlinux.org/pipermail/arch-security/2015-October/000422.html)</td>

</tr>

<tr>

<td>[CVE-2015-4734](https://access.redhat.com/security/cve/CVE-2015-4734) [CVE-2015-4803](https://access.redhat.com/security/cve/CVE-2015-4803) [CVE-2015-4805](https://access.redhat.com/security/cve/CVE-2015-4805) [CVE-2015-4806](https://access.redhat.com/security/cve/CVE-2015-4806) [CVE-2015-4810](https://access.redhat.com/security/cve/CVE-2015-4810) [CVE-2015-4835](https://access.redhat.com/security/cve/CVE-2015-4835) [CVE-2015-4840](https://access.redhat.com/security/cve/CVE-2015-4840) [CVE-2015-4842](https://access.redhat.com/security/cve/CVE-2015-4842) [CVE-2015-4843](https://access.redhat.com/security/cve/CVE-2015-4843) [CVE-2015-4844](https://access.redhat.com/security/cve/CVE-2015-4844) [CVE-2015-4860](https://access.redhat.com/security/cve/CVE-2015-4860) [CVE-2015-4871](https://access.redhat.com/security/cve/CVE-2015-4871) [CVE-2015-4872](https://access.redhat.com/security/cve/CVE-2015-4872) [CVE-2015-4881](https://access.redhat.com/security/cve/CVE-2015-4881) [CVE-2015-4882](https://access.redhat.com/security/cve/CVE-2015-4882) [CVE-2015-4883](https://access.redhat.com/security/cve/CVE-2015-4883) [CVE-2015-4893](https://access.redhat.com/security/cve/CVE-2015-4893) [CVE-2015-4902](https://access.redhat.com/security/cve/CVE-2015-4902) [CVE-2015-4903](https://access.redhat.com/security/cve/CVE-2015-4903) [CVE-2015-4911](https://access.redhat.com/security/cve/CVE-2015-4911)</td>

<td>[jdk7-openjdk](https://www.archlinux.org/packages/?name=jdk7-openjdk) [jre7-openjdk](https://www.archlinux.org/packages/?name=jre7-openjdk) [jre7-openjdk-headless](https://www.archlinux.org/packages/?name=jre7-openjdk-headless)</td>

<td>2015-09-22</td>

<td><= 7.u85_2.6.1-2</td>

<td>7.u91_2.6.2-1</td>

<td>1d</td>

<td>Fixed</td>

<td>[ASA-201510-15](https://lists.archlinux.org/pipermail/arch-security/2015-October/000417.html) [ASA-201510-16](https://lists.archlinux.org/pipermail/arch-security/2015-October/000418.html) [ASA-201510-17](https://lists.archlinux.org/pipermail/arch-security/2015-October/000419.html)</td>

</tr>

<tr>

<td>[CVE-2015-7691](https://access.redhat.com/security/cve/CVE-2015-7691) [CVE-2015-7692](https://access.redhat.com/security/cve/CVE-2015-7692) [CVE-2015-7701](https://access.redhat.com/security/cve/CVE-2015-7701) [CVE-2015-7702](https://access.redhat.com/security/cve/CVE-2015-7702) [CVE-2015-7703](https://access.redhat.com/security/cve/CVE-2015-7703) [CVE-2015-7704](https://access.redhat.com/security/cve/CVE-2015-7704) [CVE-2015-7705](https://access.redhat.com/security/cve/CVE-2015-7705) [CVE-2015-7848](https://access.redhat.com/security/cve/CVE-2015-7848) [CVE-2015-7849](https://access.redhat.com/security/cve/CVE-2015-7849) [CVE-2015-7850](https://access.redhat.com/security/cve/CVE-2015-7850) [CVE-2015-7851](https://access.redhat.com/security/cve/CVE-2015-7851) [CVE-2015-7852](https://access.redhat.com/security/cve/CVE-2015-7852) [CVE-2015-7853](https://access.redhat.com/security/cve/CVE-2015-7853) [CVE-2015-7854](https://access.redhat.com/security/cve/CVE-2015-7854) [CVE-2015-7855](https://access.redhat.com/security/cve/CVE-2015-7855) [CVE-2015-7871](https://access.redhat.com/security/cve/CVE-2015-7871) [templink](http://support.ntp.org/bin/view/Main/SecurityNotice#Recent_Vulnerabilities) [templink](http://blog.talosintel.com/2015/10/ntpd-vulnerabilities.html)</td>

<td>[ntp](https://www.archlinux.org/packages/?name=ntp)</td>

<td>2015-10-21</td>

<td><= 4.2.8.p3-1</td>

<td>4.2.8.p4-1</td>

<td>1d</td>

<td>Fixed ([FS#46826](https://bugs.archlinux.org/task/46826))</td>

<td>[ASA-201510-14](https://lists.archlinux.org/pipermail/arch-security/2015-October/000416.html)</td>

</tr>

<tr>

<td>[CVE-2015-6031](https://access.redhat.com/security/cve/CVE-2015-6031) [templink](http://talosintel.com/reports/TALOS-2015-0035/)</td>

<td>[miniupnpc](https://www.archlinux.org/packages/?name=miniupnpc)</td>

<td>2015-09-15</td>

<td><= 1.9.20150730-1</td>

<td>1.9.20151008-1</td>

<td>30d</td>

<td>Fixed</td>

<td>[ASA-201510-11](https://lists.archlinux.org/pipermail/arch-security/2015-October/000413.html)</td>

</tr>

<tr>

<td>[CVE-2015-7645](https://access.redhat.com/security/cve/CVE-2015-7645) [CVE-2015-7647](https://access.redhat.com/security/cve/CVE-2015-7647) [CVE-2015-7648](https://access.redhat.com/security/cve/CVE-2015-7648) [templink](https://helpx.adobe.com/security/products/flash-player/apsa15-05.html) [templink](https://helpx.adobe.com/security/products/flash-player/apsb15-27.html)</td>

<td>[flashplugin](https://www.archlinux.org/packages/?name=flashplugin)</td>

<td>2015-10-14</td>

<td><= 11.2.202.535-1</td>

<td>11.2.202.540-1</td>

<td>2d</td>

<td>Fixed</td>

<td>[ASA-201510-12](https://lists.archlinux.org/pipermail/arch-security/2015-October/000414.html)</td>

</tr>

<tr>

<td>[CVE-2015-7184](https://access.redhat.com/security/cve/CVE-2015-7184) [templink](https://www.mozilla.org/en-US/security/advisories/mfsa2015-115/)</td>

<td>[firefox](https://www.archlinux.org/packages/?name=firefox)</td>

<td>2015-10-15</td>

<td><= 41.0.1-1</td>

<td>41.0.2-1</td>

<td><1d</td>

<td>Fixed</td>

<td>[ASA-201510-10](https://lists.archlinux.org/pipermail/arch-security/2015-October/000412.html)</td>

</tr>

<tr>

<td>[CVE-2015-5260](https://access.redhat.com/security/cve/CVE-2015-5260) [CVE-2015-5261](https://access.redhat.com/security/cve/CVE-2015-5261) [CVE-2015-3247](https://access.redhat.com/security/cve/CVE-2015-3247) [templink](http://lists.freedesktop.org/archives/spice-devel/2015-October/022168.html) [templink](https://bugzilla.redhat.com/show_bug.cgi?id=1260822) [templink](https://bugzilla.redhat.com/show_bug.cgi?id=1261889) [templink](https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=797976;msg=21)</td>

<td>[spice](https://www.archlinux.org/packages/?name=spice)</td>

<td>2015-09-08</td>

<td><= 0.12.5-1</td>

<td>0.12.6-1</td>

<td>41d</td>

<td>Fixed ([FS#46738](https://bugs.archlinux.org/task/46738))</td>

<td>[ASA-201510-13](https://lists.archlinux.org/pipermail/arch-security/2015-October/000415.html)</td>

</tr>

<tr>

<td>[CVE-2015-6755](https://access.redhat.com/security/cve/CVE-2015-6755) [CVE-2015-6756](https://access.redhat.com/security/cve/CVE-2015-6756) [CVE-2015-6757](https://access.redhat.com/security/cve/CVE-2015-6757) [CVE-2015-6758](https://access.redhat.com/security/cve/CVE-2015-6758) [CVE-2015-6759](https://access.redhat.com/security/cve/CVE-2015-6759) [CVE-2015-6760](https://access.redhat.com/security/cve/CVE-2015-6760) [CVE-2015-6761](https://access.redhat.com/security/cve/CVE-2015-6761) [CVE-2015-6762](https://access.redhat.com/security/cve/CVE-2015-6762) [CVE-2015-6763](https://access.redhat.com/security/cve/CVE-2015-6763) [templink](http://googlechromereleases.blogspot.fr/2015/10/stable-channel-update.html)</td>

<td>[chromium](https://www.archlinux.org/packages/?name=chromium)</td>

<td>2015-10-13</td>

<td><= 45.0.2454.101-2</td>

<td>46.0.2490.71-1</td>

<td><1d</td>

<td>Fixed</td>

<td>[ASA-201510-8](https://lists.archlinux.org/pipermail/arch-security/2015-October/000410.html)</td>

</tr>

<tr>

<td>[CVE-2015-5569](https://access.redhat.com/security/cve/CVE-2015-5569) [CVE-2015-7625](https://access.redhat.com/security/cve/CVE-2015-7625) [CVE-2015-7626](https://access.redhat.com/security/cve/CVE-2015-7626) [CVE-2015-7627](https://access.redhat.com/security/cve/CVE-2015-7627) [CVE-2015-7628](https://access.redhat.com/security/cve/CVE-2015-7628) [CVE-2015-7629](https://access.redhat.com/security/cve/CVE-2015-7629) [CVE-2015-7630](https://access.redhat.com/security/cve/CVE-2015-7630) [CVE-2015-7631](https://access.redhat.com/security/cve/CVE-2015-7631) [CVE-2015-7632](https://access.redhat.com/security/cve/CVE-2015-7632) [CVE-2015-7633](https://access.redhat.com/security/cve/CVE-2015-7633) [CVE-2015-7634](https://access.redhat.com/security/cve/CVE-2015-7634) [CVE-2015-7643](https://access.redhat.com/security/cve/CVE-2015-7643) [CVE-2015-7644](https://access.redhat.com/security/cve/CVE-2015-7644) [templink](https://helpx.adobe.com/security/products/flash-player/apsb15-25.html)</td>

<td>[flashplugin](https://www.archlinux.org/packages/?name=flashplugin)</td>

<td>2015-10-13</td>

<td><= 11.2.202.521-1</td>

<td>11.2.202.535-1</td>

<td>1d</td>

<td>Fixed</td>

<td>[ASA-201510-7](https://lists.archlinux.org/pipermail/arch-security/2015-October/000409.html)</td>

</tr>

<tr>

<td>[CVE-2015-5291](https://access.redhat.com/security/cve/CVE-2015-5291) [templink](https://tls.mbed.org/tech-updates/security-advisories/mbedtls-security-advisory-2015-01)</td>

<td>[mbedtls](https://www.archlinux.org/packages/?name=mbedtls)</td>

<td>2015-10-05</td>

<td><= 2.1.1-1</td>

<td>2.1.2-1</td>

<td>10d</td>

<td>Fixed</td>

<td>[ASA-201510-9](https://lists.archlinux.org/pipermail/arch-security/2015-October/000411.html)</td>

</tr>

<tr>

<td>[CVE-2015-7384](https://access.redhat.com/security/cve/CVE-2015-7384) [templink](https://nodejs.org/en/blog/release/v4.1.2/)</td>

<td>[nodejs](https://www.archlinux.org/packages/?name=nodejs)</td>

<td>2015-10-05</td>

<td><= 4.1.1-1</td>

<td>4.1.2-1</td>

<td><1d</td>

<td>Fixed</td>

<td>[ASA-201510-3](https://lists.archlinux.org/pipermail/arch-security/2015-October/000405.html)</td>

</tr>

<tr>

<td>[CVE-2015-7687](https://access.redhat.com/security/cve/CVE-2015-7687) [templink](http://seclists.org/oss-sec/2015/q4/17) [templink](https://gitweb.gentoo.org/repo/gentoo.git/commit/?id=3f8e2fe24f3ff174d8515b82607e951e054f68f6)</td>

<td>[opensmtpd](https://www.archlinux.org/packages/?name=opensmtpd)</td>

<td>2015-10-02</td>

<td><= 5.7.1p1-1</td>

<td>5.7.3p1-1</td>

<td>6d</td>

<td>Fixed ([FS#46605](https://bugs.archlinux.org/task/46605))</td>

<td>[ASA-201510-5](https://lists.archlinux.org/pipermail/arch-security/2015-October/000407.html)</td>

</tr>

<tr>

<td>[CVE-2015-7673](https://access.redhat.com/security/cve/CVE-2015-7673) [CVE-2015-7674](https://access.redhat.com/security/cve/CVE-2015-7674) [templink](http://seclists.org/oss-sec/2015/q4/18) [templink](http://seclists.org/oss-sec/2015/q4/19)</td>

<td>[gdk-pixbuf2](https://www.archlinux.org/packages/?name=gdk-pixbuf2)</td>

<td>2015-10-01</td>

<td><= 2.31.7-1</td>

<td>2.32.1-1</td>

<td>9d</td>

<td>Fixed</td>

<td>[ASA-201510-6](https://lists.archlinux.org/pipermail/arch-security/2015-October/000408.html)</td>

</tr>

<tr>

<td>[CVE-2015-1335](https://access.redhat.com/security/cve/CVE-2015-1335) [templink](https://github.com/lxc/lxc/commit/6de26af93d3dd87c8b21a42fdf20f30fa1c1948d)</td>

<td>[lxc](https://www.archlinux.org/packages/?name=lxc)</td>

<td>2015-09-29</td>

<td><= 1:1.1.3-2</td>

<td>-</td>

<td>-</td>

<td>Rejected ([FS#46574](https://bugs.archlinux.org/task/46574))</td>

<td>None</td>

</tr>

<tr>

<td>[CVE-2015-6972](https://access.redhat.com/security/cve/CVE-2015-6972) [CVE-2015-6973](https://access.redhat.com/security/cve/CVE-2015-6973) [templink](http://hyp3rlinx.altervista.org/advisories/AS-OPENFIRE-XSS.txt) [templink](http://hyp3rlinx.altervista.org/advisories/AS-OPENFIRE-CSRF.txt)</td>

<td>[openfire](https://www.archlinux.org/packages/?name=openfire)</td>

<td>2015-09-14</td>

<td><= 3.10.2-1</td>

<td>**Vulnerable**</td>

</tr>

<tr>

<td>[CVE-2015-4499](https://access.redhat.com/security/cve/CVE-2015-4499) [templink](https://www.bugzilla.org/security/4.2.14/)</td>

<td>[bugzilla](https://www.archlinux.org/packages/?name=bugzilla)</td>

<td>2015-09-10</td>

<td><= 5.0-1</td>

<td>5.0.1-1</td>

<td>28d</td>

<td>Fixed ([FS#46573](https://bugs.archlinux.org/task/46573))</td>

<td>[ASA-201510-4](https://lists.archlinux.org/pipermail/arch-security/2015-October/000406.html)</td>

</tr>

<tr>

<td>[CVE-2015-4141](https://access.redhat.com/security/cve/CVE-2015-4141) [CVE-2015-4142](https://access.redhat.com/security/cve/CVE-2015-4142) [CVE-2015-4143](https://access.redhat.com/security/cve/CVE-2015-4143) [CVE-2015-4144](https://access.redhat.com/security/cve/CVE-2015-4144) [CVE-2015-4145](https://access.redhat.com/security/cve/CVE-2015-4145) [CVE-2015-4146](https://access.redhat.com/security/cve/CVE-2015-4146) [templink](http://w1.fi/security/2015-2/) [templink](http://w1.fi/security/2015-3/) [templink](http://w1.fi/security/2015-4/) [templink](http://w1.fi/security/2015-5/)</td>

<td>[hostapd](https://www.archlinux.org/packages/?name=hostapd)</td>

<td>2015-05-04</td>

<td><= 2.4-2</td>

<td>2.5-1</td>

<td>~150d</td>

<td>Fixed</td>

<td>[ASA-201510-2](https://lists.archlinux.org/pipermail/arch-security/2015-October/000404.html)</td>

</tr>

<tr>

<td>[CVE-2015-3239](https://access.redhat.com/security/cve/CVE-2015-3239) [templink](https://bugzilla.redhat.com/show_bug.cgi?id=1232265)</td>

<td>[libunwind](https://www.archlinux.org/packages/?name=libunwind)</td>

<td>2015-06-16</td>

<td><= 1.1-2</td>

<td>1.1-3</td>

<td>~110d</td>

<td>Fixed ([FS#46474](https://bugs.archlinux.org/task/46474))</td>

<td>[ASA-201510-1](https://lists.archlinux.org/pipermail/arch-security/2015-October/000403.html)</td>

</tr>

<tr>

<td>[CVE-2015-1303](https://access.redhat.com/security/cve/CVE-2015-1303) [CVE-2015-1304](https://access.redhat.com/security/cve/CVE-2015-1304) [templink](http://googlechromereleases.blogspot.fr/2015/09/stable-channel-update_24.html)</td>

<td>[chromium](https://www.archlinux.org/packages/?name=chromium)</td>

<td>2015-09-24</td>

<td><= 45.0.2454.99-1</td>

<td>45.0.2454.101-1</td>

<td>1d</td>

<td>Fixed</td>

<td>[ASA-201509-11](https://lists.archlinux.org/pipermail/arch-security/2015-September/000401.html)</td>

</tr>

<tr>

<td>[CVE-2015-4500](https://access.redhat.com/security/cve/CVE-2015-4500) [CVE-2015-4501](https://access.redhat.com/security/cve/CVE-2015-4501) [CVE-2015-4502](https://access.redhat.com/security/cve/CVE-2015-4502) [CVE-2015-4504](https://access.redhat.com/security/cve/CVE-2015-4504) [CVE-2015-4506](https://access.redhat.com/security/cve/CVE-2015-4506) [CVE-2015-4507](https://access.redhat.com/security/cve/CVE-2015-4507) [CVE-2015-4508](https://access.redhat.com/security/cve/CVE-2015-4508) [CVE-2015-4509](https://access.redhat.com/security/cve/CVE-2015-4509) [CVE-2015-4510](https://access.redhat.com/security/cve/CVE-2015-4510) [CVE-2015-4511](https://access.redhat.com/security/cve/CVE-2015-4511) [CVE-2015-4512](https://access.redhat.com/security/cve/CVE-2015-4512) [CVE-2015-4516](https://access.redhat.com/security/cve/CVE-2015-4516) [CVE-2015-4517](https://access.redhat.com/security/cve/CVE-2015-4517) [CVE-2015-4519](https://access.redhat.com/security/cve/CVE-2015-4519) [CVE-2015-4520](https://access.redhat.com/security/cve/CVE-2015-4520) [CVE-2015-4521](https://access.redhat.com/security/cve/CVE-2015-4521) [CVE-2015-4522](https://access.redhat.com/security/cve/CVE-2015-4522) [CVE-2015-7174](https://access.redhat.com/security/cve/CVE-2015-7174) [CVE-2015-7175](https://access.redhat.com/security/cve/CVE-2015-7175) [CVE-2015-7176](https://access.redhat.com/security/cve/CVE-2015-7176) [CVE-2015-7177](https://access.redhat.com/security/cve/CVE-2015-7177) [CVE-2015-7180](https://access.redhat.com/security/cve/CVE-2015-7180) [templink](https://www.mozilla.org/en-US/security/known-vulnerabilities/firefox/#firefox41)</td>

<td>[firefox](https://www.archlinux.org/packages/?name=firefox)</td>

<td>2015-09-22</td>

<td><= 40.0.3-1</td>

<td>41.0-1</td>

<td><1d</td>

<td>Fixed</td>

<td>[ASA-201509-9](https://lists.archlinux.org/pipermail/arch-security/2015-September/000399.html)</td>

</tr>

<tr>

<td>[CVE-2015-5567](https://access.redhat.com/security/cve/CVE-2015-5567) [CVE-2015-5568](https://access.redhat.com/security/cve/CVE-2015-5568) [CVE-2015-5570](https://access.redhat.com/security/cve/CVE-2015-5570) [CVE-2015-5571](https://access.redhat.com/security/cve/CVE-2015-5571) [CVE-2015-5572](https://access.redhat.com/security/cve/CVE-2015-5572) [CVE-2015-5573](https://access.redhat.com/security/cve/CVE-2015-5573) [CVE-2015-5574](https://access.redhat.com/security/cve/CVE-2015-5574) [CVE-2015-5575](https://access.redhat.com/security/cve/CVE-2015-5575) [CVE-2015-5576](https://access.redhat.com/security/cve/CVE-2015-5576) [CVE-2015-5577](https://access.redhat.com/security/cve/CVE-2015-5577) [CVE-2015-5578](https://access.redhat.com/security/cve/CVE-2015-5578) [CVE-2015-5579](https://access.redhat.com/security/cve/CVE-2015-5579) [CVE-2015-5580](https://access.redhat.com/security/cve/CVE-2015-5580) [CVE-2015-5581](https://access.redhat.com/security/cve/CVE-2015-5581) [CVE-2015-5582](https://access.redhat.com/security/cve/CVE-2015-5582) [CVE-2015-5584](https://access.redhat.com/security/cve/CVE-2015-5584) [CVE-2015-5587](https://access.redhat.com/security/cve/CVE-2015-5587) [CVE-2015-5588](https://access.redhat.com/security/cve/CVE-2015-5588) [CVE-2015-6676](https://access.redhat.com/security/cve/CVE-2015-6676) [CVE-2015-6677](https://access.redhat.com/security/cve/CVE-2015-6677) [CVE-2015-6678](https://access.redhat.com/security/cve/CVE-2015-6678) [CVE-2015-6679](https://access.redhat.com/security/cve/CVE-2015-6679) [CVE-2015-6682](https://access.redhat.com/security/cve/CVE-2015-6682) [templink](https://helpx.adobe.com/security/products/flash-player/apsb15-23.html)</td>

<td>[flashplugin](https://www.archlinux.org/packages/?name=flashplugin)</td>

<td>2015-09-21</td>

<td><= 11.2.202.508-1</td>

<td>11.2.202.521-1</td>

<td><1d</td>

<td>Fixed</td>

<td>[ASA-201510-8](https://lists.archlinux.org/pipermail/arch-security/2015-September/000398.html)</td>

</tr>

<tr>

<td>[CVE-2015-7236](https://access.redhat.com/security/cve/CVE-2015-7236) [templink](http://seclists.org/oss-sec/2015/q3/561)</td>

<td>[rpcbind](https://www.archlinux.org/packages/?name=rpcbind)</td>

<td>2015-09-17</td>

<td><= 0.2.3-1</td>

<td>0.2.3-2</td>

<td>7d</td>

<td>Fixed ([FS#46341](https://bugs.archlinux.org/task/46341))</td>

<td>[ASA-201509-10](https://lists.archlinux.org/pipermail/arch-security/2015-September/000400.html)</td>

</tr>

<tr>

<td>[CVE-2015-5714](https://access.redhat.com/security/cve/CVE-2015-5714) [CVE-2015-5715](https://access.redhat.com/security/cve/CVE-2015-5715) [templink](https://wordpress.org/news/2015/09/wordpress-4-3-1/)</td>

<td>[wordpress](https://www.archlinux.org/packages/?name=wordpress)</td>

<td>2015-09-15</td>

<td><= 4.3-1</td>

<td>4.3.1-1</td>

<td>5d</td>

<td>Fixed ([FS#46340](https://bugs.archlinux.org/task/46340))</td>

<td>[ASA-201510-7](https://lists.archlinux.org/pipermail/arch-security/2015-September/000397.html)</td>

</tr>

<tr>

<td>[CVE-2015-6908](https://access.redhat.com/security/cve/CVE-2015-6908) [templink](http://www.openwall.com/lists/oss-security/2015/09/11/5)</td>

<td>[openldap](https://www.archlinux.org/packages/?name=openldap)</td>

<td>2015-09-09</td>

<td><= 2.4.42-1</td>

<td>2.4.42-2</td>

<td>3d</td>

<td>Fixed ([FS#46265](https://bugs.archlinux.org/task/46265))</td>

<td>[ASA-201509-4](https://lists.archlinux.org/pipermail/arch-security/2015-September/000393.html)</td>

</tr>

<tr>

<td>[CVE-2015-5722](https://access.redhat.com/security/cve/CVE-2015-5722) [CVE-2015-5986](https://access.redhat.com/security/cve/CVE-2015-5986) [templink](https://www.isc.org/blogs/cve-2015-5986-an-incorrect-boundary-check-can-trigger-a-require-assertion-failure-in-openpgpkey_61-c/) [templink](https://www.isc.org/blogs/cve-2015-5722-parsing-malformed-keys-may-cause-bind-to-exit-due-to-a-failed-assertion-in-buffer-c/)</td>

<td>[bind](https://www.archlinux.org/packages/?name=bind)</td>

<td>2015-09-02</td>

<td><= 9.10.2.P3-1</td>

<td>9.10.2.P4-1</td>

<td><1d</td>

<td>Fixed</td>

<td>[ASA-201509-2](https://lists.archlinux.org/pipermail/arch-security/2015-September/000391.html)</td>

</tr>

<tr>

<td>[CVE-2015-5198](https://access.redhat.com/security/cve/CVE-2015-5198) [CVE-2015-5199](https://access.redhat.com/security/cve/CVE-2015-5199) [CVE-2015-5200](https://access.redhat.com/security/cve/CVE-2015-5200) [templink](http://lists.x.org/archives/xorg-announce/2015-August/002630.html)</td>

<td>[libvdpau](https://www.archlinux.org/packages/?name=libvdpau) [lib32-libvdpau](https://www.archlinux.org/packages/?name=lib32-libvdpau)</td>

<td>2015-08-31</td>

<td><= 1.1-1</td>

<td>1.1.1-1</td>

<td>13d</td>

<td>Fixed ([FS#46266](https://bugs.archlinux.org/task/46266)) ([FS#46267](https://bugs.archlinux.org/task/46267))</td>

<td>[ASA-201509-5](https://lists.archlinux.org/pipermail/arch-security/2015-September/000394.html)</td>

</tr>

<tr>

<td>[CVE-2015-1291](https://access.redhat.com/security/cve/CVE-2015-1291) [CVE-2015-1292](https://access.redhat.com/security/cve/CVE-2015-1292) [CVE-2015-1293](https://access.redhat.com/security/cve/CVE-2015-1293) [CVE-2015-1294](https://access.redhat.com/security/cve/CVE-2015-1294) [CVE-2015-1295](https://access.redhat.com/security/cve/CVE-2015-1295) [CVE-2015-1296](https://access.redhat.com/security/cve/CVE-2015-1296) [CVE-2015-1297](https://access.redhat.com/security/cve/CVE-2015-1297) [CVE-2015-1298](https://access.redhat.com/security/cve/CVE-2015-1298) [CVE-2015-1299](https://access.redhat.com/security/cve/CVE-2015-1299) [CVE-2015-1300](https://access.redhat.com/security/cve/CVE-2015-1300) [CVE-2015-1301](https://access.redhat.com/security/cve/CVE-2015-1301) [templink](http://googlechromereleases.blogspot.fr/2015/09/stable-channel-update.html)</td>

<td>[chromium](https://www.archlinux.org/packages/?name=chromium)</td>

<td>2015-09-01</td>

<td><= 44.0.2403.157-1</td>

<td>45.0.2454.85-1</td>

<td><1d</td>

<td>Fixed</td>

<td>[ASA-201509-1](https://lists.archlinux.org/pipermail/arch-security/2015-September/000390.html)</td>

</tr>

<tr>

<td>[CVE-2015-5230](https://access.redhat.com/security/cve/CVE-2015-5230) [templink](https://doc.powerdns.com/md/security/powerdns-advisory-2015-02/)</td>

<td>[powerdns](https://www.archlinux.org/packages/?name=powerdns)</td>

<td>2015-09-02</td>

<td><= 3.4.5-1</td>

<td>3.4.6-1</td>

<td>4d</td>

<td>Fixed</td>

<td>[ASA-201509-3](https://lists.archlinux.org/pipermail/arch-security/2015-September/000392.html)</td>

</tr>

<tr>

<td>[CVE-2015-5317](https://access.redhat.com/security/cve/CVE-2015-5317) [CVE-2015-5318](https://access.redhat.com/security/cve/CVE-2015-5318) [CVE-2015-5319](https://access.redhat.com/security/cve/CVE-2015-5319) [CVE-2015-5320](https://access.redhat.com/security/cve/CVE-2015-5320) [CVE-2015-5321](https://access.redhat.com/security/cve/CVE-2015-5321) [CVE-2015-5322](https://access.redhat.com/security/cve/CVE-2015-5322) [CVE-2015-5323](https://access.redhat.com/security/cve/CVE-2015-5323) [CVE-2015-5324](https://access.redhat.com/security/cve/CVE-2015-5324) [CVE-2015-5325](https://access.redhat.com/security/cve/CVE-2015-5325) [CVE-2015-5326](https://access.redhat.com/security/cve/CVE-2015-5326) [CVE-2015-8103](https://access.redhat.com/security/cve/CVE-2015-8103) [templink](https://wiki.jenkins-ci.org/display/SECURITY/Jenkins+Security+Advisory+2015-11-11) [templink](http://seclists.org/bugtraq/2015/Aug/161)</td>

<td>[jenkins](https://www.archlinux.org/packages/?name=jenkins)</td>

<td>2015-08-28</td>

<td><= 1.627-1</td>

<td>1.638-1</td>

<td>60d</td>

<td>Fixed ([FS#46268](https://bugs.archlinux.org/task/46268))</td>

<td>[ASA-201511-11](https://lists.archlinux.org/pipermail/arch-security/2015-November/000439.html)</td>

</tr>

<tr>

<td>[CVE-2015-6749](https://access.redhat.com/security/cve/CVE-2015-6749) [templink](http://seclists.org/oss-sec/2015/q3/457)</td>

<td>[vorbis-tools](https://www.archlinux.org/packages/?name=vorbis-tools)</td>

<td>2015-08-30</td>

<td><= 1.4.0-5</td>

<td>1.4.0-6</td>

<td>>60d</td>

<td>Fixed ([FS#46269](https://bugs.archlinux.org/task/46269))</td>

<td>[ASA-201510-22](https://lists.archlinux.org/pipermail/arch-security/2015-October/000424.html)</td>

</tr>

<tr>

<td>[CVE-2015-4497](https://access.redhat.com/security/cve/CVE-2015-4497) [CVE-2015-4498](https://access.redhat.com/security/cve/CVE-2015-4498) [templink](https://www.mozilla.org/en-US/security/known-vulnerabilities/firefox/#firefox40.0.3)</td>

<td>[firefox](https://www.archlinux.org/packages/?name=firefox)</td>

<td>2015-08-27</td>

<td><= 40.0.2-1</td>

<td>40.0.3-1</td>

<td><1d</td>

<td>Fixed</td>

<td>[ASA-201508-12](https://lists.archlinux.org/pipermail/arch-security/2015-August/000389.html)</td>

</tr>

<tr>

<td>[CVE-2015-5949](https://access.redhat.com/security/cve/CVE-2015-5949) [templink](http://www.ocert.org/advisories/ocert-2015-009.html)</td>

<td>[vlc](https://www.archlinux.org/packages/?name=vlc)</td>

<td>2015-08-20</td>

<td><= 2.2.1-6</td>

<td>**Vulnerable** ([FS#46037](https://bugs.archlinux.org/task/46037))</td>

</tr>

<tr>

<td>[CVE-2015-5963](https://access.redhat.com/security/cve/CVE-2015-5963) [templink](https://www.djangoproject.com/weblog/2015/aug/18/security-releases/)</td>

<td>[python-django](https://www.archlinux.org/packages/?name=python-django) [python2-django](https://www.archlinux.org/packages/?name=python2-django)</td>

<td>2015-08-18</td>

<td><= 1.8.3-1</td>

<td>1.8.4-1</td>

<td>3d</td>

<td>Fixed</td>

<td>[ASA-201508-9](https://lists.archlinux.org/pipermail/arch-security/2015-August/000386.html)</td>

</tr>

<tr>

<td>[CVE-2015-5221](https://access.redhat.com/security/cve/CVE-2015-5221) [templink](http://seclists.org/oss-sec/2015/q3/408)</td>

<td>[jasper](https://www.archlinux.org/packages/?name=jasper)</td>

<td>2015-08-16</td>

<td><= 1.900.1-14</td>

<td>**Vulnerable**</td>

</tr>

<tr>

<td>[CVE-2015-5203](https://access.redhat.com/security/cve/CVE-2015-5203) [templink](http://seclists.org/oss-sec/2015/q3/366)</td>

<td>[jasper](https://www.archlinux.org/packages/?name=jasper)</td>

<td>2015-08-16</td>

<td><= 1.900.1-13</td>

<td>1.900.1-14</td>

<td>6d</td>

<td>Fixed</td>

<td>[ASA-201508-10](https://lists.archlinux.org/pipermail/arch-security/2015-August/000387.html)</td>

</tr>

<tr>

<td>CVE Pending [templink](http://seclists.org/oss-sec/2015/q3/295)</td>

<td>[pcre](https://www.archlinux.org/packages/?name=pcre)</td>

<td>2015-08-05</td>

<td><= 8.37-2</td>

<td>8.37-3</td>

<td>12d</td>

<td>Fixed ([FS#45945](https://bugs.archlinux.org/task/45945))</td>

<td>[ASA-201508-11](https://lists.archlinux.org/pipermail/arch-security/2015-August/000388.html)</td>

</tr>

<tr>

<td>[CVE-2015-4473](https://access.redhat.com/security/cve/CVE-2015-4473) [CVE-2015-4474](https://access.redhat.com/security/cve/CVE-2015-4474) [CVE-2015-4475](https://access.redhat.com/security/cve/CVE-2015-4475) [CVE-2015-4477](https://access.redhat.com/security/cve/CVE-2015-4477) [CVE-2015-4478](https://access.redhat.com/security/cve/CVE-2015-4478) [CVE-2015-4479](https://access.redhat.com/security/cve/CVE-2015-4479) [CVE-2015-4480](https://access.redhat.com/security/cve/CVE-2015-4480) [CVE-2015-4482](https://access.redhat.com/security/cve/CVE-2015-4482) [CVE-2015-4483](https://access.redhat.com/security/cve/CVE-2015-4483) [CVE-2015-4484](https://access.redhat.com/security/cve/CVE-2015-4484) [CVE-2015-4485](https://access.redhat.com/security/cve/CVE-2015-4485) [CVE-2015-4486](https://access.redhat.com/security/cve/CVE-2015-4486) [CVE-2015-4487](https://access.redhat.com/security/cve/CVE-2015-4487) [CVE-2015-4488](https://access.redhat.com/security/cve/CVE-2015-4488) [CVE-2015-4489](https://access.redhat.com/security/cve/CVE-2015-4489) [CVE-2015-4490](https://access.redhat.com/security/cve/CVE-2015-4490) [CVE-2015-4491](https://access.redhat.com/security/cve/CVE-2015-4491) [CVE-2015-4492](https://access.redhat.com/security/cve/CVE-2015-4492) [CVE-2015-4493](https://access.redhat.com/security/cve/CVE-2015-4493) [templink](https://www.mozilla.org/en-US/security/known-vulnerabilities/firefox/#firefox40)</td>

<td>[firefox](https://www.archlinux.org/packages/?name=firefox)</td>

<td>2015-08-11</td>

<td><= 39.0.3-1</td>

<td>40.0-1</td>

<td><1d</td>

<td>Fixed</td>

<td>[ASA-201508-4](https://lists.archlinux.org/pipermail/arch-security/2015-August/000381.html)</td>

</tr>

<tr>

<td>[CVE-2014-8121](https://access.redhat.com/security/cve/CVE-2014-8121) [templink](https://access.redhat.com/security/cve/CVE-2014-8121)</td>

<td>[glibc](https://www.archlinux.org/packages/?name=glibc)</td>

<td>2015-02-23</td>

<td><= 2.21-4</td>

<td>2.22-1</td>

<td>~180d</td>

<td>Fixed</td>

<td>[ASA-201508-7](https://lists.archlinux.org/pipermail/arch-security/2015-August/000384.html)</td>

</tr>

<tr>

<td>[CVE-2015-4680](https://access.redhat.com/security/cve/CVE-2015-4680) [templink](http://www.ocert.org/advisories/ocert-2015-008.html)</td>

<td>[freeradius](https://www.archlinux.org/packages/?name=freeradius)</td>

<td>2015-06-22</td>

<td><= 3.0.8-2</td>

<td>3.0.9-1</td>

<td>~50d</td>

<td>Fixed</td>

<td>[ASA-201508-6](https://lists.archlinux.org/pipermail/arch-security/2015-August/000383.html)</td>

</tr>

<tr>

<td>[CVE-2015-3184](https://access.redhat.com/security/cve/CVE-2015-3184) [CVE-2015-3187](https://access.redhat.com/security/cve/CVE-2015-3187) [templink](https://subversion.apache.org/security/CVE-2015-3184-advisory.txt) [templink](https://subversion.apache.org/security/CVE-2015-3187-advisory.txt)</td>

<td>[subversion](https://www.archlinux.org/packages/?name=subversion)</td>

<td>2015-08-05</td>

<td><= 1.8.13-2</td>

<td>1.9.0-1</td>

<td>7d</td>

<td>Fixed</td>

<td>[ASA-201508-5](https://lists.archlinux.org/pipermail/arch-security/2015-August/000382.html)</td>

</tr>

<tr>

<td>[CVE-2015-6251](https://access.redhat.com/security/cve/CVE-2015-6251) [templink](http://www.gnutls.org/security.html#GNUTLS-SA-2015-3)</td>

<td>[gnutls](https://www.archlinux.org/packages/?name=gnutls)</td>

<td>2015-08-10</td>

<td><= 3.4.3-1</td>

<td>3.4.4.1-1</td>

<td>10d</td>

<td>Fixed</td>

<td>[ASA-201508-8](https://lists.archlinux.org/pipermail/arch-security/2015-August/000385.html)</td>

</tr>

<tr>

<td>[CVE-2015-4495](https://access.redhat.com/security/cve/CVE-2015-4495) [templink](https://www.mozilla.org/en-US/security/advisories/mfsa2015-78/)</td>

<td>[firefox](https://www.archlinux.org/packages/?name=firefox)</td>

<td>2015-08-06</td>

<td><= 39.0-1</td>

<td>39.0.3-1</td>

<td><1d</td>

<td>Fixed</td>

<td>[ASA-201508-1](https://lists.archlinux.org/pipermail/arch-security/2015-August/000378.html)</td>

</tr>

<tr>

<td>[CVE-2015-2213](https://access.redhat.com/security/cve/CVE-2015-2213) [CVE-2015-5730](https://access.redhat.com/security/cve/CVE-2015-5730) [CVE-2015-5731](https://access.redhat.com/security/cve/CVE-2015-5731) [CVE-2015-5732](https://access.redhat.com/security/cve/CVE-2015-5732) [CVE-2015-5733](https://access.redhat.com/security/cve/CVE-2015-5733) [CVE-2015-5734](https://access.redhat.com/security/cve/CVE-2015-5734) [templink](https://codex.wordpress.org/Version_4.2.4)</td>

<td>[wordpress](https://www.archlinux.org/packages/?name=wordpress)</td>

<td>2015-08-04</td>

<td><= 4.2.3-1</td>

<td>4.2.4.-1</td>

<td>2d</td>

<td>Fixed</td>

<td>[ASA-201508-2](https://lists.archlinux.org/pipermail/arch-security/2015-August/000379.html)</td>

</tr>

<tr>

<td>[CVE-2015-3245](https://access.redhat.com/security/cve/CVE-2015-3245) [CVE-2015-3246](https://access.redhat.com/security/cve/CVE-2015-3246) [templink](http://seclists.org/oss-sec/2015/q3/185)</td>

<td>[libuser](https://www.archlinux.org/packages/?name=libuser)</td>

<td>2015-07-22</td>

<td><= 0.61-1</td>

<td>0.62-1</td>

<td>2d</td>

<td>Fixed</td>

<td>[ASA-201507-19](https://lists.archlinux.org/pipermail/arch-security/2015-July/000373.html)</td>

</tr>

<tr>

<td>[CVE-2015-5600](https://access.redhat.com/security/cve/CVE-2015-5600) [templink](https://kingcope.wordpress.com/2015/07/16/openssh-keyboard-interactive-authentication-brute-force-vulnerability-maxauthtries-bypass/)</td>

<td>[openssh](https://www.archlinux.org/packages/?name=openssh)</td>

<td>2015-07-22</td>

<td><= 6.9p1-1</td>

<td>6.9p1-2</td>

<td>1d</td>

<td>Fixed</td>

<td>[ASA-201507-17](https://lists.archlinux.org/pipermail/arch-security/2015-July/000372.html)</td>

</tr>

<tr>

<td>[CVE-2015-1270](https://access.redhat.com/security/cve/CVE-2015-1270) [CVE-2015-1271](https://access.redhat.com/security/cve/CVE-2015-1271) [CVE-2015-1272](https://access.redhat.com/security/cve/CVE-2015-1272) [CVE-2015-1273](https://access.redhat.com/security/cve/CVE-2015-1273) [CVE-2015-1274](https://access.redhat.com/security/cve/CVE-2015-1274) [CVE-2015-1276](https://access.redhat.com/security/cve/CVE-2015-1276) [CVE-2015-1277](https://access.redhat.com/security/cve/CVE-2015-1277) [CVE-2015-1278](https://access.redhat.com/security/cve/CVE-2015-1278) [CVE-2015-1279](https://access.redhat.com/security/cve/CVE-2015-1279) [CVE-2015-1280](https://access.redhat.com/security/cve/CVE-2015-1280) [CVE-2015-1281](https://access.redhat.com/security/cve/CVE-2015-1281) [CVE-2015-1282](https://access.redhat.com/security/cve/CVE-2015-1282) [CVE-2015-1283](https://access.redhat.com/security/cve/CVE-2015-1283) [CVE-2015-1284](https://access.redhat.com/security/cve/CVE-2015-1284) [CVE-2015-1285](https://access.redhat.com/security/cve/CVE-2015-1285) [CVE-2015-1286](https://access.redhat.com/security/cve/CVE-2015-1286) [CVE-2015-1287](https://access.redhat.com/security/cve/CVE-2015-1287) [CVE-2015-1288](https://access.redhat.com/security/cve/CVE-2015-1288) [CVE-2015-1289](https://access.redhat.com/security/cve/CVE-2015-1289) [templink](http://googlechromereleases.blogspot.fr/2015/07/stable-channel-update_21.html)</td>

<td>[chromium](https://www.archlinux.org/packages/?name=chromium)</td>

<td>2015-07-21</td>

<td><= 43.0.2357.134-1</td>

<td>44.0.2403.89-1</td>

<td>1d</td>

<td>Fixed</td>

<td>[ASA-201507-18](https://lists.archlinux.org/pipermail/arch-security/2015-July/000371.html)</td>

</tr>

<tr>

<td>[CVE-2015-2590](https://access.redhat.com/security/cve/CVE-2015-2590) [CVE-2015-2601](https://access.redhat.com/security/cve/CVE-2015-2601) [CVE-2015-2613](https://access.redhat.com/security/cve/CVE-2015-2613) [CVE-2015-2621](https://access.redhat.com/security/cve/CVE-2015-2621) [CVE-2015-2625](https://access.redhat.com/security/cve/CVE-2015-2625) [CVE-2015-2628](https://access.redhat.com/security/cve/CVE-2015-2628) [CVE-2015-2632](https://access.redhat.com/security/cve/CVE-2015-2632) [CVE-2015-2808](https://access.redhat.com/security/cve/CVE-2015-2808) [CVE-2015-4000](https://access.redhat.com/security/cve/CVE-2015-4000) [CVE-2015-4731](https://access.redhat.com/security/cve/CVE-2015-4731) [CVE-2015-4732](https://access.redhat.com/security/cve/CVE-2015-4732) [CVE-2015-4733](https://access.redhat.com/security/cve/CVE-2015-4733) [CVE-2015-4748](https://access.redhat.com/security/cve/CVE-2015-4748) [CVE-2015-4749](https://access.redhat.com/security/cve/CVE-2015-4749) [CVE-2015-4760](https://access.redhat.com/security/cve/CVE-2015-4760) [templink](http://blog.fuseyism.com/index.php/2015/07/21/security-icedtea-2-6-1-for-openjdk-7-released/)</td>

<td>[jre7-openjdk](https://www.archlinux.org/packages/?name=jre7-openjdk)</td>

<td>2015-07-21</td>

<td><= 7.u80_2.6.0-1</td>

<td>7.u85_2.6.1-1</td>

<td><1d</td>

<td>Fixed</td>

<td>[ASA-201507-16](https://lists.archlinux.org/pipermail/arch-security/2015-July/000370.html)</td>

</tr>

<tr>

<td>[CVE-2015-5122](https://access.redhat.com/security/cve/CVE-2015-5122) [CVE-2015-5123](https://access.redhat.com/security/cve/CVE-2015-5123) [templink](https://helpx.adobe.com/security/products/flash-player/apsb15-18.html)</td>

<td>[lib32-flashplugin](https://www.archlinux.org/packages/?name=lib32-flashplugin)</td>

<td>2015-07-09</td>

<td><= 11.2.202.481-1</td>

<td>11.2.202.491-1</td>

<td>7d</td>

<td>Fixed</td>

<td>[ASA-201507-14](https://lists.archlinux.org/pipermail/arch-security/2015-July/000368.html)</td>

</tr>

<tr>

<td>[CVE-2015-5122](https://access.redhat.com/security/cve/CVE-2015-5122) [CVE-2015-5123](https://access.redhat.com/security/cve/CVE-2015-5123) [templink](https://helpx.adobe.com/security/products/flash-player/apsb15-18.html)</td>

<td>[flashplugin](https://www.archlinux.org/packages/?name=flashplugin)</td>

<td>2015-07-09</td>

<td><= 11.2.202.481-1</td>

<td>11.2.202.491-1</td>

<td>7d</td>

<td>Fixed</td>

<td>[ASA-201507-13](https://lists.archlinux.org/pipermail/arch-security/2015-July/000367.html)</td>

</tr>

<tr>

<td>[CVE-2015-0228](https://access.redhat.com/security/cve/CVE-2015-0228) [CVE-2015-0253](https://access.redhat.com/security/cve/CVE-2015-0253) [CVE-2015-3183](https://access.redhat.com/security/cve/CVE-2015-3183) [CVE-2015-3185](https://access.redhat.com/security/cve/CVE-2015-3185) [templink](http://www.apache.org/dist/httpd/CHANGES_2.4.16)</td>

<td>[apache](https://www.archlinux.org/packages/?name=apache)</td>

<td>2015-07-15</td>

<td><= 2.4.12-4</td>

<td>2.4.16-1</td>

<td>2d</td>

<td>Fixed</td>

<td>[ASA-201507-15](https://lists.archlinux.org/pipermail/arch-security/2015-July/000369.html)</td>

</tr>

<tr>

<td>[CVE-2015-2724](https://access.redhat.com/security/cve/CVE-2015-2724) [CVE-2015-2725](https://access.redhat.com/security/cve/CVE-2015-2725) [CVE-2015-2726](https://access.redhat.com/security/cve/CVE-2015-2726) [CVE-2015-2731](https://access.redhat.com/security/cve/CVE-2015-2731) [CVE-2015-2734](https://access.redhat.com/security/cve/CVE-2015-2734) [CVE-2015-2735](https://access.redhat.com/security/cve/CVE-2015-2735) [CVE-2015-2736](https://access.redhat.com/security/cve/CVE-2015-2736) [CVE-2015-2737](https://access.redhat.com/security/cve/CVE-2015-2737) [CVE-2015-2738](https://access.redhat.com/security/cve/CVE-2015-2738) [CVE-2015-2739](https://access.redhat.com/security/cve/CVE-2015-2739) [CVE-2015-2740](https://access.redhat.com/security/cve/CVE-2015-2740) [CVE-2015-2741](https://access.redhat.com/security/cve/CVE-2015-2741) [templink](https://www.mozilla.org/en-US/security/known-vulnerabilities/thunderbird/#thunderbird38.1)</td>

<td>[thunderbird](https://www.archlinux.org/packages/?name=thunderbird)</td>

<td>2015-07-09</td>

<td><= 38.0.1-1</td>

<td>38.1.0-1</td>

<td>1d</td>

<td>Fixed</td>

<td>[ASA-201507-9](https://lists.archlinux.org/pipermail/arch-security/2015-July/000363.html)</td>

</tr>

<tr>

<td>[CVE-2015-1793](https://access.redhat.com/security/cve/CVE-2015-1793) [templink](https://openssl.org/news/secadv_20150709.txt)</td>

<td>[lib32-openssl](https://www.archlinux.org/packages/?name=lib32-openssl)</td>

<td>2015-07-09</td>

<td><= 1.0.2.c-1</td>

<td>1.0.2.d-1</td>

<td><1d</td>

<td>Fixed</td>

<td>[ASA-201507-12](https://lists.archlinux.org/pipermail/arch-security/2015-July/000366.html)</td>

</tr>

<tr>

<td>[CVE-2015-1793](https://access.redhat.com/security/cve/CVE-2015-1793) [templink](https://openssl.org/news/secadv_20150709.txt)</td>

<td>[openssl](https://www.archlinux.org/packages/?name=openssl)</td>

<td>2015-07-09</td>

<td><= 1.0.2.c-1</td>

<td>1.0.2.d-1</td>

<td><1d</td>

<td>Fixed</td>

<td>[ASA-201507-8](https://lists.archlinux.org/pipermail/arch-security/2015-July/000362.html)</td>

</tr>

<tr>

<td>[CVE-2014-0578](https://access.redhat.com/security/cve/CVE-2014-0578) [CVE-2015-3114](https://access.redhat.com/security/cve/CVE-2015-3114) [CVE-2015-3115](https://access.redhat.com/security/cve/CVE-2015-3115) [CVE-2015-3116](https://access.redhat.com/security/cve/CVE-2015-3116) [CVE-2015-3117](https://access.redhat.com/security/cve/CVE-2015-3117) [CVE-2015-3118](https://access.redhat.com/security/cve/CVE-2015-3118) [CVE-2015-3119](https://access.redhat.com/security/cve/CVE-2015-3119) [CVE-2015-3120](https://access.redhat.com/security/cve/CVE-2015-3120) [CVE-2015-3121](https://access.redhat.com/security/cve/CVE-2015-3121) [CVE-2015-3122](https://access.redhat.com/security/cve/CVE-2015-3122) [CVE-2015-3123](https://access.redhat.com/security/cve/CVE-2015-3123) [CVE-2015-3124](https://access.redhat.com/security/cve/CVE-2015-3124) [CVE-2015-3125](https://access.redhat.com/security/cve/CVE-2015-3125) [CVE-2015-3126](https://access.redhat.com/security/cve/CVE-2015-3126) [CVE-2015-3127](https://access.redhat.com/security/cve/CVE-2015-3127) [CVE-2015-3128](https://access.redhat.com/security/cve/CVE-2015-3128) [CVE-2015-3129](https://access.redhat.com/security/cve/CVE-2015-3129) [CVE-2015-3130](https://access.redhat.com/security/cve/CVE-2015-3130) [CVE-2015-3131](https://access.redhat.com/security/cve/CVE-2015-3131) [CVE-2015-3132](https://access.redhat.com/security/cve/CVE-2015-3132) [CVE-2015-3133](https://access.redhat.com/security/cve/CVE-2015-3133) [CVE-2015-3134](https://access.redhat.com/security/cve/CVE-2015-3134) [CVE-2015-3135](https://access.redhat.com/security/cve/CVE-2015-3135) [CVE-2015-3136](https://access.redhat.com/security/cve/CVE-2015-3136) [CVE-2015-3137](https://access.redhat.com/security/cve/CVE-2015-3137) [CVE-2015-4428](https://access.redhat.com/security/cve/CVE-2015-4428) [CVE-2015-4429](https://access.redhat.com/security/cve/CVE-2015-4429) [CVE-2015-4430](https://access.redhat.com/security/cve/CVE-2015-4430) [CVE-2015-4431](https://access.redhat.com/security/cve/CVE-2015-4431) [CVE-2015-4432](https://access.redhat.com/security/cve/CVE-2015-4432) [CVE-2015-4433](https://access.redhat.com/security/cve/CVE-2015-4433) [CVE-2015-5116](https://access.redhat.com/security/cve/CVE-2015-5116) [CVE-2015-5117](https://access.redhat.com/security/cve/CVE-2015-5117) [CVE-2015-5118](https://access.redhat.com/security/cve/CVE-2015-5118) [CVE-2015-5119](https://access.redhat.com/security/cve/CVE-2015-5119) [templink](https://helpx.adobe.com/security/products/flash-player/apsb15-16.html) [templink](https://www.kb.cert.org/vuls/id/561288)</td>

<td>[flashplugin](https://www.archlinux.org/packages/?name=flashplugin)</td>

<td>2015-07-07</td>

<td><= 11.2.202.468-1</td>

<td>11.2.202.481-1</td>

<td><1d</td>

<td>Fixed</td>

<td>[ASA-201507-7](https://lists.archlinux.org/pipermail/arch-security/2015-July/000361.html)</td>

</tr>

<tr>

<td>[CVE-2015-4620](https://access.redhat.com/security/cve/CVE-2015-4620) [templink](https://kb.isc.org/article/AA-01267/)</td>

<td>[bind](https://www.archlinux.org/packages/?name=bind)</td>

<td>2015-07-07</td>

<td><= 9.10.2.P1-1</td>

<td>9.10.2.P2-1</td>

<td><1d</td>

<td>Fixed</td>

<td>[ASA-201507-6](https://lists.archlinux.org/pipermail/arch-security/2015-July/000360.html)</td>

</tr>

<tr>

<td>[CVE-2015-5382](https://access.redhat.com/security/cve/CVE-2015-5382) [templink](http://www.openwall.com/lists/oss-security/2015/07/07/3)</td>

<td>[roundcubemail](https://www.archlinux.org/packages/?name=roundcubemail)</td>

<td>2015-07-06</td>

<td><= 1.1.1-1</td>

<td>1.1.2-1</td>

<td><1d</td>

<td>Fixed</td>

<td>None</td>

</tr>

<tr>

<td>[CVE-2014-5355](https://access.redhat.com/security/cve/CVE-2014-5355) [CVE-2015-2694](https://access.redhat.com/security/cve/CVE-2015-2694) [templink](http://krbdev.mit.edu/rt/NoAuth/krb5-1.13/fixed-1.13.2.html)</td>

<td>[lib32-krb5](https://www.archlinux.org/packages/?name=lib32-krb5)</td>

<td>2015-05-08</td>

<td><= 1.13.1-1</td>

<td>1.13.2-1</td>

<td>63d</td>

<td>Fixed</td>

<td>[ASA-201507-11](https://lists.archlinux.org/pipermail/arch-security/2015-July/000365.html)</td>

</tr>

<tr>

<td>[CVE-2014-5355](https://access.redhat.com/security/cve/CVE-2014-5355) [CVE-2015-2694](https://access.redhat.com/security/cve/CVE-2015-2694) [templink](http://krbdev.mit.edu/rt/NoAuth/krb5-1.13/fixed-1.13.2.html)</td>

<td>[krb5](https://www.archlinux.org/packages/?name=krb5)</td>

<td>2015-05-08</td>

<td><= 1.13.1-1</td>

<td>1.13.2-1</td>

<td>63d</td>

<td>Fixed ([FS#45575](https://bugs.archlinux.org/task/45575))</td>

<td>[ASA-201507-10](https://lists.archlinux.org/pipermail/arch-security/2015-July/000364.html)</td>

</tr>

<tr>

<td>[CVE-2015-3281](https://access.redhat.com/security/cve/CVE-2015-3281) [templink](http://marc.info/?l=haproxy&m=143593901506748&w=2)</td>

<td>[haproxy](https://www.archlinux.org/packages/?name=haproxy)</td>

<td>2015-07-03</td>

<td><= 1.5.12-1</td>

<td>1.5.14-1</td>

<td><1d</td>

<td>Fixed</td>

<td>[ASA-201507-3](https://lists.archlinux.org/pipermail/arch-security/2015-July/000357.html)</td>

</tr>

<tr>

<td>[CVE-2015-2722](https://access.redhat.com/security/cve/CVE-2015-2722) [CVE-2015-2724](https://access.redhat.com/security/cve/CVE-2015-2724) [CVE-2015-2725](https://access.redhat.com/security/cve/CVE-2015-2725) [CVE-2015-2726](https://access.redhat.com/security/cve/CVE-2015-2726) [CVE-2015-2727](https://access.redhat.com/security/cve/CVE-2015-2727) [CVE-2015-2728](https://access.redhat.com/security/cve/CVE-2015-2728) [CVE-2015-2729](https://access.redhat.com/security/cve/CVE-2015-2729) [CVE-2015-2731](https://access.redhat.com/security/cve/CVE-2015-2731) [CVE-2015-2733](https://access.redhat.com/security/cve/CVE-2015-2733) [CVE-2015-2734](https://access.redhat.com/security/cve/CVE-2015-2734) [CVE-2015-2735](https://access.redhat.com/security/cve/CVE-2015-2735) [CVE-2015-2736](https://access.redhat.com/security/cve/CVE-2015-2736) [CVE-2015-2737](https://access.redhat.com/security/cve/CVE-2015-2737) [CVE-2015-2739](https://access.redhat.com/security/cve/CVE-2015-2739) [CVE-2015-2740](https://access.redhat.com/security/cve/CVE-2015-2740) [CVE-2015-2741](https://access.redhat.com/security/cve/CVE-2015-2741) [CVE-2015-2743](https://access.redhat.com/security/cve/CVE-2015-2743) [templink](https://www.mozilla.org/en-US/security/known-vulnerabilities/firefox/)</td>

<td>[firefox](https://www.archlinux.org/packages/?name=firefox)</td>

<td>2015-07-02</td>

<td><= 38.0.5</td>

<td>39.0-1</td>

<td><1d</td>

<td>Fixed</td>

<td>[ASA-201507-2](https://lists.archlinux.org/pipermail/arch-security/2015-July/000356.html)</td>

</tr>

<tr>

<td>[CVE-2015-5352](https://access.redhat.com/security/cve/CVE-2015-5352) [templink](http://www.openwall.com/lists/oss-security/2015/07/01/10)</td>

<td>[openssh](https://www.archlinux.org/packages/?name=openssh)</td>

<td>2015-06-29</td>

<td><= 6.8p1-3</td>

<td>6.9p1-1</td>

<td>5d</td>

<td>Fixed</td>

<td>[ASA-201507-4](https://lists.archlinux.org/pipermail/arch-security/2015-July/000358.html)</td>

</tr>

<tr>

<td>[CVE-2015-5146](https://access.redhat.com/security/cve/CVE-2015-5146) [templink](http://support.ntp.org/bin/view/Main/SecurityNotice#June_2015_NTP_Security_Vulnerabi)</td>

<td>[ntp](https://www.archlinux.org/packages/?name=ntp)</td>

<td>2015-06-29</td>

<td><= 4.2.8p2-1</td>

<td>4.2.8p3-1</td>

<td>8d</td>

<td>Fixed</td>

<td>[ASA-201507-5](https://lists.archlinux.org/pipermail/arch-security/2015-July/000359.html)</td>

</tr>

<tr>

<td>[CVE-2015-2141](https://access.redhat.com/security/cve/CVE-2015-2141) [templink](https://lists.ubuntu.com/archives/ubuntu-devel-discuss/2015-June/015585.html) [commit](https://github.com/weidai11/cryptopp/commit/9425e16437439e68c7d96abef922167d68fafaff)</td>

<td>[crypto++](https://www.archlinux.org/packages/?name=crypto%2B%2B)</td>

<td>2015-06-28</td>

<td><= 5.6.2-2</td>

<td>5.6.2-3</td>

<td>28d</td>

<td>Fixed ([FS#45498](https://bugs.archlinux.org/task/45498))</td>

<td>[ASA-201507-20](https://lists.archlinux.org/pipermail/arch-security/2015-July/000374.html)</td>

</tr>

<tr>

<td>[CVE-2015-5073](https://access.redhat.com/security/cve/CVE-2015-5073) [templink](https://bugs.exim.org/show_bug.cgi?id=1651) [commit](http://vcs.pcre.org/pcre?view=revision&revision=1571)</td>

<td>[pcre](https://www.archlinux.org/packages/?name=pcre)</td>

<td>2015-06-26</td>

<td><= 8.37-2</td>

<td>8.37-3</td>

<td>~52d</td>

<td>Fixed</td>

</tr>

<tr>

<td>[CVE-2015-5069](https://access.redhat.com/security/cve/CVE-2015-5069) [CVE-2015-5070](https://access.redhat.com/security/cve/CVE-2015-5070) [templink](http://www.openwall.com/lists/oss-security/2015/06/25/12)</td>

<td>[wesnoth](https://www.archlinux.org/packages/?name=wesnoth)</td>

<td>2015-06-24</td>

<td><= 1.12.2-3</td>

<td>1.12.4-1</td>

<td>< 1d</td>

<td>Fixed</td>

<td>[ASA-201507-1](https://lists.archlinux.org/pipermail/arch-security/2015-July/000355.html)</td>

</tr>

<tr>

<td>[CVE-2015-3113](https://access.redhat.com/security/cve/CVE-2015-3113) [templink](https://helpx.adobe.com/security/products/flash-player/apsb15-14.html)</td>

<td>[flashplugin](https://www.archlinux.org/packages/?name=flashplugin)</td>

<td>2015-06-23</td>

<td><= 11.2.202.466-1</td>

<td>11.2.202.468-1</td>

<td><1d</td>

<td>Fixed</td>

<td>[ASA-201506-5](https://lists.archlinux.org/pipermail/arch-security/2015-June/000346.html)</td>

</tr>

<tr>

<td>[CVE-2015-3236](https://access.redhat.com/security/cve/CVE-2015-3236) [CVE-2015-3237](https://access.redhat.com/security/cve/CVE-2015-3237) [templink](http://curl.haxx.se/docs/adv_20150617A.html) [templink](http://curl.haxx.se/docs/adv_20150617B.html)</td>

<td>[lib32-curl](https://www.archlinux.org/packages/?name=lib32-curl)</td>

<td>2015-06-17</td>

<td><= 7.42.1-1</td>

<td>7.43.0-1</td>

<td>47d</td>

<td>Fixed</td>

<td>[ASA-201506-4](https://lists.archlinux.org/pipermail/arch-security/2015-June/000345.html)</td>

</tr>

<tr>

<td>[CVE-2015-3236](https://access.redhat.com/security/cve/CVE-2015-3236) [CVE-2015-3237](https://access.redhat.com/security/cve/CVE-2015-3237) [templink](http://curl.haxx.se/docs/adv_20150617A.html) [templink](http://curl.haxx.se/docs/adv_20150617B.html)</td>

<td>[curl](https://www.archlinux.org/packages/?name=curl)</td>

<td>2015-06-17</td>

<td><= 7.42.1-1</td>

<td>7.43.0-1</td>

<td>5d</td>

<td>Fixed</td>

<td>[ASA-201506-4](https://lists.archlinux.org/pipermail/arch-security/2015-June/000345.html)</td>

</tr>

<tr>

<td>[CVE-2015-0848](https://access.redhat.com/security/cve/CVE-2015-0848) [CVE-2015-4588](https://access.redhat.com/security/cve/CVE-2015-4588) [templink](http://www.openwall.com/lists/oss-security/2015/06/16/4)</td>

<td>[libwmf](https://www.archlinux.org/packages/?name=libwmf)</td>

<td>2015-06-01</td>

<td><= 0.2.8.4-12</td>

<td>**Vulnerable**</td>

</tr>

<tr>

<td>[CVE-2015-2325](https://access.redhat.com/security/cve/CVE-2015-2325) [CVE-2015-2326](https://access.redhat.com/security/cve/CVE-2015-2326) [CVE-2015-3414](https://access.redhat.com/security/cve/CVE-2015-3414) [CVE-2015-3415](https://access.redhat.com/security/cve/CVE-2015-3415) [CVE-2015-3416](https://access.redhat.com/security/cve/CVE-2015-3416) [templink](http://php.net/ChangeLog-5.php#5.6.10)</td>

<td>[php](https://www.archlinux.org/packages/?name=php)</td>

<td>2015-06-11</td>

<td><= 5.6.9-2</td>

<td>5.6.10-1</td>

<td><1d</td>

<td>Fixed</td>

<td>None</td>

</tr>

<tr>

<td>[CVE-2015-3885](https://access.redhat.com/security/cve/CVE-2015-3885) [templink](http://www.ocert.org/advisories/ocert-2015-006.html)</td>

<td>[libraw](https://www.archlinux.org/packages/?name=libraw)</td>

<td>2015-05-11</td>

<td><= 0.16.0-3</td>

<td>0.16.1</td>

<td>5d</td>

<td>Fixed</td>

<td>None</td>

</tr>

<tr>

<td>[CVE-2015-3885](https://access.redhat.com/security/cve/CVE-2015-3885) [templink](http://www.ocert.org/advisories/ocert-2015-006.html)</td>

<td>[dcraw](https://www.archlinux.org/packages/?name=dcraw)</td>

<td>2015-05-11</td>

<td><= 9.25.0-1</td>

<td>9.26.0-1</td>

<td>~1m</td>

<td>Fixed</td>

<td>None</td>

</tr>

<tr>

<td>[CVE-2015-3885](https://access.redhat.com/security/cve/CVE-2015-3885) [templink](http://www.ocert.org/advisories/ocert-2015-006.html)</td>

<td>[gimp-ufraw](https://www.archlinux.org/packages/?name=gimp-ufraw)</td>

<td>2015-05-11</td>

<td><= 0.21-1</td>

<td>0.22-1</td>

<td>45d</td>

<td>Fixed</td>

<td>None</td>

</tr>

<tr>

<td>[CVE-2015-3885](https://access.redhat.com/security/cve/CVE-2015-3885) [templink](http://www.ocert.org/advisories/ocert-2015-006.html)</td>

<td>[rawtherapee](https://www.archlinux.org/packages/?name=rawtherapee)</td>

<td>2015-05-11</td>

<td><= 1:4.2-1</td>

<td>**Vulnerable**</td>

</tr>

<tr>

<td>[CVE-2015-3885](https://access.redhat.com/security/cve/CVE-2015-3885) [templink](http://www.ocert.org/advisories/ocert-2015-006.html)</td>

<td>[rawstudio](https://www.archlinux.org/packages/?name=rawstudio)</td>

<td>2015-05-11</td>

<td><= 2.0-12</td>

<td>**Vulnerable**</td>

</tr>

<tr>

<td>[CVE-2015-1158](https://access.redhat.com/security/cve/CVE-2015-1158) [CVE-2015-1159](https://access.redhat.com/security/cve/CVE-2015-1159) [templink](http://www.cups.org/str.php?L4609)</td>

<td>[cups](https://www.archlinux.org/packages/?name=cups)</td>

<td>2015-06-08</td>

<td><= 2.0.2-4</td>

<td>2.0.3-1</td>

<td>1d</td>

<td>Fixed ([FS#45279](https://bugs.archlinux.org/task/45279))</td>

<td>[ASA-201506-2](https://lists.archlinux.org/pipermail/arch-security/2015-June/000343.html)</td>

</tr>

<tr>

<td>[CVE-2015-1788](https://access.redhat.com/security/cve/CVE-2015-1788) [CVE-2015-1789](https://access.redhat.com/security/cve/CVE-2015-1789) [CVE-2015-1790](https://access.redhat.com/security/cve/CVE-2015-1790) [CVE-2015-1791](https://access.redhat.com/security/cve/CVE-2015-1791) [CVE-2015-1792](https://access.redhat.com/security/cve/CVE-2015-1792) [CVE-2015-4000](https://access.redhat.com/security/cve/CVE-2015-4000) [templink](https://www.openssl.org/news/secadv_20150611.txt) [templink](https://git.openssl.org/?p=openssl.git;a=commit;h=98ece4eebfb6cd45cc8d550c6ac0022965071afc)</td>

<td>[openssl](https://www.archlinux.org/packages/?name=openssl)</td>

<td>2015-06-11</td>

<td><= 1.0.2.a-1</td>

<td>1.0.2.b-1</td>

<td>1d</td>

<td>Fixed</td>

<td>[ASA-201506-3](https://lists.archlinux.org/pipermail/arch-security/2015-June/000344.html)</td>

</tr>

<tr>

<td>[CVE-2015-3210](https://access.redhat.com/security/cve/CVE-2015-3210) [templink](https://bugs.exim.org/show_bug.cgi?id=1636)</td>

<td>[pcre](https://www.archlinux.org/packages/?name=pcre)</td>

<td>2015-05-29</td>

<td><= 8.37-1</td>

<td>8.37-2</td>

<td>7d</td>

<td>Fixed ([FS#45207](https://bugs.archlinux.org/task/45207))</td>

<td>[ASA-201506-1](https://lists.archlinux.org/pipermail/arch-security/2015-June/000342.html)</td>

</tr>

<tr>

<td>[CVE-2015-3165](https://access.redhat.com/security/cve/CVE-2015-3165) [CVE-2015-3166](https://access.redhat.com/security/cve/CVE-2015-3166) [CVE-2015-3167](https://access.redhat.com/security/cve/CVE-2015-3167) [templink](http://www.postgresql.org/about/news/1587/)</td>

<td>[postgresql](https://www.archlinux.org/packages/?name=postgresql)</td>

<td>2015-05-22</td>

<td><= 9.4.1-1</td>

<td>9.4.2-1</td>

<td>4d</td>

<td>Fixed</td>

<td>[ASA-201505-17](https://lists.archlinux.org/pipermail/arch-security/2015-May/000338.html)</td>

</tr>

<tr>

<td>[CVE-2015-4054](https://access.redhat.com/security/cve/CVE-2015-4054) [templink](http://www.openwall.com/lists/oss-security/2015/05/22/5)</td>

<td>[pgbouncer](https://www.archlinux.org/packages/?name=pgbouncer)</td>

<td>2015-04-09</td>

<td><= 1.5.4-6</td>

<td>1.5.5-1</td>

<td>26d</td>

<td>Fixed</td>

<td>[ASA-201505-16](https://lists.archlinux.org/pipermail/arch-security/2015-May/000337.html)</td>

</tr>

<tr>

<td>[CVE-2015-1251](https://access.redhat.com/security/cve/CVE-2015-1251) [CVE-2015-1252](https://access.redhat.com/security/cve/CVE-2015-1252) [CVE-2015-1253](https://access.redhat.com/security/cve/CVE-2015-1253) [CVE-2015-1254](https://access.redhat.com/security/cve/CVE-2015-1254) [CVE-2015-1255](https://access.redhat.com/security/cve/CVE-2015-1255) [CVE-2015-1256](https://access.redhat.com/security/cve/CVE-2015-1256) [CVE-2015-1257](https://access.redhat.com/security/cve/CVE-2015-1257) [CVE-2015-1258](https://access.redhat.com/security/cve/CVE-2015-1258) [CVE-2015-1259](https://access.redhat.com/security/cve/CVE-2015-1259) [CVE-2015-1260](https://access.redhat.com/security/cve/CVE-2015-1260) [CVE-2015-1263](https://access.redhat.com/security/cve/CVE-2015-1263) [CVE-2015-1264](https://access.redhat.com/security/cve/CVE-2015-1264) [CVE-2015-1265](https://access.redhat.com/security/cve/CVE-2015-1265) [templink](http://googlechromereleases.blogspot.fr/2015/05/stable-channel-update_19.html)</td>

<td>[chromium](https://www.archlinux.org/packages/?name=chromium)</td>

<td>2015-05-19</td>

<td><= 42.0.2311.135-1</td>

<td>43.0.2357.65-1</td>

<td><1d</td>

<td>Fixed</td>

<td>[ASA-201505-14](https://lists.archlinux.org/pipermail/arch-security/2015-May/000335.html)</td>

</tr>

<tr>

<td>[CVE-2015-3808](https://access.redhat.com/security/cve/CVE-2015-3808) [CVE-2015-3809](https://access.redhat.com/security/cve/CVE-2015-3809) [CVE-2015-3810](https://access.redhat.com/security/cve/CVE-2015-3810) [CVE-2015-3811](https://access.redhat.com/security/cve/CVE-2015-3811) [CVE-2015-3812](https://access.redhat.com/security/cve/CVE-2015-3812) [CVE-2015-3813](https://access.redhat.com/security/cve/CVE-2015-3813) [CVE-2015-3814](https://access.redhat.com/security/cve/CVE-2015-3814) [CVE-2015-3815](https://access.redhat.com/security/cve/CVE-2015-3815) [templink](https://wireshark.org/docs/relnotes/wireshark-1.12.5.html)</td>

<td>[wireshark-cli](https://www.archlinux.org/packages/?name=wireshark-cli) [wireshark-qt](https://www.archlinux.org/packages/?name=wireshark-qt) [wireshark-gtk](https://www.archlinux.org/packages/?name=wireshark-gtk)</td>

<td>2015-05-11</td>

<td><= 1.12.4-4</td>

<td>1.12.5-1</td>

<td>1d</td>

<td>Fixed</td>

<td>[ASA-201505-10](https://lists.archlinux.org/pipermail/arch-security/2015-May/000329.html) [ASA-201505-11](https://lists.archlinux.org/pipermail/arch-security/2015-May/000330.html) [ASA-201505-12](https://lists.archlinux.org/pipermail/arch-security/2015-May/000331.html)</td>

</tr>

<tr>

<td>[CVE-2015-3456](https://access.redhat.com/security/cve/CVE-2015-3456) [templink](https://securityblog.redhat.com/2015/05/13/venom-dont-get-bitten/)</td>

<td>[qemu](https://www.archlinux.org/packages/?name=qemu)</td>

<td>2015-05-13</td>

<td><= 2.2.1-4</td>

<td>2.2.1-5</td>

<td>1d</td>

<td>Fixed ([FS#44958](https://bugs.archlinux.org/task/44958))</td>

<td>[ASA-201505-9](https://lists.archlinux.org/pipermail/arch-security/2015-May/000328.html)</td>

</tr>

<tr>

<td>[CVE-2014-0230](https://access.redhat.com/security/cve/CVE-2014-0230) [templink](https://tomcat.apache.org/security-6.html#Fixed_in_Apache_Tomcat_6.0.44)</td>

<td>[tomcat6](https://www.archlinux.org/packages/?name=tomcat6)</td>

<td>2015-04-09</td>

<td><= 6.0.43-2</td>

<td>6.0.44-1</td>

<td>34d</td>

<td>Fixed</td>

<td>[ASA-201505-8](https://lists.archlinux.org/pipermail/arch-security/2015-May/000321.html)</td>

</tr>

<tr>

<td>[CVE-2015-2708](https://access.redhat.com/security/cve/CVE-2015-2708) [CVE-2015-2709](https://access.redhat.com/security/cve/CVE-2015-2709) [CVE-2015-2710](https://access.redhat.com/security/cve/CVE-2015-2710) [CVE-2015-2713](https://access.redhat.com/security/cve/CVE-2015-2713) [CVE-2015-2716](https://access.redhat.com/security/cve/CVE-2015-2716) [templink](https://www.mozilla.org/en-US/security/known-vulnerabilities/thunderbird/#thunderbird31.7)</td>

<td>[thunderbird](https://www.archlinux.org/packages/?name=thunderbird)</td>

<td>2015-05-12</td>

<td><= 31.6.0-2</td>

<td>31.7.0-1</td>

<td>4d</td>

<td>Fixed</td>

<td>[ASA-201505-13](https://lists.archlinux.org/pipermail/arch-security/2015-May/000332.html)</td>

</tr>

<tr>

<td>[CVE-2015-2708](https://access.redhat.com/security/cve/CVE-2015-2708) [CVE-2015-2709](https://access.redhat.com/security/cve/CVE-2015-2709) [CVE-2015-2710](https://access.redhat.com/security/cve/CVE-2015-2710) [CVE-2015-2711](https://access.redhat.com/security/cve/CVE-2015-2711) [CVE-2015-2712](https://access.redhat.com/security/cve/CVE-2015-2712) [CVE-2015-2713](https://access.redhat.com/security/cve/CVE-2015-2713) [CVE-2015-2715](https://access.redhat.com/security/cve/CVE-2015-2715) [CVE-2015-2716](https://access.redhat.com/security/cve/CVE-2015-2716) [CVE-2015-2717](https://access.redhat.com/security/cve/CVE-2015-2717) [CVE-2015-2718](https://access.redhat.com/security/cve/CVE-2015-2718) [templink](https://www.mozilla.org/en-US/security/known-vulnerabilities/firefox/#firefox38)</td>

<td>[firefox](https://www.archlinux.org/packages/?name=firefox)</td>

<td>2015-05-12</td>

<td><= 37.0.2-1</td>

<td>38.0-1</td>

<td><1d</td>

<td>Fixed</td>

<td>[ASA-201505-7](https://lists.archlinux.org/pipermail/arch-security/2015-May/000320.html)</td>

</tr>

<tr>

<td>[CVE-2015-3622](https://access.redhat.com/security/cve/CVE-2015-3622) [templink](http://git.savannah.gnu.org/gitweb/?p=libtasn1.git;a=commitdiff;h=f979435)</td>

<td>[libtasn1](https://www.archlinux.org/packages/?name=libtasn1)</td>

<td>2015-04-20</td>

<td><= 4.5-1</td>

<td>4.4-1</td>

<td>16d</td>

<td>Fixed</td>

<td>[ASA-201505-5](https://lists.archlinux.org/pipermail/arch-security/2015-May/000318.html)</td>

</tr>

<tr>

<td>[CVE-2014-8964](https://access.redhat.com/security/cve/CVE-2014-8964) [templink](https://mariadb.com/kb/en/mariadb/mariadb-10018-release-notes/)</td>

<td>[mariadb-clients](https://www.archlinux.org/packages/?name=mariadb-clients)</td>

<td>2015-05-07</td>

<td><= 10.0.17-1</td>

<td>10.0.18-1</td>

<td>1d</td>

<td>Fixed</td>

<td>[ASA-201505-4](https://lists.archlinux.org/pipermail/arch-security/2015-May/000317.html)</td>

</tr>

<tr>

<td>[CVE-2014-8964](https://access.redhat.com/security/cve/CVE-2014-8964) [CVE-2015-0499](https://access.redhat.com/security/cve/CVE-2015-0499) [CVE-2015-0501](https://access.redhat.com/security/cve/CVE-2015-0501) [CVE-2015-0505](https://access.redhat.com/security/cve/CVE-2015-0505) [CVE-2015-2571](https://access.redhat.com/security/cve/CVE-2015-2571) [templink](https://mariadb.com/kb/en/mariadb/mariadb-10018-release-notes/)</td>

<td>[mariadb](https://www.archlinux.org/packages/?name=mariadb)</td>

<td>2015-05-07</td>

<td><= 10.0.17-1</td>

<td>10.0.18-1</td>

<td>1d</td>

<td>Fixed</td>

<td>[ASA-201505-3](https://lists.archlinux.org/pipermail/arch-security/2015-May/000316.html)</td>

</tr>

<tr>

<td>[CVE-2015-3627](https://access.redhat.com/security/cve/CVE-2015-3627) [CVE-2015-3629](https://access.redhat.com/security/cve/CVE-2015-3629) [CVE-2015-3630](https://access.redhat.com/security/cve/CVE-2015-3630) [CVE-2015-3631](https://access.redhat.com/security/cve/CVE-2015-3631) [templink](http://seclists.org/oss-sec/2015/q2/389)</td>

<td>[docker](https://www.archlinux.org/packages/?name=docker)</td>

<td>2015-05-07</td>

<td><= 1:1.6.0-1</td>

<td>1:1.6.1-1</td>

<td>1d</td>

<td>Fixed</td>

<td>[ASA-201505-6](https://lists.archlinux.org/pipermail/arch-security/2015-May/000319.html)</td>

</tr>

<tr>

<td>[CVE-2015-0847](https://access.redhat.com/security/cve/CVE-2015-0847) [templink](http://sourceforge.net/p/nbd/mailman/message/34091218/)</td>

<td>[nbd](https://www.archlinux.org/packages/?name=nbd)</td>

<td>2015-05-07</td>

<td><= 3.10-1</td>

<td>3.11-1</td>

<td>19d</td>

<td>Fixed</td>

<td>[ASA-201505-15](https://lists.archlinux.org/pipermail/arch-security/2015-May/000336.html)</td>

</tr>

<tr>

<td>[CVE-2015-1858](https://access.redhat.com/security/cve/CVE-2015-1858) [CVE-2015-1859](https://access.redhat.com/security/cve/CVE-2015-1859) [CVE-2015-1860](https://access.redhat.com/security/cve/CVE-2015-1860) [templink](http://lists.qt-project.org/pipermail/announce/2015-April/000067.html)</td>

<td>[qt5-base](https://www.archlinux.org/packages/?name=qt5-base)</td>

<td>2015-04-13</td>

<td><= 5.4.1-5</td>

<td>5.4.2-1</td>

<td>50d</td>

<td>Fixed</td>

<td>None</td>

</tr>

<tr>

<td>[CVE-2015-1858](https://access.redhat.com/security/cve/CVE-2015-1858) [CVE-2015-1859](https://access.redhat.com/security/cve/CVE-2015-1859) [CVE-2015-1860](https://access.redhat.com/security/cve/CVE-2015-1860) [templink](http://lists.qt-project.org/pipermail/announce/2015-April/000067.html)</td>

<td>[qt4](https://www.archlinux.org/packages/?name=qt4)</td>

<td>2015-04-13</td>

<td><= 4.8.6-6</td>

<td>4.8.7-1</td>

<td>50d</td>

<td>Fixed</td>

<td>None</td>

</tr>

<tr>

<td>[CVE-2015-3414](https://access.redhat.com/security/cve/CVE-2015-3414) [CVE-2015-3415](https://access.redhat.com/security/cve/CVE-2015-3415) [CVE-2015-3416](https://access.redhat.com/security/cve/CVE-2015-3416) [templink](http://seclists.org/fulldisclosure/2015/Apr/31)</td>

<td>[sqlite](https://www.archlinux.org/packages/?name=sqlite)</td>

<td>2015-04-24</td>

<td><= 3.8.8.3-1</td>

<td>3.8.9-1</td>

<td><1d</td>

<td>Fixed</td>

<td>None</td>

</tr>

<tr>

<td>[CVE-2015-2170](https://access.redhat.com/security/cve/CVE-2015-2170) [CVE-2015-2221](https://access.redhat.com/security/cve/CVE-2015-2221) [CVE-2015-2222](https://access.redhat.com/security/cve/CVE-2015-2222) [CVE-2015-2305](https://access.redhat.com/security/cve/CVE-2015-2305) [CVE-2015-2668](https://access.redhat.com/security/cve/CVE-2015-2668) [templink](http://blog.clamav.net/2015/04/clamav-0987-has-been-released.html)</td>

<td>[clamav](https://www.archlinux.org/packages/?name=clamav)</td>

<td>2015-04-29</td>

<td><= 0.98.6-1</td>

<td>0.98.7-1</td>

<td>1d</td>

<td>Fixed</td>

<td>[ASA-201505-2](https://lists.archlinux.org/pipermail/arch-security/2015-May/000315.html)</td>

</tr>

<tr>

<td>[CVE-2015-3455](https://access.redhat.com/security/cve/CVE-2015-3455) [templink](http://www.openwall.com/lists/oss-security/2015/04/30/2)</td>

<td>[squid](https://www.archlinux.org/packages/?name=squid)</td>

<td>2015-04-29</td>

<td><= 3.5.3-2</td>

<td>3.5.4-1</td>

<td>2d</td>

<td>Fixed</td>

<td>[ASA-201505-1](https://lists.archlinux.org/pipermail/arch-security/2015-May/000314.html)</td>

</tr>

<tr>

<td>[CVE-2015-3451](https://access.redhat.com/security/cve/CVE-2015-3451) [templink](http://www.openwall.com/lists/oss-security/2015/04/30/1)</td>

<td>[perl-xml-libxml](https://www.archlinux.org/packages/?name=perl-xml-libxml)</td>

<td>2015-04-30</td>

<td><= 2.0118-3</td>

<td>2.0119-1</td>

<td><1d</td>

<td>Fixed</td>

<td>[ASA-201504-32](https://lists.archlinux.org/pipermail/arch-security/2015-April/000313.html)</td>

</tr>

<tr>

<td>[CVE-2015-3152](https://access.redhat.com/security/cve/CVE-2015-3152) [templink](http://www.openwall.com/lists/oss-security/2015/04/29/4)</td>

<td>[mariadb](https://www.archlinux.org/packages/?name=mariadb) [mariadb-clients](https://www.archlinux.org/packages/?name=mariadb-clients)</td>

<td>2015-04-29</td>

<td><= 10.0.17-2</td>

<td>10.0.20-1</td>

<td>52d</td>

<td>Fixed</td>

<td>None</td>

</tr>

<tr>

<td>[CVE-2015-3153](https://access.redhat.com/security/cve/CVE-2015-3153) [templink](http://curl.haxx.se/docs/adv_20150429.html)</td>

<td>[curl](https://www.archlinux.org/packages/?name=curl)</td>

<td>2015-04-29</td>

<td><= 7.42.0-1</td>

<td>7.42.1-1</td>

<td>29d</td>

<td>Fixed</td>

<td>[ASA-201505-20](https://lists.archlinux.org/pipermail/arch-security/2015-May/000341.html)</td>

</tr>

<tr>

<td>[CVE-2015-1243](https://access.redhat.com/security/cve/CVE-2015-1243) [CVE-2015-1250](https://access.redhat.com/security/cve/CVE-2015-1250) [templink](http://googlechromereleases.blogspot.fr/2015/04/stable-channel-update_28.html)</td>

<td>[chromium](https://www.archlinux.org/packages/?name=chromium)</td>

<td>2015-04-28</td>

<td><= 42.0.2311.90-1</td>

<td>42.0.2311.135-1</td>

<td><1d</td>

<td>Fixed</td>

<td>[ASA-201504-30](https://lists.archlinux.org/pipermail/arch-security/2015-April/000311.html)</td>

</tr>

<tr>

<td>[CVE-2015-3420](https://access.redhat.com/security/cve/CVE-2015-3420) [templink](http://seclists.org/oss-sec/2015/q2/288)</td>

<td>[dovecot](https://www.archlinux.org/packages/?name=dovecot)</td>

<td>2015-04-24</td>

<td><= 2.2.16-1</td>

<td>2.2.16-2</td>

<td>4d</td>

<td>Fixed ([FS#44757](https://bugs.archlinux.org/task/44757))</td>

<td>[ASA-201504-31](https://lists.archlinux.org/pipermail/arch-security/2015-April/000312.html)</td>

</tr>

<tr>

<td>[CVE-2015-1868](https://access.redhat.com/security/cve/CVE-2015-1868) [templink](https://doc.powerdns.com/md/security/powerdns-advisory-2015-01/)</td>

<td>[powerdns-recursor](https://www.archlinux.org/packages/?name=powerdns-recursor)</td>

<td>2015-04-23</td>

<td><= 3.7.1-1</td>

<td>3.7.2-1</td>

<td>1d</td>

<td>Fixed ([FS#44708](https://bugs.archlinux.org/task/44708))</td>

<td>[ASA-201504-27](https://lists.archlinux.org/pipermail/arch-security/2015-April/000308.html)</td>

</tr>

<tr>

<td>[CVE-2015-1868](https://access.redhat.com/security/cve/CVE-2015-1868) [templink](https://doc.powerdns.com/md/security/powerdns-advisory-2015-01/)</td>

<td>[powerdns](https://www.archlinux.org/packages/?name=powerdns)</td>

<td>2015-04-23</td>

<td><= 3.4.3-2</td>

<td>3.4.4-1</td>

<td>1d</td>

<td>Fixed ([FS#44708](https://bugs.archlinux.org/task/44708))</td>

<td>[ASA-201504-26](https://lists.archlinux.org/pipermail/arch-security/2015-April/000307.html)</td>

</tr>

<tr>

<td>[CVE-2015-1863](https://access.redhat.com/security/cve/CVE-2015-1863) [templink](http://w1.fi/security/2015-1/wpa_supplicant-p2p-ssid-overflow.txt)</td>

<td>[wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant)</td>

<td>2015-04-22</td>

<td><= 2.3-1</td>

<td>2.4-1 (1:2.3-1)</td>

<td>2d</td>

<td>Fixed ([FS#44695](https://bugs.archlinux.org/task/44695))</td>

<td>[ASA-201504-29](https://lists.archlinux.org/pipermail/arch-security/2015-April/000310.html)</td>

</tr>

<tr>

<td>[CVE-2015-1781](https://access.redhat.com/security/cve/CVE-2015-1781) [templink](https://sourceware.org/git/?p=glibc.git;a=commitdiff;h=2959eda9272a033863c271aff62095abd01bd4e3;hp=7bf8fb104226407b75103b95525364c4667c869f)</td>

<td>[glibc](https://www.archlinux.org/packages/?name=glibc)</td>

<td>2015-04-21</td>

<td><= 2.21-2</td>

<td>2.21-3</td>

<td>2d</td>

<td>Fixed</td>

<td>[ASA-201504-25](https://lists.archlinux.org/pipermail/arch-security/2015-April/000305.html)</td>

</tr>

<tr>

<td>[CVE-2015-3143](https://access.redhat.com/security/cve/CVE-2015-3143) [CVE-2015-3144](https://access.redhat.com/security/cve/CVE-2015-3144) [CVE-2015-3145](https://access.redhat.com/security/cve/CVE-2015-3145) [CVE-2015-3148](https://access.redhat.com/security/cve/CVE-2015-3148) [templink](http://curl.haxx.se/docs/vuln-7.41.0.html)</td>

<td>[curl](https://www.archlinux.org/packages/?name=curl)</td>

<td>2015-04-22</td>

<td><= 7.41.0-1</td>

<td>7.42.0-1</td>

<td>2d</td>

<td>Fixed</td>

<td>[ASA-201504-28](https://lists.archlinux.org/pipermail/arch-security/2015-April/000309.html)</td>

</tr>

<tr>

<td>[CVE-2015-2706](https://access.redhat.com/security/cve/CVE-2015-2706) [templink](https://www.mozilla.org/en-US/security/advisories/mfsa2015-45/)</td>

<td>[firefox](https://www.archlinux.org/packages/?name=firefox)</td>

<td>2015-04-20</td>

<td><= 37.0.1-3</td>

<td>37.0.2-1</td>

<td>1d</td>

<td>Fixed</td>

<td>[ASA-201504-24](https://lists.archlinux.org/pipermail/arch-security/2015-April/000304.html)</td>

</tr>

<tr>

<td>[CVE-2015-3138](https://access.redhat.com/security/cve/CVE-2015-3138) [templink](https://github.com/the-tcpdump-group/tcpdump/issues/446)</td>

<td>[tcpdump](https://www.archlinux.org/packages/?name=tcpdump)</td>

<td>2015-03-24</td>

<td><= 4.7.3-1</td>

<td>4.7.3-2</td>

<td>26d</td>

<td>Fixed</td>

<td>[ASA-201504-20](https://lists.archlinux.org/pipermail/arch-security/2015-April/000299.html)</td>

</tr>

<tr>

<td>[CVE-2015-0346](https://access.redhat.com/security/cve/CVE-2015-0346) [CVE-2015-0347](https://access.redhat.com/security/cve/CVE-2015-0347) [CVE-2015-0348](https://access.redhat.com/security/cve/CVE-2015-0348) [CVE-2015-0349](https://access.redhat.com/security/cve/CVE-2015-0349) [CVE-2015-0350](https://access.redhat.com/security/cve/CVE-2015-0350) [CVE-2015-0351](https://access.redhat.com/security/cve/CVE-2015-0351) [CVE-2015-0352](https://access.redhat.com/security/cve/CVE-2015-0352) [CVE-2015-0353](https://access.redhat.com/security/cve/CVE-2015-0353) [CVE-2015-0354](https://access.redhat.com/security/cve/CVE-2015-0354) [CVE-2015-0355](https://access.redhat.com/security/cve/CVE-2015-0355) [CVE-2015-0356](https://access.redhat.com/security/cve/CVE-2015-0356) [CVE-2015-0357](https://access.redhat.com/security/cve/CVE-2015-0357) [CVE-2015-0358](https://access.redhat.com/security/cve/CVE-2015-0358) [CVE-2015-0359](https://access.redhat.com/security/cve/CVE-2015-0359) [CVE-2015-0360](https://access.redhat.com/security/cve/CVE-2015-0360) [CVE-2015-3038](https://access.redhat.com/security/cve/CVE-2015-3038) [CVE-2015-3039](https://access.redhat.com/security/cve/CVE-2015-3039) [CVE-2015-3040](https://access.redhat.com/security/cve/CVE-2015-3040) [CVE-2015-3041](https://access.redhat.com/security/cve/CVE-2015-3041) [CVE-2015-3042](https://access.redhat.com/security/cve/CVE-2015-3042) [CVE-2015-3043](https://access.redhat.com/security/cve/CVE-2015-3043) [CVE-2015-3044](https://access.redhat.com/security/cve/CVE-2015-3044) [templink](https://helpx.adobe.com/security/products/flash-player/apsb15-06.html)</td>

<td>[flashplugin](https://www.archlinux.org/packages/?name=flashplugin)</td>

<td>2015-04-14</td>

<td><= 11.2.202.451-1</td>

<td>11.2.202.457-1</td>

<td>3d</td>

<td>Fixed</td>

<td>[ASA-201504-18](https://lists.archlinux.org/pipermail/arch-security/2015-April/000297.html)</td>

</tr>

<tr>

<td>[CVE-2015-1351](https://access.redhat.com/security/cve/CVE-2015-1351) [CVE-2015-1352](https://access.redhat.com/security/cve/CVE-2015-1352) [CVE-2015-2783](https://access.redhat.com/security/cve/CVE-2015-2783) [CVE-2015-3330](https://access.redhat.com/security/cve/CVE-2015-3330) [CVE-2015-3329](https://access.redhat.com/security/cve/CVE-2015-3329) [templink](https://php.net/ChangeLog-5.php#5.6.8)</td>

<td>[php](https://www.archlinux.org/packages/?name=php)</td>

<td>2015-04-17</td>

<td><= 5.6.7.-2</td>

<td>5.6.8-1</td>

<td><1d</td>

<td>Fixed</td>

<td>[ASA-201504-14](https://lists.archlinux.org/pipermail/arch-security/2015-April/000291.html)</td>

</tr>

<tr>

<td>[CVE-2015-0460](https://access.redhat.com/security/cve/CVE-2015-0460) [CVE-2015-0469](https://access.redhat.com/security/cve/CVE-2015-0469) [CVE-2015-0470](https://access.redhat.com/security/cve/CVE-2015-0470) [CVE-2015-0477](https://access.redhat.com/security/cve/CVE-2015-0477) [CVE-2015-0478](https://access.redhat.com/security/cve/CVE-2015-0478) [CVE-2015-0480](https://access.redhat.com/security/cve/CVE-2015-0480) [CVE-2015-0488](https://access.redhat.com/security/cve/CVE-2015-0488)</td>

<td>[jdk8-openjdk](https://www.archlinux.org/packages/?name=jdk8-openjdk) [jre8-openjdk](https://www.archlinux.org/packages/?name=jre8-openjdk) [jre8-openjdk-headless](https://www.archlinux.org/packages/?name=jre8-openjdk-headless)</td>

<td>2015-04-14</td>

<td><= 8.u40-1</td>

<td>8.u45-1</td>

<td>6d</td>

<td>Fixed</td>

<td>[ASA-201504-21](https://lists.archlinux.org/pipermail/arch-security/2015-April/000300.html) [ASA-201504-22](https://lists.archlinux.org/pipermail/arch-security/2015-April/000301.html) [ASA-201504-23](https://lists.archlinux.org/pipermail/arch-security/2015-April/000302.html)</td>

</tr>

<tr>

<td>[CVE-2015-0460](https://access.redhat.com/security/cve/CVE-2015-0460) [CVE-2015-0469](https://access.redhat.com/security/cve/CVE-2015-0469) [CVE-2015-0477](https://access.redhat.com/security/cve/CVE-2015-0477) [CVE-2015-0478](https://access.redhat.com/security/cve/CVE-2015-0478) [CVE-2015-0480](https://access.redhat.com/security/cve/CVE-2015-0480) [CVE-2015-0488](https://access.redhat.com/security/cve/CVE-2015-0488) [templink](http://blog.fuseyism.com/index.php/2015/04/15/security-icedtea-2-5-5-for-openjdk-7-released/)</td>

<td>[jdk7-openjdk](https://www.archlinux.org/packages/?name=jdk7-openjdk) [jre7-openjdk](https://www.archlinux.org/packages/?name=jre7-openjdk) [jre7-openjdk-headless](https://www.archlinux.org/packages/?name=jre7-openjdk-headless)</td>

<td>2015-04-14</td>

<td><= 7.u75_2.5.4-1</td>

<td>7.u79_2.5.5-1</td>

<td>2d</td>

<td>Fixed</td>

<td>[ASA-201504-15](https://lists.archlinux.org/pipermail/arch-security/2015-April/000294.html) [ASA-201504-16](https://lists.archlinux.org/pipermail/arch-security/2015-April/000295.html) [ASA-201504-17](https://lists.archlinux.org/pipermail/arch-security/2015-April/000296.html)</td>

</tr>

<tr>

<td>[CVE-2015-3310](https://access.redhat.com/security/cve/CVE-2015-3310) [templink](http://www.openwall.com/lists/oss-security/2015/04/16/7)</td>

<td>[ppp](https://www.archlinux.org/packages/?name=ppp)</td>

<td>2015-04-13</td>

<td><= 2.4.7-1</td>

<td>2.4.7-2</td>

<td>~4m</td>

<td>Fixed ([FS#44607](https://bugs.archlinux.org/task/44607))</td>

<td>[ASA-201508-3](https://lists.archlinux.org/pipermail/arch-security/2015-August/000380.html)</td>

</tr>

<tr>

<td>[CVE-2015-3308](https://access.redhat.com/security/cve/CVE-2015-3308) [templink](http://www.openwall.com/lists/oss-security/2015/04/16/6)</td>

<td>[gnutls](https://www.archlinux.org/packages/?name=gnutls)</td>

<td>2015-03-30</td>

<td><= 3.3.13-1</td>

<td>3.3.14-1</td>

<td><1d</td>

<td>Fixed</td>

<td>None</td>

</tr>

<tr>

<td>[CVE-2015-1235](https://access.redhat.com/security/cve/CVE-2015-1235) [CVE-2015-1236](https://access.redhat.com/security/cve/CVE-2015-1236) [CVE-2015-1237](https://access.redhat.com/security/cve/CVE-2015-1237) [CVE-2015-1238](https://access.redhat.com/security/cve/CVE-2015-1238) [CVE-2015-1240](https://access.redhat.com/security/cve/CVE-2015-1240) [CVE-2015-1241](https://access.redhat.com/security/cve/CVE-2015-1241) [CVE-2015-1242](https://access.redhat.com/security/cve/CVE-2015-1242) [CVE-2015-1244](https://access.redhat.com/security/cve/CVE-2015-1244) [CVE-2015-1245](https://access.redhat.com/security/cve/CVE-2015-1245) [CVE-2015-1246](https://access.redhat.com/security/cve/CVE-2015-1246) [CVE-2015-1247](https://access.redhat.com/security/cve/CVE-2015-1247) [CVE-2015-1248](https://access.redhat.com/security/cve/CVE-2015-1248) [CVE-2015-1249](https://access.redhat.com/security/cve/CVE-2015-1249) [templink](http://googlechromereleases.blogspot.fr/2015/04/stable-channel-update_14.html)</td>

<td>[chromium](https://www.archlinux.org/packages/?name=chromium)</td>

<td>2015-04-14</td>

<td><= 41.0.2272.118-2</td>

<td>42.0.2311.90-1</td>

<td>3d</td>

<td>Fixed</td>

<td>[ASA-201504-19](https://lists.archlinux.org/pipermail/arch-security/2015-April/000298.html)</td>

</tr>

<tr>

<td>[CVE-2015-1855](https://access.redhat.com/security/cve/CVE-2015-1855) [templink](https://www.ruby-lang.org/en/news/2015/04/13/ruby-openssl-hostname-matching-vulnerability/)</td>

<td>[ruby](https://www.archlinux.org/packages/?name=ruby)</td>

<td>2015-04-13</td>

<td><= 2.2.1-1</td>

<td>2.2.2-1</td>

<td>1d</td>

<td>Fixed</td>

<td>[ASA-201504-13](https://lists.archlinux.org/pipermail/arch-security/2015-April/000282.html)</td>

</tr>

<tr>

<td>[CVE-2015-3026](https://access.redhat.com/security/cve/CVE-2015-3026) [templink](http://seclists.org/oss-sec/2015/q2/80)</td>

<td>[icecast](https://www.archlinux.org/packages/?name=icecast)</td>

<td>2015-04-08</td>

<td><= 2.4.1-1</td>

<td>2.4.2-1</td>

<td>3d</td>

<td>Fixed ([FS#44503](https://bugs.archlinux.org/task/44503))</td>

<td>[ASA-201504-12](https://lists.archlinux.org/pipermail/arch-security/2015-April/000281.html)</td>

</tr>

<tr>

<td>[CVE-2015-1798](https://access.redhat.com/security/cve/CVE-2015-1798) [templink](http://seclists.org/oss-sec/2015/q2/63)</td>

<td>[chrony](https://www.archlinux.org/packages/?name=chrony)</td>

<td>2015-04-08</td>

<td><= 1.31-2</td>

<td>1.31.1-1</td>

<td><1d</td>

<td>Fixed</td>

<td>[ASA-201504-9](https://lists.archlinux.org/pipermail/arch-security/2015-April/000278.html)</td>

</tr>

<tr>

<td>[CVE-2015-1798](https://access.redhat.com/security/cve/CVE-2015-1798) [CVE-2015-1799](https://access.redhat.com/security/cve/CVE-2015-1799) [templink](http://support.ntp.org/bin/view/Main/SecurityNotice#Recent_Vulnerabilities)</td>

<td>[ntp](https://www.archlinux.org/packages/?name=ntp)</td>

<td>2015-04-07</td>

<td><= 4.2.8p1</td>

<td>4.2.8p2-1</td>

<td><1d</td>

<td>Fixed ([FS#44492](https://bugs.archlinux.org/task/44492))</td>

<td>[ASA-201504-8](https://lists.archlinux.org/pipermail/arch-security/2015-April/000275.html)</td>

</tr>

<tr>

<td>[CVE-2015-2931](https://access.redhat.com/security/cve/CVE-2015-2931) [CVE-2015-2932](https://access.redhat.com/security/cve/CVE-2015-2932) [CVE-2015-2933](https://access.redhat.com/security/cve/CVE-2015-2933) [CVE-2015-2934](https://access.redhat.com/security/cve/CVE-2015-2934) [CVE-2015-2935](https://access.redhat.com/security/cve/CVE-2015-2935) [CVE-2015-2936](https://access.redhat.com/security/cve/CVE-2015-2936) [CVE-2015-2937](https://access.redhat.com/security/cve/CVE-2015-2937) [CVE-2015-2938](https://access.redhat.com/security/cve/CVE-2015-2938) [CVE-2015-2939](https://access.redhat.com/security/cve/CVE-2015-2939) [CVE-2015-2940](https://access.redhat.com/security/cve/CVE-2015-2940) [CVE-2015-2941](https://access.redhat.com/security/cve/CVE-2015-2941) [CVE-2015-2942](https://access.redhat.com/security/cve/CVE-2015-2942) [templink](http://seclists.org/oss-sec/2015/q2/61)</td>

<td>[mediawiki](https://www.archlinux.org/packages/?name=mediawiki)</td>

<td>2015-04-07</td>

<td><= 1.24.1-1</td>

<td>1.24.2-1</td>

<td>0d</td>

<td>Fixed ([FS#44489](https://bugs.archlinux.org/task/44489))</td>

<td>[ASA-201504-11](https://lists.archlinux.org/pipermail/arch-security/2015-April/000280.html)</td>

</tr>

<tr>

<td>[CVE-2015-2928](https://access.redhat.com/security/cve/CVE-2015-2928) [CVE-2015-2929](https://access.redhat.com/security/cve/CVE-2015-2929) [templink](http://seclists.org/oss-sec/2015/q2/56)</td>

<td>[tor](https://www.archlinux.org/packages/?name=tor)</td>

<td>2015-04-06</td>

<td><= 0.2.5.11-1</td>

<td>0.2.5.12-1</td>

<td><1d</td>

<td>Fixed ([FS#44482](https://bugs.archlinux.org/task/44482))</td>

<td>[ASA-201504-7](https://lists.archlinux.org/pipermail/arch-security/2015-April/000274.html)</td>

</tr>

<tr>

<td>[CVE-2015-0799](https://access.redhat.com/security/cve/CVE-2015-0799) [templink](https://www.mozilla.org/en-US/security/known-vulnerabilities/firefox/)</td>

<td>[firefox](https://www.archlinux.org/packages/?name=firefox)</td>

<td>2015-04-03</td>

<td><= 37.0-1</td>

<td>37.0.1-1</td>

<td><1d</td>

<td>Fixed</td>

<td>[ASA-201504-4](https://lists.archlinux.org/pipermail/arch-security/2015-April/000271.html)</td>

</tr>

<tr>

<td>[CVE-2015-1233](https://access.redhat.com/security/cve/CVE-2015-1233) [CVE-2015-1234](https://access.redhat.com/security/cve/CVE-2015-1234) [templink](http://googlechromereleases.blogspot.fr/2015/04/stable-channel-update.html)</td>

<td>[chromium](https://www.archlinux.org/packages/?name=chromium)</td>

<td>2015-04-01</td>

<td><= 41.0.2272.101-1</td>

<td>41.0.2272.118-1</td>

<td><1d</td>

<td>Fixed</td>

<td>[ASA-201504-2](https://lists.archlinux.org/pipermail/arch-security/2015-April/000269.html)</td>

</tr>

<tr>

<td>[CVE-2015-0801](https://access.redhat.com/security/cve/CVE-2015-0801) [CVE-2015-0807](https://access.redhat.com/security/cve/CVE-2015-0807) [CVE-2015-0813](https://access.redhat.com/security/cve/CVE-2015-0813) [CVE-2015-0814](https://access.redhat.com/security/cve/CVE-2015-0814) [CVE-2015-0815](https://access.redhat.com/security/cve/CVE-2015-0815) [CVE-2015-0816](https://access.redhat.com/security/cve/CVE-2015-0816) [templink](https://www.mozilla.org/en-US/security/known-vulnerabilities/thunderbird/)</td>

<td>[thunderbird](https://www.archlinux.org/packages/?name=thunderbird)</td>

<td>2015-03-31</td>

<td><= 31.5.0-1</td>

<td>31.6.0-1</td>

<td>4d</td>

<td>Fixed</td>

<td>[ASA-201504-6](https://lists.archlinux.org/pipermail/arch-security/2015-April/000272.html)</td>

</tr>

<tr>

<td>[CVE-2015-0801](https://access.redhat.com/security/cve/CVE-2015-0801) [CVE-2015-0802](https://access.redhat.com/security/cve/CVE-2015-0802) [CVE-2015-0803](https://access.redhat.com/security/cve/CVE-2015-0803) [CVE-2015-0804](https://access.redhat.com/security/cve/CVE-2015-0804) [CVE-2015-0805](https://access.redhat.com/security/cve/CVE-2015-0805) [CVE-2015-0806](https://access.redhat.com/security/cve/CVE-2015-0806) [CVE-2015-0807](https://access.redhat.com/security/cve/CVE-2015-0807) [CVE-2015-0808](https://access.redhat.com/security/cve/CVE-2015-0808) [CVE-2015-0811](https://access.redhat.com/security/cve/CVE-2015-0811) [CVE-2015-0812](https://access.redhat.com/security/cve/CVE-2015-0812) [CVE-2015-0813](https://access.redhat.com/security/cve/CVE-2015-0813) [CVE-2015-0814](https://access.redhat.com/security/cve/CVE-2015-0814) [CVE-2015-0815](https://access.redhat.com/security/cve/CVE-2015-0815) [CVE-2015-0816](https://access.redhat.com/security/cve/CVE-2015-0816) [templink](https://www.mozilla.org/en-US/security/known-vulnerabilities/firefox/)</td>

<td>[firefox](https://www.archlinux.org/packages/?name=firefox)</td>

<td>2015-03-31</td>

<td><= 36.0.4-1</td>

<td>37.0-1</td>

<td><1d</td>

<td>Fixed</td>

<td>[ASA-201504-1](https://lists.archlinux.org/pipermail/arch-security/2015-April/000268.html)</td>

</tr>

<tr>

<td>[CVE-2015-1817](https://access.redhat.com/security/cve/CVE-2015-1817) [templink](http://www.openwall.com/lists/oss-security/2015/03/30/3)</td>

<td>[musl](https://www.archlinux.org/packages/?name=musl)</td>

<td>2015-03-29</td>

<td><= 1.1.7-1</td>

<td>1.1.8-1</td>

<td>1d</td>

<td>Fixed</td>

<td>[ASA-201503-26](https://lists.archlinux.org/pipermail/arch-security/2015-March/000267.html)</td>

</tr>

<tr>

<td>[CVE-2015-2782](https://access.redhat.com/security/cve/CVE-2015-2782) [CVE-2015-0556](https://access.redhat.com/security/cve/CVE-2015-0556) [CVE-2015-0557](https://access.redhat.com/security/cve/CVE-2015-0557) [templink](http://www.openwall.com/lists/oss-security/2015/03/29/1)</td>

<td>[arj](https://www.archlinux.org/packages/?name=arj)</td>

<td>2015-03-28</td>

<td><= 3.10.22-8</td>

<td>3.10.22-10</td>

<td>10d</td>

<td>Fixed ([FS#44411](https://bugs.archlinux.org/task/44411)) ([FS#44488](https://bugs.archlinux.org/task/44488))</td>

<td>None</td>

</tr>

<tr>

<td>[CVE-2015-0250](https://access.redhat.com/security/cve/CVE-2015-0250) [templink](http://seclists.org/fulldisclosure/2015/Mar/142)</td>

<td>[java-batik](https://www.archlinux.org/packages/?name=java-batik)</td>

<td>2015-03-17</td>

<td><= 1.7-12</td>

<td>1.8-1</td>

<td>17d</td>

<td>Fixed ([FS#44410](https://bugs.archlinux.org/task/44410))</td>

<td>[ASA-201504-5](https://lists.archlinux.org/pipermail/arch-security/2015-April/000273.html)</td>

</tr>

<tr>

<td>[CVE-2015-2806](https://access.redhat.com/security/cve/CVE-2015-2806) [templink](http://git.savannah.gnu.org/gitweb/?p=libtasn1.git;a=commit;h=4d4f992826a4962790ecd0cce6fbba4a415ce149)</td>

<td>[libtasn1](https://www.archlinux.org/packages/?name=libtasn1)</td>

<td>2015-03-29</td>

<td><= 4.3-1</td>

<td>4.4-1</td>

<td>5d</td>

<td>Fixed</td>

<td>[ASA-201504-3](https://lists.archlinux.org/pipermail/arch-security/2015-April/000270.html)</td>

</tr>

<tr>

<td>[CVE-2015-0817](https://access.redhat.com/security/cve/CVE-2015-0817) [CVE-2015-0818](https://access.redhat.com/security/cve/CVE-2015-0818) [templink](https://www.mozilla.org/en-US/security/known-vulnerabilities/firefox/)</td>

<td>[firefox](https://www.archlinux.org/packages/?name=firefox)</td>

<td>2015-03-20</td>

<td><= 36.0.1-1</td>

<td>36.0.3-1</td>

<td><1d</td>

<td>Fixed</td>

<td>[ASA-201503-21](https://lists.archlinux.org/pipermail/arch-security/2015-March/000262.html)</td>

</tr>

<tr>

<td>[CVE-2015-2559](https://access.redhat.com/security/cve/CVE-2015-2559) [templink](https://www.drupal.org/SA-CORE-2015-001)</td>

<td>[drupal](https://www.archlinux.org/packages/?name=drupal)</td>

<td>2015-03-19</td>

<td><= 7.34-1</td>

<td>7.35-1</td>

<td>1d</td>

<td>Fixed</td>

<td>[ASA-201503-18](https://lists.archlinux.org/pipermail/arch-security/2015-March/000259.html)</td>

</tr>

<tr>

<td>[CVE-2015-0252](https://access.redhat.com/security/cve/CVE-2015-0252) [templink](https://xerces.apache.org/xerces-c/secadv/CVE-2015-0252.txt)</td>

<td>[xerces-c](https://www.archlinux.org/packages/?name=xerces-c)</td>

<td>2015-03-19</td>

<td><= 3.1.1-5</td>

<td>3.2.1-1</td>

<td>1d</td>

<td>Fixed ([FS#44272](https://bugs.archlinux.org/task/44272))</td>

<td>[ASA-201503-19](https://lists.archlinux.org/pipermail/arch-security/2015-March/000260.html)</td>

</tr>

<tr>

<td>[CVE-2015-2330](https://access.redhat.com/security/cve/CVE-2015-2330) [templink](http://www.openwall.com/lists/oss-security/2015/03/18/4)</td>

<td>[webkitgtk](https://www.archlinux.org/packages/?name=webkitgtk) [webkitgtk2](https://www.archlinux.org/packages/?name=webkitgtk2)</td>

<td>2015-03-17</td>

<td><= 2.4.8-1</td>

<td>2.4.9-1</td>

<td>30d</td>

<td>Fixed ([FS#44237](https://bugs.archlinux.org/task/44237))</td>

<td>[ASA-201505-18](https://lists.archlinux.org/pipermail/arch-security/2015-May/000339.html) [ASA-201505-19](https://lists.archlinux.org/pipermail/arch-security/2015-May/000340.html)</td>

</tr>

<tr>

<td>[CVE-2015-2305](https://access.redhat.com/security/cve/CVE-2015-2305) [CVE-2015-2331](https://access.redhat.com/security/cve/CVE-2015-2331) [CVE-2015-2348](https://access.redhat.com/security/cve/CVE-2015-2348) [CVE-2015-2787](https://access.redhat.com/security/cve/CVE-2015-2787) [templink](https://bugs.php.net/bug.php?id=69253)</td>

<td>[php](https://www.archlinux.org/packages/?name=php)</td>

<td>2015-03-18</td>

<td><= 5.6.6-1</td>

<td>5.6.7-1</td>

<td>10d</td>

<td>fixed ([FS#44236](https://bugs.archlinux.org/task/44236))</td>

<td>[ASA-201503-25](https://lists.archlinux.org/pipermail/arch-security/2015-March/000266.html)</td>

</tr>

<tr>

<td>[CVE-2015-0204](https://access.redhat.com/security/cve/CVE-2015-0204) [CVE-2015-0207](https://access.redhat.com/security/cve/CVE-2015-0207) [CVE-2015-0208](https://access.redhat.com/security/cve/CVE-2015-0208) [CVE-2015-0209](https://access.redhat.com/security/cve/CVE-2015-0209) [CVE-2015-0285](https://access.redhat.com/security/cve/CVE-2015-0285) [CVE-2015-0286](https://access.redhat.com/security/cve/CVE-2015-0286) [CVE-2015-0287](https://access.redhat.com/security/cve/CVE-2015-0287) [CVE-2015-0288](https://access.redhat.com/security/cve/CVE-2015-0288) [CVE-2015-0289](https://access.redhat.com/security/cve/CVE-2015-0289) [CVE-2015-0290](https://access.redhat.com/security/cve/CVE-2015-0290) [CVE-2015-0291](https://access.redhat.com/security/cve/CVE-2015-0291) [CVE-2015-0293](https://access.redhat.com/security/cve/CVE-2015-0293) [CVE-2015-1787](https://access.redhat.com/security/cve/CVE-2015-1787) [commit-0288](https://git.openssl.org/gitweb/?p=openssl.git;a=commitdiff;h=28a00bcd8e318da18031b2ac8778c64147cd54f9) [commit-0285](https://git.openssl.org/gitweb/?p=openssl.git;a=commitdiff;h=2b31fcc0b5e7329e13806822a5709dbd51c5c8a4) [commit-0209](https://git.openssl.org/gitweb/?p=openssl.git;a=commitdiff;h=ba5d0113e8bcb26857ae58a11b219aeb7bc2408a) [Debian-Bug-tracker](https://security-tracker.debian.org/tracker/CVE-2015-0288) [advisory](https://www.openssl.org/news/secadv_20150319.txt)</td>

<td>[openssl](https://www.archlinux.org/packages/?name=openssl) [lib32-openssl](https://www.archlinux.org/packages/?name=lib32-openssl)</td>

<td>2015-03-17</td>

<td><= 1.0.2-1</td>

<td>1.0.2.a-1</td>

<td>2d</td>

<td>Fixed ([FS#44227](https://bugs.archlinux.org/task/44227))</td>

<td>[ASA-201503-16](https://lists.archlinux.org/pipermail/arch-security/2015-March/000257.html) [ASA-201503-17](https://lists.archlinux.org/pipermail/arch-security/2015-March/000258.html)</td>

</tr>

<tr>

<td>[CVE-2015-1802](https://access.redhat.com/security/cve/CVE-2015-1802) [CVE-2015-1803](https://access.redhat.com/security/cve/CVE-2015-1803) [CVE-2015-1804](https://access.redhat.com/security/cve/CVE-2015-1804) [templink](http://www.openwall.com/lists/oss-security/2015/03/17/5)</td>

<td>[libxfont](https://www.archlinux.org/packages/?name=libxfont)</td>

<td>2015-03-17</td>

<td><= 1.5.0-1</td>

<td>1.5.1-1</td>

<td><1d</td>

<td>Fixed ([FS#44226](https://bugs.archlinux.org/task/44226))</td>

<td>[ASA-201503-15](https://lists.archlinux.org/pipermail/arch-security/2015-March/000256.html)</td>

</tr>

<tr>

<td>[CVE-2015-0332](https://access.redhat.com/security/cve/CVE-2015-0332) [CVE-2015-0333](https://access.redhat.com/security/cve/CVE-2015-0333) [CVE-2015-0334](https://access.redhat.com/security/cve/CVE-2015-0334) [CVE-2015-0335](https://access.redhat.com/security/cve/CVE-2015-0335) [CVE-2015-0336](https://access.redhat.com/security/cve/CVE-2015-0336) [CVE-2015-0337](https://access.redhat.com/security/cve/CVE-2015-0337) [CVE-2015-0338](https://access.redhat.com/security/cve/CVE-2015-0338) [CVE-2015-0339](https://access.redhat.com/security/cve/CVE-2015-0339) [CVE-2015-0340](https://access.redhat.com/security/cve/CVE-2015-0340) [CVE-2015-0341](https://access.redhat.com/security/cve/CVE-2015-0341) [CVE-2015-0342](https://access.redhat.com/security/cve/CVE-2015-0342) [templink](https://helpx.adobe.com/security/products/flash-player/apsb15-05.html)</td>

<td>[flashplugin](https://www.archlinux.org/packages/?name=flashplugin)</td>

<td>2015-03-12</td>

<td><= 11.2.202.442-1</td>

<td>11.2.202.451-1</td>

<td>3d</td>

<td>Fixed</td>

<td>[ASA-201503-11](https://lists.archlinux.org/pipermail/arch-security/2015-March/000252.html)</td>

</tr>

<tr>

<td>[CVE-2014-9687](https://access.redhat.com/security/cve/CVE-2014-9687) [templink](http://www.openwall.com/lists/oss-security/2015/02/10/10)</td>

<td>[ecryptfs-utils](https://www.archlinux.org/packages/?name=ecryptfs-utils)</td>

<td>2015-02-10</td>

<td><= 104-1</td>

<td>106-1</td>

<td>37d</td>

<td>Fixed ([FS#44157](https://bugs.archlinux.org/task/44157))</td>

<td>[ASA-201503-14](https://lists.archlinux.org/pipermail/arch-security/2015-March/000255.html)</td>

</tr>

<tr>

<td>[CVE-2015-1782](https://access.redhat.com/security/cve/CVE-2015-1782) [templink](http://www.libssh2.org/adv_20150311.html)</td>

<td>[libssh2](https://www.archlinux.org/packages/?name=libssh2)</td>

<td>2015-03-11</td>

<td><= 1.4.3-1</td>

<td>1.5.0-1</td>

<td>29d</td>

<td>Fixed ([FS#44146](https://bugs.archlinux.org/task/44146))</td>

<td>[ASA-201504-10](https://lists.archlinux.org/pipermail/arch-security/2015-April/000279.html)</td>

</tr>

<tr>

<td>[CVE-2015-2241](https://access.redhat.com/security/cve/CVE-2015-2241) [templink](https://www.djangoproject.com/weblog/2015/mar/09/security-releases/)</td>

<td>[python-django](https://www.archlinux.org/packages/?name=python-django) [python2-django](https://www.archlinux.org/packages/?name=python2-django)</td>

<td>2015-03-09</td>

<td><= 1.7.5-1</td>

<td>1.7.6-1</td>

<td>2d</td>

<td>Fixed ([FS#44122](https://bugs.archlinux.org/task/44122))</td>

<td>[ASA-201503-7](https://lists.archlinux.org/pipermail/arch-security/2015-March/000248.html)</td>

</tr>

<tr>

<td>[CVE-2015-1212](https://access.redhat.com/security/cve/CVE-2015-1212) [CVE-2015-1213](https://access.redhat.com/security/cve/CVE-2015-1213) [CVE-2015-1214](https://access.redhat.com/security/cve/CVE-2015-1214) [CVE-2015-1215](https://access.redhat.com/security/cve/CVE-2015-1215) [CVE-2015-1216](https://access.redhat.com/security/cve/CVE-2015-1216) [CVE-2015-1217](https://access.redhat.com/security/cve/CVE-2015-1217) [CVE-2015-1218](https://access.redhat.com/security/cve/CVE-2015-1218) [CVE-2015-1219](https://access.redhat.com/security/cve/CVE-2015-1219) [CVE-2015-1220](https://access.redhat.com/security/cve/CVE-2015-1220) [CVE-2015-1221](https://access.redhat.com/security/cve/CVE-2015-1221) [CVE-2015-1222](https://access.redhat.com/security/cve/CVE-2015-1222) [CVE-2015-1223](https://access.redhat.com/security/cve/CVE-2015-1223) [CVE-2015-1224](https://access.redhat.com/security/cve/CVE-2015-1224) [CVE-2015-1225](https://access.redhat.com/security/cve/CVE-2015-1225) [CVE-2015-1226](https://access.redhat.com/security/cve/CVE-2015-1226) [CVE-2015-1227](https://access.redhat.com/security/cve/CVE-2015-1227) [CVE-2015-1228](https://access.redhat.com/security/cve/CVE-2015-1228) [CVE-2015-1229](https://access.redhat.com/security/cve/CVE-2015-1229) [CVE-2015-1230](https://access.redhat.com/security/cve/CVE-2015-1230) [CVE-2015-1231](https://access.redhat.com/security/cve/CVE-2015-1231) [templink](http://googlechromereleases.blogspot.fr/2015/03/stable-channel-update.html)</td>

<td>[chromium](https://www.archlinux.org/packages/?name=chromium)</td>

<td>2015-03-03</td>

<td><= 40.0.2214.115-1</td>

<td>41.0.2272.76-1</td>

<td>1d</td>

<td>Fixed</td>

<td>[ASA-201503-5](https://lists.archlinux.org/pipermail/arch-security/2015-March/000245.html)</td>

</tr>

<tr>

<td>[CVE-2015-1572](https://access.redhat.com/security/cve/CVE-2015-1572) [templink](https://git.kernel.org/cgit/fs/ext2/e2fsprogs.git/commit/?id=49d0fe2a14f2a23da2fe299643379b8c1d37df73)</td>

<td>[e2fsprogs](https://www.archlinux.org/packages/?name=e2fsprogs)</td>

<td>2015-02-06</td>

<td><= 1.42.12-1</td>

<td>1.42.12-2</td>

<td>6d</td>

<td>Fixed ([FS#44015](https://bugs.archlinux.org/task/44015))</td>

<td>[ASA-201503-8](https://lists.archlinux.org/pipermail/arch-security/2015-March/000249.html)</td>

</tr>

<tr>

<td>[CVE-2015-2157](https://access.redhat.com/security/cve/CVE-2015-2157) [templink](http://www.chiark.greenend.org.uk/~sgtatham/putty/wishlist/private-key-not-wiped-2.html)</td>

<td>[putty](https://www.archlinux.org/packages/?name=putty)</td>

<td>2015-03-02</td>

<td><= 0.63-1</td>

<td>0.64-1</td>

<td><1d</td>

<td>Fixed</td>

<td>[ASA-201503-1](https://lists.archlinux.org/pipermail/arch-security/2015-March/000241.html)</td>

</tr>

<tr>

<td>[CVE-2015-0822](https://access.redhat.com/security/cve/CVE-2015-0822) [CVE-2015-0827](https://access.redhat.com/security/cve/CVE-2015-0827) [CVE-2015-0831](https://access.redhat.com/security/cve/CVE-2015-0831) [CVE-2015-0835](https://access.redhat.com/security/cve/CVE-2015-0835) [CVE-2015-0836](https://access.redhat.com/security/cve/CVE-2015-0836) [templink](https://www.mozilla.org/en-US/security/known-vulnerabilities/thunderbird/)</td>

<td>[thunderbird](https://www.archlinux.org/packages/?name=thunderbird)</td>

<td>2015-02-24</td>

<td><= 31.4.0-1</td>

<td>31.5.0-1</td>

<td><1d</td>

<td>Fixed</td>

<td>[ASA-201502-15](https://lists.archlinux.org/pipermail/arch-security/2015-February/000238.html)</td>

</tr>

<tr>

<td>[CVE-2015-0819](https://access.redhat.com/security/cve/CVE-2015-0819) [CVE-2015-0821](https://access.redhat.com/security/cve/CVE-2015-0821) [CVE-2015-0822](https://access.redhat.com/security/cve/CVE-2015-0822) [CVE-2015-0823](https://access.redhat.com/security/cve/CVE-2015-0823) [CVE-2015-0824](https://access.redhat.com/security/cve/CVE-2015-0824) [CVE-2015-0825](https://access.redhat.com/security/cve/CVE-2015-0825) [CVE-2015-0826](https://access.redhat.com/security/cve/CVE-2015-0826) [CVE-2015-0827](https://access.redhat.com/security/cve/CVE-2015-0827) [CVE-2015-0829](https://access.redhat.com/security/cve/CVE-2015-0829) [CVE-2015-0830](https://access.redhat.com/security/cve/CVE-2015-0830) [CVE-2015-0831](https://access.redhat.com/security/cve/CVE-2015-0831) [CVE-2015-0832](https://access.redhat.com/security/cve/CVE-2015-0832) [CVE-2015-0834](https://access.redhat.com/security/cve/CVE-2015-0834) [CVE-2015-0835](https://access.redhat.com/security/cve/CVE-2015-0835) [CVE-2015-0836](https://access.redhat.com/security/cve/CVE-2015-0836) [templink](https://www.mozilla.org/en-US/security/known-vulnerabilities/firefox/)</td>

<td>[firefox](https://www.archlinux.org/packages/?name=firefox)</td>

<td>2015-02-24</td>

<td><= 35.0.1-1</td>

<td>36.0-1</td>

<td><1d</td>

<td>Fixed</td>

<td>[ASA-201502-14](https://lists.archlinux.org/pipermail/arch-security/2015-February/000237.html)</td>

</tr>

<tr>

<td>[CVE-2015-0240](https://access.redhat.com/security/cve/CVE-2015-0240) [templink](https://www.samba.org/samba/history/samba-4.1.17.html)</td>

<td>[samba](https://www.archlinux.org/packages/?name=samba)</td>

<td>2015-02-23</td>

<td><= 4.1.16-1</td>

<td>4.1.17-1</td>

<td><1d</td>

<td>Fixed ([FS#43923](https://bugs.archlinux.org/task/43923))</td>

<td>[ASA-201502-13](https://lists.archlinux.org/pipermail/arch-security/2015-February/000236.html)</td>

</tr>

<tr>

<td>[CVE-2014-9636](https://access.redhat.com/security/cve/CVE-2014-9636) [templink](http://www.openwall.com/lists/oss-security/2014/11/02/2)</td>

<td>[unzip](https://www.archlinux.org/packages/?name=unzip)</td>

<td>2014-11-02</td>

<td><= 6.0-9</td>

<td>6.0-10</td>

<td>75d</td>

<td>Fixed ([FS#44171](https://bugs.archlinux.org/task/44171))</td>

<td>[ASA-201503-9](https://lists.archlinux.org/pipermail/arch-security/2015-March/000250.html)</td>

</tr>

<tr>

<td>[CVE-2015-1315](https://access.redhat.com/security/cve/CVE-2015-1315) [templink](http://www.openwall.com/lists/oss-security/2015/02/17/4)</td>

<td>[unzip](https://www.archlinux.org/packages/?name=unzip)</td>

<td>2014-11-02</td>

<td><= 6.0-9</td>

<td>6.0-9</td>

<td>-</td>

<td>Invalid</td>

<td>None</td>

</tr>

<tr>

<td>[CVE-2014-9680](https://access.redhat.com/security/cve/CVE-2014-9680) [templink](http://www.sudo.ws/sudo/alerts/tz.html)</td>

<td>[sudo](https://www.archlinux.org/packages/?name=sudo)</td>

<td>2015-02-09</td>

<td><= 1.8.12-1</td>

<td>1.8.12-1</td>

<td>4d</td>

<td>Fixed</td>

<td>None</td>

</tr>

<tr>

<td>[CVE-2014-5352](https://access.redhat.com/security/cve/CVE-2014-5352) [CVE-2014-5353](https://access.redhat.com/security/cve/CVE-2014-5353) [CVE-2014-5354](https://access.redhat.com/security/cve/CVE-2014-5354) [CVE-2014-9421](https://access.redhat.com/security/cve/CVE-2014-9421) [CVE-2014-9422](https://access.redhat.com/security/cve/CVE-2014-9422) [CVE-2014-9423](https://access.redhat.com/security/cve/CVE-2014-9423) [templink](http://web.mit.edu/kerberos/advisories/MITKRB5-SA-2015-001.txt) [templink](http://www.openwall.com/lists/oss-security/2014/12/16/1)</td>

<td>[krb5](https://www.archlinux.org/packages/?name=krb5)</td>

<td>2015-02-03</td>

<td><= 1.13-1</td>

<td>1.13.1-1</td>

<td>14d</td>

<td>Fixed</td>

<td>[ASA-201502-12](https://lists.archlinux.org/pipermail/arch-security/2015-February/000235.html)</td>

</tr>

<tr>

<td>[CVE-2015-0255](https://access.redhat.com/security/cve/CVE-2015-0255) [templink](http://www.x.org/wiki/Development/Security/Advisory-2015-02-10/)</td>

<td>[xorg-server](https://www.archlinux.org/packages/?name=xorg-server)</td>

<td>2015-02-10</td>

<td><= 1.16.3-2</td>

<td>1.16.4-1</td>

<td><1d</td>

<td>Fixed</td>

<td>[ASA-201502-11](https://lists.archlinux.org/pipermail/arch-security/2015-February/000234.html)</td>

</tr>

<tr>

<td>[CVE-2015-1191](https://access.redhat.com/security/cve/CVE-2015-1191) [templink](http://www.openwall.com/lists/oss-security/2015/01/18/3)</td>

<td>[pigz](https://www.archlinux.org/packages/?name=pigz)</td>

<td>2015-01-18</td>

<td><= 2.3.1-1</td>

<td>2.3.3-1</td>

<td>21d</td>

<td>Fixed ([FS#43748](https://bugs.archlinux.org/task/43748))</td>

<td>[ASA-201502-9](https://lists.archlinux.org/pipermail/arch-security/2015-February/000232.html)</td>

</tr>

<tr>

<td>[CVE-2015-0245](https://access.redhat.com/security/cve/CVE-2015-0245) [templink](http://lists.freedesktop.org/archives/dbus/2015-February/016553.html)</td>

<td>[dbus](https://www.archlinux.org/packages/?name=dbus)</td>

<td>2015-02-09</td>

<td><= 1.8.14-1</td>

<td>1.8.16-1</td>

<td>1d</td>

<td>Fixed</td>

<td>[ASA-201502-10](https://lists.archlinux.org/pipermail/arch-security/2015-February/000233.html)</td>

</tr>

<tr>

<td>[CVE-2015-1472](https://access.redhat.com/security/cve/CVE-2015-1472) [CVE-2015-1473](https://access.redhat.com/security/cve/CVE-2015-1473)</td>

<td>[glibc](https://www.archlinux.org/packages/?name=glibc)</td>

<td>2015-02-05</td>

<td><= 2.20-6</td>

<td>2.21-1</td>

<td>4d</td>

<td>Fixed ([FS#43747](https://bugs.archlinux.org/task/43747))</td>

<td>[ASA-201502-8](https://lists.archlinux.org/pipermail/arch-security/2015-February/000231.html)</td>

</tr>

<tr>

<td>[CVE-2014-9297](https://access.redhat.com/security/cve/CVE-2014-9297) [CVE-2014-9298](https://access.redhat.com/security/cve/CVE-2014-9298) [templink](http://support.ntp.org/bin/view/Main/SecurityNotice#vallen_is_not_validated_in_sever) [templink](http://support.ntp.org/bin/view/Main/SecurityNotice#1_can_be_spoofed_on_some_OSes_so)</td>

<td>[ntp](https://www.archlinux.org/packages/?name=ntp)</td>

<td>2015-02-04</td>

<td><= 4.2.8-1</td>

<td>4.2.8.p1-1</td>

<td>2d</td>

<td>Fixed</td>

<td>[ASA-201502-7](https://lists.archlinux.org/pipermail/arch-security/2015-February/000230.html)</td>

</tr>

<tr>

<td>[CVE-2014-9328](https://access.redhat.com/security/cve/CVE-2014-9328)</td>

<td>[clamav](https://www.archlinux.org/packages/?name=clamav)</td>

<td>2015-01-28</td>

<td><= 0.98.5-1</td>

<td>0.98.6-1</td>

<td><1d</td>

<td>Fixed</td>

<td>[ASA-201502-6](https://lists.archlinux.org/pipermail/arch-security/2015-February/000229.html)</td>

</tr>

<tr>

<td>[CVE-2015-1209](https://access.redhat.com/security/cve/CVE-2015-1209) [CVE-2015-1210](https://access.redhat.com/security/cve/CVE-2015-1210) [CVE-2015-1211](https://access.redhat.com/security/cve/CVE-2015-1211) [CVE-2015-1212](https://access.redhat.com/security/cve/CVE-2015-1212) [templink](http://googlechromereleases.blogspot.fr/2015/02/stable-channel-update.html)</td>

<td>[chromium](https://www.archlinux.org/packages/?name=chromium)</td>

<td>2015-02-05</td>

<td><= 40.0.2214.94-1</td>

<td>40.0.2214.111-1</td>

<td><1d</td>

<td>Fixed</td>

<td>[ASA-201502-5](https://lists.archlinux.org/pipermail/arch-security/2015-February/000228.html)</td>

</tr>

<tr>

<td>[CVE-2015-0313](https://access.redhat.com/security/cve/CVE-2015-0313) [CVE-2015-0314](https://access.redhat.com/security/cve/CVE-2015-0314) [CVE-2015-0315](https://access.redhat.com/security/cve/CVE-2015-0315) [CVE-2015-0316](https://access.redhat.com/security/cve/CVE-2015-0316) [CVE-2015-0317](https://access.redhat.com/security/cve/CVE-2015-0317) [CVE-2015-0318](https://access.redhat.com/security/cve/CVE-2015-0318) [CVE-2015-0319](https://access.redhat.com/security/cve/CVE-2015-0319) [CVE-2015-0320](https://access.redhat.com/security/cve/CVE-2015-0320) [CVE-2015-0321](https://access.redhat.com/security/cve/CVE-2015-0321) [CVE-2015-0322](https://access.redhat.com/security/cve/CVE-2015-0322) [CVE-2015-0323](https://access.redhat.com/security/cve/CVE-2015-0323) [CVE-2015-0324](https://access.redhat.com/security/cve/CVE-2015-0324) [CVE-2015-0325](https://access.redhat.com/security/cve/CVE-2015-0325) [CVE-2015-0326](https://access.redhat.com/security/cve/CVE-2015-0326) [CVE-2015-0327](https://access.redhat.com/security/cve/CVE-2015-0327) [CVE-2015-0328](https://access.redhat.com/security/cve/CVE-2015-0328) [CVE-2015-0329](https://access.redhat.com/security/cve/CVE-2015-0329) [CVE-2015-0330](https://access.redhat.com/security/cve/CVE-2015-0330) [templink](https://helpx.adobe.com/security/products/flash-player/apsb15-04.html)</td>

<td>[flashplugin](https://www.archlinux.org/packages/?name=flashplugin)</td>

<td>2015-02-05</td>

<td><= 11.2.202.440-1</td>

<td>11.2.202.442-1</td>

<td><1d</td>

<td>Fixed</td>

<td>[ASA-201502-2](https://lists.archlinux.org/pipermail/arch-security/2015-February/000225.html)</td>

</tr>

<tr>

<td>[CVE-2014-8161](https://access.redhat.com/security/cve/CVE-2014-8161) [CVE-2015-0241](https://access.redhat.com/security/cve/CVE-2015-0241) [CVE-2015-0243](https://access.redhat.com/security/cve/CVE-2015-0243) [CVE-2015-0244](https://access.redhat.com/security/cve/CVE-2015-0244) [templink](http://www.postgresql.org/docs/9.4/static/release-9-4-1.html)</td>

<td>[postgresql](https://www.archlinux.org/packages/?name=postgresql)</td>

<td>2015-02-05</td>

<td><= 9.4.0-1</td>

<td>9.4.1-1</td>

<td><1d</td>

<td>Fixed</td>

<td>[ASA-201502-4](https://lists.archlinux.org/pipermail/arch-security/2015-February/000227.html)</td>

</tr>

<tr>

<td>[CVE-2015-1380](https://access.redhat.com/security/cve/CVE-2015-1380) [CVE-2015-1381](https://access.redhat.com/security/cve/CVE-2015-1381) [CVE-2015-1382](https://access.redhat.com/security/cve/CVE-2015-1382) [templink](http://seclists.org/oss-sec/2015/q1/285)</td>

<td>[privoxy](https://www.archlinux.org/packages/?name=privoxy)</td>

<td>2015-01-26</td>

<td><= 3.0.22-1</td>

<td>3.0.23-1</td>

<td>3d</td>

<td>Fixed</td>

<td>[ASA-201502-1](https://lists.archlinux.org/pipermail/arch-security/2015-February/000224.html)</td>

</tr>

<tr>

<td>[CVE-2015-0235](https://access.redhat.com/security/cve/CVE-2015-0235) [templink](https://bugzilla.redhat.com/show_bug.cgi?id=CVE-2015-0235)</td>

<td>[glibc](https://www.archlinux.org/packages/?name=glibc)</td>

<td>2015-01-27</td>

<td>< 2.18-1 ?</td>

<td>2.18-1</td>

<td>< 1d</td>

<td>Fixed</td>

<td>None</td>

</tr>

<tr>

<td>[CVE-2015-0311](https://access.redhat.com/security/cve/CVE-2015-0311) [CVE-2015-0301](https://access.redhat.com/security/cve/CVE-2015-0301) [CVE-2015-0302](https://access.redhat.com/security/cve/CVE-2015-0302) [CVE-2015-0303](https://access.redhat.com/security/cve/CVE-2015-0303) [CVE-2015-0304](https://access.redhat.com/security/cve/CVE-2015-0304) [CVE-2015-0305](https://access.redhat.com/security/cve/CVE-2015-0305) [CVE-2015-0306](https://access.redhat.com/security/cve/CVE-2015-0306) [CVE-2015-0307](https://access.redhat.com/security/cve/CVE-2015-0307) [CVE-2015-0308](https://access.redhat.com/security/cve/CVE-2015-0308) [CVE-2015-0309](https://access.redhat.com/security/cve/CVE-2015-0309) [templink](https://helpx.adobe.com/security/products/flash-player/apsb15-01.html)</td>

<td>[flashplugin](https://www.archlinux.org/packages/?name=flashplugin)</td>

<td>2015-01-23</td>

<td><= 11.2.202.438-1</td>

<td>11.2.202.440-1</td>

<td>3d</td>

<td>Fixed</td>

<td>[ASA-201501-22](https://lists.archlinux.org/pipermail/arch-security/2015-January/000220.html)</td>

</tr>

<tr>

<td>[CVE-2015-0231](https://access.redhat.com/security/cve/CVE-2015-0231) [CVE-2014-9427](https://access.redhat.com/security/cve/CVE-2014-9427) [CVE-2015-0232](https://access.redhat.com/security/cve/CVE-2015-0232) [templink](https://bugs.php.net/bug.php?id=68710) [templink](https://bugs.php.net/bug.php?id=68618) [templink](https://bugs.php.net/bug.php?id=68799)</td>

<td>[php](https://www.archlinux.org/packages/?name=php)</td>

<td>2015-01-22</td>

<td><= 5.6.4-1</td>

<td>5.6.5-1</td>

<td><1d</td>

<td>Fixed</td>

<td>[ASA-201501-17](https://lists.archlinux.org/pipermail/arch-security/2015-January/000215.html)</td>

</tr>

<tr>

<td>[CVE-2014-9638](https://access.redhat.com/security/cve/CVE-2014-9638) [CVE-2014-9639](https://access.redhat.com/security/cve/CVE-2014-9639) [CVE-2014-9640](https://access.redhat.com/security/cve/CVE-2014-9640) [templink](http://www.openwall.com/lists/oss-security/2015/01/22/9)</td>

<td>[vorbis-tools](https://www.archlinux.org/packages/?name=vorbis-tools)</td>

<td>2015-01-21</td>

<td><= 1.4.0-4</td>

<td>1.4.0-5</td>

<td>64d</td>

<td>Fixed ([FS#44172](https://bugs.archlinux.org/task/44172))</td>

<td>[ASA-201503-24](https://lists.archlinux.org/pipermail/arch-security/2015-March/000265.html)</td>

</tr>

<tr>

<td>[CVE-2015-1345](https://access.redhat.com/security/cve/CVE-2015-1345) [templink](http://seclists.org/oss-sec/2015/q1/179)</td>

<td>[grep](https://www.archlinux.org/packages/?name=grep)</td>

<td>2015-01-18</td>

<td><= 2.21-1</td>

<td>2.21-2</td>

<td>46d</td>

<td>Fixed ([FS#44017](https://bugs.archlinux.org/task/44017))</td>

<td>[ASA-201503-4](https://lists.archlinux.org/pipermail/arch-security/2015-March/000244.html)</td>

</tr>

<tr>

<td>[CVE-2014-7923](https://access.redhat.com/security/cve/CVE-2014-7923) [CVE-2014-7924](https://access.redhat.com/security/cve/CVE-2014-7924) [CVE-2014-7925](https://access.redhat.com/security/cve/CVE-2014-7925) [CVE-2014-7926](https://access.redhat.com/security/cve/CVE-2014-7926) [CVE-2014-7927](https://access.redhat.com/security/cve/CVE-2014-7927) [CVE-2014-7928](https://access.redhat.com/security/cve/CVE-2014-7928) [CVE-2014-7930](https://access.redhat.com/security/cve/CVE-2014-7930) [CVE-2014-7931](https://access.redhat.com/security/cve/CVE-2014-7931) [CVE-2014-7929](https://access.redhat.com/security/cve/CVE-2014-7929) [CVE-2014-7932](https://access.redhat.com/security/cve/CVE-2014-7932) [CVE-2014-7933](https://access.redhat.com/security/cve/CVE-2014-7933) [CVE-2014-7934](https://access.redhat.com/security/cve/CVE-2014-7934) [CVE-2014-7935](https://access.redhat.com/security/cve/CVE-2014-7935) [CVE-2014-7936](https://access.redhat.com/security/cve/CVE-2014-7936) [CVE-2014-7937](https://access.redhat.com/security/cve/CVE-2014-7937) [CVE-2014-7938](https://access.redhat.com/security/cve/CVE-2014-7938) [CVE-2014-7939](https://access.redhat.com/security/cve/CVE-2014-7939) [CVE-2014-7940](https://access.redhat.com/security/cve/CVE-2014-7940) [CVE-2014-7941](https://access.redhat.com/security/cve/CVE-2014-7941) [CVE-2014-7942](https://access.redhat.com/security/cve/CVE-2014-7942) [CVE-2014-7943](https://access.redhat.com/security/cve/CVE-2014-7943) [CVE-2014-7944](https://access.redhat.com/security/cve/CVE-2014-7944) [CVE-2014-7945](https://access.redhat.com/security/cve/CVE-2014-7945) [CVE-2014-7946](https://access.redhat.com/security/cve/CVE-2014-7946) [CVE-2014-7947](https://access.redhat.com/security/cve/CVE-2014-7947) [CVE-2014-7948](https://access.redhat.com/security/cve/CVE-2014-7948) [CVE-2015-1205](https://access.redhat.com/security/cve/CVE-2015-1205) [templink](http://googlechromereleases.blogspot.fr/2015/01/stable-update.html)</td>

<td>[chromium](https://www.archlinux.org/packages/?name=chromium)</td>

<td>2015-01-22</td>

<td><= 39.0.2171.99-1</td>

<td>40.0.2214.91-1</td>

<td>3d</td>

<td>Fixed</td>

<td>[ASA-201501-21](https://lists.archlinux.org/pipermail/arch-security/2015-January/000219.html)</td>

</tr>

<tr>

<td>[CVE-2014-3566](https://access.redhat.com/security/cve/CVE-2014-3566) [CVE-2014-6549](https://access.redhat.com/security/cve/CVE-2014-6549) [CVE-2014-6585](https://access.redhat.com/security/cve/CVE-2014-6585) [CVE-2014-6587](https://access.redhat.com/security/cve/CVE-2014-6587) [CVE-2014-6591](https://access.redhat.com/security/cve/CVE-2014-6591) [CVE-2014-6593](https://access.redhat.com/security/cve/CVE-2014-6593) [CVE-2014-6601](https://access.redhat.com/security/cve/CVE-2014-6601) [CVE-2015-0383](https://access.redhat.com/security/cve/CVE-2015-0383) [CVE-2015-0395](https://access.redhat.com/security/cve/CVE-2015-0395) [CVE-2015-0400](https://access.redhat.com/security/cve/CVE-2015-0400) [CVE-2015-0403](https://access.redhat.com/security/cve/CVE-2015-0403) [CVE-2015-0406](https://access.redhat.com/security/cve/CVE-2015-0406) [CVE-2015-0407](https://access.redhat.com/security/cve/CVE-2015-0407) [CVE-2015-0408](https://access.redhat.com/security/cve/CVE-2015-0408) [CVE-2015-0410](https://access.redhat.com/security/cve/CVE-2015-0410) [CVE-2015-0412](https://access.redhat.com/security/cve/CVE-2015-0412) [CVE-2015-0413](https://access.redhat.com/security/cve/CVE-2015-0413) [CVE-2015-0421](https://access.redhat.com/security/cve/CVE-2015-0421) [CVE-2015-0437](https://access.redhat.com/security/cve/CVE-2015-0437) [templink](http://www.oracle.com/technetwork/topics/security/cpujan2015verbose-1972976.html#JAVA)</td>

<td>[jdk8-openjdk](https://www.archlinux.org/packages/?name=jdk8-openjdk) [jre8-openjdk](https://www.archlinux.org/packages/?name=jre8-openjdk) [jre8-openjdk-headless](https://www.archlinux.org/packages/?name=jre8-openjdk-headless)</td>

<td>2015-01-22</td>

<td><= 8.u25-2</td>

<td>8.u31-1</td>

<td>1d</td>

<td>Fixed</td>

<td>[ASA-201501-14](https://lists.archlinux.org/pipermail/arch-security/2015-January/000210.html) [ASA-201501-15](https://lists.archlinux.org/pipermail/arch-security/2015-January/000211.html) [ASA-201501-16](https://lists.archlinux.org/pipermail/arch-security/2015-January/000212.html)</td>

</tr>

<tr>

<td>[CVE-2014-3566](https://access.redhat.com/security/cve/CVE-2014-3566) [CVE-2014-6585](https://access.redhat.com/security/cve/CVE-2014-6585) [CVE-2014-6587](https://access.redhat.com/security/cve/CVE-2014-6587) [CVE-2014-6591](https://access.redhat.com/security/cve/CVE-2014-6591) [CVE-2014-6593](https://access.redhat.com/security/cve/CVE-2014-6593) [CVE-2014-6601](https://access.redhat.com/security/cve/CVE-2014-6601) [CVE-2015-0383](https://access.redhat.com/security/cve/CVE-2015-0383) [CVE-2015-0395](https://access.redhat.com/security/cve/CVE-2015-0395) [CVE-2015-0407](https://access.redhat.com/security/cve/CVE-2015-0407) [CVE-2015-0408](https://access.redhat.com/security/cve/CVE-2015-0408) [CVE-2015-0410](https://access.redhat.com/security/cve/CVE-2015-0410) [CVE-2015-0412](https://access.redhat.com/security/cve/CVE-2015-0412) [templink](http://www.oracle.com/technetwork/topics/security/cpujan2015verbose-1972976.html#JAVA)</td>

<td>[jdk7-openjdk](https://www.archlinux.org/packages/?name=jdk7-openjdk) [jre7-openjdk](https://www.archlinux.org/packages/?name=jre7-openjdk) [jre7-openjdk-headless](https://www.archlinux.org/packages/?name=jre7-openjdk-headless)</td>

<td>2015-01-22</td>

<td><= 7.u71_2.5.3-3</td>

<td>Fixed</td>

<td>[ASA-201501-18](https://lists.archlinux.org/pipermail/arch-security/2015-January/000216.html) [ASA-201501-19](https://lists.archlinux.org/pipermail/arch-security/2015-January/000217.html) [ASA-201501-20](https://lists.archlinux.org/pipermail/arch-security/2015-January/000218.html)</td>

</tr>

<tr>

<td>[CVE-2014-8157](https://access.redhat.com/security/cve/CVE-2014-8157) [CVE-2014-8158](https://access.redhat.com/security/cve/CVE-2014-8158) [templink](http://seclists.org/oss-sec/2015/q1/210)</td>

<td>[jasper](https://www.archlinux.org/packages/?name=jasper)</td>

<td>2015-01-22</td>

<td><= 1.900.1-12</td>

<td>1.900.1-13</td>

<td>5d</td>

<td>Fixed ([FS#43592](https://bugs.archlinux.org/task/43592))</td>

<td>[ASA-201501-23](https://lists.archlinux.org/pipermail/arch-security/2015-January/000222.html)</td>

</tr>

<tr>

<td>[CVE-2014-8132](https://access.redhat.com/security/cve/CVE-2014-8132) [templink](http://www.libssh.org/2014/12/19/libssh-0-6-4-security-and-bugfix-release/)</td>

<td>[libssh](https://www.archlinux.org/packages/?name=libssh)</td>

<td>2014-12-19</td>

<td><= 0.6.3-1</td>

<td>0.6.4-1</td>

<td>26d</td>

<td>Fixed</td>

<td>[ASA-201501-12](https://lists.archlinux.org/pipermail/arch-security/2015-January/000208.html)</td>

</tr>

<tr>

<td>[CVE-2015-1182](https://access.redhat.com/security/cve/CVE-2015-1182) [templink](https://polarssl.org/tech-updates/security-advisories/polarssl-security-advisory-2014-04)</td>

<td>[polarssl](https://www.archlinux.org/packages/?name=polarssl)</td>

<td>2012-09-19</td>

<td><= 1.3.9-1</td>

<td>1.3.9-2</td>

<td>1d</td>

<td>Fixed ([FS#43508](https://bugs.archlinux.org/task/43508))</td>

<td>[ASA-201501-13](https://lists.archlinux.org/pipermail/arch-security/2015-January/000209.html)</td>

</tr>

<tr>

<td>[CVE-2012-3505](https://access.redhat.com/security/cve/CVE-2012-3505) [templink](http://www.openwall.com/lists/oss-security/2012/08/18/1)</td>

<td>[tinyproxy](https://www.archlinux.org/packages/?name=tinyproxy)</td>

<td>2012-09-10</td>

<td><= 1.8.3-1</td>

<td>1.8.4-1</td>

<td>> 740d</td>

<td>Fixed ([FS#38400](https://bugs.archlinux.org/task/38400))</td>

<td>[ASA-201501-11](https://lists.archlinux.org/pipermail/arch-security/2015-January/000207.html)</td>

</tr>

<tr>

<td>[CVE-2014-9447](https://access.redhat.com/security/cve/CVE-2014-9447) [templink](https://git.fedorahosted.org/cgit/elfutils.git/commit/?id=147018e729e7c22eeabf15b82d26e4bf68a0d18e)</td>

<td>[elfutils](https://www.archlinux.org/packages/?name=elfutils)</td>

<td>2015-01-19</td>

<td><= 0.161-2</td>

<td>0.161-3</td>

<td>42d</td>

<td>Fixed ([FS#44019](https://bugs.archlinux.org/task/44019))</td>

<td>[ASA-201503-2](https://lists.archlinux.org/pipermail/arch-security/2015-March/000242.html)</td>

</tr>

<tr>

<td>[CVE-2014-9447](https://access.redhat.com/security/cve/CVE-2014-9447) [templink](https://git.fedorahosted.org/cgit/elfutils.git/commit/?id=147018e729e7c22eeabf15b82d26e4bf68a0d18e)</td>

<td>[lib32-elfutils](https://www.archlinux.org/packages/?name=lib32-elfutils)</td>

<td>2015-01-19</td>

<td><= 0.161-1</td>

<td>0.161-2</td>

<td>42d</td>

<td>Fixed ([FS#44020](https://bugs.archlinux.org/task/44020))</td>

<td>[ASA-201503-3](https://lists.archlinux.org/pipermail/arch-security/2015-March/000243.html)</td>

</tr>

<tr>

<td>[CVE-2014-8143](https://access.redhat.com/security/cve/CVE-2014-8143) [templink](https://www.samba.org/samba/security/CVE-2014-8143)</td>

<td>[samba](https://www.archlinux.org/packages/?name=samba)</td>

<td>2015-01-15</td>

<td><= 4.1.15-1</td>

<td>4.1.16-1</td>

<td>4d</td>

<td>Fixed</td>

<td>[ASA-201501-10](https://lists.archlinux.org/pipermail/arch-security/2015-January/000206.html)</td>

</tr>

<tr>

<td>[CVE-2015-1197](https://access.redhat.com/security/cve/CVE-2015-1197) [templink](http://www.openwall.com/lists/oss-security/2015/01/18/7)</td>

<td>[cpio](https://www.archlinux.org/packages/?name=cpio)</td>

<td>2015-01-16</td>

<td><= 2.11-5</td>

<td>2.11-6</td>

<td>65d</td>

<td>Fixed ([FS#44173](https://bugs.archlinux.org/task/44173))</td>

<td>[ASA-201503-22](https://lists.archlinux.org/pipermail/arch-security/2015-March/000263.html)</td>

</tr>

<tr>

<td>[CVE-2015-1196](https://access.redhat.com/security/cve/CVE-2015-1196) [CVE-2014-9637](https://access.redhat.com/security/cve/CVE-2014-9637) [templink](http://www.openwall.com/lists/oss-security/2015/01/18/6) [templink](https://savannah.gnu.org/bugs/?44051)</td>

<td>[patch](https://www.archlinux.org/packages/?name=patch)</td>

<td>2015-01-14</td>

<td><= 2.7.1-3</td>

<td>2.7.3-1</td>

<td>14d</td>

<td>Fixed</td>

<td>[ASA-201501-24](https://lists.archlinux.org/pipermail/arch-security/2015-January/000223.html)</td>

</tr>

<tr>

<td>[CVE-2014-9571](https://access.redhat.com/security/cve/CVE-2014-9571) [CVE-2014-9572](https://access.redhat.com/security/cve/CVE-2014-9572) [CVE-2014-9573](https://access.redhat.com/security/cve/CVE-2014-9573) [CVE-2014-9624](https://access.redhat.com/security/cve/CVE-2014-9624) [CVE-2015-1042](https://access.redhat.com/security/cve/CVE-2015-1042) [templink](http://www.openwall.com/lists/oss-security/2015/01/17/1) [templink](http://www.openwall.com/lists/oss-security/2015/01/17/3) [templink](http://www.openwall.com/lists/oss-security/2015/01/17/2) [templink](http://www.openwall.com/lists/oss-security/2015/01/18/11)</td>

<td>[mantisbt](https://www.archlinux.org/packages/?name=mantisbt)</td>

<td>2015-01-17</td>

<td><= 1.2.18-1</td>

<td>1.2.19-1</td>

<td>20d</td>

<td>Fixed</td>

<td>[ASA-201502-3](https://lists.archlinux.org/pipermail/arch-security/2015-February/000226.html)</td>

</tr>

<tr>

<td>[CVE-2014-8634](https://access.redhat.com/security/cve/CVE-2014-8634) [CVE-2014-8635](https://access.redhat.com/security/cve/CVE-2014-8635) [CVE-2014-8638](https://access.redhat.com/security/cve/CVE-2014-8638) [CVE-2014-8639](https://access.redhat.com/security/cve/CVE-2014-8639) [templink](https://www.mozilla.org/en-US/security/known-vulnerabilities/thunderbird/)</td>

<td>[thunderbird](https://www.archlinux.org/packages/?name=thunderbird)</td>

<td>2015-01-13</td>

<td><= 31.3.0-1</td>

<td>31.4.0-1</td>

<td><1d</td>

<td>Fixed</td>

<td>[ASA-201501-7](https://lists.archlinux.org/pipermail/arch-security/2015-January/000203.html)</td>

</tr>

<tr>

<td>[CVE-2014-8634](https://access.redhat.com/security/cve/CVE-2014-8634) [CVE-2014-8635](https://access.redhat.com/security/cve/CVE-2014-8635) [CVE-2014-8636](https://access.redhat.com/security/cve/CVE-2014-8636) [CVE-2014-8637](https://access.redhat.com/security/cve/CVE-2014-8637) [CVE-2014-8638](https://access.redhat.com/security/cve/CVE-2014-8638) [CVE-2014-8639](https://access.redhat.com/security/cve/CVE-2014-8639) [CVE-2014-8640](https://access.redhat.com/security/cve/CVE-2014-8640) [CVE-2014-8641](https://access.redhat.com/security/cve/CVE-2014-8641) [CVE-2014-8642](https://access.redhat.com/security/cve/CVE-2014-8642) [templink](https://www.mozilla.org/en-US/security/known-vulnerabilities/firefox/)</td>

<td>[firefox](https://www.archlinux.org/packages/?name=firefox)</td>

<td>2015-01-13</td>

<td><= 34.0.5-1</td>

<td>35.0-1</td>

<td><1d</td>

<td>Fixed</td>

<td>[ASA-201501-6](https://lists.archlinux.org/pipermail/arch-security/2015-January/000202.html)</td>

</tr>

<tr>

<td>[CVE-2014-3571](https://access.redhat.com/security/cve/CVE-2014-3571) [CVE-2015-0206](https://access.redhat.com/security/cve/CVE-2015-0206) [CVE-2014-3569](https://access.redhat.com/security/cve/CVE-2014-3569) [CVE-2014-3572](https://access.redhat.com/security/cve/CVE-2014-3572) [CVE-2015-0205](https://access.redhat.com/security/cve/CVE-2015-0205) [CVE-2014-8275](https://access.redhat.com/security/cve/CVE-2014-8275) [CVE-2014-3570](https://access.redhat.com/security/cve/CVE-2014-3570) [templink](https://www.openssl.org/news/secadv_20150108.txt)</td>

<td>[openssl](https://www.archlinux.org/packages/?name=openssl)</td>

<td>2015-01-08</td>

<td><= 1.0.1.j-1</td>

<td>1.0.1.k-1</td>

<td><1d</td>

<td>Fixed</td>

<td>[ASA-201501-2](https://lists.archlinux.org/pipermail/arch-security/2015-January/000198.html)</td>

</tr>

<tr>

<td>[CVE-2014-8150](https://access.redhat.com/security/cve/CVE-2014-8150) [templink](http://curl.haxx.se/docs/adv_20150108B.html)</td>

<td>[curl](https://www.archlinux.org/packages/?name=curl)</td>

<td>2015-01-08</td>

<td><= 7.39.0-1</td>

<td>7.40.0-1</td>

<td>10d</td>

<td>Fixed ([FS#43379](https://bugs.archlinux.org/task/43379))</td>

<td>[ASA-201501-9](https://lists.archlinux.org/pipermail/arch-security/2015-January/000205.html)</td>

</tr>

<tr>

<td>[CVE-2014-6272](https://access.redhat.com/security/cve/CVE-2014-6272) [templink](http://archives.seul.org/libevent/users/Jan-2015/msg00010.html)</td>

<td>[libevent](https://www.archlinux.org/packages/?name=libevent)</td>

<td>2015-01-05</td>

<td><= 2.0.21-3</td>

<td>2.0.22-1</td>

<td>7d</td>

<td>Fixed ([FS#43366](https://bugs.archlinux.org/task/43366))</td>

<td>[ASA-201501-4](https://lists.archlinux.org/pipermail/arch-security/2015-January/000200.html)</td>

</tr>

<tr>

<td>[CVE-2014-8139](https://access.redhat.com/security/cve/CVE-2014-8139) [CVE-2014-8140](https://access.redhat.com/security/cve/CVE-2014-8140) [CVE-2014-8141](https://access.redhat.com/security/cve/CVE-2014-8141) [templink](http://www.ocert.org/advisories/ocert-2014-011.html)</td>

<td>[unzip](https://www.archlinux.org/packages/?name=unzip)</td>

<td>2014-12-22</td>

<td><= 6.0-7</td>

<td>6.0-9</td>

<td>17d</td>

<td>Fixed ([FS#43300](https://bugs.archlinux.org/task/43300)) ([FS#43391](https://bugs.archlinux.org/task/43391))</td>

<td>[ASA-201501-3](https://lists.archlinux.org/pipermail/arch-security/2015-January/000199.html)</td>

</tr>

<tr>

<td>[CVE-2014-6395](https://access.redhat.com/security/cve/CVE-2014-6395) [CVE-2014-6396](https://access.redhat.com/security/cve/CVE-2014-6396) [CVE-2014-9376](https://access.redhat.com/security/cve/CVE-2014-9376) [CVE-2014-9377](https://access.redhat.com/security/cve/CVE-2014-9377) [CVE-2014-9378](https://access.redhat.com/security/cve/CVE-2014-9378) [CVE-2014-9379](https://access.redhat.com/security/cve/CVE-2014-9379) [CVE-2014-9380](https://access.redhat.com/security/cve/CVE-2014-9380) [CVE-2014-9381](https://access.redhat.com/security/cve/CVE-2014-9381) [templink](https://www.obrela.com/home/security-labs/advisories/osi-advisory-osi-1402/)</td>

<td>[ettercap](https://www.archlinux.org/packages/?name=ettercap) [ettercap-gtk](https://www.archlinux.org/packages/?name=ettercap-gtk)</td>

<td>2014-12-16</td>

<td><= 0.8.1-2</td>

<td>0.8.2-1</td>

<td>89d</td>

<td>Fixed ([FS#44174](https://bugs.archlinux.org/task/44174))</td>

<td>[ASA-201503-12](https://lists.archlinux.org/pipermail/arch-security/2015-March/000253.html) [ASA-201503-13](https://lists.archlinux.org/pipermail/arch-security/2015-March/000254.html)</td>

</tr>

<tr>

<td>[CVE-2014-9425](https://access.redhat.com/security/cve/CVE-2014-9425) [templink](https://bugs.php.net/bug.php?id=68676)</td>

<td>[php](https://www.archlinux.org/packages/?name=php)</td>

<td>2014-12-29</td>

<td><= 5.6.4-1</td>

<td>5.6.5-1</td>

<td>6d</td>

<td>Fixed</td>

<td>None</td>

</tr>

<tr>

<td>[CVE-2014-9295](https://access.redhat.com/security/cve/CVE-2014-9295) [CVE-2014-9296](https://access.redhat.com/security/cve/CVE-2014-9296) [templink](http://support.ntp.org/bin/view/Main/SecurityNotice#Buffer_overflow_in_ctl_putdata)</td>

<td>[ntp](https://www.archlinux.org/packages/?name=ntp)</td>

<td>2014-12-19</td>

<td>< 4.2.8-1</td>

<td>4.2.8-1</td>

<td>1d</td>

<td>Fixed</td>

<td>[ASA-201412-24](https://lists.archlinux.org/pipermail/arch-security/2014-December/000189.html)</td>

</tr>

<tr>

<td>[CVE-2014-8142](https://access.redhat.com/security/cve/CVE-2014-8142) [templink](https://bugzilla.redhat.com/show_bug.cgi?id=1175718)</td>

<td>[php](https://www.archlinux.org/packages/?name=php)</td>

<td>2014-12-18</td>

<td><= 5.6.3-1</td>

<td>5.6.4-1</td>

<td>1d</td>

<td>Fixed</td>

<td>[ASA-201412-23](https://lists.archlinux.org/pipermail/arch-security/2014-December/000183.html)</td>

</tr>

<tr>

<td>[CVE-2014-8137](https://access.redhat.com/security/cve/CVE-2014-8137) [CVE-2011-4516](https://access.redhat.com/security/cve/CVE-2011-4516) [CVE-2011-4517](https://access.redhat.com/security/cve/CVE-2011-4517) [templink](https://marc.info/?l=oss-security&m=141891163026757&w=2)</td>

<td>[jasper](https://www.archlinux.org/packages/?name=jasper)</td>

<td>2014-12-18</td>

<td><= 1.900.1-11</td>

<td>1.900.1-12</td>

<td>1d</td>

<td>Fixed ([FS#43155](https://bugs.archlinux.org/task/43155))</td>

<td>[ASA-201412-22](https://lists.archlinux.org/pipermail/arch-security/2014-December/000182.html)</td>

</tr>

<tr>

<td>[CVE-2014-9029](https://access.redhat.com/security/cve/CVE-2014-9029) [templink](https://marc.info/?l=oss-security&m=141770163916268&w=2)</td>

<td>[jasper](https://www.archlinux.org/packages/?name=jasper)</td>

<td>2014-12-04</td>

<td><= 1.900.1-10</td>

<td>1.900.1-12</td>

<td>6d</td>

<td>Fixed ([FS#43044](https://bugs.archlinux.org/task/43044))</td>

<td>[ASA-201412-22](https://lists.archlinux.org/pipermail/arch-security/2014-December/000182.html)</td>

</tr>

<tr>

<td>[CVE-2012-3406](https://access.redhat.com/security/cve/CVE-2012-3406) [CVE-2014-9402](https://access.redhat.com/security/cve/CVE-2014-9402) [templink](http://www.openwall.com/lists/oss-security/2014/12/18/1)</td>

<td>[glibc](https://www.archlinux.org/packages/?name=glibc) [lib32-glibc](https://www.archlinux.org/packages/?name=lib32-glibc)</td>

<td>2014-12-17</td>

<td><= 2.20-4</td>

<td>2.20-5</td>

<td>1d</td>

<td>Fixed</td>

<td>[ASA-201412-21](https://lists.archlinux.org/pipermail/arch-security/2014-December/000181.html)</td>

</tr>

<tr>

<td>[CVE-2014-9253](https://access.redhat.com/security/cve/CVE-2014-9253) [templink](http://seclists.org/oss-sec/2014/q4/1050)</td>

<td>[dokuwiki](https://www.archlinux.org/packages/?name=dokuwiki)</td>

<td>2014-12-15</td>

<td><= 20140929_a-1</td>

<td>20140929_b-1</td>

<td><1d</td>

<td>Fixed</td>

<td>[ASA-201412-19](https://lists.archlinux.org/pipermail/arch-security/2014-December/000177.html)</td>

</tr>

<tr>

<td>[CVE-2014-3580](https://access.redhat.com/security/cve/CVE-2014-3580) [CVE-2014-8108](https://access.redhat.com/security/cve/CVE-2014-8108) [templink](https://subversion.apache.org/security/CVE-2014-3580-advisory.txt) [templink](https://subversion.apache.org/security/CVE-2014-8108-advisory.txt)</td>

<td>[subversion](https://www.archlinux.org/packages/?name=subversion)</td>

<td>2014-12-16</td>

<td><= 1.8.10-1</td>

<td>1.8.11-1</td>

<td><1d</td>

<td>Fixed</td>

<td>[ASA-201412-17](https://lists.archlinux.org/pipermail/arch-security/2014-December/000175.html)</td>

</tr>

<tr>

<td>[CVE-2014-9356](https://access.redhat.com/security/cve/CVE-2014-9356) [CVE-2014-9357](https://access.redhat.com/security/cve/CVE-2014-9357) [CVE-2014-9358](https://access.redhat.com/security/cve/CVE-2014-9358) [templink](http://www.securityfocus.com/archive/1/534215)</td>

<td>[docker](https://www.archlinux.org/packages/?name=docker)</td>

<td>2014-12-12</td>

<td><= 1:1.3.2-1</td>

<td>1:1.4.0-1</td>

<td>2d</td>

<td>Fixed</td>

<td>[ASA-201412-16](https://lists.archlinux.org/pipermail/arch-security/2014-December/000174.html)</td>

</tr>

<tr>

<td>[CVE-2013-1752](https://access.redhat.com/security/cve/CVE-2013-1752) [CVE-2013-1753](https://access.redhat.com/security/cve/CVE-2013-1753) [CVE-2014-9365](https://access.redhat.com/security/cve/CVE-2014-9365) [templink](https://hg.python.org/cpython/raw-file/v2.7.9/Misc/NEWS)</td>

<td>[python2](https://www.archlinux.org/packages/?name=python2)</td>

<td>2014-12-11</td>

<td><= 2.7.8-1</td>

<td>2.7.9-1</td>

<td>3d</td>

<td>Fixed</td>

<td>[ASA-201412-15](https://lists.archlinux.org/pipermail/arch-security/2014-December/000173.html)</td>

</tr>

<tr>

<td>[CVE-2014-0580](https://access.redhat.com/security/cve/CVE-2014-0580) [CVE-2014-0587](https://access.redhat.com/security/cve/CVE-2014-0587) [CVE-2014-8443](https://access.redhat.com/security/cve/CVE-2014-8443) [CVE-2014-9162](https://access.redhat.com/security/cve/CVE-2014-9162) [CVE-2014-9163](https://access.redhat.com/security/cve/CVE-2014-9163) [CVE-2014-9164](https://access.redhat.com/security/cve/CVE-2014-9164) [templink](https://helpx.adobe.com/security/products/flash-player/apsb14-27.html)</td>

<td>[flashplugin](https://www.archlinux.org/packages/?name=flashplugin)</td>

<td>2014-12-09</td>

<td><= 11.2.202.424-1</td>

<td>11.2.202.425-1</td>

<td>3d</td>

<td>Fixed</td>

<td>[ASA-201412-13](https://lists.archlinux.org/pipermail/arch-security/2014-December/000171.html)</td>

</tr>

<tr>

<td>[CVE-2014-8091](https://access.redhat.com/security/cve/CVE-2014-8091) [CVE-2014-8092](https://access.redhat.com/security/cve/CVE-2014-8092) [CVE-2014-8093](https://access.redhat.com/security/cve/CVE-2014-8093) [CVE-2014-8094](https://access.redhat.com/security/cve/CVE-2014-8094) [CVE-2014-8095](https://access.redhat.com/security/cve/CVE-2014-8095) [CVE-2014-8096](https://access.redhat.com/security/cve/CVE-2014-8096) [CVE-2014-8097](https://access.redhat.com/security/cve/CVE-2014-8097) [CVE-2014-8098](https://access.redhat.com/security/cve/CVE-2014-8098) [CVE-2014-8099](https://access.redhat.com/security/cve/CVE-2014-8099) [CVE-2014-8100](https://access.redhat.com/security/cve/CVE-2014-8100) [CVE-2014-8101](https://access.redhat.com/security/cve/CVE-2014-8101) [CVE-2014-8102](https://access.redhat.com/security/cve/CVE-2014-8102) [CVE-2014-8103](https://access.redhat.com/security/cve/CVE-2014-8103) [templink](http://www.x.org/wiki/Development/Security/Advisory-2014-12-09/)</td>

<td>[xorg-server](https://www.archlinux.org/packages/?name=xorg-server)</td>

<td>2014-12-09</td>

<td><= 1.16.2-1</td>

<td>1.16.2.901-1</td>

<td>2d</td>

<td>Fixed</td>

<td>[ASA-201412-14](https://lists.archlinux.org/pipermail/arch-security/2014-December/000172.html)</td>

</tr>

<tr>

<td>[CVE-2014-8093](https://access.redhat.com/security/cve/CVE-2014-8093) [CVE-2014-8098](https://access.redhat.com/security/cve/CVE-2014-8098) [CVE-2014-8298](https://access.redhat.com/security/cve/CVE-2014-8298) [templink](https://nvidia.custhelp.com/app/answers/detail/a_id/3610)</td>

<td>[nvidia](https://www.archlinux.org/packages/?name=nvidia) [nvidia-lts](https://www.archlinux.org/packages/?name=nvidia-lts)</td>

<td>2014-12-09</td>

<td><= 343.22-6</td>

<td>343.36-1</td>

<td>3d</td>

<td>Fixed</td>

<td>[ASA-201412-12](https://lists.archlinux.org/pipermail/arch-security/2014-December/000170.html)</td>

</tr>

<tr>

<td>[CVE-2014-8093](https://access.redhat.com/security/cve/CVE-2014-8093) [CVE-2014-8098](https://access.redhat.com/security/cve/CVE-2014-8098) [CVE-2014-8298](https://access.redhat.com/security/cve/CVE-2014-8298) [templink](https://nvidia.custhelp.com/app/answers/detail/a_id/3610)</td>

<td>[nvidia-340xx](https://www.archlinux.org/packages/?name=nvidia-340xx) [nvidia-340xx-lts](https://www.archlinux.org/packages/?name=nvidia-340xx-lts)</td>

<td>2014-12-09</td>

<td><= 340.58-3</td>

<td>340.65-1</td>

<td>3d</td>

<td>Fixed</td>

<td>[ASA-201412-11](https://lists.archlinux.org/pipermail/arch-security/2014-December/000169.html)</td>

</tr>

<tr>

<td>[CVE-2014-8093](https://access.redhat.com/security/cve/CVE-2014-8093) [CVE-2014-8098](https://access.redhat.com/security/cve/CVE-2014-8098) [CVE-2014-8298](https://access.redhat.com/security/cve/CVE-2014-8298) [templink](https://nvidia.custhelp.com/app/answers/detail/a_id/3610)</td>

<td>[nvidia-304xx](https://www.archlinux.org/packages/?name=nvidia-304xx) [nvidia-304xx-lts](https://www.archlinux.org/packages/?name=nvidia-304xx-lts)</td>

<td>2014-12-09</td>

<td>< 304.125-1</td>

<td>304.125-1</td>

<td>< 1d</td>

<td>Fixed</td>

<td>[ASA-201412-10](https://lists.archlinux.org/pipermail/arch-security/2014-December/000168.html)</td>

</tr>

<tr>

<td>[CVE-2014-8601](https://access.redhat.com/security/cve/CVE-2014-8601) [templink](http://doc.powerdns.com/md/security/powerdns-advisory-2014-02/)</td>

<td>[powerdns-recursor](https://www.archlinux.org/packages/?name=powerdns-recursor)</td>

<td>2014-12-09</td>

<td><= 3.6.1-1</td>

<td>3.6.2-1</td>

<td><1d</td>

<td>Fixed</td>

<td>[ASA-201412-9](https://lists.archlinux.org/pipermail/arch-security/2014-December/000167.html)</td>

</tr>

<tr>

<td>[CVE-2014-8602](https://access.redhat.com/security/cve/CVE-2014-8602) [templink](https://unbound.net/downloads/CVE-2014-8602.txt)</td>

<td>[unbound](https://www.archlinux.org/packages/?name=unbound)</td>

<td>2014-12-09</td>

<td><= 1.5.0-1</td>

<td>1.5.1-1</td>

<td><1d</td>

<td>Fixed</td>

<td>[ASA-201412-8](https://lists.archlinux.org/pipermail/arch-security/2014-December/000166.html)</td>

</tr>

<tr>

<td>[CVE-2014-8500](https://access.redhat.com/security/cve/CVE-2014-8500) [CVE-2014-8680](https://access.redhat.com/security/cve/CVE-2014-8680) [templink](http://svnweb.freebsd.org/ports?view=revision&revision=374305)</td>

<td>[bind](https://www.archlinux.org/packages/?name=bind)</td>

<td>2014-12-08</td>

<td><= 9.10.1-2</td>

<td>9.10.1.P1-1</td>

<td><1d</td>

<td>Fixed</td>

<td>[ASA-201412-7](https://lists.archlinux.org/pipermail/arch-security/2014-December/000165.html)</td>

</tr>

<tr>

<td>[CVE-2014-9274](https://access.redhat.com/security/cve/CVE-2014-9274) [CVE-2014-9275](https://access.redhat.com/security/cve/CVE-2014-9275) [templink](http://seclists.org/oss-sec/2014/q4/904)</td>

<td>[unrtf](https://www.archlinux.org/packages/?name=unrtf)</td>

<td>2014-12-04</td>

<td><= 0.21.5-1</td>

<td>0.21.7-1</td>

<td>10d</td>

<td>Fixed ([FS#43131](https://bugs.archlinux.org/task/43131))</td>

<td>[ASA-201412-20](https://lists.archlinux.org/pipermail/arch-security/2014-December/000178.html)</td>

</tr>

<tr>

<td>[CVE-2014-1587](https://access.redhat.com/security/cve/CVE-2014-1587) [CVE-2014-1588](https://access.redhat.com/security/cve/CVE-2014-1588) [CVE-2014-1589](https://access.redhat.com/security/cve/CVE-2014-1589) [CVE-2014-1590](https://access.redhat.com/security/cve/CVE-2014-1590) [CVE-2014-1591](https://access.redhat.com/security/cve/CVE-2014-1591) [CVE-2014-1592](https://access.redhat.com/security/cve/CVE-2014-1592) [CVE-2014-1593](https://access.redhat.com/security/cve/CVE-2014-1593) [CVE-2014-1594](https://access.redhat.com/security/cve/CVE-2014-1594) [CVE-2014-8631](https://access.redhat.com/security/cve/CVE-2014-8631) [CVE-2014-8632](https://access.redhat.com/security/cve/CVE-2014-8632) [templink](https://www.mozilla.org/fr/security/known-vulnerabilities/firefox/)</td>

<td>[firefox](https://www.archlinux.org/packages/?name=firefox)</td>

<td>2014-12-02</td>

<td><= 33.1.1-1</td>

<td>34.0.5-1</td>

<td>< 1d</td>

<td>Fixed</td>

<td>[ASA-201412-3](https://lists.archlinux.org/pipermail/arch-security/2014-December/000161.html)</td>

</tr>

<tr>

<td>[CVE-2014-9157](https://access.redhat.com/security/cve/CVE-2014-9157) [templink](http://seclists.org/oss-sec/2014/q4/872)</td>

<td>[graphviz](https://www.archlinux.org/packages/?name=graphviz)</td>

<td>2014-11-25</td>

<td><= 2.38.0-2</td>

<td>2.38.0-3</td>

<td>8d</td>

<td>Fixed ([FS#42983](https://bugs.archlinux.org/task/42983))</td>

<td>[ASA-201412-4](https://lists.archlinux.org/pipermail/arch-security/2014-December/000162.html)</td>

</tr>

<tr>

<td>[CVE-2014-8123](https://access.redhat.com/security/cve/CVE-2014-8123) [templink](http://seclists.org/oss-sec/2014/q4/874)</td>

<td>[antiword](https://www.archlinux.org/packages/?name=antiword)</td>

<td>2014-12-01</td>

<td><= 0.37-4</td>

<td>0.37-5</td>

<td>3d</td>

<td>Fixed ([FS#42982](https://bugs.archlinux.org/task/42982))</td>

<td>[ASA-201412-5](https://lists.archlinux.org/pipermail/arch-security/2014-December/000163.html)</td>

</tr>

<tr>

<td>[CVE-2014-8104](https://access.redhat.com/security/cve/CVE-2014-8104) [templink](https://forums.openvpn.net/topic17625.html)</td>

<td>[openvpn](https://www.archlinux.org/packages/?name=openvpn)</td>

<td>2014-11-30</td>

<td><= 2.3.5-1</td>

<td>2.3.6-1</td>

<td>4d</td>

<td>Fixed ([FS#42975](https://bugs.archlinux.org/task/42975))</td>

<td>[ASA-201412-2](https://lists.archlinux.org/pipermail/arch-security/2014-December/000160.html)</td>

</tr>

<tr>

<td>[CVE-2014-9087](https://access.redhat.com/security/cve/CVE-2014-9087) [templink](http://seclists.org/oss-sec/2014/q4/801)</td>

<td>[gnupg](https://www.archlinux.org/packages/?name=gnupg)</td>

<td>2014-11-25</td>

<td><= 2.1.0-5</td>

<td>2.1.0-6</td>

<td>4d</td>

<td>Fixed ([FS#42943](https://bugs.archlinux.org/task/42943))</td>

<td>[ASA-201412-1](https://lists.archlinux.org/pipermail/arch-security/2014-December/000159.html)</td>

</tr>

<tr>

<td>[CVE-2014-9087](https://access.redhat.com/security/cve/CVE-2014-9087) [templink](http://seclists.org/oss-sec/2014/q4/801)</td>

<td>[libksba](https://www.archlinux.org/packages/?name=libksba)</td>

<td>2014-11-25</td>

<td><= 1.3.1-1</td>

<td>1.3.2-1</td>

<td><1d</td>

<td>Fixed</td>

<td>[ASA-201411-31](https://lists.archlinux.org/pipermail/arch-security/2014-November/000156.html)</td>

</tr>

<tr>

<td>[CVE-2014-9114](https://access.redhat.com/security/cve/CVE-2014-9114) [templink](http://seclists.org/oss-sec/2014/q4/819)</td>

<td>[util-linux](https://www.archlinux.org/packages/?name=util-linux)</td>

<td>2014-11-27</td>

<td><= 2.25.2-1</td>

<td>2.26.1-3</td>

<td>117d</td>

<td>Fixed ([FS#43886](https://bugs.archlinux.org/task/43886))</td>

<td>[ASA-201503-23](https://lists.archlinux.org/pipermail/arch-security/2015-March/000264.html)</td>

</tr>

<tr>

<td>[CVE-2014-9112](https://access.redhat.com/security/cve/CVE-2014-9112) [templink](http://seclists.org/oss-sec/2014/q4/818)</td>

<td>[cpio](https://www.archlinux.org/packages/?name=cpio)</td>

<td>2014-11-26</td>

<td><= 2.11-4</td>

<td>2.11-5</td>

<td>20d</td>

<td>Fixed</td>

<td>[ASA-201501-5](https://lists.archlinux.org/pipermail/arch-security/2015-January/000201.html)</td>

</tr>

<tr>

<td>[CVE-2014-9116](https://access.redhat.com/security/cve/CVE-2014-9116) [templink](http://seclists.org/oss-sec/2014/q4/835)</td>

<td>[mutt](https://www.archlinux.org/packages/?name=mutt)</td>

<td>2014-11-27</td>

<td><= 1.5.23-1</td>

<td>1.5.23-2</td>

<td>71d</td>

<td>Fixed ([FS#44110](https://bugs.archlinux.org/task/44110))</td>

<td>[ASA-201503-6](https://lists.archlinux.org/pipermail/arch-security/2015-March/000247.html)</td>

</tr>

<tr>

<td>[CVE-2014-9093](https://access.redhat.com/security/cve/CVE-2014-9093) [templink](https://bugs.freedesktop.org/show_bug.cgi?id=86449)</td>

<td>[libreoffice-fresh](https://www.archlinux.org/packages/?name=libreoffice-fresh)</td>

<td>2014-11-19</td>

<td><= 4.3.4-1</td>

<td>4.3.5-1</td>

<td>31d</td>

<td>Fixed</td>

<td>None</td>

</tr>

<tr>

<td>[CVE-2014-9092](https://access.redhat.com/security/cve/CVE-2014-9092) [templink](https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=768369#114)</td>

<td>[libjpeg-turbo](https://www.archlinux.org/packages/?name=libjpeg-turbo)</td>

<td>2014-11-26</td>

<td><= 1.3.1-2</td>

<td>1.3.1-3</td>

<td>2d</td>

<td>Fixed ([FS#42922](https://bugs.archlinux.org/task/42922))</td>

<td>[ASA-201411-33](https://lists.archlinux.org/pipermail/arch-security/2014-November/000158.html)</td>

</tr>

<tr>

<td>[CVE-2014-9272](https://access.redhat.com/security/cve/CVE-2014-9272) [CVE-2014-9270](https://access.redhat.com/security/cve/CVE-2014-9270) [CVE-2014-8987](https://access.redhat.com/security/cve/CVE-2014-8987) [CVE-2014-9271](https://access.redhat.com/security/cve/CVE-2014-9271) [CVE-2014-9281](https://access.redhat.com/security/cve/CVE-2014-9281) [CVE-2014-8986](https://access.redhat.com/security/cve/CVE-2014-8986) [CVE-2014-9269](https://access.redhat.com/security/cve/CVE-2014-9269) [CVE-2014-9280](https://access.redhat.com/security/cve/CVE-2014-9280) [CVE-2014-9089](https://access.redhat.com/security/cve/CVE-2014-9089) [CVE-2014-9279](https://access.redhat.com/security/cve/CVE-2014-9279) [CVE-2014-8988](https://access.redhat.com/security/cve/CVE-2014-8988) [CVE-2014-8553](https://access.redhat.com/security/cve/CVE-2014-8553) [CVE-2014-6387](https://access.redhat.com/security/cve/CVE-2014-6387) [CVE-2014-6316](https://access.redhat.com/security/cve/CVE-2014-6316) [CVE-2014-9117](https://access.redhat.com/security/cve/CVE-2014-9117) [templink](https://www.mantisbt.org/bugs/view.php?id=17841) [templink](https://www.mantisbt.org/bugs/view.php?id=17811) [templink](http://seclists.org/oss-sec/2014/q4/955)</td>

<td>[mantisbt](https://www.archlinux.org/packages/?name=mantisbt)</td>

<td>2014-11-25</td>

<td><= 1.2.17-4</td>

<td>1.2.18-1</td>

<td>13d</td>

<td>Fixed ([FS#42920](https://bugs.archlinux.org/task/42920))</td>

<td>[ASA-201412-6](https://lists.archlinux.org/pipermail/arch-security/2014-December/000164.html)</td>

</tr>

<tr>

<td>[CVE-2014-9090](https://access.redhat.com/security/cve/CVE-2014-9090) [templink](https://marc.info/?l=oss-security&m=141698775601426&w=2)</td>

<td>[linux](https://www.archlinux.org/packages/?name=linux) [linux-lts](https://www.archlinux.org/packages/?name=linux-lts)</td>

<td>2014-11-26</td>

<td><= 3.18-rc6</td>

<td>3.19</td>

<td>-</td>

<td>Invalid</td>

<td>None</td>

</tr>

<tr>

<td>[CVE-2014-9018](https://access.redhat.com/security/cve/CVE-2014-9018) [CVE-2014-9091](https://access.redhat.com/security/cve/CVE-2014-9091) [templink](http://seclists.org/oss-sec/2014/q4/694)</td>

<td>[icecast](https://www.archlinux.org/packages/?name=icecast)</td>

<td>2014-11-20</td>

<td><= 2.4.0-1</td>

<td>2.4.1-1</td>

<td>8d</td>

<td>Fixed ([FS#42912](https://bugs.archlinux.org/task/42912))</td>

<td>[ASA-201411-32](https://lists.archlinux.org/pipermail/arch-security/2014-November/000157.html)</td>

</tr>

<tr>

<td>[CVE-2014-8964](https://access.redhat.com/security/cve/CVE-2014-8964) [templink](http://bugs.exim.org/show_bug.cgi?id=1546)</td>

<td>[pcre](https://www.archlinux.org/packages/?name=pcre)</td>

<td>2014-11-18</td>

<td><= 8.36-1</td>

<td>8.36-2</td>

<td>8d</td>

<td>Fixed ([FS#42860](https://bugs.archlinux.org/task/42860))</td>

<td>[ASA-201411-29](https://lists.archlinux.org/pipermail/arch-security/2014-November/000154.html)</td>

</tr>

<tr>

<td>[CVE-2014-8962](https://access.redhat.com/security/cve/CVE-2014-8962) [CVE-2014-9028](https://access.redhat.com/security/cve/CVE-2014-9028) [templink](http://www.ocert.org/advisories/ocert-2014-008.html)</td>

<td>[flac](https://www.archlinux.org/packages/?name=flac)</td>

<td>2014-11-25</td>

<td><= 1.3.0-4</td>

<td>1.3.0-5</td>

<td>< 1d</td>

<td>Fixed ([FS#42898](https://bugs.archlinux.org/task/42898))</td>

<td>[ASA-201411-30](https://lists.archlinux.org/pipermail/arch-security/2014-November/000155.html)</td>

</tr>

<tr>

<td>[CVE-2014-7899](https://access.redhat.com/security/cve/CVE-2014-7899) [CVE-2014-7900](https://access.redhat.com/security/cve/CVE-2014-7900) [CVE-2014-7901](https://access.redhat.com/security/cve/CVE-2014-7901) [CVE-2014-7902](https://access.redhat.com/security/cve/CVE-2014-7902) [CVE-2014-7903](https://access.redhat.com/security/cve/CVE-2014-7903) [CVE-2014-7904](https://access.redhat.com/security/cve/CVE-2014-7904) [CVE-2014-7906](https://access.redhat.com/security/cve/CVE-2014-7906) [CVE-2014-7907](https://access.redhat.com/security/cve/CVE-2014-7907) [CVE-2014-7908](https://access.redhat.com/security/cve/CVE-2014-7908) [CVE-2014-7909](https://access.redhat.com/security/cve/CVE-2014-7909) [CVE-2014-7910](https://access.redhat.com/security/cve/CVE-2014-7910) [templink](http://googlechromereleases.blogspot.in/2014/11/stable-channel-update_18.html)</td>

<td>[chromium](https://www.archlinux.org/packages/?name=chromium)</td>

<td>2014-11-20</td>

<td><= 38.0.2125.122-1</td>

<td>39.0.2171.65-1</td>

<td><1d</td>

<td>Fixed</td>

<td>[ASA-201411-26](https://lists.archlinux.org/pipermail/arch-security/2014-November/000151.html)</td>

</tr>

<tr>

<td>[CVE-2014-9015](https://access.redhat.com/security/cve/CVE-2014-9015) [CVE-2014-9016](https://access.redhat.com/security/cve/CVE-2014-9016) [templink](http://seclists.org/oss-sec/2014/q4/697)</td>

<td>[drupal](https://www.archlinux.org/packages/?name=drupal)</td>

<td>2014-11-19</td>

<td><= 7.33-1</td>

<td>7.34-1</td>

<td><1d</td>

<td>Fixed</td>

<td>[ASA-201411-25](https://lists.archlinux.org/pipermail/arch-security/2014-November/000150.html)</td>

</tr>

<tr>

<td>[CVE-2013-6497](https://access.redhat.com/security/cve/CVE-2013-6497) [templink](http://seclists.org/oss-sec/2014/q4/673)</td>

<td>[clamav](https://www.archlinux.org/packages/?name=clamav)</td>

<td>2014-11-18</td>

<td><= 0.98.4-1</td>

<td>0.98.5-1</td>

<td>1d</td>

<td>Fixed</td>

<td>[ASA-201411-21](https://lists.archlinux.org/pipermail/arch-security/2014-November/000146.html)</td>

</tr>

<tr>

<td>[CVE-2014-7817](https://access.redhat.com/security/cve/CVE-2014-7817) [templink](https://sourceware.org/bugzilla/show_bug.cgi?id=17625)</td>

<td>[glibc](https://www.archlinux.org/packages/?name=glibc) [lib32-glibc](https://www.archlinux.org/packages/?name=lib32-glibc)</td>

<td>2014-11-19</td>

<td><= 2.20-2</td>

<td>2.20.3</td>

<td>2d</td>

<td>Fixed</td>

<td>[ASA-201411-27](https://lists.archlinux.org/pipermail/arch-security/2014-November/000152.html)</td>

</tr>

<tr>

<td>[CVE-2014-8600](https://access.redhat.com/security/cve/CVE-2014-8600) [templink](https://www.kde.org/info/security/advisory-20141113-1.txt)</td>

<td>[kwebkitpart](https://www.archlinux.org/packages/?name=kwebkitpart)</td>

<td>2014-11-18</td>

<td><= 1.3.4-2</td>

<td>1.3.4-3</td>

<td>4d</td>

<td>Fixed ([FS#44170](https://bugs.archlinux.org/task/44170) [FS#42775](https://bugs.archlinux.org/task/42775))</td>

<td>None</td>

</tr>

<tr>

<td>[CVE-2014-8767](https://access.redhat.com/security/cve/CVE-2014-8767) [CVE-2014-8768](https://access.redhat.com/security/cve/CVE-2014-8768) [CVE-2014-8769](https://access.redhat.com/security/cve/CVE-2014-8769) [CVE-2014-9140](https://access.redhat.com/security/cve/CVE-2014-9140) [CVE-2015-0261](https://access.redhat.com/security/cve/CVE-2015-0261) [CVE-2015-2153](https://access.redhat.com/security/cve/CVE-2015-2153) [CVE-2015-2154](https://access.redhat.com/security/cve/CVE-2015-2154) [CVE-2015-2155](https://access.redhat.com/security/cve/CVE-2015-2155) [templink](http://www.securityfocus.com/archive/1/534011/30/0/threaded) [templink](http://www.securityfocus.com/archive/1/534010/30/0/threaded) [templink](http://www.securityfocus.com/archive/1/534009/30/0/threaded) [templink](https://github.com/the-tcpdump-group/tcpdump/commit/0f95d441e4b5d7512cc5c326c8668a120e048eda)</td>

<td>[tcpdump](https://www.archlinux.org/packages/?name=tcpdump)</td>

<td>2014-11-18</td>

<td><= 4.6.2-1</td>

<td>4.7.3-1</td>

<td>88d</td>

<td>Fixed ([FS#44153](https://bugs.archlinux.org/task/44153))</td>

<td>[ASA-201503-20](https://lists.archlinux.org/pipermail/arch-security/2015-March/000261.html)</td>

</tr>

<tr>

<td>[CVE-2014-8090](https://access.redhat.com/security/cve/CVE-2014-8090)</td>

<td>[ruby](https://www.archlinux.org/packages/?name=ruby)</td>

<td>2014-11-13</td>

<td><= 2.1.4-1</td>

<td>2.1.5-1</td>

<td>1d</td>

<td>Fixed</td>

<td>[ASA-201411-16](https://lists.archlinux.org/pipermail/arch-security/2014-November/000141.html)</td>

</tr>

<tr>

<td>[CVE-2014-7823](https://access.redhat.com/security/cve/CVE-2014-7823)</td>

<td>[libvirt](https://www.archlinux.org/packages/?name=libvirt)</td>

<td>2014-11-13</td>

<td><= 1.2.10-1</td>

<td>1.2.11-1</td>

<td>33d</td>

<td>Fixed</td>

<td>None</td>

</tr>

<tr>

<td>[CVE-2014-8710](https://access.redhat.com/security/cve/CVE-2014-8710) [CVE-2014-8711](https://access.redhat.com/security/cve/CVE-2014-8711) [CVE-2014-8712](https://access.redhat.com/security/cve/CVE-2014-8712) [CVE-2014-8713](https://access.redhat.com/security/cve/CVE-2014-8713) [CVE-2014-8714](https://access.redhat.com/security/cve/CVE-2014-8714) [templink](https://www.wireshark.org/security/wnpa-sec-2014-20.html) [templink](https://www.wireshark.org/security/wnpa-sec-2014-21.html) [templink](https://www.wireshark.org/security/wnpa-sec-2014-22.html)</td>

<td>[wireshark-cli](https://www.archlinux.org/packages/?name=wireshark-cli) [wireshark-gtk](https://www.archlinux.org/packages/?name=wireshark-gtk) [wireshark-qt](https://www.archlinux.org/packages/?name=wireshark-qt)</td>

<td>2014-11-13</td>

<td><= 1.12.1-1</td>

<td>1.12.2-1</td>

<td>7d</td>

<td>Fixed</td>

<td>[ASA-201411-22](https://lists.archlinux.org/pipermail/arch-security/2014-November/000147.html) [ASA-201411-23](https://lists.archlinux.org/pipermail/arch-security/2014-November/000148.html) [ASA-201411-24](https://lists.archlinux.org/pipermail/arch-security/2014-November/000149.html)</td>

</tr>

<tr>

<td>[CVE-2014-0573](https://access.redhat.com/security/cve/CVE-2014-0573) [CVE-2014-0574](https://access.redhat.com/security/cve/CVE-2014-0574) [CVE-2014-0576](https://access.redhat.com/security/cve/CVE-2014-0576) [CVE-2014-0577](https://access.redhat.com/security/cve/CVE-2014-0577) [CVE-2014-0581](https://access.redhat.com/security/cve/CVE-2014-0581) [CVE-2014-0582](https://access.redhat.com/security/cve/CVE-2014-0582) [CVE-2014-0583](https://access.redhat.com/security/cve/CVE-2014-0583) [CVE-2014-0584](https://access.redhat.com/security/cve/CVE-2014-0584) [CVE-2014-0585](https://access.redhat.com/security/cve/CVE-2014-0585) [CVE-2014-0586](https://access.redhat.com/security/cve/CVE-2014-0586) [CVE-2014-0588](https://access.redhat.com/security/cve/CVE-2014-0588) [CVE-2014-0589](https://access.redhat.com/security/cve/CVE-2014-0589) [CVE-2014-0590](https://access.redhat.com/security/cve/CVE-2014-0590) [CVE-2014-8437](https://access.redhat.com/security/cve/CVE-2014-8437) [CVE-2014-8438](https://access.redhat.com/security/cve/CVE-2014-8438) [CVE-2014-8440](https://access.redhat.com/security/cve/CVE-2014-8440) [CVE-2014-8441](https://access.redhat.com/security/cve/CVE-2014-8441) [CVE-2014-8442](https://access.redhat.com/security/cve/CVE-2014-8442) [templink](https://helpx.adobe.com/security/products/flash-player/apsb14-24.html)</td>

<td>[flashplugin](https://www.archlinux.org/packages/?name=flashplugin)</td>

<td>2014-11-11</td>

<td><= 11.2.202.411-1</td>

<td>11.2.202.418-1</td>

<td><1d</td>

<td>Fixed ([FS#42769](https://bugs.archlinux.org/task/42769))</td>

<td>[ASA-201411-11](https://lists.archlinux.org/pipermail/arch-security/2014-November/000136.html)</td>

</tr>

<tr>

<td>[CVE-2014-3710](https://access.redhat.com/security/cve/CVE-2014-3710) [templink](https://bugzilla.redhat.com/show_bug.cgi?id=1155071)</td>

<td>[php](https://www.archlinux.org/packages/?name=php)</td>

<td>2014-10-29</td>

<td><= 5.6.2-2</td>

<td>5.6.3-1</td>

<td>14d</td>

<td>Fixed ([FS#42764](https://bugs.archlinux.org/task/42764))</td>

<td>[ASA-201411-13](https://lists.archlinux.org/pipermail/arch-security/2014-November/000138.html)</td>

</tr>

<tr>

<td>[CVE-2014-8564](https://access.redhat.com/security/cve/CVE-2014-8564) [templink](http://www.gnutls.org/security.html#GNUTLS-SA-2014-5)</td>

<td>[gnutls](https://www.archlinux.org/packages/?name=gnutls)</td>

<td>2014-11-10</td>

<td><= 3.3.9-1</td>

<td>3.3.10-1</td>

<td><1d</td>

<td>Fixed</td>

<td>[ASA-201411-10](https://lists.archlinux.org/pipermail/arch-security/2014-November/000135.html)</td>

</tr>

<tr>

<td>[CVE-2014-8716](https://access.redhat.com/security/cve/CVE-2014-8716) [templink](http://seclists.org/oss-sec/2014/q4/591)</td>

<td>[imagemagick](https://www.archlinux.org/packages/?name=imagemagick)</td>

<td>2014-11-12</td>

<td><= 6.8.9.9-1</td>

<td>6.8.9.10-1</td>

<td>1d</td>

<td>Fixed</td>

<td>[ASA-201411-12](https://lists.archlinux.org/pipermail/arch-security/2014-November/000137.html)</td>

</tr>

<tr>

<td>[CVE-2014-3710](https://access.redhat.com/security/cve/CVE-2014-3710) [templink](https://bugzilla.redhat.com/show_bug.cgi?id=1155071)</td>

<td>[file](https://www.archlinux.org/packages/?name=file)</td>

<td>2014-10-29</td>

<td><= 5.20-1</td>

<td>5.20-2</td>

<td>12d</td>

<td>Fixed ([FS#42759](https://bugs.archlinux.org/task/42759))</td>

<td>[ASA-201411-9](https://lists.archlinux.org/pipermail/arch-security/2014-November/000134.html)</td>

</tr>

<tr>

<td>[CVE-2014-1569](https://access.redhat.com/security/cve/CVE-2014-1569) [templink](https://bugzilla.mozilla.org/show_bug.cgi?id=1064670)</td>

<td>[nss](https://www.archlinux.org/packages/?name=nss)</td>

<td>2014-11-07</td>

<td><= 3.17.2-1</td>

<td>3.17.3-1</td>

<td>22d</td>

<td>Fixed ([FS#42760](https://bugs.archlinux.org/task/42760))</td>

<td>[ASA-201412-18](https://lists.archlinux.org/pipermail/arch-security/2014-December/000176.html)</td>

</tr>

<tr>

<td>[CVE-2014-7824](https://access.redhat.com/security/cve/CVE-2014-7824) [templink](http://www.openwall.com/lists/oss-security/2014/11/10/2)</td>

<td>[dbus](https://www.archlinux.org/packages/?name=dbus)</td>

<td>2014-11-10</td>

<td><= 1.8.8-1</td>

<td>1.8.10-1</td>

<td>14d</td>

<td>Fixed</td>

<td>[ASA-201411-28](https://lists.archlinux.org/pipermail/arch-security/2014-November/000153.html)</td>

</tr>

<tr>

<td>[CVE-2014-8598](https://access.redhat.com/security/cve/CVE-2014-8598) [CVE-2014-7146](https://access.redhat.com/security/cve/CVE-2014-7146) [templink](http://www.openwall.com/lists/oss-security/2014/11/07/27) [templink](http://www.openwall.com/lists/oss-security/2014/11/07/28)</td>

<td>[mantisbt](https://www.archlinux.org/packages/?name=mantisbt)</td>

<td>2014-11-08</td>

<td><= 1.2.17-3</td>

<td>1.2.17-4</td>

<td><4d</td>

<td>Fixed ([FS#42761](https://bugs.archlinux.org/task/42761))</td>

<td>[ASA-201411-8](https://lists.archlinux.org/pipermail/arch-security/2014-November/000133.html)</td>

</tr>

<tr>

<td>[CVE-2014-8483](https://access.redhat.com/security/cve/CVE-2014-8483) [templink](https://www.kde.org/info/security/advisory-20141104-1.txt)</td>

<td>[konversation](https://www.archlinux.org/packages/?name=konversation)</td>

<td>2014-11-04</td>

<td><= 1.5-1</td>

<td>1.5.1-1</td>

<td><4d</td>

<td>Fixed ([FS#42698](https://bugs.archlinux.org/task/42698))</td>

<td>[ASA-201411-5](https://lists.archlinux.org/pipermail/arch-security/2014-November/000130.html)</td>

</tr>

<tr>

<td>[CVE-2014-3707](https://access.redhat.com/security/cve/CVE-2014-3707) [templink](http://curl.haxx.se/docs/adv_20141105.html)</td>

<td>[curl](https://www.archlinux.org/packages/?name=curl)</td>

<td>2014-11-05</td>

<td><= 7.38.0-3</td>

<td>7.39.0-1</td>

<td>6d</td>

<td>Fixed</td>

<td>[ASA-201411-7](https://lists.archlinux.org/pipermail/arch-security/2014-November/000132.html)</td>

</tr>

<tr>

<td>[CVE-2014-8651](https://access.redhat.com/security/cve/CVE-2014-8651) [templink](http://seclists.org/oss-sec/2014/q4/520)</td>

<td>[kdebase-workspace](https://www.archlinux.org/packages/?name=kdebase-workspace)</td>

<td>2014-11-04</td>

<td><= 4.11.13-1</td>

<td>4.11.13-2</td>

<td>6d</td>

<td>Fixed ([FS#42679](https://bugs.archlinux.org/task/42679))</td>

<td>[ASA-201411-6](https://lists.archlinux.org/pipermail/arch-security/2014-November/000131.html)</td>

</tr>

<tr>

<td>[CVE-2014-8627](https://access.redhat.com/security/cve/CVE-2014-8627) [CVE-2014-8628](https://access.redhat.com/security/cve/CVE-2014-8628) [templink](http://www.openwall.com/lists/oss-security/2014/11/04/6)</td>

<td>[polarssl](https://www.archlinux.org/packages/?name=polarssl)</td>

<td>2014-10-23</td>

<td><= 1.3.8-3</td>

<td>1.3.9-1</td>

<td>11d</td>

<td>Fixed</td>

<td>[ASA-201411-4](https://lists.archlinux.org/pipermail/arch-security/2014-November/000129.html)</td>

</tr>

<tr>

<td>[CVE-2014-8321](https://access.redhat.com/security/cve/CVE-2014-8321) [CVE-2014-8322](https://access.redhat.com/security/cve/CVE-2014-8322) [CVE-2014-8323](https://access.redhat.com/security/cve/CVE-2014-8323) [CVE-2014-8324](https://access.redhat.com/security/cve/CVE-2014-8324) [templink](http://www.securityfocus.com/archive/1/533869/30/0/threaded)</td>

<td>[aircrack-ng](https://www.archlinux.org/packages/?name=aircrack-ng)</td>

<td>2014-11-02</td>

<td><= 1.2beta3-1</td>

<td>1.2rc1-1</td>

<td>1d</td>

<td>Fixed</td>

<td>[ASA-201411-2](https://lists.archlinux.org/pipermail/arch-security/2014-November/000127.html)</td>

</tr>

<tr>

<td>[CVE-2014-8554](https://access.redhat.com/security/cve/CVE-2014-8554) [templink](http://www.openwall.com/lists/oss-security/2014/10/30/9)</td>

<td>[mantisbt](https://www.archlinux.org/packages/?name=mantisbt)</td>

<td>2014-10-30</td>

<td><= 1.2.17-2</td>

<td>1.2.17-3</td>

<td>5d</td>

<td>Fixed ([FS#42683](https://bugs.archlinux.org/task/42683))</td>

<td>[ASA-201411-3](https://lists.archlinux.org/pipermail/arch-security/2014-November/000128.html)</td>

</tr>

<tr>

<td>[CVE-2014-8354](https://access.redhat.com/security/cve/CVE-2014-8354) [CVE-2014-8355](https://access.redhat.com/security/cve/CVE-2014-8355) [CVE-2014-8561](https://access.redhat.com/security/cve/CVE-2014-8561) [CVE-2014-8562](https://access.redhat.com/security/cve/CVE-2014-8562) [templink](http://seclists.org/oss-sec/2014/q4/466)</td>

<td>[imagemagick](https://www.archlinux.org/packages/?name=imagemagick)</td>

<td>2014-10-29</td>

<td><= 6.8.9.8-1</td>

<td>6.8.9.9-1</td>

<td><1d</td>

<td>Fixed</td>

<td>None</td>

</tr>

<tr>

<td>[CVE-2014-8517](https://access.redhat.com/security/cve/CVE-2014-8517) [templink](http://seclists.org/oss-sec/2014/q4/459)</td>

<td>[tnftp](https://www.archlinux.org/packages/?name=tnftp)</td>

<td>2014-10-28</td>

<td><= 20130505-2</td>

<td>20141031-1</td>

<td>4d</td>

<td>Fixed ([FS#42646](https://bugs.archlinux.org/task/42646))</td>

<td>[ASA-201411-1](https://lists.archlinux.org/pipermail/arch-security/2014-November/000126.html)</td>

</tr>

<tr>

<td>[CVE-2014-4877](https://access.redhat.com/security/cve/CVE-2014-4877) [templink](http://git.savannah.gnu.org/cgit/wget.git/commit/?id=18b0979357ed7dc4e11d4f2b1d7e0f5932d82aa7)</td>

<td>[wget](https://www.archlinux.org/packages/?name=wget)</td>

<td>2014-10-27</td>

<td><= 1.15-1</td>

<td>1.16-1</td>

<td><2d</td>

<td>Fixed</td>

<td>[ASA-201410-14](https://lists.archlinux.org/pipermail/arch-security/2014-October/000125.html)</td>

</tr>

<tr>

<td>[CVE-2014-8484](https://access.redhat.com/security/cve/CVE-2014-8484) [CVE-2014-8485](https://access.redhat.com/security/cve/CVE-2014-8485) [CVE-2014-8501](https://access.redhat.com/security/cve/CVE-2014-8501) [CVE-2014-8502](https://access.redhat.com/security/cve/CVE-2014-8502) [CVE-2014-8503](https://access.redhat.com/security/cve/CVE-2014-8503) [CVE-2014-8504](https://access.redhat.com/security/cve/CVE-2014-8504) [CVE-2014-8737](https://access.redhat.com/security/cve/CVE-2014-8737) [CVE-2014-8738](https://access.redhat.com/security/cve/CVE-2014-8738) [templink](http://seclists.org/oss-sec/2014/q4/424) [tmplink](http://seclists.org/oss-sec/2014/q4/599) [templink](http://seclists.org/oss-sec/2014/q4/600)</td>

<td>[avr-binutils](https://www.archlinux.org/packages/?name=avr-binutils)</td>

<td>2014-10-23</td>

<td><= 2.24-2</td>

<td>2.24-3</td>

<td>27d</td>

<td>Fixed ([FS#42773](https://bugs.archlinux.org/task/42773))</td>

<td>[ASA-201411-20](https://lists.archlinux.org/pipermail/arch-security/2014-November/000145.html)</td>

</tr>

<tr>

<td>[CVE-2014-8484](https://access.redhat.com/security/cve/CVE-2014-8484) [CVE-2014-8485](https://access.redhat.com/security/cve/CVE-2014-8485) [CVE-2014-8501](https://access.redhat.com/security/cve/CVE-2014-8501) [CVE-2014-8502](https://access.redhat.com/security/cve/CVE-2014-8502) [CVE-2014-8503](https://access.redhat.com/security/cve/CVE-2014-8503) [CVE-2014-8504](https://access.redhat.com/security/cve/CVE-2014-8504) [CVE-2014-8737](https://access.redhat.com/security/cve/CVE-2014-8737) [CVE-2014-8738](https://access.redhat.com/security/cve/CVE-2014-8738) [templink](http://seclists.org/oss-sec/2014/q4/424) [tmplink](http://seclists.org/oss-sec/2014/q4/599) [templink](http://seclists.org/oss-sec/2014/q4/600)</td>

<td>[mingw-w64-binutils](https://www.archlinux.org/packages/?name=mingw-w64-binutils)</td>

<td>2014-10-23</td>

<td><= 2.24-1</td>

<td>2.24-2</td>

<td>26d</td>

<td>Fixed ([FS#42773](https://bugs.archlinux.org/task/42773))</td>

<td>[ASA-201411-19](https://lists.archlinux.org/pipermail/arch-security/2014-November/000144.html)</td>

</tr>

<tr>

<td>[CVE-2014-8484](https://access.redhat.com/security/cve/CVE-2014-8484) [CVE-2014-8485](https://access.redhat.com/security/cve/CVE-2014-8485) [CVE-2014-8501](https://access.redhat.com/security/cve/CVE-2014-8501) [CVE-2014-8502](https://access.redhat.com/security/cve/CVE-2014-8502) [CVE-2014-8503](https://access.redhat.com/security/cve/CVE-2014-8503) [CVE-2014-8504](https://access.redhat.com/security/cve/CVE-2014-8504) [CVE-2014-8737](https://access.redhat.com/security/cve/CVE-2014-8737) [CVE-2014-8738](https://access.redhat.com/security/cve/CVE-2014-8738) [templink](http://seclists.org/oss-sec/2014/q4/424) [tmplink](http://seclists.org/oss-sec/2014/q4/599) [templink](http://seclists.org/oss-sec/2014/q4/600)</td>

<td>[arm-none-eabi-binutils](https://www.archlinux.org/packages/?name=arm-none-eabi-binutils)</td>

<td>2014-10-23</td>

<td><= 2.24-2</td>

<td>2.24-3</td>

<td>26d</td>

<td>Fixed ([FS#42773](https://bugs.archlinux.org/task/42773))</td>

<td>[ASA-201411-18](https://lists.archlinux.org/pipermail/arch-security/2014-November/000143.html)</td>

</tr>

<tr>

<td>[CVE-2014-8484](https://access.redhat.com/security/cve/CVE-2014-8484) [CVE-2014-8485](https://access.redhat.com/security/cve/CVE-2014-8485) [CVE-2014-8501](https://access.redhat.com/security/cve/CVE-2014-8501) [CVE-2014-8502](https://access.redhat.com/security/cve/CVE-2014-8502) [CVE-2014-8503](https://access.redhat.com/security/cve/CVE-2014-8503) [CVE-2014-8504](https://access.redhat.com/security/cve/CVE-2014-8504) [CVE-2014-8737](https://access.redhat.com/security/cve/CVE-2014-8737) [CVE-2014-8738](https://access.redhat.com/security/cve/CVE-2014-8738) [templink](http://seclists.org/oss-sec/2014/q4/424) [tmplink](http://seclists.org/oss-sec/2014/q4/599) [templink](http://seclists.org/oss-sec/2014/q4/600)</td>

<td>[binutils](https://www.archlinux.org/packages/?name=binutils)</td>

<td>2014-10-23</td>

<td><= 2.24-7</td>

<td>2.24-8</td>

<td>26d</td>

<td>Fixed ([FS#42773](https://bugs.archlinux.org/task/42773))</td>

<td>[ASA-201411-17](https://lists.archlinux.org/pipermail/arch-security/2014-November/000142.html)</td>

</tr>

<tr>

<td>[CVE-2014-8559](https://access.redhat.com/security/cve/CVE-2014-8559) [templink](http://www.openwall.com/lists/oss-security/2014/10/30/7)</td>

<td>[linux](https://www.archlinux.org/packages/?name=linux), [linux-lts](https://www.archlinux.org/packages/?name=linux-lts)</td>

<td>2014-10-30</td>

<td><= 3.17.3-1, <= 3.14.24-1</td>

<td>3.17.4-1 3.14.25-1</td>

<td>23d 22d</td>

<td>Fixed</td>

<td>None</td>

</tr>

<tr>

<td>[CVE-2014-3610](https://access.redhat.com/security/cve/CVE-2014-3610) [CVE-2014-3611](https://access.redhat.com/security/cve/CVE-2014-3611) [CVE-2014-3646](https://access.redhat.com/security/cve/CVE-2014-3646) [CVE-2014-3647](https://access.redhat.com/security/cve/CVE-2014-3647) [CVE-2014-7825](https://access.redhat.com/security/cve/CVE-2014-7825) [CVE-2014-7826](https://access.redhat.com/security/cve/CVE-2014-7826) [CVE-2014-8369](https://access.redhat.com/security/cve/CVE-2014-8369) [templink](http://permalink.gmane.org/gmane.comp.security.oss.general/14526) [templink](http://seclists.org/oss-sec/2014/q4/548)</td>

<td>[linux](https://www.archlinux.org/packages/?name=linux), [linux-lts](https://www.archlinux.org/packages/?name=linux-lts)</td>

<td>2014-10-21</td>

<td><= 3.17.2-1, <= 3.14.23-1</td>

<td>3.17.3-1, 3.14.24-1</td>

<td>Fixed</td>

<td>[ASA-201411-14](https://lists.archlinux.org/pipermail/arch-security/2014-November/000139.html) [ASA-201411-15](https://lists.archlinux.org/pipermail/arch-security/2014-November/000140.html)</td>

</tr>

<tr>

<td>[CVE-2014-8480](https://access.redhat.com/security/cve/CVE-2014-8480) [CVE-2014-8481](https://access.redhat.com/security/cve/CVE-2014-8481) [templink](http://permalink.gmane.org/gmane.comp.security.oss.general/14526)</td>

<td>[linux](https://www.archlinux.org/packages/?name=linux)</td>

<td>2014-10-21</td>

<td><= 3.17.2-1</td>

<td>3.17.3-1</td>

<td>Fixed</td>

<td>[ASA-201411-14](https://lists.archlinux.org/pipermail/arch-security/2014-November/000139.html)</td>

</tr>

<tr>

<td>[CVE-2014-3695](https://access.redhat.com/security/cve/CVE-2014-3695) [CVE-2014-3696](https://access.redhat.com/security/cve/CVE-2014-3696) [CVE-2014-3698](https://access.redhat.com/security/cve/CVE-2014-3698) [templink](https://pidgin.im/news/security/)</td>

<td>[libpurple](https://www.archlinux.org/packages/?name=libpurple)</td>

<td>2014-10-22</td>

<td><= 2.10.9-2</td>

<td>2.10.10-1</td>

<td>< 1d</td>

<td>Fixed</td>

<td>[ASA-201410-9](https://lists.archlinux.org/pipermail/arch-security/2014-October/000120.html)</td>

</tr>

<tr>

<td>[CVE-2014-8760](https://access.redhat.com/security/cve/CVE-2014-8760)</td>

<td>[ejabberd](https://www.archlinux.org/packages/?name=ejabberd)</td>

<td>2014-10-13</td>

<td><= 14.07-1</td>

<td>14.07-2</td>

<td>14d</td>

<td>Fixed ([FS#42541](https://bugs.archlinux.org/task/42541))</td>

<td>[ASA-201410-13](https://lists.archlinux.org/pipermail/arch-security/2014-October/000124.html)</td>

</tr>

<tr>

<td>[CVE-2014-3686](https://access.redhat.com/security/cve/CVE-2014-3686)</td>

<td>[wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant), [hostapd](https://www.archlinux.org/packages/?name=hostapd)</td>

<td>2014-10-09</td>

<td><= 2.2-2</td>

<td>2.3-1</td>

<td>~10d</td>

<td>Fixed ([FS#42401](https://bugs.archlinux.org/task/42401))</td>

<td>[ASA-201410-8](https://lists.archlinux.org/pipermail/arch-security/2014-October/000119.html)</td>

</tr>

<tr>

<td>[CVE-2014-0191](https://access.redhat.com/security/cve/CVE-2014-0191) [CVE-2014-3660](https://access.redhat.com/security/cve/CVE-2014-3660)</td>

<td>[libxml2](https://www.archlinux.org/packages/?name=libxml2)</td>

<td>2014-10-16</td>

<td><= 2.9.1-5</td>

<td>2.9.2-1</td>

<td>8d</td>

<td>Fixed ([FS#40790](https://bugs.archlinux.org/task/40790))</td>

<td>[ASA-201410-12](https://lists.archlinux.org/pipermail/arch-security/2014-October/000123.html)</td>

</tr>

<tr>

<td>[CVE-2014-3704](https://access.redhat.com/security/cve/CVE-2014-3704) [templink](https://www.drupal.org/SA-CORE-2014-005)</td>

<td>[drupal](https://www.archlinux.org/packages/?name=drupal)</td>

<td>2014-10-15</td>

<td><= 7.31-2</td>

<td>7.32-1</td>

<td>1d</td>

<td>Fixed ([FS#42388](https://bugs.archlinux.org/task/42388))</td>

<td>[ASA-201410-7](https://lists.archlinux.org/pipermail/arch-security/2014-October/000118.html)</td>

</tr>

<tr>

<td>[CVE-2014-3513](https://access.redhat.com/security/cve/CVE-2014-3513) [CVE-2014-3566](https://access.redhat.com/security/cve/CVE-2014-3566) [CVE-2014-3567](https://access.redhat.com/security/cve/CVE-2014-3567) [CVE-2014-3568](https://access.redhat.com/security/cve/CVE-2014-3568) [templink](https://www.openssl.org/news/secadv_20141015.txt) [temp link](https://www.openssl.org/~bodo/ssl-poodle.pdf)</td>

<td>[openssl](https://www.archlinux.org/packages/?name=openssl)</td>

<td>2014-10-15</td>

<td><= 1.0.1.i-1</td>

<td>1.0.1.j-1</td>

<td>1d</td>

<td>Fixed</td>

<td>[ASA-201410-6](https://lists.archlinux.org/pipermail/arch-security/2014-October/000117.html)</td>

</tr>

<tr>

<td>[CVE-2014-8242](https://access.redhat.com/security/cve/CVE-2014-8242) [temp link](http://www.openwall.com/lists/oss-security/2014/10/13/2)</td>

<td>[librsync](https://www.archlinux.org/packages/?name=librsync)</td>

<td>2014-10-12</td>

<td><= 0.9.7-7</td>

<td>1.0.0-1</td>

<td>166d</td>

<td>Fixed ([FS#44175](https://bugs.archlinux.org/task/44175))</td>

<td>[ASA-201503-10](https://lists.archlinux.org/pipermail/arch-security/2015-March/000251.html)</td>

</tr>

<tr>

<td>[CVE-2014-7203](https://access.redhat.com/security/cve/CVE-2014-7203) [CVE-2014-7202](https://access.redhat.com/security/cve/CVE-2014-7202) [temp link](http://seclists.org/oss-sec/2014/q3/776)</td>

<td>[zeromq](https://www.archlinux.org/packages/?name=zeromq)</td>

<td>2014-09-27</td>

<td><= 4.0.4-4</td>

<td>4.0.5-1</td>

<td>18d</td>

<td>Fixed ([FS#42381](https://bugs.archlinux.org/task/42381))</td>

<td>[ASA-201410-4](https://lists.archlinux.org/pipermail/arch-security/2014-October/000116.html)</td>

</tr>

<tr>

<td>[CVE-2014-6051](https://access.redhat.com/security/cve/CVE-2014-6051) [CVE-2014-6052](https://access.redhat.com/security/cve/CVE-2014-6052) [CVE-2014-6053](https://access.redhat.com/security/cve/CVE-2014-6053) [CVE-2014-6054](https://access.redhat.com/security/cve/CVE-2014-6054) [CVE-2014-6055](https://access.redhat.com/security/cve/CVE-2014-6055) [temp link](http://seclists.org/oss-sec/2014/q3/639)</td>

<td>[libvncserver](https://www.archlinux.org/packages/?name=libvncserver)</td>

<td>2014-09-23</td>

<td><= 0.9.9-3</td>

<td>0.9.10-1</td>

<td>31d</td>

<td>Fixed ([FS#42321](https://bugs.archlinux.org/task/42321))</td>

<td>[ASA-201410-10](https://lists.archlinux.org/pipermail/arch-security/2014-October/000121.html)</td>

</tr>

<tr>

<td>[CVE-2014-3683](https://access.redhat.com/security/cve/CVE-2014-3683) [temp link](http://www.rsyslog.com/remote-syslog-pri-vulnerability-cve-2014-3683/)</td>

<td>[rsyslog](https://www.archlinux.org/packages/?name=rsyslog)</td>

<td>2014-10-02</td>

<td><= 8.4.1-1</td>

<td>8.4.2-1</td>

<td>1d</td>

<td>Fixed</td>

<td>[ASA-201410-5](https://lists.archlinux.org/pipermail/arch-security/2014-October/000115.html)</td>

</tr>

<tr>

<td>[CVE-2014-7204](https://access.redhat.com/security/cve/CVE-2014-7204) [temp link](http://seclists.org/oss-sec/2014/q3/842)</td>

<td>[ctags](https://www.archlinux.org/packages/?name=ctags)</td>

<td>2014-09-29</td>

<td><= 5.8-4</td>

<td>5.8-5</td>

<td>26d</td>

<td>Fixed ([FS#42246](https://bugs.archlinux.org/task/42246))</td>

<td>[ASA-201410-11](https://lists.archlinux.org/pipermail/arch-security/2014-October/000122.html)</td>

</tr>

<tr>

<td>[CVE-2014-7295](https://access.redhat.com/security/cve/CVE-2014-7295) [temp link](https://lists.wikimedia.org/pipermail/mediawiki-announce/2014-October/000163.html)</td>

<td>[mediawiki](https://www.archlinux.org/packages/?name=mediawiki)</td>

<td>2014-10-02</td>

<td><= 1.23.4-1</td>

<td>1.23.5-1</td>

<td><1d</td>

<td>Fixed</td>

<td>[ASA-201410-3](https://lists.archlinux.org/pipermail/arch-security/2014-October/000114.html)</td>

</tr>

<tr>

<td>[CVE-2014-3661](https://access.redhat.com/security/cve/CVE-2014-3661) [CVE-2014-3662](https://access.redhat.com/security/cve/CVE-2014-3662) [CVE-2014-3663](https://access.redhat.com/security/cve/CVE-2014-3663) [CVE-2014-3664](https://access.redhat.com/security/cve/CVE-2014-3664) [CVE-2014-3680](https://access.redhat.com/security/cve/CVE-2014-3680) [CVE-2014-3681](https://access.redhat.com/security/cve/CVE-2014-3681) [CVE-2014-3666](https://access.redhat.com/security/cve/CVE-2014-3666) [CVE-2014-3667](https://access.redhat.com/security/cve/CVE-2014-3667) [CVE-2013-2186](https://access.redhat.com/security/cve/CVE-2013-2186) [CVE-2014-1869](https://access.redhat.com/security/cve/CVE-2014-1869) [CVE-2014-3678](https://access.redhat.com/security/cve/CVE-2014-3678) [CVE-2014-3679](https://access.redhat.com/security/cve/CVE-2014-3679) [temp link](https://wiki.jenkins-ci.org/display/SECURITY/Jenkins+Security+Advisory+2014-10-01)</td>

<td>[jenkins](https://www.archlinux.org/packages/?name=jenkins)</td>

<td>2014-10-01</td>

<td><= 1.582-1</td>

<td>1.583-1</td>

<td><1d</td>

<td>Fixed</td>

<td>[ASA-201410-2](https://lists.archlinux.org/pipermail/arch-security/2014-October/000113.html)</td>

</tr>

<tr>

<td>[CVE-2014-3634](https://access.redhat.com/security/cve/CVE-2014-3634) [temp link](http://www.rsyslog.com/remote-syslog-pri-vulnerability/)</td>

<td>[rsyslog](https://www.archlinux.org/packages/?name=rsyslog)</td>

<td>2014-09-30</td>

<td><= 8.4.0-1</td>

<td>8.4.1-1</td>

<td>1d</td>

<td>Fixed ([FS#42200](https://bugs.archlinux.org/task/42200))</td>

<td>[ASA-201410-1](https://lists.archlinux.org/pipermail/arch-security/2014-October/000112.html)</td>

</tr>

<tr>

<td>[CVE-2014-3657](https://access.redhat.com/security/cve/CVE-2014-3657) [CVE-2014-3633](https://access.redhat.com/security/cve/CVE-2014-3633) [temp link](https://www.debian.org/security/2014/dsa-3038)</td>

<td>[libvirt](https://www.archlinux.org/packages/?name=libvirt)</td>

<td>2014-09-26</td>

<td><= 1.2.8-1</td>

<td>1.2.8-2</td>

<td>3d</td>

<td>Fixed ([FS#42159](https://bugs.archlinux.org/task/42159))</td>

<td>[ASA-201409-5](https://lists.archlinux.org/pipermail/arch-security/2014-September/000111.html)</td>

</tr>

<tr>

<td>[CVE-2014-7199](https://access.redhat.com/security/cve/CVE-2014-7199) [temp link](https://lists.wikimedia.org/pipermail/mediawiki-announce/2014-September/000161.html)</td>

<td>[mediawiki](https://www.archlinux.org/packages/?name=mediawiki)</td>

<td>2014-09-24</td>

<td><= 1.23.3-1</td>

<td>1.23.4-1</td>

<td>5d</td>

<td>Fixed ([FS#42161](https://bugs.archlinux.org/task/42161))</td>

<td>[ASA-201409-4](https://lists.archlinux.org/pipermail/arch-security/2014-September/000109.html)</td>

</tr>

<tr>

<td>[CVE-2014-7185](https://access.redhat.com/security/cve/CVE-2014-7185) [temp link](http://bugs.python.org/issue21831)</td>

<td>[python2](https://www.archlinux.org/packages/?name=python2)</td>

<td>2014-09-24</td>

<td>< 2.7.8</td>

<td>2.7.8-1</td>

<td>< 1d</td>

<td>Fixed</td>

<td>[ASA-201409-3](https://lists.archlinux.org/pipermail/arch-security/2014-September/000102.html)</td>

</tr>

<tr>

<td>[CVE-2014-1568](https://access.redhat.com/security/cve/CVE-2014-1568) [temp link](https://www.mozilla.org/security/announce/2014/mfsa2014-73.html)</td>

<td>[nss](https://www.archlinux.org/packages/?name=nss)</td>

<td>2014-09-24</td>

<td>< 3.17.1</td>

<td>3.17.1-1</td>

<td>< 1d</td>

<td>Fixed</td>

<td>[ASA-201409-1](https://lists.archlinux.org/pipermail/arch-security/2014-September/000097.html)</td>

</tr>

<tr>

<td>[CVE-2014-6271](https://access.redhat.com/security/cve/CVE-2014-6271) [CVE-2014-7169](https://access.redhat.com/security/cve/CVE-2014-7169) [CVE-2014-7186](https://access.redhat.com/security/cve/CVE-2014-7186) [CVE-2014-7187](https://access.redhat.com/security/cve/CVE-2014-7187) [CVE-2014-6277](https://access.redhat.com/security/cve/CVE-2014-6277) [CVE-2014-6278](https://access.redhat.com/security/cve/CVE-2014-6278) [temp link](http://seclists.org/oss-sec/2014/q3/649)</td>

<td>[bash](https://www.archlinux.org/packages/?name=bash)</td>

<td>2014-09-24</td>

<td><= 4.3.024-1</td>

<td>4.3.026-1</td>

<td>2d</td>

<td>Fixed ([FS#42109](https://bugs.archlinux.org/task/42109))</td>

<td>[ASA-201409-2](https://lists.archlinux.org/pipermail/arch-security/2014-September/000099.html)</td>

</tr>

<tr>

<td>[CVE-2014-3635](https://access.redhat.com/security/cve/CVE-2014-3635) [CVE-2014-3636](https://access.redhat.com/security/cve/CVE-2014-3636) [CVE-2014-3637](https://access.redhat.com/security/cve/CVE-2014-3637) [CVE-2014-3638](https://access.redhat.com/security/cve/CVE-2014-3638) [CVE-2014-3639](https://access.redhat.com/security/cve/CVE-2014-3639) [temp link](http://www.openwall.com/lists/oss-security/2014/09/16/9)</td>

<td>[dbus](https://www.archlinux.org/packages/?name=dbus) [libdbus](https://www.archlinux.org/packages/?name=libdbus) [lib32-libdbus](https://www.archlinux.org/packages/?name=lib32-libdbus)</td>

<td>2014-09-16</td>

<td>< 1.8.8</td>

<td>1.8.8-1</td>

<td>1d</td>

<td>Fixed ([FS#41993](https://bugs.archlinux.org/task/41993))</td>

</tr>

<tr>

<td>[CVE-2014-3613](https://access.redhat.com/security/cve/CVE-2014-3613) [CVE-2014-3620](https://access.redhat.com/security/cve/CVE-2014-3620) [temp link](http://curl.haxx.se/docs/security.html)</td>

<td>[curl](https://www.archlinux.org/packages/?name=curl) [lib32-curl](https://www.archlinux.org/packages/?name=lib32-curl)</td>

<td>2014-09-10</td>

<td>< 7.38.0</td>

<td>7.38.0-1</td>

<td>5d ([curl](https://www.archlinux.org/packages/?name=curl)), 7d ([lib32-curl](https://www.archlinux.org/packages/?name=lib32-curl))</td>

<td>Fixed</td>

</tr>

<tr>

<td>[CVE-2014-3609](https://access.redhat.com/security/cve/CVE-2014-3609) [temp link](http://www.squid-cache.org/Advisories/SQUID-2014_2.txt)</td>

<td>[squid](https://www.archlinux.org/packages/?name=squid)</td>

<td>2014-08-28</td>

<td>< 3.4.7</td>

<td>3.4.7-1</td>

<td>< 1d</td>

<td>Fixed</td>

</tr>

<tr>

<td>[CVE-2014-5119](https://access.redhat.com/security/cve/CVE-2014-5119) [temp link](https://sourceware.org/bugzilla/show_bug.cgi?id=17187)</td>

<td>[glibc](https://www.archlinux.org/packages/?name=glibc)</td>

<td>2014-07-21</td>

<td><= 2.19</td>

<td>2.20-2</td>

<td>55d</td>

<td>Fixed ([FS#41713](https://bugs.archlinux.org/task/41713))</td>

</tr>

<tr>

<td>[CVE-2014-3508](https://access.redhat.com/security/cve/CVE-2014-3508) [CVE-2014-5139](https://access.redhat.com/security/cve/CVE-2014-5139) [CVE-2014-3509](https://access.redhat.com/security/cve/CVE-2014-3509) [CVE-2014-3505](https://access.redhat.com/security/cve/CVE-2014-3505) [CVE-2014-3506](https://access.redhat.com/security/cve/CVE-2014-3506) [CVE-2014-3507](https://access.redhat.com/security/cve/CVE-2014-3507) [CVE-2014-3510](https://access.redhat.com/security/cve/CVE-2014-3510) [CVE-2014-3511](https://access.redhat.com/security/cve/CVE-2014-3511) [CVE-2014-3512](https://access.redhat.com/security/cve/CVE-2014-3512) [temp link](https://www.openssl.org/news/secadv_20140806.txt)</td>

<td>[openssl](https://www.archlinux.org/packages/?name=openssl)</td>

<td>2014-08-06</td>

<td>< 1.0.1.i</td>

<td>1.0.1.i-1</td>

<td><1d</td>

<td>Fixed</td>

</tr>

<tr>

<td>[CVE-2014-0226](https://access.redhat.com/security/cve/CVE-2014-0226) [temp link](http://www.zerodayinitiative.com/advisories/ZDI-14-236/)</td>

<td>[apache](https://www.archlinux.org/packages/?name=apache)</td>

<td>2014-07-15</td>

<td>< 2.4.10</td>

<td>2.4.10-1</td>

<td>~7d</td>

<td>Fixed ([FS#41244](https://bugs.archlinux.org/task/41244))</td>

</tr>

<tr>

<td>[CVE-2014-4943](https://access.redhat.com/security/cve/CVE-2014-4943) [temp link](http://www.openwall.com/lists/oss-security/2014/07/17/1)</td>

<td>[linux](https://www.archlinux.org/packages/?name=linux), [linux-lts](https://www.archlinux.org/packages/?name=linux-lts), [linux-grsec](https://www.archlinux.org/packages/?name=linux-grsec)</td>

<td>2014-07-16</td>

<td>3.15.5.201407170639-1 [linux-grsec](https://www.archlinux.org/packages/?name=linux-grsec), 3.14.16 ([linux-lts](https://www.archlinux.org/packages/?name=linux-lts)), 3.16 ([linux](https://www.archlinux.org/packages/?name=linux))</td>

<td>1d ([linux-grsec](https://www.archlinux.org/packages/?name=linux-grsec)), 23d ([linux-lts](https://www.archlinux.org/packages/?name=linux-lts)), 27d [linux](https://www.archlinux.org/packages/?name=linux)</td>

<td>Fixed in [linux](https://www.archlinux.org/packages/?name=linux), [linux-lts](https://www.archlinux.org/packages/?name=linux-lts) ([FS#41231](https://bugs.archlinux.org/task/41231)), Fixed in [linux-grsec](https://www.archlinux.org/packages/?name=linux-grsec)</td>

</tr>

<tr>

<td>[CVE-2014-0475](https://access.redhat.com/security/cve/CVE-2014-0475) [temp link](http://www.openwall.com/lists/oss-security/2014/07/10/7)</td>

<td>[glibc](https://www.archlinux.org/packages/?name=glibc)</td>

<td>2014-07-10</td>

<td><=2.19</td>

<td>2.20-2</td>

<td>66d</td>

<td>Fixed ([FS#41166](https://bugs.archlinux.org/task/41166))</td>

</tr>

<tr>

<td>[CVE-2014-4699](https://access.redhat.com/security/cve/CVE-2014-4699) [temp link](http://www.openwall.com/lists/oss-security/2014/07/04/4)</td>

<td>[linux](https://www.archlinux.org/packages/?name=linux), [linux-lts](https://www.archlinux.org/packages/?name=linux-lts), [linux-grsec](https://www.archlinux.org/packages/?name=linux-grsec)</td>

<td>2014-07-04</td>

<td>3.15.3.201407060933-1 [linux-grsec](https://www.archlinux.org/packages/?name=linux-grsec), 3.15.4-1 [linux](https://www.archlinux.org/packages/?name=linux), 3.14.11-1 [linux-lts](https://www.archlinux.org/packages/?name=linux-lts)</td>

<td>2d ([linux-grsec](https://www.archlinux.org/packages/?name=linux-grsec)), 3d ([linux](https://www.archlinux.org/packages/?name=linux), [linux-lts](https://www.archlinux.org/packages/?name=linux-lts))</td>

<td>Fixed ([FS#41115](https://bugs.archlinux.org/task/41115))</td>

</tr>

<tr>

<td>[CVE-2014-4715](https://access.redhat.com/security/cve/CVE-2014-4715) [temp link](http://www.openwall.com/lists/oss-security/2014/07/02/13)</td>

<td>[lz4](https://www.archlinux.org/packages/?name=lz4)</td>

<td>2014-07-02</td>

<td>119-1</td>

<td><1d</td>

<td>Fixed</td>

</tr>

<tr>

<td>[CVE-2014-4611](https://access.redhat.com/security/cve/CVE-2014-4611) [temp link](http://www.openwall.com/lists/oss-security/2014/06/26/25)</td>

<td>[linux](https://www.archlinux.org/packages/?name=linux), [linux-grsec](https://www.archlinux.org/packages/?name=linux-grsec), [lz4](https://www.archlinux.org/packages/?name=lz4)</td>

<td>2014-06-26</td>

<td>3.15.2-1 ([linux](https://www.archlinux.org/packages/?name=linux)), 3.15.2.201406262058-1 ([linux-grsec](https://www.archlinux.org/packages/?name=linux-grsec)), 118-1 [lz4](https://www.archlinux.org/packages/?name=lz4)</td>

<td><1d ([linux](https://www.archlinux.org/packages/?name=linux), [linux-grsec](https://www.archlinux.org/packages/?name=linux-grsec), [lz4](https://www.archlinux.org/packages/?name=lz4))</td>

<td>Fixed in [linux](https://www.archlinux.org/packages/?name=linux) ([FS#40992](https://bugs.archlinux.org/task/40992)), Fixed in [linux-grsec](https://www.archlinux.org/packages/?name=linux-grsec), Fixed in [lz4](https://www.archlinux.org/packages/?name=lz4) ([FS#40997](https://bugs.archlinux.org/task/40997))</td>

</tr>

<tr>

<td>[CVE-2014-4610](https://access.redhat.com/security/cve/CVE-2014-4610) [temp link](http://www.openwall.com/lists/oss-security/2014/06/26/23)</td>

<td>[ffmpeg](https://www.archlinux.org/packages/?name=ffmpeg)</td>

<td>2014-06-26</td>

<td>1:2.2.4-1</td>

<td>-2d</td>

<td>Fixed</td>

</tr>

<tr>

<td>[CVE-2014-4609](https://access.redhat.com/security/cve/CVE-2014-4609) [temp link](http://www.openwall.com/lists/oss-security/2014/06/26/22)</td>

<td>[gst-libav](https://www.archlinux.org/packages/?name=gst-libav)</td>

<td>2014-06-26</td>

<td>1.2.4-1</td>

<td>1.2.4-2 (with libav 9.14)</td>

<td>2d</td>

<td>Fixed ([FS#40995](https://bugs.archlinux.org/task/40995))</td>

</tr>

<tr>

<td>[CVE-2014-4608](https://access.redhat.com/security/cve/CVE-2014-4608) [temp link](http://www.openwall.com/lists/oss-security/2014/06/26/21)</td>

<td>[linux](https://www.archlinux.org/packages/?name=linux), [linux-lts](https://www.archlinux.org/packages/?name=linux-lts), [linux-grsec](https://www.archlinux.org/packages/?name=linux-grsec)</td>

<td>2014-06-26</td>

<td>3.15.2-1 ([linux](https://www.archlinux.org/packages/?name=linux)), 3.10.45-1 ([linux-lts](https://www.archlinux.org/packages/?name=linux-lts)), 3.15.2.201406262058-1 ([linux-grsec](https://www.archlinux.org/packages/?name=linux-grsec))</td>

<td><1d ([linux](https://www.archlinux.org/packages/?name=linux), [linux-lts](https://www.archlinux.org/packages/?name=linux-lts), [linux-grsec](https://www.archlinux.org/packages/?name=linux-grsec))</td>

<td>Fixed in [linux](https://www.archlinux.org/packages/?name=linux) and [linux-lts](https://www.archlinux.org/packages/?name=linux-lts) ([FS#40992](https://bugs.archlinux.org/task/40992)), Fixed in [linux-grsec](https://www.archlinux.org/packages/?name=linux-grsec)</td>

</tr>

<tr>

<td>[CVE-2014-4607](https://access.redhat.com/security/cve/CVE-2014-4607) [temp link](http://www.openwall.com/lists/oss-security/2014/06/26/20)</td>

<td>[lzo2](https://www.archlinux.org/packages/?name=lzo2)</td>

<td>2014-06-26</td>

<td>2.07-2</td>

<td>3d</td>

<td>Fixed ([FS#40993](https://bugs.archlinux.org/task/40993))</td>

</tr>

<tr>

<td>[CVE-2014-4617](https://access.redhat.com/security/cve/CVE-2014-4617) [temp link](http://lists.gnupg.org/pipermail/gnupg-announce/2014q2/000345.html)</td>

<td>[gnupg](https://www.archlinux.org/packages/?name=gnupg)</td>

<td>2014-06-24</td>

<td>< 2.0.24</td>

<td>2.0.24</td>

<td>7d</td>

<td>Fixed</td>

</tr>

<tr>

<td>[CVE-2014-0244](https://access.redhat.com/security/cve/CVE-2014-0244) [CVE-2014-3493](https://access.redhat.com/security/cve/CVE-2014-3493) [temp link](https://www.samba.org/samba/history/samba-4.1.9.html)</td>

<td>[samba](https://www.archlinux.org/packages/?name=samba)</td>

<td>2014-06-23</td>

<td>< 4.1.9</td>

<td>4.1.9</td>

<td><1d</td>

<td>Fixed</td>

</tr>

<tr>

<td>[CVE-2014-1545](https://access.redhat.com/security/cve/CVE-2014-1545) [temp link](https://www.mozilla.org/security/announce/2014/mfsa2014-55.html)</td>

<td>[nspr](https://www.archlinux.org/packages/?name=nspr)</td>

<td>2014-06-10</td>

<td>< 4.10.6</td>

<td>4.10.6</td>

<td>~1d</td>

<td>Fixed</td>

</tr>

<tr>

<td>[CVE-2014-3859](https://access.redhat.com/security/cve/CVE-2014-3859)</td>

<td>[bind](https://www.archlinux.org/packages/?name=bind)</td>

<td>2014-06-11</td>

<td>9.10.0, 9.10.0-P1</td>

<td>9.10.0-P2</td>

<td><1d</td>

<td>Fixed</td>

</tr>

<tr>

<td>[CVE-2014-3477](https://access.redhat.com/security/cve/CVE-2014-3477)</td>

<td>[dbus](https://www.archlinux.org/packages/?name=dbus)</td>

<td>2014-06-10</td>

<td><= 1.8.2</td>

<td>1.8.4</td>

<td>3d</td>

<td>Fixed</td>

</tr>

<tr>

<td>[CVE-2014-0195](https://access.redhat.com/security/cve/CVE-2014-0195) [CVE-2014-0198](https://access.redhat.com/security/cve/CVE-2014-0198) [CVE-2010-5298](https://access.redhat.com/security/cve/CVE-2010-5298) [CVE-2014-3470](https://access.redhat.com/security/cve/CVE-2014-3470) [CVE-2014-0224](https://access.redhat.com/security/cve/CVE-2014-0224) [CVE-2014-0221](https://access.redhat.com/security/cve/CVE-2014-0221) [temp link](http://www.openssl.org/news/secadv_20140605.txt)</td>

<td>[openssl](https://www.archlinux.org/packages/?name=openssl)</td>

<td>2014-06-05</td>

<td>1.0.1 - 1.0.1g</td>

<td>1.0.1h</td>

<td><1d</td>

<td>Fixed</td>

</tr>

<tr>

<td>[CVE-2014-3153](https://access.redhat.com/security/cve/CVE-2014-3153) [temp link](http://seclists.org/oss-sec/2014/q2/467)</td>

<td>[linux](https://www.archlinux.org/packages/?name=linux), [linux-lts](https://www.archlinux.org/packages/?name=linux-lts), [linux-grsec](https://www.archlinux.org/packages/?name=linux-grsec)</td>

<td>2014-06-05</td>

<td> ?</td>

<td>3.14.6 ([linux](https://www.archlinux.org/packages/?name=linux)), 3.10.42-1 ([linux-lts](https://www.archlinux.org/packages/?name=linux-lts)), 3.14.5.201406051310-1 ([linux-grsec](https://www.archlinux.org/packages/?name=linux-grsec))</td>

<td>3d ([linux](https://www.archlinux.org/packages/?name=linux), [linux-lts](https://www.archlinux.org/packages/?name=linux-lts)), <1d ([linux-grsec](https://www.archlinux.org/packages/?name=linux-grsec))</td>

<td>Fixed in [linux](https://www.archlinux.org/packages/?name=linux) ([FS#40715](https://bugs.archlinux.org/task/40715)), Fixed in [linux-lts](https://www.archlinux.org/packages/?name=linux-lts), Fixed in [linux-grsec](https://www.archlinux.org/packages/?name=linux-grsec)</td>

</tr>

<tr>

<td>[CVE-2014-3466](https://access.redhat.com/security/cve/CVE-2014-3466) [temp link](https://bugzilla.redhat.com/show_bug.cgi?id=1101932)</td>

<td>[gnutls](https://www.archlinux.org/packages/?name=gnutls)</td>

<td>2014-05-30</td>

<td>< 3.3.3</td>

<td>3.3.3</td>

<td><1d</td>

<td>Fixed</td>

</tr>

<tr>

<td>[CVE-2014-0209](https://access.redhat.com/security/cve/CVE-2014-0209) [CVE-2014-0210](https://access.redhat.com/security/cve/CVE-2014-0210) [CVE-2014-0211](https://access.redhat.com/security/cve/CVE-2014-0211)</td>

<td>[libxfont](https://www.archlinux.org/packages/?name=libxfont)</td>

<td>2014-05-13</td>

<td>< 1.4.18</td>

<td>1.4.18</td>

<td>3d</td>

<td>Fixed ([FS#40409](https://bugs.archlinux.org/task/40409) )</td>

</tr>

<tr>

<td>[CVE-2014-0196](https://access.redhat.com/security/cve/CVE-2014-0196) [temp-link](https://bugzilla.redhat.com/show_bug.cgi?id=1094232)</td>

<td>[linux](https://www.archlinux.org/packages/?name=linux), [linux-lts](https://www.archlinux.org/packages/?name=linux-lts), [linux-grsec](https://www.archlinux.org/packages/?name=linux-grsec)</td>

<td>2014-05-05</td>

<td>2.6.31 - 3.14</td>

<td>3.14.3-2 ([linux](https://www.archlinux.org/packages/?name=linux)), 3.10.39-2 ([linux-lts](https://www.archlinux.org/packages/?name=linux-lts)), 3.14.3.201405121814-1 ([linux-grsec](https://www.archlinux.org/packages/?name=linux-grsec))</td>

<td>7d ([linux](https://www.archlinux.org/packages/?name=linux)), 8d [linux-lts](https://www.archlinux.org/packages/?name=linux-lts), <1d ([linux-grsec](https://www.archlinux.org/packages/?name=linux-grsec))</td>

<td>Fixed in [linux](https://www.archlinux.org/packages/?name=linux) ([FS#40232](https://bugs.archlinux.org/task/40232)), Fixed in [linux-lts](https://www.archlinux.org/packages/?name=linux-lts), Fixed in [linux-grsec](https://www.archlinux.org/packages/?name=linux-grsec)</td>

</tr>

<tr>

<td>[CVE-2014-2905](https://access.redhat.com/security/cve/CVE-2014-2905) [CVE-2014-2906](https://access.redhat.com/security/cve/CVE-2014-2906) [CVE-2014-2914](https://access.redhat.com/security/cve/CVE-2014-2914) [temp-link](https://bugzilla.redhat.com/show_bug.cgi?id=1092091)</td>

<td>[fish](https://www.archlinux.org/packages/?name=fish)</td>

<td>2014-04-28</td>

<td>1.16.0 - 2.1.0</td>

<td>2.2.1</td>

<td><0</td>

<td>Fixed</td>

</tr>

<tr>

<td>[CVE-2014-0160](https://access.redhat.com/security/cve/CVE-2014-0160)</td>

<td>[openssl](https://www.archlinux.org/packages/?name=openssl)</td>

<td>2014-04-07</td>

<td>1.0.1 - 1.0.1f</td>

<td>1.0.1g</td>

<td>~1d</td>

<td>Fixed ([FS#39775](https://bugs.archlinux.org/task/39775))</td>

</tr>

<tr>

<td>[CVE-2014-1700](https://access.redhat.com/security/cve/CVE-2014-1700) [CVE-2014-1701](https://access.redhat.com/security/cve/CVE-2014-1701) [CVE-2014-1702](https://access.redhat.com/security/cve/CVE-2014-1702) [CVE-2014-1703](https://access.redhat.com/security/cve/CVE-2014-1703) [CVE-2014-1704](https://access.redhat.com/security/cve/CVE-2014-1704) [CVE-2014-1705](https://access.redhat.com/security/cve/CVE-2014-1705) [CVE-2014-1713](https://access.redhat.com/security/cve/CVE-2014-1713) [CVE-2014-1715](https://access.redhat.com/security/cve/CVE-2014-1715)</td>

<td>[chromium](https://www.archlinux.org/packages/?name=chromium) [v8](https://www.archlinux.org/packages/?name=v8)</td>

<td>2014-03-11</td>

<td>32</td>

<td>33</td>

<td>4d</td>

<td>Fixed</td>

</tr>

<tr>

<td>[CVE-2014-0098](https://access.redhat.com/security/cve/CVE-2014-0098) [CVE-2013-6438](https://access.redhat.com/security/cve/CVE-2013-6438)</td>

<td>[apache](https://www.archlinux.org/packages/?name=apache)</td>

<td>2014-03-17</td>

<td>2.4.8</td>

<td>2.4.9</td>

<td>-1d</td>

<td>Fixed</td>

</tr>

<tr>

<td>[CVE-2014-1492](https://access.redhat.com/security/cve/CVE-2014-1492)</td>

<td>[nss](https://www.archlinux.org/packages/?name=nss)</td>

<td>2014-03-18</td>

<td>3.15.5</td>

<td>3.16</td>

<td>22d</td>

<td>Fixed</td>

</tr>

<tr>

<td>[CVE-2014-1493](https://access.redhat.com/security/cve/CVE-2014-1493) [CVE-2014-1494](https://access.redhat.com/security/cve/CVE-2014-1494) [CVE-2014-1497](https://access.redhat.com/security/cve/CVE-2014-1497) [CVE-2014-1498](https://access.redhat.com/security/cve/CVE-2014-1498) [CVE-2014-1499](https://access.redhat.com/security/cve/CVE-2014-1499) [CVE-2014-1500](https://access.redhat.com/security/cve/CVE-2014-1500) [CVE-2014-1502](https://access.redhat.com/security/cve/CVE-2014-1502) [CVE-2014-1504](https://access.redhat.com/security/cve/CVE-2014-1504) [CVE-2014-1505](https://access.redhat.com/security/cve/CVE-2014-1505) [CVE-2014-1508](https://access.redhat.com/security/cve/CVE-2014-1508) [CVE-2014-1509](https://access.redhat.com/security/cve/CVE-2014-1509) [CVE-2014-1510](https://access.redhat.com/security/cve/CVE-2014-1510) [CVE-2014-1511](https://access.redhat.com/security/cve/CVE-2014-1511) [CVE-2014-1512](https://access.redhat.com/security/cve/CVE-2014-1512) [CVE-2014-1513](https://access.redhat.com/security/cve/CVE-2014-1513) [CVE-2014-1514](https://access.redhat.com/security/cve/CVE-2014-1514)</td>

<td>[firefox](https://www.archlinux.org/packages/?name=firefox) [thunderbird](https://www.archlinux.org/packages/?name=thunderbird)</td>

<td>2014-03-18</td>

<td>27</td>

<td>28</td>

<td>1d</td>

<td>Fixed</td>

</tr>

<tr>

<td>[CVE-2014-2240](https://access.redhat.com/security/cve/CVE-2014-2240) [CVE-2014-2241](https://access.redhat.com/security/cve/CVE-2014-2241)</td>

<td>[freetype2](https://www.archlinux.org/packages/?name=freetype2)</td>

<td> ?</td>

<td>2.5.2</td>

<td>2.5.3</td>

<td> ?</td>

<td>Fixed</td>

</tr>

<tr>

<td>[CVE-2014-2029](https://access.redhat.com/security/cve/CVE-2014-2029)</td>

<td>[xtrabackup](https://www.archlinux.org/packages/?name=xtrabackup)</td>

<td>2014-02-16</td>

<td>2.1.7</td>

<td>2.1.8</td>

<td>28d</td>

<td>Fixed</td>

</tr>

<tr>

<td>[CVE-2014-1958](https://access.redhat.com/security/cve/CVE-2014-1958) [CVE-2014-2030](https://access.redhat.com/security/cve/CVE-2014-2030)</td>

<td>[imagemagick](https://www.archlinux.org/packages/?name=imagemagick)</td>

<td> ?</td>

<td> ?</td>

<td>6.8.8.9-1</td>

<td> ?</td>

<td>Fixed</td>

</tr>

<tr>

<td>[CVE-2014-1943](https://access.redhat.com/security/cve/CVE-2014-1943) [CVE-2014-2270](https://access.redhat.com/security/cve/CVE-2014-2270)</td>

<td>[php](https://www.archlinux.org/packages/?name=php)</td>

<td>2014-03-06</td>

<td>5.5.9</td>

<td>5.5.110</td>

<td>-1d</td>

<td>Fixed</td>

</tr>

<tr>

<td>[CVE-2014-0404](https://access.redhat.com/security/cve/CVE-2014-0404) [CVE-2014-0406](https://access.redhat.com/security/cve/CVE-2014-0406) [CVE-2014-0407](https://access.redhat.com/security/cve/CVE-2014-0407)</td>

<td>[virtualbox](https://www.archlinux.org/packages/?name=virtualbox)</td>

<td>2014-02-28</td>

<td>4.3.4</td>

<td>4.3.6</td>

<td> ?</td>

<td>Fixed</td>

</tr>

<tr>

<td>[CVE-2014-2323](https://access.redhat.com/security/cve/CVE-2014-2323) [CVE-2014-2324](https://access.redhat.com/security/cve/CVE-2014-2324)</td>

<td>[lighttpd](https://www.archlinux.org/packages/?name=lighttpd)</td>

<td>2014-03-12</td>

<td>1.4.34</td>

<td>1.4.35</td>

<td>0d</td>

<td>Fixed</td>

</tr>

<tr>

<td>[CVE-2014-0333](https://access.redhat.com/security/cve/CVE-2014-0333)</td>

<td>[libpng](https://www.archlinux.org/packages/?name=libpng)</td>

<td>2014-02-28</td>

<td>1.6.9</td>

<td>1.6.10</td>

<td>9d</td>

<td>Fixed</td>

</tr>

<tr>

<td>[CVE-2014-0017](https://access.redhat.com/security/cve/CVE-2014-0017)</td>

<td>[libssh](https://www.archlinux.org/packages/?name=libssh)</td>

<td>2014-03-04</td>

<td> ?</td>

<td>3.5.7.29</td>

<td>5d</td>

<td>Fixed</td>

</tr>

<tr>

<td>[CVE-2013-7339](http://seclists.org/oss-sec/2014/q1/628)</td>

<td>[linux](https://www.archlinux.org/packages/?name=linux)</td>

<td>2014-03-20</td>

<td>< 3.5.7.29</td>

<td>3.5.7.29</td>

<td>0d</td>

<td>Fixed</td>

</tr>

<tr>

<td>[CVE-2014-2568](https://access.redhat.com/security/cve/CVE-2014-2568)</td>

<td>[linux](https://www.archlinux.org/packages/?name=linux)</td>

<td>2014-03-18</td>

<td> ?</td>

<td> ?</td>

<td> ?</td>

<td>Invalid ([FS#39566](https://bugs.archlinux.org/task/39566))</td>

</tr>

<tr>

<td>[CVE-2014-2524](https://access.redhat.com/security/cve/CVE-2014-2524)</td>

<td>[tigervnc](https://www.archlinux.org/packages/?name=tigervnc)</td>

<td>2014-03-19</td>

<td> ?</td>

<td>1.3.1</td>

<td>1d</td>

<td>Fixed</td>

</tr>

<tr>

<td>[CVE-2013-7338](http://seclists.org/oss-sec/2014/q1/595)</td>

<td>[python](https://www.archlinux.org/packages/?name=python)</td>

<td>2014-03-19</td>

<td>3.4beta (?)</td>

<td>3.4</td>

<td>2013-12-27:?</td>

<td>Fixed ([FS#39540](https://bugs.archlinux.org/task/39540))</td>

</tr>

<tr>

<td>[CVE-2014-0133](http://mailman.nginx.org/pipermail/nginx-announce/2014/000135.html)</td>

<td>[nginx](https://www.archlinux.org/packages/?name=nginx)</td>

<td>2014-03-18</td>

<td> ?</td>

<td>1.4.7</td>

<td>0d</td>

<td>Fixed</td>

</tr>

<tr>

<td>[CVE-2013-7336](https://access.redhat.com/security/cve/CVE-2013-7336)</td>

<td>[libvirt](https://www.archlinux.org/packages/?name=libvirt)</td>

<td>2013-09-19</td>

<td> ?</td>

<td>1.1.1-7 (in RHEL 7)</td>

<td>0d</td>

<td>Fixed</td>

</tr>

<tr>

<td>[CVE-2014-2523](https://access.redhat.com/security/cve/CVE-2014-2523)</td>

<td>[linux](https://www.archlinux.org/packages/?name=linux)</td>

<td>2014-03-17</td>

<td> ?</td>

<td>3.13-rc5</td>

<td> ?</td>

<td>Fixed</td>

</tr>

<tr>

<td>[CVE-2014-0004](https://access.redhat.com/security/cve/CVE-2014-0004)</td>

<td>[udisks2](https://www.archlinux.org/packages/?name=udisks2) & [udisks](https://www.archlinux.org/packages/?name=udisks)</td>

<td>2014-03-10</td>

<td>2.1.3 / 1.0.5</td>

<td>2.1.3 / 1.0.5</td>

<td>3d</td>

<td>Fixed</td>

</tr>

<tr>

<td>[CVE-2014-2281](https://access.redhat.com/security/cve/CVE-2014-2281) [CVE-2014-2282](https://access.redhat.com/security/cve/CVE-2014-2282) [CVE-2014-2283](https://access.redhat.com/security/cve/CVE-2014-2283) [CVE-2014-2299](https://access.redhat.com/security/cve/CVE-2014-2299)</td>

<td>[wireshark-cli](https://www.archlinux.org/packages/?name=wireshark-cli)</td>

<td>2014-03-10</td>

<td>1.10.6</td>

<td>1.10.6</td>

<td> ?</td>

<td>Fixed</td>

</tr>

<tr>

<td>[CVE-2014-0050](https://access.redhat.com/security/cve/CVE-2014-0050)</td>

<td>[tomcat7](https://www.archlinux.org/packages/?name=tomcat7)</td>

<td>2014-02-06</td>

<td>7.0.51</td>

<td>7.0.51</td>

<td> ?</td>

<td>Fixed</td>

</tr>

<tr>

<td>[CVE-2014-0033](https://access.redhat.com/security/cve/CVE-2014-0033)</td>

<td>[tomcat6](https://www.archlinux.org/packages/?name=tomcat6)</td>

<td>2014-01-10</td>

<td>6.0.37</td>

<td>6.0.37</td>

<td> ?</td>

<td>Fixed</td>

</tr>

<tr>

<td>[CVE-2014-0032](https://access.redhat.com/security/cve/CVE-2014-0032)</td>

<td>[subversion](https://www.archlinux.org/packages/?name=subversion)</td>

<td>2014-01-10</td>

<td>1.8.6</td>

<td>1.8.6</td>

<td> ?</td>

<td>Fixed</td>

</tr>

<tr>

<td>[CVE-2014-0060](https://access.redhat.com/security/cve/CVE-2014-0060) [CVE-2014-0061](https://access.redhat.com/security/cve/CVE-2014-0061) [CVE-2014-0062](https://access.redhat.com/security/cve/CVE-2014-0062) [CVE-2014-0063](https://access.redhat.com/security/cve/CVE-2014-0063) [CVE-2014-0064](https://access.redhat.com/security/cve/CVE-2014-0064) [CVE-2014-0065](https://access.redhat.com/security/cve/CVE-2014-0065) [CVE-2014-0066](https://access.redhat.com/security/cve/CVE-2014-0066) [CVE-2014-0067](https://access.redhat.com/security/cve/CVE-2014-0067)</td>

<td>[postgresql](https://www.archlinux.org/packages/?name=postgresql)</td>

<td>2014-02-20</td>

<td>9.3.3</td>

<td>9.33</td>

<td>0d</td>

<td>Fixed</td>

</tr>

<tr>

<td>[CVE-2014-1912](https://access.redhat.com/security/cve/CVE-2014-1912)</td>

<td>[python](https://www.archlinux.org/packages/?name=python) [python2](https://www.archlinux.org/packages/?name=python2)</td>

<td>2014-02-07</td>

<td> ?</td>

<td> ?</td>

<td> ?</td>

<td>Fixed</td>

</tr>

<tr>

<td>[CVE-2013-4496](https://access.redhat.com/security/cve/CVE-2013-4496) [CVE-2013-6442](https://access.redhat.com/security/cve/CVE-2013-6442)</td>

<td>[samba](https://www.archlinux.org/packages/?name=samba)</td>

<td>2014-03-14</td>

<td> ?</td>

<td>4.1.6</td>

<td>2d</td>

<td>Fixed ([FS#39424](https://bugs.archlinux.org/task/39424))</td>

</tr>

<tr>

<td>[CVE-2014-0504](https://access.redhat.com/security/cve/CVE-2014-0504)</td>

<td>[flashplugin](https://www.archlinux.org/packages/?name=flashplugin)</td>

<td>2014-03-12</td>

<td> ?</td>

<td>11.2.202.346</td>

<td>1d</td>

<td>Fixed ([FS#39385](https://bugs.archlinux.org/task/39385))</td>

</tr>

<tr>

<td>[CVE-2014-0106](https://access.redhat.com/security/cve/CVE-2014-0106)</td>

<td>[sudo](https://www.archlinux.org/packages/?name=sudo)</td>

<td>1.8.9.p5</td>

<td>1.8.10</td>

<td> ?</td>

<td> ?</td>

<td>Fixed</td>

</tr>

<tr>

<td>[CVE-2014-2285](https://access.redhat.com/security/cve/CVE-2014-2285) [CVE-2014-2284](https://access.redhat.com/security/cve/CVE-2014-2284)</td>

<td>[net-snmp](https://www.archlinux.org/packages/?name=net-snmp)</td>

<td>2014-03-05</td>

<td> ?</td>

<td> ?</td>

<td>8d</td>

<td>Fixed ([FS#39190](https://bugs.archlinux.org/task/39190))</td>

</tr>

<tr>

<td>[CVE-2014-0092](https://access.redhat.com/security/cve/CVE-2014-0092)</td>

<td>[gnutls](https://www.archlinux.org/packages/?name=gnutls)</td>

<td>2014-03-04</td>

<td><3.2.12</td>

<td>3.2.12-1</td>

<td>1d</td>

<td>Fixed</td>

</tr>

<tr>

<td>[CVE-2014-2242](https://access.redhat.com/security/cve/CVE-2014-2242) [CVE-2014-2243](https://access.redhat.com/security/cve/CVE-2014-2243) [CVE-2014-2244](https://access.redhat.com/security/cve/CVE-2014-2244)</td>

<td>[mediawiki](https://www.archlinux.org/packages/?name=mediawiki)</td>

<td>2014-03-14</td>

<td><1.22.3</td>

<td>1.22.3</td>

<td>1d</td>

<td>Fixed</td>

</tr>

<tr>

<td>[CVE-2014-2093](https://access.redhat.com/security/cve/CVE-2014-2093) [CVE-2014-2094](https://access.redhat.com/security/cve/CVE-2014-2094) [CVE-2014-2095](https://access.redhat.com/security/cve/CVE-2014-2095) [CVE-2014-2096](https://access.redhat.com/security/cve/CVE-2014-2096)</td>

<td>[catfish](https://www.archlinux.org/packages/?name=catfish)</td>

<td>2014-02-25</td>

<td><1.0.1</td>

<td>1.0.1</td>

<td>8d</td>

<td>Fixed</td>

</tr>

<tr>

<td>[CVE-2014-0497](https://access.redhat.com/security/cve/CVE-2014-0497)</td>

<td>[flashplugin](https://www.archlinux.org/packages/?name=flashplugin)</td>

<td>2014-02-04</td>

<td> ?</td>

<td> ?</td>

<td>1d</td>

<td> ?</td>

</tr>

<tr>

<td>[CVE-2014-0015](https://access.redhat.com/security/cve/CVE-2014-0015)</td>

<td>[curl](https://www.archlinux.org/packages/?name=curl)</td>

<td>2014-01-29</td>

<td><7.35</td>

<td>7.35</td>

<td>0d</td>

<td>Fixed</td>

</tr>

<tr>

<td>[CVE-2014-1610](https://access.redhat.com/security/cve/CVE-2014-1610)</td>

<td>[mediawiki](https://www.archlinux.org/packages/?name=mediawiki)</td>

<td>2014-01-29</td>

<td><1.22.2</td>

<td>1.22.2</td>

<td>0d</td>

<td>Fixed</td>

</tr>

<tr>

<td>[CVE-2014-0021](https://access.redhat.com/security/cve/CVE-2014-0021)</td>

<td>[chrony](https://www.archlinux.org/packages/?name=chrony)</td>

<td>2014-01-17</td>

<td><1.29.1-1</td>

<td>1.29.1-1</td>

<td>14d</td>

<td>Fixed</td>

</tr>

<tr>

<td>[CVE-2014-1875](https://access.redhat.com/security/cve/CVE-2014-1875)</td>

<td>[perl-capture-tiny](https://www.archlinux.org/packages/?name=perl-capture-tiny)</td>

<td>2014-02-06</td>

<td> ?</td>

<td> ?</td>

<td>4d</td>

<td>Fixed ([FS#38862](https://bugs.archlinux.org/task/38862))</td>

</tr>

<tr>

<td>[CVE-2013-6493](https://access.redhat.com/security/cve/CVE-2013-6493)</td>

<td>[icedtea-web-java7](https://www.archlinux.org/packages/?name=icedtea-web-java7)</td>

<td>2014-02-05</td>

<td><1.4.2</td>

<td>1.4.2</td>

<td>0d</td>

<td>Fixed</td>

</tr>

<tr>

<td>[CVE-2014-1858](https://access.redhat.com/security/cve/CVE-2014-1858) [CVE-2014-1859](https://access.redhat.com/security/cve/CVE-2014-1859)</td>

<td>[python-numpy](https://www.archlinux.org/packages/?name=python-numpy)</td>

<td>2014-02-06</td>

<td> ?</td>

<td> ?</td>

<td>4d</td>

<td>Fixed ([FS#38863](https://bugs.archlinux.org/task/38863))</td>

</tr>

<tr>

<td>[CVE-2014-1932](https://access.redhat.com/security/cve/CVE-2014-1932) [CVE-2014-1933](https://access.redhat.com/security/cve/CVE-2014-1933)</td>

<td>[python-pillow](https://www.archlinux.org/packages/?name=python-pillow)</td>

<td>2014-02-10</td>

<td><2.3.1</td>

<td>2.3.1</td>

<td> ?</td>

<td>Fixed</td>

</tr>

<tr>

<td>[CVE-2014-1935](https://access.redhat.com/security/cve/CVE-2014-1935)</td>

<td>[9base](https://www.archlinux.org/packages/?name=9base)</td>

<td>2014-02-10</td>

<td> ?</td>

<td> ?</td>

<td> ?</td>

<td> ?</td>

</tr>

<tr>

<td>[CVE-2014-1949](https://access.redhat.com/security/cve/CVE-2014-1949) [temp link](http://people.canonical.com/~ubuntu-security/cve/2014/CVE-2014-1949.html)</td>

<td>[cinnamon-screensaver](https://www.archlinux.org/packages/?name=cinnamon-screensaver)</td>

<td>2014-02-12</td>

<td>2.0.3</td>

<td> ?</td>

<td> ?</td>

<td> ?</td>

</tr>

<tr>

<td>[CVE-2014-1959](https://access.redhat.com/security/cve/CVE-2014-1959)</td>

<td>[gnutls](https://www.archlinux.org/packages/?name=gnutls)</td>

<td>2014-02-13</td>

<td><3.2.11</td>

<td>3.2.11</td>

<td>2d</td>

<td>Fixed</td>

</tr>

<tr>

<td>[CVE-2014-1943](https://access.redhat.com/security/cve/CVE-2014-1943) [CVE-2014-2270](https://access.redhat.com/security/cve/CVE-2014-2270)</td>

<td>[file](https://www.archlinux.org/packages/?name=file)</td>

<td>2014-02-10</td>

<td><5.17</td>

<td>5.17-1</td>

<td>3d</td>

<td>Fixed</td>

</tr>

<tr>

<td>[CVE-2014-0001](https://access.redhat.com/security/cve/CVE-2014-0001) [CVE-2014-0412](https://access.redhat.com/security/cve/CVE-2014-0412) [CVE-2014-0437](https://access.redhat.com/security/cve/CVE-2014-0437) [CVE-2014-0420](https://access.redhat.com/security/cve/CVE-2014-0420) [CVE-2014-0393](https://access.redhat.com/security/cve/CVE-2014-0393) [CVE-2014-0386](https://access.redhat.com/security/cve/CVE-2014-0386) [CVE-2014-0401](https://access.redhat.com/security/cve/CVE-2014-0401) [CVE-2014-0402](https://access.redhat.com/security/cve/CVE-2014-0402)</td>

<td>[mariadb](https://www.archlinux.org/packages/?name=mariadb)</td>

<td>2014-01-31</td>

<td><5.5.35</td>

<td>5.5.35-1</td>

<td>1d</td>

<td>Fixed</td>

</tr>

<tr>

<td>[CVE-2014-1447](https://access.redhat.com/security/cve/CVE-2014-1447)</td>

<td>[libvirt](https://www.archlinux.org/packages/?name=libvirt)</td>

<td>2014-01-16</td>

<td><1.2.1</td>

<td>1.2.1</td>

<td>0d</td>

<td>Fixed</td>

</tr>

<tr>

<td>[CVE-2014-0979](https://access.redhat.com/security/cve/CVE-2014-0979)</td>

<td>lightdm-gtk*</td>

<td>2014-01-07</td>

<td> ?</td>

<td> ?</td>

<td>25d</td>

<td>Fixed ([FS#38715](https://bugs.archlinux.org/task/38715))</td>

</tr>

<tr>

<td>[CVE-2014-1475](https://access.redhat.com/security/cve/CVE-2014-1475) [CVE-2014-1476](https://access.redhat.com/security/cve/CVE-2014-1476)</td>

<td>[drupal](https://www.archlinux.org/packages/?name=drupal)</td>

<td>2014-01-15</td>

<td><7.26</td>

<td>7.26-1</td>

<td>12d</td>

<td>Fixed</td>

</tr>

<tr>

<td>[CVE-2014-0019](https://access.redhat.com/security/cve/CVE-2014-0019)</td>

<td>[socat](https://www.archlinux.org/packages/?name=socat)</td>

<td>2014-01-29</td>

<td><1.7.2.3</td>

<td>1.7.2.3</td>

<td>0d</td>

<td>Fixed</td>

</tr>

<tr>

<td>[CVE-2014-1838](https://access.redhat.com/security/cve/CVE-2014-1838) [CVE-2014-1839](https://access.redhat.com/security/cve/CVE-2014-1839)</td>

<td>[python-logilab-common](https://www.archlinux.org/packages/?name=python-logilab-common)</td>

<td>2014-01-31</td>

<td> ?</td>

<td> ?</td>

<td>3d</td>

<td>Fixed [[21]](https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=737051)</td>

</tr>

<tr>

<td>[CVE-2014-0368](https://access.redhat.com/security/cve/CVE-2014-0368) [CVE-2014-0373](https://access.redhat.com/security/cve/CVE-2014-0373) [CVE-2014-0376](https://access.redhat.com/security/cve/CVE-2014-0376) [CVE-2014-0411](https://access.redhat.com/security/cve/CVE-2014-0411) [CVE-2014-0416](https://access.redhat.com/security/cve/CVE-2014-0416) [CVE-2014-0422](https://access.redhat.com/security/cve/CVE-2014-0422) [CVE-2014-0423](https://access.redhat.com/security/cve/CVE-2014-0423) [CVE-2014-0428](https://access.redhat.com/security/cve/CVE-2014-0428)</td>

<td>*-openjdk-*</td>

<td>2014-01-15</td>

<td> ?</td>

<td> ?</td>

<td>2d</td>

<td> ?</td>

</tr>

<tr>

<td>[CVE-2014-1402](https://access.redhat.com/security/cve/CVE-2014-1402)</td>

<td>[python-jinja](https://www.archlinux.org/packages/?name=python-jinja)</td>

<td>2014-01-10</td>

<td><2.7.2</td>

<td>2.7.2</td>

<td>1d</td>

<td>Fixed</td>

</tr>

<tr>

<td>[CVE-2013-6462](https://access.redhat.com/security/cve/CVE-2013-6462)</td>

<td>[libxfont](https://www.archlinux.org/packages/?name=libxfont)</td>

<td>2014-01-07</td>

<td><1.4.7</td>

<td>1.4.7</td>

<td>0d</td>

<td>Fixed</td>

</tr>

<tr>

<td>[CVE-2014-1235](https://access.redhat.com/security/cve/CVE-2014-1235)</td>

<td>[graphviz](https://www.archlinux.org/packages/?name=graphviz)</td>

<td>2014-01-07</td>

<td> ?</td>

<td> ?</td>

<td>3d</td>

<td>Fixed ([FS#38441](https://bugs.archlinux.org/task/38441))</td>

</tr>

<tr>

<td>[CVE-2014-0978](https://access.redhat.com/security/cve/CVE-2014-0978)</td>

<td>[freerdp](https://www.archlinux.org/packages/?name=freerdp)</td>

<td>2014-01-10</td>

<td><1.0.2</td>

<td>1.0.2-5</td>

<td>67d</td>

<td>Fixed ([FS#38802](https://bugs.archlinux.org/task/38802))</td>

</tr>

</tbody>

</table>

Retrieved from "[https://wiki.archlinux.org/index.php?title=CVE&oldid=413199](https://wiki.archlinux.org/index.php?title=CVE&oldid=413199)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Arch development](/index.php/Category:Arch_development "Category:Arch development")
*   [Security](/index.php/Category:Security "Category:Security")