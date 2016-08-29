---
title: Hexo blog的建立
date: 2016-08-27 08:18:06
tags:
  - Hexo
categories: Hexo
---
## 为什么选择hexo

前段时间发现github pages功能，可以用来托管个人的blog(-_-|| 果然是小白，什么都不懂)，一般可以通过github+jekyll+markdown或者github+hexo+markdown来完成这个事。捣鼓了一阵jekyll之后，发现还是Hexo的主题更加酷一点，于是选择了hexo，之前用vmware安装了ubuntu虚拟机，那好，在ubuntu下面完成这件事吧。

<!-- more -->

## 条件

1.安装git（只需要一条命令，自行百度～）
2.安装node.js和npm
3.安装hexo和部署

## 步骤
### 安装nodejs
nodejs在[这里](https://npm.taobao.org/mirrors/node)下载，我选择的是node-v6.4.0-linux-x64.tar.xz，将它复制到/opt目录下；
进入/opt目录，输入命令：
```
tar -xJf node-v6.4.0-linux-x64.tar.xz	将文件解压到当前目录
mv node-v6.4.0-linux-x64 node		将文件改名为node

```
输入命令：vim /etc/profile，在末尾添加以下三行：
export NODE_HOME=/opt/node
export PATH=$PATH:$NODE_HOME/bin 
export NODE_PATH=$NODE_HOME/lib/node_modules
之后按Esc键，并输入“：wq!”命令保存配置并推出
（如果没有安装vim，用gedit也可以）

在命令行输入：source /etc/profile，然后在命令行输入：node -v，返回版本信息6.4.0，说明环境变量配置就生效了；但你会发现进入root账户，改配置并没有生效，解决的方法就是：在命令行输入：vim /root/.bashrc,并在文件末尾加入一行source etc/profile命令，保存。

另外，安装npm和node命令到系统命令
```
sudo ln -s /opt/node/bin/node /usr/local/bin/node 
sudo ln -s /opt/node/bin/npm /usr/local/bin/npm
```
可以通过“node -v”和“npm -v”验证是否生效。

### 安装hexo和初始化
安装hexo
```
sudo npm install -g hexo
```
-g表示全局安装

初始化博客的根目录
```
hexo init <dir>		<dir>为博客的根目录
npm install
hexo server
```
通过这三条指令，就可以在ubuntu的浏览器中输入http://localhost:4000 本地查看hexo博客。

### 导入NexT主题
参考[NexT使用文档](http://theme-next.iissnan.com/getting-started.html)，按照它做，基本上就可以将NexT主题导入。

### 部署到github
参考[hexo deployment](https://hexo.io/zh-cn/docs/deployment.html)。
我这里填上自己的repository: https://github.com/pqwggm/pqwggm.github.io.git

### 问题
由于github采用的是安全链接https，所以在博客根目录theme/_config.yml下的menu有点问题，部署到github之后，点击menu的链接，提示找不到页面。
我这里的处理方法直接把它们的url改为绝对路径
(我的blog地址为:https://pqwggm.github.io)。
```
menu:
  home: /
  archives: https://pqwggm.github.io/archives/
  categories: https://pqwggm.github.io/categories/
  tags: https://pqwggm.github.io/tags/
  about: https://pqwggm.github.io/about/
  #commonweal: /404.html
```

## 参考资料
【1】[Linux(ubuntu16.04)下安装nodejs及配置环境变量](http://jingyan.baidu.com/article/25648fc18ee5bd9190fd0058.html?st=2&os=0&bd_page_type=1&net_type=1)
【2】[Ubuntu 16.04 64位 搭建 node.js NodeJS 环境](http://blog.csdn.net/caib1109/article/details/51804687)
【3】[NexT使用文档](http://theme-next.iissnan.com/getting-started.html)
【4】[hexo中文开发文档](https://hexo.io/zh-cn/docs/)


