[lariza](https://github.com/vain/lariza/) is a simple and lightweight browser with minimal dependencies including [gtk2](https://www.archlinux.org/packages/?name=gtk2), [glib](https://www.archlinux.org/packages/?name=glib) and [webkit2gtk](https://www.archlinux.org/packages/?name=webkit2gtk). Generally considered to be one of the lightest front-end GUI interfaces to webkit2gtk in terms of binary size and resource consumption, notable features of lariza include an address/location bar, customizable [user agent](https://en.wikipedia.org/wiki/User_agent) and regex-based [adblocking](https://en.wikipedia.org/wiki/Ad_blocking), keyword based searching, a download manager and global content zoom. lariza leverages suckless.org [tabbed](https://www.archlinux.org/packages/?name=tabbed) to support tabs within a single window instance. Additionally, lariza supports the [XEmbed](https://freedesktop.org/wiki/Specifications/xembed-spec/) protocol which makes it possible to embed the runtime in another application. Notable feature exclusions include the lack of cookie/javascript/local storage toggles and support for custom stylesheets.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Environment variables](#Environment_variables)
    *   [2.2 Custom key bindings](#Custom_key_bindings)
    *   [2.3 Keyword based searching:](#Keyword_based_searching:)
    *   [2.4 Bookmarks workaround](#Bookmarks_workaround)
    *   [2.5 Adblock support](#Adblock_support)
*   [3 Using lariza](#Using_lariza)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 lariza + tabbed freezes with certain key press combinations](#lariza_.2B_tabbed_freezes_with_certain_key_press_combinations)
*   [5 See also](#See_also)

## Installation

lariza is available in the AUR as [lariza-git](https://aur.archlinux.org/packages/lariza-git/). Alternatively, source code is available on [GitHub](https://github.com/vain/lariza/).

To build lariza directly from GitHub, pass the following within a terminal session:

```
$ git clone [https://github.com/vain/lariza.git](https://github.com/vain/lariza.git)
$ cd lariza && make

```

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

Set various XDG environment variables to modify the default [WebKit](https://webkitgtk.org/) cache and [local storage](https://en.wikipedia.org/wiki/Web_storage) locations. To avoid setting global XDG environments which may affect other applications, XDG variables can be set on the terminal before calling lariza.

*   See [XDG Base Directory Specification](https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html).

**Tip:** lariza can be sandboxed and and environment variables set within the sandbox using [firejail](https://www.archlinux.org/packages/?name=firejail)

### Custom key bindings

Custom key bindings can be established to create a consistent and familiar input interface across applications. The default key bindings of lariza can be modified by adjusting the GDK definitions in the the `browser.c` source code file. For example, to globally change the default modifier from `Alt` to `Ctrl` requires changing all instances of `GDK_MOD1_MASK` to `GDK_CONTROL_MASK`.

**Tip:** The default `MOD1+q` (Close Window) and `MOD1+w` (Home) bindings can lead to unexpected window exits due to the relative proximity of the `q` and `w` keys to one another. Limit exposure to this by modifying `GDK_KEY_q` and/or `GDK_KEY_w` to suit your desired preference.

### Keyword based searching:

Keyword based searching can be configured by creating a file `~/.config/lariza/keywordsearch`:

**Note:** This location can be adjusted through the environment variable `XDG_CONFIG_HOME`

```
a [https://aur.archlinux.org/packages/?O=0&SeB=n&K=%s](https://aur.archlinux.org/packages/?O=0&SeB=n&K=%s)
cv [https://web.nvd.nist.gov/view/vuln/search-results?query=%s](https://web.nvd.nist.gov/view/vuln/search-results?query=%s)
d [https://duckduckgo.com/html/?q=%s](https://duckduckgo.com/html/?q=%s)
# g [https://wiki.gentoo.org/index.php?&search=%s](https://wiki.gentoo.org/index.php?&search=%s)
git [https://github.com/search?&q=%s](https://github.com/search?&q=%s)
p [https://www.archlinux.org/packages/?sort=&arch=x86_64&q=%s](https://www.archlinux.org/packages/?sort=&arch=x86_64&q=%s)

```

Each line consists of a keyword and a URI terminated with ` %s`. Typing `git lariza` in the address field + `Enter` will return the results of searching GitHub for lariza: [https://github.com/search?&q=lariza](https://github.com/search?&q=lariza). `#` commented lines are ignored.

### Bookmarks workaround

The author of lariza has explicitly stated that support for bookmarks is not forthcoming. A viable workaround is to create a static/dynamic HTML page with a list of links to serve as a Speed Dial page to be called with the home page key binding. See [lariza Speed Dial Example](http://pastebin.com/NpAvecWH) for a sample static page.

**Note:** Set the lariza home page environment variable accordingly: `LARIZA_HOME_URI=file:////home/example/.config/lariza/bookmarks.html`

### Adblock support

Support for blocking ads can be configured by creating a file `~/.config/lariza/adblock.black` with regular expressions:

```
.*/ad/.*
.*/ads/.*
^https?://ad.*
^https?://advert.*
^https?://.*\.advertising\.com/

```

## Using lariza

Provide multiple URIs to open when starting lariza:

```
$ lariza [https://archlinux.org](https://archlinux.org) [https://linux.slashdot.org/](https://linux.slashdot.org/) file:////home/example/.config/lariza/bookmarks.html

```

Prepend lariza with an environment variable to change the default WebKit local storage location:

```
$ XDG_DATA_HOME=/tmp lariza [https://344c6kbnjnljjzlz.onion](https://344c6kbnjnljjzlz.onion)

```

Set lariza to launch within a firejail sandbox using a [spectrwm](/index.php/Spectrwm "Spectrwm") window manager key binding:

```
# ~/.spectrwm.conf 

program[lariza] = firejail lariza
bind[lariza] = Mod+l

```

*   For complete documentation, review the latest README and man pages available on the lariza GitHub project page.

## Troubleshooting

### lariza + tabbed freezes with certain key press combinations

The default build of [tabbed](https://www.archlinux.org/packages/?name=tabbed) defines `SETPROP` which lariza is unaware of. Key press combinations which call `SETPROP` may freeze either lariza or the current X session or both. If [surf](https://www.archlinux.org/packages/?name=surf) or surf variants in AUR are being used, the resolution is to modify `SETPROP` key bindings within [tabbed](https://www.archlinux.org/packages/?name=tabbed) `config.h` and the application rebuilt so as to not conflict with lariza key bindings. Else, the `SETPROP` definition and subsequent calls can be safely commented out of [tabbed](https://www.archlinux.org/packages/?name=tabbed) `config.h` before being rebuilt.

## See also

*   [lariza GitHub project page](https://github.com/vain/lariza)
*   [lariza Author (Vain) website](https://www.uninformativ.de/projects/lariza/)