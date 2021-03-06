Related articles

*   [Mastodon](/index.php/Mastodon "Mastodon")

[Diaspora](https://www.diasporafoundation.org/) is the privacy aware, personally controlled, do-it-all, open source social network.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Prerequisites](#Prerequisites)
*   [2 Installation](#Installation)
*   [3 Updating](#Updating)
*   [4 Add yourself as an admin](#Add_yourself_as_an_admin)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 GDM login screen with Diaspora](#GDM_login_screen_with_Diaspora)
*   [6 See also](#See_also)

## Prerequisites

*   Since Diaspora can run on [MySQL](/index.php/MySQL "MySQL") and [PostgreSQL](/index.php/PostgreSQL "PostgreSQL") you need to decide which one you want to use. Install one of them and set it up.
*   Diaspora starts a so called appserver, on port 3000 by default, which serves the dynamic contents. You need a reverse proxy to handle the static content and that forwards requests it can't handle to the appserver. Typical tools for that are [Apache](/index.php/Apache "Apache") or [Nginx](/index.php/Nginx "Nginx").
*   You'll also need the usual tools to build packages from the AUR.
*   And [ruby2.2](https://aur.archlinux.org/packages/ruby2.2/) and [ruby2.2-bundler](https://aur.archlinux.org/packages/ruby2.2-bundler/) from the AUR.

## Installation

Install [diaspora-mysql](https://aur.archlinux.org/packages/diaspora-mysql/) or [diaspora-postgresql](https://aur.archlinux.org/packages/diaspora-postgresql/) from the AUR.

Now edit `/etc/webapps/diaspora/database.yml` and fill out the needed values. Then edit `/etc/webapps/diaspora/diaspora.yml` and change at least the url setting to the URL your installation will be reachable under (the one served by your reverse proxy). You can change the port the appserver will listen on under the server section. By default Diaspora requires a SSL setup, you can disable that with the require_ssl setting.

Ensure your database is running and then switch to the diaspora user:

```
$ su - diaspora

```

Create the database and initialize the schema:

```
$ bin/bundle exec rake db:create db:migrate

```

If the user you specified in the database.yml file can't create databases leave the 'db:create' out and create a database named diaspora_production by hand.

You can now switch back to your regular user and start **diaspora** [systemd](/index.php/Systemd "Systemd") service.

The static content your reverse proxy needs to serve will be available under `/usr/share/webapps/diaspora/public/`

## Updating

Updating is very analogous. Obtain the newest version of the package and build it, just like in the installation instructions. Watch for .pacnew files and review the changes. Also read the [changelog](https://github.com/diaspora/diaspora/blob/master/Changelog.md) over at Diaspora. Then again ensure the database is running and switch to the diaspora user:

```
 $ su - diaspora

```

And update the database schema:

```
 $ RAILS_ENV=production bin/bundle exec rake db:migrate

```

Exit and restart **diaspora** systemd service.

If you notice [missing icons or layout issues](https://wiki.diasporafoundation.org/FAQ_for_pod_maintainers#I_installed_diaspora.2A_on_my_machine.2C_but_when_I_load_the_site_there_are_no_images_and_the_layout_looks_horrible.21) after restarting the service, switch to the diaspora user again and run:

```
 $ RAILS_ENV=production bin/bundle exec rake assets:precompile

```

Once more, exit and restart **diaspora** systemd service.

## Add yourself as an admin

Switch to the diaspora user and start the Rails console:

```
 $ su - diaspora
 $ bin/bundle exec rails console production

```

Then run the following command, replacing *user* with your username (only lowercase characters):

```
 Role.add_admin User.where(username: "user").first.person

```

You can exit the Rails console by pressing `Ctrl+d`.

## Troubleshooting

### GDM login screen with Diaspora

GDM will insert the user diaspora in its login window because it currently considers the id range 500-1000 as normal users while Arch considers this range for system users as defined in /etc/login.defs. GDM does that probably to keep legacy normal users working. To exclude this user from the login window, add this 'Exclude' line in your `/etc/gdm/custom.conf` file:

```
[greeter]
Exclude=diaspora

```

## See also

*   [https://github.com/diaspora/diaspora](https://github.com/diaspora/diaspora)