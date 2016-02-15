## Contents

*   [1 全局设置](#.E5.85.A8.E5.B1.80.E8.AE.BE.E7.BD.AE)
*   [2 用户设置](#.E7.94.A8.E6.88.B7.E8.AE.BE.E7.BD.AE)
    *   [2.1 X](#X)
    *   [2.2 控制台](#.E6.8E.A7.E5.88.B6.E5.8F.B0)
    *   [2.3 使用 ALSA](#.E4.BD.BF.E7.94.A8_ALSA)
    *   [2.4 在 GNOME/Metacity 中](#.E5.9C.A8_GNOME.2FMetacity_.E4.B8.AD)
    *   [2.5 GTK+](#GTK.2B)
*   [3 附加资源](#.E9.99.84.E5.8A.A0.E8.B5.84.E6.BA.90)

## 全局设置

可以通过在[内核模块](/index.php/%E5%86%85%E6%A0%B8%E6%A8%A1%E5%9D%97 "内核模块")中移除 `pcspkr` 模块来完全禁用PC喇叭：

```
# rmmod pcspkr

```

**注意:** 将 `pcspkr` 模块加入[黑名单](/index.php/%E5%86%85%E6%A0%B8%E6%A8%A1%E5%9D%97#.E9.BB.91.E5.90.8D.E5.8D.95 "内核模块")的旧方法会阻止 [udev](/index.php/Udev "Udev") 在启动时加载。

## 用户设置

### X

```
$ xset -b

```

将这条命令加入启动文件, 例如 `~/.xinitrc`, 可以在每次X启动时关掉PC喇叭.

### 控制台

```
$ setterm -blength 0

```

和上面方法类似, 将这条命令加入 `~/.bashrc` 中就可以在每次登入控制台时关掉PC喇叭.

*   另一种方法是将下面的命令加入 `~/.inputrc`:

```
$ set bell-style none

```

### 使用 ALSA

**Tip:** 大部分 Intel 声卡不会显示在 alsamixer 的默认设备中，请按 F6, 选择 "HDA Intel PCH"，这里会有一个 "Beep"。

*   如果使用 ALSA, 可以试试下面的命令关掉 PC 喇叭：

```
$ amixer set 'PC Speaker' 0% mute

```

对某些声卡，PC 喇叭在 PC Beep 中：

```
$ amixer set 'PC Beep' 0% mute

```

或者只是 Beep：

```
$ amixer set 'Beep' 0% mute

```

你也可以在终端中使用 alsamixer

```
$ alsamixer

```

滚动到 PC beep 然后按 `M` 键静音。保存 alsa 设置：

```
# alsactl store

```

**注意:** 不是每一个声卡都会在 alsamixer 中创建 PC Speaker 或者 PC Beep 滑动控制条。

### 在 GNOME/Metacity 中

在 Gconf 中设置 **`/apps/metacity/general/audible_bell`**  为 **`false`:**

```
$ gconftool-2 -s -t string /apps/metacity/general/audible_bell false

```

### GTK+

将下行加入`.gtkrc-2.0`和`$XDG_CONFIG_HOME/gtk-3.0/settings.ini`的[Settings]部分：

```
gtk-error-bell = 0

```

## 附加资源

*   查看这些 `man` 页面获取更多信息： `xset(1)`, `setterm(1)`, `readline(3)`.
*   [内核模块](/index.php/%E5%86%85%E6%A0%B8%E6%A8%A1%E5%9D%97 "内核模块")