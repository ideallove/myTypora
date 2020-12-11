---
layout: post
title: Re:从零开始的思科模拟器之DHCP配置
date: 2020-05-07 10:00:00
description: 思科模拟器 Cisco Packet Tracer 之 DHCP服务配置。本文给出了配置DHCP的案例。请配合思科官方文档食用。<br />我真的下饭*2。
categories: 
- [网络, 基础学习]
tags: 
- 思科模拟器
- cisco
- 网络基础
cover: true
thumbnail: "https://cdn.jsdelivr.net/gh/ideallove/CDN/blog/cisco/thumbnail.jpg"
permalink: cisco/02.html
---

> 本文还需要优化，这里仅给出几个案例

### 思科模拟器 之 DHCP服务配置

>由于网络的流行和广泛使用，在企业或学校都需要配置DHCP服务器，这样可以使无论在哪的电脑，只要连上局域网，就可以通过**“自动获取IP地址“**方式来自动获取IP地址网关，这样可以节约网络成本，网络资源。

> 注意：本文不太适合新手直接阅读，请配合思科官方文档观看。

> 本文使用的模拟器为 Cisco Packet Tracer 6.2 Student Version

### 一、基于路由器和服务器的DHCP配置（无VLAN划分）

拓扑图：

![](https://cdn.jsdelivr.net/gh/ideallove/CDN/blog/cisco/cisco-02/01.png)

配置路由器Router0：

```
Router>en
Router#conf t
Router(config)#hostname R1
R1(config)#int f0/0		//进入端口f0/0
R1(config-if)#ip address 192.168.1.1 255.255.255.0	//配置IP
R1(config-if)#no shutdown	//打开端口
R1(config-if)#int f0/1
R1(config-if)#ip address 192.168.2.1 255.255.255.0
R1(config-if)#ip helper-address 192.168.1.2		//使该端口上的IP使用DHCP分配
R1(config-if)#no shutdown
```

DHCP-Server 的 IP配置：
![](https://cdn.jsdelivr.net/gh/ideallove/CDN/blog/cisco/cisco-02/02.png)

在虚拟服务器的**`Service选项卡`**中选择**DHCP 服务**：
修改配置：
默认网关：为需要DHCP的网段
设置一个DNS服务器
开始IP地址：可以自由选择
设置子网掩码：这里以 /24 的子网掩码为例
最大连接数：以 /24 的子网掩码为例，255-2=253 个地址留给主机
TFTP服务器：不需要使用，则无需修改

![](https://cdn.jsdelivr.net/gh/ideallove/CDN/blog/cisco/cisco-02/03.png)

PC运行结果：

![](https://cdn.jsdelivr.net/gh/ideallove/CDN/blog/cisco/cisco-02/04.png)
![](https://cdn.jsdelivr.net/gh/ideallove/CDN/blog/cisco/cisco-02/05.png)

### 二、基于单臂路由和服务器的DHCP配置（划分VLAN）

拓扑图：

![](https://cdn.jsdelivr.net/gh/ideallove/CDN/blog/cisco/cisco-02/06.png)

二层交换机配置：
```
Switch>en
Switch#conf t
Enter configuration commands, one per line. End with CNTL/Z.
Switch(config)#hostname SW1
SW1(config)#vlan 10
SW1(config-vlan)#vlan 20
SW1(config-vlan)#int f0/1
SW1(config-if)#switchport mode access
SW1(config-if)#switchport access vlan 10
SW1(config-if)#int f0/2
SW1(config-if)#switchport mode access
SW1(config-if)#switchport access vlan 20
SW1(config-if)#int f0/24
SW1(config-if)#switchport mode trunk
```

路由器配置：
```
Router>en
Router#conf t
Router(config)#int f0/0
Router(config-if)#no shutdown	//打开端口
Router(config-if)#int f0/0.1	//进入子端口
Router(config-subif)#encapsulation dot1Q 10	//封装数据
Router(config-subif)#ip address 192.168.1.1 255.255.255.0	//设置IP
Router(config-subif)#int f0/0.2	//同上
Router(config-subif)#encapsulation dot1Q 20	//封装数据
Router(config-subif)#ip address 192.168.2.1 255.255.255.0
```

接着，配置服务器侧的端口
```
Router(config)#int f0/1
Router(config-if)#no shutdown
Router(config-if)#ip address 192.168.3.1 255.255.255.0
Router(config-if)#int f0/0.1	//进入刚刚的子端口
Router(config-subif)#ip helper-address 192.168.3.2	//配置DHCP
Router(config-subif)#int f0/0.2	//同上
Router(config-subif)#ip helper-address 192.168.3.2
```
服务器配置：
![](https://cdn.jsdelivr.net/gh/ideallove/CDN/blog/cisco/cisco-02/07.png)
![](https://cdn.jsdelivr.net/gh/ideallove/CDN/blog/cisco/cisco-02/08.png)
![](https://cdn.jsdelivr.net/gh/ideallove/CDN/blog/cisco/cisco-02/09.png)


PC获取DHCP结果：

![](https://cdn.jsdelivr.net/gh/ideallove/CDN/blog/cisco/cisco-02/10.png)
![](https://cdn.jsdelivr.net/gh/ideallove/CDN/blog/cisco/cisco-02/11.png)

### 三、基于三层交换机和路由器的DHCP配置（划分VLAN）

拓扑图：
![](https://cdn.jsdelivr.net/gh/ideallove/CDN/blog/cisco/cisco-02/12.png)

配置二层交换机：
```
Switch>en
Switch#conf t
Switch(config)#hostname SW1
SW1(config)#vlan 10
SW1(config-vlan)#vlan 20
SW1(config-vlan)#int f0/1
SW1(config-if)#switchport mode access
SW1(config-if)#switchport access vlan 10
SW1(config-if)#int f0/2
SW1(config-if)#switchport mode access
SW1(config-if)#switchport access vlan 20
SW1(config-if)#int f0/24
SW1(config-if)#switchport mode trunk
```

配置三层交换机：
```
Switch>
Switch>en
Switch#conf t
Switch(config)#hostname MSW1
MSW1(config)#vlan 10
MSW1(config-vlan)#vlan 20
MSW1(config-vlan)#int vlan 10
MSW1(config-if)#ip address 192.168.1.1 255.255.255.0
MSW1(config-if)#int vlan 20
MSW1(config-if)#ip address 192.168.2.1 255.255.255.0
MSW1(config-if)#int f0/1
MSW1(config-if)#no switchport
MSW1(config-if)#ip address 192.168.3.1 255.255.255.0
MSW1(config-if)#ex
MSW1(config)#ip routing
```
到这里 三层交换机还有一个中继没有配，先配置路由器。
配置路由器：

```
Router>en
Router#conf t
Router(config)#int f0/0
Router(config-if)#no shutdown
Router(config-if)#int f0/0
Router(config-if)#ip address 192.168.3.2 255.255.255.0
Router(config-if)#ex
Router(config)#ip route 0.0.0.0 0.0.0.0 192.168.3.1
Router(config)#ip dhcp pool vlan10
Router(dhcp-config)#network 192.168.1.0 255.255.255.0
Router(dhcp-config)#dns-server 114.114.114.114
Router(dhcp-config)#default-router 192.168.1.1
Router(dhcp-config)#ex
Router(config)#ip dhcp excluded-address 192.168.1.1
Router(config)#ip dhcp pool vlan20
Router(dhcp-config)#default-router 192.168.2.1
Router(dhcp-config)#dns-server 114.114.114.114
Router(dhcp-config)#network 192.168.2.0 255.255.255.0
Router(dhcp-config)#ex
Router(config)#ip dhcp excluded-address 192.168.2.1
```

返回三层交换机配置：
```
MSW1>en
MSW1#conf t
MSW1(config)#int vlan 10
MSW1(config-if)#ip helper-address 192.168.3.2
MSW1(config-if)#int vlan 20
MSW1(config-if)#ip helper-address 192.168.3.2
MSW1(config-if)#ex
```
PC获取DHCP结果：

![](https://cdn.jsdelivr.net/gh/ideallove/CDN/blog/cisco/cisco-02/13.png)
![](https://cdn.jsdelivr.net/gh/ideallove/CDN/blog/cisco/cisco-02/14.png)

### 后记

第三种方法 也可把路由器换成服务器，服务器配置几乎一致。

如果有不正确的地方欢迎大佬们指正，有更好的方法欢迎大佬们指教。

我真的下饭。