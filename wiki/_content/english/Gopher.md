[Gopher](https://en.wikipedia.org/wiki/Gopher_(protocol) is a protocol for information transfer over the internet that was very popular before HTTP took over as the dominant protocol, but there is still a community of gopher users that prefer the simplicity of the protocol over the more complex and large protocols more often encountered. Note that not all browsers support gopher, or have incomplete support.

## Contents

*   [1 GoFish server](#GoFish_server)
    *   [1.1 Installation](#Installation)
    *   [1.2 Configuration](#Configuration)
    *   [1.3 .cache](#.cache)
*   [2 Gopher Browser](#Gopher_Browser)
*   [3 Overbite for Firefox](#Overbite_for_Firefox)
*   [4 HTTP access via Gopher proxy](#HTTP_access_via_Gopher_proxy)
*   [5 See also](#See_also)

## GoFish server

[GoFish](http://gofish.sourceforge.net/) is a basic gopher server that allows you to run your own gopherspace. The setup is somewhat like other servers, but generally requires less resources to function.

### Installation

[Install](/index.php/Install "Install") the [gofish](https://aur.archlinux.org/packages/gofish/) package.

### Configuration

There are some basic settings for the server you can change in the `/etc/gofish.conf` file, but the defaults will work. If you do not alter any settings, the root of the gopher server will be `/var/gopher` and it will run on port 70\. (Note that Firefox can only use the gopher protocol on port 70, so changing it will mean your users must use some other client.)

To run the server, [start](/index.php/Start "Start") `gofish.service`.

You can now connect to your server and see what you have by navigating to [gopher://127.0.0.1](gopher://127.0.0.1)

### .cache

Unlike FTP which automatically shows all files, gopher relies on a file called `.cache` in each directory to determine how the page will be shown to the end user. Although GoFish comes with the dotcache(5) man page for the `.cache` files, it can be a little confusing. GoFish also comes with a program to autogenerate `.cache` files for all the directories and files in your server root.

```
mkcache -r

```

This will create all the needed `.cache` files recursively, but you may want to edit some names. A sample `.cache` file will look something like this:

```
iHello         none            example.com     70
0ReadMe	0/ReadMe.txt	example.com	70
1Ebooks	1/ebooks	example.com	70

```

The gopher protocol uses number prefixes to describe filetype. `0` is a plain text file, `1` is a directory and `9` is a binary file. The `i` indicates an image, and if it is linked to `none`, it will show up as plain text. This is good for introducing your site. See the dotcache(5) man page for more info on the prefixes. After the prefix number is the name that will appear in the client, and it does not need to be the same as the file it links to. In the second section, we see the "path" to the file. There is not a directory named `0` or `1` in the file system, it is only added in the URI to let the gopher server and end user know what sort of file it is. The third section is whatever domain name the site is, and the fourth is the port it is on, default is 70\. The space between each of the 4 sections must be a tab, not a space or it will not be parsed correctly.

Now let's look at the `.cache` file in the ebooks directory.

```
9Book 1	9/ebooks/Book1.chm	example.com	70
9Book 2	9/ebooks/Book2.pdf	example.com	70

```

Notice that the URI is `9/ebooks/Book1.chm`, NOT `1/ebooks/9Book1.chm` . There is always only one prefix number for the last item in the URI. Also notice that a chm file nor a pdf file is really a binary, but it is still given the prefix of `9`. In the GoFish server, any file that is not a text file or a directory is given the binary prefix. Remember that if there are files within your server's root, people can download or view them even if they are not in your `.cache` file, so be careful.

## Gopher Browser

To browse gopherspace as it was originally intended to be browsed, you can install the University of Minnesota gopher browser with the [gopher](https://aur.archlinux.org/packages/gopher/) package.

## Overbite for Firefox

[The Overbite Project](https://gopher.floodgap.com/overbite/) enables gopherspace in some browsers and devices, including Mozilla Firefox. Check [firefox-extension-overbitenx](https://aur.archlinux.org/packages/firefox-extension-overbitenx/) or [overbitewx](https://addons.mozilla.org/en-US/firefox/addon/overbitewx/) add-on.

**Note:** OverbiteNX and OverbiteWX are successors of the previous Firefox addon OverbiteFF, as noted in these extensions' websites.

## HTTP access via Gopher proxy

You can use [http://gopher.floodgap.com/gopher/gw](http://gopher.floodgap.com/gopher/gw) to browse the Gopher network via HTTP, e.g. using a browser not Gopher-enabled.

## See also

*   [GoFish Homepage](http://gofish.sourceforge.net/)
*   [Example of Gopher websites](http://gopher.floodgap.com/gopher/gw?gopher/1/new)