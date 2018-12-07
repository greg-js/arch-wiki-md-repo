`drcom`作为中国大陆众多高校采用拨号上网的认证方式，某些学校不提供Linux客户端，或者不对各个发行版都支持. [dogcom](https://github.com/mchome/dogcom)通过分析drcom认证数据包，支持发送心跳包，保持握手.从而解决了校园网认证问题

## Contents

*   [1 安装](#安装)
*   [2 配置](#配置)
    *   [2.1 DHCP配置](#DHCP配置)
        *   [2.1.1 配置文件生成](#配置文件生成)
        *   [2.1.2 修改配置文件](#修改配置文件)
    *   [2.2 PPPOE配置](#PPPOE配置)
        *   [2.2.1 配置文件生成](#配置文件生成_2)
        *   [2.2.2 修改配置文件](#修改配置文件_2)
*   [3 启动](#启动)
*   [4 注意事项以及疑难解答](#注意事项以及疑难解答)

## 安装

[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") 软件包 [dogcom-git](https://aur.archlinux.org/packages/dogcom-git/).

## 配置

`drcom`分为`DHCP`和`PPPOE`二个版本，二个版本配置文件不同.

### DHCP配置

使用 [Wireshark](/index.php/Wireshark "Wireshark") 在官方客户端登录前开始截包，做一次完整的截包动作然后登出，保存为 `wireshark` 截包文件, 比如 `dr.pcapng` (扩展名为pcapng).

##### 配置文件生成

下载[配置文件生成器](https://raw.githubusercontent.com/drcoms/generic/master/drcom_d_config.py)将其与第一步的截包文件放到同一个目录下，并且将 `filename = 'dr.pcapng'` 中的 dr.pcapng 改为第一步保存的文件名。

#### 修改配置文件

进入命令提示符(或shell)进入 drcom_d_config.py 所在目录，输入 `python drcom_d_config.py > config.txt` ，打开 `config.txt` 根据提示，将如下段落拷贝到 `/etc/drcom.d/dhcp.conf`。

```
server = '172.17.254.6'
username='hahahahaha'
password=
CONTROLCHECKSTATUS = '\x20'
ADAPTERNUM = '\x01'
host_ip = '172.17.1.1'
IPDOG = '\x01'
host_name = 'DRCOMFUCKER'
PRIMARY_DNS = '114.114.114.114'
dhcp_server = '0.0.0.0'
AUTH_VERSION = '\x0f\x00'
mac = 0x28d244090e15
host_os = 'WINDIAOS'
KEEP_ALIVE_VERSION = '\xd4\x02'

```

### PPPOE配置

##### 配置文件生成

抓包同上

下载 [p版配置生成器](https://raw.githubusercontent.com/drcoms/generic/master/drcom_p_config.py) , 将其与第一步的截包文件放到同一个目录下，并且将 `filename = 'dr.pcapng'` 中的 drp.pcapng 改为第一步保存的文件名

#### 修改配置文件

进入命令提示符(或shell)进入 drcom_p_config.py 所在目录，输入 `python drcom_p_config.py > config.txt` ，打开 `config.txt` 将类似

```
server = '1.1.1.1'
pppoe_flag = '\x1d'
keep_alive2_flag = '\xd8'

```

的输出覆盖 `/etc/dogcom.d/pppoe.conf`

## 启动

请启动 `dogcom-d.service` `DHCP`认证方式或 `dogcom-p.service` 服务。

关于`systemd`用法请参阅{{Systemd|systemd}页面。

## 注意事项以及疑难解答

更多配置以及事项请见[github wiki](https://github.com/drcoms/drcom-generic/wiki)页面