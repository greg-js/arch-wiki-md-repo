## Wireless

```
02:00.0 Network controller: Intel Corporation PRO/Wireless 4965 AG or AGN Network Connection (rev 61)

```

Driver - Built into kernel, Firmware - iwlwifi-4965-ucode from installation disk under 'Support'. Place 'iwl4965' in your modules array in rc.conf.

## Motioneye Inscreen Camera

*lsusb* will show

```
05ca:1839 Ricoh Co., Ltd 

```

which has support provided by the r5u870 driver (depends on kernel26<2.6.26).

download the latest trunk using *svn*, *make*, and *make install* as per the normal build drill...

```
svn co [http://svn.mediati.org/svn/r5u870/trunk](http://svn.mediati.org/svn/r5u870/trunk) ~/r5u870
cd ~/r5u870
make
make install

```

**Note:** One may forgo the last step in favor of being required to manually load the driver and 'keep it simple' (information on manually loading can be found in the README file that you get from the trunk. **Note:** A package exists in AUR 'r5u870' and 'r5u870-svn' which still work with depends kernel26<2.6.26 and kernel26>2.6.24, feel free to use those too. All that's left now is

```
modprobe r5u870

```

you can test your webcam with *xawtv* like so

```
xawtv /dev/video0

```

*kernel26>2.6.26*: If you have a kernel that falls beyond the depends for 'r5u870' then you can try 'r5u87x' which is a user-space utility that simply loads the camera's firmware into the device. unloading and reloading uvcvideo module will give you your /dev/video* device. There are certain problems with this as any request for a resolution change below 640x480 will report successful by the camera, but actually fails. I will be following developement closely. --[OrionFyre](/index.php/User:OrionFyre "User:OrionFyre") 15:13, 14 November 2008 (EST)

*flashcam note* Flashcam project was a video loopback device that provided a v4l device that worked with flash, this project is now obsolete as flash10 supports v4l2 and as it too is subject to the same breakage that occures to r5u870 with kernel26>2.6.26\. My intention was to continue to use flashcam to take vga video (which works with uvcvideo) and have flashcam provide the proper resolution needed for the various applications--[OrionFyre](/index.php/User:OrionFyre "User:OrionFyre") 15:13, 14 November 2008 (EST)