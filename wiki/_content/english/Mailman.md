**Mailman** is an application for managing electronic mailing lists. Normally you will use it along a *mail server* and also a *web server* too; for the first you may pick one between [Postfix](/index.php/Postfix "Postfix"), [Exim](/index.php/Exim "Exim"), [Sendmail](/index.php/Sendmail "Sendmail") and Qmail —if you are unsure about which one to use, Postfix is a very good choice—; as for the latter, any web server is useful, common options are [Apache](/index.php/Apache "Apache"), [Lighttpd](/index.php/Lighttpd "Lighttpd") and [Nginx](/index.php/Nginx "Nginx"). (These three pieces do not necessarily have to run on the same computer.)

Only the Mailman installation will be covered in this article. You can refer to the correspondent wiki pages to learn how to install the mail and web servers.

For this guide we are going to suppose that you are using a machine called "arch" and you want to setup mailing lists for the organizations "a", "b" and "c", with example domains "a.org", "b.org" and "c.org" that point to "arch". For each domain,

*   Mailman's **web interface** will be accessible from *lists.[organization_name].org* and
*   the **lists' archives** under *lists.[organization_name].org/archives*.
*   **Lists addresses** will look like *[list_name]@[organization_name].org*.

**A caveat**: you can use a Mailman installation to manage lists for several domains, but two lists cannot have the same name even though its domains are different!

## Contents

