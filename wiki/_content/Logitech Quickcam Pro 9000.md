# Logitech Quickcam Pro 9000

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**This article or section is a candidate for merging with [Webcam](/index.php/Webcam "Webcam").**

**Notes:** please use the second argument of the template to provide more detailed indications. (Discuss in [Talk:Logitech Quickcam Pro 9000#](https://wiki.archlinux.org/index.php/Talk:Logitech_Quickcam_Pro_9000))

The **Logitech QuickCam Pro 9000** is an expensive and fairly high-quality webcam that is available in several versions. It is of course and UVC device and as such works out-of-the-box in most cases, but if you want to maximize the usefulness of this device on Arch Linux you'll need to do some magic.

## Building the Software

[libwebcam](https://aur.archlinux.org/packages/libwebcam/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/libwebcam)]</sup> is the support library needed for AF control. [guvcview](https://www.archlinux.org/packages/?name=guvcview) is the viewer/capture application.

Both applications are built easily using the AUR/ABS build system. In the case of libwebcam I used the patches and build scripts provided by esteemed member whitelynx.

## Registering Camera Controls

During the installation of libwebcam the following line will be added to your _/etc/udev/rules.d/80-uvcdynctrl.rules_

```
ACTION=="add", SUBSYSTEM=="video4linux", DRIVERS=="uvcvideo", RUN+="/lib/udev/uvcdynctrl"

```

After the installation, disconnect and reconnect your camera to trigger the rules, then start guvcview once as root, just to let it initialize the AF controls. If you are not yet a member of the "video" group, you should add yourself to it and login anew. After this you should be able to use the cameras full feature set, including autofocus, even as a regular user.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Logitech_Quickcam_Pro_9000&oldid=407360](https://wiki.archlinux.org/index.php?title=Logitech_Quickcam_Pro_9000&oldid=407360)"