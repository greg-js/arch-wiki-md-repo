Xorg servers starting from version 1.7 have a feature called "multi-pointer". Basically it allows to have multiple mouse cursors (each with its own keyboard focus) on the screen and control them with separate physical input devices. It can be used as a crude [multiseat](/index.php/Xorg_multiseat "Xorg multiseat") solution.

## Contents

*   [1 Basic concepts](#Basic_concepts)
    *   [1.1 Master and slave devices](#Master_and_slave_devices)
    *   [1.2 Client pointer](#Client_pointer)
*   [2 Configuration](#Configuration)
    *   [2.1 configuration file](#configuration_file)
    *   [2.2 xinput utility](#xinput_utility)
*   [3 Software support](#Software_support)
    *   [3.1 Window managers](#Window_managers)
*   [4 Useful links](#Useful_links)

## Basic concepts

### Master and slave devices

With the introduction of XInput2, input devices are organised in a two-level hierarchy:

*   Master devices, which correspond to cursors on the screen
*   Slave devices, which correspond to physical input devices

Master devices come in pairs, one for pointer and one for keyboard. Each master device can have a number of slave devices attached, so that cursor of a master device can be controlled by all slave devices attached to it.

### Client pointer

When an application grabs input (e.g. a fullscreen game), it grabs a master device that is set as its client pointer. By default, the client pointer is set to "Virtual core pointer", but it can be set to a different one with a "xinput" utility.

## Configuration

### configuration file

**Note:** Information how to configure multipointer with `xorg.conf` should be added

### xinput utility

More pointers can be added with `xinput` CLI utility. Here is how to do it:

Create a new pair of master devices named "_name_ pointer" and "_name_ keyboard":

```
xinput create-master _[name]_

```

Find out names and ids of existing slave devices:

```
xinput list

```

Reattach slave devices to newly created master devices:

```
xinput reattach _[slave device name or id]_ _[master device name or id]_

```

For example, say we create a device called "Auxiliary":

```
xinput create-master Auxiliary

```

When we list the xinput devices you should see something like this:

```
Virtual core pointer
  >Virtual Core XTEST pointer
  >[probably your main mouse]
Virtual core keyboard
  >Virtual Core XTEST pointer
  >[probably your main keyboard]
  >[other function buttons]
Auxiliary pointer
  >auxiliary XTEST pointer
Auxiliary keyboard
  >auxiliary XTEST keyboard

```

What you then want to do is simply attach your secondary mouse and keyboard to the respective auxiliary positions. The XTEST devices are irrelevant here. I found the easiest way to determine whats what was to just unplug stuff and type "xinput list" again.

To attach devices, you type:

```
xinput reattach [device id #] "Auxiliary pointer"

```

and then do so for your keyboard as well!

Shamelessly stolen from [Antonio Ospite at ao2.it](http://ao2.it/en/blog/2010/01/19/poor-mans-multi-touch-using-multiple-mice-xorg)

## Software support

It is possible to use multi-pointer with software that doesn't explicitly support it, but with limited functionality. Applications which do not support it won't distinguish between multiple pointers and will interpret all actions as if done by single master device pair.

### Window managers

In window managers multi-pointer support could mean:

*   recognizing multiple focuses
*   setting the client pointer of a focused window to the pointer that "focused" it
*   letting move and resize windows simultaneously

As of 26 September 2010, none of major window managers support multi-pointer.

## Useful links

*   [Xorg wiki article](http://www.x.org/wiki/Development/Documentation/MPX)
*   [Xorg multiseat](/index.php/Xorg_multiseat "Xorg multiseat"). A how-to for a more complicated multi-user environment. Requires 2 different xorg sessions and graphics cards!!