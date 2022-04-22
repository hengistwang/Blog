+++
title = "Linux_Commands"
author = ["hengist"]
date = 2022-04-23T00:00:00+08:00
lastmod = 2022-04-23T02:02:10+08:00
tags = ["Linux"]
draft = false
+++

OS: openSUSE Tumbleweed

```shell
#清理无用的软件包
zypper -tqn --no-refresh pa --unneeded |grep '^i |' |awk -F "|" '{print $3}' |xargs sudo zypper rm -u
#后台执行
nohup ./shell.sh > nohup.out 2>&1 &
#生成指定长度的随机字符串
openssl rand -hex 1000
```
