[Emacs](https://en.wikipedia.org/wiki/Emacs "wikipedia:Emacs") is an extensible, customizable, self-documenting real-time display editor. At the core of Emacs lies an [Emacs Lisp](https://en.wikipedia.org/wiki/Emacs_Lisp "wikipedia:Emacs Lisp") interpreter, the language in which the majority of Emacs' built-in functionality and extensions are implemented. GTK is the default X toolkit used as of GNU Emacs 22, though it functions equally well within a CLI environment. The text-editing capabilities of Emacs are often compared to that of [vim](/index.php/Vim "Vim").

## Contents

*   [1 Installation](#Installation)
*   [2 Running Emacs](#Running_Emacs)
    *   [2.1 Normal way](#Normal_way)
    *   [2.2 No Colors](#No_Colors)
    *   [2.3 As a daemon](#As_a_daemon)
    *   [2.4 As a systemd unit](#As_a_systemd_unit)
*   [3 Usage](#Usage)
    *   [3.1 The manuals](#The_manuals)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 TRAMP](#TRAMP)
    *   [4.2 Using Emacs as git mergetool](#Using_Emacs_as_git_mergetool)
    *   [4.3 Using Caps Lock as Control key](#Using_Caps_Lock_as_Control_key)
    *   [4.4 Multiplexing emacs and emacsclient](#Multiplexing_emacs_and_emacsclient)
    *   [4.5 Multiple configurations](#Multiple_configurations)
    *   [4.6 Local and custom variables](#Local_and_custom_variables)
    *   [4.7 Custom colors and theme](#Custom_colors_and_theme)
    *   [4.8 SyncTeX support](#SyncTeX_support)
    *   [4.9 Syntax highlighting for systemd Files](#Syntax_highlighting_for_systemd_Files)
    *   [4.10 Clipboard support for emacs-nox](#Clipboard_support_for_emacs-nox)
*   [5 Extensions](#Extensions)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 Colored output issues](#Colored_output_issues)
    *   [6.2 Menus appear empty](#Menus_appear_empty)
    *   [6.3 Problems displaying characters in X Windows](#Problems_displaying_characters_in_X_Windows)
    *   [6.4 Slow startup](#Slow_startup)
    *   [6.5 Cannot open load file: ...](#Cannot_open_load_file:_...)
    *   [6.6 Dead-accent keys problem: '<dead-acute> is undefined'](#Dead-accent_keys_problem:_.27.3Cdead-acute.3E_is_undefined.27)
    *   [6.7 C-M-% and some other bindings do not work in emacs nox](#C-M-.25_and_some_other_bindings_do_not_work_in_emacs_nox)
    *   [6.8 Emacs client gets stuck when switching back to it](#Emacs_client_gets_stuck_when_switching_back_to_it)
    *   [6.9 Emacs-nox output gets messy](#Emacs-nox_output_gets_messy)
    *   [6.10 Shift + Arrow keys not working in emacs within tmux](#Shift_.2B_Arrow_keys_not_working_in_emacs_within_tmux)
    *   [6.11 Improper window resizing in KDE](#Improper_window_resizing_in_KDE)
    *   [6.12 Invalid font name for Oxygen-Sans](#Invalid_font_name_for_Oxygen-Sans)
    *   [6.13 Slow startup if helm-mode is enabled](#Slow_startup_if_helm-mode_is_enabled)
*   [7 Alternatives](#Alternatives)
    *   [7.1 mg](#mg)
    *   [7.2 zile](#zile)
    *   [7.3 uemacs](#uemacs)
*   [8 See also](#See_also)

## Installation

Emacs comes in several variants (sometimes referred to as *emacsen*). The most common of these is [GNU Emacs](http://www.gnu.org/software/emacs/).

[Install](/index.php/Install "Install") [emacs](https://www.archlinux.org/packages/?name=emacs), available in the [official repositories](/index.php/Official_repositories "Official repositories"). If you usually work in a terminal, you may prefer the [emacs-nox](https://www.archlinux.org/packages/?name=emacs-nox) variant without GTK+ (nor sound and other fancy stuff). Be aware that the text version comes with some drawbacks: it supports less colors and less features for font handling (size change in live, various sizes in one document, and so on). Besides, emacs-nox has some limitation with advanced features like the Speedbar or GUD (the debugging environment), and is somewhat slower when handling complex faces (a "face" is the visual appearance of text in Emacs).

If you want to fully enjoy all the extended features of Emacs without installing a daunting amount of dependencies, you can use the PKGBUILD to customize your needs. Using anything else than `gtk3` you can get rid of gconf. Image and sound support can be disabled as well. Run `./configure --help` in Emacs source folder to list all available options.

 `PKGBUILD` 
```
# ...
  ./configure --prefix=/usr --sysconfdir=/etc --libexecdir=/usr/lib \
    --localstatedir=/var --with-x-toolkit=gtk2 --with-xft \
    --without-gconf --without-sound
# ...

```

Another common variant is [xemacs](https://www.archlinux.org/packages/?name=xemacs).

## Running Emacs

Before launching emacs, you should know how to close it (especially if you run it in a terminal): use the `Ctrl+x``Ctrl+c` key sequence.

### Normal way

To start Emacs run:

```
$ emacs

```

or, to use it from the console:

```
$ emacs -nw

```

or, for fast loading (no .emacs) and editing within CLI:

```
$ emacs -Q -nw

```

If you installed the nox version, 'emacs' and 'emacs -nw' will be the same.

A file name can also be provided to open that file immediately:

```
$ emacs filename.txt

```

### No Colors

By default, Emacs starts with a color theme showing hyperlinks in dark blue. To start Emacs without any color theme or scheme:

```
$ emacs -nw --color=no

```

This will cause all text to appear in white color only.

### As a daemon

Emacs can take some time to start since it has to load the `.emacs` file each time. Besides, you may want to access the same files from different instances. Since version 23, Emacs is able to run as a daemon to which users can connect. To run Emacs as a daemon:

```
$ emacs --daemon

```

You are likely to start the daemon at startup time and to connect a window to the daemon. Besides, it is possible to connect *both* graphical and console clients to the daemon at the same time and make the GUI to start quickly.

If you want to connect to the daemon simply use the following command (note that it will start a graphical client if called in a graphical environment or a console client if called in a console like a tty):

```
$ emacsclient

```

If you merely want a console client despite being in a graphical environment then use:

```
$ emacsclient -t

```

Furthermore, you can add the `-a ""` parameter. Now, the first time you call the command, it will start emacs as a daemon, so that it remains running in background and so improving startup times for future calls (and to remember buffers as well).

If you start the client from a terminal or another program, you may want not to wait for it to return, so that you can continue using the calling program and even close it without closing the Emacs client. To do so, start the client with the `-n` (`--no-wait`) parameter:

```
$ emacsclient -nc

```

Note that some programs such as Mutt or Git (for commit messages) wait for the editor to finish, so you cannot use the `-n` parameter. If your default editor is set to use it, you will have to specify an alternate editor (*e.g.* `emacsclient -a "" -t`) for those programs.

You could use the following shell configuration:

```
alias emt='emacsclient -nc -a ""'
alias emc='emacsclient -t -a ""'
EDITOR='emacsclient -a ""'
```

but it has some caveats: many program will fail to load the external editor because of the spaces in the command.

A more convenient and reliable solution is to write your own script:

 `/usr/local/bin/emc` 
```
#!/bin/sh
if [ -z "$DISPLAY" ]; then
    IS_GRAPHICAL=true
else
    IS_GRAPHICAL=$(emacs --batch -Q --eval='(if (fboundp '"'"'tool-bar-mode) (message "true") (message "false"))' 2>&1)
fi

if $IS_GRAPHICAL; then
    emacsclient -a "" -nc "$@"
else
    emacsclient -a "" -t "$@"
fi

```

then make it executable:

```
# chmod 755 /usr/local/bin/emc

```

Now 'emc' will work just as expected. Setting the `EDITOR` environment variable to the aforementionned script should suffice to make the client be your defaut editor.

### As a systemd unit

The old system unit method had some caveats. It gave a limited shell environment which restricted shell calls, so we'll be using a user unit, which tends to work a lot better than naively calling *emacs --daemon*.

Create a systemd unit for emacs:

 `~/.config/systemd/user/emacs.service` 
```
[Unit]
Description=Emacs: the extensible, self-documenting text editor

[Service]
Type=forking
ExecStart=/usr/bin/emacs --daemon
ExecStop=/usr/bin/emacsclient --eval "(kill-emacs)"
Restart=always

[Install]
WantedBy=default.target

```

You need to enable the unit so that it gets started on every boot (note - DO *NOT* run these commands as root - we want them for our user, not for the root user):

```
$ systemctl --user enable emacs

```

To actually use the unit, either reboot or start the unit manually:

```
$ systemctl --user start emacs

```

## Usage

Although Emacs is complex, it will not take long to begin to understand the benefits which the level of customization and extensibility bring. Furthermore, the comprehensive variety of extensions already available allows it to be transformed into a powerful environment for almost any form of text-editing.

Emacs has an excellent built-in tutorial which can be accessed by clicking the first link on the splash screen; by selecting *Help->Emacs Tutorial* from the menu or by pressing 'F1' followed by 't'.

Emacs is self-documenting by design. As such, a great deal of information is available to determine the name of a specific command or its keybinding, for example. See all contextual help bindings with **C-h C-h**.

Emacs also includes a set of reference cards, useful for beginners and experts alike, see `/usr/share/emacs/<version>/etc/refcards/` (substitute <version> for your version of emacs).

Emacs empowers the users with a tremendous amount of features, including: keyboards macros, rectangular regions, whitespace cleanup, bookmarks, desktop session, various shells, spell checking, tables, semantic analysis...

### The manuals

If you really want to master Emacs, the most recommended source of documentation remains the official manuals:

*   Emacs: the complete Emacs user manual.
*   Emacs FAQ.
*   Emacs Lisp Intro: if you never used any programming language before.
*   Elisp: if you are already familiar with a programming language.

You can access it as PDFs from [GNU.org](http://www.gnu.org/software/emacs/manual/) or directly from Emacs itself thanks to the embedded 'info' reader: **C-h i**. Press **m** to choose a book.

Some users prefer to read books using 'info' because of its convenient shortcuts, its paragraphs adapting to window width and the font adapted to current screen resolution. Some find it less irritating to the eyes. Finally you can easily copy content from the book to any Emacs buffer, and you can even execute Lisp code snippets directly from the examples.

You may want to read the **Info** book to know more about it: **C-h i m info <RET>**. Press **?** while in info mode for a quick list of shortcuts.

## Tips and tricks

### TRAMP

**Warning:** Using TRAMP with root permissions will cause `/dev/null` to be deleted after some time. [FS#47912](https://bugs.archlinux.org/task/47912) To prevent this, use the patch provided in the bug report, or replace `/bin/sh` with a link to `/bin/dash`. See [Dash#Relinking /bin/sh](/index.php/Dash#Relinking_.2Fbin.2Fsh "Dash").

TRAMP (Transparent Remote Access, Multiple Protocols) is an extension which, as its name suggests, provides transparent access to remote files across a number of protocols. When prompted for a filename, entering a specific form will invoke TRAMP. Some examples:

To prompt for the root password before opening /etc/hosts with root permissions:

```
C-x C-f /su::/etc/hosts

```

To connect to 'myhost' as 'myuser' via SSH and open the file ~/example.txt:

```
C-x C-f /ssh:myuser@myhost:~/example.txt

```

The path for TRAMP is typically of the form '/[protocol]:[[user@]host]:<file>'. TRAMP supports much more than the examples above might indicate. For more information refer to the TRAMP info manual, which is distributed with Emacs.

### Using Emacs as git mergetool

By default, Git provides support for using Emacs' Emerge mode as a merge tool. However you may prefer the Ediff mode. Unfortunately this mode is not supported by git for technical reasons. There is still a way to use it by evaluating some elisp code upon emacs call.

 `.gitconfig` 
```
[mergetool.ediff]
    cmd = emacs --eval \" (progn (defun ediff-write-merge-buffer () (let ((file ediff-merge-store-file)) (set-buffer ediff-buffer-C) (write-region (point-min) (point-max) file) (message \\\"Merge buffer saved in: %s\\\" file) (set-buffer-modified-p nil) (sit-for 1))) (setq ediff-quit-hook 'kill-emacs ediff-quit-merge-hook 'ediff-write-merge-buffer) (ediff-merge-files-with-ancestor \\\"$LOCAL\\\" \\\"$REMOTE\\\" \\\"$BASE\\\" nil \\\"$MERGED\\\"))\" 

[merge]
	tool = ediff

```

Note that the command has to be on a single line. In the above example, we launch a new instance of Emacs. You might want to use emacsclient for quicker startup; it is not recommended though since the Ediff call is not really clean: it could mess with your current Emacs session.

If you want an instant startup you can use the **-q** parameter. If you want to launch Emacs quickly while preserving at least a part of your configuration, you can call Emacs with

```
 emacs -q -l ~/.emacs-light

```

where the light configuration file loads only what you need for Ediff.

See [kerneltrap.org](http://kerneltrap.org/mailarchive/git/2007/7/1/250424) and [stackoverflow](http://stackoverflow.com/questions/1817370/using-ediff-as-git-mergetool) for more details on this trick and the Ediff issue.

### Using Caps Lock as Control key

Some users like this behavior to avoid the so-called 'emacs pinky'. If you want to try it on X, just run

```
$ setxkbmap -option 'ctrl:nocaps'

```

Alternatively, to **swap** these keys, run

```
$ setxkbmap -option 'ctrl:swapcaps'

```

To set this permanently, consider adding it to your `.xinitrc` file.

Now, if you ever need to upcase an region, just use the default `C-x C-u` keybinding, which calls the `upcase-region` function.

See [[1]](http://ergoemacs.org/emacs/swap_CapsLock_Ctrl.html) for an alternative approach.

If you are missing your Caps Lock function, map it as both "Shift" at same time.

```
$ setxkbmap -option "shift:both_capslock"

```

### Multiplexing emacs and emacsclient

Opening a new file in the same `emacs-session` requires the use of `emacsclient`. `emacs` command can be itself wrapped to do the smarter job to open the file if the session exists.

To start session you need to `start-server`. This snippet will create server in first session of emacs. Add this to your `emacs` configuration file.

 `.emacs or .emacs.d/init.el` 
```
(require 'server)
(unless (server-running-p)
  (server-start))

```

Shell alias method is not adequate for this since you also need to pass variables or start the independent session of your own. Add this to the `.bashrc` or any rc file of your shell. This will make your `$ emacs` command behave like emacsclient if the argument is passed.

```
function emacs {
    if [[ $# -eq 0 ]]; then
        /usr/bin/emacs # "emacs" is function, will cause recursion
        return
    fi
    args=($*)
    for ((i=0; i <= ${#args}; i++)); do
        local a=${args[i]}
        # NOTE: -c for creating new frame
        if [[ ${a:0:1} == '-' && ${a} != '-c' ]]; then
            /usr/bin/emacs ${args[*]}
            return
        fi
    done
    setsid emacsclient -n -a /usr/bin/emacs ${args[*]}
} 

```

If you want to run the it in new session just do `emacs <file> -`.

### Multiple configurations

You can use several configurations and tell Emacs to load one or the other.

For example, let's define two configuration files.

 `.emacs` 
```
(load "~/.emacs.d/main" nil t)
(load "~/.emacs.d/functions" nil t)
(load "~/.emacs.d/modes" nil t)
(load "~/.emacs.d/plugins" nil t)
(load "~/.emacs.d/theme" nil t)

```

This is the full configuration we load for the daemon. But the *plugins* file is huge and slow to load. If we want to spaqn a new Emacs instance that does not need the *plutings* features, it can be cumbersome to load it everytime in the long time.

 `.emacs-light` 
```
(load "~/.emacs.d/main" nil t)
(load "~/.emacs.d/functions" nil t)
(load "~/.emacs.d/modes" nil t)
(load "~/.emacs.d/theme" nil t)

```

And now we launch Emacs with

```
emacs -q -l ~/.emacs-light

```

You can create an alias to ease the call.

### Local and custom variables

You can define variables in your configuration file that can be later one modified locally for a file.

```
(defcustom my-compiler "gcc" "Some documentation")

```

Now in any file you can define local variables in two ways:

*   On the very first line, write

```
// -*- my-compiler:g++; mode:c++ -*-

```

*   If you cannot (or do not want to) write this on the first line, you can put it at the end:

```
// Local Variables:
// my-compiler: g++
// mode: c++
// End:

```

Note that the beginning characters need to be comments for the current language, that's why here we used two backslashes for C++. For Elisp you would use

```
;; -*- mode:emacs-lisp -*-

```

There is two functions that may help you in defining the variables: *add-file-local-variable* and *add-file-local-variable-prop-line*.

Finally, custom variable are considered insecure by default. If you try to open a file that contains local variable redefining insecure custom variables, Emacs will ask you for confirmation.

If you know what you are doing, you can declare the variable as secure, thus removing the Emacs prompt for confirmation. You need to specify a predicate that any new value has to verify so that it can be considered safe.

```
(defcustom my-compiler "gcc" "Some documentation" :safe 'stringp)

```

In the previous example, if you attempt to set anything else than a string, Emacs will consider it insecure.

### Custom colors and theme

Colors can be easily customized using the *face* facility.

```
(set-face-background  'region                 "color-17")
(set-face-foreground  'region                 "white")
(set-face-bold-p      'font-lock-builtin-face t ) 

```

You can have let Emacs tell you the name of the face where the point is. Use the *customize-face* function for that. The facility will show you how to set colors, bold, underline, etc.

Emacs in console can handle 256 colors, but you will have to use an appropriate terminal for that. For instance URxvt has support for 256 colors. You can use the *list-colors-display* for a comprehensive list of supported colors. This is highly terminal-dependent.

### SyncTeX support

Emacs is a powerful LaTeX editor. This is mostly due to the fact you can adapt or create a LaTeX mode to fit your needs best.

Still, there might be some challenges, like SyncTeX support. First you need to make sure your TeX distribution has it. If you installed TeX Live manually, you may need to install the *synctex* package.

```
# umask 022 && tlmgr install synctex

```

SyncTeX support is viewer-dependent. Here we will use Zathura as an example, so the code needs to be adapted if you want to use another PDF viewer.

```
(defcustom tex-my-viewer "zathura --fork -s -x \"emacsclient --eval '(progn (switch-to-buffer  (file-name-nondirectory \"'\"'\"%{input}\"'\"'\")) (goto-line %{line}))'\"" 
  "PDF Viewer for TeX documents. You may want to fork the viewer
so that it detects when the same document is launched twice, and
persists when Emacs gets closed.

Simple command:

  zathura --fork

We can use

  emacsclient --eval '(progn (switch-to-buffer  (file-name-nondirectory \"%{input}\")) (goto-line %{line}))'

to reverse-search a pdf using SyncTeX. Note that the quotes and double-quotes matter and must be escaped appropriately."
:safe 'stringp)

```

Here we define our custom variable. If you are using AucTeX or Emacs default LaTeX-mode, you will have to set the viewer accordingly.

Now open a LaTeX source file with Emacs, compile the document, and launch the viewer. Zathura will spawn. If you press `Ctrl+Left click` Emacs should place the point at the corresponding position.

### Syntax highlighting for systemd Files

You can use [systemd-mode](https://github.com/holomorph/systemd-mode).

Alternatively, you can simply tell emacs to colour systemd files (services, timer, etc.), by adding this to your init file:

```
 (add-to-list 'auto-mode-alist '("\\.service\\'" . conf-unix-mode))
 (add-to-list 'auto-mode-alist '("\\.timer\\'" . conf-unix-mode))
 (add-to-list 'auto-mode-alist '("\\.target\\'" . conf-unix-mode))
 (add-to-list 'auto-mode-alist '("\\.mount\\'" . conf-unix-mode))
 (add-to-list 'auto-mode-alist '("\\.automount\\'" . conf-unix-mode))
 (add-to-list 'auto-mode-alist '("\\.slice\\'" . conf-unix-mode))
 (add-to-list 'auto-mode-alist '("\\.socket\\'" . conf-unix-mode))
 (add-to-list 'auto-mode-alist '("\\.path\\'" . conf-unix-mode))
 (add-to-list 'auto-mode-alist '("\\.netdev\\'" . conf-unix-mode))
 (add-to-list 'auto-mode-alist '("\\.network\\'" . conf-unix-mode))
 (add-to-list 'auto-mode-alist '("\\.link\\'" . conf-unix-mode))
 (add-to-list 'auto-mode-alist '("\\.automount\\'" . conf-unix-mode))

```

### Clipboard support for emacs-nox

To use the [Xorg](/index.php/Xorg "Xorg") clipboard in emacs-nox, [install](/index.php/Install "Install") [xclip](https://www.archlinux.org/packages/?name=xclip) and add the following function to `~/.emacs` [[2]](https://lists.gnu.org/archive/html/help-gnu-emacs/2014-08/msg00189.html)

```
;; use xclip to copy/paste in emacs-nox
(unless window-system
  (when (getenv "DISPLAY")
    (defun xclip-cut-function (text &optional push)
      (with-temp-buffer
	(insert text)
	(call-process-region (point-min) (point-max) "xclip" nil 0 nil "-i" "-selection" "clipboard")))
    (defun xclip-paste-function()
      (let ((xclip-output (shell-command-to-string "xclip -o -selection clipboard")))
	(unless (string= (car kill-ring) xclip-output)
	  xclip-output )))
    (setq interprogram-cut-function 'xclip-cut-function)
    (setq interprogram-paste-function 'xclip-paste-function)
    ))
```

**Tip:** You may also enable terminal mouse support by adding:
```
;; xterm mouse support
(require 'mouse)
(xterm-mouse-mode t)
```
See also [mwheel.el](http://www.opensource.apple.com/source/emacs/emacs-51/emacs/lisp/mwheel.el).

## Extensions

Emacs includes hundreds of modes, libraries and other extensions, with many more available to further Emacs' capabilities. Most of these come with instructions detailing any changes needed to be made in `~/.emacs`. These instructions are generally found in the comment block at the beginning of an elisp source file, or in a README (or similar), should the extension consist of multiple source files.

You can use the [Emacs Lisp Package Archive (ELPA)](http://tromey.com/elpa/) to automatically install packages. See the manual for instructions. ELPA is included with Emacs 24 and above; it is an accepted part of the Emacs ecosystem. Also, check out the [Marmalade](http://marmalade-repo.org/) and [MELPA](http://melpa.milkbox.net/) repos.

**Tip:** Use `M-x list-packages` to get a list of available packages for installation.

A number of popular extensions are available as packages in the 'community' repository, and more still, via [AUR](/index.php/AUR "AUR"). The name of such packages have a 'emacs-' prefix (for example, emacs-lua-mode). In many cases, the changes which need to be made in `~/.emacs` are shown during the installation of the package.

You can load extensions using the *require* function. For instance

```
(require 'mediawiki)

```

If you try using the same configuration file on a machine where the extension is not installed, Emacs will primpt for an error. Besides, all extension-specific code would be parsed for nothing.

The trick is to test the return value of *require*:

```
(when (require 'mediawiki nil t)
  (setq mediawiki-site-alist
        '(("ArchLinux" "[https://wiki.archlinux.org/](https://wiki.archlinux.org/)" "UserName" "" "Main Page")))
  (setq mediawiki-mode-hook
        (lambda ()
          (visual-line-mode 1)
          (turn-off-auto-fill)))))

```

Should instructions describing how to activate a specific extension not be available in the aforementioned location(s), check for a corresponding page in the [Emacs Wiki](http://emacswiki.org/), which will almost certainly provide an example configuration. The Emacs Wiki is also an excellent resource for discovering even more extensions.

**Tip:** A few popular extensions worth checking out: AucTeX, auto-complete, company, el-doc, emms, helm, Magit, multiple-cursors, Org-mode, Projectile, yasnippet.

Since we are at it, you may be a contributor to Arch Linux Wiki, or any Mediawiki-based website. Then emacs will become your best friend thanks to the [Emacs Mediawiki](/index.php/Emacs_Mediawiki "Emacs Mediawiki") extension. Check the dedicated page for more details.

## Troubleshooting

### Colored output issues

By default, the Emacs shell will show raw escape sequences used to print colors. In other words, it will display strange symbols in place of the desired colored output.

Including the following into `~/.emacs` amends the problem:

```
(add-hook 'shell-mode-hook 'ansi-color-for-comint-mode-on)

```

### Menus appear empty

A bug exists in GNU Emacs 23.1 (using the GTK toolkit) which may cause some menus to appear empty. This appears to be fixed in Emacs' CVS trunk. The corresponding [Debian bug report](http://bugs.debian.org/cgi-bin/bugreport.cgi?bug=550541) contains a workaround.

### Problems displaying characters in X Windows

If when you start emacs in X windows all the characters in the main window are white boxes with black borders (the ones you see if you try to view characters for which you do not have the correct font installed), you need to install [xorg-fonts-75dpi](https://www.archlinux.org/packages/?name=xorg-fonts-75dpi) and/or [xorg-fonts-100dpi](https://www.archlinux.org/packages/?name=xorg-fonts-100dpi) and restart X windows.

### Slow startup

Slow startup times are often caused by one of two things.

To determine which it might be, run Emacs with:

```
$ emacs -q

```

*   Mistakes, particularly in /etc/hosts, will often result in a 5+ second delay when starting Emacs. Refer to '[set the hostname](/index.php/Configuring_network#Set_the_hostname "Configuring network")' in the network configuration guide for information.

*   You may need to monitor any network packets sent from your computer (using a program like Wireshark) to see if there is any strange behavior.

*   A simple way to search for the cause is to comment-out (i.e., prefix lines with ';') suspect sections of your `~/.emacs` (or `~/.emacs.d/init.el`) then start Emacs again to see if there's any change. Keep in mind use of "require" and "load" can slow the startup down, especially when used with larger extensions. They should, as a rule, only be used when their target is either: needed once Emacs starts or provides little more than "autoloads" for an extension. Otherwise, use the 'autoload function directly. For example, instead of:

```
(require 'anything)

```

you might use:

```
(autoload 'anything "anything" "Select anything" t)

```

### Cannot open load file: ...

The most common cause of this error is the 'load-path' variable not including the path to the directory within which the extension is located. To solve this, add the appropriate path to the list to be searched prior to attempting to load the extension:

```
 (add-to-list 'load-path "/path/to/directory/")

```

When attempting to use packages for extensions and Emacs has been configured with a prefix other than '/usr', the load-path will need to be updated. Place the following in `~/.emacs` prior to the instructions provided by the package:

```
 (add-to-list 'load-path "/usr/share/emacs/site-lisp")

```

If compiling Emacs by hand, keep in mind that the default prefix is '/usr/local'.

### Dead-accent keys problem: '<dead-acute> is undefined'

Searching about this bug on Google, we find this link: [http://lists.gnu.org/archive/html/help-gnu-emacs/2009-05/msg00167.html](http://lists.gnu.org/archive/html/help-gnu-emacs/2009-05/msg00167.html)

Explaining the problem: in recent versions of b72

```
Emacs, the normal way to use accent keys doesn't work as expected. Trying to accent a word like 'fiancé' will produce the message above.

```

A way to solve it is just put the line above on your startup file, `~/.emacs`:

```
  (require 'iso-transl)

```

And no, it isn't a bug, but a feature of new Emacs versions. Reading the subsequent messages about it on the mail list, we found it ([http://lists.gnu.org/archive/html/help-gnu-emacs/2009-05/msg00179.html](http://lists.gnu.org/archive/html/help-gnu-emacs/2009-05/msg00179.html)):

	*It seems that nothing is loaded automatically because there is a choice betwee iso-transl and iso-acc. Both seem to provide an input method with C-x 8 or Alt-<accent> prefix, but what you and I are doing is just pressing a dead key (^, ´, `, ~, ¨) for the accent and then another key to "compose" the accented character. And there is no Alt key used in this! And according to documentation it seems be appropriate for 8-bit encodings, so it should be pretty useless in UTF-8\. I reported this bug when it was introduced, but the bug seems to be classified as a feature ... Maybe it's just because the file is auto-loaded though pretty useless.*

### C-M-% and some other bindings do not work in emacs nox

This is because terminals are more limited than Xorg. Some terminals may handle more bindings than other, though. Two solutions:

*   either use the graphical version,
*   or change the binding to a supported one.

Example:

 `.emacs` 
```
(global-set-key (kbd "C-M-y") 'query-replace-regexp)

```

### Emacs client gets stuck when switching back to it

If you are using Emacs daemon, then you should know that input is blocking. If one Emacs instance is in the minibuffer (after an **M-x** for instance), then all other instance will wait for it to finish. Press **C-g** to cancel any input to make sure this Emacs session is not blocking.

### Emacs-nox output gets messy

When working in a terminal, the color, indentation, or anything related to the output might become crazy. This is (probably?) because Emacs was sent a special character at some point which may conflict with the current terminal. There is not much to be done but restarting emacs. If someone has a workaround or a more detailed explanation on the issue, feel free to contribute.

Graphical Emacs does not suffer from this issue.

### Shift + Arrow keys not working in emacs within tmux

First you must enable xterm-keys in your [tmux](/index.php/Tmux "Tmux") config.

 `.tmux.conf` 
```
setw -g xterm-keys on

```

But, this will break other key combinations. To fix them, put the following in your emacs config.

 `.emacs` 
```
;; handle tmux's xterm-keys
;; put the following line in your ~/.tmux.conf:
;;   setw -g xterm-keys on
(if (getenv "TMUX")
    (progn
      (let ((x 2) (tkey ""))
	(while (<= x 8)
	  ;; shift
	  (if (= x 2)
	      (setq tkey "S-"))
	  ;; alt
	  (if (= x 3)
	      (setq tkey "M-"))
	  ;; alt + shift
	  (if (= x 4)
	      (setq tkey "M-S-"))
	  ;; ctrl
	  (if (= x 5)
	      (setq tkey "C-"))
	  ;; ctrl + shift
	  (if (= x 6)
	      (setq tkey "C-S-"))
	  ;; ctrl + alt
	  (if (= x 7)
	      (setq tkey "C-M-"))
	  ;; ctrl + alt + shift
	  (if (= x 8)
	      (setq tkey "C-M-S-"))

	  ;; arrows
	  (define-key key-translation-map (kbd (format "M-[ 1 ; %d A" x)) (kbd (format "%s<up>" tkey)))
	  (define-key key-translation-map (kbd (format "M-[ 1 ; %d B" x)) (kbd (format "%s<down>" tkey)))
	  (define-key key-translation-map (kbd (format "M-[ 1 ; %d C" x)) (kbd (format "%s<right>" tkey)))
	  (define-key key-translation-map (kbd (format "M-[ 1 ; %d D" x)) (kbd (format "%s<left>" tkey)))
	  ;; home
	  (define-key key-translation-map (kbd (format "M-[ 1 ; %d H" x)) (kbd (format "%s<home>" tkey)))
	  ;; end
	  (define-key key-translation-map (kbd (format "M-[ 1 ; %d F" x)) (kbd (format "%s<end>" tkey)))
	  ;; page up
	  (define-key key-translation-map (kbd (format "M-[ 5 ; %d ~" x)) (kbd (format "%s<prior>" tkey)))
	  ;; page down
	  (define-key key-translation-map (kbd (format "M-[ 6 ; %d ~" x)) (kbd (format "%s<next>" tkey)))
	  ;; insert
	  (define-key key-translation-map (kbd (format "M-[ 2 ; %d ~" x)) (kbd (format "%s<delete>" tkey)))
	  ;; delete
	  (define-key key-translation-map (kbd (format "M-[ 3 ; %d ~" x)) (kbd (format "%s<delete>" tkey)))
	  ;; f1
	  (define-key key-translation-map (kbd (format "M-[ 1 ; %d P" x)) (kbd (format "%s<f1>" tkey)))
	  ;; f2
	  (define-key key-translation-map (kbd (format "M-[ 1 ; %d Q" x)) (kbd (format "%s<f2>" tkey)))
	  ;; f3
	  (define-key key-translation-map (kbd (format "M-[ 1 ; %d R" x)) (kbd (format "%s<f3>" tkey)))
	  ;; f4
	  (define-key key-translation-map (kbd (format "M-[ 1 ; %d S" x)) (kbd (format "%s<f4>" tkey)))
	  ;; f5
	  (define-key key-translation-map (kbd (format "M-[ 15 ; %d ~" x)) (kbd (format "%s<f5>" tkey)))
	  ;; f6
	  (define-key key-translation-map (kbd (format "M-[ 17 ; %d ~" x)) (kbd (format "%s<f6>" tkey)))
	  ;; f7
	  (define-key key-translation-map (kbd (format "M-[ 18 ; %d ~" x)) (kbd (format "%s<f7>" tkey)))
	  ;; f8
	  (define-key key-translation-map (kbd (format "M-[ 19 ; %d ~" x)) (kbd (format "%s<f8>" tkey)))
	  ;; f9
	  (define-key key-translation-map (kbd (format "M-[ 20 ; %d ~" x)) (kbd (format "%s<f9>" tkey)))
	  ;; f10
	  (define-key key-translation-map (kbd (format "M-[ 21 ; %d ~" x)) (kbd (format "%s<f10>" tkey)))
	  ;; f11
	  (define-key key-translation-map (kbd (format "M-[ 23 ; %d ~" x)) (kbd (format "%s<f11>" tkey)))
	  ;; f12
	  (define-key key-translation-map (kbd (format "M-[ 24 ; %d ~" x)) (kbd (format "%s<f12>" tkey)))
	  ;; f13
	  (define-key key-translation-map (kbd (format "M-[ 25 ; %d ~" x)) (kbd (format "%s<f13>" tkey)))
	  ;; f14
	  (define-key key-translation-map (kbd (format "M-[ 26 ; %d ~" x)) (kbd (format "%s<f14>" tkey)))
	  ;; f15
	  (define-key key-translation-map (kbd (format "M-[ 28 ; %d ~" x)) (kbd (format "%s<f15>" tkey)))
	  ;; f16
	  (define-key key-translation-map (kbd (format "M-[ 29 ; %d ~" x)) (kbd (format "%s<f16>" tkey)))
	  ;; f17
	  (define-key key-translation-map (kbd (format "M-[ 31 ; %d ~" x)) (kbd (format "%s<f17>" tkey)))
	  ;; f18
	  (define-key key-translation-map (kbd (format "M-[ 32 ; %d ~" x)) (kbd (format "%s<f18>" tkey)))
	  ;; f19
	  (define-key key-translation-map (kbd (format "M-[ 33 ; %d ~" x)) (kbd (format "%s<f19>" tkey)))
	  ;; f20
	  (define-key key-translation-map (kbd (format "M-[ 34 ; %d ~" x)) (kbd (format "%s<f20>" tkey)))

	  (setq x (+ x 1))
	  ))
      )
  )

```

### Improper window resizing in KDE

KDE users may observe that the Emacs window does not resize properly, but rather, the resized portion is transparent and mouse clicks are sent to the underlying window. To correct this behavior, change KDE's GTK3 theme to something other than oxygen-gtk. For instance, use the Emacs theme which is included with [gtk3](https://www.archlinux.org/packages/?name=gtk3).

To force Emacs to maximize completely in KDE, click the Emacs icon in the title bar, and select More Actions > Special Window Settings. Then in the "Size & Position" tab, select "Obey geometry restrictions", choose "Force" in the dropdown menu, and select "No" from the radio buttons on the right.

### Invalid font name for Oxygen-Sans

When [emacs](https://www.archlinux.org/packages/?name=emacs) (24.5-2) and [ttf-oxygen](https://www.archlinux.org/packages/?name=ttf-oxygen) (1:5.4.3-1) are installed, you will get an error like:

```
Error:invalid font name.-unknown-Oxygen-Sans-nolmal-normal--15----*-0-iso10646-1

```

when setting font attributes. This seems to be a bug in emacs, which is fixed in [emacs-git](https://aur.archlinux.org/packages/emacs-git/) (25.1.50.r125104-1).

### Slow startup if helm-mode is enabled

When `helm-mode` is enabled and causes Emacs slow to startup, we can edit the `.emacs` file by adding

```
(setq tramp-ssh-controlmaster-options
      "-o ControlMaster=auto -o ControlPath='tramp.%%C' -o ControlPersist=no")
(require 'tramp)
; before (helm-mode 1)

```

## Alternatives

There are numerous "smaller" implementations of Emacs. GNU/Emacs is probably the most popular. Some lightweight Emacs compatible alternatives will be listed here:

### mg

**mg** (originally called MicroGnuEmacs) is a lightweight implementation of Emacs written in C.

[mg](https://www.archlinux.org/packages/?name=mg) is available in the [official repositories](/index.php/Official_repositories "Official repositories") and it is also possible to download its source from its upstream [page](http://homepage.boetes.org/software/mg/). Beware **mg** has no UTF-8 support.

### zile

According to the official web [page](https://www.gnu.org/software/zile/) "GNU Zile is a lightweight Emacs clone. **Zile** is short for "Zile Is Lossy Emacs". Zile has been written to be as similar as possible to Emacs; every Emacs user should feel at home.". Zile has no UTF-8 support.

[zile](https://www.archlinux.org/packages/?name=zile) can be found in the official repositories.

The latest upstream tarballs can be found in official GNU [mirrors](http://ftp.sh.cvut.cz/MIRRORS/gnu/pub/gnu/zile/).

### uemacs

**uemacs** is a "Micro-emacs" version customized by Linus Torvalds . Available as [uemacs-git](https://aur.archlinux.org/packages/uemacs-git/) in the [AUR](/index.php/AUR "AUR").

The latest (2005) tarball can be found [here](ftp://ftp.cs.helsinki.fi/pub/Software/Local/uEmacs-PK/).

## See also

*   [GNU Emacs home page](http://www.gnu.org/software/emacs/)
*   [GNU Emacs manual](http://www.gnu.org/software/emacs/manual/emacs.html)
*   [Emacs Wiki](http://www.emacswiki.org/cgi-bin/wiki/)
*   [WikEmacs - a more readable, but less complete Emacs wiki](http://wikemacs.org)
*   [Useful introduction to Emacs and its shortcuts](http://www2.lib.uchicago.edu/keith/tcl-course/emacs-tutorial.html)
*   [The Church of Emacs (via Google drive)](https://d0edfcdc0ccc1cd13cdab5eb986fb92e8660dbef.googledrive.com/host/0B6LMD0u8OhYYZEotN2QyR1hwR1k/)
*   [Official reference card](http://www.gnu.org/software/emacs/refcards/pdf/refcard.pdf)