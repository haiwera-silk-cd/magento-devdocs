---
group: install_cli
subgroup: 05_Command-line installation
title: 更新Magento表结构及数据
menu_title: 更新Magento表结构及数据
menu_node:
menu_order: 16
version: 2.0
github_link: install-gde/install/cli/install-cli-subcommands-db-upgr.md
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

## 更新Magento数据表结构和数据 {#instgde-cli-db-upgr}
只要你执行的动作导致了Magento的{% glossarytooltip 66b924b4-8097-4aea-93d9-05a81e6cc00c %}数据库表结构{% endglossarytooltip %}或数据发生改变，你必须执行我们这节讨论的命令来更新它们，基于下面的原因：

*	你使用命令行升级了Magento
*	你使用命令行安装或更新了组件
*	你使用命令行启用或禁用了组件

注意：

*	如果你使用了之前所讲到的网页向导安装，你没有必要使用这里讨论的命令。
*	Magento的*组件*可以是一个模块、主题或语言包，无论是否来自Magento Marketplace都没有关系

命令用法：

	magento setup:upgrade [--keep-generated]

`--keep-generated`是一个可选的参数，指定不更新 [静态的视图文件]({{ page.baseurl }}/config-guide/cli/config-cli-subcommands-static-view.html).这个可选的参数被有经验的系统集成人员用于有限的情况，并且只能用在[生产模式]({{ page.baseurl }}/config-guide/bootstrap/magento-modes.html#production-mode). 不能用在[开发者模式]({{ page.baseurl }}/config-guide/bootstrap/magento-modes.html#developer-mode).

#### 相关主题

*	<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-install.html">使用命令行安装Magento</a>
*	[移除样本数据模块或更新样本数据]({{ page.baseurl }}/install-gde/install/cli/install-cli-sample-data-other.html)
*	[启用或禁用模块]({{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands-enable.html)
*	[显示或更改管理面板的URI]({{ page.baseurl }}/install-gde/install/cli/install-cli-adminurl.html)
*	[卸载模块]({{ page.baseurl }}/install-gde/install/cli/install-cli-uninstall-mods.html)
*	<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands-deployment.html">建立或更新布署配置</a>
*	<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands-maint.html">开启或关闭维护模式</a>
*	<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands-db.html">创建Magento的数据库表结构</a>
*	<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands-store.html">配置网店</a>
*	<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands-admin.html">创建或解锁Magento管理员</a>
*	[备份和还原文件系统，媒体文件和数据库]({{ page.baseurl }}/install-gde/install/cli/install-cli-backup.html)
*	[卸载主题]({{ page.baseurl }}/install-gde/install/cli/install-cli-theme-uninstall.html)
*	[卸载语言包]({{ page.baseurl }}/install-gde/install/cli/install-cli-uninstall-langpk.html)
*	<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-uninstall.html#instgde-install-uninstall">卸载Magento</a>
*	<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-uninstall.html#instgde-install-magento-update">更新Magento</a>
*	<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-uninstall.html#instgde-install-magento-reinstall">重装Magento</a>
