# Security Advisories/Examples

This article gives examples and templates for the Arch Linux Security Advisories and CVE-related bugreports.

## Contents

*   [1 Templates](#Templates)
    *   [1.1 Security Advisories](#Security_Advisories)
    *   [1.2 CVE-related bugreports](#CVE-related_bugreports)
*   [2 Examples](#Examples)
    *   [2.1 Security Advisory Example](#Security_Advisory_Example)
    *   [2.2 CVE-related bugreport example](#CVE-related_bugreport_example)

## Templates

This section will give you templates for security advisories and cve-related bugreports.

### Security Advisories

```
Subject:
[ASA-<YYYYMM-N>] <Package>: <Vulnerability Type>

Body:
Arch Linux Security Advisory ASA-YYYYMM-N
=========================================

Severity: Low, Medium, High, Critical
Date    : YYYY-MM-DD
CVE-ID  : <CVE-ID>
Package : <package>
Type    : <Vulnerability Type>
Remote  : <Yes/No>
Link    : https://wiki.archlinux.org/index.php/CVE

Summary
=======

The package <package> before version <Arch Linux fixed version> is vulnerable to <Vulnerability type>.

Resolution
==========

Upgrade to <Arch Linux fixed version>.

# pacman -Syu "<package>>=<Arch Linux fixed version>"

The problem has been fixed upstream in version <upstream fixed version>.

Workaround
==========

<Is there a way to mitigate this vulnerability without upgrading?>

Description
===========

<Long description, for example from original advisory>.

Impact
======

<
What is it that an attacker can do? Does this need existing
pre-conditions to be exploited (valid credentials, physical access)?
Is this remotely exploitable?
>.

References
==========

<CVE-Link>
<Upstream report>
<Arch Linux Bug-Tracker>

```

### CVE-related bugreports

```
Title: [<pkgname>][Security]<short description>
Body:
Summary
=======
<give a short summary about all CVEs>

Guidance
========
<give a short guidance for the maintainer.. what shall he/she do? include a patch? Just upgrade?>

References
==========
<links to patches (if not included in bugreport)>
<links to CVE-descriptions>
<links to other stuff that is maybe important>

```

## Examples

This section will give you examples for security advisories and cve-related bugreports. Every line beginning with `#` is a comment and is **not** part of the example.

### Security Advisory Example

```
Arch Linux Security Advisory ASA-201511-11
==========================================

Severity: Critical
Date    : 2015-11-18
CVE-ID  : CVE-2015-5317 CVE-2015-5318 CVE-2015-5319 CVE-2015-5320
          CVE-2015-5321 CVE-2015-5322 CVE-2015-5323 CVE-2015-5324
          CVE-2015-5325 CVE-2015-5326 CVE-2015-8103
Package : jenkins
Type    : multiple issues
Remote  : Yes
Link    : https://wiki.archlinux.org/index.php/CVE

Summary
=======

The package jenkins before version 1.638-1 is vulnerable to multiple
issues including but not limited to arbitrary code execution,
information leakage, cross-side request forgery, XML external entity
injection, access restriction bypass, cross-side scripting and directory
traversal.

Resolution
==========

Upgrade to 1.638-1.

# pacman -Syu "jenkins>=1.638-1"

The problems have been fixed upstream in version 1.638.

Workaround
==========

None.

Description
===========

- CVE-2015-5317 (information leakage)

The Jenkins UI allowed users to see the names of jobs and builds
otherwise inaccessible to them on the "Fingerprints" pages if those
shared file fingerprints with fingerprinted files in accessible jobs.

- CVE-2015-5318 (cross-side request forgery)

The salt used to generate the CSRF protection tokens was a publicly
accessible value, allowing malicious users to circumvent CSRF protection
by generating the correct token.

- CVE-2015-5319 (XML external entity injection)

When creating a job using the create-job CLI command, external entities
are not discarded (nor processed). If these job configurations are
processed by another user with an XML-aware tool (e.g. using
get-job/update-job), information from that user's computer may be
disclosed to Jenkins and the attacker.

- CVE-2015-5320 (access restriction bypass)

JNLP slave connections did not verify that the correct secret was
supplied, which allowed malicious users to connect their own machines as
slaves to Jenkins knowing only the name of the slave. This enables
attackers to take over Jenkins (unless the slave-to-master security
subsystem is enabled) or gain access to private data like keys and
source code.

- CVE-2015-5321 (information leakage)

The CLI command overview and help pages in Jenkins were accessible
without Overall/Read permission, resulting in disclosure of the names of
configured slaves (and contents of other sidepanel widgets, if present)
to unauthorized users.

- CVE-2015-5322 (directory traversal)

Access to the /jnlpJars/ URL was not limited to the specific JAR files
users needed to access, allowing browsing directories and downloading
other files in the Jenkins servlet resources, such as web.xml.

- CVE-2015-5323 (access restriction bypass)

API tokens of other users were exposed to admins by default. On
instances that don't implicitly grant RunScripts permission to admins,
this allowed admins to run scripts with another user's credentials.

- CVE-2015-5324 (information leakage)

The /queue/api URL could return information about items not accessible
to the current user (such as parameter names and values, build names,
project descriptions).

- CVE-2015-5325 (access restriction bypass)

Slaves connecting via JNLP were not subject to the optional
slave-to-master access control documented at
http://jenkins-ci.org/security-144 (CVE-2014-3665).

- CVE-2015-5326 (cross-side scripting)

Users with the permission to take slave nodes offline can enter
arbitrary HTML that gets shown unescaped to users visiting the slave
overview page.

- CVE-2015-8103 (arbitrary code execution)

Unsafe deserialization allows unauthenticated remote attackers to run
arbitrary code on the Jenkins master.

Impact
======

A remote attacker is able to execution arbitrary code, disclose
sensitive information, bypass the cross-side request forgery protection,
perform XML external entity injection, bypass multiple access
restrictions, perform a cross-side scripting attack and make use of a
directory traversal issue to download arbitrary files.

References
==========

https://access.redhat.com/security/cve/CVE-2015-5317
https://access.redhat.com/security/cve/CVE-2015-5318
https://access.redhat.com/security/cve/CVE-2015-5319
https://access.redhat.com/security/cve/CVE-2015-5320
https://access.redhat.com/security/cve/CVE-2015-5321
https://access.redhat.com/security/cve/CVE-2015-5322
https://access.redhat.com/security/cve/CVE-2015-5323
https://access.redhat.com/security/cve/CVE-2015-5324
https://access.redhat.com/security/cve/CVE-2015-5325
https://access.redhat.com/security/cve/CVE-2015-5326
https://access.redhat.com/security/cve/CVE-2015-8103
https://wiki.jenkins-ci.org/display/SECURITY/Jenkins+Security+Advisory+2015-11-11

```

### CVE-related bugreport example

Retrieved from "[https://wiki.archlinux.org/index.php?title=Security_Advisories/Examples&oldid=413738](https://wiki.archlinux.org/index.php?title=Security_Advisories/Examples&oldid=413738)"