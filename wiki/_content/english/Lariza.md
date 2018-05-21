[lariza](https://github.com/vain/lariza/) is a simple and lightweight browser with minimal dependencies against [webkit2gtk](https://www.archlinux.org/packages/?name=webkit2gtk). Generally considered to be one of the lightest front-end GUI interfaces to webkit2gtk in terms of binary size and resource consumption, notable features of lariza include an address/location bar, customizable [user agent](https://en.wikipedia.org/wiki/User_agent "wikipedia:User agent") and regex-based [adblocking](https://en.wikipedia.org/wiki/Ad_blocking "wikipedia:Ad blocking"), keyword based searching, a download manager and global content zoom. lariza leverages [suckless.org](http://suckless.org/) [tabbed](https://www.archlinux.org/packages/?name=tabbed) to support tabs within a single window instance. Additionally, lariza supports the [XEmbed](https://freedesktop.org/wiki/Specifications/xembed-spec/) protocol which makes it possible to embed the runtime in another application. Notable feature exclusions include the lack of cookie/JavaScript/local storage toggles and support for custom stylesheets.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Environment variables](#Environment_variables)
    *   [2.2 Custom key bindings](#Custom_key_bindings)
    *   [2.3 Keyword based searching](#Keyword_based_searching)
    *   [2.4 Bookmarks workaround](#Bookmarks_workaround)
        *   [2.4.1 Keyword based bookmarks](#Keyword_based_bookmarks)
        *   [2.4.2 Speed Dial home page](#Speed_Dial_home_page)
    *   [2.5 Disabling JavaScript](#Disabling_JavaScript)
    *   [2.6 Adblock support](#Adblock_support)
*   [3 Using lariza](#Using_lariza)
*   [4 Open urls with external applications](#Open_urls_with_external_applications)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 lariza + tabbed freezes with certain key combinations](#lariza_.2B_tabbed_freezes_with_certain_key_combinations)
*   [6 See also](#See_also)

## Installation

lariza is available in the AUR as [lariza-git](https://aur.archlinux.org/packages/lariza-git/). Alternatively, source code is available on [GitHub](https://github.com/vain/lariza/).

Install suckless.org [tabbed](https://www.archlinux.org/packages/?name=tabbed) if support for tabs within a single window instance of lariza is desired. tabbed will run detached and be automatically picked up by lariza. An alternative to tabbed is the use of a window manager which supports native tabbing such as [i3](/index.php/I3 "I3"), [PekWM](/index.php/PekWM "PekWM") and/or [fluxbox](/index.php/Fluxbox "Fluxbox").

## Configuration

### Environment variables

Customize select settings by way of environment variables in the rc file of your preferred shell:

```
export LARIZA_ACCEPTED_LANGUAGE=en-US
export LARIZA_DOWNLOAD_DIR=/home/example/dump
export LARIZA_HOME_URI=[https://www.archlinux.org/](https://www.archlinux.org/)
export LARIZA_USER_AGENT=Mozilla/5.0 (X11; Linux x86_64; rv:45.5.1) Gecko/20121011 Firefox/45.5.1
export LARIZA_ZOOM=1.0 # Default Zoom Level

```

Set various XDG environment variables to modify the default [WebKit](https://webkitgtk.org/) cache and/or [local storage](https://en.wikipedia.org/wiki/Web_storage "wikipedia:Web storage") locations. To avoid establishing a global environment which affects other applications, XDG variables should be set before calling lariza. [GTK+ variables](https://developer.gnome.org/gtk3/stable/gtk-running.html) can also be used to support the environment.

*   Specify a theme and cache directory before launching lariza without support for tabbed:

```
$ GTK_THEME=Adwaita:dark XDG_CACHE_HOME=/tmp lariza -T

```

*   See [XDG Base Directory Specification](https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html).
*   See [Using lariza](#Using_lariza) for additional examples.

**Tip:** lariza can be sandboxed and and environment variables set within the sandbox using [firejail](https://www.archlinux.org/packages/?name=firejail).

### Custom key bindings

Custom key bindings can be established to create a consistent and familiar input interface across applications. The default key bindings of lariza can be modified by adjusting the GDK definitions in the the `browser.c` source code file. For example, switching the default global modifier from `Alt` to `Ctrl` requires changing all instances of `GDK_MOD1_MASK` to `GDK_CONTROL_MASK`.

**Tip:** The default `MOD1+q` (Close Window) and `MOD1+w` (Home) bindings can lead to unexpected window exits due to the proximity of the `q` and `w` keys to one another. Limit exposure to this by modifying `GDK_KEY_q` and/or `GDK_KEY_w` to suit.

### Keyword based searching

Keyword based searching can be configured by creating `~/.config/lariza/keywordsearch`:

**Note:** This location can be adjusted through the environment variable `XDG_CONFIG_HOME`

```
a [https://aur.archlinux.org/packages/?O=0&SeB=n&K=%s](https://aur.archlinux.org/packages/?O=0&SeB=n&K=%s)
cv [https://web.nvd.nist.gov/view/vuln/search-results?query=%s](https://web.nvd.nist.gov/view/vuln/search-results?query=%s)
d [https://duckduckgo.com/html/?q=%s&kp=-1&k1=-1&kd=1](https://duckduckgo.com/html/?q=%s&kp=-1&k1=-1&kd=1)
# g [https://wiki.gentoo.org/index.php?&search=%s](https://wiki.gentoo.org/index.php?&search=%s)
git [https://github.com/search?&q=%s](https://github.com/search?&q=%s)
p [https://www.archlinux.org/packages/?sort=&arch=x86_64&q=%s](https://www.archlinux.org/packages/?sort=&arch=x86_64&q=%s)

```

Single line entries consist of a keyword and a URI `%s` query. Typing `git lariza` in the address field + `Enter` will return the results of searching GitHub for lariza: [https://github.com/search?&q=lariza](https://github.com/search?&q=lariza). Note that `#` commented lines are ignored.

### Bookmarks workaround

The author of lariza has explicitly stated that support for bookmarks is not forthcoming. Workarounds include:

#### Keyword based bookmarks

```
a [https://aur.archlinux.org/packages/?O=0&SeB=n&K=%s](https://aur.archlinux.org/packages/?O=0&SeB=n&K=%s)
p [https://www.archlinux.org/packages/?sort=&arch=x86_64&q=%s](https://www.archlinux.org/packages/?sort=&arch=x86_64&q=%s)
v [https://web.nvd.nist.gov/view/vuln/search-results?query=%s](https://web.nvd.nist.gov/view/vuln/search-results?query=%s)
ad [https://lists.archlinux.org/pipermail/arch-dev-public/](https://lists.archlinux.org/pipermail/arch-dev-public/)
bg [http://www.securityfocus.com/archive/1](http://www.securityfocus.com/archive/1)

```

Similar to [keyword based searching](#Keyword_based_searching) less the terminating query string. Typing `bg` in the address field + `Space` + `Enter` will return the current content of [http://www.securityfocus.com/archive/1](http://www.securityfocus.com/archive/1).

#### Speed Dial home page

Create a static/dynamic HTML page with a list of links to serve as a Speed Dial page to be called with the home page key binding. See [lariza Speed Dial Example](http://pastebin.com/3tVpksLf) for a sample static page.

**Note:** Set the lariza home page environment variable accordingly: `LARIZA_HOME_URI=file:///home/example/.config/lariza/bookmarks.html`

### Disabling JavaScript

lariza enables JavaScript by default. Rather, lariza passes through the default configuration of the underlying [webkit2gtk](https://www.archlinux.org/packages/?name=webkit2gtk) engine. Disabling JavaScript requires rebuilding webkit2gtk with the `-DENABLE_JIT=OFF` variable set.

**Warning:** This will effectively disable JavaScript across all applications which depend on webkit2gtk.

### Adblock support

Support for blocking ads or URIs in general can be configured by creating `~/.config/lariza/adblock.black` with [regular expressions](https://developer.gnome.org/glib/stable/glib-regex-syntax.html). Case-insensitive regexp and partial matches with glob wildcards are supported.

```
.*/ad/.*
.*/ads/.*
^https?://ad.*
^https?://advert.*
^https?://.*\.advertising\.com/

```

## Using lariza

*   Append lariza with multiple URIs to open in separate tabs:

```
$ lariza archlinux.org [https://linux.slashdot.org/](https://linux.slashdot.org/) file:///home/example/.config/lariza/bookmarks.html

```

*   Prepend lariza with environment variables to switch the default cache and local storage locations to `/dev/null`:

```
$ XDG_CACHE_HOME=/dev/null XDG_DATA_HOME=/dev/null lariza [https://3g2upl4pq6kufc4m.onion](https://3g2upl4pq6kufc4m.onion)

```

**Note:** This does not disable cache or local storage. Instead, cache and local storage data are retained within volatile memory and cleared upon application exit.

*   Improve upon the previous example by setting the configuration files directory to tmpfs and *running the profile completely in memory*:

```
$ XDG_CONFIG_HOME=/tmp XDG_CACHE_HOME=/dev/null XDG_DATA_HOME=/dev/null lariza [https://344c6kbnjnljjzlz.onion](https://344c6kbnjnljjzlz.onion)

```

**Note:** `XDG_CONFIG_HOME` must mirror the file and directory structure of `~/.config` whereby `/tmp/lariza/keywordsearch` is the equivalent of `~/.config/lariza/keywordsearch.`

*   Set lariza to launch within a [firejail](/index.php/Firejail "Firejail") sandbox using a [spectrwm](/index.php/Spectrwm "Spectrwm") window manager key binding:

```
# ~/.spectrwm.conf 

program[lariza] = firejail lariza -C
bind[lariza] = Mod+l

```

For complete documentation, review the latest README and man pages available on the [lariza GitHub project page](https://github.com/vain/lariza).

## Open urls with external applications

With newer versions of lariza, page url or selected url can be sent to an executable lariza-external-handler. This can be used to open youtube video with mpv/youtube-dl or opening magnet link with your favorite torrent client. To use this feature create script named lariza-external-handler in your path and make it executable. For an example (this script uses dmenu)

```
 #!/bin/bash

 shopt -s lastpipe
 ops=(
   mpv
   chromium )

 option=$(for i in "${ops[@]}"; do echo "$i"; done |  dmenu -p  "open <u>$url</u> with...")

 [[ ! $option ]] && exit

 case "$option" in
   mpv) mpv "$2" ;;
   chromium) chromium "$2" ;;
   *) $option "$2" ;;
 esac
```

To call this script from lariza use key "alt+x", this will send page url to the script as "lariza-external-handler -u $url", or right click on a link and select lariza-external-handler from context menu.

## Troubleshooting

### lariza + tabbed freezes with certain key combinations

The default build of [tabbed](https://www.archlinux.org/packages/?name=tabbed) binds two key combinations to `spawn`. Key combinations which call `spawn` to fork may freeze either lariza or the current X session or both.

*   Avoid key press combinations bound to the `spawn` function call. This is the easiest solution.
*   Modify `spawn` bindings in tabbed `config.h` to avoid conflicting with lariza key bindings. *Rebuild tabbed*.
*   Comment out all key combinations bound to `spawn` in tabbed `config.h`. *Rebuild tabbed*.

## See also

*   [lariza GitHub project page](https://github.com/vain/lariza)
*   [lariza Author (Vain) website](https://www.uninformativ.de/projects/lariza/)