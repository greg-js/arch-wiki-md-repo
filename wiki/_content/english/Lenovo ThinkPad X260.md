The Lenovo ThinkPad X260 is the successor to the [Lenovo ThinkPad X240](/index.php/Lenovo_ThinkPad_X240 "Lenovo ThinkPad X240") and [Lenovo ThinkPad X250](/index.php/Lenovo_ThinkPad_X250 "Lenovo ThinkPad X250"). Major differences include the removal of VGA, removal of the SATA channel in the M.2 slots, and end of the 400nit screen option. New in this gen is the addition of HDMI, DDR4 memory, and improved battery life.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Configuration](#Configuration)
    *   [1.1 Fingerprint](#Fingerprint)
    *   [1.2 Use Print Key for Context Menu Key](#Use_Print_Key_for_Context_Menu_Key)
*   [2 Troubleshooting](#Troubleshooting)
    *   [2.1 fn-4 sleep hotkey not recognized](#fn-4_sleep_hotkey_not_recognized)
    *   [2.2 No audio from docking station](#No_audio_from_docking_station)
    *   [2.3 No audio over HDMI](#No_audio_over_HDMI)

## Configuration

### Fingerprint

Some X260's come with vfs (Validity Sensors) fingerprint readers. If this is the case then you will need to additionally install [libfprint-git](https://aur.archlinux.org/packages/libfprint-git/), along with fprintd. See [fprint](/index.php/Fprint "Fprint") for details.

**Note:** The VFS 5011 fingerprint sensor (USB vendor ID/product ID: 138a:0017) is supported as of libfprint v0.6.0 so the AUR package is no longer needed. ([source](https://www.thinkwiki.org/wiki/Integrated_Fingerprint_Reader)) This fingerprint reader has been successfully tested using [libfprint](https://www.archlinux.org/packages/?name=libfprint) v0.8.2-1

### Use Print Key for Context Menu Key

The keyboard of the X250, X260 and X270 has got a print screen key between the right ALT and CTRL key, where normally the context menu key is located. In the case you use the context menu key more often than the print screen key, you can use the print screen key for opening the context menu by configuring it with [Xmodmap](/index.php/Xmodmap "Xmodmap"):

 `~/.Xmodmap`  `keycode 107 = Menu` 

## Troubleshooting

### fn-4 sleep hotkey not recognized

Not sure if a BIOS level error or not. fn itself is regarded as an acpi wakeup event but fn-4 registers nothing, while working under windows.

### No audio from docking station

Kernel is already supported docking station after commit 3194ed4, but maybe not enable default, edit this file to enable it.

 `/etc/modprobe.d/alsa-base.conf`  `options snd-hda-intel model=thinkpad` 

### No audio over HDMI

Use "aplay -l" to list all audio devices. Use speaker-test to find the correct device-id for HDMI audio, e.g.

`speaker-test -c 2 -r 48000 -D hw:0,7`

Once you have identified the correct audio device id, add the device at the end of your /etc/pulse/default.pa:

 `/etc/pulse/default.pa`  `load-module module-alsa-sink device=hw:0,7 channels=2 rate=48000 sink_properties=device.description=HDMI` 

Finally:

`killall pulseaudio ; pulseaudio --check`