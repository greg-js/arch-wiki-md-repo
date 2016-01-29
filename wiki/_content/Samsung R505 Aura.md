# Samsung R505 Aura

### LCD Brightness

See [Backlight](/index.php/Backlight "Backlight").

### Audio Volume hotkeys

If you are using LXDE, the following steps will get your Audio Volume hotkeys Fn-Right and Fn-Left as well as Fn-F6 to work.

First, you have to make sure that alsa is configured correctly. You can configure alsa using

```
# alsaconfig

```

Executing

```
# alsamixer

```

you can adjust the volumes to a convenient setting. Then, adding

```
@ alsa

```

to the DAEMONS section of your rc.conf, you can ensure that the values you just specified will be loaded on every startup. Finally, paste the following lines into the <keyboard>-section of your ~/.config/openbox/lxde-rc.xml file.

```
 <!-- Keybindings for audio volume control -->
    <keybind key="XF86AudioRaiseVolume">
      <action name="Execute">
        <command>amixer -q set PCM 2+ unmute</command>
      </action>
    </keybind>
    <keybind key="XF86AudioLowerVolume">
      <action name="Execute">
        <command>amixer -q set PCM 2- unmute</command>
      </action>
    </keybind><keybind key="XF86AudioMute">
      <action name="Execute">
        <command>amixer -q set Master toggle</command>
      </action>
    </keybind>

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=Samsung_R505_Aura&oldid=368752](https://wiki.archlinux.org/index.php?title=Samsung_R505_Aura&oldid=368752)"