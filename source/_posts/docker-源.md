---
title: docker-源
date: 2022-03-01 17:23:23
tags:
---
Docker在默认安装之后，通过命令docker pull 拉取镜像时，默认访问docker hub上的镜像，在国内网络环境下，下载时间较久或者拉取失败，所以要配置国内镜像仓库。

教程：


第一步.新建或编辑daemon.json

vi /etc/docker/daemon.json
第二部.编辑daemon.json文件填入一下内容 记得退出保存

{
"registry-mirrors": [
    "https://no1pfk8z.mirror.aliyuncs.com",
    "https://kfwkfulq.mirror.aliyuncs.com",
    "https://2lqq34jg.mirror.aliyuncs.com",
    "https://pee6w651.mirror.aliyuncs.com",
    "https://hub-mirror.c.163.com/",
    "https://reg-mirror.qiniu.com"
]
}

第三步.第三步：重启docker

systemctl restart docker.service
第四步.执行docker info查看是否修改成功

docker info
成功如下图



其他的加速地址如下：


##网易
http://hub-mirror.c.163.com
##Docker中国区官方镜像
https://registry.docker-cn.com
##中国科技大学
https://docker.mirrors.ustc.edu.cn
##阿里云容器  服务
https://cr.console.aliyun.com/
