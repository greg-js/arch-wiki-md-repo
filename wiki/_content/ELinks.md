# ELinks

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[ELinks](http://elinks.or.cz/) is an advanced and well-established feature-rich text mode web (HTTP/FTP/...) browser. ELinks can render both frames and tables, is highly customizable and can be extended via Lua or Guile scripts. It features tabs and some support for CSS.

## Contents

*   [1 Installing](#Installing)
*   [2 Basic Usage](#Basic_Usage)
    *   [2.1 Navigation](#Navigation)
*   [3 Configuration](#Configuration)
*   [4 Tips](#Tips)
    *   [4.1 Defining URL-handlers](#Defining_URL-handlers)
    *   [4.2 Using ELinks with Tor](#Using_ELinks_with_Tor)
    *   [4.3 Passing URL's to external commands](#Passing_URL.27s_to_external_commands)
        *   [4.3.1 Saving link to the X clipboard](#Saving_link_to_the_X_clipboard)
        *   [4.3.2 Passing YouTube-links through external player](#Passing_YouTube-links_through_external_player)
*   [5 Troubleshoot](#Troubleshoot)
    *   [5.1 ELinks froze and I can't start it without it freezing again](#ELinks_froze_and_I_can.27t_start_it_without_it_freezing_again)
*   [6 See Also](#See_Also)

## Installing

[elinks](https://www.archlinux.org/packages/?name=elinks) is available from the official repositories.

## Basic Usage

Start elinks with

```
$ elinks

```

or, if you want to start a specific website:

```
$ elinks foo.bar.org

```

### Navigation

Navigating the web with a text browser is more or less the same as a graphical browser, just without the 'distractions'. Once you've started _elinks_, you can press **g** and type in the web page you would like to request. Then you can navigate the page using arrow keys to navigate by line, the space bar to navigate by page, or the **j**, **k** keys to navigate by link.

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** Basic scripting and CSS. (Discuss in [Talk:ELinks#](https://wiki.archlinux.org/index.php/Talk:ELinks))

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** automation and boting. (Discuss in [Talk:ELinks#](https://wiki.archlinux.org/index.php/Talk:ELinks))

## Configuration

Almost everything in ELinks can be configured to suit your fancy.

ELinks provides to two menus, accessable through ELinks, to customize options and keybinds respectivly.

It is recommened to use these tools as opposed to hand-editing the config files (which are placed in ~/.elinks) It is both much easier and safer this way.

By default, access to the option manager is through the **o** key and access to the keybind-manager is through the **k** key.

**Note:** The organization of the option-manager is not always obvious and takes a bit of memorization to use efficiently once you eventually find what you were looking for

## Tips

### Defining URL-handlers

ELinks is capable of using external programs for various tasks,

Defining URL-handlers through the option menu can be a little confusing at first, but once you get it, its fine.

To do this, go into the option manager and navigate to **MIME**. All the submenus have **I**nfo pages to help you.

This is one of the few cases where it might be easier just to edit the conf file.

For example, to get ELinks to automatically launch your image-viewer when you click on a jpeg file, you can add the following to your ~/.elinks/elinks.conf file,

 `~/.elinks/elinks.conf` 

```
set mime.extension.jpg="image/jpeg"
set mime.extension.jpeg="image/jpeg"
set mime.extension.png="image/png"
set mime.extension.gif="image/gif"
set mime.extension.bmp="image/bmp"

set mime.handler.image_viewer.unix.ask = 1
set mime.handler.image_viewer.unix-xwin.ask = 0

set mime.handler.image_viewer.unix.block = 1
set mime.handler.image_viewer.unix-xwin.block = 0 

set mime.handler.image_viewer.unix.program = "ADDYOURTERMINALPICTUREVIEWERHERE %"
set mime.handler.image_viewer.unix-xwin.program = "ADDYOURXPICTUREVIEWERHERE %"

set mime.type.image.jpg = "image_viewer"
set mime.type.image.jpeg = "image_viewer"
set mime.type.image.png = "image_viewer"
set mime.type.image.gif = "image_viewer"
set mime.type.image.bmp = "image_viewer"
```

### Using ELinks with [Tor](/index.php/Tor "Tor")

ELinks does not support SOCKS directly, so alternatives are to either invoke ELinks thus `torify elinks` or install [privoxy](https://www.archlinux.org/packages/?name=privoxy) from the [official repositories](/index.php/Official_repositories "Official repositories") and use it for forwarding to Tor's SOCKS proxy, first by adding the following line to your `/etc/privoxy/config`:

```
forward-socks5 / localhost:9050 .

```

Restart `privoxy.service` and then entering the following lines to your `~/.elinks/elinks.conf`:

```
set protocol.http.proxy.host = "127.0.0.1:8118"
set protocol.https.proxy.host = "127.0.0.1:8118"

```

**Note:** The above assumes that _Tor_ is using port **9050** and that _privoxy_ is listening on port **8118**

### Passing URL's to external commands

You can define commands which ELinks will pass the the current URL to.

To do this, go into the options menu, navigate under **Document**, then to **URI-passing**. Then press **A** to add a new command name. Then navigate to the new command name and press **E** to edit. Type in the name of command, enter and save.

Assuming the command "tab-external-command" is mapped to **KEY**, whenever you press **KEY**, a menu containing your commands will appear. Select the one you want, and ELinks passes the current URL to that command

**Note:** Elinks allows you to define your own mappings for navigating this menu

Here are some useful commands to get you started...

#### Saving link to the X clipboard

```
echo -n %c | xclip -i 

```

#### Passing YouTube-links through external player

For strictly YouTube-links, [mpv](https://www.archlinux.org/packages/?name=mpv) has built-in support. Just use the following,

```
mpv %c 

```

For a more general approach that can handle many 'tube' sites, you will need [youtube-dl](https://www.archlinux.org/packages/?name=youtube-dl). Then add the following command,

```
youtube-dl -o - %c | mplayer - 

```

I used [mplayer](https://www.archlinux.org/packages/?name=mplayer) because i couldn't get it to work with mpv. Anyway, this is not as nice as mpv's support for YouTube links. Mpv gives you full control of position in the stream which is wonderful!

## Troubleshoot

### ELinks froze and I can't start it without it freezing again

By default, every time you start ELinks you are connecting to an existing instance. Thus, if that instance freezes, all current and future instances will freeze as well.

You can prevent ELinks from connecting to an existing instance by starting it like so

```
elinks -no-connect

```

If this happens a lot, you might consider making this your default startup by making an alias in your shell

```
alias elinks="elinks -no-connect"

```

## See Also

*   [Official web site](http://elinks.or.cz/)
*   [Howto: Use elinks like a pro](http://kmandla.wordpress.com/2007/05/06/howto-use-elinks-like-a-pro/)

Retrieved from "[https://wiki.archlinux.org/index.php?title=ELinks&oldid=405790](https://wiki.archlinux.org/index.php?title=ELinks&oldid=405790)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Web browser](/index.php/Category:Web_browser "Category:Web browser")

Hidden category:

*   [Pages or sections flagged with Template:Expansion](/index.php/Category:Pages_or_sections_flagged_with_Template:Expansion "Category:Pages or sections flagged with Template:Expansion")