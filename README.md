这是一个用于安卓逆向及自动化的辅助框架，它以编程化的接口大幅减少你的手动操作，你将不再需要关心琐碎的问题。通过它，你可以获得：

* 零依赖，只需 root 即可。
* 极其简单的调用，封装了大量常用接口，你只需要会写 Python。
* 极高的兼容性，覆盖了常用的安卓架构，支持主流游戏模拟器以及6.0-12的安卓版本。
* 自动化操作你的手机，你将可以通过类似 selenium、appium 的方式对被测试应用进行点击滑动等操作。
* 设置代理或者VPN实现对设备地址的切换来模拟网络环境的变化。
* 没有复杂的安装配置过程，一条命令即可完成框架的启动。
* 脱离 USB 数据线，启动后即可断开 USB 数据传输。


## 超完备一键抓包

![抓包动图演示](image/mitm.gif)

## 通过代码自动化

![自动化动图演示](image/automation.gif)

## 远程桌面连接

![远程桌面动图演示](image/lamda.gif)

如果你希望继续看下去，请先确保：手边有一台已经 root 且运行内存 **>= 3GB**，可用存储空间 **>=1GB** 的安卓设备或者安卓模拟器（推荐使用最新版**夜神**，**雷电**，**逍遥**模拟器，或者 AVD[Android Studio Virtual Device, 非 Google APIs 系统]）。**不完全支持** 网易 Mumu，**不支持**腾讯手游助手，蓝叠以及任何安卓内虚拟如 VMOS，等），对于真机，推荐运行最接近原生系统的设备如谷歌系、一加、安卓开发板等，或系统仅经过轻度改造的设备。目前**可能**不能在蓝绿厂/华为/小米类高度改造的安卓系统上正常运行，如果你只有此类品牌设备，建议使用模拟器。

