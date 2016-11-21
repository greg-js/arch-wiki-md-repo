"Zswap is a Linux kernel feature providing a compressed write-back cache for swapped pages. Instead of moving memory pages to a swap device when they are to be swapped out, zswap performs their compression and then stores them into a memory pool dynamically allocated inside system's RAM." - Wikipedia

zswap is a compressed RAM cache for swap devices. Pages which would otherwise be swapped out to disk will instead be compressed and maintained in RAM until RAM is exhausted, after which the least recently used (LRU) pages will be sent to disk. This is [in contrast to zram](/index.php/Improving_performance#Zram_or_zswap "Improving performance"), which is a swap device in RAM and does not require a backing swap device. The long and the short of it is that you need to set up a [Swap](/index.php/Swap "Swap") device in order to use zswap.

## Contents

*   [1 Enabling zswap](#Enabling_zswap)
*   [2 Customizing zswap](#Customizing_zswap)
    *   [2.1 Customize the maximum allowed size](#Customize_the_maximum_allowed_size)
    *   [2.2 Changing the compression algorithm](#Changing_the_compression_algorithm)
        *   [2.2.1 Enable LZ4 compression (faster than lzo and deflate, less compression)](#Enable_LZ4_compression_.28faster_than_lzo_and_deflate.2C_less_compression.29)
*   [3 See also](#See_also)

## Enabling zswap

To enable zswap at runtime, execute the following command:

```
# echo 1 > /sys/module/zswap/parameters/enabled

```

To enable zswap permanently, add this to your kernel boot parameters [Kernel parameters#Configuration](/index.php/Kernel_parameters#Configuration "Kernel parameters"):

```
zswap.enabled=1

```

**Tip:** You can use the [systemd-swap](https://www.archlinux.org/packages/?name=systemd-swap) package to enable and [configure](#Customizing_zswap) zswap.

## Customizing zswap

By design, zswap has relatively few customizable parameters.

### Customize the maximum allowed size

zswap does not use a preallocated pool of memory to hold compressed and swapped data. If you want to put a maximum bound on the percentage of memory that zswap can use, add this to your kernel boot parameters:

```
  zswap.max_pool_percent=25

```

This can also be set in `sysfs`.

### Changing the compression algorithm

zswaps compression algorithm can also be set as a kernel boot parameter:

```
  zswap.compressor=lzo #deflate #lz4

```

it can also be set at runtime by writing it to /sys/module/zswap/parameters/compressor, e.g:

```
  echo lz4 > /sys/module/zswap/parameters/compressor

```

#### Enable LZ4 compression (faster than lzo and deflate, less compression)

1.  Add `lz4 lz4_compress` to the [Mkinitcpio#MODULES](/index.php/Mkinitcpio#MODULES "Mkinitcpio") array.
2.  Rerun `mkinitcpio`.
3.  Add `zswap.compressor=lz4` to your kernel parameters.
4.  Reboot
5.  Check dmesg :

```
   $ dmesg | grep zswap:
   [    0.918052] zswap: loaded using pool lz4/zbud

```

## See also

*   [Zswap documentation](https://www.kernel.org/doc/Documentation/vm/zswap.txt).
*   [zswap: How to determine whether it is compressing swap pages?](https://lkml.org/lkml/2013/7/17/147).
*   [IBM Developer Works Article (with benchmarks)](https://www.ibm.com/developerworks/community/blogs/fe313521-2e95-46f2-817d-44a4f27eba32/entry/new_linux_zswap_compression_functionality7?lang=en).
*   [Ask Ubuntu: zram vs. zswap vs. zcache](http://askubuntu.com/questions/471912/zram-vs-zswap-vs-zcache-ultimate-guide-when-to-use-which-one).
*   [Archlinux forum thread](https://bbs.archlinux.org/viewtopic.php?id=169585).