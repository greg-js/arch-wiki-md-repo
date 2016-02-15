[InvoicePlane](http://invoiceplane.com) is a self-hosted open source application for managing your quotes, invoices, clients and payments.

## Installation

Install [invoiceplane](https://aur.archlinux.org/packages/invoiceplane/) from the [AUR](/index.php/AUR "AUR").

If you want to choose a different language than English you should also install [invoiceplane-translations](https://aur.archlinux.org/packages/invoiceplane-translations/). Further you will need a database (e.g. [MariaDB](/index.php/MariaDB "MariaDB")), a web server (like [Nginx](/index.php/Nginx "Nginx")) with php-support. You may refer following sites:

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