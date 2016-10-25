Emby is an open source personal media server and client infrastructure. It is used to organize personal home media, as well as play back on other devices. There are a large amount of channels that are supported by the community, and can even be used with PVR and Tuner cards to provide TV streaming remotely.

## Emby Media Server (EMS)

## Installation

Install the [emby-server](https://www.archlinux.org/packages/?name=emby-server) package through pacman

## Setup

[Enable](/index.php/Enable "Enable") and start `emby-server.service`

```
sudo systemctl start emby-server.service
sudo systemctl enable emby-server.service

```

Then access the setup through your browser by navigating to:

```
`[http://localhost:8096/](http://localhost:8096/)`

```