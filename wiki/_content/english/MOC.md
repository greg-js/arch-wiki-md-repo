[Music On Console](https://moc.daper.net/) is a lightweight music player similar to [MPD](/index.php/MPD "MPD"), but unlike it, MOC comes with an interface and its server does not support remote access.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 PulseAudio](#PulseAudio)
*   [2 Front-ends](#Front-ends)
*   [3 Configuration](#Configuration)
    *   [3.1 Using PulseAudio](#Using_PulseAudio)
    *   [3.2 Navigation](#Navigation)
    *   [3.3 systemd service](#systemd_service)
    *   [3.4 Themes](#Themes)
*   [4 Usage](#Usage)
*   [5 Scrobbling](#Scrobbling)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 MOC fails to start](#MOC_fails_to_start)
    *   [6.2 Strange characters](#Strange_characters)
    *   [6.3 FATAL_ERROR: Layout1 is malformed](#FATAL_ERROR:_Layout1_is_malformed)
*   [7 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [moc](https://www.archlinux.org/packages/?name=moc) package.

### PulseAudio

For [PulseAudio](/index.php/PulseAudio "PulseAudio") support install [moc-pulse](https://aur.archlinux.org/packages/moc-pulse/) or [moc-pulse-svn](https://aur.archlinux.org/packages/moc-pulse-svn/) for the development version. To use the pulseaudio driver, go to [#Using PulseAudio](#Using_PulseAudio).

## Front-ends

*   **mocicon** — GTK panel applet to control MOC

	[http://mocicon.sourceforge.net/](http://mocicon.sourceforge.net/) || [mocicon](https://aur.archlinux.org/packages/mocicon/)

*   **eXo** — Qt frontend to MOC, supports scrobbling

	[https://bitbucket.org/blaze/exo/](https://bitbucket.org/blaze/exo/) || [exo-player](https://aur.archlinux.org/packages/exo-player/)

## Configuration

Sample configuration files can be found in `/usr/share/doc/moc/`. On *mocp* first run, the `~/.moc/` directory is created. To configure, copy the examples to it and edit accordingly.

To use MOC with v4.1 [OSS](/index.php/OSS "OSS"), see [OSS#MOC](/index.php/OSS#MOC "OSS").

To change the default key bindings, see `/usr/share/doc/moc/keymap.example`.

### Using PulseAudio

If you have [moc-pulse](https://aur.archlinux.org/packages/moc-pulse/) or [moc-pulse-svn](https://aur.archlinux.org/packages/moc-pulse-svn/) downloaded, locate the variable `SoundDriver` and add `PULSEAUDIO:` to the front.

```
SoundDriver = PULSEAUDIO:JACK:ALSA:OSS

```

This ensures that PulseAudio gets loaded with first priority. Listing other sound drivers after this are fallbacks when the previous ones are not available.

### Navigation

To change directories with the arrow keys uncomment in `~/.moc/config`:

```
Keymap = keymap

```

Edit the following in `~/.moc/keymap`:

```
go    = ENTER RIGHT
go_up = U LEFT
#seek_forward  = RIGHT
#seek_backward = LEFT

```

To speed up navigation and detach, set the following in `~/.moc/config`:

```
ReadTags = no
ShowTime = no
TagsCacheSize = 0

```

### systemd service

[Enable](/index.php/Enable "Enable") this service for the respective user:

 `/etc/systemd/system/moc@.service` 
```
[Unit]
Description=MOC server
ConditionPathExists=/usr/bin/mocp
After=network.target sound.target

[Service]
RemainAfterExit=yes
User=%I
ExecStart=/usr/bin/mocp -S
ExecStop=/usr/bin/mocp -x
WorkingDirectory=/home/%I/

[Install]
WantedBy=multi-user.target

```

### Themes

Themes are stored in `~/.moc/themes/` and can be set in `~/.moc/config`. Example theme:

```
background                     = white black
frame                          = white black
window_title                   = white black
directory                      = white black
selected_directory             = white black reverse
playlist                       = white black
selected_playlist              = white black reverse
file                           = white black
selected_file                  = white black reverse
selected_info                  = white black reverse
marked_file                    = white black bold
marked_selected_file           = white black reverse
info                           = white black
marked_info                    = white black bold
marked_selected_info           = white black reverse
status                         = white black
title                          = white black bold
state                          = white black
current_time                   = white black bold
time_left                      = white black bold
total_time                     = white black bold
time_total_frames              = white black
sound_parameters               = white black bold
legend                         = white black
disabled                       = white black
enabled                        = white black bold
empty_mixer_bar                = white black
filled_mixer_bar               = white black reverse
empty_time_bar                 = white black
filled_time_bar                = white black reverse
entry                          = white black
entry_title                    = white black
error                          = white black bold
message                        = white black
plist_time                     = white black

```

See `/usr/share/moc/themes/example_theme` for more.

## Usage

Run *mocp* to start the server and interface. Some useful default shortcuts (press `h` for more):

| Start playing at this file or go to this directory | `Enter` |
| Pause | `Space` or `p` |
| Play next file | `n` |
| Play previous file | `b` |
| Silent seek forward by 5s | `]` |
| Silent seek backward by 5s | `[` |
| Switch between playlist and file list | `Tab` |
| Add a file/directory to the playlist | `a` |
| Add a directory recursively to the playlist | ``Shift+a`` |
| Delete an item from the playlist | `d` |
| Clear the playlist | ``Shift+c`` |
| Increase volume by 1% | `>` |
| Decrease volume by 1% | `<` |
| Increase volume by 5% | `.` (period) |
| Decrease volume by 5% | `,` (comma) |
| Set volume to 10% | `Alt+1` |
| Set volume to 90% | `Alt+9` |
| Detach MOC from the server | `q` |
| Quit | ``Shift+q`` |

**Tip:** To not wait for detach (as it sometimes takes a moment), `Ctrl+z` can be used instead.

To shut down the server, run the `mocp -x` command.

## Scrobbling

[mocp-scrobbler](https://aur.archlinux.org/packages/mocp-scrobbler/) is a Last.fm (and Libre.fm) scrobbler for MOC with support for now-playing notifications, daemonization and cache. It only depends on [Python](/index.php/Python "Python") 3.

**Note:** To use Libre.fm instead of Last.fm change `hostname` from `post.audioscrobbler.com` to `turtle.libre.fm`.

Copy the example file to your user config directory:

```
mkdir ~/.mocpscrob/
cp /usr/share/doc/mocp-scrobbler/config.example  ~/.mocpscrob/config

```

Edit `~/.mocpscrob/config` to add your login and password. The password variable will be replaced with `password_md5` on the first run. Its value will be the original value hashed using MD5 algorithm. If you want to change password, just add again password with you new password, and `password_md5` will be replaced.

To scrobble tracks, start *mocp-scrobbler* as daemon before *mocp*. You can also use an [alias](/index.php/Alias "Alias"):

```
alias mocp='/usr/bin/mocp-scrobbler.py -d; mocp'

```

In January of 2016 last.fm updated their password requirements, with all new and updated passwords requiring the inclusion of one of the following characters `!"#$%&'()*+,-./:;<=>?@[\]^_`{|}~`, or a space. This is known to cause an authentication error with mocpscrob configurations which specify passwords not conforming to these new specifications. Changing one's password and updating the `~/.mocpscrob/config` password accordingly resolves this issue.

## Troubleshooting

### MOC fails to start

If MOC fails to start, it is most probably because of something wrong in `~/.moc/`. You can try to fix it, or simply delete the whole folder.

### Strange characters

If you see strange-like characters displayed instead of the normal lines (vertical lines to separate space, etc.), you may have a font set incompatible to MOC. Either change the respective font, or edit `.moc/config` to use ASCII for drawing lines:

```
ASCIILines = no

```

### FATAL_ERROR: Layout1 is malformed

If MOC crashes with this error, try adding either line to `.moc/config`:

```
Layout1 = directory(0,0,50%,100%): playlist(50%,0,100%,100%)

```

or

```
Layout1 = directory(0,0,50%,100%): playlist(50%,0,FILL,100%)

```

See [original report](http://moc.daper.net/node/262) and [Debian bugs](https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=485059).

## See also

*   [Official documentation](http://moc.daper.net/documentation)