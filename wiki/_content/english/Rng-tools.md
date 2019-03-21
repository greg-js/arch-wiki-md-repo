Related articles

*   [haveged](/index.php/Haveged "Haveged")
*   [Trusted Platform Module](/index.php/Trusted_Platform_Module "Trusted Platform Module")
*   [Random number generation](/index.php/Random_number_generation "Random number generation")

The [rng-tools](https://git.kernel.org/cgit/utils/kernel/rng-tools/rng-tools.git/) is a set of utilities related to random number generation in kernel. The main program is **rngd**, a daemon developed to check and feed random data from hardware device to kernel entropy pool.

This is mainly useful to increase the quantity of entropy in kernel to make `/dev/random` faster. By default, `/dev/random` is very slow since it only collects entropy from [device drivers and other (slow) sources](https://en.wikipedia.org/wiki//dev/random "wikipedia:/dev/random"). *rngd* allows the use of faster entropy sources, mainly [hardware random number generators (TRNG)](https://en.wikipedia.org/wiki/Hardware_random_number_generator "wikipedia:Hardware random number generator"), present in modern hardware like [recent AMD/Intel processors](https://en.wikipedia.org/wiki/RdRand "wikipedia:RdRand"), [Via Nano](https://jve.linuxwall.info/blog/index.php?post/2013/08/19/Hardware-RNG-from-Via-CPU-(on-debibox)) or even [Raspberry Pi](http://scruss.com/blog/2013/06/07/well-that-was-unexpected-the-raspberry-pis-hardware-random-number-generator/).

While Linux itself uses the result from TRNG in `/dev/random`, if available, they are only used as a [XOR after the entropy is collected by kernel](https://www.lvh.io/posts/2013/10/thoughts-on-rdrand-in-linux.html). So `/dev/random`, by default, is slow even if you do have a TRNG. *rngd* feeds `/dev/random` itself, increasing the available entropy by far.

## Installation

[Install](/index.php/Install "Install") the [rng-tools](https://www.archlinux.org/packages/?name=rng-tools) package. [Start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") `rngd.service`.

## Configuration

The configuration file is located in `/etc/conf.d/rngd`. There is only one option though, that is `RNGD_OPTS`, the parameters to be passed to the daemon when running it with the included `rngd.service`. The default parameter (`""`, or blank) should work in the majority of cases.

By default, *rngd* will try to automatically detect your TRNG and use it. This is reported to work for Raspberry Pi and Intel Ivy Bridge CPU using the lastest versions of *rng-tools*. If this does not work, you may manually pass the [device file](https://en.wikipedia.org/wiki/Device_file "wikipedia:Device file") used by your TRNG, as in the below example:

```
RNGD_OPTS="-o /dev/random -r /dev/my_hw_random_device"

```

**Warning:** Some tutorials available on the Internet recommend the following line for systems without TRNG:
```
RNGD_OPTS="-o /dev/random -r /dev/urandom"

```
Of course, this is a [really bad idea](https://lwn.net/Articles/525459/), since you are simple filling the kernel entropy pool with entropy coming from the kernel itself! If your system does not have an available TRNG consider using [haveged](/index.php/Haveged "Haveged") instead. See [FS#34580](https://bugs.archlinux.org/task/34580) for details.

If your system does not have a [TPM module](https://en.wikipedia.org/wiki/Trusted_Platform_Module "wikipedia:Trusted Platform Module"), you may pass `"--no-tpm=1"` to `RNGD_OPTS` to suppress the following warning message from log:

```
Unable to open file: /dev/tpm0

```

By default *rngd* fills the entropy pool until at least 2048 bits of entropy are available. This is to avoid the TRNG to dominate the contents of the pool. You can override this setting if you really **trust** your TRNG. To do this, pass `"--fill-watermark=4096"` to `RNGD_OPTS`, for example (4096 is the maximum size of kernel's entropy pool by default, you shouldn't pass a value greater than the maximum either). Doing so may increase the performance of `/dev/random` even further, at the expense of maybe lower random number quality. However, it should be noted that the default setting is already sufficient for the majority of user cases.

## Testing and usage

You may test if *rngd* is working before enabling its service by running:

```
# rngd -f

```

A simple test to see if everything is working as it should is to run (in another terminal) the following command:

```
$ dd if=/dev/random of=/dev/null bs=1024 count=1 iflag=fullblock

```

Without *rngd*, the above command will take lots of time to run. With *rngd* working properly, the result should be almost instantaneous:

```
1+0 records in
1+0 records out
1024 bytes (1.0 kB, 1.0 KiB) copied, 0.0199623 s, 51.3 kB/s

```

A speed of around **50 kB/s** in *dd*'s output shows that everything is working properly. For comparison, without *rngd* you probably would get 0.0 kB/s (since the speed is too low).

Another interesting test is to run **rngtest**, to check the data using [FIPS 140-2 tests](https://en.wikipedia.org/wiki/FIPS_140-2 "wikipedia:FIPS 140-2"):

 `$ rngtest -c 1000 </dev/random` 
```
rngtest 5
Copyright (c) 2004 by Henrique de Moraes Holschuh
This is free software; see the source for copying conditions.  There is NO warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.

rngtest: starting FIPS tests...
rngtest: bits received from input: 20000032
rngtest: FIPS 140-2 successes: 999
rngtest: FIPS 140-2 failures: 1
rngtest: FIPS 140-2(2001-10-10) Monobit: 1
rngtest: FIPS 140-2(2001-10-10) Poker: 0
rngtest: FIPS 140-2(2001-10-10) Runs: 0
rngtest: FIPS 140-2(2001-10-10) Long run: 0
rngtest: FIPS 140-2(2001-10-10) Continuous run: 0
rngtest: input channel speed: (min=301.394; avg=417.091; max=693.187)Kibits/s
rngtest: FIPS tests speed: (min=64.656; avg=91.010; max=123.055)Mibits/s
rngtest: Program run time: 47037492 microseconds
```

It is normal for any random number generator to fail in a small number of tests in 1000 passes, however if the number of failures is too great (like 10), probably there is something wrong.

After that, you can [start](/index.php/Start "Start")/[enable](/index.php/Enable "Enable") the `rngd.service`.