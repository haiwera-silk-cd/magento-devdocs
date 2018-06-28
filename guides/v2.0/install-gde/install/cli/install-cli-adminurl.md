---
group: install_cli
subgroup: 05_Command-line installation
title: 显示和修改管理面板URI
menu_title: 显示和修改管理面板URI
menu_node:
menu_order: 6
version: 2.0
github_link: install-gde/install/cli/install-cli-adminurl.md
redirect_from:
  - /guides/v1.0/install-gde/install/install-cli-adminurl.html
  - /guides/v2.0/install-gde/install/install-cli-adminurl.html
functional_areas:
  - Install
  - System
  - Setup
---

<h2 id="instgde-cli-before">第一步</h2>
{% include install/first-steps-cli.html %}
我们不止在这里讨论命令参数，更多请参考<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands.html#instgde-cli-subcommands-common">命令参数</a>.

<h2 id="instgde-cli-subcommands-db-prereq">先决条件</h2>
在你运行这个命令之前，你必须a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands-deployment.html">建立或更新布署配置</a>.

<h2 id="instgde-cli-displayurl">Display the Admin URI</h2>
This section discusses how to use the command line to display the {% glossarytooltip 29ddb393-ca22-4df9-a8d4-0024d75739b1 %}Admin{% endglossarytooltip %} Uniform Resource Identifier (<a href="http://www.w3.org/Protocols/rfc2616/rfc2616-sec3.html#sec3.2" target="_blank">URI</a>).

命令参数：

	magento info:adminuri

A sample result follows:

	Admin Panel URI: /admin_1wgrah

You can also view the Admin URI in `<your Magento install dir>/app/etc/env.php`. A snippet follows:

{% highlight php startinline=true %}
  'backend' =>
  array (
    'frontName' => 'admin_1wgrah',
  ),
{% endhighlight %}

<h2 id="instgde-cli-changeurl">修改管理员面板URI</h2>
To change the Admin URI, use the <a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands-deployment.html">magento setup:config:set</a> command.

#### 相关主题

*	<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-install.html">使用命令行安装Magento</a>
*	[移除样本数据模块或更新样本数据]({{ page.baseurl }}/install-gde/install/cli/install-cli-sample-data-other.html)
*	[显示或更改管理面板的URI]({{ page.baseurl }}/install-gde/install/cli/install-cli-adminurl.html)
*	<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands-enable.html">启用或禁用模块</a>
*	[卸载模块]({{ page.baseurl }}/install-gde/install/cli/install-cli-uninstall-mods.html)
*	<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands-deployment.html">建立或更新布署配置</a>
*	<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands-maint.html">开启或关闭维护模式</a>
*	<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands-db.html">创建Magento的数据库表结构</a>
*	[更新数据库表结构和数据]({{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands-db-upgr.html)
*	<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands-store.html">配置网店</a>
*	<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands-admin.html">创建一个Magento的管理员</a>
*	[备份和还原文件系统，媒体文件和数据库]({{ page.baseurl }}/install-gde/install/cli/install-cli-backup.html)
*	[卸载主题]({{ page.baseurl }}/install-gde/install/cli/install-cli-theme-uninstall.html)
*	[卸载语言包]({{ page.baseurl }}/install-gde/install/cli/install-cli-uninstall-langpk.html)
*	<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-uninstall.html#instgde-install-uninstall">卸载Magento</a>
*	<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-uninstall.html#instgde-install-magento-update">更新Magento</a>
*	<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-uninstall.html#instgde-install-magento-reinstall">重装Magento</a>
