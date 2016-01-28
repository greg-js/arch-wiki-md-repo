# Jabberd2

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

jabberd2 is an [XMPP](https://en.wikipedia.org/wiki/XMPP "wikipedia:XMPP") server, written in the C language and licensed as Free software under the GNU General Public License. It was inspired by jabberd14.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Daemon](#Daemon)
*   [3 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [jabberd2](https://aur.archlinux.org/packages/jabberd2/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/jabberd2)]</sup> package from the [AUR](/index.php/AUR "AUR"),

## Configuration

Edit `/etc/jabberd/c2s.xml` and look for the line starting with `<id register-enable='mu'>` and edit to have your domain.

Example:

 `/etc/jabberd/c2s.xml` 

```
<id register-enable='mu'>mymachine.com</id>

```

That is the line that will be added to your users id. (If you put there `mymachine.com`, your users id will be something like `user@mymachine.com`) If the jabber service is going to be accesible over open internet (instead of a vpn or lan), then that name **SHOULD** be resolved by DNS to your server.

The `register-enable='mu'` part, allows the registration of accounts, using a standard jabber client.

Also set your server on `sm.xml`:

 `/etc/jabberd/sm.xml` 

```
<id>mymachine.com</id>

```

### Daemon

Configure the `jabberd.service` to start on boot.

Read [Daemons](/index.php/Daemons "Daemons") for more information.

## See also

*   [Jabberd2 homepage](http://jabberd2.org/)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Jabberd2&oldid=414789](https://wiki.archlinux.org/index.php?title=Jabberd2&oldid=414789)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Internet applications](/index.php/Category:Internet_applications "Category:Internet applications")

Hidden category:

*   [Pages with broken package links](/index.php/Category:Pages_with_broken_package_links "Category:Pages with broken package links")