* 支持安卓 6.0 - 12（边缘版本未经完整测试）。
* 支持通信加密
* 支持标准游戏模拟器，AVD及真机，(arm/arm64/x86/x86_64）全架构
* 内置 OpenVPN 可实现全局/非全局的 VPN
* 内置 http/socks5 代理，可实现设置系统级别/单个应用级别的代理
* 支持 OpenVPN 与代理共存
* 可通过接口轻松设置中间人证书，配合 http/socks5 代理实现中间人流量分析
* UI自动化，通过接口实现自动化操作
* 设备状态/资源消耗读取
* 大文件上传下载
* 接口锁
* 唤起APP任意 Activity
* 前后台运行脚本，授予撤销APP权限等
* 系统配置/属性读取修改
* WIFI 相关功能
* selinux 相关接口
* 内置 frida, IDA 7.5 server 等工具
* 可使用 ssh 登录设备
* 支持 crontab 定时任务
* 内置 Python3.9 及部分常用模块
* WIFI 远程桌面（web）

## 免责声明及条款

为了下载使用由 rev1si0n (账号 github.com/rev1si0n)（以下简称“本人”）个人开发的软件 lamda ，您应当阅读并遵守《用户使用协议》（以下简称“本协议”）。请您务必审慎阅读、充分理解各条款内容，特别是免除或者限制责任的条款，并选择接受或不接受；除非您已阅读并接受本协议所有条款，否则您将无权下载、安装或使用本软件及相关服务。您的下载、安装、使用、获取账号、登录等行为即视为您已阅读并同意受到上述协议的约束；若您需要获得本服务，您（以下称"用户"）应当同意本协议的全部条款并按照页面上的提示完成全部申请使用程序。您可以在本文档的相同目录找到 [DISCLAIMER.TXT](DISCLAIMER.TXT)，或者点此 [免责声明](DISCLAIMER.TXT) 查阅。

## 前言

文档目前只是介绍了基本使用，请配合下方示例手动输入语句辅助理解。如果你使用的是 Windows，附带的任何示例代码/命令可能在你的系统上不会正常工作(但是不包括客户端库)，建议在 Linux 或者 Mac 系统上操作文档及样例中的代码。

**请勿在自用手机上运行（请确保阅读三遍）**，暂未开源但绝无后门，请放心使用。

> 问题反馈及功能建议

因为安卓被各种设备广泛使用，无法保证百分百的兼容性，可能会有运行异常等各种未知情况，出现的异常情况包括：无故重启，APP经常崩溃，触摸失效或无故乱动等等，冻屏等情况。如果经常遇到，建议暂时停止使用。
点此 [报告问题/建议](https://github.com/rev1si0n/lamda/issues/new)，请详细描述。虽然此文档个人认为已经用足够简单的方法描述，但是无法保证所有人都在同一水平，在使用前，你需要了解基本的 adb 命令以及有熟练的 Python 编写能力。

## 安装

> 分为客户端以及服务端，客户端主要是Python相关库及接口，服务端则是运行在设备上的服务。

## 注意事项

此框架主要设计在纯净 root 的设备上运行，任何其他 root 类框架及功能都有可能引起冲突发生不正常的表现
最理想的环境是你仅仅刚刚 root（举个例子，新建的夜神模拟器，自带 root 的 lineageos 等，或者使用 magisk/supersu 刚 root 且未安装任何框架或者插件），在进行服务端启动前，请务必确保：

* 必须关闭 magisk hide
* 必须关闭 frida-server
* 建议关闭 xposed/magisk 插件
* 确认完毕重启设备

并且不会在启动后启用任何上述任何标记为`必须`的条目。

> 无故重启/崩溃问题自查

如果你在安卓设备上启动 lamda 后，设备多次出现无故重启或者出现应用崩溃的情况，
请在启动 lamda **之前**，在当前 shell 执行命令
```bash
export lamda_crash_system=1
```
这种情况多数是由 frida 导致的，这将禁用掉 frida 一些功能，也意味着你将无法正常使用内置的 frida。
但是将保证你可以使用大部分其他的内置接口。
仅在出现多次重启的情况下设置此变量，否则请勿设置（多次代表十五分钟内出现 >=3 次重启/崩溃情况）。

### 我不想听一句废话，只想快速看看怎么样

这是没有一句废话的快速安装过程，如果你想看详细的废话，请继续看下一节。
或者，如果你看不懂下一节的废话，请直接套用这几条命令。

```bash
# 直接复制粘贴到CMD/终端里按下回车
pip3 install -U lamda -i https://mirrors.ustc.edu.cn/pypi/web/simple
adb shell getprop ro.product.cpu.abi
# 看输出什么，输出 arm64-v8a 就用
# arm64-v8a.tar.gz-install.sh
# 输出 x86 就用
# x86.tar.gz-install.sh
adb push arm64-v8a.tar.gz-install.sh /data/local/tmp
adb shell
su
cd  /data/local/tmp
sh arm64-v8a.tar.gz-install.sh
# 无法保证所有机器都能正确执行此 install.sh
# 部分设备会发生脚本被 Killed 的情况，如果未能正确启动
# 请继续尝试下方手动安装方法
#
# 好了，现在看下面的 开始 章节
```

### 客户端安装

> 通过PIP源直接安装

请使用 3.6 - 3.10 版本的 Python

```bash
pip3 install -U lamda
# 即可
#
# 如果你需要使用内置 frida，为确保版本兼容请使用下列方法安装
# 这并不是必选项，不需要请跳过（你可能需要加入 --force-reinstall 选项来确保安装成功）
# 你可能需要外网访问才能安装 frida，否则有几率会卡住许久(~10分钟)或安装失败
# 如果你不需要 frida，请不要使用下面这条命令安装
pip3 install -U 'lamda[frida]'
```

### 服务端安装及启动

安装前，请先选择合适的架构，可以通过 adb shell 命令 `getprop ro.product.cpu.abi` 来获取当前的系统架构。
正常情况下，对于现时代的手机，可以直接选择 `arm64-v8a` 版本，而对于模拟器如雷电，你会在新建模拟器时选择32或64位版本的安卓系统，
32位模拟器系统对应 `x86`，64位则对应 `x86_64`，正常情况下，雷电模拟器默认创建的为基于 `x86` 的安卓 7.0 系统。

现在，从 `release` 页面 [rev1si0n/lamda/releases](https://github.com/rev1si0n/lamda/releases)
下载对应架构的安装文件。假设你已经从上文得知你的手机/设备架构为 `arm64-v8a`，那么在此页面点击
`arm64-v8a.tar.gz-install.sh` 以及 `arm64-v8a.tar.gz` 两个文件的链接来下载到本地。

> `arm64-v8a.tar.gz-install.sh` 是整合了的安装脚本，它在自身打包了 `arm64-v8a.tar.gz` 以及以及用于解压此安装包的 `busybox`。
> 用它安装是最简便以及通用的，但仍无法保证各版本安卓的差异性导致可能的安装失败。所以，下面将会介绍两种安装方法，推荐第一种，第二种则是
> 第一种完整的手动过程，你可以在第一种失败的情况下使用。

下载完成后，将设备连接到当前电脑并确保已连接 ADB，现在开始完成**前置条件**：

> 为了兼容各种设备的分区特性，在**每次设备启动后**，建议执行：

```bash
adb root
adb remount
```
真机应该会失败，无需关心是否报错。

> 如果使用的是 AVD (Android Studio Virtual Device)，请使用这种方法

请使用如下命令启动虚拟设备

```bash
# Pixel_4_API_29 为虚拟机ID，可以使用 emulator -list-avds 列出
emulator -avd Pixel_4_API_29 -writable-system
```

并在启动后执行

```bash
adb shell avbctl disable-verification
adb disable-verity
```

随后重启设备，继续执行

```bash
adb root
adb remount
```

> 开始安装

#### 方式 1

```bash
# /data/local/tmp 是标准服务安装路径，但并不是强制要求
# 你可以放到除了 /sdcard 之外任何具备可读写权限的文件夹
adb push arm64-v8a.tar.gz-install.sh /data/local/tmp
# 进入 adb shell
adb shell
# 输入 su 确保为 root 身份
su
# 切换到目录
cd  /data/local/tmp
# 执行安装脚本并启动（这将解包并启动服务）
sh arm64-v8a.tar.gz-install.sh
```

#### 方式 2

```bash
# /data/local/tmp 是标准服务安装路径，但并不是强制要求
# 你可以放到除了 /sdcard 之外任何具备可读写权限的文件夹
adb push arm64-v8a.tar.gz /data/local/tmp
```

完成后，进入 `adb shell`，解包文件：

```bash
# 你现在应该在 adb shell 内
cd /data/local/tmp
# 解包服务端文件
# 注意自带的 tar 命令可能因为不支持 z 选项导致解包失败，你可能需要使用 busybox tar 来解包
# 如果系统不附带 busybox 命令，请自行从 https://busybox.net/downloads/binaries/1.20.0 下载合适架构的版本
tar -xzf arm64-v8a.tar.gz
```

> 启动服务

注: 方式 1 安装后，会顺带启动服务，所以使用该方法**首次安装后**你无需执行下面的命令。

注: **并不是每次启动都需要 push 并安装**，上面方式1,2描述的过程只需首次执行即可，但是
下面的过程则需要每次设备重启后执行。

进入 adb shell，并切换为 `su` root 身份，执行：

```bash
# 你现在应该在 adb shell 内，切换到目录
cd /data/local/tmp
# 启动服务端
# 注意，arm64-v8a 这个目录根据平台不同名称也不同
# 如果你使用的是 x86 版本，那么这个目录名则是 x86/，你需要对命令做相应修改
sh arm64-v8a/bin/launch.sh
# 如果你想要启用加密传输
# 请先使用 tools/ 中的 cert.sh 来生成 lamda.pem 证书
# 将其push到设备例如 /data/local/tmp/lamda.pem
# 并将其属主及权限设置为 root 以及 600 (chown root:root lamda.pem; chmod 600 lamda.pem)
# 并使用以下命令启动
sh arm64-v8a/bin/launch.sh --certificate=/data/local/tmp/lamda.pem
# 这将加密任何通过 lamda 客户端产生的通信流量
# 但不包括 webui 例如通过浏览器远程桌面的功能
```

静待退出，随即关闭终端，至此服务启动完成。

**注意**：所有功能启动完成**可能**需要**三分钟**左右，
启动期间使用接口客户端可能引发 `ServiceUnavailable` 异常。请耐心等待。
但是如果在启动完成后的使用过程中频繁遇到 `ServiceUnavailable`，
或者在执行启动或使用过程中多次遇到设备黑屏/重启以及非配置原因导致的机器卡顿等类似情况，
请停止使用并反馈该问题。

## 关闭 lamda 服务

如果想使用接口关闭服务请参照下方 `关机重启/关闭服务` 章节。

当然，考虑到你可能不方便使用接口，你也可以使用以下命令来使 lamda 服务端退出。
你应该使用以下命令结束（确保以 su/root 身份执行命令）
注意请勿直接 kill -9 结束服务端，可能会产生僵尸进程。

```bash
kill -SIGUSR2 $(cat /data/usr/lamda.pid)
```

如无必要请勿频繁启动关闭。

## 开始

设备上的 `65000` 端口为本服务的标准公用端口，可能需要记住，但是大部分情况下，你不需要显式提供此端口号。
下面请先在 WLAN 设置中取得**当前设备的IP地址**，你也可以通过 tools/ 目录里的工具来列出当前网络中的所有设备及IP，
下面将会一直**假设**设备的IP为 `192.168.0.2`。

> 在网页端控制手机。

在浏览器中打开 `http://192.168.0.2:65000` 可进入 web 远程桌面，你可以在此操作设备以及通过该界面的root模拟终端执行命令。
不支持多人访问，不保证兼容所有浏览器，建议使用 Chrome。

注：如果启动服务端时指定了证书，打开页面时会要求输入密码，你可以在证书最后一行找到这个32位的密码。

## 连接设备

> 现在，将配合 lamda 库进行介绍，在开始前，请先确保你已经根据上文 `客户端安装` 章节正确安装了客户端库。

建议顺带翻看客户端的源码，并不是需要理解，仅仅是让你能了解到底有什么参数可以使用。

```python
from lamda.client import *

d = Device("192.168.0.2")
# 如果在服务端启用了 certificate 请这样连接
d = Device("192.168.0.2", certificate="/path/to/lamda.pem")
```

或者，直接执行命令
```bash
# 注意这个DEVICE参数是IP，自行替换
python3 -m lamda.client -device 192.168.0.2
# 随后可以直接在此 shell 中输入下方语句
```

> 下文中的 `d` 将始终假设为 `d = Device("192.168.0.2")` 实例。

## 设置 http/socks5 代理

只支持 http 以及 socks5 代理，不支持 IPV6

> 请认真阅读以下内容

```python
profile = GproxyProfile()
# socks5 代理则为 GproxyType.SOCKS5
profile.type = GproxyType.HTTP_CONNECT
# 如果你需要重定向 DNS 查询到 114.114.114.114
# 注意此 DNS 是系统全局的，系统发出的所有DNS将会被转发
# 如果是与OpenVPN共存的情况，不要设置为OpenVPN的内网DNS服务器，否则可能会导致彻底断网
# 去掉 nameserver 配置行将使用系统默认 DNS
#
# 为什么有此选项：你可以修改一些应用的 dns 域名解析
profile.nameserver = "114.114.114.114"
profile.host = "代理服务器地址"
profile.port = 代理服务器端口

# 如果这个代理服务器需要登录信息（注意：如果没有，请置为 None 或者删除这两行）
profile.password = "代理服务器登录密码"
profile.login = "代理服务器登录用户"

# socks5 模式支持 udp 代理，但是 http 代理并不支持
# 因为 udp 多数情况下并不会被代理，所以禁用 udp 流量是一个不错的选择
# 当 drop_udp 为 True 时，应用/系统的 UDP 流量将会被屏蔽，默认为 False
profile.drop_udp = False

# 本地流量是否需要*不经过*代理，如果为 True，本地流量
# 如 192.168.x.x 10.x.x.x 等路由器内网网段的流量将不会经过代理，默认为 False
profile.bypass_local_subnet = True

# 是否需要代理 udp 流量
# 注意，http 代理服务器不支持代理 udp 协议，开启此选项必须使用 socks5 作为代理服务器
# (GproxyType.SOCKS5)，且 socks5 代理服务器必须开启 udp 代理模式（且与tcp同端口）
# 当你使用 http 代理或者 drop_udp 选项为 True，此设置将会被忽略
profile.udp_proxy = False

# 如果需要仅对特定应用使用代理（例如安卓浏览器，如果是全局则删除这两行）
app = d.application("com.android.browser")
profile.application.set(app)

#     注意事项以及提示：
# 设置代理后，正在运行的应用是不会立即使用设置的代理的
# 因为这些应用在设置代理之前就已经完成了 tcp 连接的建立
# 所以，需要你手动关闭应用并启动，应用才会通过代理建立连接
# 也就是说，如果你是做中间人流量分析，那设置代理后
# 你需要关闭应用再重新打开才会看到应用的请求
#
# 注：本机的 DNS 流量始终不会经过代理

# 启动代理
d.start_gproxy(profile)
# 关闭代理
d.stop_gproxy()
```

> 此处附上一个简单无认证的 [Danted sock5 代理服务](https://www.inet.no/dante/index.html) 配置

```
internal: 0.0.0.0 port = 1080
external: 出网接口名称

clientmethod: none
socksmethod: none

client pass {
    from: 0.0.0.0/0 to: 0.0.0.0/0
	log: error
}

socks pass {
    from: 0.0.0.0/0 to: 0.0.0.0/0
    command: bind connect udpassociate bindreply udpreply
    log: error
}
```

## 中间人流量分析（MITM）

请先确保你已经准备好 fiddler,mitmproxy给你的证书，对于 mitmproxy，
给你的证书为 pem 格式如下示例。而对于 fiddler，则可能是 crt 格式，直接将该文件
作为参数提供即可无需关心转换问题。

为了避免浪费不必要的时间，在这里推荐使用 `mitmproxy`，
如果你使用的是 `Charles` 等，我无法确保你可以一次性完成设置，
因为此类应用配置项目较为复杂且你可能需要理解各种代理类型才能正确配置SSL中间人，
如果你一定要使用，建议使用 Charles 的 socks5 作为代理协议。

```python
# 以 mitmproxy 为例，使用如下代码安装证书
d.install_ca_certificate("~/.mitmproxy/mitmproxy-ca-cert.pem")
# 使用如下代码卸载证书（如不常变化不建议频繁安装卸载）
d.uninstall_ca_certificate("~/.mitmproxy/mitmproxy-ca-cert.pem")
# 此证书安装接口是通用的，你可以用它安装任何应用要求你安装的证书
# 你同样可以用其安装 Fiddler/Charles 要求你安装的证书
# 只需要提供文件即可
```

接着，看 `设置 http/socks5 代理` 节，将代理设置为中间人应用监听的地址即可。
按照流程完成后如果没有截获到流量请参加设置代理部分的**特别注意**。

## 设置 OpenVPN

> 此 OpenVPN 只支持使用证书登录，可以与 http/socks5 代理共存。
> 需要注意的是，部分配置项例如 all_traffic 可能会与服务器端配置存在关联，只有在服务器端配置为
> 非全局 VPN (只VPN特定网段）下才会生效。只包含VPN的主要功能，除了 `DNS` 配置，暂无法应用服务端推送的其他配置信息。
> 这些配置包括但不限于 PAC 代理，http 代理配置等。

```python
profile = OpenVPNProfile()

# 是否全局 VPN，为 False 时仅路由服务器端推送的特定网段
profile.all_traffic  = True
# 服务器端开启的连接协议 (或者为 OpenVPNProto.TCP)
profile.proto        = OpenVPNProto.UDP
profile.host         = "OpenVPN 服务器地址"
profile.port         = OpenVPN 服务器端口
# 服务器端通道加密方法
profile.cipher       = OpenVPNCipher.AES_256_CBC

profile.ca = """
-----BEGIN CERTIFICATE-----
服务端配置的 ca 证书
-----END CERTIFICATE-----
"""

profile.cert = """
-----BEGIN CERTIFICATE-----
客户端证书
-----END CERTIFICATE-----
"""

profile.key = """
-----BEGIN PRIVATE KEY-----
客户端私钥
-----END PRIVATE KEY-----
"""

# 启动 OpenVPN
d.start_openvpn(profile)
# 关闭 OpenVPN
d.stop_openvpn()
```

> 示例的 OpenVPN server 端配置文件（请勿直接复制，依据事实进行修改挑选）

服务端的搭建涉及到较多系统配置以及防火墙配置可能较为复杂，自行部署的话建议尽量使用公开的docker进行。
这里不会讲述如何搭建。

```
user nobody
group nogroup

topology subnet
server 192.168.168.0 255.255.255.0
proto udp
port 1233
dev tun
txqueuelen 1000
ncp-disable
cipher AES-256-CBC

# 注意你可能会遇到客户端不断重连的状况
# 因为安卓设备在息屏状态下，网络可能会由于省电措施中断
# 你可能会需要更改此处配置但是有利弊
keepalive 60 300

ca         /etc/openvpn/server/keys/ca.crt
dh         /etc/openvpn/server/keys/dh2048.pem
cert       /etc/openvpn/server/keys/ovpn.crt
key        /etc/openvpn/server/keys/ovpn.key

client-to-client

# 去掉注释为始终全局，即代表上文的 all_traffic 配置即使设为 False 也相当于 True
# 所以这里直接注释掉此配置（不要加入此配置）
#push "redirect-gateway def1 bypass-dhcp"

push "route x.x.x.x 255.255.255.0"

# 始终只会使用第一个 DNS，其他将会被忽略
push "dhcp-option DNS 114.114.114.114"
push "dhcp-option DNS 114.114.115.115"

# *** 不支持 *** PROXY_AUTO_CONFIG_URL push
#push "dhcp-option PROXY_AUTO_CONFIG_URL https://example.com/proxy.pac"

# 同一个证书是否允许多个客户端使用
duplicate-cn
verb 4
```

## 如何连接内置 frida

> 非逆向工作无需阅读此节

注意，启动本框架前后，**请勿**再次自行启动任何 frida-server，框架已内置，你只需要通过下列代码使用即可。

1. 通过代码连接

```python
# 使用框架时的做法
device = d.frida
device.enumerate_processes()
```

等效于

```python
# 通常做法
manager = frida.get_device_manager()
device = manager.add_remote_device("192.168.0.2:65000")
device.enumerate_processes()
```

2. 通过命令行方式使用
```bash
# 如果你在服务端启动时指定了 certificate 选项，请注意在此加入此参数
frida -H 192.168.0.2:65000 -f com.android.settings
```

即可。

## 使用自带的 crontab (定时任务)

内置了用于执行定时任务的 cron 服务，这样你可以在设备上定期执行一些脚本，所有规则都将以 root 身份执行

> 此功能需要你会编写 crontab 规则以及基础的 linux 命令行编辑文件的能力

注意这与你在 linux 使用 crontab 并不相同，在 linux 正常使用 `crontab -e` 命令
来编辑任务，但是框架并未提供此命令，你需要直接编辑文件来写入规则（道理是相同的，都是编辑文件而已）

现在，请打开 web 控制台或者连接设备的 ssh，执行命令 `cd` 来切换到家目录。
此时家目录中有个名为 crontab 的文件夹。执行命令 `busybox vi crontab/jobs`，你将进入编辑文件，在英文输入模式下按下字母 `i`，随后写下相关规则，并按下 `ESC`，`SHIFT` + `:`，输入 `wq` 并按下回车来保存。你可以在这个 jobs 文件中写入多行，同样，你也可以在这个文件夹下创建其他名字的规则文件。

如果你还是不懂怎么编辑，请在电脑编辑完成后使用adb转移到此目录。

> 一些规则示例

```
@reboot      echo 每次框架启动/重载(reload)时执行
0 */1 * * *  echo 每一小时执行
* * * * *    echo 每一分钟执行
0 8 * * *    echo 每天八点执行
```

## 系统属性 (get/setprop)

> 设置/读取系统属性

```python
# 获取 ro.secure 的值
d.getprop("ro.secure")

# 设置 ro.secure 的值
d.setprop("ro.secure", "0")
```

## 系统设置 (settings)

> 设置/读取安卓系统设置

```python
settings = d.stub("Settings")

# 示例：获取及修改屏幕亮度
settings.get_system("screen_brightness")
settings.put_system("screen_brightness", "5")

# 示例：关闭开发者选项
settings.get_global("development_settings_enabled")
settings.put_global("development_settings_enabled", "0")

# 示例
settings.get_secure("screensaver_enabled")
settings.put_secure("screensaver_enabled", "0)
```

## 设备状态

> 获取设备运行信息
```python
status = d.stub("Status")

# 获取设备启动时间
status.get_boot_time()

# 获取设备磁盘使用情况
status.get_disk_usage(mountpoint="/data")

# 获取电池信息
status.get_battery_info()
# 获取CPU使用情况
status.get_cpu_info()
# 获取总体磁盘读写情况
status.get_overall_disk_io_info()
# 获取用户数据磁盘的读写情况 (userdata)
status.get_userdata_disk_io_info()
# 获取总体网络收发情况
status.get_overall_net_io_info()
# 获取 wlan0 接口的网络收发情况
status.get_net_io_info("wlan0")
# 获取内存使用情况
status.get_mem_info()
```

## 在设备上执行命令

> 在设备后台，前台执行 shell 脚本/命令

```python
shell = d.stub("Shell")
# 执行前台脚本（执行时间短的脚本）
shell.execute_script("pwd")

# 执行后台脚本（执行时间长的脚本）
# 对于后台脚本，因考虑可能用户写出死循环脚本无限输出导致内存占满等问题
# 暂时无法获知其执行结果
ID = shell.execute_background_script("sleep 100; exit 0;")
# 检查后台脚本是否结束
shell.is_background_script_finished(ID)
# 强制结束后台脚本
shell.kill_background_script(ID)
```

## 使系统可调试

如果你需要使用JEB，IDA等动态分析，你可能需要设置此标志才能进行，当然也内置了这个功能，你可以这么做而无需永久修改 `ro.debuggable`。
但是记住，这个接口你并不是一定需要调用，仅当你看到任何文章/教程让你修改 `ro.debuggable` 时使用。

注意：调用此接口成功后，系统会自动重启，你可能仍需像首次启动时等待一段时间到本框架恢复

> 慎用，此功能可能不稳定且可能随时移除

```python
debug = d.stub("Debug")

r = debug.set_debuggable()
print (r)
```

## 启动 IDA 调试服务

> 内置了 IDA 7.5 服务端

```python
debug = d.stub("Debug")

# 启动 IDA 32 服务端（端口可自定义）
debug.start_ida(port=22032)
# 检查是否已启动
debug.is_ida_running()
# 关闭 IDA 32 服务端
debug.stop_ida()
# 如果调试的是64位程序，将方法名中的 ida 替换为 ida64 即可
# 例如
debug.start_ida64(port=22064)
#
# 如果需要自定义 ida-server 的环境变量例如 IDA_LIBC_PATH (同样适用于 start_ida)
debug.start_ida64(port=22064, IDA_LIBC_PATH="/apex/com.android.runtime/lib64/bionic/libc.so")
# 当你调试的目标程序是32位时使用 start_ida
# 否则使用 start_ida64
# 当你的设备系统为32位平台时，start_ida64 将会无效
```

## 开启 WIFI ADB

> 慎用，此功能可能不稳定且可能随时移除

```python
debug = d.stub("Debug")

# 启动设备 adb
# 此接口会同时将你当前主机的 adb 公钥安装到移动设备，也就是说不会再弹出ADB授权弹窗。
debug.start_android_debug_bridge()
# 启动后，你可以直接通过
# adb connect 192.168.0.2:65000 连接到设备
# 此时你可以执行任意 adb 命令。
# 你可以通过网络直接执行任意 adb forward/shell/pull/push 命令
# 类似于 WIFI ADB 的功能。
#
# 停止 adb 服务
debug.stop_android_debug_bridge()
# 检查是否启动
debug.is_android_debug_bridge_running()
```

## 文件操作

> 将文件上传至设备或从其下载文件（支持大文件）

```python
# 下载文件到本地
d.download_file("/data/local/tmp/设备上的文件.txt", "写入到的本地文件.txt")

# 上传文件到设备
# 会自动修改远程的文件权限信息为本地文件权限信息
# 即本地文件权限为 0755，那么上传到设备上的文件也为此权限
d.upload_file("本地文件路径.txt", "/data/local/tmp/上传到设备上的文件.txt")

# 删除设备上的文件
d.delete_file("/data/local/tmp/文件.txt")

# 修改设备上的文件权限
d.file_chmod("/data/local/tmp/文件.txt", mode=0o777)

# 获取设备上文件的信息
d.file_stat("/data/local/tmp/文件.txt")
```

## 关机重启/关闭服务

```python
# 关闭系统（等于关机）
d.shutdown()
# 重启系统（等于重启）
d.reboot()

# 关闭设备上运行的 lamda 服务
d.exit()
```


## 应用操作

> 列出系统上已安装的所有应用的ID

```python
d.enumerate_all_pkg_names()
```

> 列出设备上所有正在运行的应用

```python
d.enumerate_running_processes()
```

> 获取当前处于前台的应用

```python
d.current_application()

# 等价于
d.application(d.current_application().applicationId)

# 获取当前前台的 activity
d.current_application().activity
```

> 启动 Activity
```python
# 由于JSON标准，附加数据暂时只支持 boolean, int 以及 string 类型
d.start_activity(action="some", category="some", component="some",
                 extras={"boolean": False, "int": 1, "string": "me"})

# 例如：启动 设置 APP（当然这几乎等价于直接启动app）
d.start_activity(action="android.intent.action.MAIN",
                 category="android.intent.category.LAUNCHER",
                 component="com.android.settings/.Settings")

# 例如：进入证书设置
d.start_activity(action="com.android.settings.TRUSTED_CREDENTIALS")
```

> 授予/撤销 APP 权限

注意，你应在APP未启动时进行权限设置，在APP请求时调用并不会产生帮你点击允许的效果。

```python
app = d.application("com.my.app")

# 获取应用所有权限
app.permissions()
# 授予 READ_PHONE_STATE 权限
app.grant("android.permission.READ_PHONE_STATE", mode=GrantType.GRANT_ALLOW)
# 拒绝 READ_PHONE_STATE 权限
app.grant("android.permission.READ_PHONE_STATE", mode=GrantType.GRANT_DENY)
# 检查是否已授予权限
app.is_permission_granted("android.permission.READ_PHONE_STATE")
# 撤销已授予的权限
app.revoke("android.permission.READ_PHONE_STATE")
```

> 清除应用缓存，重置应用

```python
# 删除应用的缓存数据
app = d.application("com.my.app")
app.delete_cache()
# 重置应用数据
app.reset_data()
```

> 启动/停止应用

```python
app = d.application("com.my.app")

# 启动应用
app.start()
# 检查应用是否正在前台运行
app.is_foreground()
# 关闭应用
app.stop()
```

> 其他

```python
app = d.application("com.my.app")
# 获取应用信息
app.info()

# 检查应用是否已安装
app.is_installed()
# 卸载应用
app.uninstall()

# 查询启动该应用的 Activity
app.query_launch_activity()

# 启用应用
app.enable()
# 禁用应用
app.disable()
```

## WIFI操作

目前WIFI操作部分功能由于可能导致设备异常未实现，仅介绍部分实现的功能

```python
wifi = d.stub("Wifi")

# 获取wifi bssid,ssid ip 等相关信息
wifi.status()

# 获取黑名单中的所有 bssid
wifi.blacklist_get_all()

# 将bssid加入黑名单(将不会显示在wifi列表)
wifi.blacklist_add("3c:06:aa:8a:55:66")

# 清空所有黑名单
wifi.blacklist_clear()

# 执行 wifi 扫描
wifi.scan()

# 获取周边 wifi 扫描结果
wifi.scan_results()

# 获取当前wifi的mac地址
wifi.get_mac_addr()

# 获取 wifi 信号强度，链接速率
wifi.signal_poll()
```

## 基本UI操作

> 获取设备信息

```python
d.device_info()
```

> 息屏/亮屏相关

```python
# 息屏
d.sleep()
# 亮屏
d.wake_up()
# 屏幕是否点亮
d.is_screen_on()
# 屏幕是否已锁定
d.is_screen_locked()
```

> 剪切板

```python
d.set_clipboard("剪切板内容")

# 获取剪切板内容（不支持安卓10+）
d.get_clipboard()
```

> 物理按键

```python
# 此方法可使用如下17种按键
# KEY_BACK
# KEY_CAMERA
# KEY_CENTER
# KEY_DELETE
# KEY_DOWN
# KEY_ENTER
# KEY_HOME
# KEY_LEFT
# KEY_MENU
# KEY_POWER
# KEY_RECENT
# KEY_RIGHT
# KEY_SEARCH
# KEY_UP
# KEY_VOLUME_DOWN
# KEY_VOLUME_MUTE
# KEY_VOLUME_UP
d.press_key(Keys.KEY_BACK)

# 同时为了可以使用更多按键，也可以使用这个方法
d.press_keycode(KeyCodes.KEYCODE_CALL)
# 可使用的 KEYCODE 可以自行查看此文档
# https://developer.android.com/reference/android/view/KeyEvent#KEYCODE_0
```

> 屏幕截图

```python
quality = 60 # 截图质量，默认为全画质
d.take_screenshot(quality).save("screenshot.png")
# 截取屏幕上特定区域的图像
# Bound 的参数 top,left 等定义：

# top:     从距离屏幕顶部向下数 top 个像素
# bottom:  从距离屏幕顶部向下数 bottom 个像素
# left:    从距离屏幕左侧向右数 left 个像素
# right:   到距离屏幕左侧向右数 right 个像素

# 正常情况下 top 永远小于 bottom，left 永远小于 right
bound = Bound(top=50, bottom=80, left=50, right=80)
d.take_screenshot(quality, bound=bound).save("partial.png")
```

> 点击屏幕上的一个点

```python
d.click(Point(x=100, y=100))
```

> 点按点A并将其拖动到点B

```python
A = Point(x=100, y=100)
B = Point(x=500, y=500)

d.drag(A, B)
```

> 从点A滑动到点B

```python
A = Point(x=100, y=100)
B = Point(x=500, y=500)

d.swipe(A, B)
```

> 稍复杂的多点滑动（九宫格解锁）

```python
p1 = Point(x=100, y=100)
p2 = Point(x=500, y=500)
p3 = Point(x=200, y=200)

# 从点P1滑动到点P2随后滑动到点P3，可任意个点
d.swipe_points(p1, p2, p3)
```

> 打开通知栏/快捷设置栏

```python
d.open_notification()
d.open_quick_settings()
```

> 获取页面布局描述XML

```python
d.dump_window_hierarchy().getvalue()
```

> 等待界面布局停止刷新

```python
# 单位是毫秒，5*1000 代表5秒
d.wait_for_idle(5*1000)
```

## 进阶UI操作

> Selector

界面选择器，类似于网页，安卓的界面也可以通过选择器进行元素的选择。
在开始了解前，请先安装第三方的 [alibaba/web-editor](https://github.com/alibaba/web-editor)，你可以通过
```bash
pip3 install weditor
```
直接安装。

随后，在命令行输入 `weditor` 启动，你会自动跳转到相关页面，在顶部连接设备区域输入 `设备IP:65000` 并点击 CONNECT 进行连接。
注意，暂仅支持其UI审查功能，请不要使用右侧代码运行/实时等功能。

连接到设备后，点击 `Dump Hierarchy` 来获取当前界面布局，你可以将其想象成打开了开发者工具并得到DOM布局。

这样，你可以在左侧页面屏幕上选择你感兴趣的元素，在页面中部 `Selected Element` 区域将会显示其属性。
你可以将其中的大部分属性作为 Selector 的参数。

正常情况下，我们只会使用 `resourceId`, `clickable`, `text`, `description` 作为参数。
如果元素存在正常的 resourceId，优先使用其作为 Selector，即：`Selector(resourceId="com.android.systemui:id/mobile_signal_single")`。
对于无 resourceId，则会使用其 text，即：`Selector(text="点击进入")`，或者更模糊一点 `Selector(textContains="点击")`
description 与 text 同理，但是 description 用的会比较少。

当然，Selector 不止可以使用一个参数，你可以做其他组合，例如 `Selector(text="点击进入", clickable=True)`

所有常见的匹配参数：

```
text                    文本完全匹配
textContains            文本包含匹配
textStartsWith          文本起始匹配
className               类名匹配
description             描述完全匹配
descriptionContains     描述包含匹配
descriptionStartsWith   描述起始匹配
clickable               可以点击
longClickable           可以长按
scrollable              可滚动
resourceId              资源ID匹配
```

大部分情况下，你不会直接用到 `Selector`，但是间接使用无处不在。

> 元素操作

上文都是介绍了如何坐标点击这种随意性的东西，现在开始介绍如何操作固定目标元素。首先，你需要知道如何选定元素。

```python
# 选择界面上的包含文字 被测APP 的元素
element = d(textContains="被测APP")
# 当然，你不一定要这样赋值到 element，也可直接使用 d(textContains="被测APP")
```

好了，现在你知道了如何获取元素了，当然，这时并没有获取到，只是代表，你想要在当前界面操作这个元素，下面开始操作。


```python
# 我们现在假设，界面上这个 被测APP 是手机上被测APP的图标名称（图标下面的名称）。
element = d(textContains="被测APP")
# 是否存在该元素
element.exists()
# 点击该元素，不存在则会抛出异常
# Corner.COR_CENTER 代表点击该元素中心点，你可查看 COR_CENTER 定义获取其他可点击的位置
element.click(corner=Corner.COR_CENTER)

# 点击该元素，不存在不会抛出异常
element.click_exists(corner=Corner.COR_CENTER)

# 长按该元素，不存在则会抛出异常
element.long_click(corner=Corner.COR_CENTER)

# 获取元素信息
element.info()

# 获取元素的中心点坐标
element.info().bounds.center()

# 获取元素的左上点坐标
element.info().bounds.corner("top-left")

# 获取元素的高度
element.info().bounds.height

# 获取元素的宽度
element.info().bounds.width

# 获取元素个数
element.count()

# 等待元素出现，最多等待10秒
element.wait_for_exists(10*1000)

# 等待元素消失，最多等待10秒
element.wait_until_gone(10*1000)

# 获取该元素的截图（不是全屏，只是该元素）
# quality 为截图质量 1-100
element.take_screenshot(quality=60)

# 将此 APP 拖动归类到 购物 文件夹（依据实际情况修改）
element.drag_to(Selector(text="购物"))


############################
# 现在 element 改变了其意义，变为选择了输入框
############################

# 示例为：在一加搜索应用界面的搜索框输入 被测APP

# 注意，不要直接往看似输入框的地方输入文字，可能并无法输入
# 有些输入框需要点击一次才会进入真正的输入框，请使用此真正输入框的资源ID
element = d(resourceId="net.oneplus.launcher:id/search_all_apps")
element.set_text("被测APP")

# 获取输入的内容
element.get_text()

# 清空刚刚输入的内容
element.clear_text_field()

# 配合点击搜索，来完成一次类人的搜索操作。


# 滑动操作（列表上下滑动翻页）
# 注意，这些操作并不保证精度，下面这些方法正常情况下都并不需要选择器，
# 但是你可根据实际情况自行加入选择器

# 向上滑动， step 自行调整，越多会越慢，比较适合精度要求较高的滑动
d().swipe(direction=Direction.DIR_UP, step=32)
# 其他滑动方向：
#DIR_UP     向上滑动
#DIR_LEFT   向左滑动
#DIR_DOWN   向下滑动
#DIR_RIGHT  向右滑动

#########
# fling：甩动，即正常人滑动屏幕的行为，较快
#########
# 从上向下
d().fling_from_top_to_bottom()
# 从下往上
d().fling_from_bottom_to_top()
# 从左往右
d().fling_from_left_to_right()
# 从右往左
d().fling_from_right_to_left()

# 其他，一直向下/左右上滑，直到滑动到底
# 因为并不是一定可以滑动到底或者检测到滑动到底
# 所以 max_swipes 参数是必须的
d().fling_from_top_to_bottom_to_end(max_swipes=32)
d().fling_from_bottom_to_top_to_end(max_swipes=32)
d().fling_from_left_to_right_to_end(max_swipes=32)
d().fling_from_right_to_left_to_end(max_swipes=32)

#########
# scroll: 比较机械性的滑动
#########
step = 60
max_swipes = 32
# 从上往下滑动 step 步
d().scroll_from_top_to_bottom(step)
# 从下往上滑动 step 步
d().scroll_from_bottom_to_top(step)
# 从左往右滑动 step 步
d().scroll_from_left_to_right(step)
# 从右往左滑动 step 步
d().scroll_from_right_to_left(step)

# 其他，一直向下/左右上滑，直到滑动到底
# 同上文 fling 描述
d().scroll_from_top_to_bottom_to_end(max_swipes, step)
d().scroll_from_bottom_to_top_to_end(max_swipes, step)
d().scroll_from_left_to_right_to_end(max_swipes, step)
d().scroll_from_right_to_left_to_end(max_swipes, step)
```

> 监视器

监视器用来监听界面变化并在满足条件时执行设定的操作（点击元素或者按键），这可能对性能或者需要人工介入时产生影响，所以请谨慎使用，默认未开启。

```python
# 启动监视器循环
d.set_watcher_loop_enabled(True)

# 获取监视器是否已启动
d.get_watcher_loop_enabled()

# 移除系统中应用的所有 watcher，建议每次使用前都执行防止前面任务注册的未删除影响正常处理流程
d.remove_all_watchers()

# 获取系统中所有已应用的 watcher 名称列表
d.get_applied_watchers()

# 彻底移除一个 watcher
d.remove_watcher(name)

# 应用watcher到系统中（当 watcher_loop 启动，此watcher将会生效）
d.set_watcher_enabled(name, True)
# 取消应用
d.set_watcher_enabled(name, False)

# 获取此 watcher 是否应用
d.get_watcher_enabled(name)
```

> 监视系统界面出现某个元素的次数

```python
# 做一些测试前的清理，当然，并不是每 register 一个就需要这样
# 只是为了确保测试过程不被干扰
d.remove_all_watchers()
d.set_watcher_loop_enabled(True)

# 应用监视界面出现 好的 的次数
# 第二个参数为数组，可以给多个 Selector 表示条件都满足才会记录
# 但是不建议超过三个
d.register_none_op_watcher("RecordElementAppearTimes", [Selector(textContains="好的")])
d.set_watcher_enabled("RecordElementAppearTimes", True)

# ... 做满足条件的操作

# 获取记录的次数
d.get_watcher_triggered_count("RecordElementAppearTimes")

# 重置记录的次数
d.reset_watcher_triggered_count("RecordElementAppearTimes")

# 移除
d.remove_watcher("RecordElementAppearTimes")
```


> 当界面出现匹配元素时点击某个元素

```python
# 做一些测试前的清理，当然，并不是每 register 一个就需要这样
# 只是为了确保测试过程不被干扰
d.remove_all_watchers()
d.set_watcher_loop_enabled(True)

# 示例为，当APP启动后出现用户协议时，自动点击同意
# 第二个参数为数组，可以给多个 Selector 表示条件都满足才会点击
# 但是不建议超过三个
d.register_click_target_selector_watcher("ClickAcceptWhenShowAggrement", [Selector(textContains="用户协议")],
                                         Selector(textContains="同意", clickable=True))
d.set_watcher_enabled("ClickAcceptWhenShowAggrement", True)

# ... 做满足条件的操作

# 移除
d.remove_watcher("ClickAcceptWhenShowAggrement")
```


> 当界面出现匹配元素时点击物理按键

```python
# 做一些测试前的清理，当然，并不是每 register 一个就需要这样
# 只是为了确保测试过程不被干扰
d.remove_all_watchers()
d.set_watcher_loop_enabled(True)

# 示例为，当界面存在 个人中心 时，按下HOME键回到启动屏幕
# 第二个参数为数组，可以给多个 Selector 表示条件都满足才会点击
# 但是不建议超过三个
d.register_press_key_watcher("PressBackWhenHomePageShows", [Selector(textContains="个人中心")], Keys.KEY_HOME)
d.set_watcher_enabled("PressBackWhenHomePageShows", True)

# ... 做满足条件的操作

# 移除
d.remove_watcher("PressBackWhenHomePageShows")
```

## 接口锁

这里的基本功能让你可以锁定接口只能为当前 Device 实例使用。

```python
# 获得锁，此锁将在60秒后被自动释放，其他客户端将可以获得锁，你可以更改此时间
# 但是，如果改得太高因为异常脚本退出，你将近乎永远无法连接设备，你可能需要进行重启
# 此获得锁接口可重入，重入时等价于 _refresh_lock，建议只调用一次
d._acquire_lock(leaseTime=60)
# 刷新锁，每次调用后将锁过期时间设为此 leaseTime
# 做定期调用来保持设备锁定
d._refresh_lock(leaseTime=60)
# 释放锁，其他客户端将可以获得锁
d._release_lock()
```

## 如何使用内部终端

这里的内部终端，指的是你通过 web 远程桌面或者 ssh 连接的终端，里面内置了一些命令以及Python模块，你可以
直接在里面执行一些操作或者运行一些 Python 代码。

现在假设你已经打开了 web 远程桌面，你应该已经在页面上看到了一个 linux 终端。
执行命令 `cd` 可以切换到家目录（默认为 `/data/usr`），这是你的工作区，你可以在此存储文件，框架本身也会在此存储文件。

* python           (Python)
* strace           (syscall trace)
* ltrace           (libcall trace)
* curl             (cURL)
* fsmon            (文件访问监控)
* iperf3           (网络性能测试)
* nano             (文件编辑器)
* ncdu             (查找磁盘文件占用)
* socat            (网络工具)
* sqlite3          (读取 SQLite 数据库，支持 cipher 版本)
* tcpdump          (流量分析)
* busybox          (命令集合)
* MemDumper        (https://github.com/kp7742/MemDumper)
* frida            (frida-tools)
* frida-ps         (frida-tools)
* frida-trace      (frida-tools)
* frida-ls-devices (frida-tools)
* frida-discover   (frida-tools)
* frida-kill       (frida-tools)
* frida-apk        (frida-tools)
* frida-create     (frida-tools)
* frida-join       (frida-tools)
* awk
* base64
* basename
* cat
* chmod
* chown
* cp
* cpio
* cut
* date
* dd
* diff
* dirname
* echo
* find
* fuser
* grep
* kill
* less
* ln
* ls
* lsof
* md5sum
* mkdir
* more
* mount
* mv
* nice
* nohup
* pidof
* pkill
* ps
* rm
* sed
* sleep
* sort
* stat
* strings
* tail
* tar
* tee
* telnet
* timeout
* touch
* umount
* wc

同样，Python 也内置了一些可以用来使用的三方库

* lamda            (自身)
* Pillow           (图像处理)
* capstone         (反汇编引擎)
* keystone_engine  (汇编引擎)
* unicorn          (CPU模拟引擎)
* lief             (二进制程序解析)
* lxml             (xml/html解析)
* tornado          (web框架)
* pyOpenSSL        (OpenSSL)
* requests         (requests)
* scapy            (流量分析)
* ujson            (ujson)
* frida            (frida)
* urllib3          (urllib3)
* xmltodict        (xml转dict)
* msgpack_python   (msgpack)
* jmespath         (jmespath)

以及其相关依赖库，因为可能随着更新被移除，请不要使用不在上述列表的库。
这里不会介绍如何使用这些命令或库。
