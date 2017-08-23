This page should help you setting up ArchLinux on a [MacBook Pro 10,1 with Retina display](https://en.wikipedia.org/wiki/MacBook_Pro#Third_generation_.28Retina.29 "wikipedia:MacBook Pro"). Most of the steps are the same or very similar to the regular ArchLinux installation. However, because this is very new hardware, the setup requires a few different steps. The general installation guidelines are descibed in [Mac](/index.php/Mac "Mac").

**Note:** To have all hardware supported, you should run this Notebook with Kernel 3.7 or newer.

## Contents

*   [1 Preparing for the Installation](#Preparing_for_the_Installation)
    *   [1.1 Preparing the Hard drive](#Preparing_the_Hard_drive)
    *   [1.2 Using the Thunderbolt to Ethernet adapter](#Using_the_Thunderbolt_to_Ethernet_adapter)
    *   [1.3 Using a USB-to-Ethernet adapter](#Using_a_USB-to-Ethernet_adapter)
    *   [1.4 Getting wireless firmware](#Getting_wireless_firmware)
    *   [1.5 USB Tethering](#USB_Tethering)
*   [2 Installation](#Installation)
    *   [2.1 Booting the live image](#Booting_the_live_image)
    *   [2.2 Connecting Wi-Fi](#Connecting_Wi-Fi)
    *   [2.3 The installation](#The_installation)
    *   [2.4 Bootloader](#Bootloader)
        *   [2.4.1 Direct EFI booting](#Direct_EFI_booting)
        *   [2.4.2 GRUB](#GRUB)
*   [3 Post installation](#Post_installation)
    *   [3.1 Wi-Fi](#Wi-Fi)
    *   [3.2 Graphics](#Graphics)
        *   [3.2.1 General Notes](#General_Notes)
        *   [3.2.2 Nouveau backlight](#Nouveau_backlight)
        *   [3.2.3 NVIDIA backlight](#NVIDIA_backlight)
        *   [3.2.4 Switching to/from GPUs with gpu-switch](#Switching_to.2Ffrom_GPUs_with_gpu-switch)
            *   [3.2.4.1 Switch to Intel integrated GPU and turn off discrete Nvidia GPU](#Switch_to_Intel_integrated_GPU_and_turn_off_discrete_Nvidia_GPU)
            *   [3.2.4.2 Keeping the discrete GPU off at boot](#Keeping_the_discrete_GPU_off_at_boot)
        *   [3.2.5 Graphic artifacting under b43-firmware](#Graphic_artifacting_under_b43-firmware)
    *   [3.3 Sound](#Sound)
    *   [3.4 Touchpad](#Touchpad)
    *   [3.5 Memory Card (SDHCI/SDX) Reader](#Memory_Card_.28SDHCI.2FSDX.29_Reader)
*   [4 What does not work (early August 2013, 3.10.3-1)](#What_does_not_work_.28early_August_2013.2C_3.10.3-1.29)
    *   [4.1 Graphics](#Graphics_2)
*   [5 Discussions](#Discussions)
*   [6 See also](#See_also)

## Preparing for the Installation

### Preparing the Hard drive

Assuming you want to dual boot with OS X, you have to shrink its partition with the Disk Utility. You can either create your Linux partition directly here, or do that later in Linux during the installation (using `parted` and `mkfs`).

### Using the Thunderbolt to Ethernet adapter

As of late 2014, thunderbolt hotplugging has been included in the mainline Linux kernel. Ethernet cables can now be used as usual through the thunderbolt adapter. [[1]](https://plus.google.com/+gregkroahhartman/posts/bzx6EJnwMMf)

### Using a USB-to-Ethernet adapter

No special configuration is necessary to get this to work.

### Getting wireless firmware

In order for the Wi-Fi chipset to work, you need to get the firmware for it. You can just copy it from another b43-enabled Arch, extract it from Broadcom's driver using [b43-fwcutter](https://www.archlinux.org/packages/?name=b43-fwcutter), or get the firmware through the [b43-firmware](https://aur.archlinux.org/packages/b43-firmware/) package available in the [AUR](/index.php/AUR "AUR"). In the end, you should have a folder named `b43` with a lot of `.fw` files in it.

### USB Tethering

If you have a smartphone, you can also try tethering your device to get connected to the internet. This should work out of the box.

## Installation

### Booting the live image

Download the latest ISO from the download page and prepare a live USB as outlined in [USB flash installation media](/index.php/USB_flash_installation_media "USB flash installation media").

Shut down the Macbook. Plug in the USB drive. Hold the option key, then press the power button. After a few seconds, you should see Apple's boot loader display the choice of either starting up the built-in drive with OS X or the USB drive you plugged in.

Select the live USB with the arrow keys, and press Enter to boot into the live Arch Linux environment.

**Note:** You should not need to pass in any kernel parameters to boot successfully into the live environment.

### Connecting Wi-Fi

**Note:** You can skip this if you use the Thunderbolt or USB-to-Ethernet adapter for the installation.

After it has finished booting, enter a command line. Copy the entire folder with the firmware for your wireless card to `/usr/lib/firmware/`.

Now you should be able to use wifi-menu to connect to your Wi-Fi network.

### The installation

**Note:** Refer to the [Mac](/index.php/Mac "Mac") page if you do not want to have a separate partition for GRUB but rather prefer to use [rEFInd](http://www.rodsbooks.com/refind/) (or [rEFIt](/index.php/Mac#rEFIt "Mac")).

Run the installation wizard. When asked to partition your hard drive, create a small HFS partition. This is where you put the standalone GRUB package after the installation. The rest of the installation is pretty much the same as usual. When choosing the bootloader, select GRUB, and install it. Do not worry about any errors; we will create the bootable EFI image on our own afterwards.

After the installation has completed, directly copy the Wi-Fi firmware to the installed system to `/tmp/install/usr/lib/firmware/`.

Alternatively, install [broadcom-wl-dkms](https://www.archlinux.org/packages/?name=broadcom-wl-dkms) from the [AUR](/index.php/AUR "AUR") to improve Wi-Fi.

### Bootloader

#### Direct EFI booting

See [UEFI Bootloaders](/index.php/UEFI_Bootloaders "UEFI Bootloaders").

As of August 2013, refind can autodetect the Arch kernel, removing the need for copying the kernel into the EFI partition. Simply install refind and enable the "scan_all_linux_kernels" and "also_scan_dirs" options in refind.conf (see link above for instructions.)

#### GRUB

Another solution is to install [GRUB](/index.php/GRUB "GRUB"). Edit `/tmp/install/boot/grub/grub.cfg` and edit the boot entry to load Linux mainline instead of the normal one. Also append `noapic` to the kernel line again.

Now cd into `/tmp/install/` and create the GRUB image by calling:

```
grub-mkstandalone -o grub-standalone-x86_64.efi -d usr/lib/grub/x86_64-efi -O x86_64-efi -C xz boot/grub/grub.cfg

```

This will create file called `grub-standalone-x86_64.efi` which contains GRUB and the config file. It is important to `cd` into the right directory to make it pick up the config file and put it into the right place within the image. Copy this file to the HFS partition you have created earlier. Downside of this method is that you need to repeat this step whenever you want to change the GRUB config.

Reboot the machine and boot into OS X. The HFS partition should be mounted and the GRUB standalone image in there. Follow the steps on this page to create the files needed to make the Apple boot loader pick up GRUB: [http://mjg59.dreamwidth.org/7468.html](http://mjg59.dreamwidth.org/7468.html). After creating the files, use `bless` on the GRUB image on the partition. If you want to boot automatically to Arch, append `--setBoot`.

After another reboot, you should be able to select your installed Arch Linux by keeping the alt button pressed while booting in case you have not used `--setBoot` while blessing.

## Post installation

### Wi-Fi

The Macbook Pro 10,x comes with the Broadcom BCM4331 Wireless Chipset.

There are two major options to get this chipset working in Arch Linux:

The [b43-firmware](https://aur.archlinux.org/packages/b43-firmware/) package contains the open-source, reverse-engineered firmware for the chipset.

The [broadcom-wl](https://aur.archlinux.org/packages/broadcom-wl/) and [broadcom-wl-dkms](https://www.archlinux.org/packages/?name=broadcom-wl-dkms) packages ship with the propriety, restricted-license drivers for the chipset.

See [Broadcom wireless](/index.php/Broadcom_wireless "Broadcom wireless") for more information.

### Graphics

**Note:** In order to plug in an external display, you will need to have the NVIDIA card powered on as the HDMI and thunderbolt outputs are hardwired to use the NVIDIA card.

#### General Notes

The Laptop comes with an nVidia and an Intel chip. The Nouveau [xf86-video-nouveau](https://www.archlinux.org/packages/?name=xf86-video-nouveau), the intel [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) (from 3.6-rc5) and proprietary nvidia (from 302.17) drivers work. You can install the nvidia driver through [nvidia](https://www.archlinux.org/packages/?name=nvidia) or the AUR package [nvidia-beta-all](https://aur.archlinux.org/packages/nvidia-beta-all/).

**Note:** As of September, 2013 the current nvidia driver (325.15-5) does not work with the current 3.10 series kernels; X will die with an error about "Failed to allocate EVO core DMA push buffer" and leave you with a black screen (but able to SSH in to the machine). Your best current bet is to use a 3.9-series kernel and the older 319.32-series nvidia driver.

Since this device comes with a Retina (HiDPI) display, things may be really small with native resolution for some desktop environments. There are different ways to work around this "issue":

1.  Increase the DPI value to get larger fonts (other things like icons may not look great that way)
    *   KDM is a great choice because the stock UI elements are vectors (not rasters which look terrible on Retina and do not scale infinitely). In addition the [KWin compositor](/index.php/Wayland "Wayland") does a remarkable job on the Retina display.
2.  Lower the screen resolution to 1680x1050 (works fine at least with nouveau drivers), but things look a little bit blurry, of course
3.  Use xrandr scale option with nvidia driver to scale the resolution down to what you want. Take a look at: [http://linuxmacbookproretina.blogspot.no/](http://linuxmacbookproretina.blogspot.no/)
4.  See [HiDPI](/index.php/HiDPI "HiDPI") for more tweaks.

#### Nouveau backlight

If you are using the open-source Nouveau drivers and the active GPU is the Nvidia card, backlight levels can be adjusted by echoing a value to a file (as root):

```
echo 500 > /sys/class/backlight/gmux_backlight/brightness

```

To bring the backlight to its maximum level:

```
echo $(cat /sys/class/backlight/gmux_backlight/max_brightness) > /sys/class/backlight/gmux_backlight/brightness

```

#### NVIDIA backlight

If you are using the propriety nvidia drivers, note that the backlight adjustment will not work out of the box.

To enable backlight control (run as root):

```
setpci -v -H1 -s 00:01.00 BRIDGE_CONTROL=0

```

#### Switching to/from GPUs with gpu-switch

You can switch the display output to and from the discrete or integrated intel GPU from *within* Arch Linux with [gpu-switch](https://aur.archlinux.org/packages/gpu-switch/) if you are using the open-source `xf86-video-nouveau` and `xf86-video-intel` drivers.

**Installation**

You can install [gpu-switch](https://aur.archlinux.org/packages/gpu-switch/) from the AUR.

Then, just run the script as root.

**Usage**

The command switches are `-i`, to switch to the integrated card, and `-d` for switching to the discrete GPU. In order to have the changes take effect, you will need to reboot.

##### Switch to Intel integrated GPU and turn off discrete Nvidia GPU

To switch to intel card and poweroff the discrete GPU:

```
cd /path/to/gpu-switch
./gpu-switch -i

```

Then reboot.

Poweroff the discrete GPU using `vgaswitcheroo` as root:

```
echo OFF > /sys/kernel/debug/vgaswitcheroo/switch

```

This will take a second or to complete.

Then, check whether the discrete GPU is still on:

```
cat /sys/kernel/debug/vgaswitcheroo/switch

```

The output should look like this:

```
0:IGD:+:Pwr:0000:00:02.0
1:DIS: :Off:0000:01:00.0
2:DIS-Audio: :Off:0000:01:00.1

```

This is useful if you have opted to have an Arch Linux-only installation and cannot access the OS X-only tool iGPU.

##### Keeping the discrete GPU off at boot

If you want to keep the discrete GPU off at boot, see [systemd-vgaswitcheroo-units](https://aur.archlinux.org/packages/systemd-vgaswitcheroo-units/).

#### Graphic artifacting under b43-firmware

While on integrated graphics with the b43-firmware package, you might encounter moderate to severe graphic artifacting that appears to be correlated to wireless network traffic. (disconnected->no artifacting, connected->periodic artifacting, large transfer->severe artifacting/unusuable) This can be resolved by removing/blacklisting [b43-firmware](https://aur.archlinux.org/packages/b43-firmware/) and using either [broadcom-wl](https://aur.archlinux.org/packages/broadcom-wl/) or [broadcom-wl-dkms](https://www.archlinux.org/packages/?name=broadcom-wl-dkms).

### Sound

On the MacBookPro10,2 you may need to use the 'snd_hda_intel' driver with the model option 'mbp101'. This model option goes in the modprobe configuration and is undocumented in the list of models available online, but it work admirably. (Until you do this, it will look it is working because you will be able to get sound out through HDMI, but /not/ the built-in speakers.)

**Note:** **As of September 2013** this no longer appears to be required; this should work automatically.

### Touchpad

While [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics) will work, the integrated button of the touchpad may cause issues. Using the [xf86-input-mtrack-git](https://aur.archlinux.org/packages/xf86-input-mtrack-git/) driver, with a tweaked configuration should lead to a better end result:

The following config uses a single touch for left, two for middle, three for right:

```
Section "InputClass"
    MatchIsTouchpad "on"
    Identifier      "Touchpads"
    Driver          "mtrack"
    Option          "Sensitivity" "0.65"
    Option          "IgnoreThumb" "true"
    Option          "IgnorePalm" "true"
    Option          "TapButton1" "1"  
    Option          "TapButton2" "3"
    Option          "TapButton3" "2"
    Option          "ClickFinger1" "1"
    Option          "ClickFinger2" "3"
    Option          "ClickFinger3" "2"
    Option          "BottomEdge" "25"
EndSection

```

To use natural scrolling, also add the following inside this section:

```
    Option          "ScrollDownButton"  "4"
    Option          "ScrollUpButton"    "5"
    Option          "ScrollLeftButton"  "7"
    Option          "ScrollRightButton" "6"

```

For more configurations, check the document of [xf86-input-mtrack-git](https://aur.archlinux.org/packages/xf86-input-mtrack-git/).

To disable the trackpad when typing, install the [dispad-git](https://aur.archlinux.org/packages/dispad-git/) utility.

### Memory Card (SDHCI/SDX) Reader

There is currently a bug in the kernel (4.7.x) where the internal SD card reader times out.

As a workaround you will need to reload the sdhci kernel modules, as per: [https://bugzilla.kernel.org/show_bug.cgi?id=73241#c55](https://bugzilla.kernel.org/show_bug.cgi?id=73241#c55)

```
 sudo rmmod sdhci-pci sdhci
 sudo modprobe sdhci debug_quirks2=4
 sudo modprobe sdhci-pci

```

## What does not work (early August 2013, 3.10.3-1)

### Graphics

*   Using vgaswitcheroo to switch between iGPU / dGPU on the 15" version will result in a black screen. The system is still running and can be rebooted safely.
    *   The dGPU/nouveau is active on boot. As of 3.10.3-1, the only known way to switch to the iGPU/intel is to force this through gfxCardStatus v2.2.1 on MacOS (later versions of gfxCardStatus do *not* work.) This setting will survive reboots. To revert it, you must reboot into MacOS *twice* and/or reset the SMC (shutdown and press shift+control+alt+power at the same time. Press power again to boot.)
    *   Another way to force iGPU/intel is to add following commands into one of the `menuentry` in `grub.cfg`,
        ```
        outb 0x7c2 1
        outb 0x7d4 0x28
        outb 0x7c2 2
        outb 0x7d4 0x10
        outb 0x7c2 2
        outb 0x7d4 0x40

        # Power down dGPU (will not work)
        #outb 0x7c2 1
        #outb 0x7d4 0x50
        #outb 0x7c2 0
        #outb 0x7d4 0x50

        ```

        The screen will remain blank until intel driver is fully loaded. Notice that dGPU will not be powered down (adding code above will prevent the system from booting up). Workaround is to compile and run following program (need `sudo`) after system is fully booted up.

        ```
        #include <stdio.h>
        #include <sys/io.h>

        #define GMUX_PORT_SWITCH_DISPLAY	0x10
        #define GMUX_PORT_SWITCH_DDC		0x28
        #define GMUX_PORT_SWITCH_EXTERNAL	0x40
        #define GMUX_PORT_DISCRETE_POWER	0x50
        #define GMUX_PORT_VALUE			0xc2
        #define GMUX_PORT_READ			0xd0
        #define GMUX_PORT_WRITE			0xd4

        #define GMUX_IOSTART		0x700

        typedef unsigned char u8;

        enum discrete_state {STATE_ON, STATE_OFF};
        enum gpu_id {IGD, DIS};

        static void index_write8(int port, u8 val)
        {
        	outb(val, GMUX_IOSTART + GMUX_PORT_VALUE);
        	outb((port & 0xff), GMUX_IOSTART + GMUX_PORT_WRITE);
        }

        static u8 index_read8(int port)
        {
        	u8 val;
        	outb((port & 0xff), GMUX_IOSTART + GMUX_PORT_READ);
        	val = inb(GMUX_IOSTART + GMUX_PORT_VALUE);

        	return val;
        }

        static void set_discrete_state(enum discrete_state state)
        {
        	if (state == STATE_ON) {	// switch on dGPU
        		index_write8(GMUX_PORT_DISCRETE_POWER, 1);
        		index_write8(GMUX_PORT_DISCRETE_POWER, 3);
        	} else {			// switch off dGPU
        		index_write8(GMUX_PORT_DISCRETE_POWER, 1);
        		index_write8(GMUX_PORT_DISCRETE_POWER, 0);
        	}
        }

        static u8 get_discrete_state()
        {
        	return index_read8(GMUX_PORT_DISCRETE_POWER);
        }

        static void switchto(enum gpu_id id)
        {
        	if (id == IGD) {	// switch to iGPU
        		index_write8(GMUX_PORT_SWITCH_DDC, 1);
        		index_write8(GMUX_PORT_SWITCH_DISPLAY, 2);
        		index_write8(GMUX_PORT_SWITCH_EXTERNAL, 2);
        	} else {		// switch to dGPU
        		index_write8(GMUX_PORT_SWITCH_DDC, 2);
        		index_write8(GMUX_PORT_SWITCH_DISPLAY, 3);
        		index_write8(GMUX_PORT_SWITCH_EXTERNAL, 3);
        	}
        }

        int main(int argc, char **argv)
        {
        	if (iopl(3) < 0) {
        		perror("No IO permissions");
        		return 1;
        	}

        	//switchto(IGD);
        	set_discrete_state(STATE_OFF);
        	//printf("Discrete state: 0x%X
", get_discrete_state());

        	return 0;
        }
        ```

        For further information, please read [apple-gmux](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/drivers/platform/x86/apple-gmux.c) driver inside linux kernel tree.

    *   "rmmod nouveau" will crash if the dGPU is manually powered off via vgaswitcheroo. Once this happens, it will be impossible to shutdown / reboot cleanly. Fresh patches (2 August) will hopefully fix this in the future. (Note: to enter this failure state, you must use gfxCardStatus to force the iGPU, then use vgaswitcheroo explicitly. This is rather uncommon.)
    *   The dGPU / iGPU issues do not affect the 13" rmbp, which only has an intel adapter. Much simpler!
*   Nvidia drivers 319.32 fail to suspend / resume or control the backlight out of the box.
    *   Nouveau and intel work fine.
*   If you are experiencing problems with Nvidia drivers, try using emulated BIOS boot instead of EFI boot.

## Discussions

Here are a couple of interesting threads:

*   [http://ubuntuforums.org/showthread.php?t=2006475](http://ubuntuforums.org/showthread.php?t=2006475)
*   [https://bbs.archlinux.org/viewtopic.php?id=144255&p=1](https://bbs.archlinux.org/viewtopic.php?id=144255&p=1)

## See also

*   A [Puppet](/index.php/Puppet "Puppet") module for installing and configuring Arch (optionally with KDE) on the MBP Retina 10,2, along with initial install instructions, is available at [https://github.com/jantman/puppet-archlinux-macbookretina](https://github.com/jantman/puppet-archlinux-macbookretina). It is updated quite frequently, and run daily on its author's laptop.