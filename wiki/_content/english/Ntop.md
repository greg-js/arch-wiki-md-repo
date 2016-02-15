[Ntop](http://www.ntop.org/products/ntop/) is a network traffic probe based on [libcap](http://www.tcpdump.org/), that offers RMON-like network traffic statistics accessible via a web browser.

## Contents

*   [1 Installation and configuration](#Installation_and_configuration)
*   [2 Tips and tricks](#Tips_and_tricks)
    *   [2.1 Web interface](#Web_interface)
    *   [2.2 Group and user](#Group_and_user)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 **ERROR** RRD: Disabled - unable to create base directory (err 13, /var/lib/ntop/rrd)](#.2A.2AERROR.2A.2A_RRD:_Disabled_-_unable_to_create_base_directory_.28err_13.2C_.2Fvar.2Flib.2Fntop.2Frrd.29)
    *   [3.2 Please enable make sure that the ntop html/ directory is properly installed](#Please_enable_make_sure_that_the_ntop_html.2F_directory_is_properly_installed)

## Installation and configuration

[Install](/index.php/Install "Install") the [ntop](https://www.archlinux.org/packages/?name=ntop) package. The first run of ntop, you must set the admin password:

```
# ntop

```

Next, you need to edit the configuration file (`/etc/conf.d/ntop`) to adapt on your needs. Below is an example configuration, with the focus on the host to get as much as information from the hosts connections:

 `/etc/conf.d/ntop` 

```
# Parameters to be passed to ntop.
NTOP_ARGS="-K -W 2323 -i enp1s0,wlp2s0 -M -s -4 -6 -s -u ntop -c -r 30 --w3c -t 3 -a /var/log/ntop/http.log -O /var/log/ntop/ -q --skip-version-check 0"

# Location of the log file.
NTOP_LOG="/var/log/ntop/ntop.log"

```

Start the _ntop_ [systemd](/index.php/Systemd "Systemd") service and if you want to start _ntop_ at boot, enable it.

## Tips and tricks

### Web interface

To access ntop's web interface, enter [http://127.0.0.1:3000/](http://127.0.0.1:3000/) into your web browser. To make changes to the server, you will need to enter your username (default = _admin_) and password.

If ntop is not just used locally on your machine, but network wide by multiple users, you'd be better off by allowing SSL connections (http**s**) **only**.

```
# ntop -W 4223

```

Additional paramethers are allowed. Now direct our browser to [https://127.0.0.1:4223/](https://127.0.0.1:4223/).

You can also provide ntop with your own SSL certificate. Simply put it in ntop's config directory and name it **ntop-cert.pem**

```
# cd /etc/ntop/
# openssl req -x509 -nodes -days 365 
  \-subj '/C=US/L=Portland/CN=swim' 
  \-newkey rsa:1024 -keyout ntop-cert.pem -out ntop-cert.pem

```

### Group and user

In order that the _-u_ parameter is able to work properly and to secure your ntop setup a bit more, you should create an own group and user for it.

```
# useradd -M -s /usr/bin/false ntop
# passwd -l ntop

```

**Note:** The `passwd` command here is optional, but recommended, as it will render the system more secure regarding your sshd.

## Troubleshooting

### **ERROR** RRD: Disabled - unable to create base directory (err 13, /var/lib/ntop/rrd)

Directory `/var/lib/ntop/rrd/` may not exist. Create it and make sure it belongs to user nobody.

### Please enable make sure that the ntop html/ directory is properly installed

If you receive this warning while trying to access the web interface, edit `/etc/conf.d/ntop` to include your IP and restart the daemon. For example:

```
NTOP_ARGS="-i enp1s0 -w 127.0.0.1:3000"

```

This is the IP you will use to access the web interface.