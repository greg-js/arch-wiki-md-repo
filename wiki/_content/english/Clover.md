Related articles

*   [Arch boot process](/index.php/Arch_boot_process "Arch boot process")
*   [Unified Extensible Firmware Interface](/index.php/Unified_Extensible_Firmware_Interface "Unified Extensible Firmware Interface")
*   [EFISTUB](/index.php/EFISTUB "EFISTUB")

[Clover EFI](https://sourceforge.net/projects/cloverefiboot/) is a boot loader developed to boot OS X ([Hackintoshes](https://en.wikipedia.org/wiki/en:Hackintosh "wikipedia:en:Hackintosh")), Windows and Linux in legacy or UEFI mode.

The main advantages of Clover are:

*   Emulate UEFI on legacy BIOS systems
*   Boot Linux kernels with [EFISTUB](/index.php/EFISTUB "EFISTUB") support
*   Supports native resolution GUI on wide screens people commonly use today
*   Easy of use
*   Easily customizable

## Installation

Download Clover Bootable ISO from [here](https://sourceforge.net/projects/cloverefiboot/files/Bootable_ISO/).

Extract archive and find the `Clover-*-X64.iso` file, mount it.

Copy everything in `EFI` folder to your [EFI system partition](/index.php/EFI_system_partition "EFI system partition").

## Configuration

Configuration is done through an xml file `config.plist` under path `EFI/CLOVER` from the UEFI partition.

A tool is now available to easily edit your `config.plist` in any OS: [Cloud Clover Editor (CCE)](http://cloudclovereditor.altervista.org/cce/index.php)

For details please reference [their wiki](https://sourceforge.net/p/cloverefiboot/wiki/Home/), for the Linux kernel EFISTUB boot entry and native resolution GUI, add following code to the relevant place.

`/initramfs-linux.img` and `vmlinuz-linux` are relative to the root of the UEFI partition. In this example, the initramfs and kernel files have to be at the root of the EFI partition, at the same level as the `EFI` directory.

```
<key>GUI</key>
<dict>
   <key>Custom</key>
   <dict>
      <key>Entries</key>
      <array>
         <dict>
            <key>Arguments</key>
            <string>initrd=/initramfs-linux.img root=UUID=d4f1e3b7-b466-4c1b-991c-90fa99cafbc6 rw add_efi_memmap</string>
            <key>Disabled</key>
            <false/>
            <key>FullTitle</key>
            <string>Arch Linux</string>
            <key>Hidden</key>
            <false/>
            <key>Ignore</key>
            <false/>
            <key>Path</key>
            <string>vmlinuz-linux</string>
            <key>Type</key>
            <string>Linux</string>
            <key>Volume</key>
            <string>EFI</string>
            <key>VolumeType</key>
            <string>Internal</string>
         </dict>
      </array>
   </dict>
</dict>

```

## See also

*   [Project homepage](https://sourceforge.net/projects/cloverefiboot/)
*   [Clover Wiki](https://sourceforge.net/p/cloverefiboot/wiki/Home/)