# Web application package guidelines

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

**The factual accuracy of this article or section is disputed.**

**Reason:** Symlinking part of webapps causes major issues. Furthermore the file system layout is insufficient for more than one instance of a webapp. (Discuss in [Talk:Web application package guidelines#](https://wiki.archlinux.org/index.php/Talk:Web_application_package_guidelines))

**[Package creation guidelines](/index.php/Creating_packages "Creating packages")**

* * *

[CLR](/index.php/CLR_package_guidelines "CLR package guidelines") – [Cross](/index.php/Cross-compiling_tools_package_guidelines "Cross-compiling tools package guidelines") – [Eclipse](/index.php/Eclipse_plugin_package_guidelines "Eclipse plugin package guidelines") – [Free Pascal](/index.php/Free_Pascal_package_guidelines "Free Pascal package guidelines") – [GNOME](/index.php/GNOME_package_guidelines "GNOME package guidelines") – [Go](/index.php/Go_package_guidelines "Go package guidelines") – [Haskell](/index.php/Haskell_package_guidelines "Haskell package guidelines") – [Java](/index.php/Java_package_guidelines "Java package guidelines") – [KDE](/index.php/KDE_package_guidelines "KDE package guidelines") – [Kernel](/index.php/Kernel_module_package_guidelines "Kernel module package guidelines") – [Lisp](/index.php/Lisp_package_guidelines "Lisp package guidelines") – [MinGW](/index.php/MinGW_package_guidelines "MinGW package guidelines") – [Nonfree](/index.php/Nonfree_applications_package_guidelines "Nonfree applications package guidelines") – [OCaml](/index.php/OCaml_package_guidelines "OCaml package guidelines") – [Perl](/index.php/Perl_package_guidelines "Perl package guidelines") – [PHP](/index.php/PHP_package_guidelines "PHP package guidelines") – [Python](/index.php/Python_package_guidelines "Python package guidelines") – [Ruby](/index.php/Ruby_Gem_package_guidelines "Ruby Gem package guidelines") – [VCS](/index.php/VCS_package_guidelines "VCS package guidelines") – **Web** – [Wine](/index.php/Wine_package_guidelines "Wine package guidelines")

This page describes how to package web application which tends to install into `/srv/http` (for example packages written in php, such as [phpmyadmin](https://www.archlinux.org/packages/?name=phpmyadmin) and [phpvirtualbox](https://www.archlinux.org/packages/?name=phpvirtualbox)).

## Contents

*   [1 Directory structure](#Directory_structure)
*   [2 Install web application package](#Install_web_application_package)
    *   [2.1 Install with Apache](#Install_with_Apache)
    *   [2.2 Install with Nginx](#Install_with_Nginx)

## Directory structure

Layout example:

*   `/etc/webapps/_$pkgname_`
*   `/usr/share/webapps/_$pkgname_`
*   `/var/...` (according to generic FHS conventions)

`/usr/share/webapps/_$pkgname_` files and/or directories should be symlinked into `/var` and `/etc/`.

`/etc/webapps/_$pkgname_` should contain some examples which helps to setup web-server to run this web application:

*   `/etc/webapps/_$pkgname_/apache.example.conf`
*   `/etc/webapps/_$pkgname_/nginx.example.conf`
*   `/etc/webapps/_$pkgname_/other-web-server.example.conf`

## Install web application package

### Install with Apache

Install package

```
   # install 'foo' package
   # cp /etc/webapps/foo/apache.example.conf /etc/httpd/conf/extra/foo.conf
   # edit /etc/httpd/conf/httpd.conf
      Include conf/extra/foo.conf

```

Start server

```
   # systemctl start httpd

```

### Install with Nginx

Install package

```
   # install 'foo' package
   # ln -s /usr/share/webapps/foo /srv/http
   # cp /etc/webapps/foo/nginx.example.conf /etc/nginx/extra/foo.conf # conf file may be not present.

```

You may need configure [FastCGI-PHP](/index.php/Nginx#PHP_implementation "Nginx"), [FastCGI-CGI](/index.php/Nginx#CGI_implementation "Nginx")

Start server

```
   # systemctl start <fastcgi>
   # systemctl start nginx

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=Web_application_package_guidelines&oldid=372762](https://wiki.archlinux.org/index.php?title=Web_application_package_guidelines&oldid=372762)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Package development](/index.php/Category:Package_development "Category:Package development")

Hidden category:

*   [Pages or sections flagged with Template:Accuracy](/index.php/Category:Pages_or_sections_flagged_with_Template:Accuracy "Category:Pages or sections flagged with Template:Accuracy")