# Herbstluftwm

[Herbstluftwm](http://herbstluftwm.org) is a manual tiling window manager for X11 using Xlib and Glib.

## Contents

*   [1 Installation](#Installation)
*   [2 First steps](#First_steps)
*   [3 Configuration](#Configuration)
    *   [3.1 Multi-Monitor Support](#Multi-Monitor_Support)
*   [4 Commands](#Commands)
*   [5 Scripts and Hooks](#Scripts_and_Hooks)
    *   [5.1 Script to switch to the next empty tag](#Script_to_switch_to_the_next_empty_tag)
    *   [5.2 Script to cycle though paddings (or other settings)](#Script_to_cycle_though_paddings_.28or_other_settings.29)
    *   [5.3 Script to change decoration per-tag](#Script_to_change_decoration_per-tag)
*   [6 See also](#See_also)

## Installation

Herbstluftwm can be [installed](/index.php/Installed "Installed") with the package [herbstluftwm](https://www.archlinux.org/packages/?name=herbstluftwm) or the package [herbstluftwm-git](https://aur.archlinux.org/packages/herbstluftwm-git/)<sup><small>AUR</small></sup>.

## First steps

Carefully read the herbstluftwm and herbstclient man pages in your favorite terminal emulator or online ([herbstluftwm](http://herbstluftwm.org/herbstluftwm.html), [herbstclient](http://herbstluftwm.org/herbstclient.html)). Take your time to read through the whole documentation, they contain a lot of information from an explanation of the binary tree in which the layout is kept to config file options and possible values.

## Configuration

Copy `/etc/xdg/herbstluftwm/autostart` file to `$HOME/.config/herbstluftwm/autostart`. You can edit that file for your needs. Make sure the autostart file is executable, else you will probably end up without keybindings!

The configuration of herbstluftwm is updated on-the-fly by issuing `herbstclient reload` (See Commands section), or having a keybinding for the reload command. Autostart is called on each reload, therefore within autostart you typically unmap all existing configuration first.

### Multi-Monitor Support

Herbstluftwm supports multiple monitors as a virtual concept; monitors in herbstluftwm do not have to match the real monitor configuration as reported by xrandr. It brings a lot of flexibility and gives the user more control over his/her monitor-arrangement. You can use `herbstclient detect_monitors` to automatically adapt to the physical setup. Otherwise, see the manpage on how to add, remove, resize and move monitors. Tags in a multi-monitor set-up are not "owned" by a monitor. This means that when one monitor switches to a tag that is active in another monitor, the two monitors will swap tags.

## Commands

Herbstclient is a very powerful tool, as it provides you with full control over your window manager from the command line.

There is a tab-completion for the parameters for herbstclient. Try `herbstclient list_commands` to show all parameters.

Right now there is no error message if you use wrong parameters on a command, but only a non-zero return value. If you do not show the return value of a command anyway (e.g. in your $SHELL-prompt), you might want to `echo $?` to find the return value of the last command.

## Scripts and Hooks

The main way to control herbstluftwm is though commands to herbstclient. Since herbstclient can be called from any script, you have great flexibility in controlling herbstluftwm this way. Furthermore, you can listen to window management events and react to them accordingly.

### Script to switch to the next empty tag

The following ruby script allows you to switch to the (next or previous) (full or empty) tag. Call it with the arguments (+1 or -1) and (full or empty). For example, if you save the script to herbst-move.rb, then

```
ruby herbst-move.rb +1 full

```

will move you to the next full tag. I use the following key bindings.

```
hc keybind $Mod-Left  spawn ruby /home/carl/Ruby/herbst-move.rb -1 empty
hc keybind $Mod-Right spawn ruby /home/carl/herbst-move.rb +1 empty
hc keybind $Mod-Up spawn ruby /home/carl/Ruby/herbst-move.rb -1 full
hc keybind $Mod-Down spawn ruby /home/carl/Ruby/herbst-move.rb +1 full

```

And here is the script.

```
#!/usr/local/bin/ruby

incr, type = ARGV

d = incr.to_i
if type == 'full'
  ch = '.'
else
  ch = ':'
end

array = `herbstclient tag_status 0`.scan(/[:\.\#][^\t]*/)
len = array.length
orig = array.find_index{|e| e[0] == '#'}

i = (orig+d) % len
while 
  array[i][0] == ch
  i = (i+d) % len
end

if i != orig
  system "herbstclient use_index #{i}"
end

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
*   [The herbstluftwm thread](https://bbs.archlinux.org/viewtopic.php?id=128646)
*   `/usr/share/doc/herbstluftwm/examples/` - various scripts
*   `/usr/share/doc/herbstluftwm/BUGS` - bugs
*   [A herbstluftwm thread on the CrunchBang Forums](http://crunchbang.org/forums/viewtopic.php?pid=204358%23p204358#p204358k)
*   **Screenshots and configuration files:** [on ArchLinux Forum](https://bbs.archlinux.org/viewtopic.php?id=133557), [on DotShare.it](http://dotshare.it/category/wms/herbstluft/)
*   `#herbstluftwm` - IRC channel at the irc.freenode.net
*   [User git repository #1](https://github.com/ypnos/hlwm) with autostart written in Perl and a few custom scripts
*   [User git repository #2](https://github.com/ylixir/hlwm-config) with autostart and panel written in Python

Retrieved from "[https://wiki.archlinux.org/index.php?title=Herbstluftwm&oldid=415595](https://wiki.archlinux.org/index.php?title=Herbstluftwm&oldid=415595)"