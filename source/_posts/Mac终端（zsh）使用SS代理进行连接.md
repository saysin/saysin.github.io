---
title: Mac终端（zsh）使用SS代理进行连接
date: 2019-10-13 20:20:50
categories: 计算机技巧
tags: Mac
---
平时我们在使用SS代理服务后，浏览器可以正常fan墙使用，但是在终端里面使用git/brew/pip等命令时，速度却是出奇的慢，实际上这是由于虽然SS设置了全局设置，但是并没有把全局设置传递到终端。我们需要一些设置使得终端也能正确使用SS代理服务。
SS搭建问题在这里不进行展开叙述，网上教程也很多，也有现成的SS服务可以购买。
下面对终端设置SS代理服务进行简单的阐述。
# 1.开启SS
    SS:shadowsocks
# 2.检查代理状态
    curl https://ip.cn
    curl curl ipinfo.io #备用查询接口
# 3.打开SS设置
获取设置内容高级项中，SS所监听的端听IP以及监听端口
# 4.编辑zsh配置文件
    vim ~/.zshrc 
使用socks5协议对刚才获取到的监听IP与监听端口进行拼接
    socks5://(IP):(端口)
添加以下内容到配置文件内 (使用刚才拼接好的地址)
    alias proxy='export all_proxy=socks5://127.0.0.1:1080'#用于开启终端代理
    alias unproxy='unset all_proxy'#用于关闭终端代理
保存退出后
    source ~/.zshrc
# 5.应用配置
    proxy #开启终端代理
    curl https://ip.cn #发现此时ip地址发生了变化，说明终端代理设置成功
注意：不能使用ping检测是否成功代理:
ss基于的SOCKS 5代理协议,支持TCP和UDP服务。而ping是基于icmp协议的,因此在ss下不能使用ping作为检测标准。
# 6.关闭终端代理
在使用国内镜像源的时候，需要把终端代理关闭，要不然无法进行更新与下载
    unproxy #关闭终端代理

