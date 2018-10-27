According to [Wikipedia](https://en.wikipedia.org/wiki/GnuTLS "wikipedia:GnuTLS"):

	**GnuTLS** (the **GNU Transport Layer Security Library**) is a free software implementation of the TLS, SSL and DTLS protocols. It offers an application programming interface (API) for applications to enable secure communication over the network transport layer, as well as interfaces to access X.509, PKCS #12, OpenPGP and other structures.

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 Generate an RSA private key](#Generate_an_RSA_private_key)
    *   [2.2 Generate a certificate signing request](#Generate_a_certificate_signing_request)
    *   [2.3 Generate a self-signed certificate](#Generate_a_self-signed_certificate)
*   [3 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [gnutls](https://www.archlinux.org/packages/?name=gnutls) package.

For integration with the [Apache HTTP Server](/index.php/Apache_HTTP_Server "Apache HTTP Server") install [mod_gnutls](/index.php/Mod_gnutls "Mod gnutls").

## Usage

See [certtool(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/certtool.1) for the command used in the following sections and the [info document](https://www.gnutls.org/manual/html_node/index.html) for the API documentation.

### Generate an RSA private key

```
$ certtool -p --rsa --bits=*keysize*

```

### Generate a certificate signing request

```
$ certtool -q --load-privkey *private_key* --outfile *file*

```

### Generate a self-signed certificate

```
$ certtool -s --load-privkey *private_key* --outfile *file*

```

## See also

*   [Official website](https://www.gnutls.org/)