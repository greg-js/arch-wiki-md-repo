# Trusted Platform Module

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Trusted Platform Module (TPM) is an international standard for a secure cryptoprocessor, which is a dedicated microprocessor designed to secure hardware by integrating cryptographic keys into devices.

In practice a TPM can be used for various different security applications such as secure boot and key storage.

TPM is naturally supported only on devices that have TPM hardware support. If your hardware has TPM support but it is not showing up, it might need to be enabled in the BIOS settings.

## Contents

*   [1 Drivers](#Drivers)
*   [2 Usage](#Usage)
    *   [2.1 Basics](#Basics)
    *   [2.2 Securing SSH Keys](#Securing_SSH_Keys)
*   [3 References](#References)

## Drivers

TPM drivers are natively supported in modern kernels, but might need to be loaded:

```
# modprobe tpm

```

Depending on your chipset, you might also need to load one of the following:

```
# modprobe tpm_atmel tpm_bios tpm_infineon tpm_nsc tpm_tis tpm_crb

```

## Usage

TPM is managed by `tcsd`, a userspace daemon that manages Trusted Computing resources and should be (according to the TSS spec) the only portal to the TPM device driver. `tcsd` is part of the [trousers](https://aur.archlinux.org/packages/trousers/)<sup><small>AUR</small></sup> AUR package, which was created and released by IBM, and can be configured via `/etc/tcsd.conf`.

To start tcsd and watch the output, run:

```
# tcsd -f

```

or simply start and enable `tcsd.service`.

Once `tcsd` is running you might also want to install [tpm-tools](https://aur.archlinux.org/packages/tpm-tools/)<sup><small>AUR</small></sup> which provides many of the command line tools for managing the TPM.

Some other tools of interest:

*   **tpmmanager** — A Qt front-end to tpm-tools

[http://sourceforge.net/projects/tpmmanager](http://sourceforge.net/projects/tpmmanager) || [tpmmanager](https://aur.archlinux.org/packages/tpmmanager/)<sup><small>AUR</small></sup>

*   **openssl_tpm_engine** — OpenSSL engine which interfaces with the TSS API

[http://sourceforge.net/projects/trousers](http://sourceforge.net/projects/trousers) || [openssl_tpm_engine](https://aur.archlinux.org/packages/openssl_tpm_engine/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/openssl_tpm_engine)]</sup>

*   **tpm_keyring2** — A key manager for TPM based eCryptfs keys

[http://sourceforge.net/projects/trousers](http://sourceforge.net/projects/trousers) || [tpm_keyring2](https://aur.archlinux.org/packages/tpm_keyring2/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/tpm_keyring2)]</sup>

*   **opencryptoki** — A PKCS#11 implementation for Linux. It includes drivers and libraries to enable IBM cryptographic hardware as well as a software token for testing.

[http://sourceforge.net/projects/opencryptoki](http://sourceforge.net/projects/opencryptoki) || [opencryptoki](https://aur.archlinux.org/packages/opencryptoki/)<sup><small>AUR</small></sup>

### Basics

Start off by getting basic version info:

```
$ tpm_version

```

and running a selftest:

```
$ tpm_selftest -l info
 TPM Test Results: 00000000 ...
 tpm_selftest succeeded

```

### Securing SSH Keys

There are several methods to use TPM to secure keys, but here we show a simple method based on [simple-tpm-pk11-git](https://aur.archlinux.org/packages/simple-tpm-pk11-git/)<sup><small>AUR</small></sup>.

First, create a new directory and generate the key:

```
$ mkdir ~/.simple-tpm-pk11
$ stpm-keygen -o ~/.simple-tpm-pk11/my.key

```

Point the config to the key:

 `~/.simple-tpm-pk11/config` 

```
key my.key

```

Now configure SSH to use the right PKCS11 provider:

 `~/.ssh/config` 

```
Host *
    PKCS11Provider /usr/lib/libsimple-tpm-pk11.so

```

It's now possible to generate keys with the PKCS11 provider:

```
$ ssh-keygen -D /usr/lib/libsimple-tpm-pk11.so

```

**Note:** This method currently does not allow for multiple keys to be generated and used.

## References

*   [TPM on Wikipedia](https://en.wikipedia.org/wiki/Trusted_Platform_Module)
*   [Embedded Security Subsystem on Thinkwiki](http://www.thinkwiki.org/wiki/Embedded_Security_Subsystem)
*   [TPM Fundamentals (PDF)](http://www.cs.unh.edu/~it666/reading_list/Hardware/tpm_fundamentals.pdf)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Trusted_Platform_Module&oldid=416502](https://wiki.archlinux.org/index.php?title=Trusted_Platform_Module&oldid=416502)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Security](/index.php/Category:Security "Category:Security")
*   [Other hardware](/index.php/Category:Other_hardware "Category:Other hardware")

Hidden category:

*   [Pages with broken package links](/index.php/Category:Pages_with_broken_package_links "Category:Pages with broken package links")