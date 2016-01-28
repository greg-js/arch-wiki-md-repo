# Gallery2

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-document-new.png](/images/f/f0/Tango-document-new.png)](/index.php/File:Tango-document-new.png)

[![Tango-document-new.png](/images/f/f0/Tango-document-new.png)](/index.php/File:Tango-document-new.png)

**This article is a stub.**

**Notes:** please use the first argument of the template to provide more detailed indications. (Discuss in [Talk:Gallery2#](https://wiki.archlinux.org/index.php/Talk:Gallery2))

**Tip:** There is currently a [newer version](http://gallery.menalto.com/) of Gallery available.

Gallery2 gives you an intuitive way to blend photo management seamlessly into your own website or simply use your site as a standalone photo gallery.

See the [LAMP](/index.php/LAMP "LAMP") page for how to install and configure an Apache server with PHP and MySQL. Then, install the dependencies. The [php-gd](https://www.archlinux.org/packages/?name=php-gd), [imagemagick](https://www.archlinux.org/packages/?name=imagemagick), and [ffmpeg](https://www.archlinux.org/packages/?name=ffmpeg) packages are available in the repositories, while the jpegtran command is provided by [libjpeg-turbo](https://www.archlinux.org/packages/?name=libjpeg-turbo) package from the [official repositories](/index.php/Official_repositories "Official repositories").

```
pacman -S php-gd imagemagick ffmpeg

```

Next, download the source code for Gallery2\.

```
cd /tmp
wget http://downloads.sourceforge.net/gallery/gallery-2.3.2-full.tar.gz
tar xzf gallery-2.3.2-full.tar.gz
sudo mv gallery2 /usr/share/webapps/

```

Edit `/etc/httpd/conf/extra/httpd-gallery2.conf` and add the following lines:

```
Alias /gallery2 "/usr/share/webapps/gallery2"
<Directory "/usr/share/webapps/gallery2">
    AllowOverride All
    Options FollowSymlinks
    Order allow,deny
    Allow from all
</Directory>

```

Then, edit `/etc/httpd/conf/httpd.conf` and add:

```
Include conf/extra/httpd-gallery2.conf

```

Restart the Apache server with

```
 sudo /etc/rc.d/httpd restart

```

Once installation is complete, verify your ability to write to Gallery's location on the server.

```
sudo echo "RANDOM KEY" >> /usr/share/webapps/gallery2/login.txt

```

If you want maintenance to work, install the Statistics plugin:

```
Set "Themes" and "Modules" folder to 755.
Go to "Site Admin" --> "Plugins" --> "Get More Plugins"
Then click "Update Plugin List"
Install "Statistics" and other plugins that you had installed before upgrading.

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=Gallery2&oldid=394160](https://wiki.archlinux.org/index.php?title=Gallery2&oldid=394160)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Image manipulation](/index.php/Category:Image_manipulation "Category:Image manipulation")
*   [Web server](/index.php/Category:Web_server "Category:Web server")

Hidden category:

*   [Pages flagged with Template:Stub](/index.php/Category:Pages_flagged_with_Template:Stub "Category:Pages flagged with Template:Stub")