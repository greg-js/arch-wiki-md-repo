# ArchWiki Translation Team (简体中文)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Arch Wiki 上有许多中文页面，这其中大部分是从外文翻译过来的，这些页面是无数中文志愿者劳动的结晶。随着时间推移，有些页面因为没有及时维护，内容严重过时。而目前的翻译工作缺少组织，效率偏低。所以参照西班牙和意大利翻译组的做法，添加这个页面。

如果你希望对Arch Wiki做贡献，参与Wiki建设，比如翻译英文页面和对已翻译过的中文页面进行维护，只需要编辑下面的[#页面维护列表](#.E9.A1.B5.E9.9D.A2.E7.BB.B4.E6.8A.A4.E5.88.97.E8.A1.A8)，添加相应的条目，并将自己加为相关页面的维护者。同时也欢迎为wiki做出过贡献的人将自己添加到[#贡献列表](#.E8.B4.A1.E7.8C.AE.E5.88.97.E8.A1.A8)。如果你在列表中还没有找到想要翻译的页面，可以自行添加。另外，如果因为时间原因无法再维护页面，请及时将自己从维护者列表中删除。

## Contents

*   [1 创建翻译](#.E5.88.9B.E5.BB.BA.E7.BF.BB.E8.AF.91)
*   [2 完善翻译](#.E5.AE.8C.E5.96.84.E7.BF.BB.E8.AF.91)
*   [3 更新过期页面](#.E6.9B.B4.E6.96.B0.E8.BF.87.E6.9C.9F.E9.A1.B5.E9.9D.A2)
*   [4 贡献列表](#.E8.B4.A1.E7.8C.AE.E5.88.97.E8.A1.A8)
*   [5 翻译任务](#.E7.BF.BB.E8.AF.91.E4.BB.BB.E5.8A.A1)
    *   [5.1 模板 Article summary 变更为 Related](#.E6.A8.A1.E6.9D.BF_Article_summary_.E5.8F.98.E6.9B.B4.E4.B8.BA_Related)
*   [6 维护翻译](#.E7.BB.B4.E6.8A.A4.E7.BF.BB.E8.AF.91)
    *   [6.1 页面认领](#.E9.A1.B5.E9.9D.A2.E8.AE.A4.E9.A2.86)
    *   [6.2 翻译状态模板](#.E7.BF.BB.E8.AF.91.E7.8A.B6.E6.80.81.E6.A8.A1.E6.9D.BF)
    *   [6.3 页面维护列表](#.E9.A1.B5.E9.9D.A2.E7.BB.B4.E6.8A.A4.E5.88.97.E8.A1.A8)

## 创建翻译

**注意:** 如果不准备翻译页面的大部分内容，请尽量不要新建简体中文页面。检查英文页面的更新需要花费不少精力，没有翻译的页面会增加维护负担。

1.  如果还不知道如何编辑 wiki，请阅读 [编辑帮助](/index.php/Help:Editing_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Help:Editing (简体中文)")。
2.  阅读 [i18n帮助](/index.php/Help:I18n_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Help:I18n (简体中文)")，文章给出了 ArchWiki 国际化和本地化的指南。
3.  [登录](/index.php/Special:UserLogin "Special:UserLogin") 以进行编辑。
4.  选择要翻译的页面，例如从 [随机页面](/index.php/Special:Random "Special:Random") 或 [页面维护列表](#.E9.A1.B5.E9.9D.A2.E7.BB.B4.E6.8A.A4.E5.88.97.E8.A1.A8) 中选择一个未翻译完成的页面。假设要翻译 [Some Page](/index.php?title=Some_Page&action=edit&redlink=1 "Some Page (page does not exist)").
5.  进入选择的英文页面，点击页面顶部的 **编辑**。
6.  添加要翻译文件的语言间链接, 中文的话加入[[zh-CN:Some Page]]，其它语言参见[Help:i18n#Interlanguage links](/index.php/Help:I18n#Interlanguage_links "Help:I18n"))。
7.  复制所有页面代码。
8.  保存页面 (新加了语言链接)
9.  访问页面左边新添加的语言链接，应该会进到 [Some Page (简体中文)](/index.php?title=Some_Page_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)&action=edit&redlink=1 "Some Page (简体中文) (page does not exist)") : `https://wiki.archlinux.org/index.php/Some_Page_(_简体中文_)`
10.  因为页面不存在，点击 **创建**。
11.  将显示一个编辑器 - 粘贴复制的英文页面。
12.  将文章分类修改为本地化版本，例如将 `[[Category:Internationalization]]` 修改为 `[[Category:Internationalization (简体中文)]]`,参阅[Help:Category (简体中文)](/index.php/Help:Category_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Help:Category (简体中文)").
13.  修改语言间链接，指向英文页面(将 `zh-CN` 修改为 `en`，并将英文页面移到文章顶部。
14.  翻译页面，进行保存。
15.  (推荐)给翻译完成的页面加上[翻译状态](/index.php/Template:TranslationStatus_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Template:TranslationStatus (简体中文)"),后有详细介绍。
16.  更新所有其它语言页面，加入刚翻译文章的语言间链接。
17.  (可选)创建一个简体中文名称的页面，指向新创建的页面：访问 `https://wiki.archlinux.org/index.php/_页面的中文名称_`.
18.  (可选)建立新页面，并加入： `#REDIRECT [[Some Page (简体中文)]]` 

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

## 贡献列表

为翻译做出贡献的用户请加入列表，感谢所有人做出的贡献。如果因为时间原因无法再维护页面，请及时将自己从维护者列表中删除。

除[ArchWiki Administrators](/index.php/ArchWiki:Administrators "ArchWiki:Administrators")和[ArchWiki Maintainers](/index.php/ArchWiki:Maintainers "ArchWiki:Maintainers")外，其余贡献者按用户名字母顺序排列。

*   [Fengchao](/index.php/User:Fengchao "User:Fengchao") – [贡献](/index.php/Special:Contributions/Fengchao "Special:Contributions/Fengchao") – [Send Email](/index.php/Special:EmailUser/Fengchao "Special:EmailUser/Fengchao") – [ArchWiki Administrators](/index.php/ArchWiki:Administrators "ArchWiki:Administrators")
*   [Skydiver](/index.php/User:Skydiver "User:Skydiver") – [贡献](/index.php/Special:Contributions/Skydiver "Special:Contributions/Skydiver") – [Send Email](/index.php/Special:EmailUser/Skydiver "Special:EmailUser/Skydiver") – [ArchWiki Maintainers](/index.php/ArchWiki:Maintainers "ArchWiki:Maintainers")
*   [Aaron_chen](/index.php/User:Aaron_chen "User:Aaron chen") – [贡献](/index.php/Special:Contributions/Aaron_chen "Special:Contributions/Aaron chen") – [Send Email](/index.php/Special:EmailUser/Aaron_chen "Special:EmailUser/Aaron chen")
*   [Alswl](/index.php/User:Alswl "User:Alswl") – [贡献](/index.php/Special:Contributions/Alswl "Special:Contributions/Alswl") – [Send Email](/index.php/Special:EmailUser/Alswl "Special:EmailUser/Alswl")
*   [Acgtyrant](/index.php/User:Acgtyrant "User:Acgtyrant") – [贡献](/index.php/Special:Contributions/Acgtyrant "Special:Contributions/Acgtyrant") – [Send Email](/index.php/Special:EmailUser/Acgtyrant "Special:EmailUser/Acgtyrant")
*   [Cael](/index.php/User:Cael "User:Cael") – [贡献](/index.php/Special:Contributions/Cael "Special:Contributions/Cael") – [Send Email](/index.php/Special:EmailUser/Cael "Special:EmailUser/Cael")
*   [Cfunc](/index.php?title=User:Cfunc&action=edit&redlink=1 "User:Cfunc (page does not exist)") – [贡献](/index.php/Special:Contributions/Cfunc "Special:Contributions/Cfunc") – [Send Email](/index.php/Special:EmailUser/Cfunc "Special:EmailUser/Cfunc")
*   [cuihao](/index.php/User:Cuihao "User:Cuihao") – [贡献](/index.php/Special:Contributions/Cuihao "Special:Contributions/Cuihao") – [Send Email](/index.php/Special:EmailUser/Cuihao "Special:EmailUser/Cuihao")
*   [Carl X. Su](/index.php/User:Carl_tw "User:Carl tw") – [贡献](/index.php/Special:Contributions/Carl_tw "Special:Contributions/Carl tw") – [Send Email](/index.php/Special:EmailUser/Carl_tw "Special:EmailUser/Carl tw")
*   [Flockyrocky](/index.php/User:Flockyrocky "User:Flockyrocky") – [贡献](/index.php/Special:Contributions/Flockyrocky "Special:Contributions/Flockyrocky") – [Send Email](/index.php/Special:EmailUser/Flockyrocky "Special:EmailUser/Flockyrocky")
*   [Guangyu Zhang](/index.php/User:Zguangyu0000 "User:Zguangyu0000") – [贡献](/index.php/Special:Contributions/Zguangyu0000 "Special:Contributions/Zguangyu0000") – [Send Email](/index.php/Special:EmailUser/Zguangyu0000 "Special:EmailUser/Zguangyu0000")
*   [Hang yan](/index.php?title=User:Hang_yan&action=edit&redlink=1 "User:Hang yan (page does not exist)") – [贡献](/index.php/Special:Contributions/Hang_yan "Special:Contributions/Hang yan") – [Send Email](/index.php/Special:EmailUser/Hang_yan "Special:EmailUser/Hang yan")
*   [HelloCode](/index.php?title=User:HelloCode&action=edit&redlink=1 "User:HelloCode (page does not exist)") – [贡献](/index.php/Special:Contributions/HelloCode "Special:Contributions/HelloCode") – [Send Email](/index.php/Special:EmailUser/HelloCode "Special:EmailUser/HelloCode")
*   [jazzi](/index.php?title=User:Jazzi&action=edit&redlink=1 "User:Jazzi (page does not exist)") – [贡献](/index.php/Special:Contributions/jazzi "Special:Contributions/jazzi") – [Send Email](/index.php/Special:EmailUser/jazzi "Special:EmailUser/jazzi")
*   [Joshua](/index.php/User:Joshua83 "User:Joshua83") – [贡献](/index.php/Special:Contributions/Joshua83 "Special:Contributions/Joshua83") – [Send Email](/index.php/Special:EmailUser/Joshua83 "Special:EmailUser/Joshua83")
*   [Mac.Bloom](/index.php?title=User:Mac_uestc&action=edit&redlink=1 "User:Mac uestc (page does not exist)") – [贡献](/index.php/Special:Contributions/Mac_uestc "Special:Contributions/Mac uestc") – [Send Email](/index.php/Special:EmailUser/Mac_uestc "Special:EmailUser/Mac uestc")
*   [Mithrandir](/index.php/User:Mithrandir "User:Mithrandir") – [贡献](/index.php/Special:Contributions/Mithrandir "Special:Contributions/Mithrandir") – [Send Email](/index.php/Special:EmailUser/Mithrandir "Special:EmailUser/Mithrandir")
*   [Peter](/index.php/User:Peter "User:Peter") – [贡献](/index.php/Special:Contributions/Peter "Special:Contributions/Peter") – [Send Email](/index.php/Special:EmailUser/Peter "Special:EmailUser/Peter")
*   [Reverland](/index.php/User:Reverland "User:Reverland") – [贡献](/index.php/Special:Contributions/Reverland "Special:Contributions/Reverland") – [Send Email](/index.php/Special:EmailUser/Reverland "Special:EmailUser/Reverland")
*   [Shibao Zhao](/index.php?title=User:Shibao_Zhao&action=edit&redlink=1 "User:Shibao Zhao (page does not exist)") – [贡献](/index.php/Special:Contributions/Shibao_Zhao "Special:Contributions/Shibao Zhao") – [Send Email](/index.php/Special:EmailUser/Shibao_Zhao "Special:EmailUser/Shibao Zhao")
*   [Xuchunyang](/index.php?title=User:Xuchunyang&action=edit&redlink=1 "User:Xuchunyang (page does not exist)") – [贡献](/index.php/Special:Contributions/Acgtyrant "Special:Contributions/Acgtyrant") – [Send Email](/index.php/Special:EmailUser/Acgtyrant "Special:EmailUser/Acgtyrant")
*   [Stlt1sean](/index.php?title=User:Stlt1sean&action=edit&redlink=1 "User:Stlt1sean (page does not exist)") – [贡献](/index.php/Special:Contributions/Stlt1sean "Special:Contributions/Stlt1sean") – [Send Email](/index.php/Special:EmailUser/Stlt1sean "Special:EmailUser/Stlt1sean")
*   [_spaike97](/index.php/User:Spaike97 "User:Spaike97") – [贡献](/index.php/Special:Contributions/Spaike97 "Special:Contributions/Spaike97") – [Send Email](/index.php/Special:EmailUser/Spaike97 "Special:EmailUser/Spaike97")
*   [SteamedFish](/index.php/User:SteamedFish "User:SteamedFish") – [贡献](/index.php/Special:Contributions/SteamedFish "Special:Contributions/SteamedFish") – [Send Email](/index.php/Special:EmailUser/SteamedFish "Special:EmailUser/SteamedFish")
*   [Tuxzz](/index.php/User:Tuxzz "User:Tuxzz") – [贡献](/index.php/Special:Contributions/Tuxzz "Special:Contributions/Tuxzz") – [Send Email](/index.php/Special:EmailUser/Tuxzz "Special:EmailUser/Tuxzz")
*   [Vimtoy](/index.php/User:Vimtoy "User:Vimtoy") – [贡献](/index.php/Special:Contributions/Vimtoy "Special:Contributions/Vimtoy") – [Send Email](/index.php/Special:EmailUser/Vimtoy "Special:EmailUser/Vimtoy")
*   [Xinkai](/index.php?title=User:Xinkai&action=edit&redlink=1 "User:Xinkai (page does not exist)") – [贡献](/index.php/Special:Contributions/Xinkai "Special:Contributions/Xinkai") – [Send Email](/index.php/Special:EmailUser/Xinkai "Special:EmailUser/Xinkai")
*   [Yk](/index.php/User:Radflum "User:Radflum") – [贡献](/index.php/Special:Contributions/Radflum "Special:Contributions/Radflum") – [Send Email](/index.php/Special:EmailUser/Radflum "Special:EmailUser/Radflum")
*   [Zer4tul](/index.php/User:Zer4tul "User:Zer4tul") – [贡献](/index.php/Special:Contributions/Zer4tul "Special:Contributions/Zer4tul") – [Send Email](/index.php/Special:EmailUser/Zer4tul "Special:EmailUser/Zer4tul")

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

**小贴士:** 如果收到邮件通知后没有访问页面或者访问了页面却没有登录用户，下次页面改动时就不会再发邮件通知。可以点击监视列表中的**标记所有页面为已读**再次获取更新。

如果页面有维护者但长期得不到更新，将会在维护列表中删除维护者。

### 翻译状态模板

Arch 作为滚动发行版，软件变化比较快，对应的文档变化也比较快。许多翻译的文章由于缺乏更新，会产生命令运行出错或不起作用等问题。而由于这些过期页面没有及时标记出来，所以用户无法及时获得更新。[翻译状态模板](/index.php/Template:TranslationStatus_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Template:TranslationStatus (简体中文)")就是为了解决这个问题而创建。

此模板可以起到如下作用：

*   为用户提供翻译状况，包括翻译时间、英文页面的最后版本等
*   用户可以点击查看翻译后，英文页面的改动，这样英文不是很好的用户可以只查看很小一部分英文内容，并判断出是否影响操作。
*   翻译人员可以跟踪页面状况，通过[模板的反向链接](https://wiki.archlinux.org/index.php/Special:WhatLinksHere/Template:TranslationStatus_(简体中文))可以查找到所有标记页面，查看需要更新翻译的部分。

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

<table class="wikitable sortable collapsible" border="1">

<tbody>

<tr>

<th>页面</th>

<th>翻译状态</th>

<th>维护者</th>

<th class="unsortable" width="30%">备注</th>

</tr>

<tr>

<td>[AMD Catalyst (简体中文)](/index.php/AMD_Catalyst_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "AMD Catalyst (简体中文)")</td>

<td>过期</td>

<td>Shibao Zhao</td>

<td>无</td>

</tr>

<tr>

<td>[acpid (简体中文)](/index.php/Acpid_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Acpid (简体中文)")</td>

<td>过期</td>

<td>Cael</td>

</tr>

<tr>

<td>[Advanced Linux Sound Architecture (简体中文)](/index.php/Advanced_Linux_Sound_Architecture_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Advanced Linux Sound Architecture (简体中文)")</td>

<td>翻译中</td>

<td>ihonliu</td>

<td>无</td>

</tr>

<tr>

<td>[Arch Based Distributions (Active) (简体中文)](/index.php/Arch_Based_Distributions_(Active)_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch Based Distributions (Active) (简体中文)")</td>

<td>完成</td>

<td>Joshua</td>

<td>勘误中</td>

</tr>

<tr>

<td>[ATI (简体中文)](/index.php/ATI_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ATI (简体中文)")</td>

<td>完成</td>

<td>skysailing</td>

<td>无</td>

</tr>

<tr>

<td>[AUR Helpers (简体中文)](/index.php/AUR_Helpers_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "AUR Helpers (简体中文)")</td>

<td>进行中</td>

<td>Stonex</td>

<td>无</td>

</tr>

<tr>

<td>[awesome (简体中文)](/index.php/Awesome_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Awesome (简体中文)")</td>

<td>进行中</td>

<td>Cael</td>

<td>无</td>

</tr>

<tr>

<td>[BIND (简体中文)](/index.php/BIND_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "BIND (简体中文)")</td>

<td>翻译中</td>

<td>SteamedFish</td>

<td>无</td>

</tr>

<tr>

<td>[Bumblebee (简体中文)](/index.php/Bumblebee_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Bumblebee (简体中文)")</td>

<td>完成</td>

<td>Peter</td>

<td>无</td>

</tr>

<tr>

<td>[Chromium (简体中文)](/index.php/Chromium_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Chromium (简体中文)")</td>

<td>翻译中</td>

<td>Bobby</td>

<td>部分未翻译</td>

</tr>

<tr>

<td>[Cinnamon (简体中文)](/index.php/Cinnamon_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Cinnamon (简体中文)")</td>

<td>部分翻译</td>

<td>Bobby</td>

<td>部分未翻译</td>

</tr>

<tr>

<td>[Common Applications (简体中文)](/index.php/Common_Applications_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Common Applications (简体中文)")</td>

<td>部分翻译</td>

<td>DavidChen</td>

<td>翻译中</td>

</tr>

<tr>

<td>[Common Applications/Science (简体中文)](/index.php/Common_Applications/Science_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Common Applications/Science (简体中文)")</td>

<td>drop maintain</td>

<td>更新，翻译中</td>

</tr>

<tr>

<td>[Compiz (简体中文)](/index.php/Compiz_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Compiz (简体中文)")</td>

<td>翻译中</td>

<td>xiii_1991</td>

<td>20140813开始</td>

</tr>

<tr>

<td>[Core Utilities (简体中文)](/index.php/Core_Utilities_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Core Utilities (简体中文)")</td>

<td>翻译中</td>

<td>rentaro</td>

<td>同步翻译至2014年7月23日08:13英文页面，完善中</td>

</tr>

<tr>

<td>[Disk Cloning (简体中文)](/index.php/Disk_Cloning_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Disk Cloning (简体中文)")</td>

<td>翻译中</td>

<td>_spaike97</td>

<td>无</td>

</tr>

<tr>

<td>[Dynamic Kernel Module Support (简体中文)](/index.php/Dynamic_Kernel_Module_Support_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Dynamic Kernel Module Support (简体中文)")</td>

<td>完成</td>

<td>Mithrandir</td>

<td>完善中</td>

</tr>

<tr>

<td>[Emacs (简体中文)](/index.php/Emacs_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Emacs (简体中文)")</td>

<td>翻译中</td>

<td>Jaurung yuanhang</td>

<td>未完成</td>

</tr>

<tr>

<td>[File recovery (简体中文)](/index.php/File_recovery_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "File recovery (简体中文)")</td>

<td>翻译中</td>

<td>_spaike97</td>

<td>无</td>

</tr>

<tr>

<td>[Font Configuration (简体中文)](/index.php/Font_Configuration_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Font Configuration (简体中文)")</td>

<td>翻译中</td>

<td>Jaurung</td>

<td>完善中</td>

</tr>

<tr>

<td>[Fonts (简体中文)](/index.php/Fonts_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Fonts (简体中文)")</td>

<td>翻译中</td>

<td>qqbzg</td>

<td>无</td>

</tr>

<tr>

<td>[KDE (简体中文)](/index.php/KDE_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "KDE (简体中文)")</td>

<td>翻译中</td>

<td>Mithrandir</td>

<td>未完成</td>

</tr>

<tr>

<td>[LAMP (简体中文)](/index.php/LAMP_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "LAMP (简体中文)")</td>

<td>完成</td>

<td>Liuzhengyi</td>

<td>勘误中</td>

</tr>

<tr>

<td>[LibreOffice (简体中文)](/index.php/LibreOffice_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "LibreOffice (简体中文)")</td>

<td>完成</td>

<td>qqbzg</td>

<td>勘误中</td>

</tr>

<tr>

<td>[Local Mirror (简体中文)](/index.php/Local_Mirror_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Local Mirror (简体中文)")</td>

<td>完成</td>

<td>Jason Zhang</td>

<td>完善中</td>

</tr>

<tr>

<td>[NetworkManager (简体中文)](/index.php/NetworkManager_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "NetworkManager (简体中文)")</td>

<td>部分翻译</td>

<td>Jack-lijing</td>

<td>请优先翻译</td>

</tr>

<tr>

<td>[Network Time Protocol daemon (简体中文)](/index.php/Network_Time_Protocol_daemon_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Network Time Protocol daemon (简体中文)")</td>

<td>未翻译</td>

<td>无</td>

<td>部分未翻译</td>

</tr>

<tr>

<td>[OpenOffice (简体中文)](/index.php/OpenOffice_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "OpenOffice (简体中文)")</td>

<td>过期</td>

<td>无</td>

<td>无</td>

</tr>

<tr>

<td>[Opera (简体中文)](/index.php/Opera_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Opera (简体中文)")</td>

<td>未翻译</td>

<td>Bobby</td>

<td>请优先翻译此文</td>

</tr>

<tr>

<td>[Pacman GUI Frontends (简体中文)](/index.php/Pacman_GUI_Frontends_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman GUI Frontends (简体中文)")</td>

<td>翻译中</td>

<td>KaiYuan Guo</td>

<td>无</td>

</tr>

<tr>

<td>[Pidgin (简体中文)](/index.php/Pidgin_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pidgin (简体中文)")</td>

<td>进行中</td>

<td>Cael</td>

<td>无</td>

</tr>

<tr>

<td>[Plasma (简体中文)](/index.php/Plasma_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Plasma (简体中文)")</td>

<td>未翻译</td>

<td>无</td>

<td>无</td>

</tr>

<tr>

<td>[ranger (简体中文)](/index.php/Ranger_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Ranger (简体中文)")</td>

<td>完成</td>

<td>Jason Zhang</td>

<td>完善中</td>

</tr>

<tr>

<td>[Raspberry Pi (简体中文)](/index.php/Raspberry_Pi_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Raspberry Pi (简体中文)")</td>

<td>翻译中</td>

<td>Mithrandir</td>

</tr>

<tr>

<td>[Reporting_Bug_Guidelines_(简体中文)](/index.php/Reporting_Bug_Guidelines_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Reporting Bug Guidelines (简体中文)")</td>

<td>翻译中</td>

<td>Jason Zhang</td>

</tr>

<tr>

<td>[Secure Shell (简体中文)](/index.php/Secure_Shell_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Secure Shell (简体中文)")</td>

<td>完成</td>

<td>HelloCode</td>

<td>完成</td>

</tr>

<tr>

<td>[Smart Common Input Method platform (简体中文)](/index.php/Smart_Common_Input_Method_platform_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Smart Common Input Method platform (简体中文)")</td>

<td>过期</td>

<td>无</td>

<td>无</td>

</tr>

<tr>

<td>[Systemd-timesyncd (简体中文)‎‎](/index.php/Systemd-timesyncd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Systemd-timesyncd (简体中文)")</td>

<td>完成</td>

<td>Peter</td>

</tr>

<tr>

<td>[Vim (简体中文)](/index.php/Vim_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Vim (简体中文)")</td>

<td>翻译中</td>

<td>无</td>

<td>更新中</td>

</tr>

<tr>

<td>[VirtualBox (简体中文)](/index.php/VirtualBox_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "VirtualBox (简体中文)")</td>

<td>翻译中</td>

<td>Carl X. Su</td>

<td>请优先翻译此文</td>

</tr>

<tr>

<td>[VirtualBox Extras (简体中文)](/index.php/VirtualBox_Extras_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "VirtualBox Extras (简体中文)")</td>

<td>部分翻译</td>

<td>无</td>

<td>需要合并到 [VirtualBox (简体中文)](/index.php/VirtualBox_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "VirtualBox (简体中文)")</td>

</tr>

<tr>

<td>[VMware (简体中文)](/index.php/VMware_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "VMware (简体中文)")</td>

<td>翻译中</td>

<td>Jason Zhang</td>

<td>无</td>

</tr>

<tr>

<td>[Xfce (简体中文)](/index.php/Xfce_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Xfce (简体中文)")</td>

<td>翻译中</td>

<td>ZaticWu</td>

<td>请优先翻译</td>

</tr>

<tr>

<td>[Xmonad (简体中文)](/index.php/Xmonad_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Xmonad (简体中文)")</td>

<td>未翻译</td>

<td>Rns</td>

<td>翻译中</td>

</tr>

<tr>

<td>[Xrandr (简体中文)](/index.php/Xrandr_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Xrandr (简体中文)")</td>

<td>过期</td>

<td>无</td>

<td>无</td>

</tr>

</tbody>

</table>

Retrieved from "[https://wiki.archlinux.org/index.php?title=ArchWiki_Translation_Team_(简体中文)&oldid=411239](https://wiki.archlinux.org/index.php?title=ArchWiki_Translation_Team_(简体中文)&oldid=411239)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [简体中文](/index.php/Category:%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87 "Category:简体中文")
*   [ArchWiki (简体中文)](/index.php/Category:ArchWiki_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Category:ArchWiki (简体中文)")