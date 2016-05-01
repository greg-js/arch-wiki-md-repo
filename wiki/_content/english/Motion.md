[Motion](http://www.lavrsen.dk/foswiki/bin/view/Motion/WebHome) is a program that monitors the video signal from cameras. It is able to detect if a significant part of the picture has changed; in other words, it can detect motion.

## Installation

Install the [motion](https://www.archlinux.org/packages/?name=motion) package.

## Configuration

Edit the `/etc/motion/motion.conf` to match your configuration. By default it will use port `8080` (+1 for each camera feed), and it will be limited to localhost connections only, both the web configuration server (on port `8080`) and the camera feeds.