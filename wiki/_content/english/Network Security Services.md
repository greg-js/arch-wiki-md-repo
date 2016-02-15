**Network Security Services (NSS)** is a set of libraries designed to support cross-platform development of security-enabled client and server applications.

Applications built with NSS can support [SSL](https://en.wikipedia.org/wiki/SSL "wikipedia:SSL") v2 and v3, [TLS](https://en.wikipedia.org/wiki/TLS "wikipedia:TLS"), [PKCS](https://en.wikipedia.org/wiki/PKCS "wikipedia:PKCS") #5, #7, [PKCS #11](https://en.wikipedia.org/wiki/PKCS_11 "wikipedia:PKCS 11"), [PKCS #12](https://en.wikipedia.org/wiki/PKCS_12 "wikipedia:PKCS 12"), [S/MIME](https://en.wikipedia.org/wiki/S/MIME "wikipedia:S/MIME"), [X.509](https://en.wikipedia.org/wiki/X.509 "wikipedia:X.509") v3 certificates, and other security standards.

## Contents

*   [1 Installation](#Installation)
*   [2 Certificate management](#Certificate_management)
    *   [2.1 List certificate DB](#List_certificate_DB)
    *   [2.2 Import certificate](#Import_certificate)
    *   [2.3 Edit certificate](#Edit_certificate)
    *   [2.4 Delete certificate](#Delete_certificate)
*   [3 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") [nss](https://www.archlinux.org/packages/?name=nss), available in the [official repositories](/index.php/Official_repositories "Official repositories").

## Certificate management

Use _certutil_ utility provided with NSS to manage your certificates.

### List certificate DB

To get list of all certificates:

```
$ certutil -d sql:$HOME/.pki/nssdb -L

```

To get details about certificate:

```
$ certutil -d sql:$HOME/.pki/nssdb -L -n _certificate_nickname_

```

### Import certificate

To add a certificate specify the `-A` option:

```
$ certutil -d sql:$HOME/.pki/nssdb -A -t "_TRUSTARGS_" -n _certificate_nickname_ -i _/path/to/cert/filename_

```

The `TRUSTARGS` are three strings of zero or more alphabetic characters, separated by commas, for example: `"TCu,Cu,Tuw"`. They define how the certificate should be trusted for SSL, email, and object signing, and are explained in the [certutil docs](http://www.mozilla.org/projects/security/pki/nss/tools/certutil.html#1034193) or [Meena's blog post](https://blogs.oracle.com/meena/entry/notes_about_trust_flags) on trust flags.

To add a personal certificate and private key for SSL client authentication use the command:

```
$ pk12util -d sql:$HOME/.pki/nssdb -i _/path/to/PKCS12/cert/filename.p12_

```

This will import a personal certificate and private key stored in a PKCS #12 file. The `TRUSTARGS` of the personal certificate will be set to `"u,u,u"`.

### Edit certificate

Call _certutil_ with `-M` option to edit the certificate. For example, to edit the `TRUSTARGS`:

```
$ certutil -d sql:$HOME/.pki/nssdb -M -t "_TRUSTARGS_" -n _certificate_nickname_

```

### Delete certificate

Use `-D` option to remove the certificate:

```
$ certutil -d sql:$HOME/.pki/nssdb -D -n _certificate_nickname_

```

## See also

*   [Network Security Services](http://www.mozilla.org/projects/security/pki/nss/) on mozilla.org.
*   [Using the Certificate Database Tool](http://www.mozilla.org/projects/security/pki/nss/tools/certutil.html#1034193) on mozilla.org.
*   [Certificate management](http://code.google.com/p/chromium/wiki/LinuxCertManagement) on Chromium help.
*   [Managing Certificate Trust flags in NSS Database](http://blogs.oracle.com/meena/entry/notes_about_trust_flags) on Meena's blog.