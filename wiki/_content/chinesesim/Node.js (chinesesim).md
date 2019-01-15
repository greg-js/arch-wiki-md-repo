**翻译状态：** 本文是英文页面 [Node.js](/index.php/Node.js "Node.js") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2019-01-14，点击[这里](https://wiki.archlinux.org/index.php?title=Node.js&diff=0&oldid=424348)可以查看翻译后英文页面的改动。

[Node.js](http://nodejs.org/) 是一个 javascript 运行环境，并附带有功能丰富的库.使用 [Google's V8 引擎](https://code.google.com/p/v8/) 在浏览器外执行代码. 由于其是事件驱动、非阻塞 I/O 模型，它适合于实时 web 应用.

## Contents

*   [1 安装](#安装)
    *   [1.1 多版本需求](#多版本需求)
*   [2 Node Packaged Modules](#Node_Packaged_Modules)
    *   [2.1 使用 npm 管理包](#使用_npm_管理包)
        *   [2.1.1 安装软件包](#安装软件包)
        *   [2.1.2 更新包](#更新包)
            *   [2.1.2.1 更新所有包](#更新所有包)
        *   [2.1.3 删除包](#删除包)
        *   [2.1.4 列出所有包](#列出所有包)
    *   [2.2 使用 pacman 管理包](#使用_pacman_管理包)
*   [3 问题处理](#问题处理)
    *   [3.1 node-gyp python 错误](#node-gyp_python_错误)
    *   [3.2 无法找到模块错误](#无法找到模块错误)
*   [4 其他资源](#其他资源)

## 安装

[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") 软件包 [nodejs](https://www.archlinux.org/packages/?name=nodejs)。

### 多版本需求

如果需要使用多个 [nodejs](https://www.archlinux.org/packages/?name=nodejs) 版本，可以使用 [NVM](https://github.com/creationix/nvm) (Node Version Manger). [nvm](https://aur.archlinux.org/packages/nvm/) 可以很方便的安装多个版本，并在版本间快速切换。命令很简单：

将下面命令加入 shell 的启动文件：

```
# Set up Node Version Manager
source /usr/share/nvm/init-nvm.sh

```

如果需要使用自定义的 nvm 目录：

```
# Set up Node Version Manager
export NVM_DIR="$HOME/.nvm"                            # You can change this if you want.
export NVM_SOURCE="/usr/share/nvm"                     # The AUR package installs it to here.
[ -s "$NVM_SOURCE/nvm.sh" ] && . "$NVM_SOURCE/nvm.sh"  # Load NVM

```

项目的 GitHub 页面包含使用文档，命令很简单：

```
$ nvm install 8.0
Downloading and installing node v8.0.0...
[..]

$ nvm use 8.0
Now using node v8.0.0 (npm v5.0.0)

```

使用 [nvm](https://aur.archlinux.org/packages/nvm/) 时，可以用 [[1]](https://www.archlinux.org/pacman/pacman.8.html#_transaction_options_apply_to_em_s_em_em_r_em_and_em_u_em%7Cpacman) 的 `--assume-installed nodejs=<version>` 参数避免安装系统提供的版本。

## Node Packaged Modules

[npm](https://www.npmjs.org/) 是官方的 node.js 包管理器，通过软件包 [npm](https://www.archlinux.org/packages/?name=npm) 进行安装。

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

默认情形下这个命令会将包安装至 `/usr/lib/node_modules/npm`，需要管理员权限.

作为个人用户级的安装您可以使用一个本地目录来配置 `npm` 。添加下列行到您的 shell 配置文件 (e.g. `.bash_profile`)。

```
PATH="$HOME/.node_modules/bin:$PATH"
export npm_config_prefix=~/.node_modules

```

不要忘记重新登录或读取新配置。

也可以在 `npm install` 时指定 `--prefix` 参数，但是不建议使用这个方式，因为需要每次安装全局软件包时都记得使用此参数。

```
$ npm -g install packageName --prefix ~/.node_modules

```

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

仅显示顶层树：

```
$ npm list --depth=0

```

要显示需要更新的过期软件包：

```
$ npm outdated

```

### 使用 pacman 管理包

一些 node.js 包可以在 [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") 找到，命名为 `nodejs-packageName` 格式。

## 问题处理

### node-gyp python 错误

有些使用 `node-gyp` 的工具不支持系统上的 Python 3，要解决这个问题，需要安装 [python2](https://www.archlinux.org/packages/?name=python2)并在 nvm 中设置:

```
$ npm config set python /usr/bin/python2

```

如果出现 **gyp WARN EACCES user "root" does not have permission to access the ... dir**，可以使用 *--unsafe-perm* 选项:

```
# npm install --unsafe-perm -g node-inspector

```

### 无法找到模块错误

从 npm 5.x.x. 开始，package-lock.json 会和 package.json 文件一起创建，如果两个文件引用了不同的版本，会出现冲突。临时解决方案是：

```
$ rm package-lock.json
$ npm install

```

nmp 5.1.0 或以上版本已经解决了此问题，请参考: [missing dependencies](https://github.com/npm/npm/pull/17508)

## 其他资源

更多关于 [nodejs](https://www.archlinux.org/packages/?name=nodejs) 和官方包管理器 [npm](https://www.npmjs.org/) 的使用信息您也许需要查询下列额外资源。

*   [NodeJs Documentation](http://nodejs.org/documentation/) Node 文档和教程。
*   [NodeJS Community](http://nodejs.org/community/)
*   [API Documentation](https://www.npmjs.org/doc/) 官方 `npm` API 文档
*   IRC channel #node.js on irc.freenode.net

中文社区

*   [v2ex NodeJS 节点](https://www.v2ex.com/go/nodejs) 开发者作品发布与开发探讨
*   [cnodejs.org](http://cnodejs.org/) Node.js 专业中文社区