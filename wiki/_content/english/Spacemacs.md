[Spacemacs](https://en.wikipedia.org/wiki/Spacemacs "wikipedia:Spacemacs") is an extensible and customizable text editor, built on top of [Emacs](/index.php/Emacs "Emacs") and using [Vim](/index.php/Vim "Vim") keybindings. The goal of the project is to combine both Vim and Emacs editors, getting the best parts from each. Spacemacs distribution is based on community-driven [Emacs](/index.php/Emacs "Emacs") config, which greatly extends default Emacs behaviour and adds a lot of additional features.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Install Emacs](#Install_Emacs)
    *   [1.2 Backup old Emacs configuration (optional)](#Backup_old_Emacs_configuration_.28optional.29)
    *   [1.3 Install Spacemacs](#Install_Spacemacs)
    *   [1.4 Install Adobe Source Pro fonts (optional)](#Install_Adobe_Source_Pro_fonts_.28optional.29)
    *   [1.5 Run Spacemacs for the first time](#Run_Spacemacs_for_the_first_time)
*   [2 Running Spacemacs](#Running_Spacemacs)
    *   [2.1 Daemon mode](#Daemon_mode)
*   [3 Usage](#Usage)
    *   [3.1 Built-in Tutorial](#Built-in_Tutorial)
    *   [3.2 Basic Concepts](#Basic_Concepts)
        *   [3.2.1 Prerequisites](#Prerequisites)
        *   [3.2.2 Editor states](#Editor_states)
            *   [3.2.2.1 Normal state](#Normal_state)
                *   [3.2.2.1.1 Navigation](#Navigation)
                *   [3.2.2.1.2 Text manipulation](#Text_manipulation)
                *   [3.2.2.1.3 Undo/Redo](#Undo.2FRedo)
            *   [3.2.2.2 Insert state](#Insert_state)
                *   [3.2.2.2.1 Entering](#Entering)
                *   [3.2.2.2.2 Leaving](#Leaving)
            *   [3.2.2.3 Visual state](#Visual_state)
                *   [3.2.2.3.1 Visual block state](#Visual_block_state)
        *   [3.2.3 Buffers (Tabs)](#Buffers_.28Tabs.29)
            *   [3.2.3.1 Navigation](#Navigation_2)
        *   [3.2.4 Files](#Files)
            *   [3.2.4.1 Inline (Helm)](#Inline_.28Helm.29)
            *   [3.2.4.2 File manager (Dired)](#File_manager_.28Dired.29)
    *   [3.3 Advanced concepts](#Advanced_concepts)
        *   [3.3.1 Layers](#Layers)
        *   [3.3.2 File Navigation](#File_Navigation)
            *   [3.3.2.1 File tree (Neotree)](#File_tree_.28Neotree.29)
            *   [3.3.2.2 File manager (Ranger)](#File_manager_.28Ranger.29)
        *   [3.3.3 Windows](#Windows)
*   [4 Configuration](#Configuration)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Slow startup time](#Slow_startup_time)

## Installation

### Install Emacs

Spacemacs is built on top of Emacs, so we need to install Emacs first.

*   [Install](/index.php/Install "Install") [Emacs](/index.php/Emacs "Emacs") package

### Backup old Emacs configuration (optional)

If you used Emacs before, be sure to backup your previous config.

```
$ mv ~/.emacs.d ~/.emacs.d.bak && mv ~/.emacs ~/.emacs.bak

```

### Install Spacemacs

To install Spacemacs we need to clone an actual config from github, and replace Emacs config entirely.

```
$ git clone [https://github.com/syl20bnr/spacemacs](https://github.com/syl20bnr/spacemacs) ~/.emacs.d

```

**Note:** This command should be run from your user account.

### Install Adobe Source Pro fonts (optional)

The default font used by Spacemacs is Source Code Pro by Adobe. It is recommended to install it on your system if you wish to use it.

*   Install [adobe-source-code-pro-fonts](https://www.archlinux.org/packages/?name=adobe-source-code-pro-fonts) package

If the specified font is not found, the fallback one will be used.

### Run Spacemacs for the first time

Now it's time to launch Spacemacs.

```
$ emacs

```

For the first time you will be asked for features that should be installed. All the choices are alternatives, so something should be selected in any case. This choices affects some Spacemacs behavior and hotkeys. It's recommended to choose default values, just hitting **Enter**. Defaults are pretty optimized and you can always change them later.

**Tip:** Most default packages offers more features than the alternatives. However, you can find the other variants more useful in some cases (i.e performance and some special features).

When you finish with the questions, Spacemacs will download and install all the required packages. It may take a few minutes. Spacemacs may seems frozen at this time, but it's okay.

## Running Spacemacs

To start spacemacs simply run:

```
$ emacs

```

Spacemacs will be ready to work when there are no '...' operations in the bottom bar would be displayed.

**Note:** If startup time exceeds 10 seconds, refer to the troubleshooting part below.

### Daemon mode

Spacemacs can also be launched in a daemon mode. Daemon mode allows to initialize editor once, and connect to it later, without re-reading configuration file. It can be useful, when you have massive configuration file, so the initialization sequence would be completed only once. You would be able to connect immediately any time later then.

To run Spacemacs in daemon mode:

```
$ emacs --daemon=instance1

```

Then you can connect to `instance1` later, using **emacsclient**:

```
$ emacsclient -nc -s instance1

```

**Tip:** You can run multiple daemons with different names

## Usage

Using Spacemacs may be tricky for the first time, espesially for the complete beginners. However, your efforts will be rewarded. Only a few key concepts required to perform basic tasks.

You can always exit spacemacs by typing **:q[Enter]**

### Built-in Tutorial

You can always run Spacemacs built-in tutorial by pressing `SPC h T` when in Spacemacs.

### Basic Concepts

#### Prerequisites

In order to explain the basic concepts we need some text to play with. Let's generate it first. Please, don't mind if the commands are unclear right now, you don't need to know them at moment.

1.  Run Spacemacs
2.  Press `SPC b N` to create new empty buffer
3.  Press `9 SPC i l l` to insert some text

You should see a nine lines of generated text in result. Use them to experiment with the commands described in the next sections.

**Note:** When the **SPC** key sequence is used, you need to press keys one after another. So you press **SPACE** key, followed by **b**, followed by **N**. Uppercase letters should be entered with shift key, for example **N** is **Shift+n**. So the final sequence would be **SPACE**, **b**, **Shift+n**

**Tip:** When you press SPC key, help menu appears in the bottom. You can inspect possible commands there.

Now we can move closer to concept named **states**.

#### Editor states

The major difference between Spacemacs and regular text editor is **states**. Each state changes the way how the editor works. For example, there is an **insert state**, where you able to enter text (like in a regular text editor), and there is a **normal state**, where all your keypresses are used as commands, and doesn't change the actual text. Only one state can be active at the time. Switching between the states is the key skill to use Spacemacs successfully.

Current editor state is displayed in a left bottom corner. It have a form of colored rectangle with text "1" (by default). The color describes the current state. There are a lot of states, but only a few of them are used regularly:

*   Orange. This is **normal state**. Used for entering commands and text navigation.
*   Green. This is **insert state**. Used for a text input.
*   Grey. This is **visual state**. Used for selecting chunks of text and controlling them.

You can also check the cursor color for the current state.

**Note:** In order to use Spacemacs you will need to know at least **normal** and **insert** state.

##### Normal state

Normal state is used for text navigation and running commands. You can't directly enter text in this mode. Instead, you able to quickly navigate and make any sort of corrections there. Normal state is default state, and it has **orange** color.

You can always return to normal state by pressing `ESC` key or `fd` key sequence if you accidentally leave it.

**Note:** Commands listed below are not full. There are a lot more. You can check the additional documentation to find useful commands in your case.

**Note:** Nobody can learn this commands for the first time. Just take a few of them and master. Only small subset of commands required to start make things.

###### Navigation

For basic navigation, the following keys are used.

*   `h` - move cursor by one symbol left
*   `j` - move cursor by one line down
*   `k` - move cursor by one line up
*   `l` - move cursor by one symbol right

It's also possible to navigate between the words or even sentences with single key:

*   `w` - move to next word (beginning)
*   `b` - move to previous word (beginning)
*   `(` - move to the beginning of current sentence
*   `)` - move to the beginning of next sentence
*   `^` - move to beginning of line
*   `$` - move to the end of line

To scroll the pages, use the following commands:

*   `Ctrl+f` - move one page down
*   `Ctrl+b` - move one page up
*   `gg` - goto first line of the document
*   `G` - goto last line of the document

You can also use numbers with commands, so they would repeat **n** times:

*   `5j` - move cursor five lines down
*   `7w` - move cursor seven words forward
*   `3 Ctrl+f` - move three pages down
*   `20gg` - move cursor to line with number 20

**Tip:** Numeric arguments are widely used in Spacemacs world.

There are a lot of commands uncovered. Basicaly, you can navigate between everything in Spacemacs, thanks to **Vim-like** flow. Check the additional resources to get the details.

###### Text manipulation

You can modify the text with the following commands:

*   `x` - cut the symbol under cursor
*   `dw` - cut the word under cursor
*   `dd` - cut the line under cursor
*   `yw` - copy (yank) the word under cursor
*   `yd` - copy (yank) the line under cursor
*   `p` - paste copied/cut text
*   `r*a*` - replace the symbol under cursor to *a*

You can also use numeric arguments there.

###### Undo/Redo

You can undo and redo changes with the following commands:

*   `u` - undo last change
*   `Ctrl+r` - redo last change

##### Insert state

Insert state is used for the text input. It's very closed to regular editor behavior. However, the ability to modify text is limited. You will need to switch back to the **normal state** in order to make corrections. The color of insert state is **green**.

###### Entering

To enter the insert state, press `i` from the **normal state**. Your cursor will changed to thin and green one. Now you can type something. When you ready, just leave the insert state by pressing `ESC` key or `fd` key sequence.

There are a lot of ways to enter insert mode. The difference, however, is only related to initial cursor position. It would be enough to know just `i` hotkey for the first time. But there are also the others, and they will be very useful when you master them:

*   `i` - enter insert mode before the cursor
*   `a` - enter insert mode after the cursor
*   `I` - enter insert mode at the beginning of the line
*   `A` - enter insert mode at the end of the line
*   `o` - enter insert mode at next line
*   `O` - enter insert mode at previous line

###### Leaving

To leave the insert state press `ESC` key or `fd` key sequence. You will return to **normal state** and cursor will change to orange.

##### Visual state

This state used for visual text selection. It allows to select text chunks and cut/copy them. The state color is **grey**.

To enter visual state press `v` hotkey from the **normal mode**. Then you can navigate around using normal mode hotkeys with only one difference: text selection. Cursor movements would select text, based on initial cursor position, and you can `y`ank (copy) or `d`elete it later. Remember, that you can use commands like `ve` or `v(` to quickly select words or sentences. Check the `Normal state: Navigation` section to get the idea.

You can also press `V` to quickly select the whole line.

###### Visual block state

Visual block state is more powerful version of visual state. It allows to select text in columns. It's similar to multi-cursor concept on regular editors and IDEs. This state can be entered by pressing `Ctrl+v` hotkey. Then you can navigate with `h j k l` keys to see the difference.

There a lot of stuff that can be done in visual block state. Refer to the additional resources for this information. This feature is called **vim visual block mode** in origin.

#### Buffers (Tabs)

The text in Spacemacs located in the areas called buffers. They are very similar to regular editor tabs. You can switch between the buffers and create new ones. Buffers are also used by editor itself by storing some information you can inspect later.

##### Navigation

To show the list of the current buffers press `SPC b b`. You will see a new window at the bottom. This is a place you can inspect, filter, and navigate buffers. Some buffers already exist there, like *Messages* and *scratch*. They created by the editor and contain some useful information.

The first thing you can do with the bottom window is to type anything into `pattern` field. This will filter buffers. If there are no buffers left after the filtering, you can create new one instead, just pressing "Enter" after your input. New buffer will be created and opened.

You can also open any buffer by hand. Press `Ctrl+**j**` or `Ctrl+**k**` to navigate between the lines. Then press `Ctrl+**l**` or `Enter` to confirm your choice. Selected buffer will be opened.

**Tip:** Remember `h j k l` keys? They are widely used for navigation. In some cases we need to use modifier keys like `Ctrl`. That allows to input and navigate at the same time.

You can also use some hotkeys from **normal state** to control buffers:

*   `SPC b b` - list buffers
*   `SPC TAB` - switch to last viewed buffer
*   `SPC b n` - switch to next buffer (one forward)
*   `SPC b p` - switch to previous buffer (one backward)
*   `SPC f s` - save the current buffer to file
*   `SPC b d` - close current buffer

**Tip:** If you want to save a new buffer, you should choose a file for it. Refer to the next section for details.

#### Files

Spacemacs provides a two options for file navigation: inline navigation and build-in file manager. Inline navigation is used in Spacemacs confirmation dialogs and it's very similar to the shell one. Build-in file manager is more user-friendly and allows to check the file details. Learning the basics of each is the essential key of mastering Spacemacs.

There also advanced options available, like more powerful file manager and file tree. They are covered in `Advanced` section.

##### Inline (Helm)

Inline navigation available with `SPC f f` hotkey. It uses the window very similar to buffer-navigation one. You can filter and select files there. Just type anything to narrow results, or press `Ctrl+j` or `Ctrl+k` for moving the line down and up. Press `Ctrl+l` to open file or directory, and press `Ctrl+h` for going backward. Press `TAB` to autocomplete the input.

##### File manager (Dired)

If you need more visual method, run built-in file manager by pressing `SPC a d` `Enter`. You can navigate, using `Ctrl`+`h j k l` keys, and press `Enter` to enter directories and open files.

There are some hotkeys available (refer to dired documentation for more):

*   `q` - quit dired
*   `R` - rename file
*   `C` - copy file
*   `+` - create new directory

**Tip:** If you need more powerful file manager, check Ranger in `Advanced` section. It provides more features and can be the best replacement for Dired when you master it.

### Advanced concepts

At this step you are able to open files, make changes and save them successfully. Half the way is done, and now you can choose what to master next. There are some sections you may be interested.

#### Layers

One of the strongest features of Spacemacs is layers. Layer is a set of packages and configuration options, that greatly extends editor functionality in some way. There are layers for different programming languages, for example, or layers, providing additional tools (like IRC messaging, or integrated web browser). The full list of layers can be found at [Layers](http://spacemacs.org/layers/LAYERS.html) documentation page.

Some layers are already shipped with Spacemacs, the others can be added manually. To do this, open Spacemacs configuration file (`SPC f e d`), and find `dotspacemacs-configuration-layers` section there. Then simply add selected layer to the list and restart Spacemacs. It will download all the required files on the next start.

Spacemacs will also offer you to install a new layer when you open a file with already-known extension. For example, if you open `.html` file, installation of `html` layer will be offered.

You can customize layer behaviour by overriding some layer-specific variables in your Spacemacs configuration file. Check the appropriate layer documentation to get the details.

#### File Navigation

There are some additional tools for file navigation. They may greatly increase the way you use Spacemacs on a daily basis.

##### File tree (Neotree)

You can run file tree by pressing `SPC f t`. New window opens, accessible with `SPC 0`. Standard `h j k l` navigation is available there. You can change root folder with `R` and toggle hidden files with `s`. Create new files with `c` and rename the old ones with `r`. Check [Neotree](https://github.com/syl20bnr/spacemacs/blob/master/doc/DOCUMENTATION.org#neotree-file-tree) documentation for the details.

**Tip:** If you need to change the root to higher one, just press `R` while on the current root path (first line of the window). Inline file navigation opens, just go backward with `H` as far as you need and select `.` directory then

##### File manager (Ranger)

If you need a full-featured file manager then Ranger may be the best choice. A lot of useful features are available there, like an instant `h j k l` navigation, inline file preview and ability to manipulate files. It also improves default Dired behaviour (`SPC a d`) a bit. Install `ranger` layer and run it with `SPC a r`. Check [Ranger](https://github.com/syl20bnr/spacemacs/tree/master/layers/%2Btools/ranger) documentation for the details. Along with customization options, there are a lot of useful hotkeys.

**Note:** If you have issues opening Ranger, try to close Neotree first

#### Windows

Spacemacs allows you to split the screen into the separate windows. Each window has a personal number and can be accessed with `SPC *n*` hotkey, where the `*n*` is a selected number. Windows can be splitted individually, so it gives an ability to create complex layouts.

Some of windows hotkeys are presented below. Check the inline help (`SPC w`) to get more.

*   `SPC w 3` - focus window with number 3
*   `SPC w s` - split window horizontally
*   `SPC w v` - split window vertically
*   `SPC w d` - delete window
*   `SPC w u` - undo last window action
*   `SPC w m` - toggle window fullscreen
*   `SPC w .` - enter window transient state

**Tip:** Transient state allows you to play with window settings, like their order and proportions. Just enter it and all the available options will be displayed.

## Configuration

## Troubleshooting

### Slow startup time

If startup time exceeds 10 seconds, there may be a problem with `exec-path-from-shell` module. It can be safely disabled on linux systems. Complete the following steps:

1.  Open Spacemacs configuration file by pressing `SPC f e d`
2.  Find `dotspacemacs-excluded-packages` section
3.  Add `exec-path-from-shell` module here, so the final entry would be like `dotspacemacs-excluded-packages '(exec-path-from-shell)`
4.  Save changes with `SPC f s` and restart Spacemacs