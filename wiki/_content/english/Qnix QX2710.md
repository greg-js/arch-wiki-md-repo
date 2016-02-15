This article is a short tutorial on how to get the QX2710 to work well on Linux.

## Fixing X11 With Nvidia

By default, on some graphcis drivers, the QX2710 will enter a debug mode and flip through colors when you start up X. The reason for this is that the driver is having issues reading the EDID from the monitor.

This issue with reading the EDID does not occur on Windows, so I pulled the read EDID from Windows, which you can find [here](https://lambda.sx/marcus/qx2710.edid).

*   Copy the edid file to /etc/X11/edid (create the directory)
*   Remove any nvidia-generated xorg configs in /etc/X11/xorg.conf.d
*   Find the ID of the monitor through the following command

```
$ nvidia-xconfig --query-gpu-info

```

*   Create /etc/X11/xorg.conf.d/60-qnix-edid.conf and add the following to it (remember to change DFP-0 to your monitor ID)

 `/etc/X11/xorg.conf.d/60-qnix-edid.conf` 

```
Section "Device"
     Identifier     "Device0"
     Option         "CustomEDID" "DFP-0:/etc/X11/edid/qx2710.edid"
EndSection
```

*   Save the file then restart X. Your monitor should now be working.