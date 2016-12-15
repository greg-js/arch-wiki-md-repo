[Caddy](https://caddyserver.com/) is a HTTP/2 capable web server with automatic HTTPS.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Usage](#Usage)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [caddy](https://aur.archlinux.org/packages/caddy/) package or the binary [caddy-full-bin](https://aur.archlinux.org/packages/caddy-full-bin/) package.

## Configuration

Caddy is configured using a plain text file called `Caddyfile`. The `Caddyfile` starts with address of the site to be served, and is followed by a number of directives.

A simple `Caddyfile` hosting the site at `localhost:2020` using gzip compression and logging to `../access.log`:

```
localhost:2020
gzip
log ../access.log

```

## Usage

Caddy can be run by any user from the page's directory, and the `Caddyfile` should be in the same directory:

```
$ caddy

```

Alternatively you may specify a custom `Caddyfile`:

```
$ caddy -conf="../path/to/Caddyfile"

```

## See also

*   [Caddy Official Website](https://caddyserver.com/)
*   [Caddy User Guide](https://caddyserver.com/docs)
*   [Caddyfile documentation](https://caddyserver.com/docs/caddyfile)