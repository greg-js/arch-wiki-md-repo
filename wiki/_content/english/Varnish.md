[Varnish Cache](https://www.varnish-cache.org/) is a web application accelerator also known as a caching HTTP reverse proxy. You install it in front of any server that speaks HTTP and configure it to cache the contents.

## Installation

[Install](/index.php/Install "Install") the [varnish](https://www.archlinux.org/packages/?name=varnish) package.

## Customizing Varnish

By default, varnish comes configured in `/etc/varnish/default.vcl` to use **localhost:8080** as the only backend, default.vcl is called by the default systemd varnish.service file :

 ` /usr/lib/systemd/system/varnish.service ` 
```
[Unit]
Description=Web Application Accelerator
After=network.target

[Service]
ExecStart=/usr/bin/varnishd -a 0.0.0.0:80 -f /etc/varnish/default.vcl -T localhost:6082 -s malloc,64M -u nobody -g nobody -F
ExecReload=/usr/bin/varnish-vcl-reload

[Install]
WantedBy=multi-user.target
```

systemctl enable merely makes a symlink to the default

```
$ systemctl enable varnish
ln -s '/usr/lib/systemd/system/varnish.service' '/etc/systemd/system/multi-user.target.wants/varnish.service'
```

Override the defaults in the unit file by using systemctl edit.

 `$ systemctl edit varnish.service` 

To override ExecStart use an empty ExecStart line first and then an ExecStart with the new values. Eg.

```
[Service]
ExecStart=
ExecStart=/usr/bin/varnishd -j unix,user=nobody -F -a :6081 -T localhost:6082 -f /etc/varnish/default.vcl -S /etc/varnish/secret -s malloc,1G

```

Also, if you change the config file `/etc/varnish/default.vcl` you'll need to reload varnish:

 `$ systemctl reload varnish.service` 

or restart

 `$ systemctl restart varnish.service` 

### Manual VCL load

If the previous VCL configuration reload failed, try loading the VCL file manually:

1.  Connect to the varnish console: `$ varnishadm -T localhost:6082` 
2.  Load the default VCL. Make sure it has at least one backend: `varnish> vcl.load default /etc/varnish/default.vcl` 
3.  Make it active: `varnish> vcl.use default` 
4.  Start the child proccess (optional): `varnish> start`