<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Server](#Server)
    *   [2.1 Configuration](#Configuration)
    *   [2.2 Running Server in dev mode](#Running_Server_in_dev_mode)

## Installation

Vault can be [installed](/index.php/Install "Install") with the package [vault](https://www.archlinux.org/packages/?name=vault).

## Server

Vault is [controlled](/index.php/Systemd#Using_units "Systemd") with the `vault.service` [systemd](/index.php/Systemd "Systemd") unit. Enable and start this unit.

### Configuration

Edit the `/etc/vault.hcl` file.

### Running Server in dev mode

Follow [https://www.vaultproject.io/docs/concepts/dev-server.html](https://www.vaultproject.io/docs/concepts/dev-server.html). Take note of API changes [https://stackoverflow.com/questions/49872480/vault-error-while-writing](https://stackoverflow.com/questions/49872480/vault-error-while-writing).