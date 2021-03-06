---
layout: post
title: shell logrotate
subtitle:
date: 2019-09-07 16:31:21
category: 日志切割和清理
author: meetbill
tags:
   -
---

## shell logrotate


<!-- vim-markdown-toc GFM -->

* [1 功能](#1-功能)
* [2 使用](#2-使用)
    * [2.1 启动管理](#21-启动管理)
    * [2.2 配置管理](#22-配置管理)
    * [2.3 logrotate 日志](#23-logrotate-日志)
* [3 番外](#3-番外)
    * [find 中的 mtime 参数](#find-中的-mtime-参数)

<!-- vim-markdown-toc -->

## 1 功能

每小时进行切割和清理通用日志

## 2 使用
### 2.1 启动管理

```
$sh log_control.sh

Usage: log_control.sh {start|stop|restart|status}
  start   Start logrotate processes.
  stop    Kill all logrotate processes.
  restart Kill all logrotate processes and start again.
  status  Show logrotate processes status.
  version Show log_control.sh script version.
```

### 2.2 配置管理

logrotate_exe.sh
```
# app 主目录，即以此脚本为 base 路径，进行设置 APP_HOME
APP_HOME=${CUR_DIR}/..
LOG_PATH="${APP_HOME}/log"

#任务
LOG_KEEP_TIME="7"                              # 保存天数
LOG_PATH="${NGINX_LOG_PATH}/nginx.access_log"  # 日志路径
LOG_BACK_DIR=$(dirname ${LOG_PATH})            # 备份日志的路径
END_CMD=""                                     # 需要执行的额外命令
log_cut                                        # 日志切割和清理
```
### 2.3 logrotate 日志

> 启动日志
```
log/__logrotate_stdout
```
> 运行日志
```
默认存放在此目录的 log 目录
```

## 3 番外

### find 中的 mtime 参数

> find . –mtime n
```
File waslast modified n*24 hours ago.
最后一次修改发生在距离当前时间n*24小时至(n+1)*24 小时
```

> find . –mtime +n

```
最后一次修改发生在n+1天以前，距离当前时间为(n+1)*24小时或者更早
```

> find . –mtime –n
```
最后一次修改发生在n天以内，距离当前时间为n*24小时以内
```
