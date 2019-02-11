[Squid](http://www.squid-cache.org) is a caching proxy for HTTP, HTTPS and FTP, providing extensive access controls.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Accessing services on local hostnames](#Accessing_services_on_local_hostnames)
*   [4 Starting](#Starting)
*   [5 Content Filtering](#Content_Filtering)
*   [6 Frontend](#Frontend)
    *   [6.1 Squid 4.x not supported in Webmin](#Squid_4.x_not_supported_in_Webmin)
*   [7 Ad blocking with adzapper](#Ad_blocking_with_adzapper)
    *   [7.1 Installation](#Installation_2)
    *   [7.2 Configuration](#Configuration_2)
*   [8 Anti-virus layer](#Anti-virus_layer)
    *   [8.1 Installing dependencies](#Installing_dependencies)
    *   [8.2 Configuration](#Configuration_3)
    *   [8.3 Testing](#Testing)
*   [9 Transparent web proxy](#Transparent_web_proxy)
    *   [9.1 iptables](#iptables)
    *   [9.2 Shorewall](#Shorewall)
*   [10 HTTP Authentication](#HTTP_Authentication)
    *   [10.1 NTLM](#NTLM)
*   [11 Hide Browser’s Real IP Address](#Hide_Browser’s_Real_IP_Address)
*   [12 SSL Bumping](#SSL_Bumping)
    *   [12.1 Create Self-Signed Root CA Certificate](#Create_Self-Signed_Root_CA_Certificate)
    *   [12.2 Create a DER-encoded certificate to import into users' browsers](#Create_a_DER-encoded_certificate_to_import_into_users'_browsers)
    *   [12.3 Modify Squid Configuration File](#Modify_Squid_Configuration_File)
    *   [12.4 Create and initialize TLS certificates cache directory](#Create_and_initialize_TLS_certificates_cache_directory)
    *   [12.5 Finally, Restart Squid then SSL Bump will work](#Finally,_Restart_Squid_then_SSL_Bump_will_work)
*   [13 Troubleshooting](#Troubleshooting)
    *   [13.1 Squid needs to be restarted after boot](#Squid_needs_to_be_restarted_after_boot)
*   [14 Additional Resources](#Additional_Resources)

## Installation

[Install](/index.php/Install "Install") the [squid](https://www.archlinux.org/packages/?name=squid) package.

## Configuration

By default, the cache directories will be created in `/var/cache/squid`, and the appropriate permissions set up for those directories. However, for greater control, we need to delve into `/etc/squid/squid.conf`.

Everything is well commented, but if you want to strip the comments out you should run:

```
sed -i "/^#/d;/^ *$/d" /etc/squid/squid.conf

```

The following options might be of some use to you. If you do not have the option present in your configuration file, add it!

*   `http_port` - Sets the port that Squid binds to on your local machine. You can have Squid bind to multiple ports by specifying multiple http_port lines. By default, Squid binds to port 3128.

```
http_port 3128
http_port 3129

```

*   `http_access` - This is an access control list for who is allowed to use the proxy. By default only localhost is allowed to access the proxy. For testing purposes, you may want to change the option `http_access deny all` to `http_access allow all`, which will allow anyone to connect to your proxy. If you wanted to just allow access to your subnet, you can do:

```
acl ip_acl src 192.168.1.0/24
http_access allow ip_acl
http_access deny all

```

*   `cache_mgr` - This is the email address of the cache manager.

```
cache_mgr squid.admin@example.com

```

*   `shutdown_lifetime` - Specifies how long Squid should wait when its service is asked to stop. If you're running squid on your desktop PC, you may want to set this to something short.

```
shutdown_lifetime 10 seconds

```

*   `cache_mem` - This is how much memory you want Squid to use to keep objects in memory rather than writing them to disk. Squid's total memory usage will exceed this! By default this is 8MB, so you might want to increase it if you have lots of RAM available.

```
cache_mem 64 MB

```

*   `visible_hostname` - hostname that will be shown in status/error messages

```
visible_hostname cerberus

```

*   `cache_peer` - If you want your Squid to go through another proxy server, rather than directly out to the Internet, you need to specify it here.
*   `login` - Use this option if the parent proxy requires authentication.
*   `never_direct` - Tells the cache to never go direct to the internet to retrieve a page. You will want this if you have set the option above.

```
cache_peer 10.1.1.100 parent 8080 0 no-query default login=user:password
never_direct allow all

```

*   `maximum_object_size` - The largest size of a cached object. By default this is 4 MB, so if you have a lot of disk space you will want to increase the size of it to something reasonable.

```
maximum_object_size 10 MB

```

**Note:** After defining a new cache_dir it maybe necessary to initialize the caches directory structure with this command: `squid -zN` -z for Create missing swap directories and -N for No daemon mode.

*   `cache_dir` - This is your cache directory, where all the cached files are stored. There are many options here, but the format should generally go like:

```
cache_dir <storage type> <directory> <size in MB> 16 256

```

So, in the case of a school's internet proxy:

```
cache_dir diskd /cache0 200000 16 256

```

If you change the cache directory from defaults, you must set the correct permissions on the cache directory before starting Squid, else it won't be able to create its cache directories and will fail to start.

## Accessing services on local hostnames

If you plan to access web servers on the LAN using hostnames that are not fully-defined (e.g. `[http://mywebapp](http://mywebapp)`), you may need to enable the `dns_defnames` option. Without this option, Squid will make a DNS request for the hostname verbatim (`mywebapp`), which may fail, depending on your LAN's DNS setup. With the option enabled, Squid will append any domain configured in `/etc/resolv.conf` when making the request (e.g. `mywebapp.company.local`).

```
dns_defnames on

```

## Starting

Once you have finished your configuration, you should check that your configuration file is correct:

```
# squid -k check

```

Then create your cache directories:

```
# squid -z

```

Then you can [start/enable](/index.php/Start/enable "Start/enable") `squid.service`.

## Content Filtering

If you're looking for a content filtering solution to work with Squid, you should check out the very powerful [DansGuardian](/index.php/DansGuardian "DansGuardian").

## Frontend

If you'd like a web-based frontend for managing Squid, [Webmin](/index.php/Webmin "Webmin") is your best bet.

### Squid 4.x not supported in Webmin

If you receive an error indicating your version of webmin is unsupported:

```
Your version of Squid is not supported by Webmin. Only versions from 1.1 to 3.4 are supported by this module.

```

you will need to modify the file `/opt/webmin/squid/index.cgi` ([see issue #952](https://github.com/webmin/webmin/issues/952))

## Ad blocking with adzapper

Adzapper is a plugin for Squid. It catches ads of all sorts (even Flash animations) and replaces them with an image of your choice, so the layout of the page isn't altered very much.

### Installation

Adzapper is no longer in the community repository, but it can be found in the [AUR](/index.php/AUR "AUR").

### Configuration

```
echo "redirect_program /usr/bin/adzapper.wrapper" >> /etc/squid/squid.conf

```

(squid 2.6.STABLE13-1)

```
echo "url_rewrite_program /usr/bin/adzapper.wrapper" >> /etc/squid/squid.conf
echo "url_rewrite_children 10" >> /etc/squid/squid.conf

```

If you want, you can configure adzapper to your liking. The configuration out of the box works wonderfully well though.

```
nano /etc/adzapper/adzapper.conf

```

## Anti-virus layer

Adding Anti-virus capabilities to Squid is done using the HAVP program to interface it with ClamAV.

### Installing dependencies

Follow [ClamAV](/index.php/ClamAV "ClamAV") to install ClamAV on your system. When it is installed, install [havp](https://aur.archlinux.org/packages/havp/) from [AUR](/index.php/AUR "AUR").

### Configuration

Once HAVP is installed, create a user group for the HAVP instance:

```
useradd havp

```

Change the owner of the antivirus logs and temporary file-testing directories to havp :

```
chown -R havp:havp /var/run/havp
chown -R havp:havp /var/log/havp

```

Add the mandatory lock option to your filesystem (needed by HAVP) : In your /etc/fstab, modify :

```
[...] / ext3 defaults 1 1

```

to :

```
[...] / ext3 defaults,mand 1 1

```

Then reload your filesystem :

```
mount -o remount /

```

Add this info in your /etc/squid/squid.conf :

```
cache_peer 127.0.0.1 parent 8080 0 no-query no-digest no-netdb-exchange default
cache_peer_access 127.0.0.1 allow all

```

Make sure your port in your /etc/havp/havp.config matches the cache_peer port in /etc/squid/squid.conf.

### Testing

[Restart](/index.php/Restart "Restart") the `squid.service` systemd unit and [start](/index.php/Start "Start") the `havp.service` systemd unit. [Enable](/index.php/Enable "Enable") both systemd units to have them launch at boot.

You can try the antivirus capabilities with a test virus (not a real virus) available [here](http://www.eicar.org/anti_virus_test_file.htm).

## Transparent web proxy

Transparency happens by redirecting all www requests eth0 picks up, to Squid. You'll need to add a port with an `intercept` (for squid 3.2) parameter. Note that at least one port must be available without the intercept parameter:

```
 http_port 3128
 http_port 3129 **intercept**

```

### iptables

From a terminal with root privileges, run:

```
# gid=`id -g proxy`
# iptables -t nat -A OUTPUT -p tcp --dport 80 -m owner --gid-owner $gid -j ACCEPT
# iptables -t nat -A OUTPUT -p tcp --dport 80 -j DNAT --to-destination SQUIDIP:3129
# iptables-save > /etc/iptables/iptables.rules

```

Then [start](/index.php/Start "Start") the `iptables.service` systemd unit.

Replace SQUIDIP with the public IP(s) which squid may use for its listening port and outbound connections.

**Note:** If you are using a content filtering solution, you should put the port for it, not the Squid port, and you need to remove the `intercept` option in the http_port line.

### Shorewall

[Edit](/index.php/Edit "Edit") `/etc/shorewall/rules` and add

```
REDIRECT	loc	3129	tcp	www # redirect to Squid on port 3128
ACCEPT		$FW	net	tcp	www # allow Squid to fetch the www content

```

Restart the `shorewall` systemd unit.

## HTTP Authentication

Squid can be configured to require a user and password in order to use it. We will use [digest http auth](https://en.wikipedia.org/wiki/Digest_access_authentication "wikipedia:Digest access authentication")

First create a users file with `htdigest -c /etc/squid/users MyRealm username`. Enter a password when prompted.

Then add these lines to your `squid.conf`:

```
   auth_param digest program /usr/lib/squid/digest_file_auth -c /etc/squid/users
   auth_param digest children 5
   auth_param digest realm MyRealm

   acl users proxy_auth REQUIRED
   http_access allow users

```

And restart squid. Now you will be prompted to enter a username and password when accessing the proxy.

You can add more users with `htdigest /etc/squid/users MyRealm newuser`. You probably would like to install Apache package, which contains `htdigest` tool.

**Note:** Be aware that `http_access` rules cascade, so you need to set them in the desired order.

### NTLM

**Warning:** NTLM is deprecated and has security problems.

Set up [samba](/index.php/Samba "Samba") and winbindd and test it with

```
 ntlm_auth --username=DOMAIN\\user

```

Grant r-x access to /var/cache/samba/winbindd_privileged/ directory for squid user/group

Then add something like this to squid.conf:

```
 auth_param ntlm program /usr/bin/ntlm_auth --helper-protocol=squid-2.5-ntlmssp
 auth_param ntlm children 5
 auth_param ntlm max_challenge_reuses 0
 auth_param ntlm max_challenge_lifetime 2 minutes
 auth_param ntlm keep_alive off

```

```
 acl ntlm_users proxy_auth REQUIRED
 http_access allow ntlm_users
 http_access deny all

```

## Hide Browser’s Real IP Address

Reference: [Squid Proxy Hide System’s Real IP Address](https://www.cyberciti.biz/faq/squid-proxy-is-not-hiding-client-ip-address/)

 `/etc/squid/squid.conf` 
```
# Hide client ip
forwarded_for delete

# Turn off via header
via off

# Deny request for original source of a request
follow_x_forwarded_for deny all
request_header_access X-Forwarded-For deny all
```

## SSL Bumping

Reference: [Intercept HTTPS CONNECT messages with SSL-Bump](https://wiki.squid-cache.org/ConfigExamples/Intercept/SslBumpExplicit)

### Create Self-Signed Root CA Certificate

`cd /etc/squid`

 `openssl req -new -newkey rsa:2048 -sha256 -days 3650 -nodes -x509 -extensions v3_ca -keyout myCA.pem -out myCA.pem` 
```
Generating a 2048 bit RSA private key                                                                                                                                                               
.....+++                                                                                                                                                                                            
.............................................................................................................................................+++                                                    
writing new private key to 'myCA.pem'                                                                                                                                                               

* * *

You are about to be asked to enter information that will be incorporated                              
into your certificate request.                                                                                                                                                                       
What you are about to enter is what is called a Distinguished Name or a DN.                                                                                                                          
There are quite a few fields but you can leave some blank                                                                                                                                            
For some fields there will be a default value,                                                                                                                                                       
If you enter '.', the field will be left blank.                                                                                                                                                      

* * *

Country Name (2 letter code) [AU]:US
State or Province Name (full name) [Some-State]:Illinois
Locality Name (eg, city) []:Chicago
Organization Name (eg, company) [Internet Widgits Pty Ltd]:Example Company LTD.
Organizational Unit Name (eg, section) []:Information Technology
Common Name (e.g. server FQDN or YOUR name) []:Example Company LTD.
Email Address []:
```

### Create a DER-encoded certificate to import into users' browsers

`openssl x509 -in myCA.pem -outform DER -out myCA.der`

The result file (myCA.der) should be imported into the 'Authorities' section of users' browsers. For example, in FireFox:

```
   Open 'Preferences'
   Go to the 'Privacy and Security' section
   Press the 'View Certificates' button and go to the 'Authorities' tab
   Press the 'Import' button, select the .der file that was created previously and pres 'OK'

```

### Modify Squid Configuration File

 `/etc/squid/squid.conf` 
```
http_port 3128 ssl-bump tls-cert=/etc/squid/myCA.pem generate-host-certificates=on dynamic_cert_mem_cache_size=4MB options=NO_SSLv3,NO_TLSv1,NO_TLSv1_1,SINGLE_DH_USE,SINGLE_ECDH_USE
ssl_bump stare all
ssl_bump bump all
```

### Create and initialize TLS certificates cache directory

`/usr/lib/squid/security_file_certgen -c -s /var/cache/squid/ssl_db -M 4MB`

### Finally, Restart Squid then SSL Bump will work

`systemctl restart squid`

## Troubleshooting

### Squid needs to be restarted after boot

If you are using both squid and NetworkManager, the following error means that squid is launched before the wifi connection is enabled by NetworkManager (`/etc/resolv.conf` is empty).

 `/var/log/squid/cache.log` 
```
Warning: Could not find any nameservers. Trying to use localhost 
Please check your /etc/resolv.conf file
or use the 'dns_nameservers' option in squid.conf.
```

You can:

*   Enable [NetworkManager-wait-online.service](/index.php/NetworkManager#Enable_NetworkManager_Wait_Online "NetworkManager") systemd unit.
*   Using [NetworkManager dispatcher](/index.php/NetworkManager#Network_services_with_NetworkManager_dispatcher "NetworkManager") instead of systemd to start squid

[Disable](/index.php/Disable "Disable") the `squid.service` systemd unit.

 `/etc/NetworkManager/dispatcher.d/10_squid` 
```
if test "$1" = 'wlp2s0'
then
    if test "$2" = 'up'
    then
        systemctl start squid
    else
        systemctl stop squid
    fi
fi
```

`sudo chmod u+x /etc/NetworkManager/dispatcher.d/10_squid`

## Additional Resources

*   [Elite Proxy Config Example(cached)](https://archive.is/oOdiT) ([cache-two](https://web.archive.org/web/20130425134032/http://gotux.net/arch-linux/squid-proxy-server/))