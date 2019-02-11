Related articles

*   [Transport Layer Security](/index.php/Transport_Layer_Security "Transport Layer Security")

[OpenSSL](http://www.openssl.org) is an open-source implementation of the SSL and [TLS](/index.php/TLS "TLS") protocols, designed to be as flexible as possible. It is supported on a variety of platforms, including BSD, Linux, OpenVMS, Solaris and Windows.

**Warning:** Collaborated research into OpenSSL protocol usage, published in May 2015, showed further significant risks for SSL connections; named "Logjam" attack. See [https://weakdh.org/](https://weakdh.org/) for results and [https://weakdh.org/sysadmin.html](https://weakdh.org/sysadmin.html) for suggested server-side configuration changes.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 req section](#req_section)
*   [3 Usage](#Usage)
    *   [3.1 Generate an RSA private key](#Generate_an_RSA_private_key)
    *   [3.2 Generate a certificate signing request](#Generate_a_certificate_signing_request)
    *   [3.3 Generate a self-signed certificate](#Generate_a_self-signed_certificate)
    *   [3.4 Generate Diffie–Hellman parameters](#Generate_Diffie–Hellman_parameters)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 "bad decrypt" while decrypting](#"bad_decrypt"_while_decrypting)
*   [5 See also](#See_also)

## Installation

[openssl](https://www.archlinux.org/packages/?name=openssl) is installed by default on Arch Linux (as a dependency of [coreutils](https://www.archlinux.org/packages/?name=coreutils)).

There are various OpenSSL library bindings available for developers:

*   [python-pyopenssl](https://www.archlinux.org/packages/?name=python-pyopenssl), [python2-pyopenssl](https://www.archlinux.org/packages/?name=python2-pyopenssl)
*   [perl-net-ssleay](https://www.archlinux.org/packages/?name=perl-net-ssleay)
*   [lua-sec](https://www.archlinux.org/packages/?name=lua-sec), [lua52-sec](https://www.archlinux.org/packages/?name=lua52-sec), [lua51-sec](https://www.archlinux.org/packages/?name=lua51-sec)
*   [haskell-hsopenssl](https://www.archlinux.org/packages/?name=haskell-hsopenssl)
*   [haskell-openssl-streams](https://www.archlinux.org/packages/?name=haskell-openssl-streams)

## Configuration

On Arch Linux the `OPENSSLDIR` is `/etc/ssl`.

The OpenSSL configuration file, conventionally placed in `/etc/ssl/openssl.cnf`, may appear complicated at first. Remember that variables may be expanded in assignments, much like how shell scripts work. For a thorough explanation of the configuration file format, see [config(5ssl)](https://jlk.fjfi.cvut.cz/arch/manpages/man/config.5ssl).

### req section

Settings related to generating keys, requests and self-signed certificates.

The req section is responsible for the DN prompts. A general misconception is the *Common Name* (CN) prompt, which suggests that it should have the user's proper name as a value. End-user certificates need to have the **machine hostname** as CN, whereas CA should *not* have a valid TLD, so that there is no chance that, between the possible combinations of certified end-users' CN and the CA certificate's, there is a match that could be misinterpreted by some software as meaning that the end-user certificate is self-signed. Some CA certificates do not even have a CN, such as [Equifax](http://www.equifax.com):

 `$ openssl x509 -subject -noout < /etc/ssl/certs/Equifax_Secure_CA.pem`  `subject= /C=US/O=Equifax/OU=Equifax Secure Certificate Authority` 

## Usage

This sections assumes you have read [Transport Layer Security#Obtaining a certificate](/index.php/Transport_Layer_Security#Obtaining_a_certificate "Transport Layer Security").

### Generate an RSA private key

With [genpkey(1ssl)](https://jlk.fjfi.cvut.cz/arch/manpages/man/genpkey.1ssl), which supersedes *genrsa* according to [openssl(1ssl)](https://jlk.fjfi.cvut.cz/arch/manpages/man/openssl.1ssl):

```
$ openssl genpkey -algorithm RSA -pkeyopt rsa_keygen_bits:*keysize* -out *file*

```

If an encrypted key is desired, use the `-aes-256-cbc` option.

### Generate a certificate signing request

Use [req(1ssl)](https://jlk.fjfi.cvut.cz/arch/manpages/man/req.1ssl):

```
$ openssl req -new -sha256 -key *private_key* -out *filename*

```

### Generate a self-signed certificate

```
$ openssl req -key *private_key* -x509 -new -days *days* -out *filename*

```

### Generate Diffie–Hellman parameters

See [Diffie–Hellman key exchange](https://en.wikipedia.org/wiki/Diffie%E2%80%93Hellman_key_exchange "wikipedia:Diffie–Hellman key exchange") for more information.

```
$ openssl dhparam -out *filename* *2048*

```

**Tip:** To speed up generating, especially when not on high-end hardware, add the `-dsaparam` option [[1]](https://security.stackexchange.com/questions/95178/diffie-hellman-parameters-still-calculating-after-24-hours/95184#95184).

## Troubleshooting

### "bad decrypt" while decrypting

OpenSSL 1.1.0 changed the default digest algorithm for the dgst and enc commands from MD5 to SHA256\. [[2]](https://www.openssl.org/news/changelog.html#x6)

Therefore if a file has been encrypted using OpenSSL 1.0.2 or older, trying to decrypt it with an up to date version may result in an error like:

```
error:06065064:digital envelope routines:EVP_DecryptFinal_ex:bad decrypt:crypto/evp/evp_enc.c:540

```

Supplying the `-md md5` option should solve the issue:

```
$ openssl enc -d -md md5 -in encrypted -out decrypted

```

## See also

*   [Wikipedia page](https://en.wikipedia.org/wiki/OpenSSL "wikipedia:OpenSSL") on OpenSSL, with background information.
*   [OpenSSL](http://www.openssl.org) project page.
*   [FreeBSD Handbook](http://www.freebsd.org/doc/en/books/handbook/openssl.html)
*   [Step-by-step guide to create a signed SSL certificate](http://www.akadia.com/services/ssh_test_certificate.html)
*   [OpenSSL Certificate Authority](https://jamielinux.com/docs/openssl-certificate-authority/)
*   [Bulletproof SSL and TLS](https://www.feistyduck.com/books/bulletproof-ssl-and-tls/bulletproof-ssl-and-tls-introduction.pdf) by Ivan Ristić, a more formal introduction to SSL/TLS
*   [OpenSSL Certificate Authority — Jamie Nguyen](https://jamielinux.com/docs/openssl-certificate-authority/)