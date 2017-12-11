Related articles

*   [Kernel parameters](/index.php/Kernel_parameters "Kernel parameters")
*   [Mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio")

"Zswap is a Linux kernel feature providing a compressed write-back cache for swapped pages. Instead of moving memory pages to a swap device when they are to be swapped out, zswap performs their compression and then stores them into a memory pool dynamically allocated inside system's RAM." - Wikipedia

zswap is a compressed RAM cache for swap devices. Pages which would otherwise be swapped out to disk will instead be compressed and maintained in RAM until RAM is exhausted, after which the least recently used (LRU) pages will be sent to disk. This is [in contrast to zram](/index.php/Improving_performance#Zram_or_zswap "Improving performance"), which is a swap device in RAM and does not require a backing swap device. The long and the short of it is that you need to set up a [swap](/index.php/Swap "Swap") device in order to use zswap.

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

*   Either add to your [kernel parameters](/index.php/Kernel_parameters#configuration "Kernel parameters") `zswap.enabled=1`

*   Alternatively, you can use [systemd-swap](https://www.archlinux.org/packages/?name=systemd-swap) which is a script to manage swap spaces, in this case the [configuration](https://github.com/Nefelim4ag/systemd-swap/blob/master/swap.conf) takes place in `/etc/systemd/swap.conf`.

## Customizing zswap

### Current parameters

Zswap has 4 customizable parameters. The live settings can be displayed using:

```
 $ grep . /sys/module/zswap/parameters/*
/sys/module/zswap/parameters/compressor:lz4
/sys/module/zswap/parameters/enabled:Y
/sys/module/zswap/parameters/max_pool_percent:20
/sys/module/zswap/parameters/zpool:z3fold

```

### Set parameters

#### Using sysfs

Each setting can be changed at runtime via the [sysfs](https://en.wikipedia.org/wiki/sysfs "wikipedia:sysfs") interface. For example using the following command to amend the first parameter of the list, `compressor`:

```
  # echo lz4 > /sys/module/zswap/parameters/compressor

```

#### Using kernel boot parameters

To set the parameter permanently, the option, for example `zswap.compressor=lz4`, must be added to the kernel boot parameter. Therefore to set permanently all the parameters above, the following kernel parameters must be added: `zswap.enabled=1 zswap.compressor=lz4 zswap.max_pool_percent=20 zswap.zpool=z3fold`

#### Using systemd-swap

For the ones using the *systemd-swap* script, in this example `zswap_compressor=lz4` must be specified in the `/etc/systemd/swap.conf` file.

### Maximum pool size

The allocated size of compressed memory pool with respect to the total memory available is limited to 20% by default. It can be increased or decreased with the parameter `max_pool_percent`.

### Compressed memory pool allocator

The *zpool* parameter controls the management of the compressed memory pool, it is by default set to `zbud` while `z3fold` is recommended. With the *zbud* data allocator, 2 compressed objects are stored into 1 page which limits the compression ratio to 2 or less. The superior [z3fold](https://www.kernel.org/doc/Documentation/vm/z3fold.txt) allocator allows up to 3 compressed objects by page. The compression ratio with *z3fold* typically averages 2.7 while it is 1.7 for *zbud*.

A *zpool* of type *zbud* is created by default, use the kernel parameter `zswap.zpool=z3fold` to select the *z3fold* method instead. The data allocator can also be changed at a later stage.

### Compression algorithm

Zswap uses by default the lzo compression algorithm but this can be changed with `zswap.compressor` to `lz4` or `deflate`. Lz4 achieves the fastest compression compared to lzo and deflate, it also results in lower compression ratios.

There is no issue setting the compression to lz4 via *systemd-swap* or using *sysfs* but zswap starts in this case with lzo and switches at a later stage of the boot process to lz4\. To use zswap with lz4 straight away, this must be defined in the kernel boot parameter and the lz4 module must be loaded early by the kernel. This can be achieved with the following operations:

1.  Add `lz4 lz4_compress` to the [mkinitcpio#MODULES](/index.php/Mkinitcpio#MODULES "Mkinitcpio") array.
2.  Replace the ramdisk environment with a newly generated one: `# mkinitcpio -g /boot/*initramfs*.img` 
3.  Add `zswap.compressor=lz4` to your kernel parameters.
4.  Reboot
5.  Check if zswap loaded using lz4 with: `$ dmesg | grep zswap` it should look like: `[    0.318052] zswap: loaded using pool lz4/zbud` 

## See also

*   [zswap documentation](https://www.kernel.org/doc/Documentation/vm/zswap.txt).
*   [zswap: How to determine whether it is compressing swap pages?](https://lkml.org/lkml/2013/7/17/147).
*   [IBM Developer Works Article (with benchmarks)](https://www.ibm.com/developerworks/community/blogs/fe313521-2e95-46f2-817d-44a4f27eba32/entry/new_linux_zswap_compression_functionality7?lang=en).
*   [Ask Ubuntu: zram vs. zswap vs. zcache](http://askubuntu.com/questions/471912/zram-vs-zswap-vs-zcache-ultimate-guide-when-to-use-which-one).
*   [Archlinux forum thread](https://bbs.archlinux.org/viewtopic.php?id=169585).