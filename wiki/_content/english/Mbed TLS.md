According to [Wikipedia](https://en.wikipedia.org/wiki/mbed_TLS "wikipedia:mbed TLS"):

	**mbed TLS** (previously **PolarSSL**) is an implementation of the TLS and SSL protocols and the respective cryptographic algorithms and support code required. It is dual-licensed with the Apache License version 2.0 (with GPLv2 also available). Stated on the website is that mbed TLS aims to be "easy to understand, use, integrate and expand".

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 Generate an RSA private key](#Generate_an_RSA_private_key)
    *   [2.2 Generate a certificate signing request](#Generate_a_certificate_signing_request)
    *   [2.3 Generate a self-signed certificate](#Generate_a_self-signed_certificate)
*   [3 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [mbedtls](https://www.archlinux.org/packages/?name=mbedtls) package.

## Usage

The command names start with "mbedtls_", for usage examples see the [Knowledge Base](https://tls.mbed.org/kb).

### Generate an RSA private key

```
$ mbedtls_gen_key rsa_keysize=*keysize* filename=*filename*

```

### Generate a certificate signing request

```
$ mbedtls_cert_req filename=*private_key* subject_name=*subject* output_file=*filename*

```

[Relevant how-to](https://tls.mbed.org/kb/how-to/generate-a-certificate-request-csr)

### Generate a self-signed certificate

```
$ mbedtls_cert_write selfsign=1 issuer_key=*private_key* issuer_name=*subject* not_before=*YYYYMMDDHHMMSS* not_after=*YYYYMMDDHHMMSS* is_ca=1 max_pathlen=0 output_file=*file*

```

[Relevant how-to](https://tls.mbed.org/kb/how-to/generate-a-self-signed-certificate)

## See also

*   [Official website](https://tls.mbed.org/)
*   [API documentation](https://tls.mbed.org/api/)