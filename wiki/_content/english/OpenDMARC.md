Domain-based Message Authentication, Reporting and Conformance (DMARC) is a policy for mail transfer, which is already supported by some common mail providers. It depends on [SPF](/index.php/SPF "SPF") and [DKIM](/index.php/OpenDKIM "OpenDKIM"). DMARC provides and a policy for outgoing mail and checks incoming mails for compliance with that policy. The policy is published via a DNS TXT record. It is explained in [#DMARC Record](#DMARC_Record). Validation is done in a daemon. For more info see the [IETF draft](https://datatracker.ietf.org/doc/draft-kucherawy-dmarc-base/).

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Postfix integration](#Postfix_integration)
*   [4 DMARC Record](#DMARC_Record)
    *   [4.1 DMARC options in detail](#DMARC_options_in_detail)
*   [5 Weblinks](#Weblinks)

## Installation

[Install](/index.php/Install "Install") the [opendmarc](https://www.archlinux.org/packages/?name=opendmarc) package.

## Configuration

Main configuration file is `/etc/opendmarc/opendmarc.conf`

Change the following options:

 `/etc/opendmarc/opendmarc.conf` 
```
Socket                  unix:/run/opendmarc/opendmarc.sock

```

Add the socket directory and set its credentials to be accessible to the STMP server user (likely `postfix` or `mail`:

```
# mkdir /run/opendmarc
# chown opendmarc:postfix /run/opendmarc

```

**Note:** If you want to run your DMARC-Validator on a different machine, you should change the Socket field to `inet:9999@10.0.0.4` with a sample host listening at at port 9999 for an optional client 10.0.0.4 (can be omitted, listens on 0.0.0.0 then).

*   [Enable](/index.php/Enable "Enable") and [start](/index.php/Start "Start") the `opendmarc.service`. Read [Daemons](/index.php/Daemons "Daemons") for more information.

## Postfix integration

Add the following lines to `main.cf`:

 `/etc/postfix/main.cf` 
```
non_smtpd_milters   = unix:/run/opendkim/opendkim.sock, unix:/run/opendmarc/opendmarc.sock
smtpd_milters       = unix:/run/opendkim/opendkim.sock, unix:/run/opendmarc/opendmarc.sock
```

Make sure that the DMARC milter is declared after the DKIM milter.

## DMARC Record

To enable DMARC for your website, you have to add a new TXT record to your websites DNS server. An example subdomain record like this:

```
_dmarc.example.com TXT v=DMARC1; p=quarantine; pct=20; adkim=s; aspf=r; fo=1; rua=[mailto:postmaster@example.com](mailto:postmaster@example.com); ruf=[mailto:forensic@example.com](mailto:forensic@example.com);

```

### DMARC options in detail

| Tag name | Purpose | Sample |
| v | Protocol version | v=DMARC1 |
| pct | Percentage of messages subjected to filtering | pct=20 |
| ruf | Reporting URI for forensic reports | ruf=[mailto:forensic@example.com](mailto:forensic@example.com) |
| rua | Reporting URI of aggregate reports | rua=[mailto:postmaster@example.com](mailto:postmaster@example.com) |
| p | Policy for organizational domain | p=quarantine |
| sp | Policy for subdomains of the | sp=reject |
| adkim | Alignment mode for DKIM | adkim=s |
| aspf | Alignment mode for SPF | aspf=r |
| fo | Forensic report options | fo=1 |
| rf | Reporting format. either afrf or iodef | rf=afrf |
| ri | Reporting interval of aggregate reports. Often disregarded | ri=86400 |

The alignment modes for DKIM and SPF can be:

*   "s" for strict
*   "r" for relaxed

where the latter allows a subdomain in the "From" header while the former does not.

The domain policy (p) and subdomain policy (sp) might be one of:

*   "none" (for monitor mode)
*   "quarantine"
*   "reject"

The forensic report options are:

*   "0" to generate reports if all underlying authentication mechanisms fail to produce a DMARC pass result
*   "1" to generate reports if any mechanisms fail
*   "d" to generate report if the DKIM signature failed to verify
*   "s" if SPF failed.

## Weblinks

*   [DMARC Inspector](https://dmarcian.com/dmarc-inspector/)
*   [IETF RFC 7489](https://datatracker.ietf.org/doc/rfc7489/)