# Remind

Remind is a sophisticated calendar and alarm program. It includes the following features:

*   A sophisticated scripting language and intelligent handling of exceptions and holidays.
*   Plain-text, PostScript and HTML output.
*   Timed reminders and pop-up alarms.
*   A friendly graphical front-end for people who don't want to learn the scripting language.
*   Facilities for both the Gregorian and Hebrew calendars.
*   Support for 12 different languages.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Include](#Include)
*   [3 Usage](#Usage)
    *   [3.1 Postscript/pdf calendars](#Postscript.2Fpdf_calendars)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [remind](https://www.archlinux.org/packages/?name=remind) package, available in the [official repositories](/index.php/Official_repositories "Official repositories").

## Configuration

After installation, the user can define reminders in a remind script files (_.rem_). A good place for this files could be `~/.reminders` or `~/.config/remind`.

Here are some example reminders that could be in the remind script:

 `~/.config/remind/reminders.rem` 

```
REM Jan 1 MSG Remind every year on new years day
REM January 1 2015 MSG Remind only on new years day 2015
REM Sunday 2 MSG Remind every second Sunday
REM March Monday 1 --7 MSG remind on the last Monday of February
REM December 25 +30 MSG Christmas

```

The last particular day of a month is given by subtracting 7 days from the first day of the next month. The `+` symbol tells remind to start reminding that number of days ahead.

See also `remind(1)` [man page](/index.php/Man_page "Man page") for detailed information about configuring _remind_.

### Include

A reminder script can also include any number of external scripts. For example, a user might want to have a separate file for birthday reminders and a separate file for holidays. This can be done like so:

```
include ~/.config/remind/birthdays.rem
include ~/.config/remind/holidays.rem

```

## Usage

The simplest thing one can do with remind, is to check for reminders. Do this by passing a reminder file to _remind_:

```
remind ~/.config/remind/reminders.rem

```

This will output a list of reminders that it is scheduled to tell the user about.

To output a text based calendar, use the `-c` option:

```
remind -c1 ~/.config/remind/reminders.rem

```

This will output a text calendar for the current month. To print months in advance, replace `1` with the number of months to print.

### Postscript/pdf calendars

It is also possible to create calendars in a postscript format.

```
remind -c2 -p ~/.config/remind/reminders.rem | rem2ps > calendar.ps

```

The `-p` option makes _remind_ print output suitable for _rem2ps_. _rem2ps_ by default prints the output to standard output, so it must be redirected to a file so it can be opened by a program like _evince_.

_Postscript_ files can be converted with `ps2pdf`. Ps2pdf is provided by [ghostscript](https://www.archlinux.org/packages/?name=ghostscript) which is available in the [official repositories](/index.php/Official_repositories "Official repositories").

## See also

*   [remind(1)](http://linux.die.net/man/1/remind) — man page on die.net

Retrieved from "[https://wiki.archlinux.org/index.php?title=Remind&oldid=352614](https://wiki.archlinux.org/index.php?title=Remind&oldid=352614)"