**翻译状态：** 本文是英文页面 [Node.js](/index.php/Node.js "Node.js") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2014-08-16，点击[这里](https://wiki.archlinux.org/index.php?title=Node.js&diff=0&oldid=329864)可以查看翻译后英文页面的改动。

[Node.js](http://nodejs.org/) 是一个 javascript 运行环境，并附带有常用的库. 它使用了 [Google's V8 引擎](https://code.google.com/p/v8/) 在浏览器外执行代码. 由于其是事件驱动、非阻塞 I/O 模型，它适合于实时 web 应用.

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 Node Packaged Modules](#Node_Packaged_Modules)
    *   [2.1 使用 npm 管理包](#.E4.BD.BF.E7.94.A8_npm_.E7.AE.A1.E7.90.86.E5.8C.85)
        *   [2.1.1 安装软件包](#.E5.AE.89.E8.A3.85.E8.BD.AF.E4.BB.B6.E5.8C.85)
        *   [2.1.2 更新包](#.E6.9B.B4.E6.96.B0.E5.8C.85)
            *   [2.1.2.1 更新所有包](#.E6.9B.B4.E6.96.B0.E6.89.80.E6.9C.89.E5.8C.85)
        *   [2.1.3 删除包](#.E5.88.A0.E9.99.A4.E5.8C.85)
        *   [2.1.4 列出所有包](#.E5.88.97.E5.87.BA.E6.89.80.E6.9C.89.E5.8C.85)
    *   [2.2 使用 pacman 管理包](#.E4.BD.BF.E7.94.A8_pacman_.E7.AE.A1.E7.90.86.E5.8C.85)
*   [3 其他资源](#.E5.85.B6.E4.BB.96.E8.B5.84.E6.BA.90)

## 安装

[nodejs](https://www.archlinux.org/packages/?name=nodejs) 包位于 [官方软件仓库](/index.php/Official_repositories "Official repositories") .

## Node Packaged Modules

[npm](https://www.npmjs.org/) 是官方的 node.js 包管理器，已包含在 [nodejs](https://www.archlinux.org/packages/?name=nodejs) 中.

### 使用 npm 管理包

#### 安装软件包

任何包可以用以下命令安装：

```
$ npm install packageName

```

这个命令会将包安装在当前目录下 `node_modules` 目录内，可执行命令（如果有）安装在 `node_modules/.bin` 目录下.

作为系统级的全局安装使用 `-g` 选项:

```
# npm -g install packageName

```

默认情形下这个命令会将包安装至 `/usr/lib/node_modules/npm` ，需要管理员权限.

作为个人用户级的安装您可以使用一个本地目录来配置 `npm` 。这可以通过多种方式完成：

*   在命令中添加 `--prefix` 标记 (e.g. `npm -g install packageName --prefix ~/.node_modules` )。
*   使用 `npm_config_prefix` 环境变量。
*   使用用户配置文件 `~/.npmrc` 。

第一个方法已不被推荐因为您需要记住位置并且每次操作都需要添加参数。

第二个方法只是添加下列行到您的 shell 配置文件 (e.g. `.bash_profile` )。

```
PATH=$PATH:~/.node_modules/bin
export npm_config_prefix=~/.node_modules

```

不要忘记重新登录或重启您的 shell。

第三个方法您可以使用命令：

```
$ npm config edit

```

您可以找到 `prefix` 选项并且设置一个期望的位置：

```
prefix=~/.node_modules

```

不要忘记删除行前面的 `;` 否则会被当作注释。

您现在可以添加可执行命令的位置到您的 shell 配置文件 (e.g. `.bash_profile` )。

```
PATH=$PATH:~/.node_modules/bin

```

再次提示不要忘记重新登录或重启您的 shell。

#### 更新包

更新包只需要执行

```
 $ npm update packageName

```

对于全局环境安装的包 ( `-g` )

```
 # npm update -g packageName

```

**Note:** 请记住全局安装的包需要管理员权限

##### 更新所有包

有时您只希望更新所有包，去掉包名将试图更新所有包。

```
 $ npm update

```

或者添加 `-g` 标记更新全局环境安装的包

```
 # npm update -g

```

#### 删除包

删除使用 `-g` 标记安装的包只须：

```
# npm -g uninstall packageName

```

**Note:** 请记住全局安装的包需要管理员权限

若删除个人用户目录下的包去掉标记执行：

```
 $ npm uninstall packageName

```

#### 列出所有包

若要显示已安装的包的树形视图执行：

```
$ npm -g list

```

### 使用 pacman 管理包

一些 node.js 包可以在 [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") 找到，命名为 `nodejs-packageName` 格式。

## 其他资源

更多关于 [nodejs](https://www.archlinux.org/packages/?name=nodejs) 和官方包管理器 [npm](https://www.npmjs.org/) 的使用信息您也许需要查询下列额外资源。

*   [NodeJs Documentation](http://nodejs.org/documentation/) Node 文档和教程。
*   [NodeJS Community](http://nodejs.org/community/)
*   [API Documentation](https://www.npmjs.org/doc/) 官方 `npm` API 文档
*   IRC channel #node.js on irc.freenode.net

中文社区

*   [v2ex NodeJS 节点](https://www.v2ex.com/go/nodejs) 开发者作品发布与开发探讨
*   [cnodejs.org](http://cnodejs.org/) Node.js 专业中文社区