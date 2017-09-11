Related articles

*   [Security#Password hashes](/index.php/Security#Password_hashes "Security")

The Secure Hash Algorithms (SHA) are a set of [hash functions](https://en.wikipedia.org/wiki/Cryptographic_hash_function "wikipedia:Cryptographic hash function") often used to encrypt passwords. By default Arch uses SHA-512 for passwords, but some systems may still be using the older [MD5](https://en.wikipedia.org/wiki/MD5 "wikipedia:MD5") algorithm. This article describes how to increase password security.

## Benefits of SHA-2 over MD5

In Linux distributions login passwords are commonly hashed and stored in the `/etc/shadow` file using the [MD5 algorithm](https://en.wikipedia.org/wiki/MD5 "wikipedia:MD5"). The security of the MD5 hash function has been severely compromised by [collision vulnerabilities](https://en.wikipedia.org/wiki/MD5#Collision_vulnerabilities "wikipedia:MD5"). This does not mean MD5 is insecure for password hashing but in the interest of decreasing vulnerabilities a more secure and robust algorithm that has no known weaknesses (e.g. SHA-512) is recommended.

The following tutorial uses the SHA-512 hash function, which has been recommended by the United States' National Security Agency (NSA) for Red Hat Enterprise Linux 5\. Alternatively, [SHA-2](https://en.wikipedia.org/wiki/SHA-2 "wikipedia:SHA-2") consists of four additional hash functions with digests that are 224, 256, 384, and 512 bits.

## Increasing security

**Note:** With [shadow](https://www.archlinux.org/packages/?name=shadow) 4.1.4.3-3 *sha512* is the default for new passwords (see [bug 13591](https://bugs.archlinux.org/task/13591#comment85993)).

If your current password was created with [shadow](https://www.archlinux.org/packages/?name=shadow) version prior to 4.1.4.3-3 (2011-11-26) you are using MD5\. To start using a SHA-512 hash you just need to change your password with *passwd*.

**Note:** You must have root privileges to edit this file.

The `rounds=N` option helps to improve [key strengthening](https://en.wikipedia.org/wiki/Key_stretching "wikipedia:Key stretching"). The number of rounds has a larger impact on security than the selection of a hash function. For example, `rounds=65536` means that an attacker has to compute 65536 hashes for each password he tests against the hash in your `/etc/shadow`. Therefore the attacker will be delayed by a factor of 65536\. This also means that your computer must compute 65536 hashes every time you log in, but even on slow computers that takes less than 1 second. If you do not use the `rounds` option, then glibc will **default** to **5000** rounds for SHA-512\. Additionally, the default value for the `rounds` option can be found in `sha512-crypt.c`.

Open `/etc/pam.d/passwd` with a text editor and add the `rounds` option at the end of of the uncommented line. After applying this change the line should look like this:

```
password	required	pam_unix.so sha512 shadow nullok **rounds=65536**

```

**Note:** For a more detailed explanation of the `/etc/pam.d/passwd` password options check the [pam_unix(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/pam_unix.8) man page.

## Re-hash the passwords

Even though you have changed the encryption settings, your passwords are not automatically re-hashed. To fix this, you must reset all user passwords so that they can be re-hashed.

As root issue the following command,

```
# passwd *username*

```

where `*username*` is the name of the user whose password you are changing. Then re-enter their current password, and it will be re-hashed using the SHA-2 function.

To verify that your passwords have been re-hashed, check the `/etc/shadow` file as root. Passwords hashed with SHA-256 should begin with a `$5` and passwords hashed with SHA-512 will begin with `$6`.