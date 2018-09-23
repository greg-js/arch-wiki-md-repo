Arch Wiki 上有许多中文页面，这其中大部分是从外文翻译过来的，这些页面是无数中文志愿者劳动的结晶。随着时间推移，有些页面因为没有及时维护，内容严重过时。而目前的翻译工作缺少组织，效率偏低。所以参照西班牙和意大利翻译组的做法，添加这个页面。

如果你希望对Arch Wiki做贡献，参与Wiki建设，比如翻译英文页面和对已翻译过的中文页面进行维护，只需要编辑下面的[#页面维护列表](#.E9.A1.B5.E9.9D.A2.E7.BB.B4.E6.8A.A4.E5.88.97.E8.A1.A8)，添加相应的条目，并将自己加为相关页面的维护者。如果你在列表中还没有找到想要翻译的页面，可以自行添加。另外，如果因为时间原因无法再维护页面，请及时将自己从维护者列表中删除。

## Contents

*   [1 创建翻译](#.E5.88.9B.E5.BB.BA.E7.BF.BB.E8.AF.91)
*   [2 Templates](#Templates)
*   [3 完善翻译](#.E5.AE.8C.E5.96.84.E7.BF.BB.E8.AF.91)
*   [4 更新过期页面](#.E6.9B.B4.E6.96.B0.E8.BF.87.E6.9C.9F.E9.A1.B5.E9.9D.A2)
*   [5 翻译任务](#.E7.BF.BB.E8.AF.91.E4.BB.BB.E5.8A.A1)
    *   [5.1 模板 Article summary 变更为 Related](#.E6.A8.A1.E6.9D.BF_Article_summary_.E5.8F.98.E6.9B.B4.E4.B8.BA_Related)
*   [6 维护翻译](#.E7.BB.B4.E6.8A.A4.E7.BF.BB.E8.AF.91)
    *   [6.1 页面认领](#.E9.A1.B5.E9.9D.A2.E8.AE.A4.E9.A2.86)
    *   [6.2 翻译状态模板](#.E7.BF.BB.E8.AF.91.E7.8A.B6.E6.80.81.E6.A8.A1.E6.9D.BF)
    *   [6.3 页面维护列表](#.E9.A1.B5.E9.9D.A2.E7.BB.B4.E6.8A.A4.E5.88.97.E8.A1.A8)

## 创建翻译

**警告:** 如果不准备翻译页面的大部分内容，请尽量不要新建简体中文页面。检查英文页面的更新需要花费不少精力，没有翻译的页面会增加维护负担。

1.  如果还不知道如何编辑 wiki，请阅读 [编辑帮助](/index.php/Help:Editing_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Help:Editing (简体中文)")。
2.  阅读 [i18n帮助](/index.php/Help:I18n_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Help:I18n (简体中文)")，文章给出了 ArchWiki 国际化和本地化的指南。
3.  [登录](/index.php/Special:UserLogin "Special:UserLogin") 以进行编辑。
4.  选择要翻译的页面，例如从 [随机页面](/index.php/Special:Random "Special:Random") 或[页面维护列表](#.E9.A1.B5.E9.9D.A2.E7.BB.B4.E6.8A.A4.E5.88.97.E8.A1.A8) 中选择一个未翻译完成的页面。假设要翻译 [Some Page](/index.php?title=Some_Page&action=edit&redlink=1 "Some Page (page does not exist)").
5.  进入选择的英文页面，点击页面顶部的 **编辑**。
6.  添加要翻译文件的语言间链接, 简体中文的话加入[[zh-hans:Some Page]]，其它语言参见[Help:i18n#Interlanguage links](/index.php/Help:I18n#Interlanguage_links "Help:I18n"))。
7.  复制所有页面代码。
8.  保存页面 (新加了语言链接)
9.  访问页面左边新添加的语言链接，应该会进到 [Some Page (简体中文)](/index.php?title=Some_Page_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)&action=edit&redlink=1 "Some Page (简体中文) (page does not exist)") : `https://wiki.archlinux.org/index.php/Some_Page_(*简体中文*)`
10.  因为页面不存在，点击 **创建**。
11.  将显示一个编辑器 - 粘贴复制的英文页面。
12.  将文章分类修改为本地化版本，例如将 `[[Category:Internationalization]]` 修改为 `[[Category:Internationalization (简体中文)]]`,参阅[Help:Category (简体中文)](/index.php/Help:Category_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Help:Category (简体中文)").
13.  修改语言间链接，指向英文页面(将 `zh-hans` 修改为 `en`，并将英文页面移到文章顶部。
14.  翻译页面，进行保存。
15.  (推荐)给翻译完成的页面加上[翻译状态](/index.php/Template:TranslationStatus_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Template:TranslationStatus (简体中文)"),后有详细介绍。
16.  更新所有其它语言页面，加入刚翻译文章的语言间链接。
17.  (可选)创建一个简体中文名称的页面，指向新创建的页面：访问 `https://wiki.archlinux.org/index.php/*页面的中文名称*`.
18.  (可选)建立新页面，并加入： `#REDIRECT [[Some Page (简体中文)]]` 

## Templates

The following table lists the [templates](/index.php/Help:Template_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Help:Template (简体中文)") that should be translated and their Simplified Chinese equivalent.

| English template | Simplified Chinese version |
| Article templates |
| [Template:Related articles start](/index.php/Template:Related_articles_start "Template:Related articles start") | [Template:Related articles start (简体中文)](/index.php/Template:Related_articles_start_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Template:Related articles start (简体中文)") |
| [Template:Yes](/index.php/Template:Yes "Template:Yes") | [Template:是](/index.php/Template:%E6%98%AF "Template:是") |
| [Template:No](/index.php/Template:No "Template:No") | [Template:否](/index.php/Template:%E5%90%A6 "Template:否") |
| [Template:Tip](/index.php/Template:Tip "Template:Tip") | [Template:提示](/index.php/Template:%E6%8F%90%E7%A4%BA "Template:提示") |
| [Template:Note](/index.php/Template:Note "Template:Note") | [Template:注意](/index.php/Template:%E6%B3%A8%E6%84%8F "Template:注意") |
| [Template:Warning](/index.php/Template:Warning "Template:Warning") | [Template:警告](/index.php/Template:%E8%AD%A6%E5%91%8A "Template:警告") |
| [Template:Dead link](/index.php/Template:Dead_link "Template:Dead link") | [Template:失效链接](/index.php/Template:%E5%A4%B1%E6%95%88%E9%93%BE%E6%8E%A5 "Template:失效链接") |
| [Template:Broken package link](/index.php/Template:Broken_package_link "Template:Broken package link") | – |
| Translation status templates |
| [Template:Bad translation](/index.php/Template:Bad_translation "Template:Bad translation") | – |
| [Template:Translateme](/index.php/Template:Translateme "Template:Translateme") | [Template:Translateme (简体中文)](/index.php/Template:Translateme_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Template:Translateme (简体中文)") |
| [Template:TranslationStatus](/index.php/Template:TranslationStatus "Template:TranslationStatus") | [Template:TranslationStatus (简体中文)](/index.php/Template:TranslationStatus_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Template:TranslationStatus (简体中文)") |
| Special templates |
| [Template:Cat main](/index.php/Template:Cat_main "Template:Cat main") | – |
| [Template:Template](/index.php/Template:Template "Template:Template") | – |

## 完善翻译

[这个页面](https://wiki.archlinux.org/index.php?title=Special:WhatLinksHere/Template:Translateme_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)&limit=100) 包含了需要完善翻译的简体中文页面。完善翻译的基本步骤：

1.  选择自己比较熟悉的文章进行翻译
2.  先检查英文页面的对应段落，更新成最新的英文后再翻译，避免翻译过时的内容，减少信息遗漏。
3.  翻译完成后删除页面中的 {{translateme (简体中文)}} 标记
4.  (推荐)给翻译完成的页面加上[翻译状态](/index.php/Template:TranslationStatus_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Template:TranslationStatus (简体中文)"),后有详细介绍。

## 更新过期页面

如果发现有 Wiki 页面过期或错误：

*   小的改动，有时间可以立即进行修改同步，维护者并不控制页面的编辑权限，越多的人参与维护越好。如果改动较大，请先联系维护者，避免重复劳动。
*   没有时间查看更改，请给页面加上 `{{out of date}}` 模版，这样其他贡献者更容易发现需要更新的页面，而读者看到过期标记就可以直接查看英文页面，以免被错误内容误导，白白耽误时间。
*   没有时间翻译，请将过期的中文部分删去，从英文页面中复制更改的部分到中文页面的相应部分，去掉`{{out of date}}`模板(如果页面上有的话)并加上`{{translateme (简体中文)}}`模板，这样其他贡献者就更容易发现需要翻译的页面，而读者也不会被过期的内容误导。

如果发现有页面未翻译：

*   有时间的话，请将页面中的英文部分翻译为中文，并去掉`{{translateme (简体中文)}}`模板。
*   没有时间翻译，请为页面添加`{{translateme (简体中文)}}`模板，这样其他的贡献者就能更容易发现需要翻译的页面。

**注意:** 在修改页面上的模板时，请同时更新页面维护列表的翻译状态。

## 翻译任务

### 模板 Article summary 变更为 Related

因为 Summary 中的简介基本上和正文的介绍一样，所以页面左边的介绍栏进行了简化，只保留相关文章功能。英文页面正在进行大规模修改，相应的中文页面也需要同步更新。

需要注意的地方：

*   将第一行改成

	{{Related articles start (简体中文)}}

*   如果英文的相关文章存在中文翻译，则替换为简体中文页面。示例：

	{{Related2|Display Manager (简体中文)|显示管理器}}

*   示例：[英文变更](https://wiki.archlinux.org/index.php?title=Start_X_at_Login&diff=0&oldid=270155), [对应的翻译](https://wiki.archlinux.org/index.php?title=Start_X_at_Login_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)&diff=285643&oldid=242662)

## 维护翻译

完成页面的翻译只是初步完成任务，及时同步英文页面改动、更新翻译是一个持续性的工作，可能会耗费更多的时间。

### 页面认领

所有人都可以认领页面。认领后的责任包括进行翻译，关注英文页面的改动，及时同步翻译。

为了更好的跟踪英文页面的修改，请务必在设置中启用监视列表邮件通知，并监视对应的英文页面(从设置中找到监视列表，加入英文页面。或者直接到英文页面点击页面顶端的监视标签。这样只要有改动，就会收到邮件通知)。

**提示：** 如果收到邮件通知后没有访问页面或者访问了页面却没有登录用户，下次页面改动时就不会再发邮件通知。可以点击监视列表中的**标记所有页面为已读**再次获取更新。

如果页面有维护者但长期得不到更新，将会在维护列表中删除维护者。

### 翻译状态模板

Arch 作为滚动发行版，软件变化比较快，对应的文档变化也比较快。许多翻译的文章由于缺乏更新，会产生命令运行出错或不起作用等问题。而由于这些过期页面没有及时标记出来，所以用户无法及时获得更新。[翻译状态模板](/index.php/Template:TranslationStatus_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Template:TranslationStatus (简体中文)")就是为了解决这个问题而创建。

此模板可以起到如下作用：

*   为用户提供翻译状况，包括翻译时间、英文页面的最后版本等
*   用户可以点击查看翻译后，英文页面的改动，这样英文不是很好的用户可以只查看很小一部分英文内容，并判断出是否影响操作。
*   翻译人员可以跟踪页面状况，通过[模板的反向链接](/index.php/Special:WhatLinksHere/Template:TranslationStatus_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Special:WhatLinksHere/Template:TranslationStatus (简体中文)")可以查找到所有标记页面，查看需要更新翻译的部分。

[模板页面](/index.php/Template:TranslationStatus_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Template:TranslationStatus (简体中文)")有详细的使用方法。

### 页面维护列表

**注意:** 请按照拉丁字母顺序添加页面。

翻译状态说明：

	过期

	页面内容未与英文页面同步，对应`{{out of date}}` 模版

	未翻译

	页面中含有英文内容，对应`{{translateme (简体中文)}}`模板

	完成

	页面已与英文页面同步

| 页面 | 翻译状态 | 维护者 | 备注 |
| [AMD Catalyst (简体中文)](/index.php/AMD_Catalyst_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "AMD Catalyst (简体中文)") | 过期 | Shibao Zhao | 无 |
| [acpid (简体中文)](/index.php/Acpid_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Acpid (简体中文)") | 过期 | Cael |
| [Advanced Linux Sound Architecture (简体中文)](/index.php/Advanced_Linux_Sound_Architecture_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Advanced Linux Sound Architecture (简体中文)") | 翻译中 | ihonliu | 无 |
| [Arch based distributions (active) (简体中文)](/index.php/Arch_based_distributions_(active)_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch based distributions (active) (简体中文)") | 完成 | Joshua | 勘误中 |
| [ATI (简体中文)](/index.php/ATI_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ATI (简体中文)") | 完成 | skysailing | 无 |
| [AUR helpers (简体中文)](/index.php/AUR_helpers_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "AUR helpers (简体中文)") | 完成 | Kurobac | 部分用词可能需要修改 |
| [awesome (简体中文)](/index.php/Awesome_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Awesome (简体中文)") | 进行中 | Cael | 无 |
| [BIND (简体中文)](/index.php/BIND_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "BIND (简体中文)") | 完成 | Dargasia |
| [Bumblebee (简体中文)](/index.php/Bumblebee_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Bumblebee (简体中文)") | 完成 | Peter | 无 |
| [Chromium (简体中文)](/index.php/Chromium_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Chromium (简体中文)") | 完成 | Bobby | 无 |
| [Ceph (简体中文)](/index.php/Ceph_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Ceph (简体中文)") | 翻译中 | Aaron Chen | 部分未翻译 |
| [Cinnamon (简体中文)](/index.php/Cinnamon_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Cinnamon (简体中文)") | 部分翻译 | Bobby | 部分未翻译 |
| [Common Applications (简体中文)](/index.php/Common_Applications_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Common Applications (简体中文)") | 部分翻译 | DavidChen | 翻译中 |
| [Common Applications/Science (简体中文)](/index.php/Common_Applications/Science_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Common Applications/Science (简体中文)") | drop maintain | 更新，翻译中 |
| [Compiz (简体中文)](/index.php/Compiz_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Compiz (简体中文)") | 翻译中 | xiii_1991 | 20140813开始 |
| [Core utilities (简体中文)](/index.php/Core_utilities_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Core utilities (简体中文)") | 完成 | rentaro, Arisaka | 无 |
| [Clover (简体中文)](/index.php/Clover_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Clover (简体中文)") | 完成 | Yume Kankawa | 无 |
| [Disk cloning (简体中文)](/index.php/Disk_cloning_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Disk cloning (简体中文)") | 翻译中 | _spaike97 | 无 |
| [Dynamic Kernel Module Support (简体中文)](/index.php/Dynamic_Kernel_Module_Support_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Dynamic Kernel Module Support (简体中文)") | 完成 | Mithrandir | 完善中 |
| [Emacs (简体中文)](/index.php/Emacs_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Emacs (简体中文)") | 翻译中 | Jaurung yuanhang | 未完成 |
| [File recovery (简体中文)](/index.php/File_recovery_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "File recovery (简体中文)") | 翻译中 | _spaike97 | 无 |
| [Font configuration (简体中文)](/index.php/Font_configuration_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Font configuration (简体中文)") | 翻译中 | Jaurung | 完善中 |
| [Fonts (简体中文)](/index.php/Fonts_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Fonts (简体中文)") | 翻译中 | qqbzg | 无 |
| [GDM (简体中文)](/index.php/GDM_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GDM (简体中文)") | 翻译中 | Junjie Yuan | 绝大多数内容未翻译，重新进行翻译 |
| [GNOME (简体中文)](/index.php/GNOME_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GNOME (简体中文)") | 完成 | skywet |
| [KDE (简体中文)](/index.php/KDE_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "KDE (简体中文)") | 过期 |
| [LAMP (简体中文)](/index.php/LAMP_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "LAMP (简体中文)") | 完成 | Liuzhengyi | 勘误中 |
| [LibreOffice (简体中文)](/index.php/LibreOffice_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "LibreOffice (简体中文)") | 完成 | qqbzg | 勘误中 |
| [Libvirt (简体中文)](/index.php/Libvirt_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Libvirt (简体中文)") | 完成 | Kurobac | 需要格式改进 |
| [Local Mirror (简体中文)](/index.php/Local_Mirror_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Local Mirror (简体中文)") | 完成 | Jason Zhang | 完善中 |
| [Matlab (简体中文)](/index.php/Matlab_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Matlab (简体中文)") | 部分翻译 | Liu Qinyang |
| [Minecraft (简体中文)](/index.php/Minecraft_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Minecraft (简体中文)") | 完成 | Xavier Lau | 页面已经与英文版同步，长期维护中 |
| [NetworkManager (简体中文)](/index.php/NetworkManager_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "NetworkManager (简体中文)") | 翻译中 | Jack-lijing, leeking | 请优先翻译 |
| [Network Time Protocol daemon (简体中文)](/index.php/Network_Time_Protocol_daemon_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Network Time Protocol daemon (简体中文)") | 完成 | sid | 完善中 |
| [OpenOffice (简体中文)](/index.php/OpenOffice_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "OpenOffice (简体中文)") | 过期 | 无 | 无 |
| [Opera (简体中文)](/index.php/Opera_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Opera (简体中文)") | 未翻译 | Bobby | 请优先翻译此文 |
| [Pacman GUI Frontends (简体中文)](/index.php/Pacman_GUI_Frontends_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman GUI Frontends (简体中文)") | 过期 | 无 | 无 |
| [Pidgin (简体中文)](/index.php/Pidgin_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pidgin (简体中文)") | 进行中 | Cael | 无 |
| [ranger (简体中文)](/index.php/Ranger_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Ranger (简体中文)") | 完成 | Jason Zhang | 完善中 |
| [Raspberry Pi (简体中文)](/index.php/Raspberry_Pi_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Raspberry Pi (简体中文)") | 翻译中 | Mithrandir |
| [Reporting bug guidelines (简体中文)](/index.php/Reporting_bug_guidelines_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Reporting bug guidelines (简体中文)") | 完成 | 无 | 无 |
| [Secure Shell (简体中文)](/index.php/Secure_Shell_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Secure Shell (简体中文)") | 完成 | Arisaka | 无 |
| [Smart Common Input Method platform (简体中文)](/index.php/Smart_Common_Input_Method_platform_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Smart Common Input Method platform (简体中文)") | 过期 | 无 | 无 |
| [Systemd-timesyncd (简体中文)](/index.php/Systemd-timesyncd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Systemd-timesyncd (简体中文)") | 完成 | 无 | 无 |
| [TLP (简体中文)](/index.php/TLP_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "TLP (简体中文)") | 完成 | Skywet | 持续更新中 |
| [Tomcat (简体中文)](/index.php/Tomcat_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Tomcat (简体中文)") | 完成 | Starwing117 | 持续更新中 |
| [Vim (简体中文)](/index.php/Vim_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Vim (简体中文)") | 完成 | 无 | 无 |
| [VirtualBox (简体中文)](/index.php/VirtualBox_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "VirtualBox (简体中文)") | 翻译至 2017-10-15 | [User:5long](/index.php?title=User:5long&action=edit&redlink=1 "User:5long (page does not exist)") |
| [VMware (简体中文)](/index.php/VMware_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "VMware (简体中文)") | 完成 | ThomasWFan | 页面已经与英文版同步，长期维护中 |
| [Xfce (简体中文)](/index.php/Xfce_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Xfce (简体中文)") | 完成 | 无 | 无 |
| [Xmonad (简体中文)](/index.php/Xmonad_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Xmonad (简体中文)") | 过期 | 无 | 无 |
| [Xrandr (简体中文)](/index.php/Xrandr_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Xrandr (简体中文)") | 过期 | 无 | 无 |
| [Python打包指引 (简体中文)](/index.php/Python%E6%89%93%E5%8C%85%E6%8C%87%E5%BC%95_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Python打包指引 (简体中文)") | 翻译中 | SherlockHolo | 无 |