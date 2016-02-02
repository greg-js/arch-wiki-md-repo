# Random number generation

From [wikipedia:Random number generation](https://en.wikipedia.org/wiki/Random_number_generation "wikipedia:Random number generation"):

	A random number generator (RNG) is a computational or physical device designed to generate a sequence of numbers or symbols that lack any pattern, i.e. appear random.

Generation of random data is crucial for several applications like making cryptographic keys (e.g. for [Disk encryption](/index.php/Disk_encryption "Disk encryption")), [securely wiping disks](/index.php/Securely_wipe_disk "Securely wipe disk"), running encrypted [Software access points](/index.php/Software_access_point "Software access point").

## Contents

*   [1 Kernel built-in RNG](#Kernel_built-in_RNG)
    *   [1.1 /dev/random](#.2Fdev.2Frandom)
    *   [1.2 /dev/urandom](#.2Fdev.2Furandom)
*   [2 Faster alternatives](#Faster_alternatives)
*   [3 See also](#See_also)

## Kernel built-in RNG

The Linux kernel's built-in RNGs [/dev/{u}random](https://en.wikipedia.org/wiki//dev/random "wikipedia:/dev/random") are highly commended for producing reliable random data providing the same security level that is used for the creation of cryptographic keys. The random number generator gathers environmental noise from device drivers and other sources into an entropy pool.

Note that the `man random` command will misdirect to the library function manpage [random(3)](http://man7.org/linux/man-pages/man3/random.3.html) while for information about the `/dev/random` device files you should run `man 4 random` to read [random(4)](http://man7.org/linux/man-pages/man4/random.4.html).

### /dev/random

`/dev/random` uses an entropy pool of 4096 bits (512 Bytes) to generate random data and stops when the pool is exhausted until it gets (slowly) refilled. `/dev/random` is designed for generating cryptographic keys (e.g. SSL, SSH, dm-crypt's LUKS), but it is impractical to use for wiping current HDD capacities: what makes disk wiping take so long is waiting for the system to [gather enough true entropy](https://en.wikipedia.org/wiki/Hardware_random_number_generator#Using_observed_events "wikipedia:Hardware random number generator"). In an entropy-starved situation (e.g. a remote server) this might never end. While doing search operations on large directories or moving the mouse in X can slowly refill the entropy pool, it's designated pool size alone will be indication enough of the inadequacy for wiping a disk.

You can always compare `/proc/sys/kernel/random/entropy_avail` against `/proc/sys/kernel/random/poolsize` to keep an eye on the system's entropy pool.

While Linux kernel 2.4 did have writable `/proc` entries for controlling the entropy pool size, in newer kernels only `read_wakeup_threshold` and `write_wakeup_threshold` are writable. The pool size is now hardcoded in kernel line 275 of `/drivers/char/random.c`:

```
/*
 * Configuration information
 */
#define **INPUT_POOL_WORDS 128**
#define **OUTPUT_POOL_WORDS 32**
...
```

The kernel's pool size is given by `INPUT_POOL_WORDS * OUTPUT_POOL_WORDS` which makes, as already stated, 4096 bits.

**Warning:** Do not use even `/dev/random` to generate _critical_ cryptographic keys on a system you do not [control](http://everything2.com/title/Compromising+%252Fdev%252Frandom). If in doubt, for example in shared server environments, rather choose to create the keys on another system and transfer them. The cryptographer D. J. Bernstein illustrates the control problem with a [Mark Twain quotation](http://blog.cr.yp.to/20140205-entropy.html).

### /dev/urandom

In contrast to `/dev/random`, `/dev/urandom` reuses existing entropy pool data while the pool is replenished: the output will contain less entropy than the corresponding read from `/dev/random`, but its quality should be sufficient for a paranoid disk wipe, [preparing for block device encryption](/index.php/Securely_wipe_disk#Preparations_for_block_device_encryption "Securely wipe disk"), wiping LUKS keyslots, wiping single files and many other purposes.[[1]](http://www.2uo.de/myths-about-urandom/) [[2]](http://sockpuppet.org/blog/2014/02/25/safely-generate-random-numbers/) [[3]](https://www.mail-archive.com/cryptography@randombit.net/msg04748.html)

**Warning:** `/dev/urandom` is **not** recommended for the generation of long-term cryptographic keys.

## Faster alternatives

For applications other than the generation of long-term cryptographic keys, a practical compromise between performance and security is the use of a [pseudorandom number generator](https://en.wikipedia.org/wiki/Pseudorandom_number_generator "wikipedia:Pseudorandom number generator"). In Arch Linux repositories for example:

*   [Haveged](/index.php/Haveged "Haveged")
*   [Frandom](/index.php/Frandom "Frandom")
*   [rng-tools](/index.php/Rng-tools "Rng-tools")

There are also [cryptographically secure pseudorandom number generators](https://en.wikipedia.org/wiki/Cryptographically_secure_pseudorandom_number_generator "wikipedia:Cryptographically secure pseudorandom number generator") like [Yarrow](https://en.wikipedia.org/wiki/Yarrow_algorithm "wikipedia:Yarrow algorithm") (FreeBSD/OS-X) or [Fortuna](https://en.wikipedia.org/wiki/Fortuna_(PRNG) "wikipedia:Fortuna (PRNG)") (the intended successor of Yarrow).

## See also

*   [RFC4086 - Randomness Requirements for Security](http://www.ietf.org/rfc/rfc4086.txt) (Section 7.1.2 for /dev/random)
*   [Linux Kernel ML](http://lkml.indiana.edu/hypermail/linux/kernel/1302.1/00479.html) - discussion on patching /dev/random for higher throughput (February 2013)
*   [A challenge on /dev/random robustness](http://eprint.iacr.org/2013/338) (June 2013)
*   [An analysis of low entropy state](http://eprint.iacr.org/2014/167) behaviour of /dev/random, Yarrow, Fortuna and new model approach (March 2014)
*   [Randomness](http://www.random.org/randomness/) - A popular science article explaining different RNGs
*   [ENT](http://www.fourmilab.ch/random/) - A simple program for testing random sequences (entropy, Chi square test, Monte Carlo, correlation, etc.)
*   [DIY HRNG](http://www.codeproject.com/Articles/795845/Arduino-Hardware-Random-Sequence-Generator-with-Ja) - One example of a low-cost, DIY Arduino HRNG

Retrieved from "[https://wiki.archlinux.org/index.php?title=Random_number_generation&oldid=410093](https://wiki.archlinux.org/index.php?title=Random_number_generation&oldid=410093)"