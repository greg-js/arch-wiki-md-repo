Because there are [various attacks against TLS](https://en.wikipedia.org/wiki/Transport_Layer_Security#Attacks_against_TLS.2FSSL "wikipedia:Transport Layer Security") it is important to follow the [best practices](#Best_practices).

## Best practices

Obtain your certificate as described in [OpenSSL#Certificates](/index.php/OpenSSL#Certificates "OpenSSL").

*   [Disable SSLv3](https://disablessl3.com/) to prevent the [POODLE](https://en.wikipedia.org/wiki/POODLE "wikipedia:POODLE") attack.
*   [weakdh.org's Guide to Deploying Diffie-Hellman for TLS](https://weakdh.org/sysadmin.html)
*   [Mozilla's Server Side TLS article](https://wiki.mozilla.org/Security/Server_Side_TLS "mozillawiki:Security/Server Side TLS")
*   [SSL Labs' SSL and TLS Deployment Best Practices](https://github.com/ssllabs/research/wiki/SSL-and-TLS-Deployment-Best-Practices)
*   [Cipherli.st](https://cipherli.st/)

## Checking TLS

Programs to check TLS:

*   [testssl.sh](https://www.archlinux.org/packages/?name=testssl.sh)
*   [Nmap](/index.php/Nmap "Nmap")
*   [OpenSSL](/index.php/OpenSSL "OpenSSL")
*   [cipherscan](https://github.com/mozilla/cipherscan)

Websites to check TLS:

*   [https://www.ssllabs.com/ssltest/](https://www.ssllabs.com/ssltest/) (only HTTPS)
*   [https://www.checktls.com/](https://www.checktls.com/) (only email)