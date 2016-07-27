Ghost is a free and open source blogging platform written in JavaScript and distributed under the MIT License, designed to simplify the process of online publishing for individual bloggers as well as online publications.

## Contents

*   [1 AUR installation](#AUR_installation)
*   [2 Custom installation](#Custom_installation)
    *   [2.1 Prerequisites](#Prerequisites)
    *   [2.2 Installation](#Installation)
    *   [2.3 Creating a service](#Creating_a_service)

## AUR installation

[Install](/index.php/Install "Install") [Ghost](https://aur.archlinux.org/packages/Ghost/), and modify `/srv/ghost/config.js`. Then [start](/index.php/Start "Start") `ghost.service`. If you are happy with it, [enable](/index.php/Enable "Enable") it for automatic start when the system boots.

Visit [http://127.0.0.1:2368/ghost](http://127.0.0.1:2368/ghost) for final configuration.

## Custom installation

### Prerequisites

This instruction will guide you through the installation of Ghost using [nginx](/index.php/Nginx "Nginx") as web server.

[Install](/index.php/Install "Install") [nginx](https://www.archlinux.org/packages/?name=nginx), [npm](https://www.archlinux.org/packages/?name=npm), [sqlite](https://www.archlinux.org/packages/?name=sqlite), [python2](https://www.archlinux.org/packages/?name=python2), [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/), [unzip](https://www.archlinux.org/packages/?name=unzip) and [nodejs](https://www.archlinux.org/packages/?name=nodejs).

### Installation

Now it is time to configure the web server to act as a proxy of your blog. In the server block configuration file of nginx (etc/nginx/nginx.conf), change the location lines to the following:

```
location / {
       proxy_set_header   X-Real-IP $remote_addr;
       proxy_set_header   Host      $http_host;
       proxy_pass         [http://127.0.0.1:2368](http://127.0.0.1:2368);
   }

```

Create the ghost user and directory for ghost:

```
$ useradd -r -s /bin/false ghost
$ mkdir -p /srv/http/example.org

```

Now [start](/index.php/Start "Start") the `nginx.service`.

Install [Ghost](https://aur.archlinux.org/packages/Ghost/) or grab the latest version of Ghost from Ghost.org, install it manually and change into the extraction directory::

```
$ curl -L [https://ghost.org/zip/ghost-latest.zip](https://ghost.org/zip/ghost-latest.zip) -o ghost.zip
$ unzip ghost.zip -d /srv/http/example.org
$ cd /srv/http/example.org

```

Temporarily link the python path variable to python 2 instead of python 3: First create a dummy folder:

```
$ mkdir ~/bin

```

Then add a symlink python to python2 and the config scripts in it:

```
$ ln -s /usr/bin/python2 ~/bin/python
$ ln -s /usr/bin/python2-config ~/bin/python-config

```

Finally put the new folder at the beginning of your PATH variable:

```
$ export PATH=~/bin:$PATH

```

**Note:** This method of changing [environment variables](/index.php/Environment_variables "Environment variables") is not permanent and is only active in the current terminal session.

Install ghost - you do not need this step when you have installed it from the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository"):

```
$ npm install --production

```

Start ghost:

```
$ npm start --production

```

Done! Open the browser and go to 127.0.0.1 or the IP of the device you installed ghost.

### Creating a service

**Note:** You do not need this step when you have installed Ghost from the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository").

If you want to run Ghost in the background, you have to create a service. [Create](/index.php/Systemd#Writing_unit_files "Systemd") a new service unit for the local system:

 `/etc/systemd/system/ghost-example-com.service` 
```
[Unit]
Description=Ghost blog example.org  
After=network.target

[Service]
Type=simple  
PIDFile=/run/ghost-example-org.pid  
WorkingDirectory=/srv/http/example.org  
User=ghost  
Group=ghost  
ExecStart=/usr/bin/npm start --production /srv/http/example.org  
ExecStop=/usr/bin/npm stop /srv/http/example.org  
StandardOutput=null  
StandardError=null

[Install]
WantedBy=multi-user.target

```

Change the owner of the blog directory and start Ghost:

```
$ chown -R ghost:ghost /srv/http/example.org
$ systemctl start ghost-example-com

```

If everything is working fine, you can [enable](/index.php/Enable "Enable") the new unit `ghost-example-com` as well as the webserver `nginx.service`.