[Network Security Services](https://en.wikipedia.org/wiki/Network_Security_Services "wikipedia:Network Security Services") (**NSS**) is a set of libraries designed to support cross-platform development of security-enabled client and server applications.

Applications built with NSS can support [SSL](https://en.wikipedia.org/wiki/SSL "wikipedia:SSL") v2 and v3, [TLS](/index.php/TLS "TLS"), [PKCS](https://en.wikipedia.org/wiki/PKCS "wikipedia:PKCS") #5, #7, [PKCS #11](https://en.wikipedia.org/wiki/PKCS_11 "wikipedia:PKCS 11"), [PKCS #12](https://en.wikipedia.org/wiki/PKCS_12 "wikipedia:PKCS 12"), [S/MIME](https://en.wikipedia.org/wiki/S/MIME "wikipedia:S/MIME"), [X.509](https://en.wikipedia.org/wiki/X.509 "wikipedia:X.509") v3 certificates, and other security standards.

NSS is required by many packages, including, for example, [Chromium](/index.php/Chromium "Chromium") and [Firefox](/index.php/Firefox "Firefox").

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 List certificate DB](#List_certificate_DB)
    *   [2.2 Generate an RSA private key](#Generate_an_RSA_private_key)
    *   [2.3 Generate a certificate signing request](#Generate_a_certificate_signing_request)
    *   [2.4 Generate a self-signed certificate](#Generate_a_self-signed_certificate)
    *   [2.5 Import certificate](#Import_certificate)
    *   [2.6 Edit certificate](#Edit_certificate)
    *   [2.7 Delete certificate](#Delete_certificate)
*   [3 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [nss](https://www.archlinux.org/packages/?name=nss) package.

## Usage

Use *certutil* utility provided with NSS to manage your certificates.

### List certificate DB

To get list of all certificates:

```
$ certutil -d sql:$HOME/.pki/nssdb -L

```

To get details about certificate:

```
$ certutil -d sql:$HOME/.pki/nssdb -L -n *certificate_nickname*

```

### Generate an RSA private key

```
$ certutil -G -d *database_directory* -g *keysize* -n *nickname*

```

### Generate a certificate signing request

```
$ certutil -S -s *subject* -n *nickname* -x -t C,C,C -o *file*

```

### Generate a self-signed certificate

```
$ certutil -S -s *subject* -n *nickname* -x -t C,C,C -o *file*

```

### Import certificate

To add a certificate specify the `-A` option:

```
$ certutil -d sql:$HOME/.pki/nssdb -A -t "*TRUSTARGS*" -n *certificate_nickname* -i */path/to/cert/filename*

```

The `TRUSTARGS` are three strings of zero or more alphabetic characters, separated by commas, for example: `"TCu,Cu,Tuw"`. They define how the certificate should be trusted for SSL, email, and object signing, and are explained in the [certutil docs](http://www.mozilla.org/projects/security/pki/nss/tools/certutil.html#1034193) or [Meena's blog post](https://blogs.oracle.com/meena/entry/notes_about_trust_flags) on trust flags.

To add a personal certificate and private key for SSL client authentication use the command:

```
$ pk12util -d sql:$HOME/.pki/nssdb -i */path/to/PKCS12/cert/filename.p12*

```

This will import a personal certificate and private key stored in a PKCS #12 file. The `TRUSTARGS` of the personal certificate will be set to `"u,u,u"`.

### Edit certificate

Call *certutil* with `-M` option to edit the certificate. For example, to edit the `TRUSTARGS`:

```
$ certutil -d sql:$HOME/.pki/nssdb -M -t "*TRUSTARGS*" -n *certificate_nickname*

```

### Delete certificate

Use `-D` option to remove the certificate:

```
$ certutil -d sql:$HOME/.pki/nssdb -D -n *certificate_nickname*

```

## See also

*   [Network Security Services - Mozilla](https://developer.mozilla.org/en-US/docs/Mozilla/Projects/NSS)
*   [Using the Certificate Database Tool - Mozilla](https://developer.mozilla.org/en-US/docs/Mozilla/Projects/NSS/tools/NSS_Tools_certutil#Using_the_Certificate_Database_Tool)
*   [Linux Cert Management - Chromium](https://chromium.googlesource.com/chromium/src/+/master/docs/linux_cert_management.md)
*   [Managing Certificate Trust flags in NSS Database - Meena Vyas, Oracle](https://blogs.oracle.com/meena/about-trust-flags-of-certificates-in-nss-database-that-can-be-modified-by-certutil)