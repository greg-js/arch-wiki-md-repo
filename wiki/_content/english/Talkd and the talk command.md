The "talk" command allows you to talk to other users on the same system, which is useful if you're both SSH'd in from somewhere. Using it is very simple; to talk to someone the command is just

 `$ talk <username> <tty>` 

Of course, you can talk to users on another system as well:

 `$ talk <username>@<hostname> <tty>` 

In either case, the tty is optional. It is used if you wish to talk to a local user who is logged in more than once to indicate the appropriate terminal name. "tty" is of the form 'ttyXX', or 'pts/X'.

## Setup

### Using xinetd

1.  First, install the inetutils package, which contains talk and talkd. These also rely on xinetd, so install that as well. You might also need the screen command; it's in the screen package.
2.  [Install](/index.php/Install "Install") [inetutils](https://www.archlinux.org/packages/?name=inetutils), [xinetd](https://www.archlinux.org/packages/?name=xinetd) and [GNU Screen](/index.php/GNU_Screen "GNU Screen").
3.  Configure the xinetd service entry by editing `/etc/xinetd.d/talk` and setting "disable = no".
4.  If you are using tcp_wrappers or something similar, add an entry to `/etc/hosts.allow`: `talkd: 127.0.0.1` 
5.  Now [start](/index.php/Start "Start") `xinetd.service`.
6.  If you are on the local system, you might need to start a screen session to make yourself show up on the "w" and "who" commands -- you need to show up there or talk won't work.
7.  Allow write access in your terminal if needed: `$ mesg y` 

### Using systemd directly

[Start](/index.php/Start "Start") `talk.socket` and `talk.service`.