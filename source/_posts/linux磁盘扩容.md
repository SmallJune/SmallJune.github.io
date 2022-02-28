---
title: Linux 更改root与home分区大小的方法总结
date: 2022-02-28 09:37:39
tags:
---

### 安装了CentOS7.5的虚拟机 但是发现里面的操作系统 home 分区占到了400g 根分区只有50g 认为不太好,所以要改一下.

### 方法. 好像是xfs的文件格式, 没法使用resize2fs 的方式进行处理, 需要使用 xfs_growfs 的方式处理

### 方法: df -h 查看磁盘情况

```
root@ningxia-100.127.1.225-proxy gse#df -h
文件系统                 容量  已用  可用 已用% 挂载点
devtmpfs                 3.8G     0  3.8G    0% /dev
tmpfs                    3.9G     0  3.9G    0% /dev/shm
tmpfs                    3.9G  407M  3.5G   11% /run
tmpfs                    3.9G     0  3.9G    0% /sys/fs/cgroup
/dev/mapper/centos-root  400G   48G  353G   12% /
/dev/vda1               1014M  242M  773M   24% /boot
tmpfs                    782M   12K  782M    1% /run/user/42
/dev/mapper/centos-home   50G   33M   50G    1% /home
```

### 然后使用

mount |grep home
查看 home分区的文件格式
```
root@ningxia-100.127.1.225-proxy gse#mount |grep home
/dev/mapper/centos-home on /home type xfs (rw,relatime,attr2,inode64,noquota)

```

### 卸载home分区
```
umount /home
```


### 删除home的lv
```
lvremove /dev/mapper/centos-home
```
选择是 进行操作

### 扩展root分区的大小
```
lvextend -L +350G /dev/mapper/centos-root
```

### 进行 xfs_growfs
```
xfs_growfs /dev/centos/root 
```

### 创建home的lv

```
lvcreate -L 50GB -n home centos
```

### 创建文件系统
```
mkfs.xfs /dev/centos/home
```

### 挂载
```
mount /dev/mapper/centos-home`

```

