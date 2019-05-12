[YOURLS](https://yourls.org/) is a self-hosted link shortener service written in PHP.

# Installation

[Install](/index.php/Install "Install") the [yourls](https://aur.archlinux.org/packages/yourls/) package.

# Setup

A [MySQL](/index.php/MySQL "MySQL") database and user are required, to complete the config file at `/etc/webapps/yourls/config.php`.

In the same config file, set the `YOURLS_SITE` to either your short domain `[http://example.org](http://example.org)` or a subfolder `[http://example.org/s](http://example.org/s)`, but always without the trailing `/`.

Set a random cookie key, for example using `pwgen 50 1` and a user/password combo for the admin user. You can write the hash or the plain-text, but in the latter case the [web server](/index.php/Web_server "Web server") needs `rw` permissions to be able to hash it.