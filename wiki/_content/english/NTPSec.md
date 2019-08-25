Related articles

*   [Network Time Protocol daemon](/index.php/Network_Time_Protocol_daemon "Network Time Protocol daemon")

The NTP is an unencrypted UDP based protocol and has been [abused](https://www.youtube.com/watch?v=hkw9tFnJk8k) for attacks in the past. There have been [several](https://github.com/ioerror/tlsdate) [attempts](https://www.imperialviolet.org/2016/09/19/roughtime.html) to provide replacements, however the difficult nature of the protocol and its usage make this quite challenging. While the NTP provides capabilities for encryption, they have been proven to be [unreliable](https://translate.google.com/translate?hl=en&sl=de&u=https://www.golem.de/news/tls-gcm-gefahr-durch-doppelte-nonces-1605-121005.html&prev=search). With [NTPSec](https://ntpsec.org/) a ['secure'](https://docs.ntpsec.org/latest/ntpsec.html) replacement is possible.

## Installation

You can install NTPSec via the [ntpsec](https://aur.archlinux.org/packages/ntpsec/) package.

**Note:** Any that other NTP services will be uninstalled by NTPSec.

It is necessary to import a new GPG key to your keyring with:

 `$ gpg --recv-keys 5A22E330161C3978` 
```
gpg: key 5A22E330161C3978: 6 signatures not checked due to missing keys
gpg: key 5A22E330161C3978: public key "NTPsec Contact <contact@ntpsec.org>" imported
gpg: marginals needed: 3  completes needed: 1  trust model: pgp
gpg: depth: 0  valid:   8  signed:   0  trust: 0-, 0q, 0n, 0m, 0f, 8u
gpg: next trustdb check due at 2019-12-03
gpg: Total number processed: 1
gpg:               imported: 1

```

## Starting the service

Normally [start/enable](/index.php/Start/enable "Start/enable") the `ntpd.service`.

## See also

*   [Wikipedia:Network Time Protocol#NTPsec](https://en.wikipedia.org/wiki/Network_Time_Protocol#NTPsec "wikipedia:Network Time Protocol")