[RabbitMQ](https://www.rabbitmq.com/) is a messaging broker - an intermediary for messaging. It gives your applications a common platform to send and receive messages, and your messages a safe place to live until received.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Changed hostname](#Changed_hostname)
    *   [3.2 Upgraded RabbitMQ to latest version and can't start](#Upgraded_RabbitMQ_to_latest_version_and_can.27t_start)

## Installation

Install [rabbitmq](https://www.archlinux.org/packages/community/any/rabbitmq/) from the official repositories.

## Configuration

Minimal configuration should be needed. Simply start the service with

```
# systemctl start rabbitmq

```

and it should start right up.

## Troubleshooting

As always there can be problems. Here are common ones

### Changed hostname

If you've changed your hostname after you installed rabbitmq, it will no longer be able to start. This is due to the `NODENAME` specified in `/etc/rabbitmq/rabbitmq-env.conf`. Update it to reflect your new hostname. E.g:

 `/etc/rabbitmq/rabbitmq-env.conf` 
```
NODENAME=rabbit@my-new-hostname
...

```

### Upgraded RabbitMQ to latest version and can't start

This might cause your `/etc/rabbitmq/rabbitmq-env.conf` to get the wrong `NODENAME`. For example, it might cause it to add another `@hostname` part. In either way, follow [#Changed-hostname](#Changed-hostname)