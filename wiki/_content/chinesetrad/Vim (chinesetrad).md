「[Vim](http://www.vim.org/about.php) 是個進階文字編輯器，旨在提供 UNIX 上正統編輯器 'vi' 的強大功能，並加上更完整的功能集合。」

Vim 注重鍵盤的使用，並提供許多有用功能，例如語法標亮和腳本功能。Vim 不像 nano 或 pico 這些簡易的文字編輯器，它需要一段時間去學習，並得花上大量的時間才能精通。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 安裝](#安裝)
*   [2 用法](#用法)
    *   [2.1 一般編輯](#一般編輯)
    *   [2.2 到處移動](#到處移動)
    *   [2.3 重複指令](#重複指令)
    *   [2.4 刪除](#刪除)
    *   [2.5 取消和重做](#取消和重做)
    *   [2.6 視覺模式](#視覺模式)
    *   [2.7 搜尋和取代](#搜尋和取代)
    *   [2.8 儲存和退出](#儲存和退出)
    *   [2.9 額外指令](#額外指令)
*   [3 設定](#設定)
    *   [3.1 循環搜尋](#循環搜尋)
    *   [3.2 拼字檢查](#拼字檢查)
    *   [3.3 語法標亮](#語法標亮)
    *   [3.4 使用滑鼠](#使用滑鼠)
    *   [3.5 讓方向鍵通過斷行](#讓方向鍵通過斷行)
    *   [3.6 ~/.vimrc 範例](#~/.vimrc_範例)
*   [4 插件](#插件)
    *   [4.1 cscope](#cscope)
    *   [4.2 Taglist](#Taglist)
*   [5 合併檔案 (vimdiff)](#合併檔案_(vimdiff))
*   [6 Vim 提示](#Vim_提示)
    *   [6.1 行號](#行號)
    *   [6.2 Substitute on lines](#Substitute_on_lines)
    *   [6.3 Make Vim restore cursor position in files](#Make_Vim_restore_cursor_position_in_files)
    *   [6.4 Empty space at the bottom of gVim windows](#Empty_space_at_the_bottom_of_gVim_windows)
    *   [6.5 用 vim 取代 vi 指令](#用_vim_取代_vi_指令)
*   [7 疑難排解](#疑難排解)
    *   [7.1 "^M"](#"^M")
*   [8 另請參閱](#另請參閱)
    *   [8.1 官方](#官方)
    *   [8.2 教學](#教學)
        *   [8.2.1 影片](#影片)
        *   [8.2.2 遊戲](#遊戲)
    *   [8.3 範例設定](#範例設定)
    *   [8.4 其他](#其他)

## 安裝

[安裝](/index.php/Pacman_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Pacman (正體中文)")指令列介面的 [vim](https://www.archlinux.org/packages/?name=vim) 軟體包，或安裝 GUI 版本 (同時包含 `vim`) 的 [gvim](https://www.archlinux.org/packages/?name=gvim) 軟體包。

**註記:**

*   [vim](https://www.archlinux.org/packages/?name=vim) 軟體包的目的在於輕量化，因此它不支援 Python, Lua 和 Ruby 直譯，也不支援 X 伺服器 (代表它不支援來自 X 剪貼簿的複製與貼上)。如果您需要這些選項，請改安裝 [gvim](https://www.archlinux.org/packages/?name=gvim) 軟體包 (它同時包含 `vim` 執行檔)。`herecura-stable` 非官方軟體庫也提供一些不同的 Vim / gVim 變形：

 `$ pacman -Slq herecura-stable | grep vim` 
```
vim-cli
vim-gvim-gtk
vim-gvim-motif
vim-gvim-qt
vim-gvim-x11
vim-rt
vim-tiny

```

*   KDE 上使用來自官方軟體庫的 [gvim](https://www.archlinux.org/packages/?name=gvim) 可能會出現某些視覺上的問題。若出現這類型的狀況，可以安裝來自 `herecura-stable` 的 `vim-gvim-qt`，或是 AUR 的 [vim-qt](https://aur.archlinux.org/packages/vim-qt/)

## 用法

這裡有如何使用 Vim 的簡短概覽。執行 `vimtutor` 或 `gvimtutor` 會啟動 vim 自己的教學，完整跑一遍會花上約 25-30 分鐘。

Vim 有四種不同的模式：

*   指令模式 (Command mode)：鍵入字串會當作指令執行。
*   輸入模式 (Insert mode)：鍵入字串會輸入至檔案。
*   視覺模式 (Visual mode)：鍵入選擇、剪下或複製文字
*   Ex 模式：額外功能的輸入模式 (例如儲存檔案、取代文字...)

### 一般編輯

If you start Vim with:

```
$ vim somefile.txt

```

you will see a blank document (providing that somefile.txt does not exist. If it does, you will see what is in there). You will not be able to edit right away – you are in Command Mode. In this mode you are able to issue commands to Vim with the keyboard.

**Note:** Vim is an example of classic Unix-style ware. It has a difficult learning curve, but once you get started, you will find that it is extremely powerful. Also, all commands are case sensitive. Sometimes the uppercase versions are “blunter” versions (`s` will replace a character, `S` will replace a line), other times they are completely different commands (`j` will move down, `J` will join two lines).

You insert text (stick it before the cursor) with the `i` command. `I` (uppercase **i**) inserts text at the beginning of the line. You append text (place text after the cursor, what most people expect) with `a`. Typing `A` will place the cursor at the end of the line.

Return to command mode at any time by pressing `Esc`.

### 到處移動

In Vim, you can move the cursor with the arrow keys, but this isn't the **Vim way**. You’d have to move your right hand all the way from the standard typing position all the way to the arrow keys, and then back. Not fun.

In Vim you can move down by pressing `j`. You can remember this because the “j” hangs down. You move the cursor back up by pressing `k`. Left is `h` (it's left of the “j”), and right is `l` (lowercase **L**).

`^` will put the cursor at the beginning of the line, and `$` will place it at the end.

**Note:** `^` and `$` are commonly used in regular expressions to match the beginning and ending of the line. Regular expressions are very powerful and are commonly used in *nix environment, so maybe it is a little bit tricky now, but later you will notice “the idea” behind the use of most of these key mappings.

To advance a word, press the `w` key. `W` will include more characters in what it thinks is a word (e.g. underscores and dashes as a part of a word). To go back a word, `b` is used. Once again, `B` will include more characters in what Vim considers a word. To advance to the end of a word, use `e`, `E` includes more characters.

To advance to the beginning of a sentence, `(` will get the job done. `)` will do the opposite, moving to the end of a sentence. For an even bigger jump, `{` will move the the beginning a whole paragraph. `}` will advance to the end of a whole paragraph.

To advance to the header (top) of the screen, `H` will get the job done. `M` will advance to the middle of the screen, and `L` will advance to the last (bottom). `gg` will go to the beginning of the file, `G` will go to the end of the file. `Ctrl+D` will let you scroll page by page.

### 重複指令

If a command is prefixed by a number, then that command will be executed that number of times over (there are exceptions, but they still make sense, like the `s` command). For example, pressing `3i` then “Help! ” then `Esc` will print “Help! Help! Help!“. Pressing `2}` will advance you two paragraphs. This comes in handy with the next few commands…

### 刪除

The `x` command will delete the character under the cursor. `X` will delete the character before the cursor. This is where those number functions get fun. `6x` will delete 6 characters. Pressing `.` (dot) will repeat the previous command. So, lets say you have the word "foobar" in a few places, but after thinking about it, you’d like to see just “foo”. Move the cursor under the "b", hit `3x`, move to the next "foobar" and hit `.` (dot).

The `d` will tell Vim that you want to delete something. After pressing `d`, you need to tell Vim what to delete. Here you can use the movement commands. `dW` will delete up to the next word. `d^` will delete up unto the beginning of the line. Prefacing the delete command with a number works well too: `3dW` will delete the next three words. `D` (uppercase) is a shortcut to delete until the end of the line (basically `d$`). Pressing `dd` will delete the whole line.

To delete then replace the current word, place the cursor on the word and execute the command `cw`. This will delete the word and change to insert mode. To replace only a single letter use `r`.

### 取消和重做

Vim has a built-in clipboard (also known as a buffer). Actions can be undone with `u` and redone with `Ctrl+r`.

### 視覺模式

Pressing `v` will put you in visual mode . Here you can move around to select text, when you’re done, you press `y` to yank the text into the buffer (copy), or you may use `c` to cut. `p` pastes after the cursor, `P` pastes before. `V`, Visual Line mode, is the same for entire lines. `Ctrl+v` is for blocks of text.

**Note:** Whenever you delete something, that something is placed inside a buffer and is available for pasting.

### 搜尋和取代

To search for a word or character in the file, simply use `/` and then the characters your are searching for and press enter. To view the next match in the search press `n`, press `N` for the previous match.

To search and replace use the substitute `:s/` command. The syntax is: `[range]s///[arguments]`. For example:

```
Command        Outcome
:s/xxx/yyy/    Replace xxx with yyy at the first occurence
:s/xxx/yyy/g   Replace xxx with yyy first occurrence, global (whole sentence)
:s/xxx/yyy/gc  Replace xxx with yyy global with confirm
:%s/xxx/yyy/g  Replace xxx with yyy global in the whole file

```

You can use the global `:g/` command to search for patterns and then execute a command for each match. The syntax is: `[range]:g//[cmd]`.

```
Command  Outcome
:g/^#/d  Delete all lines that begins with #
:g/^$/d  Delete all lines that are empty

```

### 儲存和退出

To save and/or quit, you will need to use Ex mode. Ex mode commands are preceded by a `:`. To write a file use `:w` or if the file doesn’t have a name `**:w** filename`. Quitting is done with `:q`. If you choose not to save your changes, use `:q!`. To save and quit `:x`.

### 額外指令

1.  Pressing `s` will erase the current letter under the cursor, and place you in insert mode. `S` will erase the whole line, and place you in insert mode.
2.  `o` will create a newline below the line and put you insert mode, `O` will create a newline above the line and put you in insert mode.
3.  `yy` will yank an entire line
4.  `cc` will delete the current line and place you in insert mode.
5.  `*` will highlight the current word and `n` will search it

## 設定

Vim's user-specific configuration file is located in the home directory: `~/.vimrc`, and files are located inside `~/.vim/` The global configuration file is located at `/etc/vimrc`. Global files are located inside `/usr/share/vim/`.

The Vim global configuration in Arch Linux is very basic and differs from many other distributions' default Vim configuration file. To get some commonly expected behaviors (such as syntax highlighting, returning to the last known cursor position), consider using Vim's example configuration file:

```
# mv /etc/vimrc /etc/vimrc.bak
# cp /usr/share/vim/vim74/vimrc_example.vim /etc/vimrc

```

### 循環搜尋

With this option the *search next* behaviour allows to jump to the beginning of the file, when the end of file is reached. Similarly, *search previous* jumps to the end of the file when the start is reached.

```
set wrapscan

```

### 拼字檢查

```
set spell

```

With this setting, Vim will highlight incorrectly spelled words. Place the cursor on a misspelled word and enter `z=` to view spelling suggestions.

Only English language dictionaries are installed by default, more can be found in the [official repositories](/index.php/Official_repositories "Official repositories"). To get the list of available languages type:

```
# pacman -Ss vim-spell

```

Language dictionaries can also be found at the [Vim FTP archive](http://ftp.vim.org/vim/runtime/spell/). Put the downloaded dictionar(y/ies) into the `~/.vim/spell` folder and set the dictionary by typing: `:setlocal spell spelllang=LL`

**Tip:**

*   To enable spell checking for LaTeX (or TeX) documents only, add `autocmd FileType tex setlocal spell spelllang=en_us` into your `~/.vimrc` or `/etc/vimrc`, and then restart Vim. For spell checking of languages other than English, simply replace `en_us` with the value appropriate for your language.
*   To enable spelling in two languages (for instance English and German), add `set spelllang=en,de` into your `~/.vimrc` or `/etc/vimrc`, and then restart Vim.
*   You can enable spell checking for arbitrary file types (e.g. *.txt) by using the FileType plugin and a custom rule for file type detection. To enable spell checking for any file ending in `*.txt`, create the file `/usr/share/vim/vimfiles/ftdetect/plaintext.vim`, and insert the line `autocmd BufRead,BufNewFile *.txt setfiletype plaintext` into that file. Next, insert the line `autocmd FileType plaintext setlocal spell spelllang=en_us` into your `~/.vimrc` or `/etc/vimrc`, and then restart Vim.

### 語法標亮

To enable syntax highlighting (Vim supports a huge list of programming languages):

```
:filetype plugin on
:syntax on

```

### 使用滑鼠

Vim has the ability to make use of the mouse, but requires xterm's mouse reporting feature.

1.  See the example .vimrc below to enable the mouse.
2.  Use xterm. In your console: `export TERM=xterm-256color` or `export TERM=xterm`

Notes:

*   This even works in PuTTY over SSH.
*   In PuTTY, the normal highlight/copy behaviour is changed because Vim enters visual mode when the mouse is used. To select text with the mouse normally, hold down the `Shift` key while selecting text.

### 讓方向鍵通過斷行

By default, pressing `←` at the beginning of a line, or pressing `→` at the end of a line, will not let the cursor traverse to the previous, or following, line.

The default behavior can be changed by adding `set whichwrap=b,s,<,>,[,]` to your `~/.vimrc` file.

### ~/.vimrc 範例

一個範例 [Vim 設定](/index.php/Vim/.vimrc "Vim/.vimrc")。

## 插件

Adding plugins to vim can increase your productivity. The group vim-plugins has many plugins to choose from(there are more in the repos though ie: vim-supertab).

```
pacman -Ss vim-plugins

```

### cscope

[Cscope](http://cscope.sourceforge.net/) is a tool for browsing a project. By navigating to a word/symbol/function and calling cscope(usually with shortcut keys) it can find: functions calling the function, the function definition, and more. Multiple steps are required to search a code base.

Install the [cscope](https://www.archlinux.org/packages/?name=cscope) package.

Copy the cscope default file where it will be automatically read by vim:

```
mkdir -p ~/.vim/plugin
wget -P ~/.vim/plugin [http://cscope.sourceforge.net/cscope_maps.vim](http://cscope.sourceforge.net/cscope_maps.vim) 

```

Create a file which contains the files you wish cscope to index(Cscope can handle many languages but this example finds .c, .cpp, and .h files):

```
cd */path/to/projectfolder/*
find . -type f -print | grep -E '\.(c(pp)?|h)$' > cscope.files

```

Create database files that cscope will read:

```
cscope -bq

```

**Note:** You must browse your project files from this location or set and export the $CSCOPE_DB variable, pointing it to the cscope.out file.

Default keyboard shortcuts

```
 Ctrl-\ and
      c: Find functions calling this function
      d: Find functions called by this function
      e: Find this egrep pattern
      f: Find this file
      g: Find this definition
      i: Find files #including this file
      s: Find this C symbol
      t: Find assignments to

```

Feel free to change the shortcuts.

```
#Maps ctrl-c to find functions calling the function 
nnoremap <C-c> :cs find c <C-R>=expand("<cword>")<CR><CR>

```

### Taglist

[Taglist](http://vim-taglist.sourceforge.net/) provides an overview of the structure of source code files and allows you to efficiently browse through source code files in different programming languages.

Install the [vim-taglist](https://www.archlinux.org/packages/?name=vim-taglist) package.

Usefull options to be put in ~/.vimrc

```
let Tlist_Compact_Format = 1
let Tlist_GainFocus_On_ToggleOpen = 1
let Tlist_Close_On_Select = 1
nnoremap <C-l> :TlistToggle<CR>

```

## 合併檔案 (vimdiff)

Vim includes a diff editor, a program that aids the merging of differences between two (or more, with limited usefulness) files. `vimdiff` opens a horizontally multi-paned view that colorfully highlights differences, each pane containing one of the files to be examined/edited. Vim has [several modes](#Usage), two important ones being **Insert mode**, which lets text be edited, and **Command mode**, which lets the cursor be moved move across windows and lines. Begin by running `vimdiff file1 file2`. Some example commands follow.

	`]c`

	next difference

	`[c`

	previous difference

	`Ctrl+w+w`

	switch windows

	`i`

	enter Insert mode

	`Esc`

	exit Insert mode

	`p`

	paste

	`do`

	diff obtain. When the cursor is on a (highlighted) difference, copies the changes from the other window to the current one.

	`dp`

	diff put. Inverse of diff obtain; copies the changes from current windows to the other one.

	`zo`

	open folded text

	`zc`

	close folded text

	`:diffupdate` 

	re-scan the files for differences

	`yy`

	copy a line

	`dd`

	cut a line

	`:wq`

	save and exit the current window

	`:wqa`

	save and exit both windows

	`:q!`

	exit without saving

Once your file has been correctly edited, taking into account changes in file.pacnew:

```
# mv file file.bck
# mv file.pacnew file

```

Check whether your new file is correct, then remove your backup:

```
# rm file.bck

```

## Vim 提示

Specific user tricks to accomplish tasks.

### 行號

1.  Show line numbers by `:set number`.
2.  Jump to line number `:<line number>`.

### Substitute on lines

To only substitute between certain lines:

```
:*n*,*n*s/one/two/g

```

For example, to replace instances of 'one' with 'two' between lines 3 and 4, one would execute:

```
:3,4s/one/two/g

```

### Make Vim restore cursor position in files

If you want the cursor to appear in its previous position after you open a file, add the following to your `~/.vimrc`:

```
if has("autocmd")
au BufReadPost * if line("'\"") > 1 && line("'\"") <= line("$") | exe "normal! g`\"" | endif
endif

```

See also [this](http://vim.wikia.com/wiki/Restore_cursor_to_file_position_in_previous_editing_session) tip in Vim Wiki.

### Empty space at the bottom of gVim windows

When using a [window manager](/index.php/Window_manager "Window manager") configured to ignore window size hints, gVim will fill the non-functional area with the GTK theme background color.

The solution is to adjust how much space gVim reserves at the bottom of the window. Take note that if you set it to zero, you won't be able to see the bottom horizontal scrollbar, if you have one. Put the following line in `~/.vimrc`:

```
set guiheadroom=0

```

### 用 vim 取代 vi 指令

Create an [alias](/index.php/Bash#Aliases "Bash") for `vi` to `vim`.

## 疑難排解

### "^M"

There is a "^M" at the end of each line. This usually happens when you are editing a text file which was created in MS-DOS or Windows.

Solution: Replace all "^M" using the command:

 `:%s/^M//g` 

Pay attention, "^" is the control letter, press `Ctrl+Q` to get the right "^".

Alternatively, install the package [dos2unix](https://www.archlinux.org/packages/?name=dos2unix) from the official repositories, and run `dos2unix <file name here>`.

## 另請參閱

### 官方

*   [首頁](http://www.vim.org/)
*   [文件](http://vimdoc.sourceforge.net/)
*   [Tips Wiki](http://vim.wikia.com)

### 教學

*   [vi Tutorial and Reference Guide](http://usalug.org/vi.html)
*   [Graphical vi-Vim Cheat Sheet and Tutorial](http://www.viemu.com/a_vi_vim_graphical_cheat_sheet_tutorial.html)
*   [Vim Introduction and Tutorial](http://blog.interlinked.org/tutorials/vim_tutorial.html)
*   [Open Vim](http://www.openvim.com/) - Collection of Vim learning tools
*   [Learn Vim Progressively](http://yannesposito.com/Scratch/en/blog/Learn-Vim-Progressively/)
*   [know vim](http://www.knowvim.com/)

#### 影片

*   [Vimcasts](http://vimcasts.org/) - Screencasts in .ogg format.
*   [Tutorial Videos](http://www.derekwyatt.org/vim/vim-tutorial-videos/vim-novice-tutorial-videos/) - Covering the basics up to advanced topics.

#### 遊戲

*   [Vim Adventures](http://vim-adventures.com/)
*   [VimGolf](http://vimgolf.com/)

### 範例設定

*   [nion's](http://nion.modprobe.de/setup/vimrc)
*   [A detailed configuration from Amir Salihefendic](http://amix.dk/vim/vimrc.html)
*   [Bart Trojanowski](http://www.jukie.net/~bart/conf/vimrc)
*   [Steve Francia's Vim Distribution](https://github.com/spf13/spf13-vim)
*   [W4RH4WK's Vim configuration](https://github.com/W4RH4WK/dotVim)
*   [Fast vimrc/colorscheme from askapache](http://www.askapache.com/linux/fast-vimrc.html)

### 其他

*   [Vivify](http://bytefluent.com/vivify/) - A ColorScheme Editor for Vim