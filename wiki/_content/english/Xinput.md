Related articles

*   [Xorg](/index.php/Xorg "Xorg")
*   [libinput](/index.php/Libinput "Libinput")

*xinput* is a utility to configure and test X input devices, such as mouses, keyboards, and touchpads. It is found in the [xorg-xinput](https://www.archlinux.org/packages/?name=xorg-xinput) package.

## List devices

To list what xinput devices are available, use:

 `$ xinput list` 
```
⎡ Virtual core pointer                    	id=2	[master pointer  (3)]
⎜   ↳ Virtual core XTEST pointer              	id=4	[slave  pointer  (2)]
⎜   ↳ SYNA7813:00 06CB:16DB                   	id=13	[slave  pointer  (2)]
⎜   ↳ ETPS/2 Elantech Touchpad                	id=15	[slave  pointer  (2)]
⎜   ↳ dougav’s mouse                        	id=9	[slave  pointer  (2)]
⎣ Virtual core keyboard                   	id=3	[master keyboard (2)]
    ↳ Virtual core XTEST keyboard             	id=5	[slave  keyboard (3)]
    ↳ Power Button                            	id=6	[slave  keyboard (3)]
    ↳ Video Bus                               	id=7	[slave  keyboard (3)]
    ↳ Power Button                            	id=8	[slave  keyboard (3)]
    ↳ Clavier de Dawud W Vong                 	id=10	[slave  keyboard (3)]
    ↳ HP Wide Vision HD                       	id=11	[slave  keyboard (3)]
    ↳ Intel Virtual Button driver             	id=12	[slave  keyboard (3)]
    ↳ AT Translated Set 2 keyboard            	id=14	[slave  keyboard (3)]
    ↳ HP WMI hotkeys                          	id=16	[slave  keyboard (3)]
    ↳ HP Wireless hotkeys                     	id=17	[slave  keyboard (3)]
```

## Usage examples

Here are some of the ways *xinput* can be used.

### Remove the middle and right mouse buttons

```
$ xinput set-button-map 'dougav’s mouse' 1 1 1

```