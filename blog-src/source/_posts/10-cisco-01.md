---
layout: post
title: Re:从零开始的思科模拟器之交换机安全端口设置
date: 2020-04-29 10:50:00
description: 思科模拟器 Cisco Packet Tracer 之交换机安全端口设置。本文给出了端口绑定mac地址和限制最大连接数的两个案例。请配合思科官方文档食用。<br />我真的下饭。
categories: 
- [网络, 基础学习]
tags: 
- 思科模拟器
- cisco
- 网络基础
cover: true
thumbnail: "https://cdn.jsdelivr.net/gh/ideallove/CDN/blog/cisco-01/thumbnail.jpg"
permalink: cisco/01.html
---

### 思科模拟器 之 交换机安全端口设置

> 注意：本文不太适合新手直接阅读，请配合思科官方文档观看。

> 本文使用的模拟器为 Cisco Packet Tracer 6.2 Student Version

> 本文给出交换机端口安全配置的两个示例

### **一、** 端口绑定MAC地址

按照拓扑图连接，配置两台PC的IP地址。

如图所示：

<img src='https://cdn.jsdelivr.net/gh/ideallove/CDN/blog/cisco-01/01.jpg' height=50% width=50%>

PC 0的IP地址为：192.168.1.2/24

PC 1的IP地址为：192.168.1.3/24

PC 1的MAC地址为：0002.164D.DE81

**1、** **绑定一个非 PC 1的MAC地址，检查是否可以ping通PC 0。**

配置交换机：

```
Switch>en
Switch#
Switch#conf t
Enter configuration commands, one per line. End with CNTL/Z.
Switch(config)#hostname SW1
SW1(config)#int range f0/1-2
SW1(config-if-range)#switchport mode access
SW1(config-if-range)#switchport port-security maximum 1
SW1(config-if-range)#switchport port-security violation protect
SW1(config-if-range)#int f0/10
SW1(config-if)#switchport port-security mac-address 0002.164d.de00
```

PC 1 ping PC 0 测试：无法ping通

<img src='https://cdn.jsdelivr.net/gh/ideallove/CDN/blog/cisco-01/02.jpg' height=50% width=50%>


**2、** **修改交换机配置，将PC 1的MAC地址绑定，再次测试：**

```
SW1(config)#int f0/2
SW1(config-if)#no switchport port-security mac-address 0002.164d.de00
SW1(config-if)#switchport port-security mac-address 0002.164d.de81
```

<img src='https://cdn.jsdelivr.net/gh/ideallove/CDN/blog/cisco-01/03.jpg' height=50% width=50%>

Ping 通。

实验结果正确。

### 二、限制最大连接数为1

**按照拓扑图连接，并配置对应IP：**

<img src='https://cdn.jsdelivr.net/gh/ideallove/CDN/blog/cisco-01/04.jpg' height=50% width=50%>

配置交换机SW2：

```
Switch>en
Switch#conf t
Enter configuration commands, one per line. End with CNTL/Z.
Switch(config)#hostname SW2
SW2(config)#int range f0/11-14
SW2(config-if-range)#switchport mode access 
SW2(config-if-range)#switchport port-security 
SW2(config-if-range)#switchport port-security maximum 2
SW2(config-if-range)#switchport port-security violation protect 
```

 首先配置最大连接数为2，测试是否能ping通：

<img src='https://cdn.jsdelivr.net/gh/ideallove/CDN/blog/cisco-01/05.jpg' height=50% width=50%>

仅能ping通1个，猜测交换机也算一台设备

修改交换机配置，设maximum为3：

```
SW2(config)#int range f0/11-14
SW2(config-if-range)#switchport port-security maximum 3
```

<img src='https://cdn.jsdelivr.net/gh/ideallove/CDN/blog/cisco-01/06.jpg' height=50% width=50%>

全ping通。

然后限制maximum为1，修改交换机SW2的配置：

```
SW2(config)#int range f0/11-14
SW2(config-if-range)#switchport port-security maximum 1
```

注意：此时会报出maximum小于mac地址的错误，此时：

断开连接的f0/14的线缆，

然后重新配置SW2：

```
SW2(config-if-range)#no switchport port-security violation protect
SW2(config-if-range)#no switchport port-security maximum 3
SW2(config-if-range)#no switchport port-security 
SW2(config-if-range)#switchport port-security
SW2(config-if-range)#switchport port-security maximum 1
SW2(config-if-range)#switchport port-security violation protect
```

 然后进行ping测试：

<img src='https://cdn.jsdelivr.net/gh/ideallove/CDN/blog/cisco-01/07.jpg' height=50% width=50%>

测试成功，全不通。

### 小结

别说了，XX思科模拟器。