Related articles

*   [Kernel parameters](/index.php/Kernel_parameters "Kernel parameters")
*   [Mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio")

[Zswap](https://en.wikipedia.org/wiki/zswap "wikipedia:zswap") is a kernel feature that provides a compressed RAM cache for swap pages. Pages which would otherwise be swapped out to disk are instead compressed and stored into a memory pool in RAM. Once the pool is full or the RAM is exhausted, the least recently used *(LRU)* page is decompressed and written to disk, as if it had not been intercepted. After the page has been decompressed into the swap cache, the compressed version in the pool can be freed.

The [difference compared to zram](/index.php/Improving_performance#Zram_or_zswap "Improving performance") is that zswap works in conjunction with a [swap](/index.php/Swap "Swap") device while zram is a swap device in RAM that does not require a backing swap device.

## Contents

*   [1 Enabling zswap](#Enabling_zswap)
*   [2 Customizing zswap](#Customizing_zswap)
    *   [2.1 Current parameters](#Current_parameters)
    *   [2.2 Set parameters](#Set_parameters)
        *   [2.2.1 Using sysfs](#Using_sysfs)
        *   [2.2.2 Using kernel boot parameters](#Using_kernel_boot_parameters)
        *   [2.2.3 Using systemd-swap](#Using_systemd-swap)
    *   [2.3 Maximum pool size](#Maximum_pool_size)
    *   [2.4 Compressed memory pool allocator](#Compressed_memory_pool_allocator)
    *   [2.5 Compression algorithm](#Compression_algorithm)
*   [3 See also](#See_also)

## Enabling zswap

To enable zswap at runtime, execute the following command:

```
# echo 1 > /sys/module/zswap/parameters/enabled

```

To enable zswap permanently:

*   Either add to your [kernel parameters](/index.php/Kernel_parameters#Configuration "Kernel parameters") `zswap.enabled=1`

*   Alternatively, you can use [systemd-swap](https://www.archlinux.org/packages/?name=systemd-swap) which is a script to manage swap spaces, in this case the line `zswap_enabled=1` must be present in `/etc/systemd/swap.conf` and you must [start/enable](/index.php/Start/enable "Start/enable") `systemd-swap.service`.

## Customizing zswap

### Current parameters

Zswap has 4 customizable parameters. The live settings can be displayed using:

 `$ grep -R . /sys/module/zswap/parameters` 
```
/sys/module/zswap/parameters/enabled:Y
/sys/module/zswap/parameters/max_pool_percent:25
/sys/module/zswap/parameters/zpool:z3fold
/sys/module/zswap/parameters/compressor:lz4

```

The boot time load message showing the initial configuration can be retrieved with:

 `$ dmesg | grep zswap:` 
```
[    0.317569] zswap: loaded using pool lz4/z3fold

```

### Set parameters

#### Using sysfs

Each setting can be changed at runtime via the [sysfs](https://en.wikipedia.org/wiki/sysfs "wikipedia:sysfs") interface. For example using the following command to amend the first parameter of the list, `compressor`:

```
# echo lz4 > /sys/module/zswap/parameters/compressor

```

#### Using kernel boot parameters

To set the parameter permanently, the corresponding option, for example `zswap.compressor=lz4`, must be added to the kernel boot parameter. Therefore to set permanently all the above settings, the following kernel parameters must be added: `zswap.enabled=1 zswap.compressor=lz4 zswap.max_pool_percent=20 zswap.zpool=z3fold`.

#### Using systemd-swap

For the ones using the *systemd-swap* script, it modifies the *sysfs* parameters at a later stage of the boot process based on its [configuration](https://github.com/Nefelim4ag/systemd-swap/blob/master/swap.conf) stored in `/etc/systemd/swap.conf`.

### Maximum pool size

The memory pool is not preallocated, it is allowed to grow up to a certain limit in percentage of the total memory available, by default up to 20% of the total RAM. Once this threshold is reached, pages are evicted from the pool into the swap device. The maximum compressed pool size is controlled with the parameter `max_pool_percent`.

### Compressed memory pool allocator

The *zpool* parameter controls the management of the compressed memory pool, it is by default set to `zbud`. With the *zbud* data allocator, 2 compressed objects are stored into 1 page which limits the compression ratio to 2 or less. The superior [z3fold](https://www.kernel.org/doc/Documentation/vm/z3fold.txt) allocator allows up to 3 compressed objects by page. The compression ratio with *z3fold* typically averages 2.7 while it is 1.7 for *zbud*.

A *zpool* of type *zbud* is created by default, use the kernel parameter `zswap.zpool=z3fold` to select the *z3fold* method instead. The data allocator can also be changed at a later stage via the *sysfs* interface.

### Compression algorithm

For page compression, zswap uses compressor modules provided by the kernel's cryptographic API. It uses by default the *lzo* compression algorithm but this can be changed with `zswap.compressor`. *Lz4* can be used instead of *lzo* for faster compression and decompression for a slightly lower compression ratio. Other possible choices are *lz4hc* or *deflate*.

There is no issue setting the compression to *lz4* at runtime using *sysfs* or via *systemd-swap* but zswap starts in this case with *lzo* and switches at a later stage to *lz4*. To use zswap with *lz4* straight away, this must be defined in the kernel boot parameter and the *lz4* module must be loaded early by the kernel. This can be achieved by following these steps:

1.  Add `lz4 lz4_compress` to the [mkinitcpio#MODULES](/index.php/Mkinitcpio#MODULES "Mkinitcpio") array.
2.  Replace the ramdisk environment with a newly generated one: `# mkinitcpio -g /boot/*initramfs*.img` 
3.  Add `zswap.compressor=lz4` to your [kernel parameters](/index.php/Kernel_parameters "Kernel parameters").

On next reboot, see [#Current parameters](#Current_parameters) to check if zswap now uses *lz4* as compressor.

## See also

*   [zswap documentation](https://www.kernel.org/doc/Documentation/vm/zswap.txt).
*   [zswap: How to determine whether it is compressing swap pages?](https://lkml.org/lkml/2013/7/17/147).
*   [IBM Developer Works Article (with benchmarks)](https://www.ibm.com/developerworks/community/blogs/fe313521-2e95-46f2-817d-44a4f27eba32/entry/new_linux_zswap_compression_functionality7?lang=en).
*   [Ask Ubuntu: zram vs. zswap vs. zcache](http://askubuntu.com/questions/471912/zram-vs-zswap-vs-zcache-ultimate-guide-when-to-use-which-one).
*   [Archlinux forum thread](https://bbs.archlinux.org/viewtopic.php?id=169585).
*   [LWN.net technical article by the main developer of zswap](https://lwn.net/Articles/537422/).