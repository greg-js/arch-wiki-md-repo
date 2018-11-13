## Contents

*   [1 安装](#安装)
*   [2 入法單](#入法單)
    *   [2.1 中文](#中文)
        *   [2.1.1 Ibus-rime 注音設置範例](#Ibus-rime_注音設置範例)
            *   [2.1.1.1 標點符號](#標點符號)
    *   [2.2 日語](#日語)
    *   [2.3 韓語](#韓語)
*   [3 運行](#運行)
*   [4 問題](#問題)
    *   [4.1 ibus-table：輸入繁體中文](#ibus-table：輸入繁體中文)

## 安装

```
# pacman -S ibus

```

## 入法單

*   ibus-anthy: A Japanese IME, based on [anthy](https://www.archlinux.org/packages/?name=anthy).
*   [ibus-rime](https://www.archlinux.org/packages/?name=ibus-rime): A powerful and smart Chinese input method for Chinese (拼音, 注音, with or without tones, double pinyin, Jyutping, Wugniu, Cangjie5 and Wubi 86) (AUR)
*   ibus-hangul: A Korean IME, based on [libhangul](https://www.archlinux.org/packages/?name=libhangul).
*   ibus-unikey: An IME for typing Vietnamese characters.
*   ibus-table: An IME that accommodates table-based IMs. You can also install `ibus-table-chinese` from AUR.

### 中文

如果您要用注音、拼音、倉頡5、五筆86，你可以用ibus-rime：

```
$ yaourt -S ibus-rime

```

#### Ibus-rime 注音設置範例

首先到以下目錄：

```
$ cd ~/.config/ibus/rime

```

在此目錄下建立 `default.custom.yaml`，加入以下：

 `default.custom.yaml` 
```
patch:
  schema_list:
    - schema: bopomofo

```

注意：縮排次序很重要。這份文件會向 Rime 表明，將方案選單改成這份只包含 bopomofo (注音) 的選單。

下面是可以使用的方案清單：

```
- luna_pinyin   (拼音)
- terra_pinyin  (拼音跟聲調)
- combo_pinyin  (宮保拼音)
- bopomofo      (注音)
- double_pinyin (自然碼雙拼)
- cangjie5      (倉頡五代)
- wubi86        (五笔86)
- stroke_simp   (五笔画)
- jyutping      (粵拼)
- wugniu        (吳語)
- zyenpheng     (中古漢語拼音)

```

編輯完成後，記得在 Rime 的語言面板上按下 'Deploy' 重整。

使用 Rime 時，只需按 `F4`，就可以選擇方案：

```
1\. 注音
2\. 中文　－›　西文
3\. 全角　－›　半角
4\. 漢字　－›　汉字
……

```

##### 標點符號

您可以用 Rime 打出中文的所有標點符號。下面是一些按鍵示例：

```
[ -> 「　【　〔　［
] ->　」　】　〕　］
{ ->　『　〖　｛
} ->　』　〗　｝
< ->　《　〈　«　‹
> ->　》　〉　»　›
@ ->　＠　@　☯
/ ->　／　/　÷
* ->　＊　*　・　×　※
% ->　％　%　°　℃
$ ->　￥　$　€　£　¥
| ->　・　｜　|　§　¦
_ -> ——
\ ->　、　＼　\
^ ->　……
~ ->　〜　~　～　〰

```

### 日語

Just install ibus-anthy:

```
$ yaourt -S ibus-anthy

```

### 韓語

Just install ibus-hangul:

```
$ yaourt ibus-hangul

```

## 運行

```
# ibus-daemon &

```

## 問題

### ibus-table：輸入繁體中文

安裝後，若簡繁寫法不同的字不能輸入，例如 “體（体）” ，"個（个）"等，請修改以下文件，然後重新啟動 ibus-daemon。

```
# sudo vim /usr/share/ibus-table/engine/table.py 

```

```
 108     def get_chinese_mode (self):
 109         '''Use LC_CTYPE in your box to determine the _chinese_mode'''
 110         try:
 111             if os.environ.has_key('LC_CTYPE'):
 112                 __lc = os.environ['LC_CTYPE'].split('.')[0].lower()
 113             else:
 114                 __lc = os.environ['LANG'].split('.')[0].lower()
 115 
 116             if __lc.find('zh_') == 0:
 117                 # this is a zh_XX
 118                 __place =__lc.split('_')[1]
 119                 if __place == 'cn':
 120                     return 0
 121                 else:
 122                     return 1
 123             else:
 124                 if self.db._is_chinese:
 125                     # if IME declare as Chinese IME
 126                     return 1 # <---- 由原本的 0 改成 1
 127                 else:
 128                     return -1
 129         except:
 130             return -1

```