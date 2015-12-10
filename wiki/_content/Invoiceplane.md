# Invoiceplane

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-document-new.png](/images/f/f0/Tango-document-new.png)](/index.php/File:Tango-document-new.png)

[![Tango-document-new.png](/images/f/f0/Tango-document-new.png)](/index.php/File:Tango-document-new.png)

**This article is a stub.**

**Notes:** please use the first argument of the template to provide more detailed indications. (Discuss in [Talk:Invoiceplane#](https://wiki.archlinux.org/index.php/Talk:Invoiceplane))

[InvoicePlane](http://invoiceplane.com) is a self-hosted open source application for managing your quotes, invoices, clients and payments.

## Installation

Install [invoiceplane](https://aur.archlinux.org/packages/invoiceplane/)<sup><small>AUR</small></sup> from the [AUR](/index.php/AUR "AUR").

[![Tango-user-trash-full.png](/images/e/ee/Tango-user-trash-full.png)](/index.php/File:Tango-user-trash-full.png)

[![Tango-user-trash-full.png](/images/e/ee/Tango-user-trash-full.png)](/index.php/File:Tango-user-trash-full.png)

**This article or section is being considered for deletion.**

**Reason:** This belongs in the PKGBUILD (opt-depends, .install) (Discuss in [Talk:Invoiceplane#](https://wiki.archlinux.org/index.php/Talk:Invoiceplane))

If you want to choose a different language than English you should also install [invoiceplane-translations](https://aur.archlinux.org/packages/invoiceplane-translations/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/invoiceplane-translations)]</sup>. Further you will need a database (e.g. [MariaDB](/index.php/MariaDB "MariaDB")), a web server (like [Nginx](/index.php/Nginx "Nginx")) with php-support. You may refer following sites:

*   [Apache](/index.php/Apache "Apache")
*   [Lighttpd](/index.php/Lighttpd "Lighttpd")
*   [Nginx](/index.php/Nginx "Nginx")

Write permissions have to be granted before proceeding with the installation:

```
chown -R http:http /usr/share/webapps/invoiceplane

```

## Configuration

Here's an example on how you could setup a database for Invoiceplane with [MariaDB](/index.php/MariaDB "MariaDB") called `invoiceplane` for the user `invoiceplane` identified by the password `password`:

```
CREATE DATABASE invoiceplane;
GRANT ALL PRIVILEGES ON invoiceplane.* TO invoiceplane@'localhost' IDENTIFIED BY 'password';
FLUSH PRIVILEGES;

```

Visit the installation wizard page at [http://127.0.0.1/invoiceplane/setup](http://127.0.0.1/invoiceplane/setup) and follow the instructions.

## See also

*   [Offical web page](http://invoiceplane.com)
*   [Documentation](https://github.com/InvoicePlane/InvoicePlane/wiki)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Invoiceplane&oldid=392279](https://wiki.archlinux.org/index.php?title=Invoiceplane&oldid=392279)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Office](/index.php/Category:Office "Category:Office")