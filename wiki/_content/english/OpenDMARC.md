Domain-based Message Authentication, Reporting and Conformance (DMARC) is a policy for mail transfer, which is already supported by some common mail providers. It depends on [SPF](/index.php/SPF "SPF") and [DKIM](/index.php/OpenDKIM "OpenDKIM"). DMARC provides and a policy for outgoing mail and checks incoming mails for compliance with that policy. The policy is published via a DNS TXT record. It is explained in [#Record](#Record). Validation is done in a daemon. Its configuration is explained in [#Validator](#Validator). For more info see the [IETF draft](https://datatracker.ietf.org/doc/draft-kucherawy-dmarc-base/).

## Contents

*   [1 Record](#Record)
*   [2 Validator](#Validator)
    *   [2.1 Installation](#Installation)
    *   [2.2 Basic configuration](#Basic_configuration)
    *   [2.3 Postfix integration](#Postfix_integration)
*   [3 Security](#Security)
*   [4 Weblinks](#Weblinks)

## Record

An example record looks like this: `v=DMARC1;p=quarantine;pct=100;rua=mailto:postmaster@example.org;ruf=mailto:forensik@example.org;adkim=s;aspf=r`. It is entered as TXT record on the `_dmarc`-subdomain of your domain.

| Tag name | Purpose | Sample |
| v | Protocol version | v=DMARC1 |
| pct | Percentage of messages subjected to filtering | pct=20 |
| ruf | Reporting URI for forensic reports | ruf=[mailto:authfail@example.com](mailto:authfail@example.com) |
| rua | Reporting URI of aggregate reports | rua=[mailto:aggrep@example.com](mailto:aggrep@example.com) |
| p | Policy for organizational domain | p=quarantine |
| sp | Policy for subdomains of the | sp=reject |
| adkim | Alignment mode for DKIM | adkim=s |
| aspf | Alignment mode for SPF | aspf=r |
| fo | Forensic report options | fo=1 |
| rf | Reporting format. either afrf or iodef | rf=afrf |
| ri | Reporting interval of aggregate reports. Often disregarded | ri=86400 |

The alignment modes for DKIM and SPF can be s for strict and r for relaxed, where the latter allows a subdomain in the From header while the former does not. The domain policy (p) and subdomain policy (sp) might be one of `monitor`, `quarantine` or `reject`. The forensic report option are "0" to generate reports if all underlying authentication mechanisms fail to produce a DMARC pass result, "1" to generate reports if any mechanisms fail, "d" to generate report if the DKIM signature failed to verify, or "s" if SPF failed.

## Validator

### Installation

[Install](/index.php/Install "Install") the [opendmarc](https://www.archlinux.org/packages/?name=opendmarc) package.

### Basic configuration

Main configuration file is `/etc/opendmarc/opendmarc.conf`

*   Copy/move the sample configuration file `/etc/opendmarc/opendmarc.conf.sample` to `/etc/opendmarc/opendmarc.conf` and change the following options:

 `/etc/opendmarc/opendmarc.conf` 
```
Socket                  unix:/run/opendmarc/opendmarc.sock
UserID                  opendmarc

```

If you want to run your DMARC-Validator on a different machine, you should change the Socket field to `inet:9999@10.0.0.4` with a sample host listening at at port 9999 for an optional client 10.0.0.4 (can be omitted, listens on 0.0.0.0 then).

*   [Enable](/index.php/Enable "Enable") and [start](/index.php/Start "Start") the `opendmarc.service`. Read [Daemons](/index.php/Daemons "Daemons") for more information.

### Postfix integration

Add the following lines to `main.cf`:

 `/etc/postfix/main.cf` 
```
non_smtpd_milters   = unix:/run/opendkim/opendkim.sock, unix:/run/opendmarc/opendmarc.sock
smtpd_milters       = unix:/run/opendkim/opendkim.sock, unix:/run/opendmarc/opendmarc.sock
```

Make sure that the DMARC milter is declared after the DKIM milter.

## Security

The daemon can drop privileges on its own (as configured in the [#Validator](#Validator) section with the `UserID` option); however, as the daemon does not need root privileges, it can be started as a non-privileged user with systemd. To accomplish this, use the following systemd unit file and comment out the `UserID` option and add `Umask=002` (to allow for socket creation and writing) in the OpenDMARC config file.

 `/etc/systemd/system/opendmarc.service` 
```
[Unit]
Description=OpenDMARC daemon
After=network.target remote-fs.target nss-lookup.target

[Service]
Type=forking
User=opendmarc
Group=postfix
ExecStart=/usr/bin/opendmarc -c /etc/opendmarc/opendmarc.conf
RuntimeDirectory=opendmarc
RuntimeDirectoryMode=0750

[Install]
WantedBy=multi-user.target

```

## Weblinks

*   [DMARC Inspector](https://dmarcian.com/dmarc-inspector/)