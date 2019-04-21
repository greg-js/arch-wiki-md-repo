According to [Wikipedia](https://en.wikipedia.org/wiki/Transport_Layer_Security "wikipedia:Transport Layer Security"):

	**Transport Layer Security** (**TLS**), and its now-deprecated[[1]](https://tools.ietf.org/html/rfc7568) predecessor, **Secure Sockets Layer** (**SSL**), are cryptographic protocols designed to provide communications security over a computer network. Several versions of the protocols find widespread use in applications such as web browsing, email, instant messaging, and voice over IP (VoIP). Websites can use TLS to secure all communications between their servers and web browsers.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Implementations](#Implementations)
*   [2 Certificate authorities](#Certificate_authorities)
*   [3 Trust management](#Trust_management)
    *   [3.1 Trust a certificate authority system-wide](#Trust_a_certificate_authority_system-wide)
*   [4 Obtaining a certificate](#Obtaining_a_certificate)
*   [5 Server-side recommendations](#Server-side_recommendations)
    *   [5.1 Checking TLS](#Checking_TLS)
*   [6 Miscellaneous](#Miscellaneous)
    *   [6.1 ACME clients](#ACME_clients)
    *   [6.2 OCSP](#OCSP)
    *   [6.3 HSTS](#HSTS)
*   [7 See also](#See_also)

## Implementations

There are four TLS implementations available in the [official repositories](/index.php/Official_repositories "Official repositories"). OpenSSL is the only one part of the [base group](/index.php/Base_group "Base group") (albeit indirectly).

*   **[OpenSSL](/index.php/OpenSSL "OpenSSL")** — A robust, commercial-grade, and full-featured toolkit for the TLS and SSL protocols; also a general-purpose cryptography library.

	[https://www.openssl.org/](https://www.openssl.org/) || [openssl](https://www.archlinux.org/packages/?name=openssl)

*   **[GnuTLS](/index.php/GnuTLS "GnuTLS")** — A free software implementation of the TLS, SSL and DTLS protocols. Offers APIs for X.509, PKCS #12, OpenPGP and other structures.

	[https://www.gnutls.org/](https://www.gnutls.org/) || [gnutls](https://www.archlinux.org/packages/?name=gnutls)

*   **[Network Security Services](/index.php/Network_Security_Services "Network Security Services") (NSS)** — Implementation of cryptographic libraries supporting TLS/SSL and [S/MIME](https://en.wikipedia.org/wiki/S/MIME "wikipedia:S/MIME"). Also supports TLS acceleration and smart cards.

	[https://developer.mozilla.org/NSS](https://developer.mozilla.org/NSS) || [nss](https://www.archlinux.org/packages/?name=nss)

*   **[mbed TLS](/index.php/Mbed_TLS "Mbed TLS")** — Portable SSL/TLS implementation, aka PolarSSL.

	[https://tls.mbed.org/](https://tls.mbed.org/) || [mbedtls](https://www.archlinux.org/packages/?name=mbedtls)

## Certificate authorities

With TLS one of a set of [certificate authorities](https://en.wikipedia.org/wiki/Certificate_authority "wikipedia:Certificate authority") (CAs) signs for the authenticity of a [public key certificate](https://en.wikipedia.org/wiki/public_key_certificate "wikipedia:public key certificate") from a server. A client system connecting to the server via TLS may verify its certificate's authenticity by relying on a CA certificate obtained via a separate path. On Arch Linux the certificate authorities are provided by the [ca-certificates](https://www.archlinux.org/packages/?name=ca-certificates) package, which is indirectly part of the [base group](/index.php/Base_group "Base group"), because of the dependency chain ([pacman](/index.php/Pacman "Pacman") > [curl](https://www.archlinux.org/packages/?name=curl) > [ca-certificates](https://www.archlinux.org/packages/?name=ca-certificates)), and has the following dependency tree (excerpt):

*   [ca-certificates](https://www.archlinux.org/packages/?name=ca-certificates)
    Is just an anchor point, other packages depend on.
    *   [ca-certificates-mozilla](https://www.archlinux.org/packages/?name=ca-certificates-mozilla)
        Contains only the `/usr/share/ca-certificates/trust-source/mozilla.trust.p11-kit` file, generated from the [Mozilla CA Certificate Store](https://www.mozilla.org/en-US/about/governance/policies/security-group/certs/), which is also part of NSS (`/usr/lib/libnssckbi.so`).
        *   [ca-certificates-utils](https://www.archlinux.org/packages/?name=ca-certificates-utils)
            Provides the [update-ca-trust(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/update-ca-trust.8) script and the same-named [pacman hook](/index.php/Pacman_hook "Pacman hook").
            *   [p11-kit](https://www.archlinux.org/packages/?name=p11-kit)
                Provides the [trust(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/trust.1) utility.

## Trust management

See [Security#Managing SSL certificates](/index.php/Security#Managing_SSL_certificates "Security") on how to blacklist a certificate authority.

### Trust a certificate authority system-wide

**Warning:** This allows anyone with access to the private key to intercept all of your TLS traffic.

```
# trust anchor *certificate*.crt

```

This is for example required to allow a [HTTPS MITM proxy](/index.php/Proxy_server#HTTPS_MITM_proxies "Proxy server") to intercept traffic.

## Obtaining a certificate

The first step is to generate an RSA private key. Before generating the key, set a restrictive file mode creation mask with [umask](/index.php/Umask "Umask") (for example `077`).

**Note:** The [openssl](https://www.archlinux.org/packages/?name=openssl) package does not properly safeguard the `/etc/ssl/private` directory like most other distributions do, see [FS#43059](https://bugs.archlinux.org/task/43059).

A certificate can be obtained either from a certificate authority with a [Certificate Signing Request](https://en.wikipedia.org/wiki/Certificate_signing_request "wikipedia:Certificate signing request") (CSR) or [self-signed](https://en.wikipedia.org/wiki/Self-signed_certificate "wikipedia:Self-signed certificate"). While self-signed certificates can be generated easily, clients will reject them by default, meaning that every client needs to be configured to trust the self-signed certificate.

For the actual generation commands refer to the article of the used implementation:

*   [OpenSSL#Usage](/index.php/OpenSSL#Usage "OpenSSL")
*   [GnuTLS#Usage](/index.php/GnuTLS#Usage "GnuTLS")
*   [Network Security Services#Usage](/index.php/Network_Security_Services#Usage "Network Security Services")
*   [mbed TLS#Usage](/index.php/Mbed_TLS#Usage "Mbed TLS")

**Tip:** You can get free certificates from the [Let's Encrypt](https://letsencrypt.org/) certificate authority with [ACME](#ACME_clients).

## Server-side recommendations

Because there are [various attacks against TLS](https://en.wikipedia.org/wiki/Transport_Layer_Security#Attacks_against_TLS.2FSSL "wikipedia:Transport Layer Security") the best practices should be considered:

*   [Disable SSLv3](https://disablessl3.com/) to prevent the [POODLE](https://en.wikipedia.org/wiki/POODLE "wikipedia:POODLE") attack.
*   [weakdh.org's Guide to Deploying Diffie-Hellman for TLS](https://weakdh.org/sysadmin.html)
*   [Mozilla's Server Side TLS article](https://wiki.mozilla.org/Security/Server_Side_TLS "mozillawiki:Security/Server Side TLS")
*   [SSL Labs' SSL and TLS Deployment Best Practices](https://github.com/ssllabs/research/wiki/SSL-and-TLS-Deployment-Best-Practices)
*   [Cipherli.st](https://cipherli.st/)

### Checking TLS

Programs to check TLS:

*   [testssl.sh](https://www.archlinux.org/packages/?name=testssl.sh)
*   [Nmap](/index.php/Nmap "Nmap")
*   [OpenSSL](/index.php/OpenSSL "OpenSSL")
*   [cipherscan](https://github.com/mozilla/cipherscan)

Websites to check TLS:

*   [https://dev.ssllabs.com/ssltest/](https://dev.ssllabs.com/ssltest/) (only HTTPS)
*   [https://www.checktls.com/](https://www.checktls.com/) (only email)
*   [https://www.htbridge.com/ssl/](https://www.htbridge.com/ssl/) (any port)
*   [https://tls.imirhil.fr/tls](https://tls.imirhil.fr/tls) (any port)

## Miscellaneous

### ACME clients

The [Automated Certificate Management Environment](https://en.wikipedia.org/wiki/Automated_Certificate_Management_Environment "wikipedia:Automated Certificate Management Environment") (ACME) protocol lets you request valid X.509 certificates from [certificate authorities](https://en.wikipedia.org/wiki/Certificate_authority "wikipedia:Certificate authority"), like [Let's Encrypt](https://letsencrypt.org/).

See also [List of ACME clients](https://letsencrypt.org/docs/client-options/).

*   **acme-client** — Secure Let's Encrypt client, written in C.

	[https://kristaps.bsd.lv/acme-client/](https://kristaps.bsd.lv/acme-client/) || [acme-client](https://aur.archlinux.org/packages/acme-client/)

*   **acme-tiny** — A 200-line Python script to issue and renew TLS certs from Let's Encrypt.

	[https://github.com/diafygi/acme-tiny](https://github.com/diafygi/acme-tiny) || [acme-tiny](https://www.archlinux.org/packages/?name=acme-tiny)

*   **acme.sh** — A pure Unix shell script ACME client.

	[https://github.com/Neilpang/acme.sh](https://github.com/Neilpang/acme.sh) || [acme.sh-git](https://aur.archlinux.org/packages/acme.sh-git/)

*   **acmetool** — An easy-to-use ACME CLI, written in Go.

	[https://github.com/hlandau/acme](https://github.com/hlandau/acme) || [acmetool](https://aur.archlinux.org/packages/acmetool/), [acmetool-git](https://aur.archlinux.org/packages/acmetool-git/)

*   **[Certbot](/index.php/Certbot "Certbot")** — ACME client recommended by Let's Encrypt, written in Python.

	[https://github.com/certbot/certbot](https://github.com/certbot/certbot) || [certbot](https://www.archlinux.org/packages/?name=certbot)

*   **dehydrated** — ACME client, written in Bash.

	[https://github.com/lukas2511/dehydrated](https://github.com/lukas2511/dehydrated) || [dehydrated](https://www.archlinux.org/packages/?name=dehydrated), [dehydrated-git](https://aur.archlinux.org/packages/dehydrated-git/)

*   **getssl** — ACME client, written in Bash.

	[https://github.com/srvrco/getssl](https://github.com/srvrco/getssl) || [getssl](https://aur.archlinux.org/packages/getssl/), [getssl-git](https://aur.archlinux.org/packages/getssl-git/)

*   **lego** — Lets Encrypt client and ACME library, written in Go.

	[https://github.com/xenolf/lego](https://github.com/xenolf/lego) || [lego-git](https://aur.archlinux.org/packages/lego-git/)

*   **letsencrypt-cli** — Yet another Letsencrypt (ACME) client using Ruby.

	[https://github.com/zealot128/ruby-acme-cli](https://github.com/zealot128/ruby-acme-cli) || [letsencrypt-cli](https://aur.archlinux.org/packages/letsencrypt-cli/)

*   **manuale** — A fully manual Let's Encrypt client, written in Python.

	[https://github.com/veeti/manuale](https://github.com/veeti/manuale) || [manuale](https://aur.archlinux.org/packages/manuale/)

*   **ruby-acme-client** — A Ruby client for the letsencrypt's ACME protocol.

	[https://github.com/unixcharles/acme-client](https://github.com/unixcharles/acme-client) || [ruby-acme-client](https://aur.archlinux.org/packages/ruby-acme-client/)

*   **simp_le** — Simple Let's Encrypt client, written in Python.

	[https://github.com/zenhack/simp_le](https://github.com/zenhack/simp_le) || [simp_le-git](https://aur.archlinux.org/packages/simp_le-git/)

### OCSP

The [Online Certificate Status Protocol](https://en.wikipedia.org/wiki/Online_Certificate_Status_Protocol "wikipedia:Online Certificate Status Protocol") (OCSP) is supported by [Firefox](/index.php/Firefox "Firefox"). [Chromium](/index.php/Chromium "Chromium") has its own mechanism[[2]](http://dev.chromium.org/Home/chromium-security/crlsets).

See also [ocsptool(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ocsptool.1) by GnuTLS and [ocsp(1ssl)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ocsp.1ssl) by OpenSSL.

### HSTS

The [HTTP Strict Transport Security](https://en.wikipedia.org/wiki/HTTP_Strict_Transport_Security "wikipedia:HTTP Strict Transport Security") (HSTS) mechanism is supported by Firefox, Chromium and [wget](/index.php/Wget "Wget") (`~/.wget-hsts`).

## See also

*   [Gentoo:Certificates](https://wiki.gentoo.org/wiki/Certificates "gentoo:Certificates")
*   [A note about SSL/TLS trusted certificate stores, and platforms (OpenSSL and GnuTLS)](https://www.happyassassin.net/2015/01/12/a-note-about-ssltls-trusted-certificate-stores-and-platforms/)