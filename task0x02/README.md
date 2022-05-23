# 第二次作业

## 实验环境

本地虚拟机环境（Ubuntu 20.04）以及阿里云环境（CentOS 7.7）

## 实验问题

### 使用表格方式记录至少 2 个不同 Linux 发行版本上以下信息的获取方法，使用 asciinema录屏方式「分段」记录相关信息的获取过程和结果

|       版本号       | ubuntu 20.04 | CentOS 7.7 |
| :----------------: | :----------: | :----: |
|        安装        |     sudo apt install XXX         | yum install xxx |
|      安装路径      | which XXX | which xxx |
|        卸载        | sudo apt-get remove --purge XXX | yum -y remove xxx |
|      验证卸载      | which | which xxx |
| 找特殊文件名的文件 | sudo find ./ -name '*XXX*' | sudo find ./ -name '*XXX* |
|  找特殊内容的文件  | sudo grep -r 'XXX' ./ | sudo grep -r 'XXX' ./ |
|     文件的压缩     | 具体用法见实例 | 具体用法见实例 |
|    文件的解压缩    | 具体用法见实例 | 具体用法见实例 |
|    CPU信息获取     | cat /proc/cpuinfo | cat /proc/cpuinfo |
|      内存大小      | free -h | free -h |
|      硬盘数量以及容量      | df -h/ lsblk | df -h/ lsblk |

#### 在本地虚拟机安装 `asciinema` ：
```

sudo apt-get update
sudo apt-get install asciinema
asciinema auth

```
![asciinema_download](img/asciinema_download.png)

#### 在云环境安装`asciinema` ：

```
yum install -y  asciinema
asciinema auth
```
![remote_asciinema_install](img/remote_asciinema_install.png)

### 【软件包管理】在目标发行版上安装 tmux 和 tshark ；查看这 2 个软件被安装到哪些路径；卸载 tshark ；验证 tshark 卸载结果 ：

#### 在本地虚拟机操作：

