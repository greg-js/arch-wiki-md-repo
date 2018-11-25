Related articles

[Transfer More](https://up.sceptique.eu) is an minimalist open-source upload http server to store and share files temporarily, written in [Crystal](/index.php/Crystal "Crystal"), and based on Kemal [[1]](https://kemalcr.com/).

## Contents

*   [1 Installation](#Installation)
*   [2 Running](#Running)
    *   [2.1 Starting](#Starting)
    *   [2.2 Autostarting](#Autostarting)
        *   [2.2.1 System service](#System_service)
        *   [2.2.2 User service](#User_service)
*   [3 Configuration](#Configuration)
    *   [3.1 Parameters](#Parameters)
    *   [3.2 Environment variables](#Environment_variables)
    *   [3.3 Behind Nginx](#Behind_Nginx)
    *   [3.4 Others](#Others)

## Installation

[Install](/index.php/Install "Install") the [transfer-more](https://aur.archlinux.org/packages/transfer-more/) package. It only requires [crystal](https://www.archlinux.org/packages/?name=crystal) and [shards](https://www.archlinux.org/packages/?name=shards) in order to compile the initial binary, because pre-built binaries are not provided. There is not 3rd database or service dependencies.

## Running

### Starting

Run the `transfer-more` binary manually from a terminal.

### Autostarting

TODO

#### System service

TODO

#### User service

TODO

## Configuration

### Parameters

```
 transfer-more --port 3000 --host 0.0.0.0

```

### Environment variables

*   TRANSFER_SSL_ENABLED: if "true", you should see [[page](http://kemalcr.com/guide/#ssl%7Cthis)]
*   TRANSFER_BASE_STORAGE: the base path where the upload should be stored
*   TRANSFER_SECURE_SIZE: the size of the salt (minimum 1)
*   TRANSFER_STORAGE_DAYS: default 7, number of days minimum to keep the files stored
*   TRANSFER_TIME_FORMAT: default "%y%m%d%H", a part of the url to access the files (also the path in the filesystem)

### Behind Nginx

You could configure your nginx with a **/etc/nginx/servers-enabled/some-file.conf**

```
 server {
   listen 443 ssl;
   server_name up.sceptique.eu;
   client_max_body_size 1G;
   location / {
       proxy_pass [http://localhost:3000](http://localhost:3000);
       include proxy_forward.conf;
   }
 }

```

### Others

See [[2]](https://github.com/Nephos/transfer_more#usage) to get the last version of the documentation. See [[3]](https://kemalcr.com/guide/) to understand how the web framework behind transfer-more works.