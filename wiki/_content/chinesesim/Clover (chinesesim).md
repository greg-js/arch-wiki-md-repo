**翻译状态：** 本文是英文页面 [Clover](/index.php/Clover "Clover") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-06-25，点击[这里](https://wiki.archlinux.org/index.php?title=Clover&diff=0&oldid=438963)可以查看翻译后英文页面的改动。

Clover 是一个为了在非 Macintosh 计算机上安装 Mac OS X 而开发的 UEFI 引导程序。除了 OS X，Clover 也可以引导其他操作系统。Clover 可以用于引导支持 [EFISTUB](/index.php/EFISTUB "EFISTUB") 的 Linux 内核。相对于其他的引导器来说，Clover 原生支持现今被广泛使用的宽屏显示器所采用的高分辨率界面。

## 安装

从 [Sourceforge](http://sourceforge.net/projects/cloverefiboot/files/Bootable_ISO/) 上下载可引导的 Clover ISO 文件。

解压已下载的压缩文件，然后找到文件名为 `Clover-*-X64.iso` 的镜像文件，将其挂载或解压。将 `EFI` 文件夹里的所有文件复制到你的 EFI 分区中。如果当前有其他的操作系统（例如 Windows）接管了你的 EFI 分区，不要忘记备份 EFI 分区中 `BOOT` 文件夹下的 bootx64.efi 文件。

## 配置

Clover 的配置是通过 `EFI/CLOVER` 目录下的 XML 文件 `config.plist` 记录的。Clover 的强大功能依赖于它的复杂配置，如果你想深入了解有关于 Clover 配置的细节，请访问 [Clover Wiki](http://clover-wiki.zetam.org/Home)。如果你想要添加 Linux 的引导选项，并且开启原生高分辨率的 GUI，请添加以下代码到 `config.plist` 中。其中的一部分内容可能已经在 `config.plist` 中有所涉及，请将已有的内容替换。

与此同时，请将 Linux /boot/ 下的 `/initramfs-linux.img` 和 `vmlinuz-linux` 放到你 EFI 分区的根目录。在以下的示例中，initramfs 和 Linux 内核文件必须放在 EFI 分区的根目录中，即和 `EFI` 文件夹同级的目录下。

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

## 参考阅读

*   [http://sourceforge.net/projects/cloverefiboot/](http://sourceforge.net/projects/cloverefiboot/)