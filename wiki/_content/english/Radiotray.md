[Radio Tray](http://radiotray.sourceforge.net/) is an online radio streaming player that runs on a Linux system tray. Is available in the AUR: [radiotray](https://aur.archlinux.org/packages/radiotray/) .

## Troubleshooting

### No suitable plugins found error

If when trying to connect to a radio station you get the following error:

```
gstdecodebin2.c(3679): gst_decode_bin_expose (): /GstPlayBin2:player/GstURIDecodeBin:uridecodebin16/GstDecodeBin2:decodebin216:no suitable plugins found

```

[Install](/index.php/Install "Install") the [gstreamer0.10-ugly-plugins](https://www.archlinux.org/packages/?name=gstreamer0.10-ugly-plugins) package.