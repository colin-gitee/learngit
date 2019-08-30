## Linux

### 网络设置
在最小版安装后，centos没有联网，联网方法:
```shell
# 进入路径
cd /etc/sysconfig/network-scripts/
# 编译文件，可能不完全一样
vi ifcfg-ens33
```

```shell
# 配置网卡信息
BOOTPROTO="none"
ONBOOT="yes"
IPADDR="192.168.100.100"
PREFIX="24"
GATEWAY="192.168.100.2"
DNS1="8.8.8.8"
```

```shell
# 重启网卡
service network restart
```

---

### 源设置
centos默认为国外源，速度很慢，可以更换为国内源
```shell
yum install -y wget

# 备份你的原镜像文件,出错后还可以恢复
mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.backup
# 下载新的CentOS-Base.repo到/etc/yum.repos.d/
wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-6.repo
# wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo
# 生成缓存
yum makecache
# 清除缓存
yum clean all
```

```shell
# 扩展源
wget -O /etc/yum.repos.d/epel.repo http://mirrors.aliyun.com/repo/epel-6.repo
# wget -O /etc/yum.repos.d/epel.repo http://mirrors.aliyun.com/repo/epel-7.repo

# 验证是否成功
yum repolist
```

---
### 交换空间
```shell
#!/bin/bash

# 查看交换空间
# free -m
# grep SwapTotal /proc/meminfo
cat /proc/swaps

# ---of：输出的交换文件的路径及名称；
# ---bs：块大小，单位byte，1024=1k
# ---count：总块数即空间总大小，单位为块即kb；
# ---if：读取的源空闲空间
# 1Kb * 2048Mb = 2Gb 加上原有的2Gb，刚好4Gb
dd if=/dev/zero of=/swap bs=1024 count=2048000

# 将swap设置为swap空间
mkswap /swap

# 启用交换空间，这个操作有点类似于mount操作
swapon /swap
# 如果不再使用空间可以选择关闭交换空间,这个操作有点类似于umount操作
# swapoff swap
echo "/sbin/swapon /swap" >> /etc/rc.d/rc.local
```

