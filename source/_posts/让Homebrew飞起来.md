---
title: 让Homebrew飞起来
date: 2019-10-07 20:05:14
categories: 计算机技巧
tags: homebrew
---
国内homebrew连接速度不稳定，brew update 经常卡死，可以通过替换镜像源的方式提高连接的稳定性。
```
cd  $(brew --repo)  #进入 homebrew 根目录
git remote set-url origin  https://mirrors.ustc.edu.cn/brew.git #替换brew远程库
cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core"
git remote set-url origin https://mirrors.ustc.edu.cn/homebrew-core.git #替换 home-brew 远程库
echo "export HOMEBREW_BOTTLE_DOMAIN=https://mirrors.ustc.edu.cn/homebrew-bottles">>~/.zshrc #替换bottles源,根据 bash 的不同有区别
source ~/.zshrc
brew update #应用
```
# 国内源
中科大:https://mirrors.ustc.edu.cn/brew.git

清华大学:https://mirrors.tuna.tsinghua.edu.cn/help/homebrew/
