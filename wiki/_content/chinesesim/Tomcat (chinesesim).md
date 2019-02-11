**翻译状态：** 本文是英文页面 [Tomcat](/index.php/Tomcat "Tomcat") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-11-30，点击[这里](https://wiki.archlinux.org/index.php?title=Tomcat&diff=0&oldid=498974)可以查看翻译后英文页面的改动。

Tomcat 是一个由 Apache Software Foundation 开发的开源的 Java [Servlet 容器](https://en.wikipedia.org/wiki/Java_Servlet#Servlet_containers "wikipedia:Java Servlet")。想要了解更多的配置信息，请参阅 [Tomcat and Apache](/index.php/Tomcat_and_Apache "Tomcat and Apache") 。

**注意:** 目前存在两个版本的稳定分支： [7](http://tomcat.apache.org/download-70.cgi) 和 [8](https://tomcat.apache.org/download-80.cgi)。没一个版本能完全替代另一个。相反，[每个分支是一部分 "Servlet" 和 "JSP" Java 标准的实现](http://tomcat.apache.org/whichversion.html#Apache_Tomcat_Versions)。两个版本都被 Arch Linux 官方支持：[tomcat7](https://www.archlinux.org/packages/?name=tomcat7) 和 [tomcat8](https://www.archlinux.org/packages/?name=tomcat8)。选用哪个版本主要由你的 web 程序的需求来决定的。如果你只是为了试试 tomcat 或者你不打算花时间来区分，那么你选用 tomcat7 可能会更好点。这个页面针对的是 tomcat7 ，但是大部分内容也适用于 tomcat8。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 安装](#安装)
    *   [1.1 文件系统层次结构](#文件系统层次结构)
*   [2 初始化配置](#初始化配置)
*   [3 启动/停止 Tomcat](#启动/停止_Tomcat)
    *   [3.1 备用“手动”方法](#备用“手动”方法)
*   [4 部署和处理 Web 程序](#部署和处理_Web_程序)
    *   [4.1 GUI 方法](#GUI_方法)
    *   [4.2 CLI 方法](#CLI_方法)
    *   [4.3 把项目部署在别的目录](#把项目部署在别的目录)
*   [5 日志记录](#日志记录)
*   [6 进一步设置](#进一步设置)
    *   [6.1 从以前版本的 Tomcat 中迁移](#从以前版本的_Tomcat_中迁移)
    *   [6.2 使用不同版本的 JRE/JDK 来运行 Tomcat](#使用不同版本的_JRE/JDK_来运行_Tomcat)
    *   [6.3 安全配置](#安全配置)
*   [7 故障排除](#故障排除)
    *   [7.1 Tomcat 服务已经启动，但是无法加载页面](#Tomcat_服务已经启动，但是无法加载页面)

## 安装

安装 [tomcat7](https://www.archlinux.org/packages/?name=tomcat7) 或者 [tomcat8](https://www.archlinux.org/packages/?name=tomcat8) 中的一个。

如果打算部署 Tomcat 到一个生产环境，请考虑安装 [tomcat-native](https://www.archlinux.org/packages/?name=tomcat-native) 。Tomcat-native 将配置服务器来使用 Apache Portable Runtime (APR) 库的网络连接（socket）和 RNG 实现。它将使用原生的32位或64位代码来提升性能，对速度非常敏感的生产环境经常会用到。Tomcat 的安装不需要额外的配置。更多的信息请参阅 [Tomcat 官方文档](http://tomcat.apache.org/native-doc/) 。

使用 tomcat-native 将会移除位于 `catalina.err` 的下列警告：

```
INFO: The APR based Apache Tomcat Native library which allows optimal performance in production environments was not found on the java.library.path [...]

```

### 文件系统层次结构

将 `*` 用你所安装的版本 (7 或者 8) 替代。

| 路径 | 用途 |
| `/etc/tomcat*` | 配置文件。包括： `tomcat-users.xml` (defines users allowed to use administration tools and their roles), `server.xml` (Main Tomcat configuration file), `catalina.policy` (security policies configuration file) |
| `/usr/share/tomcat*` | Tomcat 主文件夹。包括脚本文件及到其它文件夹的链接 |
| `/usr/share/java/tomcat*` | Tomcat 的 Java 库（jar文件） |
| `/var/log/tomcat*` | **不**被 `systemd` 记录的日志文件 (参阅 [#日志记录](#日志记录)) |
| `/var/lib/tomcat*/webapps` | Tomcat 部署你的 Web 程序的地方 |
| `/var/tmp/tomcat*` | Tomcat 存储你的 Web 程序数据的地方 |

## 初始化配置

你需要通过编辑下面这个文件来使用 manager 和 admin 管理界面： `/etc/tomcat7/tomcat-users.xml`

取消 XML 声明中"role and user"这一块的注释，然后根据你的需要，修改并启用 `tomcat`, {{Ic|admin-{gui,script} }} 和 {{Ic|manager-{gui,script,jmx,status} }} 等角色（详情请参阅 [Configuring Manager Application Access](http://tomcat.apache.org/tomcat-7.0-doc/manager-howto.html#Configuring_Manager_Application_Access)）。

简单来说，`tomcat` 用于运行 Tomcat 服务器，`manager-*` 用于管理 Tomcat 服务器上的 web 程序，`admin-*` 是 Tomcat 服务器的全权管理员。

下面是一个配置文件的样例，里面定义了一些包含用户名和密码的角色（请务必修改把 [CHANGE_ME] 改成更为更安全的密码）：

 `/etc/tomcat7/tomcat-users.xml` 
```
<?xml version='1.0' encoding='utf-8'?>
<tomcat-users>
  <role rolename="tomcat"/>
  <role rolename="manager-gui"/>
  <role rolename="manager-script"/>
  <role rolename="manager-jmx"/>
  <role rolename="manager-status"/>
  <role rolename="admin-gui"/>
  <role rolename="admin-script"/>
  <user username="tomcat" password="**[CHANGE_ME]**" roles="tomcat"/>
  <user username="manager" password="**[CHANGE_ME]**" roles="manager-gui,manager-script,manager-jmx,manager-status"/>
  <user username="admin" password="**[CHANGE_ME]**" roles="admin-gui"/>
</tomcat-users>
```

请记住，每一次修改了这个文件都必须要重启 Tomcat 服务器。

[这篇博文](http://blog.techstacks.com/2010/07/new-manager-roles-in-tomcat-7-are-wonderful.html) 更好地介绍了这些角色。

为了读取配置文件，以及为了和一些 IDE 更好地配合，你需要把你的用户加入 `tomcat7` (或者 `tomcat8`) 的组：

```
 gpasswd -a <user> tomcat<number>

```

## 启动/停止 Tomcat

[启动](/index.php/Start "Start") `tomcat7` 服务。

一旦 Tomcat 启动了，你可以通过访问这个页面来查看结果：[http://localhost:8080](http://localhost:8080) 。如果显示了一个漂亮的 Tomcat 本地页面，表明你的 Servlet 容器正在运行，并且可以装载你的 web 程序了。如果启动脚本失败了，又或者你在浏览器里只看到了一个 Java 错误页面，你可以通过 [systemd的 journalctl](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#日志 "Systemd (简体中文)") 命令来查看启动日志。Google 上有 Tomcat 日志里常见问题的解决办法。

**Note:** To improve security, Arch Linux's Tomcat packages use the [jsvc](http://commons.apache.org/daemon/jsvc.html) binary from Apache's [common-daemons](http://commons.apache.org/daemon/). Tomcat's `systemd` service runs this Apache binary with root privileges which itself starts Tomcat with an underprivileged user (`tomcat7:tomcat7` in Arch Linux). This prevents malicious code that could be executed in a bad web application from causing too much damage. This also enables the use of ports under 1024 if needed. See `man jsvc` for options available and pass them through the `CATALINA_OPTS` environment variable declared in `/etc/conf.d/tomcat7`.

### 备用“手动”方法

Tomcat 也能通过上游脚本来直接控制：

```
/usr/share/tomcat/bin/{startup.sh,shutdown.sh,..}

```

这种方法对于调试程序甚至调试 Tomcat 非常有帮助。但不要在首次启动 Tomcat 的时候用这种方法，因为这会导致一些权限错误，从而使一些程序停止运行。为了使用这些脚本，可能需要做一些额外的配置。并且使用这些脚本将会阻止上面所提到的 jsvc 安全优势。

## 部署和处理 Web 程序

Tomcat 7 捆绑了5个已经部署了的 Web 程序（有必要的话，把 localhost 换成你的服务器的全称域名）：

*   默认主页: [http://localhost:8080/](http://localhost:8080/)
*   Tomcat 7 的本地文档: [http://localhost:8080/docs/](http://localhost:8080/docs/)
*   Servlets 和 JSP 的示例: [http://localhost:8080/examples/](http://localhost:8080/examples/)
*   用于处理虚拟主机的 host-manager: [http://localhost:8080/host-manager/](http://localhost:8080/host-manager)
*   用于管理 web 程序的 manager: [http://localhost:8080/manager/html/](http://localhost:8080/manager/html)

### GUI 方法

最简单的方法是通过 manager 程序来部署 [http://localhost:8080/manager/html](http://localhost:8080/manager/html)。 使用你在 `tomcat-users.xml` 定义的 `manager` 角色的用户名和密码来登陆。登陆进去后，你将看到5个已经部署了的 Web 程序。通过 “Deploy” 区域来添加你自己的 Web 程序，通过 “Applications” 区域来停止/启动/取消部署。

### CLI 方法

你也可以通过复制程序的 WAR 文件到 `/usr/share/tomcat7/webapps` 目录来部署。确保 `autoDeploy` 选项如下面所示，设置在了正确的主机：

 `/etc/tomcat7/server.xml` 
```
...
<Host name="localhost"  appBase="webapps"
      unpackWARs="true" **autoDeploy="true"**>
...
```

### 把项目部署在别的目录

你也可以通过设置 `Context` 来把你的项目部署在别的目录。 你需要在 `/etc/tomcat<number>/Catalina/localhost/` 目录下创建你的 context。Context 是一个用于指定 tomcat 查找目录的 xml 文件，其基本格式如下：

 `/etc/tomcat7/Catalina/localhost/whatShouldFollowLocalhost.xml`  `<Context path="/whatSholdFollwLocalhost" docBase="/where/your/project/is/" reloadable="true"/>` 

假设项目放在用户 /home 目录下的某个文件夹里，则 context 像这样写：

 `/etc/tomcat7/Catalina/localhost/myProject.xml`  `<Context path="/myProject" docBase="/home/archie/code/jsp/myProject" reloadable="true"/>` 

现在项目文件可以放在 `/home/archie/code/jsp/myProject/` 目录下了。要想在浏览器里查看这个项目，访问 [http://localhost:8080/myProject](http://localhost:8080/myProject) 。 如果 tomcat 无法加载这些文件，可能是遇到了权限问题，运行 `chmod o+x /home/archie/code/jsp/myProject` 应该可以解决这个问题。

## 日志记录

如果使用的是 Arch Linux 官方的 Tomcat 包，则使用 [systemd的 journalctl](/index.php/Systemd#Journal "Systemd") 来记录 **启动日志**。这意味着 `/var/log/tomcat7/catalina.err` 和 `/var/log/tomcat7/catalina.out` 将 **不会** 被使用。而其它的日志，例如作为 `Valve` 定义在 `/etc/tomcat7/server.xml` 里的 access logs 和 business logs 则默认会记录在 `/var/log/tomcat7/` 目录下。

为了保存上游风格的日志，把 systemd 文件 `/lib/systemd/system/tomcat7.service` 复制到 `/etc/systemd/system/tomcat7.service` ，然后把两处 `SYSLOG` 改为日志文件的绝对路径。

## 进一步设置

基本的配置，可以通过虚拟主机管理程序来设置：[http://localhost:8080/host-manager/html](http://localhost:8080/host-manager/html) 。使用你在 `tomcat-users.xml` 中设置的用户名和密码来登陆。其它选项可通过修改 `/etc/tomcat7` 下的配置文件来设置，最重要的莫过于 `server.xml`。对这些文件的修改已经超过了本入门页面的范围，请访问 [官方 Tomcat 7 文档](http://tomcat.apache.org/tomcat-7.0-doc/index.html) 来获得更多支持。

### 从以前版本的 Tomcat 中迁移

正如介绍里说的，“Tomcat 8 并不替代 Tomcat 7”。他们都是 Servlet/JSP 标准的实现。因此，你的程序使用了哪个版本的 Servlet/JSP 决定了你需要使用 [哪个版本的](http://tomcat.apache.org/whichversion.html#Apache_Tomcat_Versions) Tomcat 。如果你需要迁移，官方网站 [会给你建议](http://tomcat.apache.org/migration.html) 。

### 使用不同版本的 JRE/JDK 来运行 Tomcat

除了安装需要的 JRE/JDK 外，唯一要做的就是设置 Tomcat `systemd` service 文件的 TOMCAT_JAVA_HOME 变量。

正如 [Systemd#Editing provided units](/index.php/Systemd#Editing_provided_units "Systemd") 里所说的，这个变量可以被用户配置覆盖：

1.  创建 */etc/systemd/system/tomcat7.service.d* 目录
2.  在这个目录里，创建一个包含以下内容的 *start.conf* 文件（如果使用的是 Oracle JDK [jdk](https://aur.archlinux.org/packages/jdk/) ，则替换为*/usr/lib/jvm/java-8-jdk*）：

```
[Service]
Environment=TOMCAT_JAVA_HOME=/usr/lib/jvm/java-8-openjdk

```

另外，把 service 文件 */usr/lib/systemd/system/tomcat7.service* ，复制到 */etc/systemd/system/* ，并替换这一行

```
Environment=TOMCAT_JAVA_HOME=/usr/lib/jvm/java-7-openjdk

```

为 (以 Oracle JDK 为例)

```
Environment=TOMCAT_JAVA_HOME=/opt/java

```

### 安全配置

本页面最低限度地使你的第一个 web 应用运行在 Tomcat 上，并不意味着这是一个管理 Tomcat （这是一项单独的工作）的明确的指导。Tomcat 官方网站提供了所有必须的官方事项。你也可以参考 [这个 O'Reilly 页面](http://oreilly.com/java/archive/tomcat-tips.html) 和 这个 [页面](http://www.unidata.ucar.edu/projects/THREDDS/tech/reference/TomcatSecurity.html) 。这里还是提供了一些安全方面的建议：

*   保持你的 Tomcat 更新到了最新版，以便获得安全问题的最新修复
*   移除不需要的默认程序，比如 `examples`，`docs`，默认的主页 `ROOT` ("_" 在 `manager` 程序里) 。这可以防止潜在的安全漏洞被利用。使用 `manager` 来管理。

为了更安全，你甚至可以删除 host-manager 和 manager 应用。但是别忘了，后者对部署 web 应用非常有用。

*   关闭 WAR 自动部署选项。这可以防止某些获得限制权限的人复制 WAR 文件到 `/usr/share/java/webapps` 来直接运行它。编辑 `server.xml` 并把 `autoDeploy` 设为 `false`：

 `/etc/tomcat7/server.xml` 
```
...
<Host name="localhost"  appBase="webapps"
      unpackWARs="true" **autoDeploy="false"**>
...
```

*   匿名化 Tomcat 的默认错误页面来防止潜在的攻击者取得 Tomcat 的版本。想知道 Tomcat 默认显示什么，只需要访问一个不存在的页面，比如 [http://localhost:8080/I_dont_exist](http://localhost:8080/I_dont_exist) ，你将会看到一个404错误页面，最底下标明了 Tomcat 的版本。

要想匿名化这个，编辑或打开这个 JAR （像 `vim` 等编辑器能直接编辑 zip 文件）

```
/usr/share/tomcat7/lib/catalina.jar

```

然后编辑这个文件

 `org/apache/catalina/util/ServerInfo.properties` 
```
...
server.info=
server.number=
server.built=
...
```

*   禁用 `server.xml` 里不使用的 `connectors`
*   保持对 `/etc/tomcat7/server.xml` 的访问限制。只有 `tomcat` 用户，和/或者 `root` 能读写这个文件
*   保持 `jsvc` 的使用。不要使用上游启动脚本，除非有上文安全部分提到的特别原因。
*   在 `tomcat-users.xml` 里为每个用户启用强壮并且不同的密码，给真正需要的用户角色，并且禁用你用不到的用户或者角色。

你还可以用使用下列上游脚本来加密 `tomcat-users.xml` 里的密码：

```
/usr/share/tomcat7/bin/digest.sh -a SHA NEW_PASSWORD

```

这条命令将会输出类似于下面的信息：

```
NEW_PASSWORD:b7bbb48a5b7749f1f908eb3c0c021200c72738ce

```

然后用哈希的部分替换掉 `tomcat-users.xml` 里的密码部分，然后把下文加入到 `server.xml` 中：

 `/etc/tomcat7/server.xml` 
```
<Host
  ...
  <Realm
    ...
    **className="org.apache.catalina.realm.MemoryRealm" digest="SHA"**
    ...
  />
  ...
/>
```

注意，这个方法可能意义并不大。因为只有 root 和/或者 tomcat 能读写这个文件，而如果一个入侵者成功获得了 root 权限，那么他将不需要这些密码来混乱你的程序和数据。请确保对这个文件的读写限制！

*   永远弄清楚你在部署什么

## 故障排除

### Tomcat 服务已经启动，但是无法加载页面

首先，检查 `/etc/tomcat7/tomcat-users.xml` 有没有语法错误。如果一切正常并且 `tomcat7` 正在运行，输入 `journalctl -r` 查看log，看看有没有抛出什么异常（参照 [Logging](/index.php/Tomcat#Logging "Tomcat") ）。 如果你看到有类似 `java.lang.Exception: Socket bind failed: [98] Address already in use` 的异常，说明其它服务正在监听这个端口。例如，有可能 [Apache](/index.php/Apache_HTTP_Server "Apache HTTP Server") 和 Tomcat 都在监听同一个端口（例如你在8080端口运行的 Apache 使用在80端口运行的[Nginx](/index.php/Nginx "Nginx") 作为代理）。如果是这种情况，编辑 `/etc/tomcat7/server.xml` 文件，然后修改 `<Service name="Catalina">` 下的 Connector port 为其它的值：

 `/etc/tomcat7/server.xml` 
```
<?xml version='1.0' encoding='utf-8'?>
...
...
<Service name="Catalina">
    <Connector executor="tomcatThreadPool"
                 port="8090" protocol="HTTP/1.1"
                 connectionTimeout="20000"
                 redirectPort="8443" />
...
...
</Service>
```

最后 [重启](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#使用单元 "Systemd (简体中文)") `tomcat7` 和 `httpd` 服务。