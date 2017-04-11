[Motion](https://motion-project.github.io/) is a program that monitors the video signal from cameras. It is able to detect if a significant part of the picture has changed; in other words, it can detect motion.

## Installation

Install the [motion](https://www.archlinux.org/packages/?name=motion) package.

## Configuration

Motion can be called with the `-c` option to define a specific configuration file (as is the case with [motionEye](https://github.com/ccrisan/motioneye/wiki))

If you do not specify `-c` or the filename you give Motion does not exist, Motion will search for the configuration file called 'motion.conf' in the following order:

1.  Current directory from where motion was invoked
2.  Then in a directory called '.motion' in the current users home directory (shell environment variable `$HOME`). E.g. `/home/goofy/.motion/motion.conf`
3.  `/etc/motion/`

The default configuration file (`/etc/motion/motion.conf`) is well commented so it is easy to find which options are required and how to set them (ie `rotate 90`)

By default Motion will use port `8080` (+1 for each camera feed), and it will be limited to localhost connections only, both the web configuration server (on port `8080`) and the camera feeds.