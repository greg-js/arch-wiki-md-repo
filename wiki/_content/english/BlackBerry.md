BlackBerry is a line of mobile e-mail and smartphone devices developed by Canadian company BlackBerry Limited, formerly known as Research In Motion (RIM). Whilst including typical smartphone applications such as an address book, calendar and to-do lists, the BlackBerry is primarily known for its ability to send and receive Internet e-mail wherever it can access a mobile network of certain cellular phone carriers. The service is available in North America and in most European countries.

## Synchronization using Barry

**Warning:** As of 2015-09-17, these instructions are non-functional because the Barry opensync0.4x plugin will not build. [[1]](http://sourceforge.net/p/barry/mailman/barry-devel/thread/20120725215119.GA31202@foursquare.net/)

Barry is an application that provides backup and sync support for BlackBerry devices. Synchronization is provided via the [OpenSync](/index.php/OpenSync "OpenSync") library; Barry must be compiled with OpenSync support in order for synchronization with BlackBerry devices to work. The steps below show how you can synchronize your BlackBerry's contacts and calender with your [Evolution](/index.php/Evolution "Evolution") contacts and calender using Barry. In theory the same principle should be able to be applied to other mail and calendar clients including Kmail and Google calender. For more information, please see the [Net Direct website](http://www.netdirect.ca/software/packages/barry/sync.php).

### Packages required for Evolution sync

**Note:** *osynctool* is only required if you wish to sync through the command line.

*   [evolution](https://www.archlinux.org/packages/?name=evolution)
*   [osynctool](https://aur.archlinux.org/packages/osynctool/)
*   *libopensync-plugin-evolution3*
*   [barry](https://aur.archlinux.org/packages/barry/)

### Syncing using the command line

**Note:** These instructions are for syncing via the command line. Syncing can be done graphically using the *barrydesktop* application.

Create a sync group called evoberry

```
$ osynctool --addgroup evoberry

```

Add Evolution and the BlackBerry to the sync group.

```
$ osynctool --addmember evoberry evo3-sync
$ osynctool --addmember evoberry barry-sync

```

Configure the Evolution member

```
$ osynctool --configure evoberry 1

```

Change the defaults to the location of your Evolution files as shown in the example

```
<config>
<address_path>file:///home/user/.evolution/addressbook/local/system</address_path>
<calender_path>file:///home/user/.evolution/calendar/local/system</calender_path>
<tasks_path>file:///home/user/.evolution/tasks/local/system</tasks_path>
</config>

```

Configure the BlackBerry member

```
$ osynctool --configure evoberry 2

```

Change the device number to your BlackBerry pin number as shown in the example.

Finally, make sure Evolution is closed and your BlackBerry is connected and then issue the sync command.

```
$ osynctool --sync evoberry

```