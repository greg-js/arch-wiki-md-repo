# init Rosetta

Related articles

*   [init](/index.php/Init "Init")

This article draws a parallel between [systemd](/index.php/Systemd "Systemd") and other [init](/index.php/Init "Init") systems.

You can omit the `.service` and `.target` extensions, especially if temporarily editing the [kernel parameters](/index.php/Kernel_parameters "Kernel parameters").

## SysVinit

| systemd | SysVinit | OpenRC | Description |
| `systemctl list-units` | `rc.d list` | `rc-status` | List running services status |
| `systemctl --failed` | `rc-status --crashed` | Check failed services |
| `systemctl --all` | `rc-update -v show` | Display all available services. |
| `systemctl (start, stop, restart, status) daemon.service` | `rc.d (start, stop, restart) daemon` | `rc-service daemon (start, stop, restart, status)` | Change service state. |
| `systemctl (enable, disable) daemon.service` | `chkconfig daemon (on, off)` | `rc-update (add, del) daemon` | Turn service on or off. |
| `systemctl daemon-reload` | `chkconfig daemon --add` | Create or modify configuration. |

### Targets table

| systemd Target | SysV Runlevel | Notes |
| runlevel0.target, poweroff.target | 0 | Shut down the system. |
| runlevel1.target, rescue.target | 1, s, single | Single user mode. |
| runlevel2.target, runlevel4.target, multi-user.target | 2, 4 | User-defined/Site-specific runlevels. By default, identical to 3. |
| runlevel3.target, multi-user.target | 3 | Multi-user, non-graphical. Users can usually login via multiple consoles or via the network. |
| runlevel5.target, graphical.target | 5 | Multi-user, graphical. Usually has all the services of runlevel 3 plus a graphical login. |
| runlevel6.target, reboot.target | 6 | Reboot |
| emergency.target | emergency | Emergency shell |

Retrieved from "[https://wiki.archlinux.org/index.php?title=Init_Rosetta&oldid=362994](https://wiki.archlinux.org/index.php?title=Init_Rosetta&oldid=362994)"