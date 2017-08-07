[Twister](http://twister.net.co/) is an experimental peer-to-peer microblogging software. It's in very alpha state!

## Contents

*   [1 Installation](#Installation)
*   [2 First Time Setup](#First_Time_Setup)
*   [3 Gui Interface](#Gui_Interface)
*   [4 JSON/CLI Interface](#JSON.2FCLI_Interface)

## Installation

The [twister-core-git](https://aur.archlinux.org/packages/twister-core-git/) package and the [twister-html-git](https://aur.archlinux.org/packages/twister-html-git/) html interface are available in the AUR.

## First Time Setup

[Start/enable](/index.php/Start/enable "Start/enable") `twister.service`.

This will by default load both the twister-core daemon, and the twister-html gui.

1.  Go to [http://user:pwd@127.0.0.1:28332/home.html](http://user:pwd@127.0.0.1:28332/home.html). If authentication window pops up enter "user" and "pwd"

**Note:** The "user" and "pwd" is hard coded into the source currently and only accessible from your machine. That is why you create a new user here.

1.  Go to the Network tab and wait until the daemon downloads the entire blockchain.
2.  Go to the Login tab and create a new user.
3.  Wait a few seconds for the daemon to calculate the Proof-Of-Work to propagate your registration.
4.  You’ll be redirected to the Edit Profile tab. Choose your avatar, name, location etc.
5.  Wait a few minutes until your registration is accepted into a new block. The “Save” button will be disabled in the meantime.
6.  Your account is ready.

```
   IMPORTANT: save your secret key (this is the only way to “authorize”, there's no send me pwd by mail, …)

```

Search users to follow, send new posts etc.

```
   A great way for others to find you is by using tags, e.g. write a msg like: Hello #twister community!

```

Switch to the network tab and wait for the complete download of the blockchain. Go to the 'setup account' tab and create a new user. Wait for your registration to be finished. Edit your profile. Your profile will be set in a new block, so wait for the 'save' button to appear.

The next time you enter the page press **Login** and choose your newly created user to login.

## Gui Interface

The twister-html aur package contains a web based gui interface, which can be accessed at [http://127.0.0.1:28332/home.html](http://127.0.0.1:28332/home.html). This interface allows full configuration of Twister, and can be used to create and read posts.

## JSON/CLI Interface

Twisterd comes with a command line based utility, that can be used run and configure twister. However, this interface is an overlay on the JSON-RPC interface, and therefore is mostly useful for debugging and development. See the following page for the full documentation of this interface [http://twister.net.co/?page_id=58](http://twister.net.co/?page_id=58).