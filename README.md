细刻doc文档
==========


1.Mac工具安装
-----------

使用Mac需要安装应用的命令

> **Note**
> - Xcode: 在APP Store即可下载
> - Homebrew: 是Mac OSX上的软件包管理工具，能在Mac中方便的安装软件或者卸载软件
> - Homebrew Install:
```sh
$ ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```
> - 查看安装应用，包括版本号: 
```sh
$ brew list --versions
```
> - Homebrew Cask(Homebrew扩展): 
```sh
$ brew install caskroom/cask/brew-cask
```
> - Homebrew 安装应用demo: 
```sh
$ brew cask install google-chrome
```
> - Tip: Homebrew Cask网页链接 <i class="icon-upload"></i> http://sourabhbajaj.com/mac-setup/Homebrew/Cask.html.


2.本地服务环境配置
------------------

> **Note**
> **在启动你的 Homestead 环境之前，你必须先安装 VirtualBox 和 Vagrant.**
> - virtualbox install: 
```sh
$ brew install Caskroom/cask/virtualbox
```
> - Vagrant install: 
```sh
$ brew install Caskroom/cask/vagrant
```
> - Homestead配置(laravel链接说明): http://laravel-china.org/docs/5.0/homestead


3.代码部署配置
--------------

> **Note**
> **获取代码之前先安装git应用**
> - git install: 
```sh
$ brew install Caskroom/cask/git
```
> - git的一些使用方法: http://git-scm.com/docs/gittutorial
> - git的提交原理: https://git-scm.com/book/en/v2/Getting-Started-Git-Basics
