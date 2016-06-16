The HASEE K650D-i7-D3 is a powerful laptop, on which Arch-Linux runs fine. For a light-weight window manager, some additional configuration should be setup.

## Contents

*   [1 Touchpad synaptics](#Touchpad_synaptics)
*   [2 Backlight](#Backlight)
*   [3 Video cards](#Video_cards)
*   [4 Audio](#Audio)
*   [5 Webcam](#Webcam)
*   [6 Further suggestions](#Further_suggestions)

## Touchpad synaptics

[xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics) should be installed for a light-weight window manager (but not Gnome or KDE). See [Touchpad_Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics").

## Backlight

Hot keys for backlight might not work after installation of Arch-Linux, so [xorg-xbacklight](https://www.archlinux.org/packages/?name=xorg-xbacklight) is necessary for backlight configuration. See [Backlight#xbacklight](/index.php/Backlight#xbacklight "Backlight").

## Video cards

Install [bumblebee along with Nvidia and Intel drivers](/index.php/Bumblebee "Bumblebee"). [nvidia-dkms](https://www.archlinux.org/packages/?name=nvidia-dkms) is recommended for auto configuration after kernel updates. Acceleration mode of the Intel video card should be changed to "uxa", according to [Intel_graphics#SNA_issues](/index.php/Intel_graphics#SNA_issues "Intel graphics"), so that firefox will not fail to scroll smoothly, and 3D games will run normally.

## Audio

After [regular sound check](/index.php/Advanced_Linux_Sound_Architecture "Advanced Linux Sound Architecture"), additional configuration should be conducted. Run `aplay -l` to find default build-in Audio Analog Stereo. In current machine, you can find the card ID with 1 and the device ID with 0\. Then following configuration file can be created as following:

 `~/.asoundrc` 
```
defaults.pcm.card 1
defaults.pcm.device 0
defaults.ctl.card 1
```

After that, run `alsamixer` to unmute.

## Webcam

The webcam is supported fully by default. [MPlayer](/index.php/Webcam_setup#MPlayer "Webcam setup") or [FFmpeg](/index.php/Webcam_setup#FFmpeg "Webcam setup") can be used for test.

## Further suggestions

*   [Microcode](/index.php/Microcode#Enabling_Intel_microcode_updates "Microcode") should be installed for cpu.
*   UEFI/GPT mode is recommended for a rapid boot process; the default boot logo can be hidden under UEFI.
*   Wireless and bluetooth are supported at the same time. Run [rfkill](https://www.archlinux.org/packages/?name=rfkill) to shutdown bluetooth for power-saving.
*   Micphone should be set to 0, and webcam should be covered for potential risk.