## Contents

*   [1 下载链接：](#.E4.B8.8B.E8.BD.BD.E9.93.BE.E6.8E.A5.EF.BC.9A)
*   [2 主要特性](#.E4.B8.BB.E8.A6.81.E7.89.B9.E6.80.A7)
*   [3 XX-Net不是匿名工具](#XX-Net.E4.B8.8D.E6.98.AF.E5.8C.BF.E5.90.8D.E5.B7.A5.E5.85.B7)
*   [4 平台支持情况](#.E5.B9.B3.E5.8F.B0.E6.94.AF.E6.8C.81.E6.83.85.E5.86.B5)
*   [5 链接](#.E9.93.BE.E6.8E.A5)
*   [6 使用方法](#.E4.BD.BF.E7.94.A8.E6.96.B9.E6.B3.95)
*   [7 感谢](#.E6.84.9F.E8.B0.A2)
*   [8 如何帮助项目](#.E5.A6.82.E4.BD.95.E5.B8.AE.E5.8A.A9.E9.A1.B9.E7.9B.AE)
*   [9 附图](#.E9.99.84.E5.9B.BE)
*   [10 集成XX-Net的项目](#.E9.9B.86.E6.88.90XX-Net.E7.9A.84.E9.A1.B9.E7.9B.AE)

## 下载链接：

```
 测试版： [https://codeload.github.com/XX-net/XX-Net/zip/2.0.6](https://codeload.github.com/XX-net/XX-Net/zip/2.0.6)

```

```
 稳定版： [https://codeload.github.com/XX-net/XX-Net/zip/2.0.6](https://codeload.github.com/XX-net/XX-Net/zip/2.0.6)

```

```
 (1.13.6 之前的用户，请重新部署服务端)

```

```
 版本历史和说明： [https://github.com/XX-net/XX-Net/releases](https://github.com/XX-net/XX-Net/releases)

```

## 主要特性

```
  .大量改良过的GoAgent 稳定快速
  .Web界面，傻瓜易用
  .内置了公共 appid, 方便新手
  .自动导入证书，减少大量手动工作
  .可设置开机启动
  .支持自动升级，保留辛苦找到的ip资源

```

## XX-Net不是匿名工具

详情请看： [https://github.com/XX-net/XX-Net/wiki/Anonymous-and-Security](https://github.com/XX-net/XX-Net/wiki/Anonymous-and-Security)

## 平台支持情况

```
   Windows XP （需要 tcpip.sys 补丁, 比如用 tcp-z）
   Win7/8/10
   Ubuntu （不显示系统托盘）
   Debian （debian 8 php_proxy无法工作）
   Mac OS X(10.7; 10.8; 10.9; 10.10)

```

## 链接

*   [https://github.com/XX-net/XX-Net/issues](https://github.com/XX-net/XX-Net/issues) 问题报告
*   [https://groups.google.com/forum/#!forum/xx-net](https://groups.google.com/forum/#!forum/xx-net) 讨论群
*   Email:xxnet.dev at gmail.com

## 使用方法

```
   Windows下, 双击 start.lnk/start.vbs
       启动弹出浏览器： 访问 [http://localhost:8085/](http://localhost:8085/)
       托盘图标：点击可弹出Web管理界面, 右键可显示常用功能菜单。
       Win7/8/10：提示请求管理员权限, 安装CA证书。请点击同意。
       推荐用Chrome浏览器, 安装SwichySharp, 可在swichysharp目录下找到插件和配置文件
       Firefox 需手动导入证书 data/gae_proxy/CA.crt 启动后生成
   Linux下, 执行 start.sh
       自动导入证书，需安装 libnss3-tools 包
       第一次启动, 请用sudo ./start.sh, 以安装CA证书
       配置http代理 localhost 8087, 勾选全部协议使用这个代理。 推荐Chrome + SwitchyOmega
   Mac下，双击 start.command
       会自动导入证书，如果还有提示非安全连接，请手动导入data/gae_proxy/CA.crt证书
       命令行启动方式：./start.sh 推荐Chrome + SwitchyOmega
   服务端
       协议采用3.3的版本，请重新部署服务端，服务端兼容3.1.x/3.2.x的客户端
       虽然系统内置了公共appid, 还是建议部署自己的appid，公共appid限制看视频

```

## 感谢

```
   GoAgent
   GoGoTest
   goagentfindip
   checkgoogleip

```

## 如何帮助项目

[如何帮助项目](https://github.com/XX-net/XX-Net/wiki/How-to-contribute)

## 附图

## 集成XX-Net的项目

```
   ChromeGAE 主页：[http://www.ccav1.com/chromegae](http://www.ccav1.com/chromegae) 集成Google Chrome和XX-Net的自动翻墙浏览器 维护人：Yanu
   plusburg 主页：[https://github.com/Plusburg/Plusburg](https://github.com/Plusburg/Plusburg) 集成XX-Net的启动光盘镜像
   appifed-xx-net [https://github.com/binarydist/appified-xx-net](https://github.com/binarydist/appified-xx-net) Mac OSX 环境下，变成一个标准的app

```