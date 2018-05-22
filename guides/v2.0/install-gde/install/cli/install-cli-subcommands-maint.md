---
group: install_cli
subgroup: 05_Command-line installation
title: 开启或关闭维护模式
menu_title: 开启或关闭维护模式
menu_node:
menu_order: 10
version: 2.0
github_link: install-gde/install/cli/install-cli-subcommands-maint.md
redirect_from:
  - /guides/v1.0/install-gde/install/install-cli-subcommands-maint.html
  - /guides/v2.0/install-gde/install/install-cli-subcommands-maint.html
functional_areas:
  - Install
  - System
  - Setup
---

<h2 id="instgde-cli-before">第一步</h2>
{% include install/first-steps-cli.html %}
我们不止在这里讨论命令参数，更多请参考<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands.html#instgde-cli-subcommands-common">命令参数</a>.

<h2 id="instgde-cli-subcommands-maint-prereq">先决条件</h2>
在使用这个命令之前，你必须 <a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-install.html">安装Magento</a>.

<h2 id="instgde-cli-maint">开启或关闭维护模式</h2>
Magento使用*维护模式*来禁用引导，例如，此时你正在维护，升级或配置你的网站。 

Magento用下面的方式检测是否处于维护模式：

*	如果`var/.maintenance.flag`文件不存在表示维护模式是关闭的，此时Magento的可正常操作
*	否则，维护模式是开启的，除非`var/.maintenance.ip`文件存在：

	`var/.maintenance.ip`可以包含一个ip地址列表，如果客户端通过ip地址访问并且这个客户端地址在列表中，那么对这个客户来说，维护模式是关的。

命令用法：

	magento maintenance:enable [--ip=<ip address> ... --ip=<ip address>] | [ip=none]
	magento maintenance:disable [--ip=<ip address> ... --ip=<ip address>] | [ip=none]
	magento maintenance:status

where

`--ip=<ip address>`指定一个不进入维护模式的ip(比如正在维护的开发者). 要在一个命令中指定多个IP，可多次使用这个选项。

<div class="bs-callout bs-callout-info" id="info">
<span class="glyphicon-class">
  <ul><li>使用<code>--ip=&lt;ip地址></code> with <code>magento maintenance:disable</code> 表示你仅仅保存这个地址为下次开启维护模式时使用。</li>
  	<li>要清除这个白名单，你可以命名用<code>magento maintenance:enable --ip=none</code>或参考<a href="#instgde-cli-maint-exempt">维护模式IP地址白名单</a>.</li></ul></span>
</div>

`magento maintenance:status`来显示当前维护模式是否开启.

例如，要开启维护模式而不使用ip白名单：

	magento maintenance:enable

开启维护模式，并将192.0.2.10和192.0.2.11加入白名单中：

	magento maintenance:enable --ip=192.0.2.10 --ip=192.0.2.11

<h2 id="instgde-cli-maint-exempt">维护模式IP地址白名单</h2>
要维护这个IP白名单，你即可以使用前面提到命令并加上`[--ip=<ip list>]`选项，也可以使用下面的命令：

	magento maintenance:allow-ips <ip address> .. <ip address> [--none]

where 

`<ip address> .. <ip address>`是一个可选的空格隔开要加入白名单的的ip地址的列表。 

`--none`清除白名单.


#### 相关主题

*	<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-install.html">使用命令行安装Magento</a>
*	[移除样本数据模块或更新样本数据]({{ page.baseurl }}/install-gde/install/cli/install-cli-sample-data-other.html)
*	[启用或禁用模块]({{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands-enable.html)
*	[显示或更改管理面板的URI]({{ page.baseurl }}/install-gde/install/cli/install-cli-adminurl.html)
*	[卸载模块]({{ page.baseurl }}/install-gde/install/cli/install-cli-uninstall-mods.html)
*	<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands-deployment.html">建立或更新布署配置</a>
*	<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands-db.html">创建Magento的数据库表结构</a>
*	[更新数据库表结构和数据]({{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands-db-upgr.html)
*	<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands-store.html">配置网店</a>
*	<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands-admin.html">创建或解锁Magento管理员</a>
*	[备份和还原文件系统，媒体文件和数据库]({{ page.baseurl }}/install-gde/install/cli/install-cli-backup.html)
*	[卸载主题]({{ page.baseurl }}/install-gde/install/cli/install-cli-theme-uninstall.html)
*	[卸载语言包]({{ page.baseurl }}/install-gde/install/cli/install-cli-uninstall-langpk.html)
*	<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-uninstall.html#instgde-install-uninstall">卸载Magento</a>
*	<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-uninstall.html#instgde-install-magento-update">更新Magento</a>
*	<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-uninstall.html#instgde-install-magento-reinstall">重装Magento</a>
