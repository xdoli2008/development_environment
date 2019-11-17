# 加速国内Github访问速度

## [原作者](https://bestzuo.cn/posts/497652030.html)

>由于某些原因，国内访问 Github 会异常缓慢，在 clone 仓库时甚至只有 10kb/s 以下的速度，下载半天有时还会失败需要从头再来，甚是让人恼火。 本文介绍通过修改系统 hosts 文件的办法，绕过国内 DNS 解析，直接访问GitHub 的 CDN 节点，从而达到加速的目的。不需要科学上网，也不需要海外的服务器辅助。

## 获取Github的官方CDN地址

打开 `https://www.ipaddress.com/` 查询以下三个链接的的 DNS 地址：

+ `github.com`
+ `assets-cdn.github.com`
+ `github.global.ssl.fastly.net`

*记录下查询到的 IP 地址。*

## 修改系统hosts文件

>打开系统 hosts 文件(需管理员权限)。 路径： `C:\Windows\System32\drivers\etc` windows10 可以将 hosts 文件复制到桌面进行修改后覆盖原文件，windows7 使用管理员权限即可。在末尾添加三行记录并保存。(需管理员权限，注意 IP 地址与域名间需留有空格)

```text
# Copyright (c) 1993-2009 Microsoft Corp.
#
# This is a sample HOSTS file used by Microsoft TCP/IP for Windows.
#
# This file contains the mappings of IP addresses to host names. Each
# entry should be kept on an individual line. The IP address should
# be placed in the first column followed by the corresponding host name.
# The IP address and the host name should be separated by at least one
# space.
#
# Additionally, comments (such as these) may be inserted on individual
# lines or following the machine name denoted by a '#' symbol.
#
# For example:
#
#      102.54.94.97     rhino.acme.com          # source server
#       38.25.63.10     x.acme.com              # x client host

# localhost name resolution is handled within DNS itself.
#   127.0.0.1       localhost
#   ::1             localhost

  192.30.253.112     github.com

  151.101.72.133    assets-cdn.github.com

  151.101.193.194    github.global.ssl.fastly.net
```

## 刷新系统DNS缓存

>Windows+X 打开系统命令行（管理员身份）或 powershell运行 `ipconfig /flushdns` 手动刷新系统 DNS 缓存。现在打开 Github，clone 一个项目到本地试试吧！
