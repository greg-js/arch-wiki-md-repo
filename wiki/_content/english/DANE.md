[DANE](https://en.wikipedia.org/wiki/DNS-based_Authentication_of_Named_Entities "w:DNS-based Authentication of Named Entities") (DNS-based Authentication of Named Entities) is a protocol to allow X.509 certificates, commonly used for Transport Layer Security (TLS), to be bound to DNS names using Domain Name System Security Extensions (DNSSEC).

## Resource Record

TLSA resource record is an own type of DNS record. It consists of port number and protocol of the service secured by it. An example record for port 25 over tcp could look like `_25._tcp.example.com IN TLSA 3 0 1 $DATA`. The TLSA parameters `3 0 1` are explaining the data following it. The first number is the Certificate Usage Field, the second is the Selector Field and the third is named Matching Type Field.

<caption>Certificate Usage Field</caption>
| Value | Name | Description |
| 0 | PKIX trust anchor | Hash contains a public CA from the x509 tree by which your cert has to be signed |
| 1 | PKIX end entity | Hash contains your cert which also has to pass x509 validation |
| 2 | DANE trust anchor | Hash contains a private CA (unknown to the x509 tree) by which your cert has to be signed |
| 3 | DANE end entity | Hash contains your cert which is not matched against any other validation |

<caption>Selector Field</caption>
| Value | Name | Description |
| 0 | cert | DATA is based on the full cert |
| 1 | SPKI | DATA is based on public key only |

<caption>Matching Type Field</caption>
| Value | Name | Description |
| 0 | Full | DATA ist the full cert or SPKI |
| 1 | sha256 | DATA is the sha256 hash of the cert or SPKI |
| 2 | sha512 | DATA is the sha512 hash of the cert or SPKI |

The RR can also easily be generated with the tools `ldns-dane` from [ldns](https://www.archlinux.org/packages/?name=ldns) and `dane` from [sshfp](https://aur.archlinux.org/packages/sshfp/).

## DANE supporting software

*   [Postfix](/index.php/Postfix#Dane "Postfix")
*   Exim > 4.85
*   Prosody (via [prosody-mod-s2s-auth-dane](https://aur.archlinux.org/packages/prosody-mod-s2s-auth-dane/))

## See also

*   [DANE Validator](https://danetools.com/dane)
*   [Common implementation mistakes](https://dane.sys4.de/common_mistakes)
*   [Generate TLSA records online](https://www.huque.com/bin/gen_tlsa)