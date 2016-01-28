# ASP.NET with Apache

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**This article or section is a candidate for merging with [Apache](/index.php/Apache "Apache").**

**Notes:** please use the second argument of the template to provide more detailed indications. (Discuss in [Talk:ASP.NET with Apache#](https://wiki.archlinux.org/index.php/Talk:ASP.NET_with_Apache))

Describes how to show ASP.NET-sites under [Apache](/index.php/Apache "Apache") by using Mod_Mono.

From [Mod_Mono's site](http://www.mono-project.com/Mod_mono):

"_Mod_Mono is an Apache 2.0/2.2 module that provides ASP.NET support for the web's favorite server, Apache ([http://httpd.apache.org/](http://httpd.apache.org/))._"

## Contents

*   [1 Installing](#Installing)
*   [2 Configuring](#Configuring)
    *   [2.1 AutoHosting](#AutoHosting)
*   [3 Testing](#Testing)

## Installing

The setup requires [mono](https://www.archlinux.org/packages/?name=mono) and [mod_mono](https://www.archlinux.org/packages/?name=mod_mono) for Apache compliance. Package [xsp](https://www.archlinux.org/packages/?name=xsp) is a simple webserver for ASP.NET, optionally installed for testing the configuration.

## Configuring

Edit `/etc/httpd/conf/httpd.conf` and add the following line:

```
 Include /etc/httpd/conf/extra/mod_mono.conf

```

Finally, restart apache with:

```
 systemctl restart httpd.service

```

Now, Apache should be able to show ASP.NET-pages.

### AutoHosting

_Further details: [http://www.mono-project.com/AutoHosting](http://www.mono-project.com/AutoHosting)_

With this setting, configuring apache for each deployment is no longer needed; just place the application in any directory within html-root and it will be promptly auto-configured. Add the following lines to `/etc/httpd/conf/httpd.conf` to enable the option:

```
 # Choose ASP2.0 support instead of the default 1.0
 MonoServerPath "/usr/bin/mod-mono-server4" # mono 4
 MonoAutoApplication enabled

```

## Testing

If xsp is installed and html-path is `/httpd/html`, then open a browser and access [http://server/xsp/](http://server/xsp/) to see an overview over the ASP.NET-testfiles.

Retrieved from "[https://wiki.archlinux.org/index.php?title=ASP.NET_with_Apache&oldid=398529](https://wiki.archlinux.org/index.php?title=ASP.NET_with_Apache&oldid=398529)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Web server](/index.php/Category:Web_server "Category:Web server")

Hidden category:

*   [Pages or sections flagged with Template:Merge](/index.php/Category:Pages_or_sections_flagged_with_Template:Merge "Category:Pages or sections flagged with Template:Merge")