[Matrix](https://matrix.org/) is an ambitious new ecosystem for open federated Instant Messaging and VoIP. It consists of servers, clients and bridge software to connect to existing messaging solutions like IRC.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Webclient](#Webclient)
*   [3 Service](#Service)
*   [4 User management](#User_management)

## Installation

The reference server implementation **Synapse** is available in the community repository as [matrix-synapse](https://www.archlinux.org/packages/?name=matrix-synapse). Synapse does not run on Python 3 and requires version 2.7\. The community package creates a *synapse* user.

## Configuration

After installation, a configuration file needs to be generated. It should be readable by the *synapse* user:

```
$ cd /var/lib/synapse
$ sudo -u synapse python2 -m synapse.app.homeserver \
  --server-name my.domain.name \
  --config-path /etc/synapse/homeserver.yaml \
  --generate-config \
  --report-stats=yes

```

Note that this will generate corresponding SSL keys and self-signed certificates for the specified server name. You have to regenerate those if you change the server name.

### Webclient

The default synapse configuration enables the webclient feature. Unless you have [python2-matrix-angular-sdk](https://www.archlinux.org/packages/?name=python2-matrix-angular-sdk) installed this will make synapse fail to start. Either disable it, or install [python2-matrix-angular-sdk](https://www.archlinux.org/packages/?name=python2-matrix-angular-sdk).

**Note:** From the [developers website:](https://matrix.org/docs/projects/client/matrix-console.html) Matrix.org’s original reference AngularJS webclient has major performance issues and is not being actively maintained. Please see Riot and matrix-react-sdk for better alternatives.

**Note:** There is a bug with disabling the web_client. You need to edit multiple lines, see the issue [https://github.com/matrix-org/synapse/issues/2113](https://github.com/matrix-org/synapse/issues/2113)

## Service

A systemd service named *synapse.service* will be installed by the matrix-synapse package. It will start the synapse server as user *synapse* and use the configuration file `/etc/synapse/homeserver.yaml`.

## User management

You need at least one user on your fresh synapse server. You may create one as your normal non-root user with the command

 `$ register_new_matrix_user -c /etc/synapse/homeserver.yaml [https://localhost:8448](https://localhost:8448)` 

or using one of the [matrix clients](https://matrix.org/docs/projects/try-matrix-now.html)