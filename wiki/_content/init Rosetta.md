# init Rosetta

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** Add comparisons with the other available [init](/index.php/Init "Init") systems. (Discuss in [Talk:Init Rosetta#](https://wiki.archlinux.org/index.php/Talk:Init_Rosetta))

Related articles

*   [init](/index.php/Init "Init")

This article draws a parallel between [systemd](/index.php/Systemd "Systemd") and other [init](/index.php/Init "Init") systems.

You can omit the `.service` and `.target` extensions, especially if temporarily editing the [kernel parameters](/index.php/Kernel_parameters "Kernel parameters").

## SysVinit

<table class="wikitable">

<tbody>

<tr>

<th>systemd</th>

<th>SysVinit</th>

<th>OpenRC</th>

<th>Description</th>

</tr>

<tr>

<td>`systemctl list-units`</td>

<td>`rc.d list`</td>

<td>`rc-status`</td>

<td>List running services status</td>

</tr>

<tr>

<td>`systemctl --failed`</td>

<td>`rc-status --crashed`</td>

<td>Check failed services</td>

</tr>

<tr>

<td>`systemctl --all`</td>

<td>`rc-update -v show`</td>

<td>Display all available services.</td>

</tr>

<tr>

<td>`systemctl (start, stop, restart, status) daemon.service`</td>

<td>`rc.d (start, stop, restart) daemon`</td>

<td>`rc-service daemon (start, stop, restart, status)`</td>

<td>Change service state.</td>

</tr>

<tr>

<td>`systemctl (enable, disable) daemon.service`</td>

<td>`chkconfig daemon (on, off)`</td>

<td>`rc-update (add, del) daemon`</td>

<td>Turn service on or off.</td>

</tr>

<tr>

<td>`systemctl daemon-reload`</td>

<td>`chkconfig daemon --add`</td>

<td>Create or modify configuration.</td>

</tr>

</tbody>

</table>

### Targets table

<table class="wikitable">

<tbody>

<tr>

<th>systemd Target</th>

<th>SysV Runlevel</th>

<th>Notes</th>

</tr>

<tr>

<td>runlevel0.target, poweroff.target</td>

<td>0</td>

<td>Shut down the system.</td>

</tr>

<tr>

<td>runlevel1.target, rescue.target</td>

<td>1, s, single</td>

<td>Single user mode.</td>

</tr>

<tr>

<td>runlevel2.target, runlevel4.target, multi-user.target</td>

<td>2, 4</td>

<td>User-defined/Site-specific runlevels. By default, identical to 3.</td>

</tr>

<tr>

<td>runlevel3.target, multi-user.target</td>

<td>3</td>

<td>Multi-user, non-graphical. Users can usually login via multiple consoles or via the network.</td>

</tr>

<tr>

<td>runlevel5.target, graphical.target</td>

<td>5</td>

<td>Multi-user, graphical. Usually has all the services of runlevel 3 plus a graphical login.</td>

</tr>

<tr>

<td>runlevel6.target, reboot.target</td>

<td>6</td>

<td>Reboot</td>

</tr>

<tr>

<td>emergency.target</td>

<td>emergency</td>

<td>Emergency shell</td>

</tr>

</tbody>

</table>

Retrieved from "[https://wiki.archlinux.org/index.php?title=Init_Rosetta&oldid=362994](https://wiki.archlinux.org/index.php?title=Init_Rosetta&oldid=362994)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Boot process](/index.php/Category:Boot_process "Category:Boot process")