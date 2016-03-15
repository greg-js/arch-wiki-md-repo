[Audacious](http://audacious-media-player.org/) 是輕量級、自由軟體、基於GTK2開發的GUI音樂播放器， 注重音質且支援廣泛的音源編碼格式，並可透過第三方外掛程式擴充功能。

Audacious有著Winamp風格且支援面板更換，使用過WinAMP的人應該相當熟悉。

## Contents

*   [1 特性](#.E7.89.B9.E6.80.A7)
*   [2 安裝](#.E5.AE.89.E8.A3.9D)
*   [3 Audtool](#Audtool)
*   [4 GTK UI](#GTK_UI)
*   [5 標準 UI 面板](#.E6.A8.99.E6.BA.96_UI_.E9.9D.A2.E6.9D.BF)
    *   [5.1 使用 Winamp 面板](#.E4.BD.BF.E7.94.A8_Winamp_.E9.9D.A2.E6.9D.BF)
    *   [5.2 加入Winamp面板](#.E5.8A.A0.E5.85.A5Winamp.E9.9D.A2.E6.9D.BF)
*   [6 音樂 CD](#.E9.9F.B3.E6.A8.82_CD)
*   [7 OSS 支援](#OSS_.E6.94.AF.E6.8F.B4)

# 特性

*   支援眾多音源格式(and even more with [xmp](https://aur.archlinux.org/packages/xmp/) plugin),
*   PulseAudio, ALSA, OSS, Crossfade output (also file and null),
*   WAV, Vorbis, Mp3, FLAC transcoding,
*   Sound effects,
*   Visualization,
*   Scrobbler plugin, OSD, EvDev, status icon, alarm,
*   Streaming support

# 安裝

用[Pacman](/index.php/Pacman "Pacman")安裝：

```
pacman -S audacious

```

你可能會想安裝增加Audacious功能的一些外掛：

```
pacman -S audacious-plugins

```

# Audtool

Audacious附帶有威力強大的管理工具Audtool，可以從播放器取得資訊或控制播放器。

例如，取得目前播放的歌名或歌手：

```
audtool2 current-song

```

```
audtool2 current-song-tuple-data artist

```

基它還有播放控制、編輯播放列表、調整等化器和主視窗等功能。空整的選項列表在

```
audtool2 --help

```

# GTK UI

Audacious 2有選項可使用不同的UI(使用者介面)。 要使用新的 GTK UI，用以下方式啟動 audacious2

```
audacious2 -i gtkui

```

# 標準 UI 面板

## 使用 Winamp 面板

Audacious 支援 Winamp classic 面板，你可以在 Audacious 任意使用它們。 啟動方式:

```
audacious2 -i skinned

```

## 加入Winamp面板

加入 Winamp 面板到 Audacious 很簡單，只要複製你的面板(.zip, .wsz, .tgz, .tar.gz, 和 .tar.bz2 檔)到 **`/usr/share/audacious/Skins`**。 之後你就能在 主選單 > *Preferences* > *Skinned Interface* 選擇面板使用。

這些地方可以找到面板：

[http://www.customize.org/list/winamp2](http://www.customize.org/list/winamp2)

[http://www.deviantart.com/#catpath=customization/skins/media/winamp/classic](http://www.deviantart.com/#catpath=customization/skins/media/winamp/classic)

[http://www.1001skins.com](http://www.1001skins.com)

# 音樂 CD

```
pacman -S libcdio

```

在你安裝 libcdio 後， 播放音樂CD前用主選單(點右鍵開啟) > Plugin Services > Add CD

參考來源: [https://bbs.archlinux.org/viewtopic.php?id=40075](https://bbs.archlinux.org/viewtopic.php?id=40075)

# OSS 支援

當你使用的是 Open Sound System 而不是 ALSA，請確定 Audacious 設定有被設罝過。

只要在主選單中選擇：*Preferences*-->*Audio*-->*Current output plugin*-->***OSS Output Plugin***。