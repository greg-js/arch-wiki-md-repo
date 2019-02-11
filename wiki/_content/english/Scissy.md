[Scissy](https://github.com/abique/scissy) is a standalone and minimal git hosting service.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 Create certificate](#Create_certificate)
    *   [1.2 Initialize git account](#Initialize_git_account)
    *   [1.3 Start scissy](#Start_scissy)
    *   [1.4 Login to scissy](#Login_to_scissy)
    *   [1.5 Become admin](#Become_admin)

## Installation

**Warning:** Scissy is still in early and active development.

[Install](/index.php/Install "Install") the [scissy](https://aur.archlinux.org/packages/scissy/) package.

### Create certificate

You have to provide SSL certificate to run scissy, so you have to create them first:

```
# cd /etc/scissy
# openssl req -new -x509 -nodes -newkey rsa:4096 -keyout server.key -out server.crt
# chmod 600 server.key server.csr server.crt
# chown scissy:scissy server.key server.csr server.crt

```

### Initialize git account

```
# su scissy - scissy-init

```

### Start scissy

To start scissy at boot [enable](/index.php/Enable "Enable") `scissy.service`. You can also [start](/index.php/Start "Start") it now.

### Login to scissy

Now to try your setup, you can register and login into [https://localhost:19042](https://localhost:19042)

### Become admin

You can get admin by doing:

```
# su scissy - scissy-set-admin my-user-name

```