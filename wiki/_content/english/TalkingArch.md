This page describes a bootable CD / USB image customized for blind users. The modified version is mostly equivalent to the official Archiso image, but the system should start speaking as soon as you boot with it. Speech is provided via the sound card, using the eSpeak-ng software synthesizer and the Speakup screenreader. It is also possible to use a braille display, via brltty. You can obtain the image [from this page](https://talkingarch.info/).

Like the Archiso image, this image is compatible with the x86_64 architecture. Also, it is suitable for either a recordable CD or a USB stick. Just download it and write it to the medium of your choice.

A detached GPG signature is provided on the download page.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Credits](#Credits)
*   [2 Installing from the CD](#Installing_from_the_CD)
*   [3 Braille support](#Braille_support)
*   [4 Maintaining your speech-enabled Arch Linux installation](#Maintaining_your_speech-enabled_Arch_Linux_installation)
*   [5 Mastering speech-enabled ISO images](#Mastering_speech-enabled_ISO_images)
*   [6 Further resources](#Further_resources)
*   [7 Disclaimer](#Disclaimer)

### Credits

The build system, which is a respin of the Archiso releng configuration, is maintained by Alexander Epaneshnikov.

Thanks to Kelly Prescott, Kyle and Chris Brannon, the past maintainers, and to the following people for submitting valuable feedback regarding this project: Chuck Hallenbeck, Julien Claassen, Alastair Irving, Tyler Spivey, Keith Hinton, and many others. Thanks also go to Tyler Littlefield, who previously hosted the files.

## Installing from the CD

The following list of steps is a brief guide to installing Arch Linux using this CD. The instructions assume that your root partition will be mounted on `/mnt`.

1.  You can just press `enter` at the boot prompt, or wait for the bootloader to time-out. The boot process will begin at that point. or you can, wait about 10 to 20 seconds after the CD starts spinning, or about 3 to 5 seconds after the system begins to boot from USB, and then press `enter` to boot the image.
2.  You are strongly encouraged to read the Arch Linux documentation, especially the [Installation guide](/index.php/Installation_guide "Installation guide"). Do the installation procedure described in the [Installation guide](/index.php/Installation_guide "Installation guide"), as modified by the instructions below.
3.  You'll need to install the `espeakup` and `alsa-utils` packages. The [Installation guide](/index.php/Installation_guide "Installation guide") mentions that you can install additional packages by appending their names to the pacstrap command. For example, `pacstrap /mnt base espeakup alsa-utils`
4.  If you heard a voice recording informing you that multiple sound cards were detected, and you selected a card by pressing enter at the beep, a /etc/asound.conf file was generated that will configure ALSA to use your selected card as the default. You will need to copy this file by executing `cp /etc/asound.conf /mnt/etc`
5.  While in the arch-chroot, Enable the espeakup systemd service by executing `systemctl enable espeakup.service`
6.  When you boot the system from the hard disk, it should start speaking.

## Braille support

The latest image includes brltty, for those who own braille displays. The brltty package available on the CD was compiled with as few dependencies as possible. It is packaged as brltty-minimal in the Arch User Repository. If you wish to use braille, you will need to supply the brltty parameter at the boot prompt. Alternatively, you can start brltty from the shell, after the system has booted.

The brltty boot-time parameter consists of three comma-separated fields: driver, device, and table. The first is the driver for your display, the second is the name of the device file, and the third is a relative path to a translation table. You can use "auto" to specify that the driver should be automatically detected. I encourage you to read the brltty documentation for a fuller explanation of the program.

For example, suppose that you have a device connected to /dev/ttyS0, the first serial port. You wish to use the US English text table, and the driver should be automatically detected. Here is what you should type at the boot prompt:

```
brltty=auto,ttyS0,en_US

```

Once brltty is running, you may wish to disable speech. You can do so via the "print screen" key, also known as sysrq. On my qwerty keyboard, that key is located directly above the insert key, between F12 and scroll lock.

## Maintaining your speech-enabled Arch Linux installation

You shouldn't need to do anything extraordinary to maintain the installation. Everything should just seamlessly work.

## Mastering speech-enabled ISO images

look at [talkingarch github page](https://github.com/alex19EP/talkingarch/)

## Further resources

TalkingArch has an IRC channel at #talkingarch on irc.talkabout.cf. Feel free to drop in and talk to the maintainers or anyone else in the channel.

## Disclaimer

This is not an official release. It is not endorsed by anyone other than its maintainers. It is provided solely for the convenience of blind and visually impaired users, and it comes with absolutely no warranty.