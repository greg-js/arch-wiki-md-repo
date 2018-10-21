This page deals with setting up Arch Linux on the Dell Vostro 1310 laptop. Nvidia graphics work excellently with the Nvidia 8400GS. There have been some problems with the Ethernet NIC, but it is possible for it to work correctly.

## Contents

*   [1 Hardware](#Hardware)
    *   [1.1 Audio](#Audio)
        *   [1.1.1 OSS](#OSS)
    *   [1.2 Video](#Video)
    *   [1.3 Network](#Network)
    *   [1.4 Webcam](#Webcam)
*   [2 Power Management](#Power_Management)
    *   [2.1 CPU](#CPU)
    *   [2.2 Hibernate/Suspend](#Hibernate.2FSuspend)

## Hardware

### Audio

#### OSS

After comparing both ALSA & OSS on the Vostro 1310 I have come to the conclusion that OSS indeed sounds clearer with more range. However I cannot recommend the use of OSS on the 1310 due to a consistent crackling noise that can be heard in the background whenever any audio is played. A complete reinstall and several restarts of OSS has been tried to correct the problem but has not helped the situation at all. Instead I recommend installing [ALSA](/index.php/ALSA "ALSA") which has given me zero problems.

### Video

See [Xorg](/index.php/Xorg "Xorg") and [NVIDIA](/index.php/NVIDIA "NVIDIA").

### Network

See [Network configuration](/index.php/Network_configuration "Network configuration") and [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration").

### Webcam

The webcam is detected by lsusb as the **0c45:63e0 Microdia Sonix Integrated Webcam**. To get the webcam to properly function follow the steps listed below.

*   Make sure the **uvcvideo** module is loaded by performing the following command: "lsmod | grep uvcvideo". Your output should be something like

```
# uvcvideo               68316  0
# videodev               42080  1 uvcvideo
# v4l1_compat            18228  2 uvcvideo,videodev
# usbcore               179024  5 uvcvideo,usbhid,uhci_hcd,ehci_hcd

```

*   Once you have confirmed that the '**uvcvideo'** module is loaded, add your user to the '**video'** group.

```
# gpasswd -a UserNameGoesHere video

```

*   Log your user out and back in to ensure that your user is apart of the the **video** group.
*   Now you should be able to install your Webcam application such as cheese and you should find that your camera works perfectly. See [Webcam setup](/index.php/Webcam_setup "Webcam setup") for more details on configuring your webcam.

## Power Management

### CPU

For the Intel Core 2 Duo (and all laptop cpu's) you must follow the instructions to setup [CPU frequency scaling](/index.php/CPU_frequency_scaling "CPU frequency scaling").

### Hibernate/Suspend

Hibernate/Suspend works out of the box with pm-utils however integration with HAL does not. In order for you to enable power-related settings like "Suspend on closing of Laptop Lid" in Gnome you will need to

*   Copy `/usr/share/hal/fdi/policy/10osvendor/10-power-mgmt-policy.fdi` to `/etc/hal/fdi/policy/`.
*   Add your user to the `power` [user group](/index.php/User_group "User group").
*   Restart the HAL service or your machine for the change take affect.