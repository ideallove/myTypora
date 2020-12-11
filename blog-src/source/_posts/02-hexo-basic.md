---
layout: post
title: Re:从零搭建Hexo博客并部署到GitHub或云服务器上
date: 2020-02-23 11:00:00
updated: 2020-02-23 23:10:00
description: 本文将介绍如何在个人PC上搭建Hexo博客框架并将博客部署到GitHub上或者部署到个人云服务器上，这是我自己在搭建博客的过程的一个汇总。搭建的期间遇到了很多问题，所以本文会直接从我掉过的坑上飞过去.....
categories: 
- [笔记本, 教程]
tags: 
- 正经
- 科学
- 教程
- Hexo
- GitHub
- 云
- 博客
permalink: post/hexo-basic.html
---
### 前言

心血来潮买了云主机，浪费了几个月都没用，然后就学着搭建博客，对比了一下 WordPress 和 Hexo 之后，随性选择了以 Hexo 为框架搭建博客平台。<br/>经过了几次的从零开始，遇到了各种各样的问题之后才成功地搭建好了。我将自己在搭建博客的过程中遇到的一些问题做汇总和记录来帮助自己回顾，也希望对有想法要搭建自己的博客的同学们有一些帮助。  

> Hexo 是一个快速、简洁且高效的博客框架。Hexo 使用 Markdown 解析文章，在几秒内，即可利用靓丽的主题生成静态网页。通过 Hexo 的官方网站 https://hexo.io/ 了解更多关于这个博客框架，它拥有中文文档。

### 主要目录

1. 前言
2. 本地主机的 Hexo 安装操作（以Windows系统为例）
3. Hexo 基本操作
4. 部署到GitHub
5. 部署云服务器（以CentOS服务器为例）
6. 完成部署
7. 常见问题
8. 后记

### 本地主机的 Hexo 安装操作

本地主机以 Windows 10 系统为例。（ **本地主机** 下文均称 **本地PC** ）苹果电脑的 macOS 可以自行使用搜索引擎，安装 Node.js 有很多种方式。

##### 1、安装 Node.js® 

> Node.js是一个基于 Chrome V8 引擎的  JavaScript 运行环境，是一个让 JavaScript 运行在服务端的开发平台。

Node.js 的官方下载地址：https://nodejs.org/ 当然它也有中文网：http://nodejs.cn/ 

<img src="http://cdn.idealx.cn/image/blog-02-01.png" alt="blog-02-01.png" style="zoom:67%;" />

建议下载**LTS**（即Long Term Support，长期技术支持）（此处是**64位**版本的，其他版本如源码可以在DOWNLOAD界面找到），较为稳定，下载的文件名为：node-v12.16.1-x64.msi ，安装过程基本直接**下一步**即可。<br/>安装完成后使用**命令提示符（以下均简写cmd）**查看是否安装成功。

`node -v` 和 `npm -v` 

