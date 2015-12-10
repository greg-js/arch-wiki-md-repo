# File Sharing with Webdav and DNSSD

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

**This article or section is out of date.**

**Reason:** There is no rc.conf nor dbus-core anymore. (Discuss in [Talk:File Sharing with Webdav and DNSSD#](https://wiki.archlinux.org/index.php/Talk:File_Sharing_with_Webdav_and_DNSSD))

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**This article or section is a candidate for merging with [WebDAV](/index.php/WebDAV "WebDAV").**

**Notes:** please use the second argument of the template to provide more detailed indications. (Discuss in [Talk:File Sharing with Webdav and DNSSD#](https://wiki.archlinux.org/index.php/Talk:File_Sharing_with_Webdav_and_DNSSD))

Say you need a location that you can use to store things: eg music, photos, books etc. Say you want Nautilus and other file managers to find this automatically. You could use [Samba](/index.php/Samba "Samba") or you could do the following which uses webdav and dnssd on a server.

## Install the required packages

```
pacman -S apache mod_dnssd avahi dbus-core

```

Edit /etc/rc.conf and add "avahi-daemon" and "dbus" to the daemons line.

Follow the configuration instructions for [apache](/index.php/Apache "Apache") to where you test if it is running. Once it is working continue.

## Configure the repositories

1) Create one or more directories - one for each repository eg:

*   /home/music
*   /home/photos
*   /home/books

Add another directory for the webdav locks:

*   /home/DavLock

They can be anywhere but the instructions below will assume they follow the above. Note it is a good idea to keep the repositories together so that it is easy to back them up.

2) change the ownership to http and permissions so apache can access them:

```
chown -R http:http /home/music
chmod -R 700 /home/music

```

**Edit /etc/httpd/conf/httpd.conf**

3) add the following outside any declaration block:

```
DNSSDEnable On
DNSSDAutoRegisterVHosts On
DavLockDB /home/DavLock

```

4) Load the mod_dnssd module: add the following with all the other load module lines:

```
LoadModule dnssd_module modules/mod_dnssd.so

```

5) at the bottom of the file create a virtual host block

```
<VirtualHost *:80>

```

```
</VirtualHost>

```

_For some reason the I could only get the mod_dnssd module to work as part of a virtual host block. This was the case with both Ubuntu and also Arch._

6) In between the virtual host tags create a section for each repository as follows

```
<Directory /home/music>
  Options indexes Multiviews
  AllowOverride None
  Order allow,deny
  allow from all
</Directory>

```

```
Alias /music "/home/music"
<Location /music>
  Dav On
  DNSSDServiceName "Music Repository"
  DNSSDServiceTypes _webdav._tcp
  DNSSDServiceTxtRecord "path=/music"
  DNSSDServiceTxtRecord "u=Korah"
</Location>

```

*   The directory block is pretty standard for no security and browsing of the directory. Check [apache](/index.php/Apache "Apache") documentation for alternatives.
*   The Alias statement is also pretty standard it links the url ending in /music to the directory /home/music
*   The Location block sets up webdav to share the directory and DNSSD so that things like nautilus and avahi-discover can find it.
    *   Dav On enables webdav on this location
    *   DNSSDServiceName has the string that will be displayed in things like Nautilus for this service so the user will see "Music Repository" under Browse Network.
    *   DNSSDServiceTypes are the service types we are broadcasting. If you want them to be aware of these directories as web folders browsable by a web browser add "_http._tcp" with a space between them.

```
DNSSDServiceTypes _webdav._tcp _http._tcp

```

*   *   DNSSDServiceTxtRecord "path=/music" this is the part of the URL after the fully qualified domain name. It is required for the service to be correctly broadcast and shared
    *   DNSSDServiceTxtRecord "u=Korah". This specifies the username. I used my server name but "Anon" also works but it must be included to work. Otherwise when you click on the icon in nautilus it will not mount. The only other txt record that is defined for webdav is "p" for password but I did not need to use that.

Repeat this block for each repository you are setting up.

7) Add the fully qualified server name to the virtual host block. If you do not have a domain:

```
ServerName korah.local

```

if you do:

```
ServerName korah.home.singlespoon.org.au

```

_If you do not add a fully qualified domain name via the ServerName directive then the setup will fail with the error: "[error] avahi_entry_group_add_service_strlst("<service name>") failed: Invalid host name" in the apache logs_

Save the file and exit your editor.

### Test that it is all working

1) Ensure that dbus and avahi are running

```
/etc/rc.d/dbus start
/etc/rc.d/avahi-daemon start

```

2) Ensure that apache is running with the current configuration

```
/etc/rc.d/httpd restart

```

3) Install dbus and the avahi-daemon on a workstation/desktop somewhere.

```
pacman -S dbus avahi

```

4) Start them:

```
/etc/rc.d/dbus start
/etc/rc.d/avahi-daemon start

```

5) Check that the services are discoverable:

```
avahi-discover

```

You should be able to see various entries to do with your server. Look for webdav shares. If you click on the ones you have created it will show you the parameters you set up.

7) Open Nautilus and browse the network. You should see the shares you have created. Click on them and they should mount.

Retrieved from "[https://wiki.archlinux.org/index.php?title=File_Sharing_with_Webdav_and_DNSSD&oldid=397007](https://wiki.archlinux.org/index.php?title=File_Sharing_with_Webdav_and_DNSSD&oldid=397007)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Network sharing](/index.php/Category:Network_sharing "Category:Network sharing")