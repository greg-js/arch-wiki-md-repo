# ArchWiki:Reports

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

This table is used to report questionable edits as described in [ArchWiki:Maintenance Team](/index.php/ArchWiki:Maintenance_Team "ArchWiki:Maintenance Team"). Please use the [talk page](/index.php/ArchWiki_talk:Reports "ArchWiki talk:Reports") for discussing reports.

<table class="wikitable sortable" border="1">

<tbody>

<tr>

<th>Diff</th>

<th>Timestamp</th>

<th>Type</th>

<th>Notes</th>

</tr>

<tr>

<td>[VirtualBox](https://wiki.archlinux.org/index.php?title=VirtualBox&diff=next&oldid=300995)</td>

<td style="white-space: nowrap;">2014-03-02 22:47:46</td>

<td>content</td>

<td>The script should probably not be installed in `/sbin` (resp. `/usr/bin`), but will _mount_ recognize different path, e.g. `/usr/local/sbin`?</td>

</tr>

<tr>

<td>[Python](https://wiki.archlinux.org/index.php?title=Python&curid=5717&diff=310404&oldid=309101)</td>

<td>2014-04-14 12:25:13</td>

<td>content</td>

<td>not exactly "repeated", it was added with [[1]](https://wiki.archlinux.org/index.php?title=Python&diff=294397&oldid=294307), I can't test it right now</td>

</tr>

<tr>

<td>[Linux_Containers](https://wiki.archlinux.org/index.php?title=Linux_Containers&diff=next&oldid=313748)</td>

<td>2014-05-06 22:03:51</td>

<td>content</td>

<td>this edit should be double-checked, at a glance some content seems lost without explanation, some links are lost, there are several style issues (e.g. pacman -Sy); note that the initial part has been restored in another place with the next edit [[2]](https://wiki.archlinux.org/index.php?title=Linux_Containers&diff=next&oldid=313750)</td>

</tr>

<tr>

<td>[Bluez4](https://wiki.archlinux.org/index.php?title=Bluez4&diff=next&oldid=309941)</td>

<td>2014-05-04 20:42:58</td>

<td>content</td>

<td>Is `module-bluetooth-device` relevant for Bluez4, or just for Bluez5? Either way, there should be only one set of modules.</td>

</tr>

<tr>

<td>[Pkgfile](https://wiki.archlinux.org/index.php?title=Pkgfile&diff=next&oldid=341680)</td>

<td>2014-10-27 13:54:37</td>

<td>content</td>

<td>formatting in section headings; introduced a function for [Fish](/index.php/Fish "Fish"), but considering that [this section for Bash](/index.php/Bash#Command-not-found_.28AUR.29 "Bash") has been moved in and out multiple times recently, it does not fit in.</td>

</tr>

<tr>

<td>[Python](https://wiki.archlinux.org/index.php?title=Python&diff=next&oldid=343316)</td>

<td>2014-11-05 14:14:25</td>

<td>content</td>

<td>This is more complicated, `python -m venv` works without installing [python-virtualenv](https://www.archlinux.org/packages/?name=python-virtualenv).</td>

</tr>

<tr>

<td>[PhpPgAdmin](https://wiki.archlinux.org/index.php?title=PhpPgAdmin&curid=11293&diff=346886&oldid=345943)</td>

<td>2014-11-28 11:09:42</td>

<td>style</td>

<td>I'm not qualified to check the content, but style is poor regardless</td>

</tr>

<tr>

<td>[AMD_Catalyst](https://wiki.archlinux.org/index.php?title=AMD_Catalyst&diff=next&oldid=339951)</td>

<td>2014-12-18 18:29:24</td>

<td>content</td>

<td>I've never heard of Arch using `/usr/X11R6/` path</td>

</tr>

<tr>

<td>[Uniform_Look_for_Qt_and_GTK_Applications](https://wiki.archlinux.org/index.php?title=Uniform_Look_for_Qt_and_GTK_Applications&diff=355820&oldid=353302)</td>

<td>2015-01-07 20:22:56</td>

<td>content</td>

<td>Unless the intention is to (re)style [LightDM](/index.php/LightDM "LightDM") itself, it could/should be done in [xprofile](/index.php/Xprofile "Xprofile").</td>

</tr>

<tr>

<td>[Qt](https://wiki.archlinux.org/index.php?title=Qt&diff=next&oldid=358120)</td>

<td>2015-02-20 18:38:44</td>

<td>content</td>

<td>Sounds like packaging bugs that should be reported.</td>

</tr>

<tr>

<td>[AMD_Catalyst](https://wiki.archlinux.org/index.php?title=AMD_Catalyst&curid=8947&diff=363433&oldid=361244)</td>

<td>2015-03-02 22:21:39</td>

<td>content</td>

<td>This is a general issue when using Polkit in a graphical environment without matching agent.</td>

</tr>

<tr>

<td>[Bumblebee](https://wiki.archlinux.org/index.php?title=Bumblebee&diff=364954&oldid=363929)</td>

<td>2015-03-11 00:18:57</td>

<td>content</td>

<td>DISPLAY variables are fleeting, output dump, other duplication</td>

</tr>

<tr>

<td>[Vagrant](https://wiki.archlinux.org/index.php?title=Vagrant&curid=17522&diff=368401&oldid=367783)</td>

<td>2015-04-03 15:18:48</td>

<td>content</td>

<td>packaging bugs and especially hacks to remedy them should not be described on the wiki</td>

</tr>

<tr>

<td>[NVIDIA](https://wiki.archlinux.org/index.php?title=NVIDIA&curid=1120&diff=369218&oldid=368531)</td>

<td>2015-04-10 17:09:42</td>

<td>content</td>

<td>config dump instead of explaining options, more generic issue cf. [Xrandr#Troubleshooting](/index.php/Xrandr#Troubleshooting "Xrandr")</td>

</tr>

<tr>

<td>[Install_from_existing_Linux](https://wiki.archlinux.org/index.php?title=Install_from_existing_Linux&diff=next&oldid=371130)</td>

<td>2015-04-27 15:18:53</td>

<td>content</td>

<td>Poor style. Also, is it the problem with LVM on Debian or with trying to install Arch on LVM?</td>

</tr>

<tr>

<td>[CUPS](https://wiki.archlinux.org/index.php?title=CUPS&curid=982&diff=371948&oldid=371826)</td>

<td>2015-04-30 19:52:46</td>

<td>content</td>

<td>vague "workaround", doesn't mention why or how the "conflict" exists</td>

</tr>

<tr>

<td>[Power_management](https://wiki.archlinux.org/index.php?title=Power_management&curid=14678&diff=379621&oldid=376366)</td>

<td>2015-06-21 20:45:02</td>

<td>content</td>

<td>we can't document every screenlocker quirk on a general systemd page</td>

</tr>

<tr>

<td>[Lighttpd](https://wiki.archlinux.org/index.php?title=Lighttpd&diff=next&oldid=379969)</td>

<td>2015-06-26 17:31:18</td>

<td>content</td>

<td>As the links are not directly related to ligttpd, perhaps an Accuracy template would be more appropriate?</td>

</tr>

<tr>

<td>[HiDPI](https://wiki.archlinux.org/index.php?title=HiDPI&curid=17360&diff=380667&oldid=380242)</td>

<td>2015-07-02 01:43:18</td>

<td>style</td>

<td>explicit echo command</td>

</tr>

<tr>

<td>[Transmission](https://wiki.archlinux.org/index.php?title=Transmission&curid=14119&diff=380691&oldid=379586)</td>

<td>2015-07-02 13:24:15</td>

<td>content</td>

<td>Transmission itself also provides these warnings [https://trac.transmissionbt.com/browser/trunk/libtransmission/tr-udp.c?rev=11956#L82](https://trac.transmissionbt.com/browser/trunk/libtransmission/tr-udp.c?rev=11956#L82) , otherwise no background and duplicats [sysctl](/index.php/Sysctl "Sysctl")</td>

</tr>

<tr>

<td>[XWiimote](https://wiki.archlinux.org/index.php?title=XWiimote&curid=12739&diff=381396&oldid=376304)</td>

<td>2015-07-09 06:09:37</td>

<td>style</td>

<td>Duplication with [bluetooth](/index.php/Bluetooth "Bluetooth"), poor style</td>

</tr>

<tr>

<td>[Steam/Game-specific_troubleshooting](https://wiki.archlinux.org/index.php?title=Steam/Game-specific_troubleshooting&curid=16228&diff=381103&oldid=380209)</td>

<td>2015-07-05 20:10:21</td>

<td>style</td>

<td>duplication with [Java](/index.php/Java "Java"), boiler plate</td>

</tr>

<tr>

<td>[ASUS_UL30A](https://wiki.archlinux.org/index.php?title=ASUS_UL30A&curid=9253&diff=380796&oldid=253549)</td>

<td>2015-07-03 15:20:29</td>

<td>content</td>

<td>possibly unrelated to Arch, no source, unrelated kernel parameters</td>

</tr>

<tr>

<td>[Steam/Game-specific_troubleshooting](https://wiki.archlinux.org/index.php?title=Steam/Game-specific_troubleshooting&curid=16228&diff=387162&oldid=381103)</td>

<td>2015-07-23 02:23:55</td>

<td>content</td>

<td>"an incompability", a ridiciulous hack like this needs some reference (or should just be deleted)</td>

</tr>

<tr>

<td>[WeeChat](https://wiki.archlinux.org/index.php?title=WeeChat&curid=10854&diff=387024&oldid=377229)</td>

<td>2015-07-22 10:42:55</td>

<td>content</td>

<td>there's hundreds of weechat plugins, we can't document them all</td>

</tr>

<tr>

<td>[OpenVAS](https://wiki.archlinux.org/index.php?title=OpenVAS&curid=9748&diff=388691&oldid=386014)</td>

<td>2015-07-28 07:29:28</td>

<td>style</td>

<td>systemd services should be reported upstream, or at least the arch bugtracker, instead of on archwiki page developers may not follow</td>

</tr>

<tr>

<td>[SSH_keys](https://wiki.archlinux.org/index.php?title=SSH_keys&curid=1156&diff=390131&oldid=389626)</td>

<td>2015-08-06 00:24:55</td>

<td>content</td>

<td>Silly alias hack was added for the n-th time, add a better approach or reword the section. Related following edit: [[3]](https://wiki.archlinux.org/index.php?title=SSH_keys&diff=next&oldid=390131).</td>

</tr>

<tr>

<td>[QEMU](https://wiki.archlinux.org/index.php?title=QEMU&curid=1173&diff=398150&oldid=394212)</td>

<td>2015-09-03 21:50:30</td>

<td>content</td>

<td>`-m` is mentioned in a Tip above, this should be expanded there as a warning (preferably with better background via links)</td>

</tr>

<tr>

<td>[Multiboot_USB_drive](https://wiki.archlinux.org/index.php?title=Multiboot_USB_drive&diff=next&oldid=399366)</td>

<td>2015-09-13 02:39:00</td>

<td>style</td>

<td>If the previous snippet is outdated, why not just remove it?</td>

</tr>

<tr>

<td>[Music_Player_Daemon/Tips_and_tricks](https://wiki.archlinux.org/index.php?title=Music_Player_Daemon/Tips_and_tricks&diff=next&oldid=400052)</td>

<td>2015-10-06 04:38:05</td>

<td>content</td>

<td>That's really bad description of [MPRIS](http://specifications.freedesktop.org/mpris-spec/latest/)' purpose. Follow-up: [[4]](https://wiki.archlinux.org/index.php?title=Music_Player_Daemon/Tips_and_tricks&diff=403536&oldid=403487)</td>

</tr>

<tr>

<td>[Rxvt-unicode](https://wiki.archlinux.org/index.php?title=Rxvt-unicode&curid=6447&diff=404018&oldid=404009)</td>

<td>2015-10-10 11:44:23</td>

<td>content</td>

<td>if by "new font" a new font setting for urxvt is meant, running xrdb ... is sufficient</td>

</tr>

<tr>

<td>[Toshiba_Z30-A](https://wiki.archlinux.org/index.php?title=Toshiba_Z30-A&curid=20323&diff=403989&oldid=367613)</td>

<td>2015-10-10 07:57:08</td>

<td>content</td>

<td>barely comprehensible, unclear "gnome does not check ..." nor what this aur package does</td>

</tr>

<tr>

<td>[VirtualBox](https://wiki.archlinux.org/index.php?title=VirtualBox&curid=3745&diff=400434&oldid=400154)</td>

<td>2015-09-18 12:04:14</td>

<td>content</td>

<td>editor isn't aware how kernel upgrades work on Arch, or did a partial upgrade</td>

</tr>

<tr>

<td>[Makepkg](https://wiki.archlinux.org/index.php?title=Makepkg&diff=next&oldid=404410#Signature_checking)</td>

<td>2015-10-15 14:33:20</td>

<td>style</td>

<td>The `auto-key-retrieve` option bypasses the added `--search-keys`, perhaps an explicit warning is in order?</td>

</tr>

<tr>

<td>[Tmux](https://wiki.archlinux.org/index.php?title=Tmux&curid=9362&diff=405285&oldid=398381)</td>

<td>2015-10-17 17:39:36</td>

<td>content</td>

<td>"now", belongs in [Tmux#Setting the correct term](/index.php/Tmux#Setting_the_correct_term "Tmux")</td>

</tr>

<tr>

<td>[TLP](https://wiki.archlinux.org/index.php?title=TLP&curid=11380&diff=405760&oldid=401719)</td>

<td>2015-10-20 19:41:22</td>

<td>style</td>

<td>so the X220 and T420 require _both_ tp_smapi and acpi_call ?</td>

</tr>

<tr>

<td>[Plex](https://wiki.archlinux.org/index.php?title=Plex&curid=16254&diff=407187&oldid=401109)</td>

<td>2015-10-28 11:20:08</td>

<td>content</td>

<td>out of scope, no context with other articles</td>

</tr>

<tr>

<td>[Matlab](https://wiki.archlinux.org/index.php?title=Matlab&curid=6036&diff=409486&oldid=408099)</td>

<td>2015-11-18 09:07:30</td>

<td>content</td>

<td>overly specific, yet no references to claimed behaviour</td>

</tr>

<tr>

<td>[VirtualBox](https://wiki.archlinux.org/index.php?title=VirtualBox&diff=413957&oldid=413779)</td>

<td>2015-12-31 15:18:01</td>

<td>content</td>

<td>information was lost on file conflicts, no indication the behaviour changed (if at all)</td>

</tr>

<tr>

<td>[LXQt](https://wiki.archlinux.org/index.php?title=LXQt&curid=13117&diff=413859&oldid=413729)</td>

<td>2015-12-30 16:10:17</td>

<td>content</td>

<td>No proof this is "required" besides a vague edit summary</td>

</tr>

<tr>

<td>[Steam](https://wiki.archlinux.org/index.php?title=Steam&curid=2540&diff=413763&oldid=413532)</td>

<td>2015-12-29 11:25:48</td>

<td>content</td>

<td>relating a wrong ELF class and disabling displays is inaccurate at best</td>

</tr>

<tr>

<td>[NFS/Troubleshooting](https://wiki.archlinux.org/index.php?title=NFS/Troubleshooting&curid=15558&diff=414053&oldid=413169)</td>

<td>2016-01-01 16:51:12</td>

<td>style</td>

<td>unintelligible</td>

</tr>

<tr>

<td>[Unofficial_user_repositories](https://wiki.archlinux.org/index.php?title=Unofficial_user_repositories&curid=1394&diff=414918&oldid=414760)</td>

<td>2016-01-11 09:10:09</td>

<td>content</td>

<td>repos for different distributions don't belong on archwiki</td>

</tr>

<tr>

<td>[Steam](https://wiki.archlinux.org/index.php?title=Steam&curid=2540&diff=414877&oldid=414674)</td>

<td>2016-01-10 12:49:57</td>

<td>content</td>

<td>purely speculative, editor likely didn't configure [ALSA](/index.php/ALSA "ALSA") correctly</td>

</tr>

<tr>

<td>[Dell_XPS_13_(2016)](https://wiki.archlinux.org/index.php?title=Dell_XPS_13_(2016)&curid=21659&diff=414780&oldid=414469)</td>

<td>2016-01-09 08:12:31</td>

<td>content</td>

<td>wrong place for [TLP](/index.php/TLP "TLP") workarounds, at least the issue should be restricted to the general case (for which there again is no bug report)</td>

</tr>

<tr>

<td>[Steam](https://wiki.archlinux.org/index.php?title=Steam&curid=2540&diff=414674&oldid=414314)</td>

<td>2016-01-08 02:21:18</td>

<td>content</td>

<td>needs external reference</td>

</tr>

</tbody>

</table>

Retrieved from "[https://wiki.archlinux.org/index.php?title=ArchWiki:Reports&oldid=417518](https://wiki.archlinux.org/index.php?title=ArchWiki:Reports&oldid=417518)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [ArchWiki](/index.php/Category:ArchWiki "Category:ArchWiki")