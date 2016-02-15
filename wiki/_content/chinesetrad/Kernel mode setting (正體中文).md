## Contents

*   [1 簡介](#.E7.B0.A1.E4.BB.8B)
*   [2 背景](#.E8.83.8C.E6.99.AF)
*   [3 開啟 KMS 的方法](#.E9.96.8B.E5.95.9F_KMS_.E7.9A.84.E6.96.B9.E6.B3.95)
*   [4 更多相關資源](#.E6.9B.B4.E5.A4.9A.E7.9B.B8.E9.97.9C.E8.B3.87.E6.BA.90)

## 簡介

核心模式設定(KMS)是一種把顯示解析度和顯示色深從使用者空間(user space)提升到核心空間(kernel space)的方法。

KMS使用適合幀緩衝(framebuffer)的螢幕解析度，此外可以提快速得地不同的console(tty)之間切換。 同時KMS也支援了更多新的技術(例：DRI2)，其將能減少偽影(artifact)和增強3D表現，甚至核心空間(kernel space)省電。

可以預期以後主要的顯示晶片將支援或是預設啟用KMS。

## 背景

在有KMS之前，X windows下設定顯示卡這項工是X server在運作的。也因為這樣，想要流暢地在X windows和console之間切換(`Ctrl+Alt+F1~7`)幾乎是不可能的。主要困難的原因是切換過程中控制顯卡的工作從X server交付給核心，或是從核心交還給X server。而在這過程當中，螢幕常會有黑屏、閃爍等"痛苦"的表現。

在有了KMS後，核心已經先把顯示卡設定好了，這使得在開機程序執行中即可看到適合的顯示畫面，在X windows和console之間切換也顯的正常流暢。

KMS是一個新的技術，仍無法支援所有的顯卡，因此被認為還在實驗階段。它無法穩定支援所有新的軟體，也可能還存在著一些問題。

## 開啟 KMS 的方法

有非常多種開啟KMS的方法。但請寄的不管你用什麼樣的方法，請記得把開機載入程序(bootloader)中的"vga="、"video=" 這些選項刪除，因為這些會造成KMS啟動時程式衝突。其他幀緩衝(framebuffer)驅動(例：[uvesafb](/index.php/Uvesafb "Uvesafb"))也請在啟動KMS前關閉。

KMS現在並沒有支援全部的顯卡。請針對您的顯卡察看下列文章。

*   [ATI](/index.php/ATI "ATI")
*   [Intel](/index.php/Intel "Intel")
*   [NVIDIA](/index.php/NVIDIA "NVIDIA")

## 更多相關資源

[Mode-setting at Wikipedia](https://en.wikipedia.org/wiki/Mode-setting "wikipedia:Mode-setting")