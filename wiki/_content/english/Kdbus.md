kdbus is an alternative in-kernel implementation of [D-Bus](/index.php/D-Bus "D-Bus").

## Installation

[Install](/index.php/Install "Install") the [kdbus](https://aur.archlinux.org/packages/kdbus/) package, then add `kdbus=1` to the [kernel parameters](/index.php/Kernel_parameters "Kernel parameters").

After rebooting, you can verify a working _kdbus_ installation with:

 `$ dmesg | grep kdbus`  `kernel: kdbus: initialized` 

Also check that `/sys/fs/kdbus/` contains the `0-system/` folder, denoting the system bus. Another sign of a working _kdbus_ installation is that, after invoking `busctl`, the `DESCRIPTION` column should not be entirely empty for all services.

## See also

*   [kdbus official homepage](http://www.freedesktop.org/wiki/Software/systemd/kdbus/)
*   [Greg-KH kdbus module repository](https://github.com/gregkh/kdbus)
*   [systemd developer google+ post on kdbus](https://plus.google.com/u/0/+DavidHerrmann/posts/3wNuKCJeGJs)