Related articles

*   [Improving performance](/index.php/Improving_performance "Improving performance")

Article on utilizing video memory for system swap.

**Warning:** This will not work with binary drivers.

**Warning:** Unless your graphics driver can be made to use less ram than is detected, Xorg may crash when you try to use the same section of RAM to store textures as swap. Using a video driver that allows you to override videoram should increase stability.

## Contents

*   [1 Potential benefits](#Potential_benefits)
*   [2 Kernel requirements](#Kernel_requirements)
*   [3 Pre-setup](#Pre-setup)
*   [4 Setup](#Setup)
    *   [4.1 Xorg driver config](#Xorg_driver_config)
*   [5 Troubleshooting](#Troubleshooting)
*   [6 See also](#See_also)

## Potential benefits

A graphics card with GDDR SDRAM or DDR SDRAM may be used as swap by using the MTD subsystem of the kernel. Systems with dedicated graphics memory of 256 MB or greater which also have limited amounts of system memory (DDR SDRAM) may benefit the most from this type of setup.

**Note:** Using legacy AGP (Accelerated Graphics Port) card may limit reads to approximately 8 MB per second (but port speed is from 266MB/s to 2133MB/s so may it work fast). AGP bus has a limited amount of bus bandwidth.

## Kernel requirements

MTD is in the mainline kernel since version 2.6.23.

## Pre-setup

When you are running a kernel with MTD modules, you have to load the modules specifying the pci address ranges that correspond to the ram on your video card.

To find the available memory ranges run the following command and look for the VGA compatible controller section (see the example below).

 `$ lspci -vvv` 
```
01:00.0 VGA compatible controller: NVIDIA Corporation GK104 [GeForce GTX 670] (rev a1) (prog-if 00 [VGA controller])
	Subsystem: ASUSTeK Computer Inc. Device 8405
	Control: I/O+ Mem+ BusMaster+ SpecCycle- MemWINV- VGASnoop- ParErr- Stepping- SERR- FastB2B- DisINTx-
	Status: Cap+ 66MHz- UDF- FastB2B- ParErr- DEVSEL=fast >TAbort- <TAbort- <MAbort- >SERR- <PERR- INTx-
	Latency: 0
	Interrupt: pin A routed to IRQ 57
	Region 0: Memory at f5000000 (32-bit, non-prefetchable) [size=16M]
	Region 1: Memory at e8000000 (64-bit, prefetchable) [size=128M]
	Region 3: Memory at f0000000 (64-bit, prefetchable) [size=32M]
	Region 5: I/O ports at e000 [size=128]
	[virtual] Expansion ROM at f6000000 [disabled] [size=512K]
	Capabilities: <access denied>
	Kernel driver in use: nvidia
	Kernel modules: nouveau, nvidia
```

**Note:** Systems with multiple GPUs will likely have multiple entries here.

Of most potential benefit is a region that is prefectable, 64-bit, and the largest in size.

**Note:** The graphics card used above has 2 GB of GDDR5 SDRAM, though as indicated above the full amount is not exposed or listed by the command provided above.

A video card needs some of its memory to function, as such some calculations are needed. The offsets are easy to calculate as powers of 2\. The card should use the beginning of the address range as a framebuffer for textures and such. However, if limited or as indicated in the beginning of this article, if two programs try to write to the same sectors, stability issues are likely to occur.

**Warning:** The following example is dated and may no longer be accurate.

As an example: For a total of 256 MB of graphics memory, the forumla is 2^28 (two to the twenty-eighth power). Approximately 64 MB could be left for graphics memory and as such the start range for the swap usage of graphics memory would be calculated with the formula 2^26\.

Using the numbers above, you can take the difference and determine a reseasonable range for usage as swap memory. leaving 2^24 (32M) for the normal function (less will work fine)

## Setup

Load the modules:

 `# /etc/modules-load.d/vramswap.conf` 
```
slram
mtdblock

```

systemd service:

 `# /usr/lib/systemd/system/vramswap.service` 
```
[Unit]
Description=Swap on Video RAM

[Service]
Type=oneshot
ExecStart=/usr/bin/bash -c "mkswap /dev/mtdblock0 && swapon /dev/mtdblock0 -p 10"
ExecStop=/usr/bin/bash -c "swapoff /dev/mtdblock0"
RemainAfterExit=yes

[Install]
WantedBy=multi-user.target

```

Add the following.

 `# /etc/modprobe.d/modprobe.conf`  ` options slram map=VRAM,0xStartRange,+0xUsedAmount` 

### Xorg driver config

To keep X stable, your video driver needs to be told to use less than the detected videoram.

 `# /etc/X11/xorg.conf.d/vramswap.conf` 
```
Section "Device"
    Driver "radeon" # or whichever other driver you use
    VideoRam 32768
	#other stuff
EndSection
```

The above example specifies that you use 32 MB of graphics memory.

**Note:** Some drivers might take the number for videoram as being in MiB. See relevant manpages.

## Troubleshooting

The following command may help you getting the used swap in the different spaces like disk partitions, flash disks and possibly this example of the swap on video ram

 `swapon -s` 

## See also

*   [MTD website](http://www.linux-mtd.infradead.org)