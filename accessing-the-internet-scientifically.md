# 科学上网

在互联网时代，Google、Facebook、Youtube 都不能上？太不科学了！

由于 [GFW（国家防火墙）](https://baike.baidu.com/item/Great%20Firewall/4843556?fromtitle=GFW&fromid=18582731&fr=aladdin) 的安全策略，国外有很多的网站在国内无法正常访问！

科学上网，顾名思义，就是利用技术手段能够帮助我们科学地正常访问这些 GFW 禁止/过滤掉的国外网站或 APP！

它还有个更通俗更形象的解释，[翻墙](https://baike.baidu.com/item/%E7%BF%BB%E5%A2%99/754773)！

出于学习的目的，经常需要访问 Google、Wikipedia、StackOverflow 等网站中涉及到计算机技术开发相关技术资源！

本文主要是记录总结个人科学上网的经验，方便查阅！

## 一道隐形的墙 GFW

众所周知，天朝局域网通过 [GFW](http://zh.wikipedia.org/wiki/%E9%87%91%E7%9B%BE%E5%B7%A5%E7%A8%8B) 隔离了我们与外界的交流，当然，这个隔离并非完全隔离，而是选择性的，天朝不希望你上的网站就直接阻断。每一个网络请求都是有数据特征的，不同的协议具备不同的特征，比如 HTTP/HTTPS 这类请求，会很明确地告诉 GFW 它们要请求哪个域名；再比如 TCP 请求，它只会告诉 GFW 它们要请求哪个 IP。

GFW 封锁包含多种方式，最容易操作也是最基础的方式便是域名黑白名单，在黑名单内的域名不让通过，IP 黑白名单也是这个道理。如果你有一台国外服务器不在 GFW 的黑名单内，天朝局域网的机器就可以跟这一台机器通讯。那么一个翻墙的方案就出来了：境内设备与境外机器通讯，境内想看什么网页，就告诉境外的机器，让境外机器代理抓取，然后送回来，我们要做的就是保证境内设备与境外设备通讯时不被 GFW 怀疑和窃听。

ssh tunnel 是比较具有代表性的防窃听通讯隧道，通过 ssh 与境外服务器建立一条加密通道，此时的通讯 GFW 会将其视作普通的连接。由于大家都这么玩，GFW 着急了，于是它通过各种流量特征分析，渐渐的能够识别哪些连接是 ssh 隧道，并尝试性的对隧道做干扰，结果还是玩不过 GFW，众多隧道纷纷不通。

## 科学上网工具 Shadowsocks

科学上网工具有很多，我也尝试过不少，有免费的和付费的，但是均由于速度不够好或不是足够稳定等原因而放弃。

直到遇上了 Shadowsocks！目前已使用好几年，速度和稳定性效果都很好。

Shadowsocks（中文名称：影梭，俗称：小飞机），是一款国人开发的开源加密代理工具，支持 Windows、Mac、Android、iOS 等几乎所有的平台，是目前最稳定最好用的科学上网工具之一。

其官网为：https://shadowsocks.org/，代码托管在 Github 上。

Shadowsocks 的故事很精彩，有兴趣的朋友可以了解下《[Shadowsocks-的前世后生](http://www.chinagfw.org/2016/08/shadowsocks_31.html)》。

如果你理解了 GFW 的原理，那 Shadowsocks 的原理就可以用一句简单的描述来理解了：它发出的 TCP 包，没有明显包特征，GFW 分析不出来，当作普通流量放过了。

具体而言，Shadowsocks 将原来 ssh 创建的 Socks5 协议拆开成 Server 端和 Client 端，两个端分别安装在境外服务器和境内设备上。

Client 和 Server 之间可以通过多种方式加密，并要求提供密码确保链路的安全性。 

### Shadowsocks Client

客户端可以从 [官网](https://shadowsocks.org/en/download/clients.html) 或者 Github 直接下载。

各平台推荐下载：

Windows：[Github](https://github.com/shadowsocks/shadowsocks-windows/releases)

Mac：[Github](https://github.com/shadowsocks/ShadowsocksX-NG/releases)

Android：[Github](https://github.com/shadowsocks/shadowsocks-windows/releases)

iOS：Shadowrocket（安装  PP 助手PC版，然后连接手机安装 PP 助手 iOS 版，然后搜索安装 Shadowrocket）

安装好客户端，设置好服务器，并启用系统代理即可。

### Shadowsocks Server

有了 Client，还需要境外的 Server 账号。

网络上提供 Shadowsocks Server 的服务账号有很多，使用下来还是建议买一台靠谱的 VPS，搭建自己的 Shadowsocks Server，稳定可靠，被封掉的风险小得多。

推荐使用一款性价比较高的便宜 VPS 主机 - 搬瓦工 VPS。

**搬瓦工**，因其官网网站标识是 BandwagonHost，有点类似 BanWaGong 的拼写，所以国内用户喜欢称作为搬瓦工 VPS。搬瓦工 VPS 性价比极高，支持支付宝付款，管理面板还支持一键搭建 Shadowsocks，使用非常简单。

[搬瓦工VPS中文网](http://banwagong.cn/ ) 专门介绍和分享搬瓦工 VPS 便宜主机的信息，并且长期提供。

总结下来的搭建步骤：

1. 访问 [搬瓦工官网](https://bandwagonhost.com/aff.php?aff=34596) 
2. 在首页选择 $19.99 的 10G VPS，并选择性能更好的 KVM 架构
3. 确认产品并添加到购物车
4. 在订单页面的 **Promotional Code** 中，输入从 [搬瓦工VPS中文网](http://banwagong.cn/ ) 获取的优惠码，并点击 *Validate Code* 应用优惠，然后点击 *Checkout* 结算
5. 在结算页面，需要输入个人信息，选择 *Alipay*，然后完成订单，并付款。
6. 在 Client Area -> Services -> My Services 页面，可以查看到我们购买的主机及其IP地址，点击 *KiwiVM Control Panel* 进入主机控制面板
7. 新版的 KiwiVM Extras 中已经移除了 一键安装 Shadowsocks Server 的链接，但是 我们还是访问 [链接]( https://kiwivm.64clouds.com/preloader.php?load=/main-exec.php?mode=extras_shadowsocks) 进入，点击 *Install Shadowsocks Server* 很快就可以安装成功。
8. 将得到的IP地址、端口、密码、加密方式配置到客户端中，开启可以科学上网了。

如果对以上步骤有疑问，可以参考更详细的 [购买攻略](http://banwagong.cn/gonglue.html)。

#后记

互联网时代，更需要坚持正确价值观！

请勿将科学上网方式用作非法用途！

## 参考

1. 《[Shadowsocks 原理简介及安装指南](https://www.barretlee.com/blog/2016/08/03/shadowsocks/)》