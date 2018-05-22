---
group: install2
subgroup: Getting Started
title: 如何使用终端、命令行或ssh登录到我的Magento服务器
menu_title: 如何使用终端、命令行或ssh登录到我的Magento服务器
menu_node:
menu_order: 105
level3_menu_node: level3child
level3_subgroup: basics
version: 2.1
github_link: install-gde/basics/basics_login.md
redirect_from: /guides/v1.0/install-gde/basics/basics_login.html
functional_areas:
  - Install
  - System
  - Setup
---

<!-- This topic is referred to from Magento 2 code! Don't change the {% glossarytooltip a05c59d3-77b9-47d0-92a1-2cbffe3f8622 %}URL{% endglossarytooltip %} without informing engineering! -->
<!-- Referring file: README.md owned by core -->

在这个手册中几乎所有的要完成的作务都必须远程地登录到你的Magento服务器 

**先决条件**: 你必须有:

*	一个终端应用程序

	Windows和Mac OS用的是不同的终端应用程序. 
	
	*	Windows: 你可以选: <a href="http://www.putty.org/" target="_blank">putty</a>, <a href="https://www.cygwin.com/" target="_blank">Cygwin</a>
	
	*	Mac OS: 你可以使用自带的<a href="http://en.wikipedia.org/wiki/Terminal_(OS_X)" target="_blank">终端</a>或以下之一: <a href="http://iterm2.com/" target="_blank">iTerm</a>和<a href="http://computers.tutsplus.com/tutorials/beyond-terminal-4-os-x-terminal-alternatives--mac-56217" target="_blank">these</a>
	
*	Magento服务器的登录用户名和密码
	

	在一个托管理的每中, 可能是一个没有管理员权限的普通用户; 不过没关系只要这个用户可以安装系统的软件，可以开启和停止诸如web服务的服务等就可以了。 
	
	如果是你自己的服务器，你或你的系统管理员通常可以使用<a href="http://www.linfo.org/root.html" target="_blank">root</a>身份登录, 在Linux上这个用户拥有整个系统的管理权限

使用终端应用程远程登录到Magento服务器:

1.	根据这个应用的提供的文档配置好你的终端应用程序.
2.	启动终端应用程序.
3.	根据提示输入你的Magento服务器的主机名或IP地址.
4.	使用得到的用户名和密码登录到你的服务器.

下图展示了当你用root在Windows的Cygwin上登入到你的服务器的样子.

<img src="{{ site.magentourl }}/common/images/install_cygwin.png" alt="用root在Windows的Cygwin上登入到你的服务器">

<div class="bs-callout bs-callout-info" id="info">
<span class="glyphicon-class">
  <p><a href="http://en.wikipedia.org/wiki/Secure_Shell" target="_blank">Secure Shell (ssh)</a>是一种可以不通可用户名和密码安全连接到你的服务器的协议，它防止了在网络上直接传输你的用户名和密码。</p></span>
</div>
	
