## G300s community drivers

Install [ratslap](https://aur.archlinux.org/packages/ratslap/) for drivers for the mouse. It can change colors, binding, and even create custom macros. After installation, use the ratslap binary to change the mouse.

## How to make G300 work correctly

This Wiki page will show you how to get your G300 mouse working as desired.

G300 is recognized as both mouse and keyboard by system, you could check by execute:

```
xinput list | grep G300

```

We have to disable the G300 keyboard to make it work correctly.

Here's the code:

```
#!/bin/sh
DEVICE_ID=$(xinput list |  grep "Logitech Gaming Mouse G300" | grep keyboard | sed 's/.*id=\([0-9]*\).*/\1/')

if xinput -list-props $DEVICE_ID | grep "Device Enabled" | grep "1$" > /dev/null
then
        xinput set-int-prop $DEVICE_ID "Device Enabled" 8 0
fi

```

Simply execute the code above to see if it's working.

And you could put it into your xinitrc.d to make it load automatically.