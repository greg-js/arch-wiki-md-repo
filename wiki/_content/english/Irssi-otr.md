The [irssi-otr](http://irssi-otr.tuxfamily.org/) module brings [Off-the-Record Messaging](http://www.cypherpunks.ca/otr/) to your [favorite IRC client](http://irssi.org/).

## Contents

*   [1 Installing](#Installing)
*   [2 Usage](#Usage)
*   [3 Loading the module on startup](#Loading_the_module_on_startup)
*   [4 Stripping HTML](#Stripping_HTML)

## Installing

You can install the [irssi-otr](https://aur.archlinux.org/packages/irssi-otr/) module from the [AUR](/index.php/AUR "AUR"). If you like to test bleeding edge software, there is also [irssi-otr-git](https://aur.archlinux.org/packages/irssi-otr-git/).

## Usage

See the [README](http://git.tuxfamily.org/irssiotr/irssiotr.git/plain/README).

## Loading the module on startup

If you are tired of typing `/LOAD otr` you can put the following in your `~/.irssi/startup`:

```
LOAD otr

```

## Stripping HTML

If you are using irssi-otr with [BitlBee](/index.php/Bitlbee "Bitlbee") you will notice that some clients send you HTML formatted messages. Normally BitlBee automatically strips the HTML formatting, but since the messages are encrypted this does not work anymore. Nevertheless you can achieve the same by stripping the HTML with regular expressions using the [Trigger script](http://wouter.coekaerts.be/site/irssi/trigger). Just make sure you load the script before the otr module. You can either do this manually or again make your `~/.irssi/startup` look like this:

```
SCRIPT LOAD trigger.pl
LOAD otr

```

Also make sure that `trigger.pl` is not in `~/.irssi/scripts/autorun` since the files from this directory are loaded after `~/.irssi/startup`.

Since it is not possible to perfectly match HTML code with regular expressions we will take a somewhat conservative approach. We will only strip HTML tags we explicitly specified from PRIVMSGS from the BitlBee network, where we assume you added you server.

You can `/TRIGGER add` the following lines or copy them to `~/.irssi/triggers`.

```
-privmsgs -nocase -tags 'BitlBee' -regexp '</?(a|b|body|div|em|font|i|s|u)( +\w+=".*?")*>' -replace '' 

```

You can even make HTML line breaks look like multiple messages:

```
-privmsgs -nocase -tags 'BitlBee' -regexp '(\s*<br>\s*)+' -replace '\n�8/<�g�</$N�8/>�g �e' 

```

Where `�` is the non-printable character `^D`. In vi(m) you can get it by pressing `Ctrl-v Ctrl-d` in insert mode. If your are using a theme different than the default one you probably have to adapt the replacing string to match color and indentation.

And finally we convert some escaped HTML characters:

```
-privmsgs -nocase -tags 'BitlBee' -regexp '&amp;' -replace '&' 
-privmsgs -nocase -tags 'BitlBee' -regexp '&gt;' -replace '>' 
-privmsgs -nocase -tags 'BitlBee' -regexp '&lt;' -replace '<' 
-privmsgs -nocase -tags 'BitlBee' -regexp '&quot;' -replace '"' 

```

These are just some basic replaces, just extend them if you need more.