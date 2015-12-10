# Sony Vaio VGN NR320FH

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

**This article or section needs language, wiki syntax or style improvements.**

**Reason:** please use the first argument of the template to provide a brief explanation. (Discuss in [Talk:Sony Vaio VGN NR320FH#](https://wiki.archlinux.org/index.php/Talk:Sony_Vaio_VGN_NR320FH))

**Note:** When I plugged my headphones to the jack the speakers were still turned on. This was due to some alsa options. **Solution:** Add the following line to **/etc/modprobe.d/modprobe.conf**:

```
options snd-hda-intel model=sony-assamd

```

Also here's my alsa-info.sh output: [link[[1]](http://www.alsa-project.org/db/?f=87a0375da784b69f99081b708f4b1cc1c02479d7)]

Needs some work

*   FN Keys (Volume)
    *   **Solution:** Use xev to map the keyodes. Then load them:

My .Xdefaults:

```
keycode 174 = XF86AudioLowerVolume
keycode 176 = XF86AudioRaiseVolume
keycode 160 = XF86AudioMute
keycode 151 = XF86AudioPlay

```

*   A 1280x800 framebuffer (Needed for splashy, and I guess other boot splash managers)
    *   **Solution:** This guide: [Uvesafb](/index.php/Uvesafb "Uvesafb")

*   S1 and AV Mode Buttons (to the left of the power button) work weird. S1 prints keycode 101 but when triggered (mapped or not) it also triggers Brightness down in Gnome. AV Mode does nothing, however it prints some output to xev:

```
FocusOut event, serial 34, synthetic NO, window 0x3800001,
   mode NotifyGrab, detail NotifyAncestor

```

```
FocusIn event, serial 34, synthetic NO, window 0x3800001,
   mode NotifyUngrab, detail NotifyAncestor

```

```
KeymapNotify event, serial 34, synthetic NO, window 0x0,
   keys:  2   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   
          0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=Sony_Vaio_VGN_NR320FH&oldid=349256](https://wiki.archlinux.org/index.php?title=Sony_Vaio_VGN_NR320FH&oldid=349256)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Sony](/index.php/Category:Sony "Category:Sony")