# Ubuntu16.04 科学上网

[toc]

## 问题描述

ros操作系统的一些命令如rosdep总显示链接不到source。

参考[ldg个人博客]([https://ldgyyf.cn/2019/06/27/Linux/ubuntu%E4%B8%8B%E7%A7%91%E5%AD%A6%E4%B8%8A%E7%BD%91/](https://ldgyyf.cn/2019/06/27/Linux/ubuntu下科学上网/))

## 安装shadowsocks-qt5

添加源：

```shell
sudo add-apt-repository ppa:hzwhuang/ss-qt5
sudo apt-get update
```

安装shadowsocks-qt5：

```shell
sudo apt-get install shadowsocks-qt5
```

搜索shadowsocks-qt5，打开shadowsocks-qt5。

## 配置shadowsocks-qt5

添加连接：

![shadowsocks-qt5-add](https://amnesiagreens-1301256683.cos.ap-chengdu.myqcloud.com/Ubuntu/shadowsocks-qt5-add.jpg)

填写账户：

![image-20200224222855243](https://amnesiagreens-1301256683.cos.ap-chengdu.myqcloud.com/Ubuntu/image-20200224222855243.png)

## Proxychains安装

咱们安装的代理是基于本地服务器SOCKS，而我们平常的一些上网活动是通过HTTP进行的，所以距离能科学上网还需要安装proxychains插件。

插件安装：

下载压缩包：<https://github.com/rofl0r/proxychains-ng.git>

![image-20200224224048860](https://amnesiagreens-1301256683.cos.ap-chengdu.myqcloud.com/Ubuntu/image-20200224224048860.png)

解压：

```shell
cd ~/Downloads
unzip pro*.zip
```

安装：

```shell
cd ~/Downloads
cd proxychains-ng-master/
./configure
sudo make && sudo make install
sudo cp ./src/proxychains.conf /etc/proxychains.conf
```

## Proxychains配置

```shell
sudo gedit /etc/proxychains.conf
```

将最后一行的 socks4 127.0.0.1 9050修改为socks5 127.0.0.1 1080，最终如下图

## 科学上网测试

安装curl

```shell
sudo apt-get install curl
proxychains4 curl www.google.com.hk
```

成功后是这样的：

![image-20200225141257757](https://amnesiagreens-1301256683.cos.ap-chengdu.myqcloud.com/Ubuntu/image-20200225141257757.png)

## 终端科学上网

在命令前面加上`proxychains4`即可，如：

```shell
proxychains4 rosdep update
```

![image-20200225152516790](https://amnesiagreens-1301256683.cos.ap-chengdu.myqcloud.com/Ubuntu/image-20200225152516790.png)

## 浏览器科学上网

了解自己浏览器的命令行启动代码，如我的chrome可以用命令`google-chrome`启动，如果想让其通过代理科学上网，可以在这个命令前加上`proxychains4`即可。