![blog-02-02.png](http://cdn.idealx.cn/image/blog-02-02.png)

出现安装的版本号说明安装成功。

##### 2、安装 Git

> Git 是一个开源的分布式版本控制系统，可以有效、高速地处理从很小到非常大的项目版本管理。

Git Bash 可以便捷后面的操作。<br/>

> Git Bash 和 CMD 的区别：Bash是基于CMD的，Bash在CMD的基础上新增了一些命令和功能，故建议使用Bash更方便。

官方网站：https://git-scm.com/ 选择Windows版本安装。按照官方文档推荐中国大陆用户从 [淘宝 Git for Windows 镜像](https://npm.taobao.org/mirrors/git-for-windows/) 下载 Git（说得对）。<br/>macOS 和 Linux 系统都有自带的 ***Terminal*** 终端方便下载 Git 。<br/>

<img src="http://cdn.idealx.cn/image/blog-02-03.png" alt="blog-02-03.png" style="zoom: 50%;" />

##### 3、安装 Hexo 

Hexo 的官方网站：https://hexo.io/ 该博客框架拥有中文文档，有些资料需要参考文档。<br/>由于 npm 服务器在国外，因此使用 npm 直接下载可能会遇到卡顿的问题，所以我们先将 npm 转换成淘宝的源。<br/>在 cmd 或 Git Bush 中输入命令：

```bash
npm config set npm config set registry https://registry.npm.taobao.org
```

然后安装 cnpm ：

```bash
npm install -g cnpm --registry=https://registry.npm.taobao.org
```

然后安装 Hexo ：

```bash
cnpm install -g hexo-cli
```

等待安装结束。<br/>选择一个目录来初始化博客：（例如 E:/blog）

```bash
# 如果在图形界面中创建过文件夹，可直接进入
cd e:/blog
hexo init
# 如果没有创建文件夹
cd e:/
mkdir blog
cd blog
hexo init
# 或者按照官方文档的安装方法
cd e:/
hexo init blog
cd blog
```

执行成功后安装两个插件：

```bash
npm install hexo-deployer-git --save
npm install hexo-server
# 或者按照官方文档 直接
npm install
```

然后就可以在本机查看自己的博客了

```bash
hexo s
```

![blog-02-04.png](http://cdn.idealx.cn/image/blog-02-04.png)

打开浏览器输入`localhost:4000`可以看到初始界面。按 Ctrl+C 关闭本地服务器。<br/>本地初始化完成，接下来在部署环节介绍。<br/>注意：部署到 GitHub 或者 云服务器 ，选一种就可以了，也可以自己拓展，以下给出参考操作步骤。

###  Hexo 的基本操作

本节可以参考官方文档，以下仅给出部分示例，这些命令都在 **本地PC** 上运行。

##### 1、创建新的文章

创建一篇名为《Hello》的文章

```bash
hexo new "Hello"
```

在 `source/_posts`会出现一个 MarkDown 文件 `Hello.md` ，可以使用任意一种MD编辑器编写（当然TXT编辑器也可哈如果你愿意的话）。

##### 2、清除缓存

```bash
hexo clean
```

清除缓存文件（`db.json`）和已生成的静态文件（`public`）。

##### 3、生成静态文件

```bash
hexo generate
```

生成静态文件 （`public`）。可以简写为：

```bash
hexo g
```

##### 4、启动服务器

```bash
hexo server
```

启动服务器，默认情况下为 `localhost:4000`。如果想在其他端口运行，需要端口号，例如想在 4001 端口上运行：

```bash
hexo server -p 4001
```

以上命令中的 `server` 可以简写为 `s`。

##### 5、部署服务器

在之后部署的时候会用到。

```bash
hexo deploy
# 可以简写为
hexo d
```

##### 6、其他使用频率高的命令

```bash
# 显示 Hexo 版本
hexo version
# 列出网站的资料
hexo list <type>
hexo list post # 例如显示博文列表
```

### 部署到GitHub

##### 1、准备工作

> 提示：没有 GitHub 的同学可以直接创建一个哈！

打开 GitHub ，点击 `new` 一个repository，创建一个新的仓库，仓库名称必须要遵守 GitHub Pages 的格式： **用户名.github.io** ，否则会出问题，并且勾选 **Initialize this repository with a README** ，如下图所示。

![blog-02-12.png](http://cdn.idealx.cn/image/blog-02-12.png)

建好仓库后，在 **Settings** 设置中有一个 GitHub Pages 一项，里面就写着 GitHub Pages 为我们创建好的域名。在浏览器中访问就可以看到一个初始的界面。这就是博客的默认地址，当然后面我们也可换成自己的域名。

![blog-02-13.png](http://cdn.idealx.cn/image/blog-02-13.png)

![blog-02-14.png](http://cdn.idealx.cn/image/blog-02-14.png)

##### 2、设置 SSH

务必确保在 **本地PC** 已经完成了Node.js、Git 和 Hexo 的安装，打开 Git Bash ，如果是第一次使使用 Git 的话：

```bash
# 以下 user.name 和 user.email 输入自己的，示例：
git config --global user.name "ideallove"
git config --global user.email ideallove@example.com
```

使用 ssh-keygen 生成私钥和公钥：

```bash
ssh-keygen -t rsa
```

可以一路回车键

![blog-02-15.png](http://cdn.idealx.cn/image/blog-02-15.png)

找到你的密钥  `id_rsa` 和公钥 `id_rsa.pub`  的位置。<br/>接着在 GitHub **头像下的 Settings** 里找到添加 SSH key，点击**New SSH key** 。

![blog-02-16.png](http://cdn.idealx.cn/image/blog-02-16.png)

将刚刚生成的公钥 `id_rsa.pub` 文件里的内容复制到 Key 里面（用 **记事本** 打开公钥文件，这里 Office 还提示我说是 publish 文件，2333XD），然后选择添加，GitHub 会提示输入密码确认。<br/>接着在 **本地PC** 的 bash 上输入：

```bash
ssh -T git@github.com
```

![blog-02-17.png](http://cdn.idealx.cn/image/blog-02-17.png)

第一次的时候依旧会让你 yes 确认 ，如果看到 Hi 后面是自己的用户名，就说明成功了。（当然，GitHub 不提供 shell 的连接）

##### 3、在本地PC上完成推送部署

接下来回到我们的 **PC** 上，在刚刚我们生成的 e:/blog 目录下，找到 hexo 的配置文件 `_config.yml` ，使用各种好用的编辑器打开它（意思就是 TXT 编辑器也可，我用的是 Notepad++）。在最下面有个 `deploy` 的配置，在那里**修改为自己的 ID**，示例：

```yaml
deploy:
 type: git
 repo: git@github.com:ideallove/ideallove.github.io.git
 branch: master
```

> 提示：缩进一定不能出问题。

保存并退出，然后发布到 GitHub 上。

```bash
hexo clean && hexo generate && hexo deploy
# 当然也可简写成
hexo clean && hexo g && hexo d
# 这里，不一定每次都要 clean，clean 会清除缓存，导致一些计数脚本清零。
```

然后我们就可以在 **本地PC** 浏览器上输入 GitHub Pages 的域名 `https://自己的用户名.github.io` 访问我们的博客了。

更换为自己的域名，则为后话了。部署到 GitHub 或者 云服务器 ，选一种就可以了。

### 部署到云服务器

##### 1、购买云服务器和域名

购买任意服务器（例如阿里云ECS、阿里云轻量应用服务器、腾讯云CVM、百度云BCC等）和域名。

> 提示：如果使用国内的域名在国内的服务器部署网站需要进行备案，可以使用搜索引擎进行资料的查找。

##### 2、选择服务器镜像类型

建议使用Linux系统的服务器镜像。（Windows也可，这里以阿里云服务器CentOS为例）<br/>首先进入服务器的管理界面，找到***安全***选项中的***防火墙***（可能有一些服务商写的类似的***安全组***），确认应用类型 `HTTP` 协议 `TCP` 端口 `80` 是否设置打开，类似下图所示：

<img src="http://cdn.idealx.cn/image/blog-02-05.png" alt="blog-02-05.png" style="zoom: 67%;" />

确认打开之后进行下一步，可以先配置Git库也可先进行服务器环境的搭建。

##### 3、服务器环境 nginx 搭建

使用云服务商提供的远程登陆登录进云服务器，可以现在服务商设置中设置 root 用户的密码以提高安全性。<br/>以阿里云为例，输入 `sudo su root` **进入 root 用户**，这里我建议使用 nginx 作为服务器环境。

> Nginx 是一款轻量级的 Web 服务器 / 反向代理服务器及电子邮件代理服务器，在 BSD-like 协议下发行。其特点是占有内存少，并发能力强，事实上 nginx 的并发能力在同类型的网页服务器中表现较好，中国大陆使用 nginx 网站用户有：百度、京东、新浪、网易、腾讯、淘宝等。---节选自*百度百科*

首先，**安装 nginx **，在控制台中执行如下命令：

```bash
yum install -y nginx
```

等待下载安装，很快将会显示 `Complete!` 。安装结束后使用如下命令开启环境：

```bash
nginx
```

现在，尝试使用自己的**个人电脑(PC)**上使用浏览器输入云服务器的**公网IP**，就会显示如下界面：

![blog-02-06.png](http://cdn.idealx.cn/image/blog-02-06.png)

恭喜你已经打开了新世界的大门。<br/>这是nginx的默认网页，以上界面是CentOS版本的，其他服务器会有所不同，但这表示我们已经成功了第一步。<br/>实际上我们需要将这个地址指向我们的博客，接下来我们去修改nginx的配置文件。在那之前可以先关闭 nginx （当然也可以不关）：

```bash
# 快速关闭
nginx -s stop
# 有序而完整地关闭
nginx -s quit
```

> 提示：在修改 nginx 的配置文件的时候查阅了相关的资料，阿里云默认库下载的 fedora 版本的 nginx 的文件结构中，配置文件是位于  `/etc/nginx` 下的 `nginx.conf` ，有些服务器可能是 `/etc/nginx/conf.d/default.conf` ，而按照官方的安装方法则可能是 `/etc/nginx/conf/nginx.conf` 。

对于新手来说不一定要使用 `include` 的方法，直接修改 `nginx.conf` 比较快捷。执行如下命令：

```bash
# 进入路径
cd /etc/nginx
# 使用vim编辑器编辑配置文件
vi nginx.conf
```

接下来是vim编辑器的使用（可以使用搜索引擎辅助，查找vim的相关使用命令），在键盘上输入 `i` 进入 `insert` 模式，并进行如下修改：<br/>（1）将最上一行的 user 改为 root（或者创建名为nginx的用户并给予权限）<br/>（2）向下寻找，在 http 中更改 root 指向的路径，比如我这里选择 `/home/www/website` ，当然此时我们还没有创建这个文件夹。<br/>（3）同时如果有了域名的话可以在 `server_name` 写上域名。<br/><img src="http://cdn.idealx.cn/image/blog-02-07.png" alt="blog-02-07.png" style="zoom:67%;" /><br/>![blog-02-08.png](http://cdn.idealx.cn/image/blog-02-08.png)

编辑结束之后，按 `esc` 键，然后输入 `:wq` 并敲回车键退出vim编辑器并保存文件。<br/>接着在我们刚刚 `nginx.conf`配置文件中写的地址创建对应的文件夹（当然也可先创建再修改配置文件，只要没启动都是一样的。）

```bash
cd ~/home
mkdir www
cd /www
mkdir website
```

这样我们就得到了博客的根路径 `/home/www/website` （当然也可设置其他路径）并且与 `nginx.conf` 文件对应。

#####  4、安装 Node.js 和 Git

（1）安装 Node.js 

在 Linux 系统上安装 Node.js 的方法有很多种，详细可以参考搜索引擎或者 Node.js 的GitHub文件。这里使用一种方法：

```bash
curl -sL https://rpm.nodesource.com/setup_13.x | bash -
# 这里的setup_13.x指Node.js13的版本，可以改为其他版本，建议不要太低为好，hexo一些主题的Node.js版本都比较高。
yum install -y nodejs
```

在安装过程中可能会发生下载速度极慢的情况，具体取决于云服务器选择的源。<br/>安装完成之后像我们PC上一样执行一下版本号命令：

```bash
node -v
npm -v
```

![blog-02-09.png](http://cdn.idealx.cn/image/blog-02-09.png)

如果成功打印版本号则说明安装成功。

（2）安装 Git 以及配置仓库

主要是让我们的PC可以通过ssh的方式连接到云服务器，然后我们可以通过 `deploy` 的方式将我们的博客推到服务器上，在控制台中输入如下命令：<br/>安装 Git ：

```bash
yum install git
```

安装结束后配置 git 用户：

```bash
adduser git
```

修改用户的权限：

```bash
chmod 740 /etc/sudoers
vi /etc/sudoers
```

在 `sudoers` 文件中找到这段话并添加进去，同样是vim编辑器的操作。

![blog-02-10.png](http://cdn.idealx.cn/image/blog-02-10.png)

编辑结束之后，按 `esc` 键，然后输入 `:wq` 并敲回车键退出vim编辑器并保存文件。<br/>保存退出后将 `sudoers` 文件的权限改回来：

```bash
chmod 400 /etc/sudoers
```

并设置 git 用户的密码：

```bash
sudo password git
# 这里会让输入密码，然后确认密码，如果密码太简单的话它会嫌弃并说密码是"Bad Password"（并不影响使用）
```

切换到 git 用户，并创建 .ssh 文件夹和公钥密钥文件

```bash
# 切换到 git 用户
su git
cd ~
mkdir .ssh && cd .ssh
# 生成公钥和密钥文件
ssh-keygen
# 然后一路 enter 键即可，此时在目录下有两个文件，密钥 id_rsa 和公钥 id_rsa.pub ，接下来复制一份公钥
cp id_rsa.pub anthorized_keys
# 然后修改它的权限
chmod 600 ~/.ssh/authorized_keys
chmod 700 ~/.ssh
```

接下来在我们自己的 **本地PC** 上，打开 cmd 或者 bash ，尝试使用 ssh 方式连接到我们的云服务器。

```bash
ssh -v git@云服务器的公网IP地址
```

> 提示：在第一次登录的时候，服务器会让你确认是否连接，输入 `yes` 进入下一步，然后服务器会让你输入 git 用户的密码，输完密码后回车键就可以进入了。
>
> 当然这里也可以用其他方法，让服务器与 PC 建立 ssh 信任关系，这样就不需要输入密码了。
>
> 如果为了安全起见，还可以将 git 用户的 shell 登录权限禁用。

![blog-02-11.png](http://cdn.idealx.cn/image/blog-02-11.png)

出现 `Welcome to Alibaba Cloud Elastic Compute Service !` 或其他服务器有类似的语句（或者直接出现 git 用户的命令），就说明登录成功了。<br/>接下来我们要创建一个新的 git 仓库，并且新建一个 `post-update` 文件（有些 git 版本可能是 `post-receive` ，注意分辨即可）。

```bash
cd ~
git init --bare blog.git
vi ~/home/git/blog.git/hooks/post-update
```

> 提示：在初始化 `init` 之后可以 `cd ~/home/git/blog.git/hooks/` 然后使用 `ls -a` 来展示文件夹下的全部文件，如果出现了 `post-update.sample` ，则可以选择更改文件名来使它有作用，也可新建。

vim 编辑器下在键盘上输入 `i` 进入 `insert` 模式，并输入以下内容：

```bash
git --work-tree=/home/www/website --git-dir=/home/git/blog.git checkout -f
```

编辑结束之后，按 `esc` 键，然后输入 `:wq` 并敲回车键退出vim编辑器并保存文件。<br/>添加完毕后修改权限：

```bash
chmod +x ~/home/git/blog.git/hooks/post-update
exit # 退出到 root 登录
chown -R git:git /home/git/blog.git # 添加权限
```

这样我们就完成了**服务器端**的操作。

##### 5、在本地PC上完成推送部署

接下来回到我们的 **本地PC** 上，在刚刚我们生成的 e:/blog 目录下，找到 hexo 的配置文件 `_config.yml` ，使用各种好用的编辑器打开它（意思就是 TXT 编辑器也可，我用的是 Notepad++）。在最下面有个 `deploy` 的配置，在那里修改：

```yaml
deploy:
 type: git
 repo: git@云服务器的公网IP:/home/git/blog.git
 branch: master
 message:
```

> 提示：缩进一定不能出问题。如果域名已经能正常解析云服务器的IP，也可以在输入IP的地方换成域名。

保存并退出，然后发布到服务器上。

```bash
hexo clean && hexo generate && hexo deploy
# 当然也可简写成
hexo clean && hexo g && hexo d
# 这里，不一定每次都要 clean，clean 会清除缓存，导致一些计数脚本清零。
```

接着我们在 **服务器控制台** 上重新运行 nginx 服务器：

```bash
nginx
```

然后我们就可以在 **本地主机** 浏览器上输入域名或者公网IP访问我们的博客了。

### 完成部署

以上两种方法选择一种即可，完成部署以后可以仔细修改 `_config.yml` 的配置文件，并且修改自己的博客主题，美化一下。

### 常见问题

如果在本教程过程中出现问题，可以在下方评论（如果评论板搭建好了的话......）或者mail给我。

Q：部署到云服务器，出现了 403 界面怎么办？

A： 403 为禁止访问，nginx 服务器没有获得你的路径的读取的权限，检查是否给予了 `post-update` 权限 `chmod +x ~/home/git/blog.git/hooks/post-update`。如果还不行可以尝试使用 `chmod -R 777 /home/www/website` （当然 777 要慎用~~玩LOL的时候也是~~）。

##### 参考资料链接

1. [Node.js 中文网](http://nodejs.cn/)
2. [Hexo 中文文档](https://hexo.io/zh-cn/)
3. [Nginx 中文文档](https://www.nginx.cn/)
4. [Nginx 安装配置](https://www.runoob.com/linux/nginx-install-setup.html)
5. [从零搭建Hexo博客并部署阿里云服务器](https://blog.csdn.net/NoCortY/article/details/99631249)
6. [带你跳过各种坑，一次性把 Hexo 博客部署到自己的服务器](https://blog.csdn.net/qq_35561857/article/details/81590953)
7. [通过Git将Hexo博客部署到服务器](https://www.jianshu.com/p/e03e363713f9)
8. [使用hexo搭建github博客](https://www.jianshu.com/p/1bcad7700c46)

### 后记

除了感觉自己写的太长之外没什么想说的，本身想把这个博客变成技术博客我觉得我太天真了。大胆预言一波我的博客绝对会变成杂货铺的......

另附CSDN地址：https://blog.csdn.net/qq_43187818/article/details/104468721