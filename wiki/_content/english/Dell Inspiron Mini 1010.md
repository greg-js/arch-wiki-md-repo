BIOS upgrade is highly recommended before installing Arch Linux.

## Quirks

### Suspend

Suspend has issues caused by Intel SpeedStep. Disabling it in the BIOS will fix the issue but also not allow cpu scaling. The solution below seems to work **without** disabling speed step. Add this suspend script to `/etc/pm/sleep.d/00-dell-quirks.conf`

 `/etc/pm/sleep.d/00-dell-quirks.conf` 
```
#!/bin/sh
# intel suspend speedstep workaround
. "${PM_FUNCTIONS}"

case "$1" in
	hibernate|suspend)
		for i in /sys/devices/system/cpu/cpu*/online ; do
			echo 0 >$i
		done
		;;
	thaw|resume) 
		sleep 10	# run with one core for 10 secs
		for i in /sys/devices/system/cpu/cpu*/online ; do
			echo 1 >$i
		done
		;;
	*)
		;;
esac

```

And give it executable permissions:

```
# chmod +x /etc/pm/sleep.d/00-dell-quirks.conf

```

It may also be possible to fix the suspend problem by updating the BIOS. This fix was tested on BIOS A07.

### Sources

*   [blank screen on sleep and overflowing box on dell mini 1012](http://ubuntuforums.org/showpost.php?p=10244075&postcount=21)