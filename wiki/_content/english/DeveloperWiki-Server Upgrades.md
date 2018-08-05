## Process

**Updating servers**

The following steps should be used to update our managed servers:

*   pacman -Syu
*   manually update the kernel, since it is in IgnorePkg by default
*   sync
*   checkservices
*   reboot