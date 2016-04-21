From [GitLab's homepage:](https://about.gitlab.com/)

	GitLab offers git repository management, code reviews, issue tracking, activity feeds and wikis. Enterprises install GitLab on-premise and connect it with LDAP and Active Directory servers for secure authentication and authorization. A single GitLab server can handle more than 25,000 users but it is also possible to create a high availability setup with multiple active servers.

An example live version can be found at [GitLab.com](https://gitlab.com/).

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Notes Before Configuring](#Notes_Before_Configuring)
    *   [2.2 Basic configuration](#Basic_configuration)
        *   [2.2.1 GitLab Shell](#GitLab_Shell)
        *   [2.2.2 GitLab](#GitLab)
    *   [2.3 Further configuration](#Further_configuration)
        *   [2.3.1 Database backend](#Database_backend)
        *   [2.3.2 MariaDB](#MariaDB)
        *   [2.3.3 PostgreSQL](#PostgreSQL)
        *   [2.3.4 Firewall](#Firewall)
        *   [2.3.5 Satellites access](#Satellites_access)
        *   [2.3.6 Initialize Gitlab database](#Initialize_Gitlab_database)
        *   [2.3.7 Configure Git User](#Configure_Git_User)
        *   [2.3.8 Adjust modifier bits](#Adjust_modifier_bits)
*   [3 Start and test GitLab](#Start_and_test_GitLab)
*   [4 Advanced Configuration](#Advanced_Configuration)
    *   [4.1 Custom SSH Connection](#Custom_SSH_Connection)
    *   [4.2 HTTPS/SSL](#HTTPS.2FSSL)
        *   [4.2.1 Change GitLab configs](#Change_GitLab_configs)
        *   [4.2.2 Let's Encrypt](#Let.27s_Encrypt)
    *   [4.3 Web server configuration](#Web_server_configuration)
        *   [4.3.1 Node.js](#Node.js)
        *   [4.3.2 Nginx and unicorn](#Nginx_and_unicorn)
            *   [4.3.2.1 AUR Installation](#AUR_Installation)
            *   [4.3.2.2 Manual Installation](#Manual_Installation)
        *   [4.3.3 Apache and unicorn](#Apache_and_unicorn)
            *   [4.3.3.1 Configure Unicorn](#Configure_Unicorn)
            *   [4.3.3.2 Create a virtual host for Gitlab](#Create_a_virtual_host_for_Gitlab)
            *   [4.3.3.3 Enable host and start unicorn](#Enable_host_and_start_unicorn)
    *   [4.4 Redis](#Redis)
        *   [4.4.1 Redis Over Unix Socket](#Redis_Over_Unix_Socket)
    *   [4.5 Gitlab-workhorse](#Gitlab-workhorse)
    *   [4.6 GitLab CI](#GitLab_CI)
*   [5 Useful Tips](#Useful_Tips)
    *   [5.1 Fix Rake Warning](#Fix_Rake_Warning)
    *   [5.2 Hook into /var](#Hook_into_.2Fvar)
    *   [5.3 Hidden options](#Hidden_options)
    *   [5.4 Backup and restore](#Backup_and_restore)
    *   [5.5 Migrate from sqlite to mysql](#Migrate_from_sqlite_to_mysql)
    *   [5.6 Running GitLab with rvm](#Running_GitLab_with_rvm)
    *   [5.7 Sending mails from Gitlab via SMTP](#Sending_mails_from_Gitlab_via_SMTP)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 HTTPS is not green (gravatar not using https)](#HTTPS_is_not_green_.28gravatar_not_using_https.29)
    *   [6.2 Error at push bad line length character: API](#Error_at_push_bad_line_length_character:_API)
    *   [6.3 Errors after updating](#Errors_after_updating)
    *   [6.4 /etc/webapps/gitlab/secret is empty](#.2Fetc.2Fwebapps.2Fgitlab.2Fsecret_is_empty)
*   [7 See also](#See_also)

## Installation

**Note:** If you want to use RVM refer to the article [#Running GitLab with rvm](#Running_GitLab_with_rvm) before starting with the installation

**Note:** This article covers installing and configuring GitLab without HTTPS at first. If needed, see [#Advanced Configuration](#Advanced_Configuration) to set up SSL

GitLab requires a database backend. If you plan to run it on the same machine, first install either [MySQL](/index.php/MySQL "MySQL") or [PostgreSQL](/index.php/PostgreSQL "PostgreSQL").

[Install](/index.php/Install "Install") the [gitlab](https://aur.archlinux.org/packages/gitlab/) package.

In order to receive mail notifications, a mail server must be installed and configured. See the following for more information: [Category:Mail server](/index.php/Category:Mail_server "Category:Mail server")

## Configuration

### Notes Before Configuring

The [gitlab](https://aur.archlinux.org/packages/gitlab/) package installs GitLab's files in a manner that more closely follows standard Linux conventions:

| Description | [GitLab's Official](https://github.com/gitlabhq/gitlabhq/blob/6-5-stable/doc/install/installation.md) | [gitlab](https://aur.archlinux.org/packages/gitlab/) |
| Configuration File GitShell | `/home/git/gitlab-shell/config.yml` | `/etc/webapps/gitlab-shell/config.yml` |
| Configuration File GitLab | `/home/git/gitlab/config/gitlab.yml` | `/etc/webapps/gitlab/gitlab.yml` |
| User (Home Directory) | `git` (`/home/git`) | `gitlab` (`/var/lib/gitlab`) |

**Tip:** If you are familiar with the [Arch Build System](/index.php/Arch_Build_System "Arch Build System") you can edit the PKGBUILD and relevant files to change gitlab's home directory to a place of your liking.

### Basic configuration

#### GitLab Shell

**Note:** You can leave the `gitlab_url` with default value if you intend to host GitLab on the same host.

Edit `/etc/webapps/gitlab-shell/config.yml` and set `gitlab_url:` to the prefer url and port:

 `/etc/webapps/gitlab-shell/config.yml` 
```
# GitLab user. git by default
user: gitlab

# Url to gitlab instance. Used for api calls. Should end with a slash.
# Default: [http://localhost:8080/](http://localhost:8080/)
# You only have to change the default if you have configured Unicorn
# to listen on a custom port, or if you have configured Unicorn to
# only listen on a Unix domain socket.
gitlab_url: "[http://localhost:8080/](http://localhost:8080/)" # <<-- right here

http_settings:
#  user: someone
#  password: somepass
...
```

Update the `/usr/share/webapps/gitlab/unicorn.rb` configuration if the port and/or hostname is different from the default:

 `/etc/webapps/gitlab/unicorn.rb`  `listen "127.0.0.1:8080", :tcp_nopush => true # <<-- right here` 

#### GitLab

Edit `/etc/webapps/gitlab/gitlab.yml` and setup at least the following parameters:

**Tip:** The hostname and port are used for the `git clone [http://hostname:port](http://hostname:port)` as example.

**Hostname:** In the `gitlab:` section set `host:` - replacing `localhost` to `yourdomain.com` (**note:** no '[http://'](http://') or trailing slash) - into your fully qualified domain name.

**Port:** `port:` can be confusing. This is not the port that the gitlab server (unicorn) runs on; it's the port that users will initially access through in their browser. Basically, if you intend for users to visit 'yourdomain.com' in their browser, without appending a port number to the domain name, leave `port:` as `80`. If you intend your users to type something like 'yourdomain.com:3425' into their browsers, then you'd set `port:` to `3425`. You will also have to **configure your webserver** to listen on that port.

**Timezone (optional):** The `time_zone:` parameter is optional, but may be useful to force the zone of GitLab applications.

Those are the minimal changes needed for a working GitLab install. The adventurous may read on in the comment and customize as needed.

### Further configuration

#### Database backend

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

For more info and other ways to create/manage MySQL databases, see the [MariaDB documentation](https://mariadb.org/docs/) and the [GitLab official (generic) install guide](https://github.com/gitlabhq/gitlabhq/blob/6-5-stable/doc/install/installation.md).

#### PostgreSQL

Login to PostgreSQL and create the `gitlabhq_production` database with along with it's user. Remember to change `your_username_here` and `your_password_here` to the real values:

```
# psql -d template1

```

```
template1=# CREATE USER your_username_here WITH PASSWORD 'your_password_here';
template1=# ALTER USER your_username_here SUPERUSER;
template1=# CREATE DATABASE gitlabhq_production OWNER your_username_here;
template1=# \q
```

**Note:** The reason for creating the user as a superuser is that GitLab is trying to be "smart" and install extensions (not just create them in it's own userspace). And this is only allowed by superusers in Postgresql.

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

Finally, open `/usr/lib/systemd/system/gitlab.target` and `/usr/lib/systemd/system/gitlab-unicorn.service` change all instances of `mysql.service` to `postgresql.service`.

#### Firewall

If you want to give direct access to your Gitlab installation through an [iptables](/index.php/Iptables "Iptables") firewall, you may need to adjust the port and the network address:

```
# iptables -A tcp_inbound -p TCP -s **192.168.1.0/24** --destination-port **80** -j ACCEPT

```

To enable API-access:

```
# iptables -A tcp_inbound -p TCP -s **192.168.1.0/24** --destination-port **8080** -j ACCEPT

```

If you are behind a router, do not forget to forward this port to the running GitLab server host, if you want to allow WAN-access.

#### Satellites access

The folder `satellites` should have the following permissions set:

```
# chmod 750 /var/lib/gitlab/satellites

```

#### Initialize Gitlab database

Start the Redis server before we create the database:

```
# systemctl start redis
# systemctl enable redis

```

Now you have to install bundler and the required gems with:

```
# export PATH=$PATH:/var/lib/gitlab/.gem/ruby/2.3.0/bin
# sudo -u gitlab -H gem install bundler --no-document
# cd /usr/share/webapps/gitlab
# sudo -u gitlab -H bundle install

```

**Warning:** GitLab requires `bundle` command, not `bundle-2.1`, don't forget to install it.

**Note:** If you're getting errors later on saying bundle is missing for the user 'gitlab', then this is most likely because ruby is installed in a non-readable folder such as /usr/lib or something similar and this solves that issue:
```
su - gitlab -s /bin/sh -c "export PATH=$PATH:/var/lib/gitlab/.gem/ruby/2.3.0/bin; gem install bundler --no-document"
su - gitlab -s /bin/sh -c "export PATH=$PATH:/var/lib/gitlab/.gem/ruby/2.3.0/bin; cd /usr/share/webapps/gitlab; bundle install"
su - gitlab -s /bin/sh -c "export PATH=$PATH:/var/lib/gitlab/.gem/ruby/2.3.0/bin; cd /usr/share/webapps/gitlab; bundle exec rake gitlab:setup RAILS_ENV=production"
su - gitlab -s /bin/sh -c "export PATH=$PATH:/var/lib/gitlab/.gem/ruby/2.3.0/bin; cd /usr/share/webapps/gitlab; bundle exec rake assets:precompile RAILS_ENV=production"

```

Initialize the database and activate advanced features:

```
# cd /usr/share/webapps/gitlab
# su - gitlab -s /bin/sh -c "cd '/usr/share/webapps/gitlab'; bundle exec rake gitlab:setup RAILS_ENV=production"

```

```
Missing `db_key_base` for 'production' environment. The secrets will be generated and stored in `config/secrets.yml`
This will create the necessary database tables and seed the database.
You will lose any previous data stored in the database.
Do you want to continue (yes/no)? yes

gitlabhq_production already exists
-- enable_extension("plpgsql")
   -> 0.0009s
-- create_table("abuse_reports", {:force=>true})
   -> 0.0300s
-- create_table("application_settings", {:force=>true})
   -> 0.0116s

...

Administrator account created:

login.........root
password......5iveL!fe

```

Now compile the assets:

```
# su - gitlab -s /bin/sh -c "cd '/usr/share/webapps/gitlab'; bundle exec rake assets:precompile RAILS_ENV=production"

```

Finally, check that `/etc/webapps/gitlab/secret` contains a random hex string.

#### Configure Git User

**Note:** This must match the `user` and `email_from` defined in `/usr/share/webapps/gitlab/config/gitlab.yml`.

```
# cd /usr/share/webapps/gitlab
# sudo -u gitlab -H git config --global user.name  "GitLab"
# sudo -u gitlab -H git config --global user.email "example@example.com"
# sudo -u gitlab -H git config --global core.autocrlf "input"

```

#### Adjust modifier bits

(The gitlab check won't pass if the user and group ownership isn't configured properly)

```
# chmod -R ug+rwX,o-rwx /var/lib/gitlab/repositories/
# chmod -R ug-s /var/lib/gitlab/repositories
# find /var/lib/gitlab/repositories/ -type d -print0 | xargs -0 chmod g+s

```

## Start and test GitLab

**Note:** See [#Troubleshooting](#Troubleshooting) and log files inside the `/usr/share/webapps/gitlab/log` directory for troubleshooting.

Make systemd see your new daemon unit files:

```
# systemctl daemon-reload

```

Make sure [MySQL](/index.php/MySQL "MySQL") or [PostgreSQL](/index.php/PostgreSQL "PostgreSQL") and Redis are running and setup correctly.

If needed see [#Redis Over Unix Socket](#Redis_Over_Unix_Socket) example if GitLab cannot load `redis` correctly.

After starting the database backends, we can start GitLab with its webserver (Unicorn):

```
# systemctl start gitlab-sidekiq gitlab-unicorn

```

With the following commands we check if the steps we followed so far are configured properly:

```
# cd /usr/share/webapps/gitlab
# sudo -u gitlab bundle exec rake gitlab:env:info RAILS_ENV=production
# sudo -u gitlab bundle exec rake gitlab:check RAILS_ENV=production

```

**Note:** These gitlab:env:info and gitlab:check commands will show a fatal error related to git. This is OK.
 `$ sudo -u gitlab bundle exec rake gitlab:env:info RAILS_ENV=production` 
```
fatal: Not a git repository (or any of the parent directories): .git

System information
System:		Arch rolling
Current User:	gitlab
Using RVM:	no
Ruby Version:	2.2.3p173
Gem Version:	2.4.5.1
Bundler Version:1.10.6
Rake Version:	10.4.2
Sidekiq Version:3.3.0

GitLab information
Version:	7.14.0
Revision:	fatal: Not a git repository (or any of the parent directories): .git
Directory:	/usr/share/webapps/gitlab
DB Adapter:	mysql2
URL:		http://gitlab.arch
HTTP Clone URL:	http://gitlab.arch/some-project.git
SSH Clone URL:	git@gitlab.arch:some-project.git
Using LDAP:	no
Using Omniauth:	no

GitLab Shell
Version:	2.6.4
Repositories:	/var/lib/gitlab/repositories/
Hooks:		/usr/share/webapps/gitlab-shell/hooks/
Git:		/usr/bin/git

```

**Note:** `gitlab:check` will complain about missing initscripts. This is nothing to worry about, as [systemd](/index.php/Systemd "Systemd") service files are used instead (which GitLab does not recognize).
 `$ sudo -u gitlab bundle exec rake gitlab:check RAILS_ENV=production` 
```
fatal: Not a git repository (or any of the parent directories): .git
Checking Environment ...

Git configured for gitlab user? ... yes
Has python2? ... yes
python2 is supported version? ... yes

Checking Environment ... Finished

Checking GitLab Shell ...

GitLab Shell version >= 1.7.9 ? ... OK (1.8.0)
Repo base directory exists? ... yes
Repo base directory is a symlink? ... no
Repo base owned by gitlab:gitlab? ... yes
Repo base access is drwxrws---? ... yes
update hook up-to-date? ... yes
update hooks in repos are links: ... can't check, you have no projects
Running /srv/gitlab/gitlab-shell/bin/check
Check GitLab API access: OK
Check directories and files:
        /srv/gitlab/repositories: OK
        /srv/gitlab/.ssh/authorized_keys: OK
Test redis-cli executable: redis-cli 2.8.4
Send ping to redis server: PONG
gitlab-shell self-check successful

Checking GitLab Shell ... Finished

Checking Sidekiq ...

Running? ... yes
Number of Sidekiq processes ... 1

Checking Sidekiq ... Finished

Checking LDAP ...

LDAP is disabled in config/gitlab.yml

Checking LDAP ... Finished

Checking GitLab ...

Database config exists? ... yes
Database is SQLite ... no
All migrations up? ... fatal: Not a git repository (or any of the parent directories): .git
yes
GitLab config exists? ... yes
GitLab config outdated? ... no
Log directory writable? ... yes
Tmp directory writable? ... yes
Init script exists? ... no
  Try fixing it:
  Install the init script
  For more information see:
  doc/install/installation.md in section "Install Init Script"
  Please fix the error above and rerun the checks.
Init script up-to-date? ... can't check because of previous errors
projects have namespace: ... can't check, you have no projects
Projects have satellites? ... can't check, you have no projects
Redis version >= 2.0.0? ... yes
Your git bin path is "/usr/bin/git"
Git version >= 1.7.10 ? ... yes (1.8.5)

Checking GitLab ... Finished

```

To automatically launch GitLab at startup, enable the `gitlab.target`, `gitlab-sidekiq` and `gitlab-unicorn` services.

Now test your GitLab instance by visiting [http://localhost:8080](http://localhost:8080) or [http://yourdomain.com](http://yourdomain.com) and login with the default credentials:

```
username: root
password: 5iveL!fe

```

**Note:** If your browser runs not on the machine where gitlab is running, modify your unicorn.rb in order to be able to test your setup without the use of a proxy. The corresponding line looks like this: `listen "127.0.0.1:8080, :tcp_nopush => true` 

you should replace that with:

 `listen "example.yourhost.com:8080, :tcp_nopush => true` 

## Advanced Configuration

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

To validate your URL, the Let's Encrypt process will try to access your gitlab server with something like `https://gitlab.*YOUR_SERVER_FQDN*/.well-known/*A_LONG_ID*`. But, due to gitlab configuration, every request to `gitlab.*YOUR_SERVER_FQDN*` will be redirected to a proxy (gitlab-workhorse) that will not be able to deal with this URL.

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

You can easily set up an http proxy on port 443 to proxy traffic to the GitLab application on port 8080 using http-master for Node.js. After you have creates your domain's OpenSSL keys and have gotten you CA certificate (or self signed it), then go to [https://github.com/CodeCharmLtd/http-master](https://github.com/CodeCharmLtd/http-master) to learn how easy it is to proxy requests to GitLab using HTTPS. http-master is built on top of [node-http-proxy](https://github.com/nodejitsu/node-http-proxy).

#### Nginx and unicorn

##### AUR Installation

Setup [Nginx](/index.php/Nginx "Nginx"), and create the following directories (if not exist already):

```
# mkdir /etc/nginx/servers-available
# mkdir /etc/nginx/servers-enabled

```

**Note:** You may need to change `localhost:8080` with the correct gitlab address and `example.com` to your desired server name.

**Tip:** See [Nginx#TLS/SSL](/index.php/Nginx#TLS.2FSSL "Nginx") before enabling SSL.

Create a file `/etc/nginx/servers-available/gitlab` with the following content:

 `/etc/nginx/servers-available/gitlab` 
```
# Created by: Sameer Naik
# Contributor: francoism90
# Source: [https://gist.github.com/sameersbn/becd1c976c3dc4866ef8](https://gist.github.com/sameersbn/becd1c976c3dc4866ef8)
upstream gitlab {
  server localhost:8080 fail_timeout=0;
}

server {
  listen 80;
  #listen 443 ssl; # uncomment to enable ssl
  keepalive_timeout 70;
  server_name example.com
  server_tokens off;
  #ssl_certificate ssl/example.com.crt;
  #ssl_certificate_key ssl/example.com.key;
  charset utf-8;
  root /dev/null;

  # Increase this if you want to upload larger attachments
  client_max_body_size 20m;

  location / {
      proxy_read_timeout 300;
      proxy_connect_timeout 300;
      proxy_redirect off;

      proxy_set_header X-Forwarded-Proto $scheme;
      proxy_set_header Host $http_host;
      proxy_set_header X-Real-IP $remote_addr;
      proxy_set_header X-Forwarded-Ssl on;
      proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
      proxy_set_header X-Forwarded-Proto $scheme;
      proxy_set_header X-Frame-Options SAMEORIGIN;

      proxy_pass [http://localhost:8080](http://localhost:8080);
  }  
}
```

Make sure the following line exists at the end of the `http` block in `/etc/nginx/nginx.conf`:

```
include servers-enabled/*;

```

Enable the `github` configuration:

```
# ln -s /etc/nginx/servers-available/gitlab /etc/nginx/servers-enabled/gitlab

```

Verify the new configuration:

```
# nginx -t

```

Finally, (re)start the `gitlab.target`, `resque.target` and `nginx.service`.

##### Manual Installation

If you did not use AUR, you need to copy `/usr/lib/support/nginx/gitlab` to `/etc/nginx/sites-available/`.

Run these commands to setup nginx:

```
# ln -s /etc/nginx/sites-available/gitlab /etc/nginx/sites-enabled/gitlab

```

Edit `/etc/nginx/sites-enabled/gitlab` and change YOUR_SERVER_IP and YOUR_SERVER_FQDN to the IP address and fully-qualified domain name of the host serving Gitlab.

Make sure the following line exists at the end of the `http` block in `/etc/nginx/nginx.conf`:

```
include sites-enabled/*;

```

Enable the `github` configuration:

```
# ln -s /etc/nginx/sites-available/gitlab /etc/nginx/sites-enabled/gitlab

```

Verify the new configuration:

```
# nginx -t

```

Finally, (re)start the `gitlab.target`, `resque.target` and `nginx.service`.

#### Apache and unicorn

[Install](/index.php/Install "Install") [apache](https://www.archlinux.org/packages/?name=apache) from the [official repositories](/index.php/Official_repositories "Official repositories").

##### Configure Unicorn

As the official installation guide instructs, copy the unicorn configuration file:

```
# sudo -u git -H cp /usr/share/webapps/gitlab/config/unicorn.rb.example /usr/share/webapps/gitlab/config/unicorn.rb

```

Now edit `config/unicorn.rb` and add a listening port by uncommenting the following line:

```
listen "127.0.0.1:8080"

```

**Tip:** You can set a custom port if you want. Just remember to also include it in Apache's virtual host. See below.

##### Create a virtual host for Gitlab

Create a configuration file for Gitlab’s virtual host and insert the lines below adjusted accordingly. For the ssl section see [LAMP#SSL](/index.php/LAMP#SSL "LAMP"). If you do not need it, remove it. Notice that the SSL virtual host needs a specific IP instead of generic. Also if you set a custom port for Unicorn, do not forget to set it at the BalanceMember line.

You can use these [examples](https://gitlab.com/gitlab-org/gitlab-recipes/blob/079f70dd2c091434a8dd04ed5b1a0d0e937cd361/web-server/apache/gitlab-ssl-apache2.4.conf) to get you started.

##### Enable host and start unicorn

Enable your Gitlab virtual host and reload [Apache](/index.php/Apache "Apache"):

 `/etc/httpd/conf/httpd.conf`  ` Include /etc/httpd/conf/extra/gitlab.conf` 

Copy the Apache gitlab.conf file

```
# cp /etc/webapps/gitlab/apache.conf.example /etc/httpd/conf/extra/gitlab.conf

```

Finally [start](/index.php/Start "Start") `gitlab-unicorn.service`.

### Redis

Using a Redis setup different from default (e.g. different address, port, unix socket) requires the environment variable *REDIS_URL* to be set accordingly for unicorn. This can be achieved by extending the systemd service file. Create a file */etc/systemd/system/gitlab-unicorn.service.d/redis.conf* that injects the *REDIS_URL* environment variable:

```
[Service]
Environment=REDIS_URL=unix:///run/gitlab/redis.sock

```

#### Redis Over Unix Socket

If Redis is set to listen on socket, you may want to adjust the default configuration:

 `/etc/redis.conf` 
```
...
# Accept connections on the specified port, default is 6379.
# If port 0 is specified Redis will not listen on a TCP socket.
port 0
...
# By default Redis listens for connections from all the network interfaces
# available on the server. It is possible to listen to just one or multiple
# interfaces using the "bind" configuration directive, followed by one or
# more IP addresses.
#
# Examples:
#
# bind 192.168.1.100 10.0.0.1
bind 127.0.0.1

# Specify the path for the Unix socket that will be used to listen for
# incoming connections. There is no default, so Redis will not listen
# on a unix socket when not specified.
#
unixsocket /var/run/redis/redis.sock
unixsocketperm 770
```

Create the directory `/var/run/redis` and set the correct permissions:

```
# mkdir /var/run/redis
# chown redis:redis /var/run/redis
# chmod 755 /var/run/redis

```

Add the user `git` and `gitlab` to the `redis` group:

```
# usermod -a -G redis git
# usermod -a -G redis gitlab

```

Update `/etc/webapps/gitlab-shell/config.yml` and `/etc/webapps/gitlab/resque.yml` files:

 `/etc/webapps/gitlab/resque.yml` 
```
development: unix:/var/run/redis/redis.sock
test: unix:/run/redis/redis.sock
production: unix:/run/redis/redis.sock
```
 `/etc/webapps/gitlab-shell/config.yml` 
```
...
# Redis settings used for pushing commit notices to gitlab
redis:
  bin: /usr/bin/redis-cli
  host: 127.0.0.1
  port: 6379
  # pass: redispass # Allows you to specify the password for Redis
  database: 5 # Use different database, default up to 16
  socket: /var/run/redis/redis.sock # uncomment this line
  namespace: resque:gitlab
...
```

Finally restart the `redis`, `gitlab-sidekiq` and `gitlab-unicorn` services.

For more information, please see issue [#6100](https://github.com/gitlabhq/gitlabhq/issues/6100).

### Gitlab-workhorse

Since 8.0 GitLab uses separate HTTP server `gitlab-workhorse` for large HTTP requests like Git push/pull. If you want to use this instead of SSH, install the [gitlab-workhorse](https://aur.archlinux.org/packages/gitlab-workhorse/) package, enable `gitlab-workhorse.service` and configure web server for this.

### GitLab CI

## Useful Tips

### Fix Rake Warning

When running rake tasks for the gitlab project, this error will occur: `fatal: Not a git repository (or any of the parent directories): .git`. This is a bug in bundler, and it can be safely ignored. However, if you want to git rid of the error, the following method can be used:

```
# cd /usr/share/webapps/gitlab
# sudo -u gitlab git init
# sudo -u gitlab git commit -m "initial commit" --allow-empty
```

### Hook into /var

```
# mkdir -m700 /var/log/gitlab /var/tmp/gitlab
# chown gitlab:gitlab /var/log/gitlab /var/tmp/gitlab
# sudo -u gitlab -i
# cd ~/gitlab
# d=log; mv $d/* /var/$d/gitlab; rm -f $d/.gitkeep; rm -r $d && ln -s /var/$d/gitlab $d
# d=tmp; mv $d/* /var/$d/gitlab; rm -f $d/.gitkeep; rm -r $d && ln -s /var/$d/gitlab $d
```

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

### Migrate from sqlite to mysql

Get latest code as described in [#Update Gitlab](#Update_Gitlab). Save data.

```
# cd /home/gitlab/gitlab
# sudo -u gitlab bundle exec rake db:data:dump RAILS_ENV=production

```

Follow [#Mysql](#Mysql) instructions and then setup the database.

```
# sudo -u gitlab bundle exec rake db:setup RAILS_ENV=production

```

Finally restore old data.

```
# sudo -u gitlab bundle exec rake db:data:load RAILS_ENV=production

```

### Running GitLab with rvm

To run gitlab with rvm first you have to set up an rvm:

```
 curl -L [https://get.rvm.io](https://get.rvm.io) | bash -s stable --ruby=1.9.3

```

**Note:** Version 1.9.3 is currently recommended to avoid some compatibility issues.

For the complete installation you will want to be the final user (e.g. `git`) so make sure to switch to this user and activate your rvm:

```
 su - git
 source "$HOME/.rvm/scripts/rvm"

```

Then continue with the installation instructions from above. However, the systemd scripts will not work this way, because the environment for the rvm is not activated. The recommendation here is to create to separate shell scripts for `unicorn` and `sidekiq` to activate the environment and then start the service:

 `gitlab.sh` 
```
#!/bin/sh
source `/home/git/.rvm/bin/rvm 1.9.3 do rvm env --path`
bundle exec "unicorn_rails -c /usr/share/webapps/gitlab/config/unicorn.rb -E production"

```
 `sidekiq.sh` 
```
#!/bin/sh
source `/home/git/.rvm/bin/rvm 1.9.3 do rvm env --path`
case $1 in
    start)
        bundle exec rake sidekiq:start RAILS_ENV=production
        ;;
    stop)
        bundle exec rake sidekiq:stop RAILS_ENV=production
        ;;
    *)
        echo "Usage $0 {start|stop}"
esac

```

Then modify the above systemd files so they use these scripts. Modify the given lines:

 `gitlab.service` 
```
ExecStart=/home/git/bin/gitlab.sh

```
 `sidekiq.service` 
```
ExecStart=/home/git/bin/sidekiq.sh start
ExecStop=/home/git/bin/sidekiq.sh stop

```

### Sending mails from Gitlab via SMTP

You might want to use a gmail (or other mail service) to send mails from your gitlab server. This avoids the need to install a mail daemon on the gitlab server.

Adjust `smtp_settings.rb` according to your mail server settings:

 `/usr/share/webapps/gitlab/config/initializers/smtp_settings.rb` 
```
if Rails.env.production?
  Gitlab::Application.config.action_mailer.delivery_method = :smtp

  Gitlab::Application.config.action_mailer.smtp_settings = {
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

Sometimes things may not work as expected. Be sure to visit the [Trouble Shooting Guide](https://github.com/gitlabhq/gitlab-public-wiki/wiki/Trouble-Shooting-Guide).

### HTTPS is not green (gravatar not using https)

Redis caches gravatar images, so if you have visited your GitLab with http, then enabled https, gravatar will load up the non-secure images. You can clear the cache by doing

```
cd /usr/share/webapps/gitlab
RAILS_ENV=production bundle exec rake cache:clear

```

as the gitlab user.

### Error at push bad line length character: API

If you get the following error while trying to push

```
fatal: protocol error: bad line length character: API

```

Check that your `/etc/webapps/gitlab-shell/secret` matches `/usr/share/webapps/gitlab/.gitlab_shell_secret`

If it is not the same, recreate the file with the following command

```
ln -s /etc/webapps/gitlab-shell/secret /usr/share/webapps/gitlab/.gitlab_shell_secret

```

### Errors after updating

After updating the package from the AUR, the database migrations and asset updates will sometimes fail. These steps may resolve the issue, if a simple reboot does not.

First, move to the gitlab installation directory.

```
# cd /usr/share/webapps/gitlab

```

If every gitlab page gives a 500 error, then the database migrations and the assets are probably stale. If not, skip this step.

```
# sudo -u gitlab -H bundle-2.1 exec rake db:migrate RAILS_ENV=production

```

If gitlab is constantly waiting for the deployment to finish, then the assets have probably not been recompiled.

```
# sudo -u gitlab -H bundle-2.1 exec rake assets:clean assets:precompile cache:clear RAILS_ENV=production

```

Finally, restart the gitlab services and test your site.

```
# systemctl restart gitlab-unicorn gitlab-sidekiq gitlab-workhorse

```

### /etc/webapps/gitlab/secret is empty

This file is usually generated while installing the [gitlab-shell](https://aur.archlinux.org/packages/gitlab-shell/) and the [gitlab](https://aur.archlinux.org/packages/gitlab/) packages, but in some cases it may need to be generated manually.

```
# hexdump -v -n 64 -e '1/1 "%02x"' /dev/urandom > /etc/webapps/gitlab-shell/secret
# chown root:gitlab /etc/webapps/gitlab-shell/secret
# chmod 640 /etc/webapps/gitlab-shell/secret

```

```
# hexdump -v -n 64 -e '1/1 "%02x"' /dev/urandom > /etc/webapps/gitlab/secret
# chown root:gitlab /etc/webapps/gitlab/secret
# chmod 640 /etc/webapps/gitlab/secret

```

## See also

*   [Official Documentation](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/doc/install/installation.md)
*   [Gitlab recipes with further documentation on running it with several webservers](https://gitlab.com/gitlab-org/gitlab-recipes)
*   [GitLab source code](https://github.com/gitlabhq/gitlabhq)