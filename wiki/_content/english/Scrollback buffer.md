Scrollback allows the user to go back and view text which has scrolled off the screen of a text console. This is made possible by a buffer created between the video adapter and the display device called the scrollback buffer. By default, the key combinations of Shift+PageUp and Shift+PageDown scroll the buffer up and down.

## Expanding the buffer

If scrolling up all the way does not show you enough information, you need to expand your scrollback buffer to hold more output. This is done by tweaking the kernel's framebuffer console (fbcon) with the [kernel parameter](/index.php/Kernel_parameter "Kernel parameter") `fbcon=scrollback:Nk` where `N` is the desired buffer size is kilobytes. The default size is 32k.

If this does not work, your framebuffer console may not be properly enabled. Check the [Framebuffer Console documentation](https://www.kernel.org/doc/Documentation/fb/fbcon.txt) for other parameters e.g. for changing the framebuffer driver.