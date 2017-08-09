Trusted Platform Module (TPM) is an international standard for a secure cryptoprocessor, which is a dedicated microprocessor designed to secure hardware by integrating cryptographic keys into devices.

In practice a TPM can be used for various different security applications such as secure boot and key storage.

TPM is naturally supported only on devices that have TPM hardware support. If your hardware has TPM support but it is not showing up, it might need to be enabled in the BIOS settings.

## Contents

*   [1 Versions](#Versions)
*   [2 Drivers](#Drivers)
*   [3 Usage](#Usage)
    *   [3.1 Basics](#Basics)
    *   [3.2 Securing SSH Keys](#Securing_SSH_Keys)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 tcsd.service failed to start](#tcsd.service_failed_to_start)
*   [5 See also](#See_also)

## Versions

**Note:** Support for TPM 2.0 is still incomplete (both on the kernel and in userspace), and no known workflow for TPM2 exists at the moment.

Current attempts to run `tcsd` on a system with TPM 2.0 will result in the following:

```
# cat /sys/class/tpm/tpm0/device/description 
TPM 2.0 Device

```

```
# tcsd -f
TCSD TDDL ioctl: (25) Inappropriate ioctl for device
TCSD TDDL Falling back to Read/Write device support.
TCSD TCS ERROR: TCS GetCapability failed with result = 0x1e

```

The rest of this article will focus only on TPM 1.2

## Drivers

TPM drivers are natively supported in modern kernels, but might need to be loaded:

```
# modprobe tpm

```

Depending on your chipset, you might also need to load one of the following:

```
# modprobe tpm_{atmel,bios,infineon,nsc,tis,crb}

```

## Usage

TPM is managed by `tcsd`, a userspace daemon that manages Trusted Computing resources and should be (according to the TSS spec) the only portal to the TPM device driver. `tcsd` is part of the [trousers](https://aur.archlinux.org/packages/trousers/) AUR package, which was created and released by IBM, and can be configured via `/etc/tcsd.conf`.

To start tcsd and watch the output, run:

```
# tcsd -f

```

or simply start and enable `tcsd.service`.

Once `tcsd` is running you might also want to install [tpm-tools](https://aur.archlinux.org/packages/tpm-tools/) which provides many of the command line tools for managing the TPM.

Some other tools of interest:

*   **tpmmanager** — A Qt front-end to tpm-tools

	[http://sourceforge.net/projects/tpmmanager](http://sourceforge.net/projects/tpmmanager) || [tpmmanager](https://aur.archlinux.org/packages/tpmmanager/)

*   **openssl_tpm_engine** — OpenSSL engine which interfaces with the TSS API

	[http://sourceforge.net/projects/trousers](http://sourceforge.net/projects/trousers) || [openssl_tpm_engine](https://aur.archlinux.org/packages/openssl_tpm_engine/)

*   **tpm_keyring2** — A key manager for TPM based eCryptfs keys

	[http://sourceforge.net/projects/trousers](http://sourceforge.net/projects/trousers) || [tpm_keyring2](https://aur.archlinux.org/packages/tpm_keyring2/)

*   **opencryptoki** — A PKCS#11 implementation for Linux. It includes drivers and libraries to enable IBM cryptographic hardware as well as a software token for testing.

	[http://sourceforge.net/projects/opencryptoki](http://sourceforge.net/projects/opencryptoki) || [opencryptoki](https://aur.archlinux.org/packages/opencryptoki/)

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

There are several methods to use TPM to secure keys, but here we show a simple method based on [simple-tpm-pk11-git](https://aur.archlinux.org/packages/simple-tpm-pk11-git/).

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

## Troubleshooting

### tcsd.service failed to start

The `tcsd.service` service may not start correctly due to permissions issues. [[1]](https://bugs.launchpad.net/ubuntu/+source/trousers/+bug/963587/comments/3). It's possible to fix this using:

```
$ chown tss:tss /dev/tpm*
$ chown -R tss:tss /var/lib/tpm

```

## See also

*   [TPM on Wikipedia](https://en.wikipedia.org/wiki/Trusted_Platform_Module "wikipedia:Trusted Platform Module")
*   [Protecting systems with the TPM](http://lwn.net/Articles/674751/)
*   [Embedded Security Subsystem on Thinkwiki](http://www.thinkwiki.org/wiki/Embedded_Security_Subsystem)
*   [TPM Fundamentals (PDF)](http://www.cs.unh.edu/~it666/reading_list/Hardware/tpm_fundamentals.pdf)