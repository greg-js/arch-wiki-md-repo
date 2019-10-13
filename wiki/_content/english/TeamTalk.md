From [Wikipedia:TeamTalk](https://en.wikipedia.org/wiki/TeamTalk "wikipedia:TeamTalk"):

	TeamTalk is a conferencing system which people use to communicate on the Internet using VoIP and video streaming.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 Client](#Client)
    *   [1.2 Server](#Server)
*   [2 Server configuration and startup](#Server_configuration_and_startup)
    *   [2.1 Configuration](#Configuration)
    *   [2.2 First startup](#First_startup)
    *   [2.3 Regular startup](#Regular_startup)
    *   [2.4 Changing configuration options manually](#Changing_configuration_options_manually)
    *   [2.5 See also](#See_also)

## Installation

### Client

[Install](/index.php/Install "Install") the [teamtalk](https://aur.archlinux.org/packages/teamtalk/) package. It is the same package for the server. But the client files will be under the pkgsrc/srcdir/client directory. The client can be invoked by running ./run.sh.

### Server

Install the [teamtalk](https://aur.archlinux.org/packages/teamtalk/) package.

## Server configuration and startup

### Configuration

*   Teamtalk comes with a configuration script in the server binary, `tt5srv`.

Just execute `tt5srv -wizard` and follow the steps. This makes the file in `/etc/teamspeak/tt5srv.xml` initially. Minor edits can be made to this file later. The usernames/passwords and other configuration options are stored in plaintext, so you may want to `chmod 0600` the configuration file with `chown teamtalk`. Also the connection by default is not SSL/TLS enabled.

Teamtalk also has a facebook capability, which allows the user to enter `facebook` into the username box on the client. To configure this feature on the server, an option will show up to create a generic `facebook` user to authenticate using facebook's network creating a profile for each facebook user on teamtalk directly from facebook. It will be created like a normal user and ACLs. An internet connection with DNS is required (if only using a local lan server) to use facebook's auth challenge which will alleviate having to administrate users. However, a username can be used over and over again with multiple connections to the server, but this can also be restricted per user.

To enable file sharing, it can be given a storage directory in the wizard. It needs to be a directory that the `teamtalk` user has access to. A quota seems to be enforced by the wizard, making disabling a quota more difficult. This might actually be a benefit to keep down spamming and only using the server for temporary storage until everyone has received the file. The file uploader can delete the file share when finished.

IPv6 support is available and needs to be a specified listening address, but if IPv6 is not being used can be simply ignored.

The IP port for teamtalk is `10333`, but is flexible to other port numbers/assignments and can also be changed through the wizard or manually edited configuration file.

### First startup

You will need to configure at least one user through the server wizard to be able to use the client. Facebook functionality is enabled by creating a special facebook user through the wizard. Then you can

*   [Start](/index.php/Start "Start") the `tt5srv` service.

*   To find the privilege key:

There is not a privilege key like there is with [TeamSpeak](/index.php/TeamSpeak "TeamSpeak") or [Mumble](/index.php/Mumble "Mumble"). You create users with the server wizard directly without using the client program. An admin user can use the client program like in Mumble to assign ACLs. By default, most users will be able to do most things that a common user will need to be able to do in a conference including creating temporary rooms, sharing video, files or desktops. Desktop sharing doesn't appear to be working on Linux.

### Regular startup

*   Simply [enable](/index.php/Enable "Enable") the `tt5srv` service.

### Changing configuration options manually

*   Most likely remember to restart the `tt5srv` service. Using the client admin function is usually more preferable for user administration, but other options are configured through manual edits or the server wizard. Using the facebook login function may save administrative maintainence, but may not be desirable. Reusing users may not be desirable either.

### See also

*   [Official website](https://www.bearware.dk)