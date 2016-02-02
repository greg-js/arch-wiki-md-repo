# Ttytter

**ttytter** Not another Twitter client! Yes, another Twitter client. The difference here is that you're dealing with a multi-functional, fully 100% text, Perl command line client.

tytter is a twitter client for the command line

[ttytter](https://www.archlinux.org/packages/?name=ttytter)

When you start TTYtter without a keyfile, which will be the case the first time you run it, it will automatically

start an assistant to help you create the keyfile. You only need to create the keyfile once for each account. It will never expire.

TTYtter will find where your cURL is located, and if successful, you should see something like this:

[ttyter launch image](http://postimg.org/image/fthxntgv3/)

Once installed simply type

```
ttytter -dostream

```

into your command line and it will prompt you for the Oauth key, click the given URL

and type in the key which appears in your browser.

Now you should see your twitter timeline in the shell.

Note: If you use this screen name on other machines you use TTYtter on, simply copy the keyfile there

To enable ANSI colours and some other features here is a template .ttytterrc which should suffice for most users

[.ttytterrc](http://paste.debian.net/147463/) create this file in your home dir and restart ttytter to see the differences.

For a more indepth look at ttytter & its commands see the [ttytter homepage](http://www.floodgap.com/software/ttytter/#bt)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Ttytter&oldid=360642](https://wiki.archlinux.org/index.php?title=Ttytter&oldid=360642)"