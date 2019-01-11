Web is the default web browser for [GNOME](/index.php/GNOME "GNOME"). Web provides a simple and minimalist interface for accessing the internet. Whilst it is developed primarily for GNOME, Web works acceptably in other [desktop environments](/index.php/Desktop_environments "Desktop environments") as well.

**Note:** Web was known as [Epiphany](https://wiki.gnome.org/Apps/Web) prior to version 3.4\. The application was given new descriptive names, one for each supported language. The name *Epiphany* is still used in numerous places such as the executable name, some package names, some desktop entries, and some GSettings schemas.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Blocking advertisements](#Blocking_advertisements)
    *   [2.2 Web applications](#Web_applications)
    *   [2.3 Custom stylesheet](#Custom_stylesheet)
    *   [2.4 Fonts](#Fonts)
    *   [2.5 Video](#Video)
*   [3 See also](#See_also)

## Installation

Web can be installed by [installing](/index.php/Install "Install") the [epiphany](https://www.archlinux.org/packages/?name=epiphany) package. If you want to save login passwords, install [gnome-keyring](https://www.archlinux.org/packages/?name=gnome-keyring).

## Configuration

### Blocking advertisements

Enabled by default, you can disable it by unchecking *Try blocking ads* in *Preferences*. EasyList, EasyPrivacy and Fanboy-annoyance are default blocking lists. All lists are periodically refreshed.

**Note:** Due to some missing features, for example element hiding, Web misses to block/hide some ads. See the [related bugreport](https://gitlab.gnome.org/GNOME/epiphany/issues/288) for progress.

To get list of currently enabled filters:

```
$ gsettings get org.gnome.Epiphany adblock-filters

```

To set new list of filters, for example [uBlock Origin default lists](https://github.com/gorhill/uBlock/wiki/Blocking-mode:-easy-mode):

```
$ gsettings set org.gnome.Epiphany adblock-filters "['https://easylist.to/easylist/easylist.txt', 'https://easylist.to/easylist/easyprivacy.txt', 'https://easylist.to/easylist/fanboy-annoyance.txt', 'https://pgl.yoyo.org/adservers/serverlist.php?hostformat=hosts&showintro=1&mimetype=plaintext', 'https://www.malwaredomainlist.com/hostslist/hosts.txt', 'https://mirror.cedia.org.ec/malwaredomains/justdomains']"

```

See [EasyList](https://easylist.to/) and [Known Adblock Plus subscriptions](https://adblockplus.org/en/subscriptions)) for some of the popular ad blocking lists.

### Web applications

Web can create web applications out of websites and add them to desktop menu. To configure and remove them enter `about:applications` in the address bar.

### Custom stylesheet

Web supports custom stylesheet you can enable under **Fonts and style** in **Preferences**.

Use example below to set new tab page layout and colors according to Adwaita dark variant:

 `~/.config/epiphany/user-stylesheet.css` 
```
#overview {
  background-color: #2E3436 !important;
  max-width: 100% !important;
  max-height: 100% !important;
  position: fixed !important;
}

#overview .overview-title {
  color: white !important;
}

```

### Fonts

Web does not check GNOME font settings, but checks [Font configuration](/index.php/Font_configuration "Font configuration").

### Video

See [GStreamer](/index.php/GStreamer "GStreamer") for required plugin installation.

## See also

*   [Apps/Web - GNOME Wiki!](https://wiki.gnome.org/Apps/Web)