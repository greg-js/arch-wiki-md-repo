[RabbitMQ](https://www.rabbitmq.com/) is a messaging broker, an intermediary for messaging. It gives your applications a common platform to send and receive messages, and your messages a safe place to live until received.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Enabling MQTT](#Enabling_MQTT)
    *   [2.2 Enabling HTTP admin](#Enabling_HTTP_admin)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Service stop hangs for a minutes](#Service_stop_hangs_for_a_minutes)
    *   [3.2 Changed hostname](#Changed_hostname)
    *   [3.3 Upgraded RabbitMQ to latest version and cannot start](#Upgraded_RabbitMQ_to_latest_version_and_cannot_start)
    *   [3.4 Erlang cookie error](#Erlang_cookie_error)
    *   [3.5 can't establish TCP connection](#can.27t_establish_TCP_connection)
    *   [3.6 Can't connect with pika Python client through localhost](#Can.27t_connect_with_pika_Python_client_through_localhost)
*   [4 References](#References)

## Installation

[Install](/index.php/Install "Install") the [rabbitmq](https://www.archlinux.org/packages/?name=rabbitmq) package.

## Configuration

No configuration should be needed. Simply [start](/index.php/Start "Start") and/or [enable](/index.php/Enable "Enable") `rabbitmq.service`.

Default configuration file location `/etc/rabbitmq/rabbitmq-env.conf`. See more about configuration [on the official docs](https://www.rabbitmq.com/configure.html)

### Enabling MQTT

RabbitMQ can act as MQTT server. For this functionality to work following plugin needs to be enabled:

```
# rabbitmq-plugins enable rabbitmq_mqtt

```

RabbitMQ service needs to be restarted for this change to take effect.

Clients need to authenticate before they can post to topics. RabbitMQ segregates traffic via virtual hosts, you need to issue `**your_user_name:configured_vhost_name**` as user name in order to authenticate.

### Enabling HTTP admin

To enable the HTTP admin page:

```
# rabbitmq-plugins enable rabbitmq_management

```

Then navigate to `<ip_address_of_host>:15672`. Default credentials are `username:guest password:guest`

To allow remote machines to connect to the HTTP admin page edit/create `/etc/rabbitmq/rabbitmq.config`:

```
[{rabbit, [{loopback_users, []}]}].

```

## Troubleshooting

### Service stop hangs for a minutes

Rabbitmq package install epmd (Erlang Port Mapping Daemons) as dependency. If you run rabbitmq server via systemd, it will start detached epmd process, that will not be stopped with `systemctl stop`. You can avoid this, if add `After=epmd.service` in `[Unit]` section. Don't forget to reload daemons.

### Changed hostname

If you have changed your hostname after you installed rabbitmq, it will no longer be able to start. This is due to the `NODENAME` specified in `/etc/rabbitmq/rabbitmq-env.conf`. Update it to reflect your new hostname, for example:

 `/etc/rabbitmq/rabbitmq-env.conf` 
```
NODENAME=rabbit@my-new-hostname
...

```

### Upgraded RabbitMQ to latest version and cannot start

This might cause your `/etc/rabbitmq/rabbitmq-env.conf` to get the wrong `NODENAME`. For example, it might cause it to add another `@hostname` part. In any case, this can be fixed by following [#Changed hostname](#Changed_hostname).

### Erlang cookie error

Failure to authenticate might be caused by a wrong rabbitmq HOME setting:

```
Authentication failed (rejected by the remote node), please check the Erlang cookie
...
home dir: /root

```

Home can be set in the configuration file:

 `/etc/rabbitmq/rabbitmq-env.conf` 
```
...
HOME=/var/lib/rabbitmq
...

```

### can't establish TCP connection

If you see this error then make sure first entry with your host name within `/etc/hosts` contains the same IP address as specified within `/etc/rabbitmq/rabbitmq-env.conf` (this error is common if you configure rabbitmq to bind to specific interface).

### Can't connect with pika Python client through localhost

Trying to connect through localhost with pika Python client, raises an exception:

```
...
pika.exceptions.ProbableAccessDeniedError: (541, "INTERNAL_ERROR - access to vhost '/' refused for user 'guest': vhost '/' is down")

```

Default configuration file `/etc/rabbitmq/rabbitmq-env.conf` of the package is:

 `/etc/rabbitmq/rabbitmq-env.conf` 
```
NODENAME=rabbit@localhost
NODE_IP_ADDRESS=0.0.0.0
NODE_PORT=5672
```

Removing the username part of `NODENAME`, and leaving the hostname of the machine (which should match the one shown in `/etc/hosts`), fixes the issue:

 `/etc/rabbitmq/rabbitmq-env.conf` 
```
NODENAME=localhost
NODE_IP_ADDRESS=0.0.0.0
NODE_PORT=5672
```

## References

[erlang kernel parameters](http://erlang.org/doc/man/kernel_app.html) - kernel parameters for advanced configuration

[rabbitmq.config example](https://github.com/rabbitmq/rabbitmq-server/blob/master/docs/rabbitmq.config.example) - rabbitmq.config example (not included with rabbitmq package)