[RabbitMQ](https://www.rabbitmq.com/) is a messaging broker, an intermediary for messaging. It gives your applications a common platform to send and receive messages, and your messages a safe place to live until received.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Changed hostname](#Changed_hostname)
    *   [3.2 Upgraded RabbitMQ to latest version and cannot start](#Upgraded_RabbitMQ_to_latest_version_and_cannot_start)
    *   [3.3 Erlang cookie error](#Erlang_cookie_error)

## Installation

Install the [rabbitmq](https://www.archlinux.org/packages/?name=rabbitmq) package.

## Configuration

Minimal configuration should be needed. Simply [start](/index.php/Start "Start") the `rabbitmq` service.

## Troubleshooting

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