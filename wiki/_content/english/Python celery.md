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

Follow [RabbitMQ documentation](http://docs.celeryproject.org/en/latest/getting-started/brokers/rabbitmq.html#broker-rabbitmq) and add your user and virtual host:

```
$ su rabbitmq -c 'rabbitmqctl add_user myuser mypassword'
$ su rabbitmq -c 'rabbitmqctl add_vhost myvhost'
$ su rabbitmq -c 'rabbitmqctl set_user_tags myuser mytag'
$ su rabbitmq -c 'rabbitmqctl set_permissions -p myvhost myuser ".*" ".*" ".*"'

```

Read [RabbitMQ admin guide](http://www.rabbitmq.com/admin-guide.html#access-control) to understand the above.

If issuing `su rabbitmq -c "rabbitmqctl status"` results in `badrpc,nodedown` visit [this blog post](http://www.somic.org/2009/02/19/on-rabbitmqctl-and-badrpcnodedown/) for more information how to fix the problem.

### Security

You may want to read a security section from [relevant Celery documentation](http://docs.celeryproject.org/en/latest/userguide/security.html)

## Example task

### Celery application

Follow [Celery documentation](http://docs.celeryproject.org/en/latest/getting-started/first-steps-with-celery.html#application) to create a sample task:

Create a celery application python file:

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