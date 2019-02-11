[Herbstluftwm](http://herbstluftwm.org) is a manual tiling window manager for X11 using Xlib and Glib.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Starting](#Starting)
*   [3 First steps](#First_steps)
*   [4 Configuration](#Configuration)
    *   [4.1 Multi-Monitor Support](#Multi-Monitor_Support)
*   [5 Commands](#Commands)
*   [6 Scripts and Hooks](#Scripts_and_Hooks)
    *   [6.1 Script to switch to the next empty tag](#Script_to_switch_to_the_next_empty_tag)
    *   [6.2 Script to cycle though paddings (or other settings)](#Script_to_cycle_though_paddings_(or_other_settings))
    *   [6.3 Script to change decoration per-tag](#Script_to_change_decoration_per-tag)
*   [7 See also](#See_also)

## Installation

[install](/index.php/Install "Install") the [herbstluftwm](https://www.archlinux.org/packages/?name=herbstluftwm) package or [herbstluftwm-git](https://aur.archlinux.org/packages/herbstluftwm-git/) for the development version.

## Starting

Run `herbstluftwm` with [xinit](/index.php/Xinit "Xinit").

## First steps

Read the [herbstluftwm(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/herbstluftwm.1) and [herbstclient(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/herbstclient.1) man pages, they contain a lot of information from an explanation of the binary tree in which the layout is kept to config file options and possible values.

## Configuration

Copy `/etc/xdg/herbstluftwm/autostart` file to `~/.config/herbstluftwm/autostart`. You can edit that file for your needs. Make sure the autostart file is executable, else you will probably end up without keybindings!

The configuration of herbstluftwm can be updated on-the-fly by running `herbstclient reload` (See [#Commands](#Commands)). Autostart is called on each reload, therefore within autostart you typically unmap all existing configuration first.

### Multi-Monitor Support

Herbstluftwm supports multiple monitors as a virtual concept; monitors in herbstluftwm do not have to match the real monitor configuration as reported by xrandr. It brings a lot of flexibility and gives the user more control over his/her monitor-arrangement. You can use `herbstclient detect_monitors` to automatically adapt to the physical setup. Otherwise, see the manpage on how to add, remove, resize and move monitors. Tags in a multi-monitor set-up are not "owned" by a monitor. This means that when one monitor switches to a tag that is active in another monitor, the two monitors will swap tags.

## Commands

Herbstclient is a very powerful tool, as it provides you with full control over your window manager from the command line.

There is a tab-completion for the parameters for herbstclient. Try `herbstclient list_commands` to show all parameters.

Right now there is no error message if you use wrong parameters on a command, but only a non-zero return value. If you do not show the return value of a command anyway (e.g. in your $SHELL-prompt), you might want to `echo $?` to find the return value of the last command.

## Scripts and Hooks

The main way to control herbstluftwm is though commands to herbstclient. Since herbstclient can be called from any script, you have great flexibility in controlling herbstluftwm this way. Furthermore, you can listen to window management events and react to them accordingly.

### Script to switch to the next empty tag

The following ruby script allows you to switch to the (next or previous) (full or empty) tag. Call it with the arguments (+1 or -1) and (full or empty). For example, if you save the script to herbst-move.py, then

```
python3 herbst-move.py +1 full

```

will move you to the next full tag. I use the following key bindings.

```
hc keybind $Mod-Left  spawn herbst-move.py -1 empty
hc keybind $Mod-Right spawn herbst-move.py +1 empty
hc keybind $Mod-Up spawn herbst-move.py -1 full
hc keybind $Mod-Down spawn herbst-move.py +1 full

```

And here is the script.

```
#!/usr/bin/env python3
def run(*cmd):
    from subprocess import Popen, PIPE
    proc = Popen(cmd, shell=False, stderr=PIPE, stdout=PIPE)
    return proc.stdout.read()

import sys
tag_offset, mode = sys.argv[1:]
tag_offset = int(tag_offset)
if mode == 'full':
    ch = {'.'}
elif mode == 'empty':
    ch = {':', '!'}
else:
    raise Exception('Unknown type ' + mode)
tag_list = run('herbstclient', 'tag_status', '0').strip().decode('ascii').split('\t')
tag_curr = int(run('herbstclient', 'attr', 'tags.focus.index').strip())
tag_next = (tag_curr + tag_offset) % len(tag_list)
while (tag_next != tag_curr) and (tag_list[tag_next][0] in ch):
    tag_next = (tag_next + tag_offset) % len(tag_list)
if tag_next != tag_curr:
    run('herbstclient', 'use_index', str(tag_next))

```

### Script to cycle though paddings (or other settings)

Here is a ruby script to cycle through a set of paddings, although you can modify it to cycle though any collection of settings. The script knows the previous layout by looking for the presence of two dummy files in /tmp.

```
#!/usr/bin/ruby

file1 = "/tmp/herbst-padding-1"
file2 = "/tmp/herbst-padding-2"

pad1 = 'pad 0 0 0 0 0'
pad2 = 'pad 0 0 20 0 200'
pad3 = 'pad 0 0 0 0 150'

files = [file1, file2].map{|f| File.exist? File.expand_path(f)}

if files == [false, false]  # 0 files
  system "herbstclient #{pad2}"
  system "touch #{file1}"
elsif files == [true, false]  # 1 file
  system "herbstclient #{pad1}"
  system "touch #{file2}"
else           # 2 files
  system "herbstclient #{pad3}"
  system "rm #{file1} #{file2}"
end

```

### Script to change decoration per-tag

The following Perl script demonstrates how to use hooks to react to window management events. It can be called in autostart (with backgrounding).

```
#!/usr/bin/perl
# This script watches for tag changes and gives visual feedback

## Configuration (fill with your tag names)
my %colors = (
	main => '#DD0000',
	devel => '#13B8E0',
	write => '#96E013',
	admin => '#C713E0'
);

## Apply tag color
# Right now we change the active window's border color to the tag's color.
sub redecorate
{
	my ($foo, $activity) = @_;
	system("herbstclient", "set", "window_border_active_color",
		"$colors{$activity}");
}

## main routine
use v5.20;

# set up a pipe for reading hooks
open HOOKS, "herbstclient -i '(tag_changed|reload)'|"
	or die "can't fork: $!";
# process incoming messages
OUTER:
while (<HOOKS>) {
	chomp;
	for ($_) {
		redecorate(split(/\t/)) when /^tag_changed/;
		last OUTER when /^reload/; # quit on reload
	}
}
close HOOKS or die "unfinished love story: $! $?"; # happens on hlwm crash

```

## See also

*   [The herbstluftwm homepage](http://herbstluftwm.org)
*   [Arch Linux BBS thread](https://bbs.archlinux.org/viewtopic.php?id=128646)
*   `/usr/share/doc/herbstluftwm/examples/` - various scripts
*   `/usr/share/doc/herbstluftwm/BUGS` - bugs
*   [A herbstluftwm thread on the CrunchBang Forums](http://crunchbang.org/forums/viewtopic.php?pid=204358%23p204358#p204358k)
*   **Screenshots and configuration files:** [on ArchLinux Forum](https://bbs.archlinux.org/viewtopic.php?id=133557), [on DotShare.it](http://dotshare.it/category/wms/herbstluft/)
*   `#herbstluftwm` - IRC channel at the irc.freenode.net
*   [User git repository #1](https://github.com/ypnos/hlwm) with autostart written in Perl and a few custom scripts
*   [User git repository #2](https://github.com/ylixir/hlwm-config) with autostart and panel written in Python