*   [1 Mailman installation](#Mailman_installation)
*   [2 Mailman configuration](#Mailman_configuration)
    *   [2.1 Web Server integration](#Web_Server_integration)
    *   [2.2 MTA integration](#MTA_integration)
    *   [2.3 Postfix integration](#Postfix_integration)
    *   [2.4 Exim integration](#Exim_integration)
*   [3 Mail Server Configuration](#Mail_Server_Configuration)
    *   [3.1 Postfix](#Postfix)
    *   [3.2 Exim](#Exim)
*   [4 Web Server Configuration](#Web_Server_Configuration)
    *   [4.1 Nginx](#Nginx)
    *   [4.2 Lighttpd](#Lighttpd)
    *   [4.3 Apache](#Apache)
*   [5 Post configuration](#Post_configuration)
    *   [5.1 Site-wide mailing list](#Site-wide_mailing_list)
    *   [5.2 Set up timers](#Set_up_timers)
    *   [5.3 Start Mailman](#Start_Mailman)
    *   [5.4 Create a password](#Create_a_password)
*   [6 Using Mailman](#Using_Mailman)
*   [7 Mailman 3](#Mailman_3)
*   [8 Troubleshooting](#Troubleshooting)
    *   [8.1 Postfix](#Postfix_2)
    *   [8.2 UTF-8](#UTF-8)
*   [9 See also](#See_also)

## Mailman installation

[Install](/index.php/Install "Install") the [mailman](https://www.archlinux.org/packages/?name=mailman) package.

## Mailman configuration

The full set of configuration defaults lives in the `/usr/lib/mailman/Mailman/Defaults.py` file. However you should never modify this file! Instead, change the **mm_cfg.py** file, `/etc/mailman/mm_cfg.py`. You only need to add values to mm_cfg.py that are different than the defaults in Defaults.py. Future Mailman upgrades are guaranteed never to touch your mm_cfg.py file.

### Web Server integration

```
DEFAULT_URL_HOST = 'lists.a.org'

VIRTUAL_HOSTS.clear()
add_virtualhost(DEFAULT_URL_HOST, DEFAULT_EMAIL_HOST)
add_virtualhost('lists.b.org', 'b.org')
add_virtualhost('lists.c.org', 'c.org')

POSTFIX_STYLE_VIRTUAL_DOMAINS = ['a.org', 'b.org', 'c.org']

DEFAULT_URL_PATTERN = 'http://%s/'
PUBLIC_ARCHIVE_URL = 'http://%(hostname)s/archives/%(listname)s'

```

For Apache make this change from the above:

```
DEFAULT_URL_PATTERN = 'http://%s/lists/'

```

### MTA integration

The content of `/etc/mailman/mm_cfg.py` varies depending on the chosen mail server.

### Postfix integration

```
DEFAULT_EMAIL_HOST = 'a.org'
MTA = 'Postfix'

```

Once you have edited mm_cfg.py, run

```
# /usr/lib/mailman/bin/genaliases

```

to generate an aliases file that Postfix needs.

### Exim integration

```
DEFAULT_EMAIL_HOST = 'a.org'
MTA = None

```

## Mail Server Configuration

*Note*: Ensure your domain name server (DNS) setup. For mail delivery on the internet, your DNS must be correct. An MX record should point to the mail host. More info about DNS is beyond the scope of this document.

### Postfix

For installing and configuring this mail server, see [Postfix](/index.php/Postfix "Postfix"). (If you will be using Postfix just for Mailman, its setup is much simpler: ignore all the *mailbox* and *database* stuff.)

`/etc/postfix/main.cf` should have the following fields and values:

```
myhostname = arch.a.org
mydomain = a.org
myorigin = $mydomain
mydestination = localhost, a.org, b.org, c.org
mynetworks_style = host

alias_maps = hash:/etc/postfix/aliases, hash:/var/lib/mailman/data/aliases
alias_database = $alias_maps
virtual_alias_maps = hash:/etc/postfix/virtual, hash:/var/lib/mailman/data/virtual-mailman

recipient_delimiter = +
```

### Exim

Edit your `/etc/mail/exim.conf` to add entries in the following sections:

In `routers`:

```
local_mailman_list:
    driver = accept
    require_files = /var/lib/mailman/lists/${lc::$local_part}/config.pck
    local_part_suffix = -admin : -bounces : -bounces+* : -confirm : -confirm+* : -join : -leave : -owner : -request : -subscribe : -unsubscribe
    local_part_suffix_optional
    transport = mailman_transport
```

In `transports`:

```
mailman_transport:
    driver = pipe
    user = mailman
    group = mailman
    home_directory = /usr/lib/mailman
    current_directory = /usr/lib/mailman
    command = /usr/lib/mailman/mail/mailman '${if def:local_part_suffix {${sg{$local_part_suffix}{-(\\w+)(\\+.*)?}{\$1}}}{post}}' $local_part
```

## Web Server Configuration

### Nginx

For installing and configuring this web server, see [Nginx](/index.php/Nginx "Nginx"). Mailman web interface relies on CGI processing; this setup uses Nginx along `fcgiwrap`, see [Nginx#fcgiwrap](/index.php/Nginx#fcgiwrap "Nginx").

`/etc/nginx/nginx.conf` should include the following configuration per domain (example for *a.org*):

```
server {
  server_name lists.a.org;
  root /usr/lib/mailman/cgi-bin;

  location = / {
    rewrite ^ /listinfo permanent;
  }

  location / {
    fastcgi_split_path_info ^(/[^/]*)(.*)$;
    fastcgi_pass unix:/run/fcgiwrap.sock;
    include fastcgi.conf;
    fastcgi_param PATH_INFO         $fastcgi_path_info;
    fastcgi_param PATH_TRANSLATED   $document_root$fastcgi_path_info;
  }

  location /mailman-icons {
    alias /usr/lib/mailman/icons;
  }

  location /archives {
    alias /var/lib/mailman/archives/public;
    autoindex on;
  }

}
```

**Note:** Nginx must run with `user` http and `group` http or Mailman will complain. Be sure to define the `user` directive in `/etc/nginx/conf/nginx.conf` as follows (outside the `html` block):
```
user http http;

```

### Lighttpd

```
server.modules = ("mod_rewrite",
                  "mod_cgi")

url.rewrite = ( "^/$" => "/listinfo" )
alias.url = (
        "/icons" => "/usr/lib/mailman/icons",
        "/archives" => "/var/lib/mailman/archives/public"
)

cgi.assign = (
        "/usr/lib/mailman/cgi-bin/admin" => "",
        "/usr/lib/mailman/cgi-bin/admin/" => "",
        "/usr/lib/mailman/cgi-bin/admindb" => "",
        "/usr/lib/mailman/cgi-bin/admindb/" => "",
        "/usr/lib/mailman/cgi-bin/confirm" => "",
        "/usr/lib/mailman/cgi-bin/confirm/" => "",
        "/usr/lib/mailman/cgi-bin/create" => "",
        "/usr/lib/mailman/cgi-bin/create/" => "",
        "/usr/lib/mailman/cgi-bin/edithtml" => "",
        "/usr/lib/mailman/cgi-bin/edithtml/" => "",
        "/usr/lib/mailman/cgi-bin/listinfo" => "",
        "/usr/lib/mailman/cgi-bin/listinfo/" => "",
        "/usr/lib/mailman/cgi-bin/options" => "",
        "/usr/lib/mailman/cgi-bin/options/" => "",
        "/usr/lib/mailman/cgi-bin/private" => "",
        "/usr/lib/mailman/cgi-bin/private/" => "",
        "/usr/lib/mailman/cgi-bin/rmlist" => "",
        "/usr/lib/mailman/cgi-bin/rmlist/" => "",
        "/usr/lib/mailman/cgi-bin/roster" => "",
        "/usr/lib/mailman/cgi-bin/roster/" => "",
        "/usr/lib/mailman/cgi-bin/subscribe" => "",
        "/usr/lib/mailman/cgi-bin/subscribe/" => ""
        )

$HTTP["host"] =~ "(^|\.)lists.a.org$" {
        server.document-root            = "/usr/lib/mailman/cgi-bin/"
        server.errorlog                 = "/var/log/lighttpd/lists.a.org_error.log"
        accesslog.filename              = "/var/log/lighttpd/lists.a.org_access.log"
}

```

### Apache

Add following line to your `/etc/mailman/mm_cfg.py`:

`IMAGE_LOGOS = '/mailman-icons/'`

The example use of of creating lists.a.org implies creating a vhost. Consider moving the following config into a vhost definition instead of modifying your global httpd.conf.

Modify your /etc/httpd/conf/httpd.conf with the following snippets added.

```
<IfModule alias_module>
    Alias /mailman-icons/ "/usr/lib/mailman/icons/"
    Alias /archives/ "/var/lib/mailman/archives/public/"
    ScriptAlias /lists/ "/usr/lib/mailman/cgi-bin/"
    ScriptAlias / "/usr/lib/mailman/cgi-bin/listinfo"
</IfModule>

<Directory "/usr/lib/mailman/cgi-bin/">
    AllowOverride None
    Options Indexes FollowSymlinks ExecCGI
    Require all granted
</Directory>

<Directory "/usr/lib/mailman/icons/">
    Require all granted
</Directory>

<Directory "/var/lib/mailman/archives/public/">
    Require all granted
</Directory>

```

Restart httpd [systemd](/index.php/Systemd "Systemd") service.

## Post configuration

### Site-wide mailing list

To create this specific list requested by Mailman for its proper operation (between other things, it is used for password reminders), run:

```
# /usr/lib/mailman/bin/newlist mailman

```

This will create a list called "mailman" under the default domain (*mailman@a.org* in the example). You do not have to do it for the other domains (i.e. *b.org* and *c.org*).

Later you should also subscribe yourself to the site list.

### Set up timers

Several Mailman features occur on a regular schedule, so you must set up [timers](/index.php/Systemd/Timers "Systemd/Timers") to run the right programs at the right time.

```
# cd /usr/lib/systemd/system
# for X in mailman-*.timer ; do systemctl enable $X && systemctl start $X ; done

```

### Start Mailman

Mailman will not start processing and sending emails until the `mailman` daemon is started, and optionally enabled, with [systemctl](/index.php/Systemd#Using_units "Systemd").

If you run into problems, run it more verbose so it can help you troubleshoot:

```
# /usr/lib/mailman/bin/mailmanctl start

```

### Create a password

There are two type of passwords that you can create from the command line. The first is the "general password" which can be used anywhere a password is required in the system. The site password will get you into the administration page for any list, and it can be used to log in as any user.

The second password is a site-wide "list creator" password. You can use this to delegate the ability to create new mailing lists without providing all the privileges of the site password. Of course, the owner of the site password can also create new mailing lists, but the list creator password is limited to just that special role.

To set the general password, use this command:

```
# /usr/lib/mailman/bin/mmsitepass <general-password>

```

To set the list creator password, this:

```
# /usr/lib/mailman/bin/mmsitepass -c <list-creator-password>

```

It is okay not to set a list creator password, but you probably do want a general password.

## Using Mailman

To administrate your lists (create and configure lists, manage users, etcetera) use the web interface; remember that each domain has its own. For example, the URL of organization "a" would be *[http://lists.a.org](http://lists.a.org)*.

Mailman can be also managed by command-line. Example for list creation:

```
# newlist --urlhost=lists.b.org --emailhost=b.org list_name

```

## Mailman 3

Mailman 3 was designed in a modular fashion:

*   [mailman-core](https://aur.archlinux.org/packages/mailman-core/) or [mailman-core-git](https://aur.archlinux.org/packages/mailman-core-git/) provides the core component of mailman.
    **Note:** As of December 2015 *mailman-core* only supports Python 3.4 and crashes using Python 3.5\. Use *mailman-core-git* until Python 3.5 support is added in version 3.1.

*   [python2-django-postorius](https://aur.archlinux.org/packages/python2-django-postorius/) or [python2-django-postorius-git](https://aur.archlinux.org/packages/python2-django-postorius-git/) provides a management interface for Mailman.
*   [python2-django-hyperkitty](https://aur.archlinux.org/packages/python2-django-hyperkitty/) [python2-django-hyperkitty-git](https://aur.archlinux.org/packages/python2-django-hyperkitty-git/) is the interface to the mailing lists' archives.
*   [python-mailmanclient](https://aur.archlinux.org/packages/python-mailmanclient/) and [python2-mailmanclient](https://aur.archlinux.org/packages/python2-mailmanclient/) provide python bindings to Mailman's REST API.
*   [python-mailman-hyperkitty-plugin](https://aur.archlinux.org/packages/python-mailman-hyperkitty-plugin/) is a plugin that is used to forward emails to hyperkitty.

In order to deploy postorius and/or hyperkitty django is needed. [mailman-suite-git](https://aur.archlinux.org/packages/mailman-suite-git/) provides a django project skeleton that can be used to deploy them. It also includes a README.md with instructions on how to deploy postorius and/or hyperkitty.

mailman-core can be configured using `/var/lib/mailman/var/etc/mailman.cfg`. Then [start](/index.php/Start "Start") `mailman.service`.

Refer to the official documentation of the projects for more information.

## Troubleshooting

You should check that your installation has all the correct permissions and group ownerships by running the **check_perms** script:

```
# /usr/lib/mailman/bin/check_perms

```

. If it reports problems, then you can either fix them manually or use the same program to fix them (probably the easiest solution):

```
# /usr/lib/mailman/bin/check_perms -f

```

. Repeat previous steps until no more errors are reported!

### Postfix

Make sure that the files in `/var/lib/mailman/data/`:

*   aliases.db,
*   aliases,
*   virtual-mailman,
*   virtual-mailman.db,

are **user** and **group** owned by *mailman* and that are **group writable**.

### UTF-8

[http://www.divideandconquer.se/2009/08/17/convert-mailman-translation-to-utf-8](http://www.divideandconquer.se/2009/08/17/convert-mailman-translation-to-utf-8).

## See also

*   [GNU Mailman installation manual](http://list.org/mailman-install/index.html)