This page covers usage of package signing with [pacman](/index.php/Pacman "Pacman"), as well as being a brain dump and collaborative design document. To set up package signing in pacman, see [pacman-key](/index.php/Pacman-key "Pacman-key").

See also: [DeveloperWiki:Package Signing Proposal for Pacman](/index.php/DeveloperWiki:Package_Signing_Proposal_for_Pacman "DeveloperWiki:Package Signing Proposal for Pacman")

Pacman 4 uses [GnuPG](/index.php/GnuPG "GnuPG") to implement package signing.

## Contents

*   [1 Usage](#Usage)
    *   [1.1 Arch implementation](#Arch_implementation)
    *   [1.2 Signature checking](#Signature_checking)
*   [2 Course of action for development](#Course_of_action_for_development)
    *   [2.1 Documentation](#Documentation)
    *   [2.2 Additional Features](#Additional_Features)
        *   [2.2.1 Package validation without root privileges](#Package_validation_without_root_privileges)
        *   [2.2.2 Timeline for increasing security](#Timeline_for_increasing_security)
*   [3 How signing is implemented in other distributions](#How_signing_is_implemented_in_other_distributions)
    *   [3.1 Frugalware](#Frugalware)
    *   [3.2 Gnuffy](#Gnuffy)
    *   [3.3 Debian](#Debian)
        *   [3.3.1 Binary packages (.deb)](#Binary_packages_.28.deb.29)
        *   [3.3.2 Source packages](#Source_packages)
    *   [3.4 Gentoo](#Gentoo)
    *   [3.5 Red Hat/Fedora/CentOS](#Red_Hat.2FFedora.2FCentOS)
        *   [3.5.1 Pros](#Pros)
        *   [3.5.2 Cons](#Cons)
    *   [3.6 SUSE](#SUSE)
    *   [3.7 Slackware](#Slackware)
    *   [3.8 Ubuntu](#Ubuntu)
        *   [3.8.1 Cons](#Cons_2)
*   [4 Links](#Links)
    *   [4.1 Bug reports](#Bug_reports)
    *   [4.2 Blogs](#Blogs)
    *   [4.3 Forum discussions](#Forum_discussions)

## Usage

### Arch implementation

*   Packages are signed using `makepkg --sign`. This creates a detached binary signature (.sig).
*   The signed package is added to the repository database, and a detached signature of the repository database will be generated, using `repo-add --verify --sign`. The command line options indicate that the signature of the old database will be verified, and that the new database will be signed. Independently of these options, `repo-add` will detect the detached signature, convert it via base64 to ASCII, and add it to the repository database.
*   `pacman` will download both the databases and the database signatures and verify the databases upon database sync and each time the database is opened. When a package is loaded, its signature will be checked whether that comes from a repo database or a standalone .sig file.
*   `pacman-key` exists for the sake of managing keys, but there is missing functionality

### Signature checking

To prepare for checking signed packages, run the [pacman-key](/index.php/Pacman-key "Pacman-key") command shown below, with root permissions. It generates a random key and a “keyring” in `/etc/pacman.d/gnupg/`. You may need to move the mouse around to generate [entropy](/index.php/Pacman-key#How_can_I_collect_entropy.3F "Pacman-key") for the key.

```
# pacman-key --init

```

If this command is never run, pacman will abort saying “*failed to commit transaction (invalid or corrupted package [PGP signature])*” when it encounters packages signed with an unknown key.

Pacman usually prompts to add new keys of signed packages to its keyring. Keys can be manually compared against the lists of Arch [developers](/index.php/Developer "Developer") and [trusted users](/index.php/Trusted_Users "Trusted Users") on the [Arch Linux web site](https://www.archlinux.org). If the *SigLevel* configuration specifies “TrustAll”, pacman considers keys to be trusted once they are imported to the keyring, so it will then continue installing each package. If pacman does not prompt to add new keys (cannot find on configured key server perhaps?), they could still be added manually by using the [pacman-key](/index.php/Pacman-key "Pacman-key") tool.

If *SigLevel* specifies *TrustedOnly* (the default), pacman also considers the “trust level” for each key. A key is considered trusted if it is locally signed, or it has a sufficient level in the pacman web of trust. Locally signing a key (with `pacman-key --lsign`) only really works after the key has already been imported.

If there is a long time and failure right after checking packages integrity, edit `/etc/pacman.d/gnupg/gpg.conf` to use a different key server, for example `keyserver hkp://pgp.mit.edu` instead of keys.gnupg.net.

## Course of action for development

### Documentation

Documentation for the new features must be reviewed and finalized.

### Additional Features

These are important but non-essential features that should be added soon after package signing is implemented. Work on these issues can start now, but priority should be given to the "requirements" above.

#### Package validation without root privileges

Currently, pacman's GnuPG home directory (aka gpgdir, typically /etc/pacman.d/gnupg/) must be locked in order to check a package's signature. Only root can perform this locking, so either locking must be disabled for read-only accesses, or the directory must be copied/linked to a writable location when a user is performing package verification.

#### Timeline for increasing security

A timeline for transitioning between some unsigned packages and a fully-signed set of packages must be made. This is the responsibility of the developers.

## How signing is implemented in other distributions

### Frugalware

Frugalware uses a fork of pacman which implements package signing (verify)

### Gnuffy

Arch based distro gnuffy uses signed packages with their custom package manager [Spaceman](http://gnuffy.chaotika.org/index.php/Spaceman) modeled on pacman.

### Debian

#### Binary packages (.deb)

To sum up, the GPG signature is included in the .deb.

Details:

Regular non signed binary packages are "ar" archives of at least 3 files:

*   data.tar.gz (files to be installed)
*   control.tar.gz (package metadata)
*   debian-binary (contains the version of the deb format)

Signed packages also have a _gpgorigin file at the root of the .deb that is a "gpg -abs" of the concatenation of the 3 laters (as [explained here](http://purplefloyd.wordpress.com/2009/02/05/signing-deb-packages/)):

```
cat debian-binary control.tar.gz data.tar.gz > /tmp/combined-contents
gpg -abs -o _gpgorigin /tmp/combined-contents (-a "Create ASCII armored output" ; -b "detach signature" ; -s "sign")

```

#### Source packages

Original files are provided on [the repo](http://ftp.de.debian.org/debian/pool/main/a/acpid/) like this [acpid_2.0.4.orig.tar.gz](http://ftp.de.debian.org/debian/pool/main/a/acpid/acpid_2.0.4.orig.tar.gz) with diff if necessary ([acpid_2.0.4-1.diff.gz](http://ftp.de.debian.org/debian/pool/main/a/acpid/acpid_2.0.4-1.diff.gz)). A [description file](http://ftp.de.debian.org/debian/pool/main/a/acpid/acpid_2.0.4-1.dsc) containing MD5sums of the orig.tar.gz and diff.gz is written and signed using GPG and uploaded along these.

### Gentoo

According to the Gentoo wiki, individual ebuilds are not signed.

### Red Hat/Fedora/CentOS

*   Signature type: GPG
*   Stored: in the RPM

A RPM package is a tarball of installed files to which is added a header made up of metadata (name of package, version, ...). This metadata can contain a GPG signature of the tarball. See the [file format specification for details](http://www.rpm.org/wiki/DevelDocs/FileFormat).

NB: packages built for the Red Hat Network are signed with the [Red Hat official key(s)](https://www.redhat.com/security/team/key/) but technically a RPM can be signed using any other key (one can even add another signature to the RPM)

To check a package correction, one must first import the signer's key first: Example for Red Hat:

```
rpm --import /usr/share/doc/rpm-4.1/RPM-GPG-KEY

```

And can then check signature manually:

```
$ rpm -K openldap-clients-2.3.43-4.x86_64.rpm 
  openldap-clients-2.3.43-4.x86_64.rpm: sha1 md5 OK

```

And even fully check the package (MD5):

```
$ rpm -Kv openldap-clients-2.3.43-4.x86_64.rpm 
  openldap-clients-2.3.43-4.x86_64.rpm:
     SHA1 header hash: OK (65999383ad859be0ce337aee4c1f6bd049ebe4a0)
     MD5 sum: OK (4be23a341d23b794d08fbee35c459c83)

```

Option `--nogpg` prevents rpm from checking GPG signatures

#### Pros

*   Enable Official Distribution package signature but also enables personal and multiple signatures

#### Cons

*   Implies complicated package format with header containing signature of an inner tarball (not very KISS)
*   Space greedy on repos

### SUSE

### Slackware

### Ubuntu

For each package, a small description file containing the SHA sum of the package is created. That file is then signed using gpg (.dsc) and uploaded within the same folder as the package:

```
gpg --clearsign description_of_package

```

See [result](http://security.ubuntu.com/ubuntu/pool/main/a/acpid/acpid_1.0.4-1ubuntu11.2.dsc) for [acpid in Ubuntu](http://security.ubuntu.com/ubuntu/pool/main/a/acpid/)

#### Cons

*   Space greedy (2 files for 1 package)

## Links

### Bug reports

1.  [Bugreport Signed packages](https://bugs.archlinux.org/task/5331)

### Blogs

1.  [Attack on package managers](http://www.cs.arizona.edu/people/justin/packagemanagersecurity/attacks-on-package-managers.html#overview)
2.  [Attack faq](http://www.cs.arizona.edu/people/justin/packagemanagersecurity/faq.html)

### Forum discussions

1.  [Pacman vulnerable to MITM attacks?](https://bbs.archlinux.org/viewtopic.php?id=35609)
2.  [Arch approach to security](https://bbs.archlinux.org/viewtopic.php?pid=333982#p333982)
3.  [Pacman Veanurability](https://bbs.archlinux.org/viewtopic.php?id=58302)
4.  [Package signing](https://bbs.archlinux.org/viewtopic.php?id=27867)
5.  [pacman vulnerabilities](https://bbs.archlinux.org/viewtopic.php?id=51570)