##### `tmux`的安装以及查看路径：
```
sudo apt-get install tmux
which tmux
```
![local_tmux](img/local_tmux.png)
[![asciinema](https://asciinema.org/a/58lXA6BUBR9CZ8a3LkLrMW3Gp.svg)](https://asciinema.org/a/58lXA6BUBR9CZ8a3LkLrMW3Gp)

##### `tshark`的安装卸载、路径查看
```
sudo apt-get install tshark
which tshark
sudo apt-get remove --purge tshark
```
![local_tshark](img/local_tshark.png)

[![asciinema](https://asciinema.org/a/NVxrjKMyQ7luZHLoVsOMr0E0C.svg)](https://asciinema.org/a/NVxrjKMyQ7luZHLoVsOMr0E0C)

#### 在云环境操作：

##### `tmux`的安装以及查看路径：
```
yum install tmux
which tmux
```

![remote_tmux](img/remote_tmux.png)

[![asciinema](https://asciinema.org/a/bU5xVLXpdpIcvSdXza2zJeuQ2.svg)](https://asciinema.org/a/bU5xVLXpdpIcvSdXza2zJeuQ2)

##### `tshark`的安装卸载、路径查看

```
yum install wireshark
which tshark
yum -y remove wireshark
which tshark
```

![remote_tshark](img/remote_tshark.png)

[![asciinema](https://asciinema.org/a/rI1So3c7azhzAgoL91lQeJ5Sv.svg)](https://asciinema.org/a/rI1So3c7azhzAgoL91lQeJ5Sv)

### 【文件管理】复制以下 shell 代码到终端运行，在目标 Linux 发行版系统中构造测试数据集，然后回答以下问题：1.找到 /tmp 目录及其所有子目录下，文件名包含 666 的所有文件找到 2./tmp 目录及其所有子目录下，文件内容包含 666 的所有文件

#### 本地虚拟机操作:

将`shell`代码复制到终端运行：


`cd /tmp && for i in $(seq 0 1024);do dir="test-$RANDOM";mkdir "$dir";echo "$RANDOM" > "$dir/$dir-$RANDOM";done`

 ![add_shellcode](img/add_shellcode.png)
```
cd /tmp
sudo find ./ -name '*666*'
sudo grep -r '666' ./
```
![check_666](img/local_Check_666.png)

[![asciinema](https://asciinema.org/a/U67140cMxMqCUJXUyFCIMc4Gr.svg)](https://asciinema.org/a/U67140cMxMqCUJXUyFCIMc4Gr)

#### 云平台操作：

此处的指令和`Ubuntu 20.04`保持一致。

将`shell`代码复制到终端运行：

`cd /tmp && for i in $(seq 0 1024);do dir="test-$RANDOM";mkdir "$dir";echo "$RANDOM" > "$dir/$dir-$RANDOM";done`
```
cd /tmp
sudo find ./ -name '*666*'
sudo grep -r '666' ./
```

![remote_check_666](img/remote_check_666.png)
[![asciinema](https://asciinema.org/a/wLuDv7CsHqBOeCkN8181iTWv9.svg)](https://asciinema.org/a/wLuDv7CsHqBOeCkN8181iTWv9)

### 【文件压缩与解压缩】练习课件中 文件压缩与解压缩 一节所有提到的压缩与解压缩命令的使用方法

#### 本地虚拟机操作:

测试文件为 `test.txt`
`gzip`: 
```
gzip test.txt
gzip -d test.txt.gz
```
![local_gzip](img/local_gzip.png)

[![asciinema](https://asciinema.org/a/9NscPhjNXRpd36A3LQTqtH67j.svg)](https://asciinema.org/a/9NscPhjNXRpd36A3LQTqtH67j)

`bzip2`:
```
bzip2 -z test.txt
bzip2 -d test.txt.bz2
```
![local_bzip2](img/Local_bzip2.png)

[![asciinema](https://asciinema.org/a/1DQ6S7jZlUbvZBz6253Xx0lLj.svg)](https://asciinema.org/a/1DQ6S7jZlUbvZBz6253Xx0lLj)

`zip`:
```
zip test.txt.zip /tmp
unzip test.txt.zip
```
![local_zip](img/local_zip.png)

[![asciinema](https://asciinema.org/a/Jji3W9lbesAmSzoQajN5MKqy5.svg)](https://asciinema.org/a/Jji3W9lbesAmSzoQajN5MKqy5)

`tar`：
```
tar -czvf test-1.tar.gz test.txt
tar -xzvf test-1.tar.gz
```
![local_tar](img/local_tar.png)
[![asciinema](https://asciinema.org/a/i8PLFyYe4XJ8pfrITJOXLRYru.svg)](https://asciinema.org/a/i8PLFyYe4XJ8pfrITJOXLRYru)

`7z`:
```
7za a test.7z /test.txt
7za x test.7z
```
![local_7z](img/local_7z.png)
[![asciinema](https://asciinema.org/a/A2GweUV0c1xWGDddpGUuxSZF8.svg)](https://asciinema.org/a/A2GweUV0c1xWGDddpGUuxSZF8)


`rar`:

首先在本地主机上发送文件到虚拟机

通过scp指令将rar文件传输给云平台：`scp C:/Users/HUAWEI/Desktop/netclass.rar cuc@139.196.223.58:~/`

虚拟机执行
`unrar x netclass.rar`

![local_rar](img/local_rar.png)

[![asciinema](https://asciinema.org/a/rSX3CczF3q5GKXHLSCCEO4G2z.svg)](https://asciinema.org/a/rSX3CczF3q5GKXHLSCCEO4G2z)


#### 云平台操作：

测试文件为`test.txt`

通过`scp`指令将测试文件传输到云平台

`scp C:/Users/HUAWEI/Desktop/test.txt root@47.101.151.25:~/`

查看文件  `cat ./test.txt`

![remote_doc_txt](img/remote_doc_txt.png)
```
gzip:
gzip test.txt
gzip -d test.txt.gz
```
![remote_gzip](img/remote_gzip.png)

[![asciinema](https://asciinema.org/a/HTItsxrP54CAjCZ6w3MOwKIlP.svg)](https://asciinema.org/a/HTItsxrP54CAjCZ6w3MOwKIlP)
```
bzip2:
yum install bzip2
bzip2 -z test.txt
bzip2 -d test.txt.bz2
```
![remote_bzip2](img/remote_bzip2.png)

[![asciinema](https://asciinema.org/a/d7iwcO7Ih5vRBfU8me7xiiWd4.svg)](https://asciinema.org/a/d7iwcO7Ih5vRBfU8me7xiiWd4)
```
zip:
zip test.txt.zip /tmp
yum install unzip
unzip test.txt.zip
```
![remote_zip](img/remote_zip.png)

[![asciinema](https://asciinema.org/a/IDd0dxnJaxoAYIt1Rs23i87rg.svg)](https://asciinema.org/a/IDd0dxnJaxoAYIt1Rs23i87rg)
```
tar：
tar -czvf test-1.tar.gz test.txt
tar -xzvf test-1.tar.gz
```
![remote_tar(img/remote_tar.png)
[![asciinema](https://asciinema.org/a/KzMhPfpCkIthmnqQm1bX8iRQx.svg)](https://asciinema.org/a/KzMhPfpCkIthmnqQm1bX8iRQx)

```
7z:
yum install -y p7zip
7za a test.7z /test.txt
7za x test.7z
```
![remote_7z](img/remote_7z.png)
[![asciinema](https://asciinema.org/a/CDD2D5X1xwqF6C8a1eWCfCQkq.svg)](https://asciinema.org/a/CDD2D5X1xwqF6C8a1eWCfCQkq)

`rar`:

首先在本地上发送文件到云环境：

通过scp指令将rar文件传输给虚拟机`scp C:/Users/HUAWEI/Desktop/netclass.rar root@139.196.223.58:~/`

![remote_doc_rar](img/remote_doc_rar.png)

安装`rar`：

下载安装包：`wget --no-check-certificate http://www.rarlab.com/rar/rarlinux-x64-6.0.2.tar.gz`

解压安装包到目录：`tar xf rarlinux-x64-6.0.2.tar.gz -C /usr/local/`

创建软连接：
```
ln -s /usr/local/rar/rar /usr/local/bin/rar
ln -s /usr/local/rar/unrar /usr/local/bin/unrar
```
云平台执行
`unrar x netclass.rar`

[![asciinema](https://asciinema.org/a/dYvi61HL6O7U81GXlicmHabqa.svg)](https://asciinema.org/a/dYvi61HL6O7U81GXlicmHabqa)


### 【跟练】 子进程管理实验

#### 本地虚拟机：

![local_exercise](img/local_exercise.png)
[![asciinema](https://asciinema.org/a/UqkJXBY11vNnw7WVWq0hk8fW6.svg)](https://asciinema.org/a/UqkJXBY11vNnw7WVWq0hk8fW6)

#### 云平台操作：


![reomote_exercise](img/remote_exercise.png)
[![asciinema](https://asciinema.org/a/vyIt55qZ02sFFLCwelRUfCgtN.svg)](https://asciinema.org/a/vyIt55qZ02sFFLCwelRUfCgtN)


### 【硬件信息获取】目标系统的 CPU、内存大小、硬盘数量与硬盘容量

#### 本地虚拟机：

获取CPU信息 `cat /proc/cpuinfo`
获取内存信息 `free -h`
获取硬盘数量以及容量信息`df -h`
![local_checkinfo](img/local_checkinfo.png)

[![asciinema](https://asciinema.org/a/bNAzlRs7GR3A2HEh79EOBA4EM.svg)](https://asciinema.org/a/bNAzlRs7GR3A2HEh79EOBA4EM)

#### 云平台：
获取方式与`Ubuntu`一致
获取CPU信息 `cat /proc/cpuinfo`
获取内存信息 `free -h`
获取硬盘数量以及容量信息`df -h`
![remote_checkinfo](img/remote_checkinfo.png)

[![asciinema](https://asciinema.org/a/gWnCGZisZGBQfJTiORNeewfrx.svg)](https://asciinema.org/a/gWnCGZisZGBQfJTiORNeewfrx)


实验思考：
1.`tar`是打包，不是压缩。

2.`gzip`和`bzip2`将压缩包解压后，文件出现，这个压缩包消失。文件压缩时，压缩包也会替换文件。

3.`lsblk`相比`df -h`，能显示未挂载的硬盘，主要是用来查看块设备的。

4.直接用`yum`安装`tshark`，报错显示找不到。了解后发现，`tshark`是`wireshark`的一个工具，我们可以直接安装wireshark。

5.此次实验还是有些不足，相比上次，这次不再用中文命名图片，下次还可以更好的地方如附上参考链接的同时，标注是分享什么内容的，这样更友好。

6.此次也出现技术上的问题，就是`CentOS`上的`unrar`的使用。它是需要安装的，但是`yum`上没有相应的资源，不像那个`wireshark`。于是，就得搜寻各种安装方法，`wget http://www.rarlab.com/rar/rarlinux-x64-6.0.2.tar.gz`这个指令我开始尝试，发现到后面不行。然后换那个`rpm`,`pip`也都出现问题。我就想着冷静，看报错的提示，总会有办法的，看了一会发现可能是没有证书的意思。报错也提示了，可以以加上`--no-check-certificate`的形式去访问，然后确实能安装成功。但是发现解压不了，看了一下版本，应该是太低了。我就对比各个帮助网站的信息，成功下载了可用的版本，最后也能成功解压缩了。虽然耽误了不少时间，但也积累了宝贵的经验。
7.这次我觉得做得还比较好的地方就是对`asciinema`产生的录像软件也进行了相对整洁的命名。方便老师查看，也方便自己订正错误。
![asciinema_nam](img/asciinema_nam.png)

参考链接：

[linux查找指定内容文件](https://www.cnblogs.com/linjiqin/p/11678012.html)

[gzip命令_Linux gzip命令](http://c.biancheng.net/linux/gzip.html)

[linux下各种文件格式的压缩以及解压缩命令](https://www.cnblogs.com/cnland/p/3559042.html)

[linux查看硬盘信息](https://www.php.cn/linux-474598.html)

[Linux系统命令 - 查看内存使用情况](https://blog.csdn.net/renfufei/article/details/105851728)

[Linux-tshark抓包工具安装和使用](https://blog.csdn.net/carefree2005/article/details/122131633)
