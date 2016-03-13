This article covers the installation and configuration of Arch Linux on a Lenovo T460s laptop.

## Troubleshooting

### Touchpad

There is an open [kernel bug](https://bugzilla.kernel.org/show_bug.cgi?id=114321) which causes the physical mouse button (belonging to the TrackPoint) to report release events immediately even when pressing and holding the button. This prevents drag and drop and similar actions from working.