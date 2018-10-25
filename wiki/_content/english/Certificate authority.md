Arch Linux uses the [Certificate authority](https://en.wikipedia.org/wiki/Certificate_authority "wikipedia:Certificate authority") (CA) [store from Mozilla](https://www.mozilla.org/en-US/about/governance/policies/security-group/certs/). In particular the certificates are provided by the [ca-certificates-mozilla](https://www.archlinux.org/packages/?name=ca-certificates-mozilla) package, which is indirectly part of the [base group](/index.php/Base_group "Base group") because of the following dependency chain: ([pacman](/index.php/Pacman "Pacman") > [curl](https://www.archlinux.org/packages/?name=curl) > [ca-certificates](https://www.archlinux.org/packages/?name=ca-certificates) > [ca-certificates-mozilla](https://www.archlinux.org/packages/?name=ca-certificates-mozilla)). *ca-certificates-mozilla* in turn depends on [ca-certificates-utils](https://www.archlinux.org/packages/?name=ca-certificates-utils), which provides the [update-ca-trust(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/update-ca-trust.8) command and depends on [p11-kit](https://www.archlinux.org/packages/?name=p11-kit), which provides the [trust(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/trust.1) utility.

## Tools

| Package | Tools |
| [ca-certificates-utils](https://www.archlinux.org/packages/?name=ca-certificates-utils) | [update-ca-trust(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/update-ca-trust.8) |
| [p11-kit](https://www.archlinux.org/packages/?name=p11-kit) | [trust(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/trust.1) |
| [Network Security Services](/index.php/Network_Security_Services "Network Security Services") | [certutil(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/certutil.1) |

## Trusting certificates system-wide

**Warning:** This allows the private key-holder to impersonate any website for your system.

```
# trust anchor *certificate*.crt

```

## Miscellaneous

[Chromium](/index.php/Chromium "Chromium") and [Firefox](/index.php/Firefox "Firefox") depend on [Network Security Services](/index.php/Network_Security_Services "Network Security Services") ([nss](https://www.archlinux.org/packages/?name=nss)).

While Firefox uses the [OCSP](https://en.wikipedia.org/wiki/OCSP "wikipedia:OCSP"), Chromium has its own mechanism.[[1]](http://dev.chromium.org/Home/chromium-security/crlsets)