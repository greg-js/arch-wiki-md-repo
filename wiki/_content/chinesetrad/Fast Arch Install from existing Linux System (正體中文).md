如果你的電腦內已經安裝有一套 Linux 系統，或著你沒有 CD 燒錄機，或著你只是想要快速的安裝好 Arch，下面這一篇教學就是要告訴你，如何從硬碟上安裝 Arch 。

在開始前，你該先閱讀 [Arch Linux 安裝指南](https://www.archlinux.org/docs/en/guide/install/arch-install-guide.html) ，因為我們不會對一些安裝上的細節作太多解釋。

你需要**另**一個可用的硬碟分割區，空間需要比 Arch 的安裝光碟 ISO 檔還大。在下面的步驟內，我將以 **root** 的身分登入我的系統，並使用 "/dev/hda12" 作為我要使用的分割區 (我的分割區大小為 6GB)。

依照你所使用的 boot loader 程式，請直接跳到相關的段落 ("GRUB" 或是 "LiLo"。然後再跳到 "重新開機與安裝" 這個段落繼續系統的安裝。

## Contents

*   [1 Lilo](#Lilo)
*   [2 Grub](#Grub)
*   [3 重新開機和安裝 Arch](#.E9.87.8D.E6.96.B0.E9.96.8B.E6.A9.9F.E5.92.8C.E5.AE.89.E8.A3.9D_Arch)
*   [4 安裝完 Arch 並可正常使用後，回收之前空出的硬碟分割區...](#.E5.AE.89.E8.A3.9D.E5.AE.8C_Arch_.E4.B8.A6.E5.8F.AF.E6.AD.A3.E5.B8.B8.E4.BD.BF.E7.94.A8.E5.BE.8C.EF.BC.8C.E5.9B.9E.E6.94.B6.E4.B9.8B.E5.89.8D.E7.A9.BA.E5.87.BA.E7.9A.84.E7.A1.AC.E7.A2.9F.E5.88.86.E5.89.B2.E5.8D.80...)

## Lilo

1) 將開機光碟 ISO 內的檔案完全複製到剛剛空出來的硬碟分割區內 (你可以直接使用 cp -R 這個指令來迴遞複製，不需要使用到 dd 這個指令。因為使用 dd 有時可能會不小心把整個分割區都破壞了):

```
dd if=arch-0.7.iso of=/dev/hda12

```

2) 建立或是使用一個適當的掛載點，把剛剛的硬碟分割區掛載起來 (你可以使用mount 搭配 -t iso9660 這個選項，但是直接使用 mount 這個指令應該也沒問題):

```
mkdir /mnt/archCD
mount /dev/hda12 /mnt/archCD

```

3) 編輯 lilo.conf 並加入 :

```
image=/mnt/archCD/isolinux/vmlinuz
        label=archCD
        initrd=/mnt/archCD/isolinux/initrd.img
        append="root=/dev/rd/0 BOOTMEDIA=cd"
```

最後不要忘記執行 :

```
lilo

```

## Grub

我一直都沒辦法使用 grub 來直接開機啟動 Arch 的安裝光碟 ISO 檔。所以在使用安裝光碟內的檔案前，我們需要先把光碟內的檔案解壓後複製到一個硬碟分割區內。就算如此，使用這個方法來安裝 Arch 還是比燒製一片光碟來安裝還快 :

1) 格式化之前空出來的硬碟分割區然後把硬碟掛載起來 (建立或是使用一個適當的掛載點) :

```
mkreiserfs /dev/hda12
mkdir /mnt/archCD
mount /dev/hda12 /mnt/archCD

```

2) 掛載 Arch iso 檔 (建立或是使用一個適當的掛載點):

```
mkdir /mnt/tmp
mount -o loop arch-0.7.iso /mnt/tmp

```

3) 將 ISO 內的程式完全複製到空出來的硬碟分割區內 :

```
cd /mnt/tmp
cp -a * /mnt/archCD

```

4) 然後編輯 `/boot/grub/menu.lst`

```
title ArchCD
kernel (hd0,11)/isolinux/vmlinuz root=/dev/rd/0 BOOTMEDIA=cd
initrd (hd0,11)/isolinux/initrd.img

```

## 重新開機和安裝 Arch

重新開機然後選擇 **archCD** ，當 Arch 的安裝程式問你是使用 CD 或是 SRC 作為安裝來源時，你可以切換到另一個 shell 下，然後 :

```
mount -tiso9660 /dev/discs/disc0/part12 /src

```

*   請把 `/dev/discs/disc0/part12` 用你剛空出來的分割區的正確名稱取代
*   記得，你不需要自己輸入完整的名稱，你可以使用 "tab 自動補上名稱" 的功能來幫你找到你要的分割區名稱。
*   最後，請再切回執行安裝程式的 shell 下，選擇使用 SRC 作為安裝來源。

## 安裝完 Arch 並可正常使用後，回收之前空出的硬碟分割區...

1) 你可以使用 "mkreiserfs", "mke2fs" 或是其他程式來重新格式化之前用來安裝 Arch 時使用的硬碟分割區。在我們的例子中，我只需要執行 :

```
mkreiserfs /dev/hda12

```

2) 然後編輯 /etc/fstab 並檢查我們的分割區的檔案系統和選項的設定都正確無誤 :

```
/dev/hda12 /mnt/spare reiserfs defaults,noatime,notail,noauto 0 0

```

3) 最後，檢查看看掛載點是否存在，如果不存在，那就 :

```
mkdir /mnt/spare

```