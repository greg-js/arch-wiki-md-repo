# Scrollback buffer

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**This article or section is a candidate for merging with [Boot debugging](/index.php/Boot_debugging "Boot debugging").**

**Notes:** this article should be expanded to cover general framebuffer console tweaks, or should simply be added to boot debugging for those who need more output (Discuss in [Talk:Scrollback buffer#](https://wiki.archlinux.org/index.php/Talk:Scrollback_buffer))

Scrollback allows the user to go back and view text which has scrolled off the screen of a text console. This is made possible by a buffer created between the video adapter and the display device called the scrollback buffer. By default, the key combinations of Shift+PageUp and Shift+PageDown scroll the buffer up and down.

## Expanding the buffer

If scrolling up all the way does not show you enough information, you need to expand your scrollback buffer to hold more output. This is done by tweaking the kernel's framebuffer console (fbcon) with the [kernel parameter](/index.php/Kernel_parameter "Kernel parameter") `fbcon=scrollback:Nk` where `N` is the desired buffer size is kilobytes. The default size is 32k.

If this does not work, your framebuffer console may not be properly enabled. Check the [Framebuffer Console documentation](https://www.kernel.org/doc/Documentation/fb/fbcon.txt) for other parameters e.g. for changing the framebuffer driver.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Scrollback_buffer&oldid=410329](https://wiki.archlinux.org/index.php?title=Scrollback_buffer&oldid=410329)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Terminal emulators](/index.php/Category:Terminal_emulators "Category:Terminal emulators")