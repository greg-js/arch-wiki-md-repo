**Note:** This page previously contained some bad advice. Setting the TERM environment variable in your ~/.bashrc is a **BAD** idea. Please do not do it. Follow the advice below.

A frequent problem in command line programs is that keys like Home and End do not work as expected. This is usually because the terminal emulator sends multi-character escape codes when such keys are pressed, which the running program (such as your shell) does not know how to interpret correctly. Usually this problem can be fixed by configuring the offending program to perform the correct action when receiving certain escape codes. Thus the solution varies from program to program.

First you should check the common culprits that can affect the behavior of many programs.

## Contents

*   [1 TERM](#TERM)
*   [2 Readline](#Readline)
*   [3 Terminfo](#Terminfo)
*   [4 Other Applications](#Other_Applications)
    *   [4.1 Lynx](#Lynx)
    *   [4.2 URxvt/Rxvt](#URxvt.2FRxvt)
    *   [4.3 Zsh](#Zsh)
    *   [4.4 Less](#Less)

## TERM

The **number one cause of broken keys** is overriding the TERM environment variable to something that conflicts with your shell. All modern terminals are smart enough to set their own TERM variable, so before you go delving into program configurations ensure that you are not incorrectly overriding it (for example, in your `~/.bashrc`). Again, **do not set TERM manually - let the terminal do it.**

If you do not like the TERM value chosen by your terminal (e.g. 'xterm' when you want 'xterm-256color'), there is typically a way to configure your terminal to properly override it without changing the TERM variable.

For xterm and urxvt, you can set it in your [X resources](/index.php/X_resources "X resources")

```
XTerm*termName: xterm-256color
...
URxvt*termName: rxvt-unicode

```

For [Screen](/index.php/Screen "Screen"), you can set it in your ~/.screenrc:

```
term screen-256color

```

For [Tmux](/index.php/Tmux "Tmux"), you can set it in your ~/.tmux.conf:

```
set -g default-terminal screen-256color

```

## Readline

Many command line applications use the [Readline](/index.php/Readline "Readline") library to read input. So properly configuring Readline can fix Home and End in many cases. Readline maintains mappings for more obscure keys in `/etc/inputrc` and `~/.inputrc` for global and per-user mappings, respectively.

In the default `/etc/inputrc`, there are several lines that attempt to handle common Home/End escape codes:

```
"\e[1~": beginning-of-line
"\e[4~": end-of-line
"\e[7~": beginning-of-line
"\e[8~": end-of-line
"\eOH": beginning-of-line
"\eOF": end-of-line
"\e[H": beginning-of-line
"\e[F": end-of-line

```

If your keys are not working, it could be because your particular terminal sends escape codes not in this list. First you need to find out what escape codes are being sent. To see them, you can use a Readline command called "quoted-insert" or run the command `showkey --scancodes` which outputs the value of a key verbatim. The default binding for quoted-insert is <kbd>Ctrl</kbd>+<kbd>V</kbd>.

For example, you could give the following series of inputs in your terminal:

1.  <kbd>Ctrl</kbd>+<kbd>V</kbd>
2.  <kbd>Home</kbd>
3.  <kbd>Spacebar</kbd>
4.  <kbd>Ctrl</kbd>+<kbd>V</kbd>
5.  <kbd>End</kbd>

And get as output

```
$ ^[[1~ ^[[4~

```

The `^[` indicates an escape character in your shell, so this means that your Home key has an escape code of `[1~` and you End key has an escape code of `[4~`. Since these escape codes are not listed in the default Readline config, you will need to add them:

```
"\e[1~": beginning-of-line
"\e[4~": end-of-line

```

Note that Readline uses `\e` to indicate an escape character.

## Terminfo

For programs that do not use Readline (e.g. ncurses), you can try editing your terminfo to change which escape codes are sent to the terminal for certain actions.

First save your existing terminfo to a file

```
infocmp $TERM >terminfo.src

```

Then edit it to change the escape codes. For example change khome and kend:

```
khome=\E[1~, kend=\E[4~,

```

**Warning:** Ensure that no other key use the same character sequence.

Then compile the new terminfo (which saves it to your `~/.terminfo` directory)

```
tic terminfo.src

```

And lastly specify the new terminfo in your shell's environment variables

```
export TERMINFO=~/.terminfo

```

## Other Applications

If the above steps do not resolve the issue, it is probably a program-specific problem rather than a system-wide one. You may have to consult the documentation for the given program on how to fix it. Below are fixes for common programs.

### Lynx

You can add key binds using the same quoted-insert characters as used for [Readline](#Readline), but use `\033` to represent an escape character:

 `lynx.cfg` 

```
setkey "\033[1~" HOME
setkey "\033[4~" END
```

### URxvt/Rxvt

Add escape code binds to your [X resources](/index.php/X_resources "X resources") using the same escape sequence format as for [Lynx](#Lynx):

```
URxvt.keysym.Home: \033[1~
URxvt.keysym.End: \033[4~
URxvt.keysym.KP_Home: \033[1~
URxvt.keysym.KP_End:  \033[4~
```

Where KP_Home and KP_End are the numpad Home and End keys. These binds might also fix programs running within URxvt e.g. Nano.

### Zsh

In short, use the terminfo database to set the correct keybind.

 `~/.zshrc` 

```
bindkey "${terminfo[khome]}" beginning-of-line
bindkey "${terminfo[kend]}" end-of-line
```

See [Zsh#Key bindings](/index.php/Zsh#Key_bindings "Zsh") and [zshwiki: bindkeys](http://zshwiki.org/home/zle/bindkeys#reading_terminfo) for more complete information.

### Less

Create a config file using `lesskey` and the same escape codes for [Readline](#Readline):

 `$ lesskey -o .less -` 

```
#command
\e[4~ goto-end
\e[1~ goto-line

```

or for [xterm](/index.php/Xterm "Xterm") you may have to use different escape codes

 `$ lesskey -o .less -` 

```
#command
\eOF goto-end
\eOH goto-line
```