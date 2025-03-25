---
title: Zerotier内网穿透+公网自建Moon节点+飞牛影视库
---
## 场景描述：
最近购买了天钡WTR PRO N100准系统版本，自己购买齐其他备件，装上了飞牛NAS系统。但是这样只能在NAS接入的网络通过局域网IP地址体验NAS，在其他地方便无法使用。为了解决该问题，实现在异地体验NAS观影以及其他体验，决定使用拥有公网IP地址的服务器配置zerotier和Moon节点的方案来实现内网穿透。
## 需求：
一台拥有公网ipv4地址的机器，如云服务器，vps等

## 步骤：
### 1.公网服务器安装Zerotier，以ubuntu22.04为例：
①安装Zerotier
``` bash
curl -s https://install.zerotier.com | sudo bash
```
②查看是否安装成功,看到Online即成功
``` bash
zerotier-cli status
```
### 2.公网服务器自建Moon节点
①生成 Moon 配置文件
``` bash
cd /var/lib/zerotier-one
```
``` bash
zerotier-idtool initmoon identity.public > moon.json
```
②编辑 Moon 配置文件
``` bash
vim moon.json
```

``` bash
  "id": "96******8c",
  "objtype": "world",
  "roots": [
    {
      "identity": "96******8c:0:******",
      "stableEndpoints": []
    }
  ],
  "signingKey": "signingKey",
  "signingKey_SECRET": "signingKey_SECRET",
  "updatesMustBeSignedBy": "updatesMustBeSigned",
  "worldType": "moon"
```
找到 "stableEndpoints": [] 。
添加 "IPv4地址/9993" 或者 "IPv4地址/9993","IPv6地址/9993" 。

③生成 .moon 签名文件
``` bash
zerotier-idtool genmoon moon.json
```

④创建 moon 结点文件夹并复制签名文件到该文件夹内
``` bash
mkdir /var/lib/zerotier-one/moons.d
```
``` bash
cp 0000006xxxxxxxxx.moon moons.d/
```

⑤重启 ZeroTier 服务
``` bash
/etc/init.d/zerotier-one restart
```

### 3.Moon节点加入zerotier网络
``` bash
zerotier-cli join <Network ID>
```

### 4.设备加入zerotier网络
``` bash
zerotier-cli join <Network ID>
```
``` bash
zerotier-cli orbit <Moon 节点 ID> <Moon 节点 ID>
```

### 5.测试
``` bash
zerotier-cli listpeers
```

