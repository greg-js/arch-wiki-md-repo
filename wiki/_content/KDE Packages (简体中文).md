# KDE Packages (简体中文)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

相关文章

*   [KDE](/index.php/KDE "KDE")

**翻译状态：** 本文是英文页面 [KDE_Packages](/index.php/KDE_Packages "KDE Packages") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2013-03-28，点击[这里](https://wiki.archlinux.org/index.php?title=KDE_Packages&diff=0&oldid=246688)可以查看翻译后英文页面的改动。

我们从 KDE SC 4.3 开始为每个应用提供单独的软件包。本文描述组和 meta-packages 的概念。

## Contents

*   [1 名词解释](#.E5.90.8D.E8.AF.8D.E8.A7.A3.E9.87.8A)
*   [2 使用软件包组](#.E4.BD.BF.E7.94.A8.E8.BD.AF.E4.BB.B6.E5.8C.85.E7.BB.84)
    *   [2.1 为什么使用组?](#.E4.B8.BA.E4.BB.80.E4.B9.88.E4.BD.BF.E7.94.A8.E7.BB.84.3F)
        *   [2.1.1 优点](#.E4.BC.98.E7.82.B9)
        *   [2.1.2 缺点](#.E7.BC.BA.E7.82.B9)
    *   [2.2 谁使用组?](#.E8.B0.81.E4.BD.BF.E7.94.A8.E7.BB.84.3F)
*   [3 使用元软件包](#.E4.BD.BF.E7.94.A8.E5.85.83.E8.BD.AF.E4.BB.B6.E5.8C.85)
    *   [3.1 为什么使用元软件包？](#.E4.B8.BA.E4.BB.80.E4.B9.88.E4.BD.BF.E7.94.A8.E5.85.83.E8.BD.AF.E4.BB.B6.E5.8C.85.EF.BC.9F)
        *   [3.1.1 优点](#.E4.BC.98.E7.82.B9_2)
        *   [3.1.2 缺点](#.E7.BC.BA.E7.82.B9_2)
    *   [3.2 谁使用元软件包？](#.E8.B0.81.E4.BD.BF.E7.94.A8.E5.85.83.E8.BD.AF.E4.BB.B6.E5.8C.85.EF.BC.9F)
*   [4 显示软件包成员](#.E6.98.BE.E7.A4.BA.E8.BD.AF.E4.BB.B6.E5.8C.85.E6.88.90.E5.91.98)

## 名词解释

**module**（模块）：KDE的源代码划分为几个分类称为 _模块_，例如 kdebase、kdeutils 等等。KDE 项目为每个模块发布一个源码包。参见 [Coordinator List](http://techbase.kde.org/Projects/Release_Team#Coordinator_List)

**group**（组）：软件包组是一组软件包。按组安装/删除时， [Pacman](/index.php/Pacman "Pacman") 能够选择多个软件包。

**meta-package**（元软件包）：元软件包是空包，只用依赖来关联各软件包。

## 使用软件包组

每个 KDE 模块都位于某些组中，例如 **kdebase**, **kdeutils** 等等。 安装一个软件包组将会安装当时属于这个组的所有软件包。例如要安装当前发行的 **kdebase** 和 **kdeutils** 可以使用：

```
# pacman -S kdebase kdeutils ...

```

除此之外还有一个**kde**组，包含了所有这些组。安装 **kde** 组将会完整安装当前 KDE 软件集中的软件：

```
# pacman -S kde

```

### 为什么使用组?

#### 优点

*   更便捷地安装或删除一系列软件包。可以用单个命令安装或删除某个模块中的所有软件。
*   组与其中的软件包之间没有直接依赖关系。所以不需要安装组中的所有软件包，可以只删除组中的某几个软件，其它软件保持不变。

#### 缺点

*   [Pacman](/index.php/Pacman "Pacman") 在安装组之后不会自动安装新加入组的软件包。例如，如果下一个 KDE 软件集发布版本的一个或多个模块添加了新的软件，这些新软件不会在升级系统时被自动安装。需要手动安装这些软件。要克服这点，需要使用元软件包(参见下一章节)。

### 谁使用组?

如果只希望安装 KDE 软件集的一部分模块，应该使用组。如果希望保留组中的一部分软件而删除另外的软件，请使用组。

## 使用元软件包

和组一样，每个 KDE 模块都有对应的元软件包，例如 **kde-meta-kdebase**、**kde-meta-kdeutils** 等。安装元软件包将会安装和升级所有属于这个模块的软件。如果应用在未来版本被加入，将会在升级系统时自动安装。要使用元软件包安装指定模块，如**kdebase** 或者 **kdeutils** ，可以使用：

```
# pacman -S kde-meta-kdebase kde-meta-kdeutils ...

```

此外，还有一个 **kde-meta** 组，包含了所有这些元软件包。安装 **kde-meta** 组将安装整个 KDE 软件集:

```
# pacman -S kde-meta

```

### 为什么使用元软件包？

#### 优点

*   和组一样，元软件包可以简化软件集的安装和维护，用单个命令安装模块中的所有软件。
*   使用元软件包保证 [pacman](/index.php/Pacman "Pacman") 将会在升级系统时安装新加入的软件包，模拟了 KDE SC 4.3 之前的单一软件包功能。

#### 缺点

*   元软件包中的应用是它的一部分，它们有直接的依赖关系。也就是说，只有删除元软件包之后，才能自由删除其中的单个包。例如，安装了 **kde-meta-kdebase** 之后，如果要删除一个成员软件包，例如 **kdebase-kwrite**，需要先删除元软件包：

```
# pacman -R kde-meta-kdebase
# pacman -R kdebase-kwrite

```

这样做不会删除 **kde-meta-kdebase** 中的其它软件，但是同样不会在使用 pacman -Syu 升级系统的时候自动安装（下次发布时）新加入的包。可以随时重新安装 **kde-meta-kdebase** 元软件包，恢复到单一软件包时的方式。

如果安装了 kde-meta 软件包，可以一次删除所有元软件包：

```
# pacman -R kde-meta

```

仅会删除元软件包，不会删除实际的成员软件包。

### 谁使用元软件包？

如果想安装全部的 KDE 软件集，或者某个模块中的所有软件，可以考虑使用元软件包。这保证了平滑的升级过程，后续版本升级的时候，自动添加新的单个软件包。

## 显示软件包成员

要获得所有 KDE 应用的列表，请使用

```
pacman -Sg kde

```

列出所有元软件包：

```
pacman -Sg kde-meta

```

列出所有 KDE 模块组：

```
for i in $(pacman -Sqg kde-meta); do echo ${i#kde-meta-};done

```

列出所有 KDE 软件包和它们所属的模块组:

```
for i in $(pacman -Sqg kde-meta); do pacman -Sg ${i#kde-meta-};done

```

还可以访问 [archlinux.de](https://www.archlinux.de/?page=Packages;group=5) 浏览软件包组。

Retrieved from "[https://wiki.archlinux.org/index.php?title=KDE_Packages_(简体中文)&oldid=413922](https://wiki.archlinux.org/index.php?title=KDE_Packages_(简体中文)&oldid=413922)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Arch development (简体中文)](/index.php/Category:Arch_development_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Category:Arch development (简体中文)")
*   [Desktop environments (简体中文)](/index.php/Category:Desktop_environments_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Category:Desktop environments (简体中文)")