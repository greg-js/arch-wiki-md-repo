**羅技木星軌跡球**具有四個按鍵，且是對稱的，因而不論左右手都適合使用。[Picture](http://www.logitech.com/assets/21083/21083.png)缺點是不具滾輪功能，但可以設定來啟用此功能。

## Contents

*   [1 安裝](#.E5.AE.89.E8.A3.9D)
*   [2 基本功能](#.E5.9F.BA.E6.9C.AC.E5.8A.9F.E8.83.BD)
*   [3 配置](#.E9.85.8D.E7.BD.AE)
    *   [3.1 按鍵與軌跡球](#.E6.8C.89.E9.8D.B5.E8.88.87.E8.BB.8C.E8.B7.A1.E7.90.83)
        *   [3.1.1 指定按鍵](#.E6.8C.87.E5.AE.9A.E6.8C.89.E9.8D.B5)
        *   [3.1.2 雙擊大按鍵](#.E9.9B.99.E6.93.8A.E5.A4.A7.E6.8C.89.E9.8D.B5)
        *   [3.1.3 滾輪修正鍵](#.E6.BB.BE.E8.BC.AA.E4.BF.AE.E6.AD.A3.E9.8D.B5)
    *   [3.2 左撇子或右撇子](#.E5.B7.A6.E6.92.87.E5.AD.90.E6.88.96.E5.8F.B3.E6.92.87.E5.AD.90)
    *   [3.3 System-wide or per-user](#System-wide_or_per-user)
    *   [3.4 Xorg input hotplugging](#Xorg_input_hotplugging)
    *   [3.5 Without Xorg hotplugging](#Without_Xorg_hotplugging)
*   [4 Sample configuration](#Sample_configuration)
    *   [4.1 Configuration file](#Configuration_file)
    *   [4.2 Restarting X](#Restarting_X)
*   [5 Minimal configuration](#Minimal_configuration)
    *   [5.1 Using evdev](#Using_evdev)
    *   [5.2 Using libinput](#Using_libinput)
*   [6 Additional tweaks](#Additional_tweaks)
    *   [6.1 Console (gpm)](#Console_.28gpm.29)
    *   [6.2 Chromium browser](#Chromium_browser)
    *   [6.3 Firefox browser](#Firefox_browser)
*   [7 See also](#See_also)

## 安裝

無缺額外驅動程式。在系統啟動或在已開啟系統中連接時，即可偵測到羅技木星。羅技木星雖然可以當作一般滑鼠來使用，不進行設定，然而你可能想要啟用滾輪功能或客制化按鍵。

## 基本功能

無論何種硬體設定，木星的硬體ID固定的。

當沒有額外設定時，按鈕會為下列功能：

| ID | 硬體動作 | 結果 |
| 1 | 左大按鍵 | 左鍵 |
| 2 | 雙擊（大按鍵） | 中鍵 † |
| 3 | 右大按鍵 | 右鍵 |
| 4 | 「無」 | - |
| 5 | 「無」 | - |
| 6 | 「無」 | - |
| 7 | 「無」 | - |
| 8 | 左小按鍵 | 上一頁 |
| 9 | 右小按鍵 | 下一頁 |

**Note:**

*   大按鍵雙產生「中鍵」
*   † 同時按壓按鍵需要 `Emulate3buttons`.
*   本文中「中鍵」、「滾輪鍵」同意義。
*   「選擇鍵」、「右鍵」同義，一般用於彈出選單。
*   以上結果，不按壓修正鍵（modifier key）
*   若按壓修正鍵結果可能不相同

| ID | 硬體動作 | 結果 |
| 4 | 球體向下 | 鼠標向下 |
| 5 | 球體向上 | 鼠標向上 |
| 6 | 球體向左 | 鼠標向左 |
| 7 | 球體向右 | 鼠標向右 |

**Note:**

*   不使用修正鍵時，鼠標移動。
*   使用修正鍵時，結果可能不盡相同。
*   「修正鍵」可以是一個鍵盤按鍵（如：Ctrl）或是木星上的按鍵。

**Note:** 當**[scroll mod­ifier](#Scroll_modifier)**按壓同時滾動軌跡球，便可將軌跡球當滾輪使用。你必需到少配置**[minimal configuration](#Minimal_configuration)**來啟用這個功能。

在「滾輪模式」使用軌跡球時，也可使用一些滑鼠手勢的功能，例如，在同時按壓Ctrl鍵跟滾動滾輪可以縮放瀏覽器中的字體。使用軌跡球時，則需同時按壓Ctrl與「滾輪模式按壓鍵」來觸發功能。

## 配置

你可以參考及嘗試這個 [簡易配置](#Sample_configuration)。

這個配置含有一些資訊，大部份的Arch使用者使用的現行X server的配置是需要udev熱插拔。

**Note:** 可參考May 2012五月的這篇[Gnome 3 and middle click emulation](http://who-t.blogspot.com.au/2011/04/gnome-30-middle-mouse-button-emulation.html). See [#"Both-large-buttons" combination-click](#.22Both-large-buttons.22_combination-click)

可在Ubuntu 12.04 的Gnome 3環境下使用。

### 按鍵與軌跡球

```
[簡單配置](#Configuration_file)依照你的喜好修改後，放置在正確位置即可使用。

```

#### 指定按鍵

藉由設定參數，你可以指定功能給不同按鍵。

按鍵的值可以修改為1、2、3、8、及9（2是雙擊兩個大按鍵），但不要調整成4、5、6、或7。

```
# 此行是不同的按鈕配置
Option "ButtonMapping" "1 2 3 4 5 6 7 8 9"

```

左手使用需要使用不同的按鈕動作。

```
# 此行是左手使用都的按鈕配置（僅按鍵左右交換）
Option "ButtonMapping" "3 2 1 4 5 6 7 8 9"

```

對小按鈕，不喜歡「原始」配置可以修改按鍵的值

這一行修改按鈕2成「上一頁」。參數2（雙擊大按鈕）的值修改9，改成「上一頁」。此行也將參數8、9的值都改為2，使兩個小按鈕都各別修改成「中鍵」。

```
# 這是給右手使用者的，修改了三個按鈕
Option "ButtonMapping" "1 9 3 4 5 6 7 2 2"

```

參數按順序排列，參數1、2、3、8、9可修改，但軌跡的移動的參數4、5、6、7 不要修改。

#### 雙擊大按鍵

如前述，參數2是表示兩個大按鍵同時按下。

經試驗，在缺少設定的情形下，會產生不可確定的結果， 而非預期的「中鍵」。然而，若要雙擊能正確使用，你需要啟用「相黏鍵」功能：

```
# Emulate3Buttons 係指同時按下按鍵A與D
# 同時按可以模擬「中鍵」或「滾輪鍵」
Option "Emulate3Buttons" "true"

```

可以使用預設2（滾輪鍵），請參[minimal configuration](#Minimal_configuration)。

在2012五月些文章[Gnome 3 and middle click emulation](http://who-t.blogspot.com.au/2011/04/gnome-30-middle-mouse-button-emulation.html)顯示，在ubuntu 12.04 Gnome 3的環境下，預設值會變成 「false」而成為「中鍵」，原因是Gnome在Xorg進行設定（即Gnome的設定覆蓋了Xorg的設定），使的模擬被取消了。可由以下令命修正Gnome的行為：

```
gsettings set org.gnome.settings-daemon.peripherals.mouse middle-button-enabled true

```

每個使用者僅需下一次令命即可，Gnome會記得這個設定。如果你感興趣可以參考 [launchpad bug](https://bugs.launchpad.net/ubuntu/+source/xserver-xorg-input-evdev/+bug/874237/comments/13)。

#### 滾輪修正鍵

羅技木星軌跡球的一個嚴重缺點是沒有滾輪或是滾輪環，但可以藉由設定「滾輪修正鍵」來克服這個問題，即按下一個按鈕，使得軌跡球的滾動變成滾輪。雖然，預設已有提供滾輪修正鍵的功能(參 [基本功能](#Basic_function))，但滾動修正鍵並沒有被啟用。若要啟用，必需設定給不同的按鍵。

**Note:** 除了滾動功能外，滾輪鍵還有「點」的功能。滾輪修正鍵的「長壓」與「點」的功能是分開的，較佳可將兩個小按鍵之一設定成滾輪修正鍵。 原本小按鍵的預設功能也不甚方便，我建議你重新設定它們。

小按鍵的原設定是滾動修正鍵，但同時該小按鍵的「點」的預設功能是「上一頁」，根據多年的使用經驗，建議設成「中鍵」。

撇開關於小按鍵的抱怨不談，你可以如下設定「滾輪修正鍵」

```
Option "EmulateWheel" "true"
Option "EmulateWheelButton" "8"

# 按鍵8是左邊的小按鍵，適合右手使用者。
# 按鍵9是右邊的小按鍵，適合左手使用者。
# 按鍵2不可設定成「滾輪修正鍵」（又稱做"EmulateWheelButton"）

```

**取消水平捲動** 你可以取消下行的註解，來取消水平捲動。

```
# 井字號是註解
# Option "XAxisMapping" "6 7"

```

雖然我使用兩個方向的捲動，但不少人認為單一方向的捲動比較好用。 也許你想嘗試取消垂直方向的捲動，但是類似設定是不能取消垂直方向捲動的。

### 左撇子或右撇子

前面章節已經說明如何設定給右手或左手使用的設置。

*   你可能經常的左右手交替使用
*   我會在我感到不適前交替

為了左右手交替，我會手動修改配置（加註一些內容）後[重啟X server](#Restarting_X)。你也可以依你需要自已寫一些Script自動化這些步驟。

*   在Arch Linux上，我建議使用輕量的**[Openbox](/index.php/Openbox "Openbox")**做視窗管理。

在其他的桌面環境中，可能有一些簡單（或複雜）的小工具做左右手交替的設定。例如，Ubuntu 10.10中，你可以點擊一個滑鼠控制的面版按鈕即進行交替。

### System-wide or per-user

**Note:** Section undergoing revision. Please jump to the sample configuration

If you want the configuration to be system wide, you can add this line to the InputDevice-Section.

```
Option "ButtonMapping" "1 8 3 2 9"

```

For a per-user-configuration you need to put this in your ~/.Xmodmap

```
pointer = 1 8 3 4 5 6 7 2 9 10 11 12 13

```

or this in your ~/.xinitrc.

```
xmodmap -e "pointer = 1 8 3 4 5 6 7 2 9 10 11 12 13"

```

### Xorg input hotplugging

**Note:** Section undergoing revision. Please jump to the sample configuration

Two expositions help you configure a trackball with buttons for click, middle-click, right-click, and scrolling. The first exposition uses [Xorg Input Hotplugging](/index.php/Xorg#Input_devices "Xorg"); the second does not. Edit them to suit your preferences.

Add this entry to your `/etc/X11/xorg.conf`:

```
Section "InputClass"
    Identifier   "Logitech Trackball"
    MatchProduct "Trackball"
    Option       "ButtonMapping"      "1 8 3 4 5 6 7 2 9"
    Option       "EmulateWheel"       "True"
    Option       "EmulateWheelButton" "9"
    Option       "XAxisMapping"       "6 7"
EndSection

```

To learn more about the used parameters you should read the apropriate section in the evdev man page.

### Without Xorg hotplugging

**Note:** Section undergoing revision. Please jump to the sample configuration

The mouse device entry in `/etc/X11/xorg.conf` should look like this:

```
Section "InputDevice"
    Identifier "Mouse0"
    Driver     "mouse"
    Option     "CorePointer"
    Option     "Device"             "/dev/input/mice"
    Option     "Protocol"           "ExplorerPS/2"
    Option     "Buttons"            "9"
    Option     "ZAxisMapping"       "4 5"
    Option     "XAxisMapping"       "6 7"
    Option     "EmulateWheelButton" "9"
    Option     "EmulateWheel"       "true"
EndSection

```

The `"Auto"` option for `"Protocol"` works fine, too. Of course you can use the name you prefer as the `Identifier`, as long as it is the same you use as `InputDevice` in the `Section "ServerLayout"` .

## Sample configuration

The sample configuration modifies and extends the [basic function](#Basic_function) of the Marble Mouse.

In this example, either of the two small buttons may be clicked to send a ***wheel-click***. Wheel-click means the same as "middle-click" here. In addition, one of the small buttons provides ***scrolling*** in conjunction with the trackball. Note that only *one* small button has the ability for scrolling, although both small buttons are able to *wheel-click.*

Finally, clicking both large buttons simultaneously sends the ***browser back*** event. There is no button to send *browser forward*.

| ID | Hardware Action | Result (this configuration) | New assignment |
| 1 | Large button left | normal click | 1 |
| 2 | Both large buttons | browser back | 8 |
| 3 | Large button right | right-click | 3 |
| 8 | Small button left † | wheel-click | 2 |
| 9 | Small button right ‡ | wheel-click | 2 |

**Note:**

*   Both large buttons pressed simultaneously results in *browser back*.
*   Either small button, when clicked, results in *middle-click*.
*   † This small button allows trackball scrolling when held down. It is the scroll modifier.
*   ‡ This button can be mapped for scrolling function instead. This button works better for left-side placement because it lies near the thumb of one's left-hand. Only one button can be assigned as the scroll modifier as far as I know.

### Configuration file

The following lines are appended to **`/etc/X11/xorg.conf.d/10-evdev.conf`**

**Note:** *Users of other Linux distributions may find the configuration file in another location. Ubuntu uses /usr/share/X11/xorg.conf.d/10-evdev.conf*

This example is set up for right-hand placement with horizontal scrolling disabled.

```
#       - - - Logitech Marble Mouse Settings - - -
#
#       The Logitech Marble Mouse buttons are mapped [A-D] from left to right: 
#       A (large); B (small) |  C (small); D (large). 
#
#       Preferred options for right-handed usage:
#       A = normal click [1]  
#       B = middle-click [2] 
#       C = middle-click [2] 
#       D = right-click [3]
#       Hold button B while rolling trackball to emulate wheel-scrolling. 
#
#       Preferred options for left-handed usage:
#       A = right-click [3]  
#       B = middle-click [2] 
#       C = middle-click [2]
#       D = normal click [1]
#       Hold button C while rolling trackball to emulate wheel-scrolling.
#       Pressing both large buttons simultaneously (b) produces a "back" action.

Section "InputClass"
        Identifier  "Marble Mouse"
        MatchProduct "Logitech USB Trackball"
        MatchIsPointer "on"
        MatchDevicePath "/dev/input/event*"
        Driver "evdev"

#       Physical button #s:     A b D - - - - B C    
#       Option "ButtonMapping" "1 8 3 4 5 6 7 2 2"   right-hand placement
#       Option "ButtonMapping" "3 8 1 4 5 6 7 2 2"   left-hand placement
#       b = A & D 
        Option "ButtonMapping" "1 8 3 4 5 6 7 2 2"

#       EmulateWheel: Use Marble Mouse trackball as mouse wheel 
#       Factory Default: 8; Use 9 for right side small button
        Option "EmulateWheel" "true"
        Option "EmulateWheelButton" "8"

#       EmulateWheelInertia: How far (in pixels) the pointer must move to
#       generate button press/release events in wheel emulation mode.
#       Factory Default: 50
        Option "EmulateWheelInertia" "10"

#       Axis Mapping: Enable vertical [ZAxis] and horizontal [XAxis] scrolling
        Option "ZAxisMapping" "4 5"
#       Option "XAxisMapping" "6 7"

#       Emulate3Buttons: Required to interpret simultaneous press of two large
#       buttons, A & D, as a seperate command, b.
#       Factory Default: true
        Option "Emulate3Buttons" "true"
EndSection

```

### Restarting X

Changes made to xorg configuration files do not take effect until the X session is restarted. To restart the X session, simply log out from your window manager and log back in.

Or, depending on what display manager you use, you can use one of the following commands:

Default Ubuntu (with LightDM) : `sudo restart lightdm`

Gnome (with GDM) : `sudo restart gdm`

KDE (with KDM) : `sudo restart kdm`

## Minimal configuration

### Using evdev

At times it can be useful to start with the absolute minimum and build from there. This is one facet of [The Arch Way](/index.php/The_Arch_Way "The Arch Way"). In this spirit, I decided to see how few lines I might use to create a usable Marble Mouse configuration.

You can omit *all* configuration lines and the Marble Mouse is still usable for basic pointing and clicking. However, it will not be able to scroll. The "both-large-button" simultaneous click produces indeterminate results — experimentation shows this.

Given that you are satisfied with [default button settings](#Basic_function) and you wish only to enable scrolling and the "both-large-button" click, you need these lines. The following lines are appended to **`/etc/X11/xorg.conf.d/10-evdev.conf`**.

```
Section "InputClass"
        Identifier  "Marble Mouse"
        MatchProduct "Logitech USB Trackball"
        Option "EmulateWheel" "true"
        Option "EmulateWheelButton" "8"
        Option "XAxisMapping" "6 7"
        Option "Emulate3Buttons" "true"
EndSection

```

### Using libinput

As of version 3.16 GDM/Gnome uses libinput. For the device to work as described in the above section (note that wheel click emulation is not yet supported by libinput) you need to install [xf86-input-libinput](https://www.archlinux.org/packages/?name=xf86-input-libinput) and instead append this to `/etc/X11/xorg.conf.d/10-libinput.conf`.

 `/etc/X11/xorg.conf.d/10-libinput.conf` 
```
Section "InputClass"
        Identifier      "Marble Mouse"
        MatchProduct    "Logitech USB Trackball"
        Driver          "libinput"
        Option          "ScrollMethod" "button"
        Option          "ScrollButton" "8"
EndSection

```

## Additional tweaks

### Console (gpm)

See [Console mouse support](/index.php/Console_mouse_support "Console mouse support") for details. Within the console you can use `gpm` with type option set to **imps2**. Edit **`/etc/conf.d/gpm`** such that:

```
GPM_ARGS="-m /dev/input/mice -t imps2"

```

This lets you use the large left button for selecting text and the right button to extend the selection. The small left button acts as a middle-click; it pastes the selection.

### Chromium browser

By default, Chromium treats a middle-click as a *paste* command. This choice stems from "Linux tradition", not the capricious whim of one developer. Like myself, you may prefer a ***Windows*** approach. I want the middle button(s) to initiate *automatic scrolling,* not *pasting*:

*   A browser extension **AutoScroll** allows middle-click to initiate automatic scrolling.
*   This extension is helpful for any Linux user with a wheel mouse, not just Marble Mouse users.
*   A middle-click initiates automatic scrolling when clicked on a blank area of a web page.

*   When you program both small buttons to emit middle-click, either button can initiate automatic scrolling. That is a click function.
*   When you program one of the small buttons to act as scroll modifier (mouse setup), you can manually scroll web pages **without** fixing the browser. That is a press‑and‑hold function. (I recommend installing AutoScroll even though it is not absolutely necessary for scrolling.)
*   After you assign the scroll modifier to one of the small buttons, the small buttons act a bit differently from one another. The difference is seen when you compare their "press‑and‑hold" behaviors.

Be sure to install ***AutoScroll***; the similarly-named *Auto Scroll* extension implements a different feature.

This information also applies to the browser called **Google Chrome**.

### Firefox browser

Older versions of Firefox map horizontal-scrolling hardware to perform ***browser back*** and ***browser forward*** navigation.

This makes vertical scrolling using the trackball almost impossible.

The slightest horizontal motion triggers a URL redirection. To fix this:

*   Enter `about:config` in the location bar
*   Find the internal variable named `mousewheel.horizscroll.withnokey.action`. Set its value to **0**.
*   It may be useful to set `mousewheel.horizscroll.withnokey.numlines` to **1** as well.

## See also

*   Arch wiki documentation: [All Mouse Buttons Working](/index.php/All_Mouse_Buttons_Working "All Mouse Buttons Working")
*   Arch wiki documentation: [Xorg#Configuration](/index.php/Xorg#Configuration "Xorg")
*   Marble mouse scroll wheel: [Replacement for SetPoint driver](http://simans.net/marble/)
*   Joe Shaw blog post: [Linux input ecosystem](http://joeshaw.org/2010/10/01/681/)
*   Ubuntu community: [Logitech Marble Mouse](https://help.ubuntu.com/community/Logitech_Marblemouse_USB)
*   Chrome web store: [AutoScroll extension](https://chrome.google.com/webstore/detail/occjjkgifpmdgodlplnacmkejpdionan)