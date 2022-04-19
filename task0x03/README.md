# 第三次作业

## 实验环境

`Ubuntu 20.04`

## 具体实验

###  [`systemd `入门教程：命令篇](http://www.ruanyifeng.com/blog/2016/03/systemd-tutorial-commands.html)

#### 查看`systemd`的版本

`systemctl --version`

![Check_Version](img/Check_Version.png)



#### `systemd-analyze`命令用来查看启动耗时

查看启动耗时

`systemd-analyze`

查看每个服务的启动耗时

`systemd-analyze blame`

显示瀑布状的启动过程流

`systemd-analyze critical-chain`

显示指定服务的启动流

`systemd-analyze critical-chain atd.service`

[![asciinema](https://asciinema.org/a/3NNlHTGcujCMZnSZ9PqOuH90D.svg)](https://asciinema.org/a/3NNlHTGcujCMZnSZ9PqOuH90D)

#### `hostnamectl`查看当前主机信息

显示当前主机的信息

`hostnamectl`

设置主机名

`sudo hostnamectl set-hostname taozi`

[![asciinema](https://asciinema.org/a/xclWDdIr93LIMDSAs14S6EBV2.svg)](https://asciinema.org/a/xclWDdIr93LIMDSAs14S6EBV2)

#### `localectl`查看本地化设置

查看本地化设置

`localectl`

设置本地化参数

`sudo localectl set-locale LANG=en_GB.utf8`
`sudo localectl set-keymap en_GB`

[![asciinema](https://asciinema.org/a/LNAl059zTGuRTT1gMgQ25DcRp.svg)](https://asciinema.org/a/LNAl059zTGuRTT1gMgQ25DcRp)

#### `timedatectl`查看当前时区设置

查看当前时区设置

`timedatectl`

显示所有可用的时区

`timedatectl list-timezones`

设置当前时区

`sudo timedatectl set-timezone America/New_York`
`sudo timedatectl set-time YYYY-MM-DD`
`sudo timedatectl set-time HH:MM:SS`

[![asciicast](https://asciinema.org/a/whABRrUiWLQdTYy6whwWrzmwP.svg)](https://asciinema.org/a/whABRrUiWLQdTYy6whwWrzmwP)

#### `loginctl` 查看当前登录的用户

列出当前`session`
`loginctl list-sessions`

列出当前登录用户
`loginctl list-users`

列出显示指定用户的信息
`loginctl show-user cuc`

[![asciicast](https://asciinema.org/a/SVhRLfODQZwqNsFJEWfkVFhV4.svg)](https://asciinema.org/a/SVhRLfODQZwqNsFJEWfkVFhV4)

#### `systemctl list-units`查看当前系统的所有Unit

列出正在运行的 `Unit`

`systemctl list-units`

列出所有`Unit`，包括没有找到配置文件的或者启动失败的

`systemctl list-units --all`

列出所有没有运行的 `Unit`

`systemctl list-units --all --state=inactive`

列出所有加载失败的 `Unit`

`systemctl list-units --failed`

列出所有正在运行的、类型为 
`service` 的 `Unit`

`systemctl list-units --type=service`

[![asciicast](https://asciinema.org/a/f9FEA3hB2vMO8hYncnCPiPghl.svg)](https://asciinema.org/a/f9FEA3hB2vMO8hYncnCPiPghl)

#### `systemctl status`查看系统状态和单个Unit


显示系统状态

`systemctl status`

显示单个 `Unit` 的状态

`systemctl status dbus.service`

显示远程主机的某个 `Unit` 的状态


![remote_machine](img/Remote_machine.png)


`systemctl -H root@47.116.69.106 status dbus.service`

[![asciicast](https://asciinema.org/a/ePePRMDXatCFAygIgfN0u7Dcq.svg)](https://asciinema.org/a/ePePRMDXatCFAygIgfN0u7Dcq)

#### `systemctl`提供查询状态的其他三个方法

显示某个 `Unit` 是否正在运行

`systemctl is-active application.service`

显示某个 `Unit` 是否处于启动失败状态

`systemctl is-failed application.service`

显示某个 `Unit` 服务是否建立了启动链接

`systemctl is-enabled application.service`

[![asciicast](https://asciinema.org/a/kZ9aFzSzwikiJBDBvY9QCilJz.svg)](https://asciinema.org/a/kZ9aFzSzwikiJBDBvY9QCilJz)

#### `Unit`管理命令

立即启动一个服务

`sudo systemctl start apache.service`

立即停止一个服务

`sudo systemctl stop apache.service`

重启一个服务

`sudo systemctl restart apache.service`

杀死一个服务的所有子进程

`sudo systemctl kill apache.service`

重新加载一个服务的配置文件

`sudo systemctl reload apache.service`

重载所有修改过的配置文件

`sudo systemctl daemon-reload`

显示某个 `Unit` 的所有底层参数

`systemctl show httpd.service`

显示某个` Unit` 的指定属性的值

`systemctl show -p CPUShares httpd.service`

设置某个 `Unit` 的指定属性

`sudo systemctl set-property httpd.service CPUShares=500`

[![asciicast](https://asciinema.org/a/p8IiJotDquRIuEKPca4kla6gs.svg)](https://asciinema.org/a/p8IiJotDquRIuEKPca4kla6gs)

#### `Unit`的依赖关系

列出一个 `Unit`的所有依赖

`systemctl list-dependencies nginx.service`

展开`target`类型的依赖

`systemctl list-dependencies --all nginx.service`

[![asciicast](https://asciinema.org/a/c1CSpng92uA9jtQQe5WaBm2IW.svg)](https://asciinema.org/a/c1CSpng92uA9jtQQe5WaBm2IW)

#### `systemd`启动 `Unit`

开机启动
`sudo systemctl enable apache2.service`

`sudo ln -s '/usr/lib/systemd/system/apache2.service'`

撤销开机启动

`sudo systemctl disable apache2.service`

[![asciicast](https://asciinema.org/a/TMeuDsFaHtUkIozfn62ZlcpLx.svg)](https://asciinema.org/a/TMeuDsFaHtUkIozfn62ZlcpLx)

#### `systemctl list-unit-files`用于列出所有配置文件 

列出所有配置文件

`systemctl list-unit-files`

列出指定类型的配置文件

`systemctl list-unit-files --type=service`

[![asciicast](https://asciinema.org/a/Fhc2Wz8doKxVrG5e3Iwawm22l.svg)](https://asciinema.org/a/Fhc2Wz8doKxVrG5e3Iwawm22l)

#### `systemctl cat`查看配置文件内容

`systemctl cat atd.service`

![check_disposition](img/check_disposition.png)


#### `target`

查看当前系统的所有 `Target`

`systemctl list-unit-files --type=target`

查看一个 `Target` 包含的所有 `Unit`

`systemctl list-dependencies multi-user.target`

查看启动时的默认 `Target`

`systemctl get-default`

设置启动时的默认 `Target`

`sudo systemctl set-default multi-user.target`

切换 `Target` 时，默认不关闭前一个 `Target` 启动的进程，
`systemctl isolate` 命令改变这种行为,关闭前一个 `Target` 里面所有不属于后一个 `Target `的进程

`sudo systemctl isolate multi-user.target`

[![asciicast](https://asciinema.org/a/9xW99mH1HqHwKCSLi7qmMIwqj.svg)](https://asciinema.org/a/9xW99mH1HqHwKCSLi7qmMIwqj)

#### `journalctl`查看所有日志

查看所有日志（默认情况下 ，只保存本次启动的日志）

`sudo journalctl`

查看内核日志（不显示应用日志）

`sudo journalctl -k`

查看系统本次启动的日志


`sudo journalctl -b`
`sudo journalctl -b -0`

查看上一次启动的日志（需更改设置）

`sudo journalctl -b -1`

查看指定时间的日志

`sudo journalctl --since="2022-4-4 18:17:16"`

`sudo journalctl --since "20 min ago"`

`sudo journalctl --since yesterday`

`sudo journalctl --since "2022-04-03" --until "2022-04-04 22:00"`

`sudo journalctl --since 09:00 --until "1 hour ago"`

显示尾部的最新10行日志

`sudo journalctl -n`

显示尾部指定行数的日志

`sudo journalctl -n 20`

实时滚动显示最新日志

`sudo journalctl -f`

查看指定服务的日志

`sudo journalctl /usr/lib/systemd/systemd`

查看指定进程的日志

`sudo journalctl _PID=1`

查看某个路径的脚本的日志

`sudo journalctl /usr/bin/bash`

查看指定用户的日志

`sudo journalctl _UID=33 --since today`

查看某个 `Unit` 的日志

`sudo journalctl -u nginx.service`

`sudo journalctl -u nginx.service --since today`

实时滚动显示某个 `Unit` 的最新日志

`sudo journalctl -u nginx.service -f`

合并显示多个 `Unit` 的日志

`journalctl -u nginx.service -u php-fpm.service --since today`

查看指定优先级（及其以上级别）的日志，共有8级

`sudo journalctl -p err -b`

日志默认分页输出，`--no-pager` 改为正常的标准输出

`sudo journalctl --no-pager`

以 `JSON` 格式（单行）输出

`sudo journalctl -b -u nginx.service -o json`

以 `JSON` 格式（多行）输出，可读性更好

`sudo journalctl -b -u nginx.serviceqq -o json-pretty`

显示日志占据的硬盘空间

`sudo journalctl --disk-usage`

指定日志文件占据的最大空间

`sudo journalctl --vacuum-size=1G`

指定日志文件保存多久
`sudo journalctl--vacuum-time=1years`

[![asciicast](https://asciinema.org/a/umhpT2RVhSYOYyIXjIdtXrIn3.svg)](https://asciinema.org/a/umhpT2RVhSYOYyIXjIdtXrIn3)

### [`systemd`入门教程：实战篇](http://www.ruanyifeng.com/blog/2016/03/systemd-tutorial-part-two.html)

#### 开机启动、启动服务以及停止服务

`sudo systemctl enable apache2`

`sudo systemctl start apache2`

`sudo systemctl status apache2`

`sudo systemctl stop apache2.service`

`sudo systemctl kill apache2.service`

`sudo systemctl restart apache2.service`

[![asciicast](https://asciinema.org/a/OsjrCo7Spn0PjaGibdBjCV3vR.svg)](https://asciinema.org/a/OsjrCo7Spn0PjaGibdBjCV3vR)

#### 查看配置文件

`systemctl cat sshd.service`

![sshd.disposition](img/sshd.disposition.png)

#### 启动的target

查看 `multi-user.target` 包含的所有服务

`systemctl list-dependencies multi-user.target`

切换到另一个 `target`

`sudo systemctl isolate shutdown.target`

[![asciicast](https://asciinema.org/a/MN8341yUDO510nTrCt4V3bxny.svg)](https://asciinema.org/a/MN8341yUDO510nTrCt4V3bxny)

#### 修改配置后重启

重新加载配置文件

`sudo systemctl daemon-reload`

重启相关服务

`sudo systemctl restart apache2`

![apache_new](img/apache_new.png)

### 具体实验内容

#### 如何添加一个用户并使其具备`sudo`执行程序的权限？

`sudo adduser taozi`

`sudo usermod -G sudo taozi`

[![asciicast](https://asciinema.org/a/a5kIJceODTFeTdBZdZh1Xa1q6.svg)](https://asciinema.org/a/a5kIJceODTFeTdBZdZh1Xa1q6)

`groups taozi`

![Add_user](img/Add_user.png)

#### 如何将一个用户添加到一个用户组

`usermod -a -G <group_name> <user_name>`

![User_groups](img/user_Groups. png)

#### 如何查看当前系统的分区表和文件系统详细信息？

`df -h`

![df-check](img/df_check.png)

`sudo fdisk -l`

[![asciicast](https://asciinema.org/a/Sqdxz8LAmhq5nsHclC3OjopJm.svg)](https://asciinema.org/a/Sqdxz8LAmhq5nsHclC3OjopJm)


#### 如何实现开机自动挂载Virtualbox的共享目录分区？

在`windows`上创建一个共享文件夹，我的目录为`D:\ VirtualBox_share`

![virtual_box_share](img/Virtualbox_Share.png)

新建共享文件夹的配置情况

![Share_disposition](img/Share_disposition.png)

`sudo mkdir /mnt/share`

`sudo mount -t vboxsf VirtualBox_share /mnt/share/`

`cd /mnt/share`

![cat_info](img/cat_info.png)

`sudo vim /etc/fstab`

修改相关配置，添加上最后一行代码，并保存退出

![start_disposition](img/start_disposition.png)


#### 基于`LVM`（逻辑分卷管理）的分区如何实现动态扩容和缩减容量

增加一个虚拟硬盘

![Add_harddisk](img/Add_harddisk.png)

依次增加两个硬盘

![Add_harddisk_2](img/Add_harddisk_2.png)

`lsblk`

![lsblk_1](img/lsblk_1.png)

物理硬盘分区并写入

![sdb_p_1](img/sdb_p_1.png)

![sdc_p_1](img/sdc_p_1.png)

`lsblk`

![lsblk_2](img/lsblk_2.png)

在指定分区创建文件系统

![mkfs.ext4_1](img/mkfs.ext4_1.png)

未挂载前 `df-h`

![df-h_1](img/df_h_1.png)

依次挂载

![mount_1](img/mount_1.png)

挂载后`df -h`

![df-h_2](img/df-h_2.png)

依次卸载硬盘分区

![unmount_1](img/unmount_1.png)

创建物理卷

![pvscan](img/PVscan_1.png)

卷组的创建与扩展

![VG-create-extend](img/VG-create.png)

创建逻辑卷并查看信息

![lv_create](img/lv_create.png)

`lsblk`

![lsblk_3](img/lsblk_3.png)

`lvscan`

![lvscan](img/lvscan.png)

给此逻辑卷扩容`1G`

`lvextend -L +1G /dev/taozi-vg/taozi-lv-1`

![lvextend_1](img/lvextend_1.png)

给此逻辑卷减容`3G`

`lvreduce -L -3G /dev/taozi-vg/taozi-lv-1`

![lvreduce](img/lvreduce.png)

#### 如何通过`systemd`设置实现在网络连通时运行一个指定脚本，在网络断开时运行另一个脚本？

[![asciicast](https://asciinema.org/a/rCWcr4H5sl8HjfpQLlxL50tn0.svg)](https://asciinema.org/a/rCWcr4H5sl8HjfpQLlxL50tn0)


#### 如何通过systemd设置实现一个脚本在任何情况下被杀死之后会立即重新启动？实现杀不死？

修改一下相应脚本的服务配置文件

[`service`]

`Restart=always`

然后用到上面学到的知识

`sudo systemctl daemon-reload`

再重新启动该服务即可

`sudo systemctl restart XXXXX`


### 实验反思

1.我跟着作者阮一峰的网络日志进行相关训练的时候，其实也出现了一些问题。比如说有的包我们没有装上，发现`sudo apt-get install xxx`也不行，要安装好像还很麻烦，我就只能用别的软件去替代，这样简单一点。比如说`apache`我就用`apache2`代替，`bluetooth`我就用查看`service`时找到的`dbus`来代替。

2.跟随训练的时候还出现了一个问题，就是`sudo timedatectl set-time YYYY-MM-DD`这样一条指令报错了。错误反馈为`Failed to parse time specification 'YYYY-MM-DD': Invalid argument` 。我当时就复制到`baidu`上看，找不到类似的错误，后来在畅课讨论区才得到相关结果。原来说是参数无效，得用具体的数字去替代。而且我也明白修改电脑的时间意味着什么，我提前备份了，但是没想到会一直报错。感谢老师还提供了时间同步校准的方法。

3.最后这次实验还有点糊涂的地方应该就是网络状态的不同脚本那里了，不过下一个章节就讲相关的内容了，学到了应该就会有更深的理解了吧。



###  参考链接

[`Ubuntu`添加一个具有`sudo`权限的用户](https://blog.csdn.net/breeze5428/article/details/52837768)

[`Linux`查看用户组有哪些用户](https://www.sohu.com/a/332316655_495675)

[`Linux`查看磁盘分区，文件系统](https://blog.51cto.com/u_13233/82677)

[`Virtualbox`实现共享文件夹并自动挂载](https://blog.csdn.net/hexf9632/article/details/93774198)

[`Linux`之`systemd`服务配置及自动重启](https://www.cnblogs.com/nxzblogs/p/11755972.html)