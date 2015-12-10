# Frandom

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

**This article or section is out of date.**

**Reason:** Needs updating to SystemD (Discuss in [Talk:Frandom#](https://wiki.archlinux.org/index.php/Talk:Frandom))

**frandom** is a fast alternative to [/dev/urandom](/index.php/Random_number_generation "Random number generation").

From the [frandom page](http://billauer.co.il/frandom.html): "The frandom suite comes as a Linux kernel module for several kernels, or a kernel patch for 2.4.22\. It implements a random number generator, which is 10-50 times faster than what you get from Linux' built-in `/dev/urandom`."

Does frandom generate good random numbers? For anything not related to cryptography the answer is probably "yes". Don't use frandom for cryptographic purposes though, as it internally uses the dated and vulnerable RC4 algorithm.

Beneath in the example section, you'll find 'real', 'user' and 'sys' information, what they mean you can find [here](http://stackoverflow.com/questions/556405/what-do-real-user-and-sys-mean-in-the-output-of-time1?answertab=active#tab-top).

## Installation

Frandom is available as a package from the [AUR](https://aur.archlinux.org/packages.php?ID=9869).

After installing frandom, you can make it available with:

```
# modprobe frandom

```

The `/dev/frandom` device should now exist on the filesystem.

## Wiping a disk

**Warning:** **frandom** uses the vulnerable RC4 algorithm. Therefore:

*   Do not use frandom for cryptographic purposes!
*   Usage for "randomising" large hard drives prior to [disk encryption](/index.php/Disk_encryption "Disk encryption") is not recommended as `RC4` may be distinguished from random noise. See [Securely wipe disk#Overwrite the target](/index.php/Securely_wipe_disk#Overwrite_the_target "Securely wipe disk") for other methods.

To use frandom to wipe a disk without encrypting it afterwards (for example for the simple destruction of data (even though overwriting the disk with /dev/zero would be sufficient and faster in this case)), use the `dd` command:

```
# dd if=/dev/frandom of=/dev/sdX

```

Here, `X` refers to the drive you want to wipe.

Refer to [Securely wipe disk](/index.php/Securely_wipe_disk "Securely wipe disk") for more general information on this topic.

## Example

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**This article or section is a candidate for merging with [Benchmarking disk wipes](/index.php/Benchmarking_disk_wipes "Benchmarking disk wipes").**

**Notes:** Maybe anyone can bring this to nicer Formatting, move it there and link to it? (Discuss in [Talk:Frandom#](https://wiki.archlinux.org/index.php/Talk:Frandom))

1) On a 1.73 GHZ Thinkpad T43 with 2 GB ram:

```
# time dd if=/dev/frandom of=/dev/sdb2
 dd: writing to `/dev/sdb2': No space left on device
 587384596+0 records in
 587384595+0 records out
 300740912640 bytes (301 GB) copied, 12844.6 s, 23.4 MB/s
 real    214m4.620s
 user    3m34.693s
 sys     77m28.660s

```

Summary: 300 GB in approx 3.5 hours

2) On a 2.4 GHZ (T8300 Core 2 Duo) Thinkpad T61 with 2 GB ram:

```
# dd if=/dev/frandom of=/dev/sdb bs=1M
  dd: writing `/dev/sdb': No space left on device
  476941+0 records in
  476940+0 records out
  500107862016 bytes (500 GB) copied, 5954.52 s, 84.0 MB/s

```

Summary: 500 GB in approx 1.65 hours

3) On a 2.8 GHz (Athlon2 X4) with 4 GB ram:

```
# dd if=/dev/frandom of=/dev/sdc3 bs=1M seek=100KB
  dd: writing `/dev/sdc3': No space left on device
  1807429+0 records in
  1807428+0 records out
  1895225712640 bytes (1.9 TB) copied, 20300.3 s, 93.4 MB/s

```

Summary: ~2TB in ~5.64 hours. However, on the same machine:

```
# dd if=/dev/frandom of=/dev/null bs=1M count=1000
  1000+0 records in
  1000+0 records out
  1048576000 bytes (1.0 GB) copied, 7.81581 s, 134 MB/s

```

versus

```
# dd if=/dev/urandom of=/dev/null bs=1M count=1000
  1000+0 records in
  1000+0 records out
  1048576000 bytes (1.0 GB) copied, 144.296 s, 7.3 MB/s

```

This makes frandom 10-20 times faster on this machine, meaning it would take approx 50-120 hours (2-5 days!) to randomize 2TB using urandom.

4) On a 2.70GHz (i7-2620M) ThinkPad x220 with 8GB Ram:

```
# time dd if=/dev/frandom of=/dev/sdc
  dd: writing to `/dev/sdc': No space left on device
  625140336+0 records in
  625140335+0 records out
  320071851520 bytes (320 GB) copied, 9618.12 s, 33.3 MB/s
  real    160m18.126s
  user    1m8.916s
  sys     36m16.401s

```

**Summary:** 320 GB in approx. 2.67 hours

5) On a 2.70GHz (i7-2620M) ThinkPad x220 with 8GB Ram:

```
# time dd if=/dev/frandom of=/dev/sdc
  dd: writing to `/dev/sde': Input/output error
  467085833+0 records in
  467085832+0 records out
  239147945984 bytes (239 GB) copied, 24675.2 s, 9.7 MB/s
  real    411m15.208s
  user    2m58.028s
  sys     83m14.188s

```

**Summary:** 500 GB in approx. 6.85 hours (connected on USB3)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Frandom&oldid=376066](https://wiki.archlinux.org/index.php?title=Frandom&oldid=376066)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Encryption](/index.php/Category:Encryption "Category:Encryption")
*   [File systems](/index.php/Category:File_systems "Category:File systems")