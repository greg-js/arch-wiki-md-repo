Related articles

*   [GnuPG](/index.php/GnuPG "GnuPG")
*   [DeveloperWiki:Package signing](/index.php/DeveloperWiki:Package_signing "DeveloperWiki:Package signing")

To determine if packages are authentic, *pacman* uses [GnuPG keys](http://www.gnupg.org/) in a [web of trust](http://www.gnupg.org/gph/en/manual.html#AEN385) model. The current Master Signing Keys are found [here](https://www.archlinux.org/master-keys/). At least three of these Master Signing Keys are used to sign the Developer's and Trusted User's own keys. They are then used to sign their packages. Each user also has a unique PGP key, which is generated when you configure *pacman-key*. It is this web of trust that links the user's key to the master keys.

Examples of webs of trust:

*   **Custom packages**: Packages made and signed with a local key.
*   **Unofficial packages**: Packages made and signed by a developer. Then, a local key was used to sign the developer's key.
*   **Official packages**: Packages made and signed by a developer. The developer's key was signed by the Arch Linux master keys. You used your key to sign the master keys, and you trust them to vouch for developers.

**Note:** The HKP protocol uses 11371/tcp for communication. In order to get the signed keys from the servers (using *pacman-key*), this port is required for communication.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Setup](#Setup)
    *   [1.1 Configuring pacman](#Configuring_pacman)
    *   [1.2 Initializing the keyring](#Initializing_the_keyring)
*   [2 Managing the keyring](#Managing_the_keyring)
    *   [2.1 Verifying the master keys](#Verifying_the_master_keys)
    *   [2.2 Adding developer keys](#Adding_developer_keys)
    *   [2.3 Adding unofficial keys](#Adding_unofficial_keys)
    *   [2.4 Debugging with gpg](#Debugging_with_gpg)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Cannot import keys](#Cannot_import_keys)
    *   [3.2 Disabling signature checking](#Disabling_signature_checking)
    *   [3.3 Resetting all the keys](#Resetting_all_the_keys)
    *   [3.4 Removing stale packages](#Removing_stale_packages)
    *   [3.5 Signature is unknown trust](#Signature_is_unknown_trust)
    *   [3.6 Updating keys via proxy](#Updating_keys_via_proxy)
*   [4 See also](#See_also)

## Setup

### Configuring pacman

The `SigLevel` option in `/etc/pacman.conf` determines the level of trust required to install a package. For a detailed explanation of `SigLevel` see the [pacman.conf man page](https://www.archlinux.org/pacman/pacman.conf.5.html#_package_and_database_signature_checking) and the file comments. One can set signature checking globally or per repository. If `SigLevel` is set globally in the `[options]` section, all packages will then require signing. Any packages you build will then need to be signed using *makepkg*.

**Note:** Although all official packages are now signed, as of November 2018 signing of the databases is a [work in progress](https://bbs.archlinux.org/viewtopic.php?id=242258). If `Required` is set then `DatabaseOptional` should also be set.

The default configuration will only support the installation of packages signed by trusted keys:

 `/etc/pacman.conf`  `SigLevel = Required DatabaseOptional` 

`TrustedOnly` is a default compiled-in *pacman* parameter. The default configuration is identical to using the global option of:

```
SigLevel = Required DatabaseOptional TrustedOnly

```

The above can be achieved too on a repository level further below in the configuration, e.g.:

```
[core]
SigLevel = PackageRequired
Include = /etc/pacman.d/mirrorlist

```

explicitly adds signature checking for the packages of the repository, but does not require the database to be signed. `Optional` here would turn off a global `Required` for this repository

**Warning:** The SigLevel `TrustAll` option exists for debugging purposes and makes it very easy to trust keys that have not been verified. You should use `TrustedOnly` for all official repositories.

### Initializing the keyring

To initialize the *pacman* keyring run:

```
# pacman-key --init

```

Initializing the keyring requires [entropy](https://en.wikipedia.org/wiki/Entropy_(computing) "wikipedia:Entropy (computing)"). To generate entropy, move your mouse around, press random characters on the keyboard, or run some disk-based activity (for example in another console running `ls -R /` or `find / -name foo` or `dd if=/dev/sda8 of=/dev/tty7`). If your system does not already have sufficient entropy, this step may take hours; if you actively generate entropy, it will complete much more quickly.

The randomness created is used to initialize the keyring (`/etc/pacman.d/gnupg`) and the GPG signing key of your system.

**Note:** If you need to run `pacman-key --init` on computer that does not generate much entropy (e.g. a headless server), key generation may take a very long time. To generate pseudo-entropy, install either [haveged](/index.php/Haveged "Haveged") or [rng-tools](/index.php/Rng-tools "Rng-tools") on the target machine and start the corresponding service before running `pacman-key --init`.

## Managing the keyring

### Verifying the master keys

The initial setup of keys is achieved using:

```
# pacman-key --populate archlinux

```

Take time to verify the [Master Signing Keys](https://www.archlinux.org/master-keys/) when prompted as these are used to co-sign (and therefore trust) all other packager's keys.

PGP keys are too large (2048 bits or more) for humans to work with, so they are usually hashed to create a 40-hex-digit fingerprint which can be used to check by hand that two keys are the same. The last eight digits of the fingerprint serve as a name for the key known as the '(short) key ID' (the last *sixteen* digits of the fingerprint would be the 'long key ID').

### Adding developer keys

The official developer and [Trusted Users](/index.php/Trusted_Users "Trusted Users") *(TU)* keys are signed by the master keys, so you do not need to use *pacman-key* to sign them yourself. Whenever *pacman* encounters a key it does not recognize, it will prompt to download it from a `keyserver` configured in `/etc/pacman.d/gnupg/gpg.conf` (or by using the `--keyserver` option on the command line). Wikipedia maintains a [list of keyservers](https://en.wikipedia.org/wiki/Key_server_(cryptographic) "wikipedia:Key server (cryptographic)").

Once you have downloaded a developer key, you will not have to download it again, and it can be used to verify any other packages signed by that developer.

**Note:** The [archlinux-keyring](https://www.archlinux.org/packages/?name=archlinux-keyring) package, which is a dependency of [pacman](https://www.archlinux.org/packages/?name=pacman), contains the latest keys. However keys can also be updated manually using `pacman-key --refresh-keys` (as root). While doing `--refresh-keys`, your local key will also be looked up on the remote keyserver, and you will receive a message about it being not found. This is nothing to be concerned about.

### Adding unofficial keys

This method can be utilized to add a key to the *pacman* keyring, or to enable signed [unofficial user repositories](/index.php/Unofficial_user_repositories "Unofficial user repositories").

First, get the **key ID** (`*keyid*`) from its owner. Then add it to the keyring using one of the two methods:

1.  If the key is found on a keyserver, import it with: `# pacman-key --recv-keys *keyid*` 
2.  If otherwise a link to a keyfile is provided, download it and then run: `# pacman-key --add */path/to/downloaded/keyfile*` 

It is recommended to verify the fingerprint, as with any master key or any other key you are going to sign:

```
$ pacman-key --finger *keyid*

```

Finally, you must locally sign the imported key:

```
# pacman-key --lsign-key *keyid*

```

You now trust this key to sign packages.

### Debugging with gpg

For debugging purposes, you can access *pacman'*s keyring directly with *gpg*, e.g.:

```
# gpg --homedir /etc/pacman.d/gnupg --list-keys

```

## Troubleshooting

**Warning:** *pacman-key* depends on [system time](/index.php/System_time "System time"). If your system clock is wrong, you'll get:
```
error: PackageName: signature from "User <email@archlinux.org>" is invalid
error: failed to commit transaction (invalid or corrupted package (PGP signature))
Errors occured, no packages were upgraded.

```

### Cannot import keys

There are multiple possible sources of this problem:

*   An outdated [archlinux-keyring](https://www.archlinux.org/packages/?name=archlinux-keyring) package.
*   Incorrect date.
*   Your ISP blocked the port used to import PGP keys.
*   Your *pacman* cache contains copy of unsigned packages from previous attempts.
*   `dirmngr` is not correctly configured

You might be stuck because of outdated [archlinux-keyring](https://www.archlinux.org/packages/?name=archlinux-keyring) package when doing an upgrade synchronization. Try if [upgrading the system](/index.php/Pacman#Upgrading_packages "Pacman") can fix it first.

If you are still having issues, make sure the following file exists `/root/.gnupg/dirmngr_ldapservers.conf` and that you can successfully run `# dirmngr`. Create an empty file if it doesn't and run `# dirmngr` again.

If it does not help and your date is correct, you could try to switch to the MIT keyserver, which provides an alternate port. To do this, edit `/etc/pacman.d/gnupg/gpg.conf` and change the `keyserver` line to:

```
keyserver hkp://pgp.mit.edu:11371

```

If even port 80 doesn't work (for example when company uses some kind of http-only "transparent" proxy instead of routing, following could work:

```
keyserver hkps://hkps.pool.sks-keyservers.net:443

```

If you have IPv6 disabled, *gpg* will fail when it found some IPv6 address. In this case try with an IPv4-only keyserver like:

```
keyserver hkp://ipv4.pool.sks-keyservers.net:11371

```

If you happen to forget to run `pacman-key --populate archlinux` you might get some errors while importing keys.

If none of this helps, your *pacman* cache, located at `/var/cache/pacman/pkg/` might contain unsigned packages from previous attempts. Try cleaning the cache manually or run:

```
# pacman -Sc

```

which removes all cached packages that have not been installed.

### Disabling signature checking

**Warning:** Use with caution. Disabling package signing will allow *pacman* to install untrusted packages automatically.

If you are not concerned about package signing, you can disable PGP signature checking completely. Edit `/etc/pacman.conf` and uncomment the following line under `[options]`:

```
SigLevel = Never

```

You need to comment out any repository-specific SigLevel settings too because they override the global settings. This will result in no signature checking, which was the behavior before pacman 4\. If you decide to do this, you do not need to set up a keyring with *pacman-key*. You can change this option later if you decide to enable package verification.

### Resetting all the keys

If you want to remove or reset all the keys installed in your system, you can remove `/etc/pacman.d/gnupg` folder as root and rerun `pacman-key --init` followed by `pacman-key --populate archlinux` to re-add the default keys.

### Removing stale packages

If the same packages keep failing and you are sure you did all the *pacman-key* stuff right, try removing them like so `rm /var/cache/pacman/pkg/*badpackage**` so that they are freshly downloaded.

This might actually be the solution if you get a message like `error: linux: signature from "Some Person <Some.Person@example.com>" is invalid` or similar when upgrading (i.e. you might not be the victim of a MITM attack after all, your downloaded file was simply corrupt).

### Signature is unknown trust

Sometimes when running `pacman -Suy` you might encounter this error:

```
error: *package-name*: signature from "*packager*" is unknown trust

```

This occurs because the `*packager*`'s key used in the package `*package-name*` is not present and/or not trusted in the local pacman-key gpg database. Pacman does not seem to always be able to check if the key was received and marked as trusted before continuing. This could also be because a key has expired since it was added to your keychain.

Mitigate by:

*   Refreshing your keys with `pacman-key --refresh-keys`, or
*   [manually signing the untrusted key locally](#Adding_unofficial_keys), or
*   [resetting all the keys](#Resetting_all_the_keys).

### Updating keys via proxy

In order to use a proxy when updating keys the `honor-http-proxy` option must be set in both `/etc/gnupg/dirmngr.conf` and `/etc/pacman.d/gnupg/dirmngr.conf`. See [GnuPG#Use a keyserver](/index.php/GnuPG#Use_a_keyserver "GnuPG") for more information.

**Note:** If *pacman-key* is used without the `honor-http-proxy` option and fails, a reboot may solve the issue.

## See also

*   [DeveloperWiki:Package Signing Proposal for Pacman](/index.php/DeveloperWiki:Package_Signing_Proposal_for_Pacman "DeveloperWiki:Package Signing Proposal for Pacman")
*   [Pacman Package Signing – 1: Makepkg and Repo-add](http://allanmcrae.com/2011/08/pacman-package-signing-1-makepkg-and-repo-add/)
*   [Pacman Package Signing – 2: Pacman-key](http://allanmcrae.com/2011/08/pacman-package-signing-2-pacman-key/)
*   [Pacman Package Signing – 3: Pacman](http://allanmcrae.com/2011/08/pacman-package-signing-3-pacman/)
*   [Pacman Package Signing – 4: Arch Linux](http://allanmcrae.com/2011/12/pacman-package-signing-4-arch-linux/)