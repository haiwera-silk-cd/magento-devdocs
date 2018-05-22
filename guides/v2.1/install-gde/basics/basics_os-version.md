---
group: install2
title: 我的服务器是什么操作系统?
version: 2.1
github_link: install-gde/basics/basics_os-version.md
redirect_from: /guides/v1.0/install-gde/basics/basics_os-version.html
functional_areas:
  - Install
  - System
  - Setup
---
 
 
如何辨别你的Magento服务用的什么操作系统，是什么版本？

**先决条件**: 你必须可以通过访问服务器的命令提符(允许你在上面输入并执行命令的应用程序). 

如果你可以直接登录上这个机器，这个应用程序通常称为Terminal(终端)

如果不能直接登录，可以参考<a href="{{ page.baseurl }}/install-gde/basics/basics_login.html">远程地登录到你的服务器</a>.

## Exact command or process of elimination?

如果你已经知道了你的操作系统，是Ubuntu或CentOS，但你还不能确定是什么版本，下面将逐一说明。如果两个都不是，那就用排除法把命令都运行一遍直到找到能正确运行的命令.

### CentOS

可以通过在终端执行下面的的命令，确定CentOS的版本：

	cat /etc/*release*

下面是在CentoOS 6.5上执行的示例输出（你可以大部分）

	CentOS release 6.5 (Final)
	LSB_VERSION=base-4.0-amd64:base-4.0-noarch:core-4.0-amd64:core-4.0-noarch:graphics-4.0-amd64:graphics-4.0-noarch:printing-4.0-amd64:printing-4.0-noarch
	cat: /etc/lsb-release.d: Is a directory
	CentOS release 6.5 (Final)
	CentOS release 6.5 (Final)

### Ubuntu

要知道Ubuntu的版本，在终端执行下面的命令

	lsb_release -a

下面是在Ubuntu 14上执行的示例输出:

	No LSB modules are available.
	Distributor ID: Ubuntu
	Description:    Ubuntu 14.04.1 LTS
	Release:        14.04
	Codename:       trusty



