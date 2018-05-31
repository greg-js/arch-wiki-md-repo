[Emacs](https://en.wikipedia.org/wiki/Emacs "wikipedia:Emacs") is an extensible, customizable, self-documenting real-time display editor. At the core of Emacs lies an [Emacs Lisp](https://en.wikipedia.org/wiki/Emacs_Lisp "wikipedia:Emacs Lisp") interpreter, the language in which the majority of Emacs' built-in functionality and extensions are implemented. GNU Emacs uses GTK as its X toolkit, though it functions equally well within a CLI environment. The text-editing capabilities of Emacs are often compared to that of [vim](/index.php/Vim "Vim").

## Contents

*   [1 Installation](#Installation)
*   [2 Running Emacs](#Running_Emacs)
    *   [2.1 No Colors](#No_Colors)
    *   [2.2 As a daemon](#As_a_daemon)
    *   [2.3 As a systemd unit](#As_a_systemd_unit)
*   [3 Getting Help](#Getting_Help)
    *   [3.1 The manuals](#The_manuals)
*   [4 Customization](#Customization)
    *   [4.1 Configuration file](#Configuration_file)
*   [5 Tips and tricks](#Tips_and_tricks)
    *   [5.1 TRAMP](#TRAMP)
    *   [5.2 Using Emacs as git mergetool](#Using_Emacs_as_git_mergetool)
    *   [5.3 Using Caps Lock as Control key](#Using_Caps_Lock_as_Control_key)
    *   [5.4 Multiplexing emacs and emacsclient](#Multiplexing_emacs_and_emacsclient)
    *   [5.5 Multiple configurations](#Multiple_configurations)
    *   [5.6 Local and custom variables](#Local_and_custom_variables)
    *   [5.7 Custom colors and theme](#Custom_colors_and_theme)
    *   [5.8 SyncTeX support](#SyncTeX_support)
    *   [5.9 Syntax highlighting for systemd Files](#Syntax_highlighting_for_systemd_Files)
    *   [5.10 Clipboard support for emacs-nox](#Clipboard_support_for_emacs-nox)
*   [6 Packages](#Packages)
*   [7 Troubleshooting](#Troubleshooting)
    *   [7.1 Emacs fails to start with the error message 'Undefined color: "WINDOW_FOREGROUND"'](#Emacs_fails_to_start_with_the_error_message_.27Undefined_color:_.22WINDOW_FOREGROUND.22.27)
    *   [7.2 Colored output issues](#Colored_output_issues)
    *   [7.3 Problems displaying characters in X Windows](#Problems_displaying_characters_in_X_Windows)
    *   [7.4 Slow startup](#Slow_startup)
    *   [7.5 Cannot open load file: ...](#Cannot_open_load_file:_...)
    *   [7.6 Dead-accent keys problem: '<dead-acute> is undefined'](#Dead-accent_keys_problem:_.27.3Cdead-acute.3E_is_undefined.27)
    *   [7.7 C-M-% and some other bindings do not work in emacs nox](#C-M-.25_and_some_other_bindings_do_not_work_in_emacs_nox)
    *   [7.8 Emacs hangs](#Emacs_hangs)
    *   [7.9 Emacs-nox output gets messy](#Emacs-nox_output_gets_messy)
    *   [7.10 Weirds escaped numbers(utf-8) displaying in emacs terminal](#Weirds_escaped_numbers.28utf-8.29_displaying_in_emacs_terminal)
    *   [7.11 Shift + Arrow keys not working in emacs within tmux](#Shift_.2B_Arrow_keys_not_working_in_emacs_within_tmux)
    *   [7.12 Improper window resizing in KDE](#Improper_window_resizing_in_KDE)
*   [8 Alternatives](#Alternatives)
    *   [8.1 mg](#mg)
    *   [8.2 zile](#zile)
    *   [8.3 uemacs](#uemacs)
    *   [8.4 remacs](#remacs)
*   [9 See also](#See_also)

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

## Running Emacs

Before launching emacs, you should know how to close it (especially if you run it in a terminal): use the `Ctrl+x``Ctrl+c` key sequence.

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

By default, Emacs starts with a color theme showing hyperlinks in dark blue. To start Emacs on a text terminal without any color theme or scheme:

```
$ emacs -nw --color=no

```

This will cause all text to appear in the foreground color of the terminal — normally white text on a black background, or black text on a white background.

### As a daemon

In order to avoid reloading the Emacs config file every time Emacs starts, you can run Emacs as a daemon:

```
$ emacs --daemon

```

You may then connect to the daemon by running:

```
$ emacsclient -nc

```

Which creates a new frame `-c` (use `-t` if you prefer to use it in the terminal) and does not hog the terminal `-n` (`--no-wait`). Note that some programs such as Mutt or Git (for commit messages) wait for the editor to finish, so you cannot use the `-n` parameter. If your default editor is set to use it, you will have to specify an alternate editor (*e.g.* `emacsclient -a "" -t`) for those programs.

### As a systemd unit

A systemd unit is included in Emacs 26.1\. The unit is installed with Emacs, but it must be enabled after installing Emacs:

```
 $ systemctl --user enable --now emacs

```

Run this command as the user you want to run the Emacs server as; do not run the command as root. After the service is started, Emacs is ready to The unit file is stored in /usr/lib/systemd/user/emacs.service. Here is the contents of the unit file for reference:

 `/usr/lib/systemd/user/emacs.service` 
```
[Unit]
Description=Emacs text editor
Documentation=info:emacs man:emacs(1) https://gnu.org/software/emacs/

[Service]
Type=simple
ExecStart=/usr/bin/emacs --fg-daemon
ExecStop=/usr/bin/emacsclient --eval "(kill-emacs)"
Environment=SSH_AUTH_SOCK=%t/keyring/ssh
Restart=on-failure

[Install]
WantedBy=default.target

```

Note that systemd user units do not inherit environment variables from a login shell (like `~/.bash_profile`), so you may want to set the variables in `~/.pam_environment` instead. See [Systemd/User](/index.php/Systemd/User "Systemd/User") for more information.

If you start emacs as a daemon, you may want to set the `VISUAL` and `EDITOR` environment variables to `emacsclient` so that programs that start an editor use emacsclient instead of starting a new full instance of the editor. Programs that use an external editor include email programs (for editing the message), Git (for editing the commit message), and less (the `v` command for editing the displayed file). Do not use the `-n` (`--nowait`) option to emacsclient, since programs typically expect editing to be finished when the editor exits.

It is also recommended to change any GUI start menu entries (or equivalent) for Emacs to point to emacsclient instead of emacs, so that the emacs daemon is used instead of starting a new emacs process.

## Getting Help

Emacs has a built-in tutorial which can be accessed by clicking the first link on the splash screen and selecting *Help->Emacs Tutorial* from the menu or by pressing `C-h t`.

Emacs is self-documenting by design. As such, a great deal of information is available to determine the name of a specific command or its keybinding, for example. See all contextual help bindings with **C-h C-h**.

Emacs also includes a set of reference cards, useful for beginners and experts alike, see `/usr/share/emacs/<version>/etc/refcards/` (substitute <version> for your version of emacs).

### The manuals

If you really want to master Emacs, the most recommended source of documentation remains the official manuals:

*   Emacs: the complete Emacs user manual.
*   Emacs FAQ.
*   Emacs Lisp Intro: if you never used any programming language before.
*   Elisp: if you are already familiar with a programming language.

You can access them as PDFs from [GNU.org](http://www.gnu.org/software/emacs/manual/) or directly from Emacs itself thanks to the embedded 'info' reader: **C-h i**. Press **m** to choose a book.

Some users prefer to read books using 'info' because of its convenient shortcuts, its paragraphs adapting to window width and the font adapted to current screen resolution. Some find it less irritating to the eyes. Finally you can easily copy content from the book to any Emacs buffer, and you can even execute Lisp code snippets directly from the examples.

You may want to read the **Info** book to know more about it: **C-h i m info <RET>**. Press **?** while in info mode for a quick list of shortcuts.

## Customization

One of Emacs's main features is its extensibility and the ease of configuration. Emacs has a built-in customization engine. You can do `M-x customize` which displays a list of customization options. For how to use this interface, see the Easy Customization info node: `(info "(emacs) Easy Customization")`. You can set customization opens just for one Emacs session or save them into a [#Configuration file](#Configuration_file) so that they are saved across Emacs sessions. Note that this is what the customization interface does if you select "Apply and Save."

### Configuration file

When Emacs is started, it normally tries to load a Lisp program from an “initialization file”, or “init file” for short. This file, if it exists, specifies how to initialize Emacs for you. Emacs looks for your init file using the filenames ‘~/.emacs’, ‘~/.emacs.el’, or ‘~/.emacs.d/init.el’. See the info node "Init File" for more: `(info "(emacs) Init File")`

## Tips and tricks

### TRAMP

TRAMP (Transparent Remote Access, Multiple Protocols) is an extension which, as its name suggests, provides transparent access to remote files across a number of protocols. When prompted for a filename, entering a specific form will invoke TRAMP. Some examples:

To prompt for the root password before opening /etc/hosts with root permissions:

```
C-x C-f /sudo::/etc/hosts

```

To connect to 'remotehost' as 'you' via SSH and open the file ~/example.txt:

```
C-x C-f /ssh:you@remotehost:~/example.txt

```

The path for TRAMP is typically of the form '/[protocol]:[[user@]host]:<file>'.

To connect to 'myhost' as 'you' and edit /etc/hosts with sudo:

```
/ssh:you@remotehost|sudo:remotehost:/etc/hosts

```

TRAMP supports much more than the examples above might indicate. For more information refer to the TRAMP info manual, which is distributed with Emacs.

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

Some desktop environments include graphical tools to simplify keyboard remappings. For example, in [Plasma 5](/index.php/Plasma "Plasma") open System Settings and click on Input Devices. Select Keyboard and in the Advanced tab you will find the setting Caps Lock behaviour under which you can select Caps Lock is also a Ctrl.

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

If you want to run it in a new session just do `emacs <file> -`.

### Multiple configurations

You can use several configurations and tell Emacs to load one or the other.

For example, let us define two configuration files.

 `.emacs` 
```
(load "~/.emacs.d/main" nil t)
(load "~/.emacs.d/functions" nil t)
(load "~/.emacs.d/modes" nil t)
(load "~/.emacs.d/plugins" nil t)
(load "~/.emacs.d/theme" nil t)

```

This is the full configuration we load for the daemon. But the *plugins* file is huge and slow to load. If we want to spawn a new Emacs instance that does not need the *plugins* features, it can be cumbersome to load it everytime in the long run.

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

Now in any file you can define local variables in two ways, see [the manual for complete details](https://www.gnu.org/software/emacs/manual/html_node/emacs/Specifying-File-Variables.html)

*   Using `M-x add-file-local-variable-prop-line`, which adds a commented line at the beginning similar to:

```
// -*- my-compiler:g++; mode:c++ -*-

```

*   Or you can use `M-x add-file-local-variable` to add lines near the end of the file:

```
// Local Variables:
// my-compiler: g++
// mode: c++
// End:

```

Note that for the values to take effect, you will need to call `M-x revert-buffer`.

Custom variables are considered unsafe by default. If you try to open a file that contains local variable redefining custom variables, Emacs will ask you for confirmation.

You can declare the variable as secure, thus removing the Emacs prompt for confirmation. You need to specify a predicate that any new value has to verify so that it can be considered safe.

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

See also:

*   [https://www.emacswiki.org/emacs/ColorThemes](https://www.emacswiki.org/emacs/ColorThemes)
*   [https://www.gnu.org/software/emacs/manual/html_node/emacs/Custom-Themes.html](https://www.gnu.org/software/emacs/manual/html_node/emacs/Custom-Themes.html)

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

## Packages

Emacs's functionality can be extended with third-party packages. The built-in package manager `package.el` is the officially supported way to do this, though there are several other package managers written by members of the Emacs community. `package.el` relies on the variable `package-archives` to find packages. By default, this includes the [Emacs Lisp Package Archive (ELPA)](https://elpa.gnu.org/). `M-x list-packages` will create a buffer listing all the packages your Emacs knows about. The manual (`[(info "(emacs) Packages")](https://www.gnu.org/software/emacs/manual/html_node/emacs/Packages.html)`) contains much more information.

Third-party package archives can be added. The most widely used of these is [MELPA](https://melpa.org/).

A number of popular extensions are available as packages in the `[community]` repository, and more still, via the [AUR](/index.php/AUR "AUR"). The name of such packages usually have a 'emacs-' prefix (for example, [emacs-lua-mode](https://www.archlinux.org/packages/?name=emacs-lua-mode)), though not always (for example, [auctex](https://www.archlinux.org/packages/?name=auctex)).

**Tip:** Arch Linux Wiki contributors may be interested in the [Emacs Mediawiki](/index.php/Emacs_Mediawiki "Emacs Mediawiki") package.

Some packages may require you to make changes to your configuration file in order to activate them so that their features are available during an Emacs session. For example, if you install [auctex](https://www.archlinux.org/packages/?name=auctex), you will need to add

```
(load "auctex.el" nil t t)
(load "preview-latex.el" nil t t)
```

to your configuration file. Other packages should let you know how to activate them in the commentary section of their source code or in their README.

## Troubleshooting

### Emacs fails to start with the error message 'Undefined color: "WINDOW_FOREGROUND"'

You need to install either the [mcpp](https://www.archlinux.org/packages/?name=mcpp) package or the [gcc](https://www.archlinux.org/packages/?name=gcc) package. The C preprocessor *cpp* is used to preprocess [X resources](/index.php/X_resources "X resources") by *xrdb*. If a C preprocessor is not installed on the system, *xrdb* silently skips running the C preprocessor and the symbol WINDOW_FOREGROUND is not expanded to a hexadecimal color code.

### Colored output issues

By default, the Emacs shell will show raw escape sequences used to print colors. In other words, it will display strange symbols in place of the desired colored output.

Including the following into `~/.emacs` amends the problem:

```
(add-hook 'shell-mode-hook 'ansi-color-for-comint-mode-on)

```

### Problems displaying characters in X Windows

If when you start emacs in X windows all the characters in the main window are white boxes with black borders (the ones you see if you try to view characters for which you do not have the correct font installed), you need to install [xorg-fonts-75dpi](https://www.archlinux.org/packages/?name=xorg-fonts-75dpi) and/or [xorg-fonts-100dpi](https://www.archlinux.org/packages/?name=xorg-fonts-100dpi) and restart X windows.

### Slow startup

**Tip:** To eliminate startup time, users may want to consider running Emacs [#As a systemd unit](#As_a_systemd_unit).

Slow startup times are often caused by one of two things.

To determine which it might be, run Emacs with:

```
$ emacs -q

```

*   Mistakes, particularly in /etc/hosts, will often result in a 5+ second delay when starting Emacs. Refer to '[set the hostname](/index.php/Configuring_network#Set_the_hostname "Configuring network")' in the network configuration guide for information.

*   You may need to monitor any network packets sent from your computer (using a program like Wireshark) to see if there is any strange behavior.

*   A simple way to search for the cause is to comment-out (i.e., prefix lines with ';') suspect sections of your `~/.emacs` (or `~/.emacs.d/init.el`) then start Emacs again to see if there is any change. Keep in mind use of "require" and "load" can slow the startup down, especially when used with larger extensions. They should, as a rule, only be used when their target is either: needed once Emacs starts or provides little more than "autoloads" for an extension. Otherwise, use the 'autoload function directly. For example, instead of:

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
Emacs, the normal way to use accent keys does not work as expected. Trying to accent a word like 'fiancé' will produce the message above.

```

A way to solve it is just put the line above on your startup file, `~/.emacs`:

```
  (require 'iso-transl)

```

And no, it is not a bug, but a feature of new Emacs versions. Reading the subsequent messages about it on the mail list, we found it ([http://lists.gnu.org/archive/html/help-gnu-emacs/2009-05/msg00179.html](http://lists.gnu.org/archive/html/help-gnu-emacs/2009-05/msg00179.html)):

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

### Emacs hangs

Due to its single-threaded nature, many operations block Emacs. This could happen in a few ways. For example, Emacs may be waiting for input from you (e.g. you've opened the minibuffer in one frame but are trying to work in another). Alternatively, Emacs could be running code that simply takes a while to finish. Or perhaps you've run across a bug. There are several ways of trying to unblock Emacs without killing the Emacs process.

*   Try pressing `C-g`. Depending on what Emacs is doing, you may need to press it multiple times.
*   Try pressing `ESC ESC ESC`.
*   From another terminal, run `killall -SIGUSR2 emacs`

### Emacs-nox output gets messy

When working in a terminal, the color, indentation, or anything related to the output might become crazy. This is (probably?) because Emacs was sent a special character at some point which may conflict with the current terminal. If this happens you can do `M-x redraw-display`, which will redraw the terminal's display. If this problem happens frequently, you might want to bind the command to a key, e.g. by putting something like

```
(global-set-key (kbd "<f7>") 'redraw-display)

```

in your .emacs file.

Graphical Emacs does not suffer from this issue.

### Weirds escaped numbers(utf-8) displaying in emacs terminal

Export these values in your .bashrc or .zshrc:

 `$ ~/.bashrc or ~/.zshrc` 
```
export LANG\='en_US.UTF-8'
export LC_ALL\="en_US.UTF-8"
export TERM\=xterm-256color
```

It can be a source of errors since in Linux distributions the correct values use lowercase utf (e.g. en_US.utf-8)

To view all available locales use locale -a

### Shift + Arrow keys not working in emacs within tmux

Enable xterm-keys in your [tmux](/index.php/Tmux "Tmux") configuration:

 `~/.tmux.conf` 
```
setw -g xterm-keys on

```

Because this will break other key combinations, put the following in your emacs config.

 `~/.emacs` 
```
(defadvice terminal-init-screen
  ;; The advice is named `tmux', and is run before `terminal-init-screen' runs.
  (before tmux activate)
  ;; Docstring.  This describes the advice and is made available inside emacs;
  ;; for example when doing C-h f terminal-init-screen RET
  "Apply xterm keymap, allowing use of keys passed through tmux."
  ;; This is the elisp code that is run before `terminal-init-screen'.
  (if (getenv "TMUX")
    (let ((map (copy-keymap xterm-function-map)))
    (set-keymap-parent map (keymap-parent input-decode-map))
(set-keymap-parent input-decode-map map))))

```

See [tmux FAQ](https://github.com/tmux/tmux/blob/master/FAQ#L242) for details.

### Improper window resizing in KDE

KDE users may observe that the Emacs window does not resize properly, but rather, the resized portion is transparent and mouse clicks are sent to the underlying window. To correct this behavior, change KDE's GTK3 theme to something other than oxygen-gtk. For instance, use the Emacs theme which is included with [gtk3](https://www.archlinux.org/packages/?name=gtk3).

To force Emacs to maximize completely in KDE, click the Emacs icon in the title bar, and select More Actions > Special Window Settings. Then in the "Size & Position" tab, select "Obey geometry restrictions", choose "Force" in the dropdown menu, and select "No" from the radio buttons on the right.

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

### remacs

**remacs** is a community-driven port of Emacs to Rust. Available as [remacs-git](https://aur.archlinux.org/packages/remacs-git/) in the [AUR](/index.php/AUR "AUR").

## See also

*   [GNU Emacs home page](http://www.gnu.org/software/emacs/)
*   [GNU Emacs manual](http://www.gnu.org/software/emacs/manual/emacs.html)
*   [Emacs Wiki](http://www.emacswiki.org/cgi-bin/wiki/)
*   [WikEmacs - a more readable, but less complete Emacs wiki](http://wikemacs.org)
*   [Useful introduction to Emacs and its shortcuts](http://www2.lib.uchicago.edu/keith/tcl-course/emacs-tutorial.html)
*   [The Church of Emacs (via Google drive)](https://d0edfcdc0ccc1cd13cdab5eb986fb92e8660dbef.googledrive.com/host/0B6LMD0u8OhYYZEotN2QyR1hwR1k/)
*   [Official reference card](http://www.gnu.org/software/emacs/refcards/pdf/refcard.pdf)
*   [EXWM](/index.php/EXWM "EXWM"), the Emacs X Window Manager