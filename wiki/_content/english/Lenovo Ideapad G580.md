The 15.6" Lenovo G580 laptop PC combines top notch essentials – such as cutting-edge 3rd generation Intel® Core™ i Series processors – with a price you can afford. This ideal entry-level PC also boasts solid multimedia features like stereo speakers, HD visuals and the latest Intel® HD Graphics.

## Installation

A basic Arch Linux installation will do just fine for about everything except network cards. No custom kernel needed. However, for network cards you need to install following packages:

*   [broadcom-wl](https://aur.archlinux.org/packages/broadcom-wl/) and [wireless_tools](https://www.archlinux.org/packages/?name=wireless_tools) for wireless
*   (This backport driver is not need anymore in newer kernel 3.10) [backports-patched](https://aur.archlinux.org/packages/backports-patched/) for Atheros Network driver (Choose Alx) (find more information at [linuxfoundation.org](http://www.linuxfoundation.org/collaborate/workgroups/networking/alx))

## Graphic

G580 is one of those laptop with hybrid technology, Using Nvidia 610m and Intel® HD Graphics 4000, manually Intel HD graphic works like a charm! if you want to use Nvidia graphic card you have to install [nvidia](https://www.archlinux.org/packages/?name=nvidia) and [nvidia-utils](https://www.archlinux.org/packages/?name=nvidia-utils) drivers. for switching between graphic cards you need [bumblebee](https://www.archlinux.org/packages/?name=bumblebee) and [bbswitch](https://www.archlinux.org/packages/?name=bbswitch) follow [NVIDIA](/index.php/NVIDIA "NVIDIA") article for more information.

## Powertop

To see additional sources of power drain, install [powertop](https://www.archlinux.org/packages/?name=powertop) from [official repositories](/index.php/Official_repositories "Official repositories"). And run it while on battery power.

See [Powertop](/index.php/Powertop "Powertop") for more information.