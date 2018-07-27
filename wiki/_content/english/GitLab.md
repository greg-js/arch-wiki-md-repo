Related articles

*   [Gitolite](/index.php/Gitolite "Gitolite")
*   [Ruby on Rails](/index.php/Ruby_on_Rails "Ruby on Rails")

From [GitLab's homepage](https://about.gitlab.com/):

	GitLab offers git repository management, code reviews, issue tracking, activity feeds and wikis. Enterprises install GitLab on-premise and connect it with LDAP and Active Directory servers for secure authentication and authorization. A single GitLab server can handle more than 25,000 users but it is also possible to create a high availability setup with multiple active servers.

An example live version can be found at [GitLab.com](https://gitlab.com/).

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Preliminary Notes](#Preliminary_Notes)
    *   [2.2 GitLab](#GitLab)
    *   [2.3 Custom port for Unicorn](#Custom_port_for_Unicorn)
    *   [2.4 Secret strings](#Secret_strings)
    *   [2.5 Redis](#Redis)
    *   [2.6 Database backend](#Database_backend)
        *   [2.6.1 MariaDB](#MariaDB)
        *   [2.6.2 PostgreSQL](#PostgreSQL)
    *   [2.7 Firewall](#Firewall)
    *   [2.8 Initialize Gitlab database](#Initialize_Gitlab_database)
    *   [2.9 Adjust modifier bits](#Adjust_modifier_bits)
*   [3 Start and test GitLab](#Start_and_test_GitLab)
*   [4 Upgrade database on updates](#Upgrade_database_on_updates)
*   [5 Advanced Configuration](#Advanced_Configuration)
    *   [5.1 Basic SSH](#Basic_SSH)
    *   [5.2 Custom SSH Connection](#Custom_SSH_Connection)
    *   [5.3 HTTPS/SSL](#HTTPS.2FSSL)
        *   [5.3.1 Change GitLab configs](#Change_GitLab_configs)
        *   [5.3.2 Let's Encrypt](#Let.27s_Encrypt)
    *   [5.4 Web server configuration](#Web_server_configuration)
        *   [5.4.1 Node.js](#Node.js)
        *   [5.4.2 Nginx](#Nginx)
        *   [5.4.3 Apache](#Apache)
    *   [5.5 Gitlab-workhorse](#Gitlab-workhorse)
*   [6 Useful Tips](#Useful_Tips)
    *   [6.1 Hidden options](#Hidden_options)
    *   [6.2 Backup and restore](#Backup_and_restore)
    *   [6.3 Sending mails from Gitlab via SMTP](#Sending_mails_from_Gitlab_via_SMTP)
*   [7 Troubleshooting](#Troubleshooting)
    *   [7.1 HTTPS is not green (gravatar not using https)](#HTTPS_is_not_green_.28gravatar_not_using_https.29)
    *   [7.2 Errors after updating](#Errors_after_updating)
    *   [7.3 Gitlab-Unicorn cannot access non-default repositories directory](#Gitlab-Unicorn_cannot_access_non-default_repositories_directory)
*   [8 See also](#See_also)

## Installation

**Note:** This article covers installing and configuring GitLab without HTTPS at first. If needed, see [#Advanced Configuration](#Advanced_Configuration) to set up SSL.

GitLab requires [Redis](/index.php/Redis "Redis") and a database backend. If you plan to run it on the same machine, first install either [MySQL](/index.php/MySQL "MySQL") or [PostgreSQL](/index.php/PostgreSQL "PostgreSQL").

[Install](/index.php/Install "Install") the [gitlab](https://www.archlinux.org/packages/?name=gitlab) package.

In order to receive mail notifications, a mail server must be installed and configured. See [Category:Mail server](/index.php/Category:Mail_server "Category:Mail server") for details.

## Configuration

### Preliminary Notes

GitLab is composed of multiple components, see the [architecture overview page](https://docs.gitlab.com/ce/development/architecture.html).

The [gitlab](https://www.archlinux.org/packages/?name=gitlab) package installs GitLab's files in a manner that more closely follow standard Linux conventions:

| Description | [GitLab's Official](https://github.com/gitlabhq/gitlabhq/blob/master/doc/install/installation.md) | [gitlab](https://www.archlinux.org/packages/?name=gitlab) |
| Configuration File GitShell | `/home/git/gitlab-shell/config.yml` | `/etc/webapps/gitlab-shell/config.yml` |
| Configuration File GitLab | `/home/git/gitlab/config/gitlab.yml` | `/etc/webapps/gitlab/gitlab.yml` |
| User (Home Directory) | `git` (`/home/git`) | `gitlab` (`/var/lib/gitlab`) |

**Tip:** If you are familiar with the [Arch Build System](/index.php/Arch_Build_System "Arch Build System") you can edit the PKGBUILD and relevant files to change gitlab's home directory to a place of your liking.

### GitLab

Edit `/etc/webapps/gitlab/gitlab.yml` and setup at least the following parameters:

**Note:** The `hostname` and `port` are used for the `git clone [http://hostname:port](http://hostname:port)` as example.

**Hostname:** In the `gitlab:` section set `host:` - replacing `localhost` to `yourdomain.com` (**note:** no '[http://'](http://') or trailing slash) - into your fully qualified domain name.

**Port:** `port:` can be confusing. This is not the port that the gitlab server (unicorn) runs on; it's the port that users will initially access through in their browser. Basically, if you intend for users to visit 'yourdomain.com' in their browser, without appending a port number to the domain name, leave `port:` as `80`. If you intend your users to type something like 'yourdomain.com:3425' into their browsers, then you'd set `port:` to `3425`. You will also have to **configure your webserver** to listen on that port.

**Timezone (optional):** The `time_zone:` parameter is optional, but may be useful to force the zone of GitLab applications.

Finally set the correct [permissions](/index.php/Permissions "Permissions") to the *uploads* directory:

```
# chmod 700 /var/lib/gitlab/uploads

```

### Custom port for Unicorn

GitLab Unicorn is the main component which processes most of the user requests. By default, it listens on the `127.0.0.1:8080` address which can be changed in the `/etc/webapps/gitlab/unicorn.rb` file:

 `/etc/webapps/gitlab/unicorn.rb` 
```
listen "/run/gitlab/gitlab.socket", :backlog => 1024
listen "**127.0.0.1:8080**", :tcp_nopush => true
```

If the Unicorn address is changed, the configuration of other components which communicate with Unicorn have to be updated as well:

*   For GitLab Shell, update the `gitlab_url` variable in `/etc/webapps/gitlab-shell/config.yml`.

**Tip:** According to the comment in the config file, UNIX socket path can be specified with URL-escaped slashes (i.e. `http+unix://%2Frun%2Fgitlab%2Fgitlab.socket` for the default `/run/gitlab/gitlab.socket`). Additionally, un-escaped slashes can be used to specify the [relative URL root](https://docs.gitlab.com/ce/install/relative_url.html) (e.g. `/gitlab`).

*   For GitLab Workhorse, [edit](/index.php/Edit "Edit") the `gitlab-workhorse.service` and update the `-authBackend` option.

### Secret strings

Make sure that the files `/etc/webapps/gitlab/secret` and `/etc/webapps/gitlab-shell/secret` files contain something. Their content should be kept secret because they are used for the generation of authentication tokens etc.

For example, random strings can be generated with the following commands:

```
# hexdump -v -n 64 -e '1/1 "%02x"' /dev/urandom > /etc/webapps/gitlab/secret
# chown root:gitlab /etc/webapps/gitlab/secret
# chmod 640 /etc/webapps/gitlab/secret

```

```
# hexdump -v -n 64 -e '1/1 "%02x"' /dev/urandom > /etc/webapps/gitlab-shell/secret
# chown root:gitlab /etc/webapps/gitlab-shell/secret
# chmod 640 /etc/webapps/gitlab-shell/secret

```

### Redis

In order to provide sufficient performance you will need a cache database. [Install](/index.php/Redis#Installation "Redis") and [configure](/index.php/Redis#Configuration "Redis") a Redis instance, being careful to the section dedicated to listening via a socket.

*   Add the *gitlab* user to the *redis* [group](/index.php/Group "Group").

*   Update the configuration files:

 `/etc/webapps/gitlab/resque.yml` 
```
development: unix:/run/redis/redis.sock
test: unix:/run/redis/redis.sock
production: unix:/run/redis/redis.sock
```
 `/etc/webapps/gitlab-shell/config.yml` 
```
# Redis settings used for pushing commit notices to gitlab
redis:
  bin: /usr/bin/redis-cli
  host: 127.0.0.1
  port: 6379
  # pass: redispass # Allows you to specify the password for Redis
  database: 5 # Use different database, default up to 16
  socket: /run/redis/redis.sock # **uncomment** this line
  namespace: resque:gitlab
```

### Database backend

A Database backend will be required before Gitlab can be run. Currently GitLab supports [MariaDB](/index.php/MariaDB "MariaDB") and [PostgreSQL](/index.php/PostgreSQL "PostgreSQL"). By default, GitLab assumes you will use MySQL. Extra work is needed if you plan to use PostgreSQL.

#### MariaDB

To set up MySQL (MariaDB) you need to create a database called `gitlabhq_production` along with a user (default: `gitlab`) who has full privileges to the database:

 `$ mysql -u root -p` 
```
mysql> CREATE DATABASE `gitlabhq_production` DEFAULT CHARACTER SET `utf8` COLLATE `utf8_unicode_ci`;
mysql> CREATE USER 'gitlab'@'localhost' IDENTIFIED BY 'password';
mysql> GRANT ALL ON `gitlabhq_production`.* TO 'gitlab'@'localhost';
mysql> \q
```

Try connecting to the new database with the new user:

```
$ mysql -u **gitlab** -p -D gitlabhq_production

```

Copy the MySQL template file before configuring it:

```
# cp /usr/share/doc/gitlab/database.yml.mysql /etc/webapps/gitlab/database.yml

```

Next you will need to open `/etc/webapps/gitlab/database.yml` and set `username:` and `password:` for the `gitlabhq_production`:

 `/etc/webapps/gitlab/database.yml` 
```
#
# PRODUCTION
#
production:
  adapter: mysql2
  encoding: utf8
  collation: utf8_general_ci
  reconnect: false
  database: gitlabhq_production
  pool: 10
  username: **username**
  password: **"password"**
  # host: localhost
  # socket: /run/mysqld/mysqld.sock # If running MariaDB as socket
...

```

It should not be set as world readable, e.g. only processes running under the `gitlab` user should have read/write access:

```
# chmod 600 /etc/webapps/gitlab/database.yml
# chown gitlab:gitlab /etc/webapps/gitlab/database.yml

```

For more info and other ways to create/manage MySQL databases, see the [MariaDB documentation](https://mariadb.org/docs/) and the [GitLab official (generic) install guide](https://github.com/gitlabhq/gitlabhq/blob/master/doc/install/installation.md).

#### PostgreSQL

Login to PostgreSQL and create the `gitlabhq_production` database with along with its user.

**Note:** Make sure that the table `template1` has the correct encoding. It can be changed by following these steps [here](https://ptpb.pw/Hp3W)

Remember to change `your_username_here` and `your_password_here` to the real values:

```
# psql -d template1

```

```
template1=# CREATE USER your_username_here WITH PASSWORD 'your_password_here';
template1=# ALTER USER your_username_here SUPERUSER;
template1=# CREATE DATABASE gitlabhq_production OWNER your_username_here;
template1=# \q
```

**Note:** The reason for creating the user as a superuser is that GitLab is trying to be "smart" and install extensions (not just create them in its own userspace). And this is only allowed by superusers in Postgresql.

Try connecting to the new database with the new user to verify it works:

```
# psql -d gitlabhq_production

```

Copy the PostgreSQL template file before configuring it (overwriting the default MySQL configuration file):

```
# cp /usr/share/doc/gitlab/database.yml.postgresql /etc/webapps/gitlab/database.yml

```

Open the new `/etc/webapps/gitlab/database.yml` and set the values for `username:` and `password:`. For example:

 `/etc/webapps/gitlab/database.yml` 
```
#
# PRODUCTION
#
production:
  adapter: postgresql
  encoding: unicode
  database: gitlabhq_production
  pool: 10
  username: your_username_here
  password: "your_password_here"
  # host: localhost
  # port: 5432
  # socket: /tmp/postgresql.sock
...

```

For our purposes (unless you know what you are doing), you do not need to worry about configuring the other databases listed in `/etc/webapps/gitlab/database.yml`. We only need to set up the production database to get GitLab working.

### Firewall

If you want to give direct access to your Gitlab installation through an [iptables](/index.php/Iptables "Iptables") firewall, you may need to adjust the port and the network address:

```
# iptables -A tcp_inbound -p TCP -s **192.168.1.0/24** --destination-port **80** -j ACCEPT

```

To enable API-access:

```
# iptables -A tcp_inbound -p TCP -s **192.168.1.0/24** --destination-port **8080** -j ACCEPT

```

If you are behind a router, do not forget to forward this port to the running GitLab server host, if you want to allow WAN-access.

### Initialize Gitlab database

Start the [Redis](/index.php/Redis "Redis") server before we create the database.

Initialize the database and activate advanced features:

```
# su - gitlab -s /bin/sh -c "cd '/usr/share/webapps/gitlab'; bundle-2.3 exec rake gitlab:setup RAILS_ENV=production"

```

Finally run the following commands to check your installation:

```
# su - gitlab -s /bin/sh -c "cd '/usr/share/webapps/gitlab'; bundle-2.3 exec rake gitlab:env:info RAILS_ENV=production"
# su - gitlab -s /bin/sh -c "cd '/usr/share/webapps/gitlab'; bundle-2.3 exec rake gitlab:check RAILS_ENV=production"

```

**Note:**

*   The *gitlab:env:info* and *gitlab:check* commands will show a fatal error related to git. This is OK.
*   The *gitlab:check* will complain about missing initscripts. This is nothing to worry about, as [systemd](/index.php/Systemd "Systemd") service files are used instead (which GitLab does not recognize).

### Adjust modifier bits

(The gitlab check won't pass if the user and group ownership isn't configured properly)

```
# chmod -R ug+rwX,o-rwx /var/lib/gitlab/repositories/
# chmod -R ug-s /var/lib/gitlab/repositories
# find /var/lib/gitlab/repositories/ -type d -print0 | xargs -0 chmod g+s

```

## Start and test GitLab

Make sure [MySQL](/index.php/MySQL "MySQL") or [PostgreSQL](/index.php/PostgreSQL "PostgreSQL") and [Redis](/index.php/Redis "Redis") are running and setup correctly.

Then [start](/index.php/Start "Start")/[enable](/index.php/Enable "Enable") `gitlab.target`.

Now test your GitLab instance by visiting [http://localhost:8080](http://localhost:8080) or [http://yourdomain.com](http://yourdomain.com), you should be prompted to create a password:

```
username: root
password: You'll be prompted to create one on your first visit.

```

See [#Troubleshooting](#Troubleshooting) and log files inside the `/usr/share/webapps/gitlab/log/` directory for troubleshooting.

## Upgrade database on updates

After updating the [gitlab](https://www.archlinux.org/packages/?name=gitlab) package, it is required to upgrade the database:

```
# su - gitlab -s /bin/sh -c "cd '/usr/share/webapps/gitlab'; bundle-2.3 exec rake db:migrate RAILS_ENV=production"

```

Afterwards, restart gitlab-related services:

```
# systemctl daemon-reload
# systemctl restart gitlab-sidekiq gitlab-unicorn gitlab-workhorse gitlab-gitaly

```

## Advanced Configuration

### Basic SSH

After completing the basic installation, set up SSH access for users. Configuration for [OpenSSH](/index.php/Secure_Shell#OpenSSH "Secure Shell") is described below. [Other SSH clients and servers](/index.php/Secure_Shell#Other_SSH_clients_and_servers "Secure Shell") will require different modifications.

For tips on adding user SSH keys, the process is well-documented on the [GitLab](https://docs.gitlab.com/ee/ssh/) website. You can check the administrator logs at `/var/lib/gitlab/log/gitlab-shell.log` to confirm user SSH keys are being submitted properly. Behind the scenes, GitLab adds these keys to its *authorized_keys* file in `/var/lib/gitlab/.ssh/authorized_keys`.

The common method of testing keys (ex: `$ ssh -T git@*YOUR_SERVER*`) requires a bit of extra configuration to work correctly. The user configured in `/etc/webapps/gitlab/gitlab.yml` (default user: `gitlab`) must be added to the server's sshd configuration file, in addition to a handful of other changes:

 `/etc/ssh/sshd_config` 
```
PubkeyAuthentication   yes
AuthorizedKeysFile     %h/.ssh/authorized_keys

```

After updating the configuration file, restart the ssh daemon:

```
# systemctl restart sshd

```

Test user SSH keys (optionally add -v to see extra information):

```
$ ssh -T **gitlab**@*YOUR_SERVER*

```

### Custom SSH Connection

If you are running SSH on a non-standard port, you must change the GitLab user's SSH config:

 `/var/lib/gitlab/.ssh/config` 
```
host localhost      # Give your setup a name (here: override localhost)
user gitlab         # Your remote git user
port 2222           # Your port number
hostname 127.0.0.1; # Your server name or IP
```

You also need to change the corresponding options (e.g. ssh_user, ssh_host, admin_uri) in the `/etc/webapps/gitlab/gitlab.yml` file.

### HTTPS/SSL

#### Change GitLab configs

Modify `/etc/webapps/gitlab/shell.yml` so the url to your GitLab site starts with `https://`. Modify `/etc/webapps/gitlab/gitlab.yml` so that `https:` setting is set to `true`.

See also [Apache HTTP Server#TLS/SSL](/index.php/Apache_HTTP_Server#TLS.2FSSL "Apache HTTP Server") and [Let’s Encrypt](/index.php/Let%E2%80%99s_Encrypt "Let’s Encrypt").

#### Let's Encrypt

To validate your URL, the Let's Encrypt process will try to access your gitlab server with something like `https://gitlab.*YOUR_SERVER_FQDN*/.well-known/acme-challenge/*A_LONG_ID*`. But, due to gitlab configuration, every request to `gitlab.*YOUR_SERVER_FQDN*` will be redirected to a proxy (gitlab-workhorse) that will not be able to deal with this URL.

To bypass this issue, you can use the Let's Encrypt webroot configuration, setting the webroot at `/srv/http/letsencrypt/`.

Additionally, force the Let's Encrypt request for gitlab to be redirected to this webroot by adding the following:

 `/etc/http/conf/extra/gitlab.conf` 
```
Alias "/.well-known"  "/srv/http/letsencrypt/.well-known"
RewriteCond   %{REQUEST_URI}  !/\.well-known/.*

```

### Web server configuration

If you want to integrate Gitlab into a running web server instead of using its build-in http server Unicorn, then follow these instructions.

##### Node.js

You can easily set up an http proxy on port 443 to proxy traffic to the GitLab application on port 8080 using http-master for Node.js. After you have created your domain's OpenSSL keys and have gotten you CA certificate (or self signed it), then go to [https://github.com/CodeCharmLtd/http-master](https://github.com/CodeCharmLtd/http-master) to learn how easy it is to proxy requests to GitLab using HTTPS. http-master is built on top of [node-http-proxy](https://github.com/nodejitsu/node-http-proxy).

#### Nginx

See [Nginx#Configuration](/index.php/Nginx#Configuration "Nginx") for basic *nginx* configuration and [Nginx#TLS/SSL](/index.php/Nginx#TLS.2FSSL "Nginx") for enabling HTTPS. The sample in this section also assumes that server blocks are managed with [Nginx#Managing server entries](/index.php/Nginx#Managing_server_entries "Nginx").

Create and edit the configuration based on the following snippet. See the [upstream GitLab repository](https://gitlab.com/gitlab-org/gitlab-ce/tree/master/lib/support/nginx) for more examples.

 `/etc/nginx/servers-available/gitlab` 
```
upstream gitlab-workhorse {
  server unix:/run/gitlab/gitlab-workhorse.socket fail_timeout=0;
}

server {
  listen 80;
  #listen 443 ssl; # uncomment to enable ssl
  server_name example.com

  #ssl_certificate ssl/example.com.crt;
  #ssl_certificate_key ssl/example.com.key;

  location / {
      # unlimited upload size in nginx (so the setting in GitLab applies)
      client_max_body_size 0;

      # proxy timeout should match the timeout value set in /etc/webapps/gitlab/unicorn.rb
      proxy_read_timeout 60;
      proxy_connect_timeout 60;
      proxy_redirect off;

      proxy_set_header Host $http_host;
      proxy_set_header X-Real-IP $remote_addr;
      proxy_set_header X-Forwarded-Ssl on;
      proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
      proxy_set_header X-Forwarded-Proto $scheme;

      proxy_pass http://gitlab-workhorse;
  }

  error_page 404 /404.html;
  error_page 422 /422.html;
  error_page 500 /500.html;
  error_page 502 /502.html;
  error_page 503 /503.html;
  location ~ ^/(404|422|500|502|503)\.html$ {
    root /usr/share/webapps/gitlab/public;
    internal;
  }
}

```

#### Apache

Install and configure the [Apache HTTP Server](/index.php/Apache_HTTP_Server "Apache HTTP Server"). You can use these [upstream recipes](https://gitlab.com/gitlab-org/gitlab-recipes/tree/master/web-server/apache) to get started with the configuration file for GitLab's virtual host.

For the SSL configuration see [Apache HTTP Server#TLS/SSL](/index.php/Apache_HTTP_Server#TLS.2FSSL "Apache HTTP Server"). If you do not need it, remove it. Notice that the SSL virtual host needs a specific IP instead of generic. Also if you set a custom port for Unicorn, do not forget to set it at the `BalanceMember` line.

### Gitlab-workhorse

Since 8.0 GitLab uses separate HTTP server [gitlab-workhorse](https://www.archlinux.org/packages/?name=gitlab-workhorse) for large HTTP requests like Git push/pull. If you want to use this instead of SSH, install the [gitlab-workhorse](https://www.archlinux.org/packages/?name=gitlab-workhorse) package, enable `gitlab-workhorse.service` and configure web server for this. [gitlab-workhorse](https://www.archlinux.org/packages/?name=gitlab-workhorse) should now be preferred over `gitlab-unicorn` according to the GitLab team: [https://gitlab.com/gitlab-org/gitlab-ce/issues/22528#note_16036216](https://gitlab.com/gitlab-org/gitlab-ce/issues/22528#note_16036216)

**Note:** Unicorn is still needed so don't disable or stop `gitlab-unicorn.service`.

By default [gitlab-workhorse](https://www.archlinux.org/packages/?name=gitlab-workhorse) listens on `/run/gitlab/gitlab-workhorse.socket`. You can [edit](/index.php/Edit "Edit") `gitlab-workhorse.service` and change the parameter `-listenAddr` to make it listen on an address, for example `-listenAddr 127.0.0.1:8181`. If listening on an address you also need to set the network type to `-listenNetwork tcp`

When using nginx remember to edit your nginx configuration file. To switch from gitlab-unicorn to gitlab-workhorse edit the two following settings accordingly

 `/etc/nginx/servers-available/gitlab` 
```
upstream gitlab {
   server unix:/run/gitlab/gitlab-workhorse.socket fail_timeout=0;
}

...

      proxy_pass [http://unix:/run/gitlab/gitlab-workhorse.socket](http://unix:/run/gitlab/gitlab-workhorse.socket);
  }  
}
```

## Useful Tips

### Hidden options

Go to Gitlab's home directory:

```
# cd /usr/share/webapps/gitlab

```

and run:

 `# rake -T | grep gitlab` 
```
rake gitlab:app:check                         # GITLAB | Check the configuration of the GitLab Rails app
rake gitlab:backup:create                     # GITLAB | Create a backup of the GitLab system
rake gitlab:backup:restore                    # GITLAB | Restore a previously created backup
rake gitlab:check                             # GITLAB | Check the configuration of GitLab and its environment
rake gitlab:cleanup:block_removed_ldap_users  # GITLAB | Cleanup | Block users that have been removed in LDAP
rake gitlab:cleanup:dirs                      # GITLAB | Cleanup | Clean namespaces
rake gitlab:cleanup:repos                     # GITLAB | Cleanup | Clean repositories
rake gitlab:env:check                         # GITLAB | Check the configuration of the environment
rake gitlab:env:info                          # GITLAB | Show information about GitLab and its environment
rake gitlab:generate_docs                     # GITLAB | Generate sdocs for project
rake gitlab:gitlab_shell:check                # GITLAB | Check the configuration of GitLab Shell
rake gitlab:import:all_users_to_all_groups    # GITLAB | Add all users to all groups (admin users are added as owners)
rake gitlab:import:all_users_to_all_projects  # GITLAB | Add all users to all projects (admin users are added as masters)
rake gitlab:import:repos                      # GITLAB | Import bare repositories from gitlab_shell -> repos_path into GitLab project instance
rake gitlab:import:user_to_groups[email]      # GITLAB | Add a specific user to all groups (as a developer)
rake gitlab:import:user_to_projects[email]    # GITLAB | Add a specific user to all projects (as a developer)
rake gitlab:satellites:create                 # GITLAB | Create satellite repos
rake gitlab:setup                             # GITLAB | Setup production application
rake gitlab:shell:build_missing_projects      # GITLAB | Build missing projects
rake gitlab:shell:install[tag,repo]           # GITLAB | Install or upgrade gitlab-shell
rake gitlab:shell:setup                       # GITLAB | Setup gitlab-shell
rake gitlab:sidekiq:check                     # GITLAB | Check the configuration of Sidekiq
rake gitlab:test                              # GITLAB | Run all tests
rake gitlab:web_hook:add                      # GITLAB | Adds a web hook to the projects
rake gitlab:web_hook:list                     # GITLAB | List web hooks
rake gitlab:web_hook:rm                       # GITLAB | Remove a web hook from the projects
rake setup                                    # GITLAB | Setup gitlab db

```

### Backup and restore

Create a backup of the gitlab system:

```
# sudo -u gitlab -H rake RAILS_ENV=production gitlab:backup:create

```

Restore the previously created backup file `/home/gitlab/gitlab/tmp/backups/20130125_11h35_1359131740_gitlab_backup.tar`:

```
# sudo -u gitlab -H rake RAILS_ENV=production gitlab:backup:restore BACKUP=/home/gitlab/gitlab/tmp/backups/20130125_11h35_1359131740

```

**Note:** Backup folder is set in `config/gitlab.yml`. GitLab backup and restore is documented [here](https://github.com/gitlabhq/gitlabhq/blob/master/doc/raketasks/backup_restore.md).

### Sending mails from Gitlab via SMTP

You might want to use a gmail (or other mail service) to send mails from your gitlab server. This avoids the need to install a mail daemon on the gitlab server.

Adjust `smtp_settings.rb` according to your mail server settings:

 `/usr/share/webapps/gitlab/config/initializers/smtp_settings.rb` 
```
if Rails.env.production?
  Gitlab::Application.config.action_mailer.delivery_method = :smtp

  ActionMailer::Base.delivery_method = :smtp
  ActionMailer::Base.smtp_settings = {
    address:              'smtp.gmail.com',
    port:                 587,
    domain:               'gmail.com',
    user_name:            'username@gmail.com',
    password:             'application password',
    authentication:       'plain',
    enable_starttls_auto: true
  }
end
```

Gmail will reject mails received this way (and send you a mail that it did). You will need to disable secure authentication (follow the link in the rejection mail) to work around this. The more secure approach is to enable two-factor authentication for username@gmail.com and to set up an application password for this configuration file.

## Troubleshooting

### HTTPS is not green (gravatar not using https)

Redis caches gravatar images, so if you have visited your GitLab with http, then enabled https, gravatar will load up the non-secure images. You can clear the cache by doing

```
cd /usr/share/webapps/gitlab
RAILS_ENV=production bundle-2.3 exec rake cache:clear

```

as the gitlab user.

### Errors after updating

After updating the package from the AUR, the database migrations and asset updates will sometimes fail. These steps may resolve the issue, if a simple reboot does not.

First, move to the gitlab installation directory.

```
# cd /usr/share/webapps/gitlab

```

If every gitlab page gives a 500 error, then the database migrations and the assets are probably stale. If not, skip this step.

```
# su - gitlab -s /bin/sh -c "cd '/usr/share/webapps/gitlab'; bundle-2.3 exec rake db:migrate RAILS_ENV=production"

```

If gitlab is constantly waiting for the deployment to finish, then the assets have probably not been recompiled.

```
# su - gitlab -s /bin/sh -c "cd '/usr/share/webapps/gitlab'; bundle-2.3 exec rake gitlab:assets:clean gitlab:assets:compile cache:clear RAILS_ENV=production"

```

Finally, restart the gitlab services and test your site.

```
# systemctl restart gitlab-unicorn gitlab-sidekiq gitlab-workhorse

```

### Gitlab-Unicorn cannot access non-default repositories directory

If a custom repository storage directory is set in `/home`, disable the `ProtectHome=true` parameter in the `gitlab-unicorn.service` (see [Systemd#Drop-in files](/index.php/Systemd#Drop-in_files "Systemd") and the [relevant forum thread on gitlab.com](https://forum.gitlab.com/t/cannot-change-repositores-location/9634/2)).

## See also

*   [Official installation documentation](https://docs.gitlab.com/ce/install/installation.html)
*   [GitLab recipes with further documentation on running it with several web servers](https://gitlab.com/gitlab-org/gitlab-recipes)
*   [GitLab source code](https://gitlab.com/gitlab-org/gitlab-ce)