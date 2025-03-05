---
title: Zerotier内网穿透+公网自建Moon节点+飞牛影视库
---
## 场景描述：
    最近购买了天钡WTR PRO N100准系统版本，自己购买齐其他备件，装上了飞牛NAS系统。但是这样只能在NAS接入的网络通过局域网IP地址体验NAS，在其他地方便无法使用。为了解决该问题，实现在异地体验NAS观影以及其他体验，决定使用拥有公网IP地址的服务器配置zerotier和Moon节点的方案来实现内网穿透。
## 需求：
一台拥有公网ipv4地址的机器，如云服务器，vps等
### 1.公网服务器安装Zerotier，以ubuntu22.04为例：
``` bash
curl -s https://install.zerotier.com | sudo bash
```
### 2.公网服务器自建Moon节点

### 2.Moon节点加入zerotier网络

### 3.设备加入zerotier网络

### 4.设备将Moon节点入轨
``` bash
$ zerotier-cli orbit Moon节点ID Moon节点ID
```

### 5.测试

