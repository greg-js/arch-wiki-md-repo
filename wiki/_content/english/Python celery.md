Quoting authors of the [project](http://www.celeryproject.org/):

	Celery is "an asynchronous task queue/job queue based on distributed message passing. It is focused on real-time operation, but supports scheduling as well. (...) Tasks can execute asynchronously (in the background) or synchronously (wait until ready)."

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Celery](#Celery)
    *   [2.2 RabbitMQ](#RabbitMQ)
    *   [2.3 Security](#Security)
*   [3 Example task](#Example_task)
    *   [3.1 Celery application](#Celery_application)
    *   [3.2 Test run](#Test_run)
    *   [3.3 Prepare module for Celery service](#Prepare_module_for_Celery_service)
    *   [3.4 Run tasks periodically](#Run_tasks_periodically)
*   [4 Run Celery in chroot (experimental)](#Run_Celery_in_chroot_.28experimental.29)
    *   [4.1 Create chroot directory and devices](#Create_chroot_directory_and_devices)
    *   [4.2 Create necessary directories](#Create_necessary_directories)
    *   [4.3 Populate chroot](#Populate_chroot)
    *   [4.4 Your package within chroot](#Your_package_within_chroot)
    *   [4.5 Test chroot](#Test_chroot)
    *   [4.6 systemd chroot unit](#systemd_chroot_unit)
*   [5 Troubleshooting](#Troubleshooting)

## Installation

[Install](/index.php/Install "Install") the package [python-celery](https://www.archlinux.org/packages/?name=python-celery). As with most python-based packages you get a package compatible with Python 3.x. If you need Python 2.x compatibility, install [python2-celery](https://www.archlinux.org/packages/?name=python2-celery) instead.

Quoting [Celery documentation](http://docs.celeryproject.org/en/latest/getting-started/first-steps-with-celery.html): "Celery requires a solution to send and receive messages" - one of the options is [rabbitmq](https://www.archlinux.org/packages/?name=rabbitmq) which also can be installed from official repositories.

## Configuration

### Celery

For configuration files the directory `/etc/celery/` needs to be created. An example configuration file is provided within [Celery documentation](http://docs.celeryproject.org/en/latest/tutorials/daemonizing.html#example-configuration).

[Start/enable](/index.php/Start/enable "Start/enable") the `celery@*celery*.service`.

### RabbitMQ

RabbitMQ stores its configuration within `/etc/rabbitmq/rabbitmq-env.conf`

The default configuration:

```
   NODENAME=rabbit@rakieta
   NODE_IP_ADDRESS=0.0.0.0
   NODE_PORT=5672

   LOG_BASE=/var/log/rabbitmq
   MNESIA_BASE=/var/lib/rabbitmq/mnesia

```

You probably want to replace `0.0.0.0` with `127.0.0.1`, RabbitMQ does not support Unix sockets. Read more about environmental variables within [RabbitMQ docs](http://www.rabbitmq.com/configure.html)

[Start/enable](/index.php/Start/enable "Start/enable") the `rabbitmq.service`.

**Note:** `rabbitmq-service` is being started as rabbitmq user with home folder stored within `/var/lib/rabbitmq` - you may want to make sure rabbitmq user owns this folder and all subfolders

Follow [RabbitMQ documentation](http://docs.celeryproject.org/en/latest/getting-started/brokers/rabbitmq.html#broker-rabbitmq) and add your user and virtual host:

```
$ cd /var/lib/rabbitmq
$ su rabbitmq -c 'rabbitmqctl add_user myuser mypassword'
$ su rabbitmq -c 'rabbitmqctl add_vhost myvhost'
$ su rabbitmq -c 'rabbitmqctl set_user_tags myuser mytag'
$ su rabbitmq -c 'rabbitmqctl set_permissions -p myvhost myuser ".*" ".*" ".*"'

```

Read [RabbitMQ admin guide](http://www.rabbitmq.com/admin-guide.html#access-control) to understand the above.

If issuing `su rabbitmq -c "rabbitmqctl status"` results in `badrpc,nodedown` visit [this blog post](http://www.somic.org/2009/02/19/on-rabbitmqctl-and-badrpcnodedown/) for more information how to fix the problem.

**Note:** You may also want to run `su rabbitmq -c "erl"` and as a result you should get an erlang prompt with no errors

### Security

You may want to read a security section from [relevant Celery documentation](http://docs.celeryproject.org/en/latest/userguide/security.html)

## Example task

### Celery application

Follow [Celery documentation](http://docs.celeryproject.org/en/latest/getting-started/first-steps-with-celery.html#application) to create a python sample task:

 `$ nano test.py` 
```
from celery import Celery

    app = Celery('tasks', backend='amqp', broker='amqp://myuser:mypassword@localhost:5672/myvhost')

    @app.task
    def add(x, y):
        return x + y
```

`amqp://myuser:mypassword@localhost:5672/myvhost` - use the same credentials/vhost you have created when configuring RabbitMQ

`backend='amqp'` - this parameter is optional since RabbitMQ is the default broker utilised by celery.

### Test run

While in the same directory as your `test.py` you can run:

```
$ celery -A task worker --loglevel=info

```

Then from another console (but within same directory) create:

 `$ nano call.py` 
```
from test import add

    add.delay(4, 4)
```

Run it:

```
$ python call.py

```

First, the console should log some information suggesting worker was called:

```
Received task: task.add[f4aff99a-7477-44db-9f6e-7e0f9342cd4e]
Task task.add[f4aff99a-7477-44db-9f6e-7e0f9342cd4e] succeeded in 0.0007182330009527504s: 8

```

### Prepare module for Celery service

Procedure below is slightly different than what you will find within [Celery documentation](http://docs.celeryproject.org/en/latest/getting-started/next-steps.html#our-project)

Create `test_task` module:

```
# mkdir /lib/python3.5/site-packages/test_task
# touch /lib/python3.5/site-packages/test_task/__init__.py
# touch /lib/python3.5/site-packages/test_task/test_task.py
# touch /lib/python3.5/site-packages/test_task/celery.py

```
 `# nano /lib/python3.5/site-packages/test_task/celery.py` 
```
from __future__ import absolute_import

from celery import Celery

app = Celery('tasks', backend='amqp', broker='amqp://myuser:mypassword@localhost:5672/myvhost')

if __name__ == '__main__':
 app.start()
```
 `# nano /lib/python3.5/site-packages/test_task/test_task.py` 
```
from __future__ import absolute_import

from test_task.celery import app

@app.task
def add(x, y):
 return x + y
```

At this point if you issue `python` in your console you should be able to issue following without any error:

```
>>> from test_task import celery

```

In `/etc/celery/celery.conf` replace:

```
CELERY_APP="proj"

```

with the following line:

```
CELERY_APP="test_task"

```

[Restart](/index.php/Restart "Restart") the `celery@*celery*.service`.

### Run tasks periodically

Tasks can be ran periodicaly through Celery Beat, basic setup is described within relevant [Celery documentation pages](http://docs.celeryproject.org/en/latest/userguide/periodic-tasks.html). An example:

If you want to specify `CELERYBEAT_SCHEDULE` within your `celery.py`, then you need to add the `app.conf` prefix to make celery recognise your scheduled tasks. After that you need to add the `--beat --schedule=/var/lib/celery/celerybeat-schedule` parameters when you start the celery daemon. Further, the `/var/lib/celery` directory must exist within the celery-relevant environment and be owned by the user that runs celery.

## Run Celery in chroot (experimental)

Installing celery in a [chroot](/index.php/Chroot "Chroot") adds an additional layer of security. To achieve an advanced security level, the chroot should include only the files needed to run the Celery application and all files should have the most restrictive permissions possible. For example, as much as possible should be owned by root, directories such as `/usr/bin` should be unreadable and unwriteable, etc.

This section adapts [Nginx#Installation in a chroot](/index.php/Nginx#Installation_in_a_chroot "Nginx") for creating the Celery chroot.

**Warning:** This is experimental approach and no guarantee is given that resulting configuration will be stable or usable. Use at your own risk.

### Create chroot directory and devices

Arch comes with an `http` user and group by default which we can use to run celery. The chroot will be in `/srv/http/apps/celery`.

```
# mkdir -p /srv/http/apps/celery
# cd /srv/http/apps/celery

```

Celery needs `/dev/null` and `/dev/urandom`. Celery will not crash at startup if `/dev/random` is missing. To install these in the chroot create the `/dev/` directory and add the devices with *mknod*. Avoid mounting all of `/dev/` to ensure that, even if the chroot is compromised, an attacker must break out of the chroot to access important devices like `/dev/sda1`.

**Tip:** Be sure that `/srv/http/apps/celery` is mounted without no-dev option

**Tip:** See `man mknod` and `ls -l /dev/{null,urandom}` to better understand the *mknod* options.

```
# mkdir /srv/http/apps/celery/dev
# mknod -m 0666 /srv/http/apps/celery/dev/null c 1 3
# mknod -m 0666 /srv/http/apps/celery/dev/random c 1 8
# mknod -m 0444 /srv/http/apps/celery/dev/urandom c 1 9

```

### Create necessary directories

The original idea was to use [python-virtualenv](https://www.archlinux.org/packages/?name=python-virtualenv) to bring all necessary python deliverables. Unfortunately, virtualenv does only half of work for us and since we are going to run Celery in chroot we need to take care of all other dependencies. We use an environment created by virtualenv for further adjustments:

```
# virtualenv --always-copy /srv/http/apps/celery

```

Create required directories:

```
# cd /srv/http/apps/celery
# mkdir {usr,dev,etc,run,tmp,var,proc}
# mv {lib,bin,include} usr
# ln -s usr/lib lib
# ln -s usr/bin bin
# ln -s usr/lib lib64
# ln -s usr/include include
# cd usr/

```

**Note:** If using a 64 bit kernel you will need to create symbolic links `lib64` and `usr/lib64` to `usr/lib`: `cd $JAIL; ln -s usr/lib lib64` and `cd $JAIL/usr; ln -s lib lib64`.

```
# ln -s lib lib64

```

Celery requires `/proc/loadavg` - bind mount it together with `/srv/http/apps/celery/tmp` and `/srv/http/apps/celery/run` as tmpfs's. The size should be limited to ensure an attacker cannot eat all the RAM:

```
# touch /srv/http/apps/celery/proc/loadavg
# mount --bind /proc/loadavg /srv/http/apps/celery/proc/loadavg
# mount -t tmpfs none /srv/http/apps/celery/run -o 'noexec,size=1M'
# mount -t tmpfs none /srv/http/apps/celery/tmp -o 'noexec,size=100M'

```

In order to preserve the mounts across reboots, the following entries should be added to `/etc/fstab`:

 `/etc/fstab` 
```
 tmpfs   /srv/http/apps/celery/run   tmpfs   rw,noexec,relatime,size=1024k   0       0
 tmpfs   /srv/http/apps/celery/tmp   tmpfs   rw,noexec,relatime,size=102400k 0       0
 /proc/loadavg /srv/http/apps/celery/proc/loadavg none bind

```

Create a log folder for celery:

```
# mkdir -p /srv/http/apps/celery/var/log/celery
# chown http:http /srv/http/apps/celery/var/log/celery

```

### Populate chroot

Copy python dependencies:

```
# cp $(ldd /usr/bin/python | grep /usr/lib | sed -sre 's/(.+)(\/usr\/lib\/\S+).+/\2/g') /srv/http/apps/celery/lib

```

**Note:** Do not try to copy `linux-vdso.so`: it is not a real library and does not exist in `/usr/lib`. Also `ld-linux-x86-64.so` will likely be listed in `/lib64` for a 64 bit system.

We are running from chroot, hence normal virtualenv behavior will not work and we need to accommodate for that by copying complete python lib folder (without site-packages):

```
# mv /srv/http/apps/celery/lib/python3.5/site-packages /tmp 
# rm -r /srv/http/apps/celery/lib/python3.5/* 
# mv /tmp/site-packages /srv/http/apps/celery/lib/python3.5/
# 
# cp -r -p /usr/lib/python3.5 /tmp
# rm -r /tmp/python3.5/site-packages
# mv /tmp/python3.5/* /srv/http/apps/celery/lib/python3.5/

```

Install celery:

```
# source /srv/http/apps/celery/bin/activate
# pip install celery

```

Celery requires `libssl`:

```
# cp $(ldd /usr/lib/libssl.so.1.0.0 | grep /usr/lib | sed -sre 's/(.+)(\/usr\/lib\/\S+).+/\2/g') /srv/http/apps/celery/usr/lib
# cp /usr/lib/libssl.so* /srv/http/apps/celery/usr/lib

```

Celery requires `libgcc_s` if you want to use multithreading:

```
# cp /usr/lib/libgcc_s* /srv/http/apps/celery/usr/lib

```

```
# cp $(ldd /usr/lib/libssl.so.1.0.0 | grep /usr/lib | sed -sre 's/(.+)(\/usr\/lib\/\S+).+/\2/g') /srv/http/apps/celery/usr/lib
# cp /usr/lib/libssl.so* /srv/http/apps/celery/usr/lib

```

Celery also requires `/bin/getent`, which in turn requires `libnss_files`:

```
# cp /bin/getent /srv/http/apps/celery/bin
# cp /lib/libnss_files* /srv/http/apps/celery/lib

```

`/bin/env` is required to register `$HOME` after chrooting but before running celery:

```
# cp /bin/env /srv/http/apps/celery/bin

```

Copy your task module (in this example the task module is called `test_task` and is stored within `/lib/python3.5/site-packages/test_task`):

```
# cp -r /lib/python3.5/site-packages/test_task lib/python3.5/site-packages

```

Copy over some miscellaneous but necessary libraries and system files.

```
# cp -rfvL /etc/{services,localtime,nsswitch.conf,nscd.conf,protocols,hosts,ld.so.cache,ld.so.conf,resolv.conf,host.conf} /srv/http/apps/celery/etc

```

Create restricted user/group files for the chroot. This way only the users needed for the chroot to function exist in it and none of the system users/groups are leaked to attackers, should they gain access to the chroot.

 `/srv/http/apps/celery/etc/group` 
```
http:x:33:
nobody:x:99:

```
 `/srv/http/apps/celery/etc/passwd` 
```
http:x:33:33:http:/:/bin/false
nobody:x:99:99:nobody:/:/bin/false

```
 `/srv/http/apps/celery/etc/shadow` 
```
http:x:14871::::::
nobody:x:14871::::::

```
 `/srv/http/apps/celery/etc/gshadow` 
```
http:::
nobody:::

```

### Your package within chroot

Now you can copy your package into chroot.

**Tip:** See [packaging](http://python-packaging-user-guide.readthedocs.org/en/latest/distributing/#configuring-your-project) and and [celery project structure](http://docs.celeryproject.org/en/latest/getting-started/next-steps.html#our-project) for python packaging instructions.

Assuming your project lives in `your_project` directory and its structure looks like following:

```
.
|-setup.py
|-CHANGES.txt
|-MANIFEST.in
|-README.txt
|-package_name
   |-__init__.py
   |-celery.py
   |-task_1.py
   |-task_2.py
   |-(...)

```

Install your package in development mode:

```
# cd /srv/http/apps/celery/your_project
# source ../bin/activate
# pip install -e .

```

All paths are relevant to your main root, you need to:

 `$ nano /srv/http/apps/celery/lib/python3.5/site-packages/package_name.egg-link` 
```
/your_project
.
```
 `$ nano /srv/http/apps/celery/lib/python3.5/site-packages/easy-install.pth` 
```
/your_project
(...)
```

**Note:** easy-install.pth will contain other packages installed within your virtualenv, make sure you do not modify other entries than the one that points to your_project

**Note:** you can also install your package running `python setup.py develop` and in such case you would have to update `/srv/http/apps/celery/lib/python3.5/site-packages/setuptools.pth`
 `$ nano /srv/http/apps/celery/lib/python3.5/site-packages/setuptools.pth`  `/usr/lib/python3.5/site-packages` 

### Test chroot

Run following to confirm chroot is correctly set up:

```
# /usr/bin/chroot --userspec=root:root /srv/http/apps/celery env -i HOME=/ /usr/bin/python -m celery worker -c 10 -A package_name --uid=33 --gid=33 --pidfile=/run/celery.pid --logfile=/var/log/celery/celery.log --loglevel="INFO"

```

Celery will be started by root but then will drop to http user.

**Note:**

*   RabbitMQ must be running before you perform above test.
*   Broker credentials within your project must match what was set within RabbitMQ.
*   You may wish to ensure your firewall is configured to allow celery/rabbitmq traffic.

### systemd chroot unit

Prepare a systemd unit:

 `# nano /etc/systemd/system/celery.service` 
```
[Unit] 
Description=Celery Nodes Daemon 
After=network.target 

[Service] 
Type=oneshot 
ExecStart=/usr/bin/chroot --userspec=root:root /srv/http/apps/celery /usr/bin/env -i HOME=/ /usr/bin/python -m celery multi start worker1 -c 2 -A package_name --uid=33 --gid=33 --pidfile=/run/celery/celery.pid --logfile=/var/log/celery/celery.log 
ExecStop=/usr/bin/chroot --userspec=root:root /srv/http/apps/celery /usr/bin/python -m celery multi stopwait worker1 --uid=33 --gid=33 --pidfile=/run/celery/celery.pid --logfile=/var/log/celery/celery.log --loglevel="INFO" 
ExecReload=/usr/bin/chroot --userspec=root:root /srv/http/apps/celery /usr/bin/python -m celery multi restart worker1 -c 2 -A package_name --uid=33 --gid=33 --pidfile=/run/celery/celery.pid --logfile=/var/log/celery/celery.log 
KillMode=control-group 
RemainAfterExit=yes 

[Install] 
WantedBy=multi-user.target
```

At this stage following should work:

```
# systemctl start celery

```

## Troubleshooting

If the [#systemd chroot unit](#systemd_chroot_unit) does not report issues but the celery service is not running, you can start the chrooted celery from console and add a more detailed log level. For example:

```
# /usr/bin/chroot --userspec=root:root /srv/http/apps/celery /usr/bin/env -i HOME=/ /usr/bin/python -m celery worker -A package_name --uid=33 --gid=33 --pidfile=/run/celery.pid --logfile=/var/log/celery/celery.log --loglevel="INFO"

```