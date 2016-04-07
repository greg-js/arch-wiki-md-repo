Clover is a UEFI bootloader developed for booting Hackintosh and multiboot with other operating systems. It can be used to boot Linux kernels with [EFISTUB](/index.php/EFISTUB "EFISTUB") support. The advantage of Clover to other bootloaders is it supports native resolution GUI on wide screens people commonly use today.

## Installation

Download Clover Bootable ISO from [here](http://sourceforge.net/projects/cloverefiboot/files/Bootable_ISO/)

extract archive and find the `Clover-*-X64.iso` file, mount it.

copy everything in `EFI` folder to your UEFI partition.

## Configuration

Configuration is done through an xml file `config.plist` under path `EFI/CLOVER` from the UEFI partition. For details please reference [their wiki](http://clover-wiki.zetam.org/Home), for the Linux kernel EFISTUB boot entry and native resolution GUI, add following code to the relevent place:

```
<key>GUI</key>
<dict>
   <key>Custom</key>
   <dict>
      <key>Entries</key>
      <array>
         <dict>
            <key>AddArguments</key>
            <string>root=UUID=d4f1e3b7-b466-4c1b-991c-90fa99cafbc6 rw add_efi_memmap initrd=/initramfs-linux.img</string>
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
   <key>ScreenResolution</key>
   <string>2560x1080</string>
   <key>Theme</key>
   <string>bootcamp</string>
</dict>

```

## See also

*   [http://sourceforge.net/projects/cloverefiboot/](http://sourceforge.net/projects/cloverefiboot/)