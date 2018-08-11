## Process

**Updating servers**

The following steps should be used to update our managed servers:

1.  pacman -Syu
2.  manually update the kernel, since it is in IgnorePkg by default
3.  sync
4.  checkservices
5.  reboot