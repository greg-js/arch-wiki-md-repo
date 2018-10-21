Related articles

*   [Puppet](/index.php/Puppet "Puppet")
*   [Puppet Dashboard](/index.php/Puppet_Dashboard "Puppet Dashboard")

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Tuning the server for lower memory usage](#Tuning_the_server_for_lower_memory_usage)
    *   [2.2 Installing support for hiera eyaml](#Installing_support_for_hiera_eyaml)
*   [3 Accessing the puppet server web interface](#Accessing_the_puppet_server_web_interface)

## Installation

To install puppet server install the [puppetserver](https://aur.archlinux.org/packages/puppetserver/) package. Note: Puppet Labs updated their GPG keys in January 2017 [[1]](https://puppet.com/blog/updated-puppet-gpg-signing-key). You may need to import their new keys.

```
$ gpg --fetch-keys [https://yum.puppetlabs.com/RPM-GPG-KEY-puppet](https://yum.puppetlabs.com/RPM-GPG-KEY-puppet)

```

Then [enable](/index.php/Enable "Enable") and [start](/index.php/Start "Start") the `puppetserver` service.

## Configuration

The Puppet Server's configuration files are stored in `/etc/puppetlabs/puppetserver/`:

```
.
|-- conf.d
|   |-- auth.conf
|   |-- global.conf
|   |-- puppetserver.conf
|   |-- web-routes.conf
|   `-- webserver.conf
|-- logback.xml
|-- request-logging.xml
`-- services.d
    `-- ca.cfg

```

in conf.d there are:

*   auth.conf which allows you to configure what puppet nodes (clients) are allowed to request from the server.
*   global.conf by default just contains the path to the logging configuration file.
*   puppetserver.conf is the main configuration file for the server, it allows you to set the JRuby load path, JRuby gem home path, the puppet master-conf-dir, master-code-dir, master-var-dir, master-run-dir, master-log-dir and most importantly the max-active-instances. It also has a section for adjusting the http-client allowed protocols which enable you to enable or disable the various SSL cipher suites and protocols.
*   web-routes.conf allows you to configure the puppet server's web-routes.
*   webserver.conf allows you to set the listen address, port, authentication type and log file path for the puppet server web interface.

Additionally, there is the `/etc/default/puppetserver` configuration file that allows you to tweak the Java Virtual Machine's startup settings, set the user and group the server runs as, the path to the puppet server's files and the configuration path.

### Tuning the server for lower memory usage

By default the puppet server allocates 2 gigabytes of RAM for itself, this can be adjusted in `/etc/default/puppetserver` by editing the JAVA_ARGS.

By default it is:

```
-Xms2g -Xmx2g -XX:MaxPermSize=256m

```

But if you are using a server that does not have sufficient RAM spare you can set it to as little as 512 megabytes. Keep in mind though that this will only cater for a small amount of managed servers and you will also need to change the maximum active instances of puppet to 1 in `/etc/puppetlabs/puppetserver/puppetserver.conf` which limits the number of server's that the server is able to communicate with at once.

### Installing support for hiera eyaml

If you wish to use Hiera eyaml on the puppet server you should install the gems for it on the puppet server using the following command:

```
puppetserver gem install hiera-eyaml

```

and then restart puppet server.

## Accessing the puppet server web interface

The web interface by default listens on https port 8140 on all interfaces. This can be changed by editing the ssl-host and ssl-port configuration options in `/etc/puppetlabs/conf.d/webserver.conf`.