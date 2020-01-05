Related articles

*   [Java package guidelines (简体中文)](/index.php/Java_package_guidelines_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Java package guidelines (简体中文)")
*   [Java Runtime Environment Fonts](/index.php/Java_Runtime_Environment_Fonts "Java Runtime Environment Fonts")

这是来自 [维基百科的文章](https://en.wikipedia.org/wiki/Java_(programming_language) "wikipedia:Java (programming language)"):

	Java是由Sun微系统公司原创开发的编程语言并且在1995年发布，用作Sun微系统公司的Java平台的核心组件。它从C和C++派生了许多语法，但有一个简洁的对象模型和更少的底层组件。Java的应用一般被编译成能在([JVM](https://en.wikipedia.org/wiki/Java_virtual_machine "wikipedia:Java virtual machine"))运行的字节码，并能无视计算机结构。

Arch Linux官方支持开源的 [OpenJDK](https://openjdk.java.net/) 版本7、8、10和11.所有的JVM都能无冲突的被安装，并切换到帮助脚本`archlinux-java`. 一些其他的Java环境也是可使用的，在 [Arch User Repository (简体中文)](/index.php/Arch_User_Repository_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch User Repository (简体中文)")中，但官方并不支持。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 安装](#安装)
    *   [1.1 OpenJDK](#OpenJDK)
    *   [1.2 其他实现](#其他实现)
    *   [1.3 开发工具](#开发工具)
        *   [1.3.1 反编译器](#反编译器)
*   [2 在JVM间切换](#在JVM间切换)
    *   [2.1 列出兼容的安装了的Java环境](#列出兼容的安装了的Java环境)
    *   [2.2 改变默认Java环境](#改变默认Java环境)
    *   [2.3 取消设置的默认Java环境](#取消设置的默认Java环境)
    *   [2.4 解决默认Java环境的问题](#解决默认Java环境的问题)
    *   [2.5 运行非默认Java版本的程序](#运行非默认Java版本的程序)
*   [3 包支持archlinux-java的先决条件](#包支持archlinux-java的先决条件)
*   [4 故障排除](#故障排除)
    *   [4.1 MySQL](#MySQL)
    *   [4.2 IntelliJ IDEA](#IntelliJ_IDEA)
    *   [4.3 冒充另一个窗口管理器](#冒充另一个窗口管理器)
    *   [4.4 难以辨认的字体](#难以辨认的字体)
    *   [4.5 一些应用缺少文字](#一些应用缺少文字)
    *   [4.6 应用未调整WM大小，菜单快速关闭](#应用未调整WM大小，菜单快速关闭)
    *   [4.7 当调试JavaFX程序的时候系统卡住](#当调试JavaFX程序的时候系统卡住)
    *   [4.8 JavaFX 的 MediaPlayer 构造函数抛出了一个 exception](#JavaFX_的_MediaPlayer_构造函数抛出了一个_exception)
    *   [4.9 Java程序无法打开外部链接](#Java程序无法打开外部链接)
*   [5 建议和技巧](#建议和技巧)
    *   [5.1 更好的字体渲染](#更好的字体渲染)
    *   [5.2 禁止命令行的 'Picked up _JAVA_OPTIONS' 消息](#禁止命令行的_'Picked_up_JAVA_OPTIONS'_消息)
    *   [5.3 GTK 视觉效果和感觉](#GTK_视觉效果和感觉)
        *   [5.3.1 GTK3支持](#GTK3支持)
    *   [5.4 更好的2D性能](#更好的2D性能)
    *   [5.5 非重新父母窗口管理器 / 灰色窗口 / 程序被绘制得不恰当](#非重新父母窗口管理器_/_灰色窗口_/_程序被绘制得不恰当)
*   [6 参阅](#参阅)

## 安装

**注意:**

*   arch Linux官方只支持 [OpenJDK](#OpenJDK) 实现.
*   安装之后，Java环境需要被shell(`$PATH` 变量)识别. 可以通过命令行用source处理 `/etc/profile` 或者重新登出登入桌面环境.

两个 *公共* 包应该被当做依赖分别安装，他们是 [java-runtime-common](https://www.archlinux.org/packages/?name=java-runtime-common) (包含Java运行环境（JRE）的公共文件) 和 [java-environment-common](https://www.archlinux.org/packages/?name=java-environment-common) (包括Java开发包（JDK）的公共文件). 提供的环境文件 `/etc/profile.d/jre.sh` 指向了一个链接路径 `/usr/lib/jvm/default/bin`, 它被 `archlinux-java` 帮助脚本设置. 这个链接 `/usr/lib/jvm/default` 和 `/usr/lib/jvm/default-runtime` 应该 **总是** 被 `archlinux-java`编辑. 这用来显示和指向默认运行的Java环境，在`/usr/lib/jvm/java-${JAVA_MAJOR_VERSION}-${VENDOR_NAME}` ，或Java运行，在 `/usr/lib/jvm/java-${JAVA_MAJOR_VERSION}-${VENDOR_NAME}/jre`.

大多数可执行的Java安装都在直接路径`/usr/bin`里,而其他的在 `$PATH`.

**警告:** 文件 `/etc/profile.d/jdk.sh` 再也不被任何包提供了.

### OpenJDK

[OpenJDK](https://en.wikipedia.org/wiki/OpenJDK "wikipedia:OpenJDK") 是一种Java平台、标准版（Java SE）的开源实现(Java SE).

	Headless JRE

	最小的Java运行环境 - 需要被用来执行非GUI的Java程序.

	Full JRE

	完全的Java运行环境 - 需要用来运行JavaGUI程序，依赖于headless JRE.

	JDK

	[Java Development Kit](https://en.wikipedia.org/wiki/Java_Development_Kit "wikipedia:Java Development Kit") - 需要用来搭建Java开发环境, 依赖于 full JRE.

| 版本 | Headless JRE | Full JRE | JDK | 文献 | 来源 |
| [OpenJDK 11](https://openjdk.java.net/projects/jdk/11/) | [jre-openjdk-headless](https://www.archlinux.org/packages/?name=jre-openjdk-headless) | [jre-openjdk](https://www.archlinux.org/packages/?name=jre-openjdk) | [jdk-openjdk](https://www.archlinux.org/packages/?name=jdk-openjdk) | [openjdk-doc](https://www.archlinux.org/packages/?name=openjdk-doc) | [openjdk-src](https://www.archlinux.org/packages/?name=openjdk-src) |
| [OpenJDK 10](https://openjdk.java.net/projects/jdk/10/) | [jre10-openjdk-headless](https://www.archlinux.org/packages/?name=jre10-openjdk-headless) | [jre10-openjdk](https://www.archlinux.org/packages/?name=jre10-openjdk) | [jdk10-openjdk](https://www.archlinux.org/packages/?name=jdk10-openjdk) | [openjdk10-doc](https://www.archlinux.org/packages/?name=openjdk10-doc) | [openjdk10-src](https://www.archlinux.org/packages/?name=openjdk10-src) |
| [OpenJDK 8](https://openjdk.java.net/projects/jdk8/) | [jre8-openjdk-headless](https://www.archlinux.org/packages/?name=jre8-openjdk-headless) | [jre8-openjdk](https://www.archlinux.org/packages/?name=jre8-openjdk) | [jdk8-openjdk](https://www.archlinux.org/packages/?name=jdk8-openjdk) | [openjdk8-doc](https://www.archlinux.org/packages/?name=openjdk8-doc) | [openjdk8-src](https://www.archlinux.org/packages/?name=openjdk8-src) |
| [OpenJDK 7](https://openjdk.java.net/projects/jdk7/) | [jre7-openjdk-headless](https://www.archlinux.org/packages/?name=jre7-openjdk-headless) | [jre7-openjdk](https://www.archlinux.org/packages/?name=jre7-openjdk) | [jdk7-openjdk](https://www.archlinux.org/packages/?name=jdk7-openjdk) | [openjdk7-doc](https://www.archlinux.org/packages/?name=openjdk7-doc) | [openjdk7-src](https://www.archlinux.org/packages/?name=openjdk7-src) |

**IcedTea-Web** — Java web第一步 但是是一个被弃用的Java浏览器插件.

	[https://icedtea.classpath.org/wiki/IcedTea-Web](https://icedtea.classpath.org/wiki/IcedTea-Web) || [icedtea-web](https://www.archlinux.org/packages/?name=icedtea-web)

**OpenJFX 8** — JavaFX的开源实现. 你[不需要](https://wiki.openjdk.java.net/display/OpenJFX/Repositories+and+Releases) 安装这个包，如果你使用Java SE的话 (下面要讲的Oracle的JRE和JDK实现). 这个包仅仅是因为担心Java开源实现的用户 (OpenJDK 项目).

	[https://openjdk.java.net/projects/openjfx/](https://openjdk.java.net/projects/openjfx/) || [java-openjfx](https://www.archlinux.org/packages/?name=java-openjfx), [java-openjfx-doc](https://www.archlinux.org/packages/?name=java-openjfx-doc), [java-openjfx-src](https://www.archlinux.org/packages/?name=java-openjfx-src)

**OpenJDK EA** — Oracle的OpenJDK为最新开发版本的早期接入.

	[https://jdk.java.net](https://jdk.java.net) || [openjdk-devel](https://aur.archlinux.org/packages/openjdk-devel/)

**OpenJFX EA** — Oracle的OpenJFK为最新开发版本的早期接入.

	[https://jdk.java.net/openjfx/](https://jdk.java.net/openjfx/) || [java-openjfx-devel](https://aur.archlinux.org/packages/java-openjfx-devel/)

### 其他实现

**Java SE** — Oracle的JRE和JDK实现.

	[https://www.oracle.com/technetwork/java/javase/downloads/index.html](https://www.oracle.com/technetwork/java/javase/downloads/index.html) || [jre](https://aur.archlinux.org/packages/jre/) [jre9](https://aur.archlinux.org/packages/jre9/) [jre8](https://aur.archlinux.org/packages/jre8/) [jre7](https://aur.archlinux.org/packages/jre7/) [jre6](https://aur.archlinux.org/packages/jre6/) [jdk](https://aur.archlinux.org/packages/jdk/) [jdk9](https://aur.archlinux.org/packages/jdk9/) [jdk8](https://aur.archlinux.org/packages/jdk8/) [jdk7](https://aur.archlinux.org/packages/jdk7/) [jdk6](https://aur.archlinux.org/packages/jdk6/) [jdk5](https://aur.archlinux.org/packages/jdk5/) [jdk-devel](https://aur.archlinux.org/packages/jdk-devel/)

**OpenJ9** — Eclipse的JRE实现，由IBM贡献

	[https://www.eclipse.org/openj9/](https://www.eclipse.org/openj9/) || [jdk9-openj9-bin](https://aur.archlinux.org/packages/jdk9-openj9-bin/) [jdk8-openj9-bin](https://aur.archlinux.org/packages/jdk8-openj9-bin/)

**IBM J9** — IBM的第八版Java实现.

	[https://developer.ibm.com/javasdk/](https://developer.ibm.com/javasdk/) || [jdk8-j9-bin](https://aur.archlinux.org/packages/jdk8-j9-bin/) [jdk7-j9-bin](https://aur.archlinux.org/packages/jdk7-j9-bin/) [jdk7r1-j9-bin](https://aur.archlinux.org/packages/jdk7r1-j9-bin/)

**Parrot VM** — 一个对Java [[1]](http://trac.parrot.org/parrot/wiki/Languages)提供实验支持的虚拟机 ，通过两种方式，一种是 [Java VM bytecode translator](https://code.google.com/p/parrot-jvm/)，另一种是[Java compiler targeting the Parrot VM](https://github.com/chrisdolan/perk).

	[http://www.parrot.org/](http://www.parrot.org/) || [parrot](https://aur.archlinux.org/packages/parrot/)

**注意:** 32比特版本的JavaSE可以通过添加前缀 `bin32-`来找到，例如 [bin32-jre](https://aur.archlinux.org/packages/bin32-jre/) 和 [bin32-jdk](https://aur.archlinux.org/packages/bin32-jdk/). 他们使用的是 [java32-runtime-common](https://aur.archlinux.org/packages/java32-runtime-common/),而这和 [java-runtime-common](https://www.archlinux.org/packages/?name=java-runtime-common)功能一样只要添加后缀就好了`32`, 例如. `java32`. 同样的方法也适用于 [java32-environment-common](https://aur.archlinux.org/packages/java32-environment-common/),它只用于32比特版本的JDK包.

### 开发工具

对于集成开发环境，查阅[List of applications#Integrated development environments](/index.php/List_of_applications#Integrated_development_environments "List of applications") 和特定的 *Java IDEs* 的子分区

为了阻止逆向工程，可以使用像[proguard](https://aur.archlinux.org/packages/proguard/)的混淆器.

#### 反编译器

*   **Bytecode Viewer** — Java逆向工程套件, 包括一个反编译器, 编辑器和调试器.

	[https://bytecodeviewer.com](https://bytecodeviewer.com) || [bytecode-viewer](https://aur.archlinux.org/packages/bytecode-viewer/)

*   **CFR** — Java反编译器，支持Java 9,10和更高版本的现代功能

	[https://www.benf.org/other/cfr/](https://www.benf.org/other/cfr/) || [cfr](https://aur.archlinux.org/packages/cfr/)

*   **Fernflower** — Java的分析反编译器, 被开发为[IntelliJ IDEA](/index.php/IntelliJ_IDEA "IntelliJ IDEA")的一部分.

	[https://github.com/JetBrains/intellij-community/tree/master/plugins/java-decompiler/engine](https://github.com/JetBrains/intellij-community/tree/master/plugins/java-decompiler/engine) || [fernflower-git](https://aur.archlinux.org/packages/fernflower-git/)

*   **[JAD](https://en.wikipedia.org/wiki/JAD_(software) "wikipedia:JAD (software)")** — 不被维护的Java反编译器.

	[https://varaneckas.com/jad](https://varaneckas.com/jad) || [jad](https://www.archlinux.org/packages/?name=jad)

*   **JD-Core-java** — [Java反编译器]的薄包装](https://en.wikipedia.org/wiki/Java_Decompiler "wikipedia:Java Decompiler").

	[https://github.com/nviennot/jd-core-java](https://github.com/nviennot/jd-core-java) || [jd-core-java](https://aur.archlinux.org/packages/jd-core-java/)

*   **Krakatau** — Java的反编译器，汇编器和反汇编器.

	[https://github.com/Storyyeller/Krakatau](https://github.com/Storyyeller/Krakatau) || [krakatau-git](https://aur.archlinux.org/packages/krakatau-git/)

*   **Procyon decompiler** — 实验性质的Java反编译器, 被ILSpy and Mono.Cecil启发.

	[https://bitbucket.org/mstrobel/procyon/wiki/Java%20Decompiler](https://bitbucket.org/mstrobel/procyon/wiki/Java%20Decompiler) || [procyon-decompiler](https://aur.archlinux.org/packages/procyon-decompiler/), GUI: [luyten](https://aur.archlinux.org/packages/luyten/)

## 在JVM间切换

帮助脚本 `archlinux-java` 提供了如下功能:

```
archlinux-java <COMMAND>

COMMAND:
	status		List installed Java environments and enabled one
	get		Return the short name of the Java environment set as default
	set <JAVA_ENV>	Force <JAVA_ENV> as default
	unset		Unset current default Java environment
	fix		Fix an invalid/broken default Java environment configuration

```

### 列出兼容的安装了的Java环境

```
$ archlinux-java status

```

例如:

```
$ archlinux-java status
Available Java environments:
  java-7-openjdk (default)
  java-8-openjdk/jre

```

标着 *(default)* 表示 `java-7-openjdk` 被设为默认. `java` 的调用和其他二进制调用都依赖于这个安装的Java.同时前面的输出表示只有OpenJDK8的JRE部分被安装了.

### 改变默认Java环境

```
# archlinux-java set <JAVA_ENV_NAME>

```

例如:

```
# archlinux-java set java-8-openjdk/jre

```

**Tip:** 想看可用的 `<JAVA_ENV_NAME>` 名字, 使用 `archlinux-java status`.

注意到 `archlinux-java` 并不会让你设置一个不可用的Java环境. 在前面的例子中, [jre8-openjdk](https://www.archlinux.org/packages/?name=jre8-openjdk) 安装了但是 [jdk8-openjdk](https://www.archlinux.org/packages/?name=jdk8-openjdk) 并 **没有** 所以尝试设置 `java-8-openjdk` 将会失败:

```
# archlinux-java set java-8-openjdk
'/usr/lib/jvm/java-8-openjdk' is not a valid Java environment path

```

### 取消设置的默认Java环境

没必要取消设置的Java环境因为安装包会让它们注意这种情况. 如果你还想这么做的话，用这条命令 `unset`:

```
# archlinux-java unset

```

### 解决默认Java环境的问题

如果一个不可用的Java环境链接被设置，用 `archlinux-java fix` 命令尝试修复它. 同时如果没有默认Java环境被设置，它会找可用的并尝试为你设置。官方支持的包 "OpenJDK 8" 将会比其他安装的环境被优先考虑.

```
# archlinux-java fix

```

### 运行非默认Java版本的程序

如果你想运行其它版本而不是默认版本的程序(例如你有JRE7和JRE8同时装在系统里), 你可以把你的程序打包进一个小bash脚本里来暂时改变Java的默认版本。例如如果默认版本是JRE7而你想用JRE8:

```
#!/bin/sh 

export PATH=/usr/lib/jvm/java-8-openjdk/jre/bin/:$PATH
exec /path/to/application "$@"

```

## 包支持`archlinux-java`的先决条件

**注意:** 这条信息同样适用于 `archlinux32-java` 的32位比特Java包, 如果它们的包或者可执行名字里有 `32` ，都可适用.

这个分区的信息针对愿意提供包作为备份JVM给 [Arch User Repository (简体中文)](/index.php/Arch_User_Repository_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch User Repository (简体中文)") 的贡献者， 并且能够用 `archlinux-java`集成Arch Linux JVM方案. 如果要这样的话，这些包应该:

*   把所有文件放在这里 `/usr/lib/jvm/java-${JAVA_MAJOR_VERSION}-${VENDOR_NAME}`
*   确认所有的 [java-runtime-common](https://www.archlinux.org/packages/extra/any/java-runtime-common/files/) 和 [java-environment-common](https://www.archlinux.org/packages/extra/any/java-environment-common/files/) 提供的可执行链接在相关包里都是可用的
*   把所有链接从 `/usr/bin` 移动到可执行文件里, 除非这些链接不属于 [java-runtime-common](https://www.archlinux.org/packages/extra/any/java-runtime-common/files/) 和 [java-environment-common](https://www.archlinux.org/packages/extra/any/java-environment-common/files/)
*   用 `-${VENDOR_NAME}${JAVA_MAJOR_VERSION}` 的格式给手册页添加后缀 (查阅 [jre8-openjdk file list](https://www.archlinux.org/packages/extra/x86_64/jre8-openjdk/files/) 它的手册页用 `-openjdk8`做后缀)
*   不要定义任何 [冲突](/index.php/PKGBUILD_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#conflicts "PKGBUILD (简体中文)") 和[替代](/index.php/PKGBUILD_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#replaces "PKGBUILD (简体中文)") ，用其他的JDK, `java-runtime`, `java-runtime-headless` 和 `java-environment`
*   在*安装函数* 里使用`archlinux-java` 脚本来把Java环境设置为默认 **如果没有其他可用的Java环境准备设置的话** (即: 这些包不应该 **强制** 被装为默认). 查阅 [officially supported Java environment package sources](https://projects.archlinux.org/svntogit/packages.git/tree/trunk?h=packages/java7-openjdk) 做例子

同时也该注意到:

*   包需要的 **任何** Java环境应该声明依赖，和往常一样在 `java-runtime`, `java-runtime-headless` 或者 `java-environment`里声明
*   包如果需要 **特定Java提供商** 应该在相关包里声明依赖。
*   OpenJDK 包现在应该声明 `provides="java-runtime-openjdk=${pkgver}"` 等. 这能让第三方的包在没有特定版本要求的OpenJDK里声明依赖

## 故障排除

### MySQL

因为JDBC-驱动经常使用URL的端口来建立到数据库的连接, 所以通过 "远程" (i.e., MySQL不会根据默认设置监听端口)的办法应该被考虑，尽管它们可能运行在同一个主机上, 所有, 要用JDBC和MySQL的话你应该启用到MySQL的远程连接，, 在[MySQL#Grant remote access](/index.php/MySQL#Grant_remote_access "MySQL")查询指导.

### IntelliJ IDEA

如果你在设置JDK的时候选择了系统的JDK，同时碰到了错误提示 `The selected directory is not a valid home for JDK`，这个时候你需要重新安装一个jdk，在IntelliJ IDEA设置jdk的时候选择新安装的JDK.

### 冒充另一个窗口管理器

你可以使用 [wmname](https://www.archlinux.org/packages/?name=wmname) ，从 [suckless.org](https://tools.suckless.org/x/wmname)下载，来使JVM相信你是在运行一个不同的窗口管理器. 这可以解决在窗口管理器发生的Java GUIs渲染问题， 比如说 [awesome (简体中文)](/index.php/Awesome_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Awesome (简体中文)") 或者 [Dwm (简体中文)](/index.php/Dwm_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Dwm (简体中文)") 或者 [Ratpoison (简体中文)](/index.php/Ratpoison_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Ratpoison (简体中文)").

```
$ wmname LG3D

```

你必须在运行了这条命令后重启有问题的程序.

这个能起作用是因为JVM包含了一个已知的、非重新父母窗口管理器的硬编码名单. 为了最大化反讽效果，一些用户喜欢冒充 `LG3D`, 一种非重新父母窗口管理器 [由Sun公司用Java写成](https://en.wikipedia.org/wiki/Project_Looking_Glass "wikipedia:Project Looking Glass").

### 难以辨认的字体

除了下述的建议 [#更好的字体渲染](#更好的字体渲染), 可能还是有一些字体难以辨认. 如果是这样的话,有一个很好的机会能用Microsoft的字体. 在[AUR](/index.php/AUR "AUR")安装[ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/) .

### 一些应用缺少文字

如果一些应用完全没有文字，你可以用下面的办法[#建议和技巧](#建议和技巧) 它在[FS#40871](https://bugs.archlinux.org/task/40871)里被建议.

### 应用未调整WM大小，菜单快速关闭

标准Java GUI工具包有一个非重新父母窗口管理器的硬编码名单. 如果你使用的不在名单里, 运行一些Java 程序就可能产生一些问题. 最普遍的一个问题是 "灰斑", 这发生在Java程序渲染纯灰色的盒子而不是渲染GUI的时候. 另一个问题是菜单会响应你的点击，但是立马关闭.

有很多事能帮到忙:

*   对于 [jre7-openjdk](https://www.archlinux.org/packages/?name=jre7-openjdk) 或者 [jre8-openjdk](https://www.archlinux.org/packages/?name=jre8-openjdk), 在 `/etc/profile.d/jre.sh`文件里加入一行 `export _JAVA_AWT_WM_NONREPARENTING=1` . 然后，用source命令处理 `/etc/profile.d/jre.sh` 或者重新登出登录.
*   对于 Oracle 的 JRE/JDK, 用 [SetWMName.](https://wiki.haskell.org/Xmonad/Frequently_asked_questions#Using_SetWMName) 然而，当使用`XMonad.Hooks.EwmhDesktops`的时候它的作用可能被取消. 这种情况下，添加

```
>> setWMName "LG3D"

```

到 `LogHook` 可以起作用.

查阅[[2]](https://wiki.haskell.org/Xmonad/Frequently_asked_questions#Problems_with_Java_applications.2C_Applet_java_console) 可以获取更多信息.

### 当调试JavaFX程序的时候系统卡住

当你调试JavaFX程序的时候系统卡住了，你可以尝试提供JVM以下选项 `-Dsun.awt.disablegrab=true`.

查阅 [https://bugs.java.com/view_bug.do?bug_id=6714678](https://bugs.java.com/view_bug.do?bug_id=6714678)

### JavaFX 的 MediaPlayer 构造函数抛出了一个 exception

从JavaFX声音模板里创造 MediaPlayer 类的实例可能会抛出下面的exception (Oracle JDK 和 OpenJDK都会有)

```
... (i.e. FXMLLoader construction exceptions) ...
Caused by: MediaException: UNKNOWN : com.sun.media.jfxmedia.MediaException: Could not create player! : com.sun.media.jfxmedia.MediaException: Could not create player!
 at javafx.scene.media.MediaException.exceptionToMediaException(MediaException.java:146)
 at javafx.scene.media.MediaPlayer.init(MediaPlayer.java:511)
 at javafx.scene.media.MediaPlayer.<init>(MediaPlayer.java:414)
 at <constructor call>
...

```

这是JavaFX和Arch Linux库里提供的 [ffmpeg](https://www.archlinux.org/packages/?name=ffmpeg) 构建不兼容的结果.

解决办法是安装 [ffmpeg-compat-55](https://aur.archlinux.org/packages/ffmpeg-compat-55/).

查阅 [https://www.reddit.com/r/archlinux/comments/70o8o6/using_a_javafx_mediaplayer_in_arch/](https://www.reddit.com/r/archlinux/comments/70o8o6/using_a_javafx_mediaplayer_in_arch/)

### Java程序无法打开外部链接

如果Java程序不能打开链接到, 比如说, 你的浏览器, 安装[gvfs](https://www.archlinux.org/packages/?name=gvfs).这是 Desktop.Action.BROWSE 方法所必须的. 查阅 [[3]](https://bugs.launchpad.net/ubuntu/+source/openjdk-8/+bug/1574879/comments/2)

## 建议和技巧

**注意:** 这个区里提的建议在所有程序里有用,如果你用的是明确的安装的 (外部) Java 运行的话.一些程序是用个人的 (私有的) Java运行或者是自己的GUI机制, 字体渲染机制, 等等., 这样的话下面写的都不保证能起作用.

大多数Java程序的行为都可以通过向Java运行提供预定义变量来操控. 查阅 [this forum post](https://bbs.archlinux.org/viewtopic.php?id=72892), 一种这样做的方法包括添加下面的行到你的 `~/.bashrc`文件 (或者通过 `/etc/profile.d/jre.sh` 来影响不是通过用source命令处理`~/.bashrc`来运行的程序 , 比如., 用Gnome应用师徒来运行程序):

```
export _JAVA_OPTIONS="-D**<option 1>** -D**<option 2>**..."

```

比如，用系统的反别名字体来使swing有GTK的视觉效果和感觉:

```
export _JAVA_OPTIONS='-Dawt.useSystemAAFontSettings=on -Dswing.aatext=true -Dswing.defaultlaf=com.sun.java.swing.plaf.gtk.GTKLookAndFeel'

```

### 更好的字体渲染

开源和闭源的Java实现都有不合适的反别名字体实现. 这可以通过以下办法来解决: `-Dawt.useSystemAAFontSettings=on`, `-Dswing.aatext=true`

查阅 [Java Runtime Environment fonts](/index.php/Java_Runtime_Environment_fonts "Java Runtime Environment fonts") 来获取更多信息.

### 禁止命令行的 'Picked up _JAVA_OPTIONS' 消息

设置 _JAVA_OPTIONS 环境变量使 java (openjdk) 写入以下形式的stderr消息: 'Picked up _JAVA_OPTIONS=...'. 要在终端中禁止这些消息，可以取消设置shell启动文件中的环境变量，并使用别名java来传递与命令行参数相同的选项:

```
_SILENT_JAVA_OPTIONS="$_JAVA_OPTIONS"
unset _JAVA_OPTIONS
alias java='java "$_SILENT_JAVA_OPTIONS"'

```

### GTK 视觉效果和感觉

如果你的Java程序看起来很丑, 你可能想为swing组件设置默认外表和感觉:

`swing.defaultlaf=com.sun.java.swing.plaf.gtk.GTKLookAndFeel`.

一些Java程序坚持用跨平台的金属外表和感觉. 在这些情况下，你可以通过设置下面的属性强制这些app用GTK外表和感觉:

`swing.crossplatformlaf=com.sun.java.swing.plaf.gtk.GTKLookAndFeel`.

#### GTK3支持

在Java的版本9之前, GTK的外观和感觉是与GTK2链接的，但是同时许多更新的桌面程序用的是GTK3\. 这种GTK版本间的不兼容性可能打断程序使用Java的GUI插件，因为同一个进程里GTK2和GTK3的混合不被支持 (例如, LibreOffice 5.0).

从 [Java 9](https://openjdk.java.net/jeps/283)以来, GTK的外观和感觉可以和GTK的版本 `2`, `2.2` 和 `3`一起运行, 默认GTK2\. 这可以通过设置下面的属性来覆盖:

`jdk.gtk.version=3`

### 更好的2D性能

切换到基于OpenGL的硬件加速管道会提升2D性能

```
export _JAVA_OPTIONS='-Dsun.java2d.opengl=true'

```

**注意:** 开启这项选项会导致像Jetbrains的IDE这样的软件的UI表现不正常, 让它们的窗口、弹窗和工具栏只画一部分.

### 非重新父母窗口管理器 / 灰色窗口 / 程序被绘制得不恰当

非重新父母窗口管理器的用户应该在他们的 `.xinitrc`里设置以下环境变量

```
export _JAVA_AWT_WM_NONREPARENTING=1

```

不设置这个的话会导致Java程序被绘制得不恰当.

## 参阅

*   [Introduction to Programming Using Java](https://math.hws.edu/javanotes/)