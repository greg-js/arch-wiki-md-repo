Describes how to show ASP.NET-sites under [Apache](/index.php/Apache "Apache") by using Mod_Mono.

From [Mod_Mono's site](http://www.mono-project.com/Mod_mono/):

	"*Mod_Mono is an Apache 2.0/2.2 module that provides ASP.NET support for the web's favorite server, Apache ([http://httpd.apache.org/](http://httpd.apache.org/)).*"

**Warning:** The Apache module mod-mono along with the web server xsp (which mod-mono depends) has not been in active development since April 2018 and may therefore have issues with updated Arch Linux systems as well as possible security vulnerabilities.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installing](#Installing)
*   [2 Configuring](#Configuring)
    *   [2.1 AutoHosting](#AutoHosting)
*   [3 Testing](#Testing)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Application/Site Instance Hangs with high cpu usage.](#Application/Site_Instance_Hangs_with_high_cpu_usage.)

## Installing

The setup requires [mono](https://www.archlinux.org/packages/?name=mono) and [mod_mono](https://aur.archlinux.org/packages/mod_mono/) for Apache compliance. Package [xsp](https://aur.archlinux.org/packages/xsp/) is a simple webserver for ASP.NET, optionally installed for testing the configuration.

## Configuring

Edit `/etc/httpd/conf/httpd.conf` and add the following line:

```
 Include /etc/httpd/conf/extra/mod_mono.conf

```

Finally, restart apache with:

```
 systemctl restart httpd.service

```

Now, Apache should be able to show ASP.NET-pages.

### AutoHosting

	*Further details: [http://www.mono-project.com/AutoHosting/](http://www.mono-project.com/AutoHosting/)*

With this setting, configuring apache for each deployment is no longer needed; just place the application in any directory within html-root and it will be promptly auto-configured. Add the following lines to `/etc/httpd/conf/httpd.conf` to enable the option:

```
 # Choose ASP2.0 support instead of the default 1.0
 MonoServerPath "/usr/bin/mod-mono-server4" # mono 4
 MonoAutoApplication enabled

```

## Testing

If xsp is installed and html-path is `/httpd/html`, then open a browser and access [http://server/xsp/](http://server/xsp/) to see an overview over the ASP.NET-testfiles.

## Troubleshooting

### Application/Site Instance Hangs with high cpu usage.

This is believed to be caused by a bug/incompatibility in the mod-mono module with SystemD versions above 239.303.

Currently there is no fix (other than a workaround) as the project appears to have ceased development.

See [https://github.com/mono/mod_mono/issues/9](https://github.com/mono/mod_mono/issues/9) for more information.