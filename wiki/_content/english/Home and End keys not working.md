A frequent problem in command line programs is that keys like Home and End do not work as expected. This is usually because the terminal emulator sends multi-character escape codes when such keys are pressed, which the running program (such as your shell) does not know how to interpret correctly. Usually this problem can be fixed by configuring the offending program to perform the correct action when receiving certain escape codes. Thus the solution varies from program to program.

First you should check the common culprits that can affect the behavior of many programs.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 TERM](#TERM)
*   [2 Shell prompt](#Shell_prompt)
*   [3 Readline](#Readline)
*   [4 Terminfo](#Terminfo)
*   [5 Other Applications](#Other_Applications)
    *   [5.1 Lynx](#Lynx)
    *   [5.2 URxvt/Rxvt](#URxvt/Rxvt)
    *   [5.3 Zsh](#Zsh)
    *   [5.4 Less](#Less)

## TERM

The **number one cause of broken keys** is overriding the TERM environment variable to something that conflicts with your shell. All modern terminals are smart enough to set their own TERM variable, so before you go delving into program configurations ensure that you are not incorrectly overriding it (for example, in your `~/.bashrc`). Again, **do not set TERM manually - let the terminal do it.**

If you do not like the TERM value chosen by your terminal (e.g. 'xterm' when you want 'xterm-256color'), there is typically a way to configure your terminal to properly override it without changing the TERM variable.

For xterm and urxvt, you can set it in your [X resources](/index.php/X_resources "X resources"):

```
XTerm*termName: xterm-256color
...
URxvt*termName: rxvt-unicode

```

For [GNU Screen](/index.php/GNU_Screen "GNU Screen"), you can set it in your `~/.screenrc`:

```
term screen-256color

```

For [Tmux](/index.php/Tmux "Tmux"), you can set it in your `~/.tmux.conf`:

```
set -g default-terminal screen-256color

```

## Shell prompt

Another possible reason for misbehaving Home and End keys is malformed custom shell prompt. The shell tries to calculate actual length of the prompt contained in `PS1` environment variable, but if `PS1` contains some escape sequences (e.g. for colored text), shell may assume that they are actual printable characters with non-zero length. This will obviously result in text rendering mistakes.

To avoid that, you should enclose your non-printable stuff in `PS1` with `\[` and `\]` so that shell can understand that it is actually non-printable. For example, this line in your `.bashrc`

```
PS1="\e[32m\u \e[34m\w \e[37m\$ \e[0m"

```

should become this:

```
PS1="\[\e[32m\]\u \[\e[34m\]\w \[\e[37m\]\$ \[\e[0m\]"

```

For more info, please refer to [Bash/Prompt customization](/index.php/Bash/Prompt_customization "Bash/Prompt customization").

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

If your keys are not working, it could be because your particular terminal sends escape codes not in this list. First you need to find out what escape codes are being sent. To see them, you can use a Readline command called "quoted-insert" or run the command `showkey --scancodes` which outputs the value of a key verbatim. The default binding for quoted-insert is `Ctrl+v`.

For example, you could give the following series of inputs in your terminal:

1.  `Ctrl+v`
2.  `Home`
3.  `Space`
4.  `Ctrl+v`
5.  `End`

And get as output:

```
^[[1~ ^[[4~

```

The `^[` indicates an escape character in your shell, so this means that your Home key has an escape code of `[1~` and you End key has an escape code of `[4~`. Since these escape codes are not listed in the default Readline configuration, you will need to add them:

```
"\e[1~": beginning-of-line
"\e[4~": end-of-line

```

Note that Readline uses `\e` to indicate an escape character.

## Terminfo

For programs that do not use Readline (e.g. ncurses), you can try editing your terminfo to change which escape codes are sent to the terminal for certain actions.

First save your existing terminfo to a file

```
$ infocmp $TERM > terminfo.src

```

Then edit it to change the escape codes. For example change `khome` and `kend`:

```
khome=\E[1~, kend=\E[4~,

```

**Warning:** Ensure that no other key use the same character sequence.

Then compile the new terminfo (which saves it to your `~/.terminfo` directory)

```
$ tic terminfo.src

```

And lastly specify the new terminfo in your shell's [environment variables](/index.php/Environment_variables "Environment variables"):

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

Where `KP_Home` and `KP_End` are the numpad `Home` and `End` keys. These binds might also fix programs running within URxvt e.g. [nano](/index.php/Nano "Nano").

Another solution is to add the following section to `/etc/inputrc`

```
# those two are for rxvt
"\e[7~":beginning-of-line
"\e[8~":end-of-line

```

### Zsh

Use the [terminfo(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/terminfo.5) database to set the correct key bindings, see [Zsh#Key bindings](/index.php/Zsh#Key_bindings "Zsh").

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