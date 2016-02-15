## important todo's

*   aif filesystem/blockdevice code is a bit complex (mostly due to limitations of bash)

```
 details: [https://bugs.archlinux.org/task/15640](https://bugs.archlinux.org/task/15640)

```

*   support btrfs: include tools, integrate in AIF, add mkinitcpio hook
*   support for filesystem optimized for ssd's? nilfs?
*   support softraid
*   streamline automatic installations: ability to autostart aif on [pxe] boot with a specific profile, understand/convert kickstart files, ..
*   include a tool (preferrably something with simple libui-sh/dialog/ncurses interface) which can help you set up wireless networks, and use it in aif