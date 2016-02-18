OCRdesktop is a useful accessibility tool to grab content from the screen as text via OCR technology.

It takes an image of the current window or workspace, prepares it for better results and uses tesseract to recognize text on it. The result is presented in a caret enabled text area, in a detailed list with coordinates and confidence or in the clipboard. It also can emulate clicks on the text. It consists of two main parts.

1\. The main window: This is a caret browsable text area with the recognized content. There is a menubar with many options. Focus the menu with `F10`

2\. The Macro executor: this is a window where you can choose to *Run*, *Unload*, *Load* or *Save* the current stored macros and preclicks. You also can skip running a macro by pressing the *cancel* button. (See [#Macros and the preclick concept](#Macros_and_the_preclick_concept)).

## Contents

*   [1 Installation](#Installation)
*   [2 Setup](#Setup)
*   [3 Using](#Using)
    *   [3.1 View Modes](#View_Modes)
    *   [3.2 OCR Language](#OCR_Language)
    *   [3.3 OCR Options](#OCR_Options)
        *   [3.3.1 Invert](#Invert)
        *   [3.3.2 Grayscale](#Grayscale)
        *   [3.3.3 Barrier Black White method](#Barrier_Black_White_method)
    *   [3.4 Help](#Help)
    *   [3.5 Recognize current workspace](#Recognize_current_workspace)
    *   [3.6 Emulate mouse events](#Emulate_mouse_events)
    *   [3.7 Macros and the preclick concept](#Macros_and_the_preclick_concept)
    *   [3.8 Emulate keyboard events](#Emulate_keyboard_events)
    *   [3.9 Handle Macros](#Handle_Macros)
    *   [3.10 Copy to clipboard](#Copy_to_clipboard)
    *   [3.11 Debug Mode](#Debug_Mode)

## Installation

Just [Install](/index.php/Install "Install") the package [ocrdesktop](https://aur.archlinux.org/packages/ocrdesktop/) from the [AUR](/index.php/AUR "AUR"). Make sure that you have the corresponding tesseract-data-<languagecode> package for your language installed.

## Setup

Assign the command `ocrdesktop` to a shortcut in your desktop environment. You also can use parameters to expand the function of OCRdesktop. For languages other than english, you need to set your language code `ocrdesktop -l <languagecode>`. Use the tesseract language codes for <languagecode>

Basically, this should work in any desktop environment.

In Gnome you can do this via the *Gnome Control Center* in the *Keyboard* window under the *Shortcuts* tab.

## Using

Just press the assigned shortcut. With no parameters, OCRdesktop will recognize just the current window and present it in a caret enabled text area.

### View Modes

OCRdesktop provides different view modes. You can toggle between the modes with `Ctrl+v`

*   Browse mode: show all the text in a caret navigatable textbox. The view presents the layout of the currently recognized content. You can move the caret with the arrow keys.
*   Detail mode: This is basically a list where you can see details for any word on the Browse mode. I.e fontsize, fontcolor, position on the screen (X, Y), confidence of the OCR process and other attributes. Things like fontsize or color are approximate values because its calculated by the ocr image. Some characters are visually smaller than others, So there is a little difference.

### OCR Language

OCRdesktop is able to use all available tesseract languages with `-l <language code>`. If no language is set. OCRdesktop will use english.

 `$ *ocrdesktop -l deu*` 

You can also set more than one OCR language

 `$ *ocrdesktop -l deu+eng*` 

### OCR Options

OCRdesktop always upscales the current screenshot 3 times for better results. Besides this, you can use different types of transformations before OCRdesktop attempts to recognize the text. You can start OCRdesktop with the parameter you want, or select the options in the navigation window via the *OCR Options* submenu of the *OCRdesktop* menu. After selecting the options, press `F5` to recognize the text again. This is a little trial and error for better results. Autodetection may be be implemented in a later version.

**Tip:** You can also combine different options.

#### Invert

Inversion of the colours could lead to better results if the colours in the original image cause problems with the text recognition.

 `$ *ocrdesktop -i*` 

#### Grayscale

Here the colour is removed overall. We get a range of different tones of gray, which could lead to less confusion of tesseract.

 `$ *ocrdesktop -g*` 

#### Barrier Black White method

This may be the method that most often leads to the best results. Grayscale is always active. The different tones of gray will break on a defined value between 0 (white) and 255 (black). Everything less than the defined point will be converted to black. A gray tone equal or greater is converted into white. This leads to a clean image for OCR. No Colours, no noise, no grayscale, just black and white. With this type of image tesseract could also read realy bright colour fonts (because they are converted into black) The parameter `-b` activates this feature. The parameter `-t <barriervalue>` sets the barrier value. <barriervalue> is a integer between 0 and 255\. If `-t` is not set, 200 is the default value.

 `$ *ocrdesktop -b -t 180*` 

### Help

You can see a little help and the available parameters if you enter the following in a terminal.

 `$ *ocrdesktop -h*`  `$ *man ocrdesktop*` 

You can always mix different parameters.

### Recognize current workspace

If you do not want to restrict recognition to the current window, use the -d option.

 `$ *ocrdesktop -d*` 

### Emulate mouse events

You can emulate clicks on the word at the current cursor position via the *Interact* menu.

Shortcuts:

*   Single left click (`Ctrl+l`): common for selecting/activating entry's
*   Double left click (`Ctrl+d`): common for opening entry's in the same window
*   Single right click (`Ctrl+r`): open the context menu for the object under the mouse
*   Single middle click (`Ctrl+m`): Usually opens an object in a new tab
*   Route the mouse over an Object (`Ctrl+t`): used for mouse over events like tool tips

for doing a mouse operation immediately: Place the mouse on the word in the text area or list entry (in the list view) and press on the corresponding shortcut.

### Macros and the preclick concept

The concept of preclicks is not easy to understand at first, but it solves a really easy to understand problem.

In most desktop environments, global shortcuts don't work while a menu is open, (for example the *file* menu in the menu bar at the top of most programs).

Preclicks are basically macros that can be run before OCRdesktop takes its screen shot. This allows you to close all menus and let OCRdesktop click on the menu before it recognizes the window. Preclicks macros are really easy to use. In the *Interact* menu is a check box *Preclick* `Ctrl+p`. Set this check box and choose a mouse click that should be performed before OCRdesktop starts the next time, much the same as doing a normal mouse click emulation ( see [#Emulate mouse events](#Emulate_mouse_events)). After emulating a mouse click, nothing will happen. Next time you run OCRdesktop, it will ask you what to do. You can press *Run*, so all stored clicks will execute. After that, OCRdesktop takes its screen shot for OCR (with the opened menu). If you now check the *Preclick* option again the second click will also be stored, (e.g. for opening a sub menu). You can save as many mouse operations as you want. Choose *Unload* in the macro window to erase the macro, so its lost. If you press *Cancel*, no mouse clicks are performed, but the main window opens. The macro will not be deleted and you will be asked next time you start OCRDesktop if you want to run your stored clicks.

**Tip:** The active preclick macro file is stored under `~/.activeOCRMacro.ocrm`.

You can execute an existing macro file stored anywhere on the hard disk by using the `-m </path/to/macro/macroname.ocrm>` option.

 `$ *ocrdesktop -m </path/to/macro/macroname.ocrm>*` 
**Tip:** You can combine it with the `-n` option. OCRdesktop will just start the click sequence for you without any GUI.

### Emulate keyboard events

You can also fire keyboard shortcuts into the preclick macros. To enter the shortcut recording mode, press `Ctrl+k` or select the *Send Key* menue entry in the *Interact* menu. Now every keystroke you type is appended to the currently active preclick macro. Pressing `F4` will leve the recording mode. Leving the shortcut recording mode may have a delay of up to 2 seconds. This is a known issue.

### Handle Macros

You can Save, Load, Unload or Run the current macro from the *macro* menu.

*   Save (`Ctrl+s`): save a macro on the filesystem, in case you need it more often.
*   Load (`Ctrl+o`): loading meens that this macro will be started the next time OCRdesktop runs
*   Unload (`Ctrl+u`): remove the macro from the buffer and prevent it from running. If you loaded the macro from the filesystem, the original macro file won´t be used
*   Run (`Ctrl+n`): close the window an just run the macro now

### Copy to clipboard

OCRdesktop provides the possibility to send the currently recognized content to the clipboard.

This is easily done by specifying the `-c` option.

 `$ *ocrdesktop -c*` 

This opens the main window and sends the content to the clipboard. If you dont want to open the main window, you could add the "no GUI" option `-n`.

 `$ *ocrdesktop -c -n*` 
**Tip:** you can always use the short term. `$ *ocrdesktop -cn*` 

Now you have the recognized text in the clipboard and no window appears.

You can also press `Ctrl+b` when the GUI is open.

### Debug Mode

You can start the debugmode with the `-v` option.

 `$ *ocrdesktop -v >> /tmp/debug.out*` 

The debug output is send to the std output. So you have to pipe it.

**Tip:** OCRdesktop stores a copy of all images (original, upscaled and manipulated) in /tmp/ in debug mode