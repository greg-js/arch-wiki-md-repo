## Contents

*   [1 Hardware](#Hardware)
*   [2 Networking](#Networking)
    *   [2.1 Wireless](#Wireless)
*   [3 Power Management](#Power_Management)
    *   [3.1 ACPI](#ACPI)
    *   [3.2 CPU frequency scaling](#CPU_frequency_scaling)
*   [4 Xorg](#Xorg)
*   [5 Special keys](#Special_keys)
*   [6 External Resources](#External_Resources)

## Hardware

**Processor:** Intel Pentium M (Centrino) 1.50GHz

**Video:** Intel Corporation Mobile 915GM/GMS/910GML Chipset

**Audio:** Intel Corporation 82801FB/FBM/FR/FW/FRW (ICH6 Family) AC'97 Audio

**Wired NIC:** Broadcom Corporation NetXtreme BCM5788 Gigabit Ethernet (rev 03)

**Wireless NIC:** Intel Corporation PRO/Wireless 2200BG Network Connection (rev 05)

## Networking

### Wireless

See [Wireless network configuration#ipw2100 and ipw2200](/index.php/Wireless_network_configuration#ipw2100_and_ipw2200 "Wireless network configuration").

## Power Management

### ACPI

Install [ACPI daemon](/index.php/Acpid "Acpid") and start it.

I found out that when booted with ACPI on, the laptop makes kind of high frequency noise which can be really annoying when you work in otherwise quiet room. There is no such noise when you boot with `acpi=off`. I searched for a solution and I found this:

Add this line to `/etc/modprobe.d/modprobe.conf`:

```
options processor max_cstate=2

```

Then re-generate the initramfs image (see [mkinitcpio#Image creation and activation](/index.php/Mkinitcpio#Image_creation_and_activation "Mkinitcpio")). Reboot, and check if things work:

```
$ cat /proc/acpi/processor/CPU0/power |grep max_cstate
max_cstate:              C2

```

In this case, many thanks for finding solution go to [Victor Julien](http://www.inliniac.net/blog/2008/07/25/fixing-noise-on-ubuntu-hardy-804-aka-setting-max_cstate.html) [[1]](http://www.inliniac.net/blog/2008/07/25/fixing-noise-on-ubuntu-hardy-804-aka-setting-max_cstate.html)

NB: You should know that any of these solutions will reduce the battery life, so it seems so far that you need to choose which one is more important for you: either the longer-lasting battery or the quiet laptop. You can find more information about the whole problem concerning high pitch noise and ACPI CPU power saving states [here](http://www.thinkwiki.org/wiki/Problem_with_high_pitch_noises) [[2]](http://www.thinkwiki.org/wiki/Problem_with_high_pitch_noises)

### CPU frequency scaling

See the main [CPU frequency scaling](/index.php/CPU_frequency_scaling "CPU frequency scaling") article.

## Xorg

To make the touchpad work, edit your xorg.conf following this howto: [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics"). You may need to replace "AllwaysCore" with "SendCoreEvents" in the Section "ServerLayout" [[3]](https://bbs.archlinux.org/viewtopic.php?id=39492).

(Also look here for a useful trick: [Disable touchpad temporarily when typing](http://ubuntu.wordpress.com/2006/09/20/disable-touchpad-temporarily-when-typing/))

## Special keys

To use all the keyboard's special keys, I've installed [keytouch](/index.php/Keytouch "Keytouch").

 `/usr/share/keytouch/keyboards/Aspire 1690.Acer` 

```
<keyboard>
 <file-info>
   <syntax-version>1.1</syntax-version>
   <last-change format="%d-%m-%Y">13-08-2007</last-change>
   <author></author>
 </file-info>
 <keyboard-info>
   <keyboard-name>
     <manufacturer>Acer</manufacturer>
     <model>Aspire 1690</model>
   </keyboard-name>
 </keyboard-info>
 <key-list>
   <key>
     <name>Mute</name>
     <scancode>160</scancode>
     <keycode>MUTE</keycode>
     <default-action action-type="plugin">
       <plugin-name>Amixer</plugin-name>
       <plugin-function>Mute</plugin-function>
     </default-action>
   </key>
   <key>
     <name>Disable touchpad</name>
     <scancode>242</scancode>
     <keycode>LEFTMETA</keycode>
     <default-action></default-action>
   </key>
   <key>
     <name>Disable screen</name>
     <scancode>56</scancode>
     <keycode>CYCLEWINDOWS</keycode>
     <default-action></default-action>
   </key>
   <key>
     <name>Help</name>
     <scancode>165</scancode>
     <keycode>HELP</keycode>
     <default-action>khelpcenter || gnome-help</default-action>
   </key>
   <key>
     <name>Brightness up</name>
     <scancode>238</scancode>
     <keycode>BRIGHTNESSUP</keycode>
     <default-action></default-action>
   </key>
   <key>
     <name>Brightness down</name>
     <scancode>239</scancode>
     <keycode>BRIGHTNESSDOWN</keycode>
     <default-action></default-action>
   </key>
   <key>
     <name>Volume Up</name>
     <scancode>176</scancode>
     <keycode>VOLUMEUP</keycode>
     <default-action action-type="plugin">
       <plugin-name>Amixer</plugin-name>
       <plugin-function>Volume increase</plugin-function>
     </default-action>
   </key>
   <key>
     <name>Volume Down</name>
     <scancode>174</scancode>
     <keycode>VOLUMEDOWN</keycode>
     <default-action action-type="plugin">
       <plugin-name>Amixer</plugin-name>
       <plugin-function>Volume decrease</plugin-function>
     </default-action>
   </key>
   <key>
     <name>Play/Pause</name>
     <scancode>162</scancode>
     <keycode>PLAYPAUSE</keycode>
     <default-action action-type="plugin">
       <plugin-name>XMMS</plugin-name>
       <plugin-function>Play/Pause</plugin-function>
     </default-action>
   </key>
   <key>
     <name>Stop CD</name>
     <scancode>164</scancode>
     <keycode>STOPCD</keycode>
     <default-action action-type="plugin">
       <plugin-name>XMMS</plugin-name>
       <plugin-function>Stop</plugin-function>
     </default-action>
   </key>
   <key>
     <name>Previous song</name>
     <scancode>144</scancode>
     <keycode>PREVIOUSSONG</keycode>
     <default-action action-type="plugin">
       <plugin-name>XMMS</plugin-name>
       <plugin-function>Previous</plugin-function>
     </default-action>
   </key>
   <key>
     <name>Next song</name>
     <scancode>153</scancode>
     <keycode>NEXTSONG</keycode>
     <default-action action-type="plugin">
       <plugin-name>XMMS</plugin-name>
       <plugin-function>Next</plugin-function>
     </default-action>
   </key>
   <key>
     <name>Video out</name>
     <scancode>169</scancode>
     <keycode>SWITCHVIDEOMODE</keycode>
     <default-action></default-action>
   </key>
   <key>
     <name>P Key</name>
     <scancode>243</scancode>
     <keycode>PROG1</keycode>
     <default-action>keytouch</default-action>
   </key>
   <key>
     <name>E key</name>
     <scancode>244</scancode>
     <keycode>PROG2</keycode>
     <default-action>keytouch</default-action>
   </key>
   <key>
     <name>WWW</name>
     <scancode>178</scancode>
     <keycode>WWW</keycode>
     <default-action action-type="plugin">
       <plugin-name>WWW Browser</plugin-name>
       <plugin-function>Home</plugin-function>
     </default-action>
   </key>
   <key>
     <name>E-mail</name>
     <scancode>236</scancode>
     <keycode>EMAIL</keycode>
     <default-action action-type="plugin">
       <plugin-name>E-mail</plugin-name>
       <plugin-function>E-mail</plugin-function>
     </default-action>
   </key>
 </key-list>
</keyboard>

```

## External Resources

*   [Disable touchpad temporarily when typing](http://ubuntu.wordpress.com/2006/09/20/disable-touchpad-temporarily-when-typing/)
*   This report has been listed in the [Linux Laptop and Notebook Installation Guides Survey: Acer](http://tuxmobil.org/acer.html).