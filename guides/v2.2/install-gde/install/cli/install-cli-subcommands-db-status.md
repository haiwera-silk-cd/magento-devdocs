---
group: install_cli
subgroup: 05_Command-line installation
title: 检查Magento数据库状态
menu_title: 检查Magento数据库状态
menu_node:
menu_order: 16
version: 2.2
github_link: install-gde/install/cli/install-cli-subcommands-db-status.md
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

## 命令用法
要检查Magento的数据库状态，执行

	magento setup:db:status

这个命令不需要参数。

示例结果如下：

	All modules are up to date.

命令将返回如下之一的退出码：

退出码  | 描述 | 建议动作
|--------------|--------------|--------------|
 0 | 正常 | 无 |
 1 | 有模块使用了比数据库更新或更老的版本 | 执行[`magento setup:upgrade`]({{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands-db-upgr.html)来更新数据库表结构，在Magent根目录运行`composer update`来更新组件依赖 |
 2 | setup:upgrade is required | 使用[`magento setup:upgrade`]({{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands-db-upgr.html)来更新{% glossarytooltip 66b924b4-8097-4aea-93d9-05a81e6cc00c %}数据库表结构{% endglossarytooltip %} |

#### 相关主题

*	<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-install.html">使用命令行安装Magento</a>
*	[移除样本数据模块或更新样本数据]({{ page.baseurl }}/install-gde/install/cli/install-cli-sample-data-other.html)
*	[启用或禁用模块]({{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands-enable.html)
*	[显示或更改管理面板的URI]({{ page.baseurl }}/install-gde/install/cli/install-cli-adminurl.html)
*	[卸载模块]({{ page.baseurl }}/install-gde/install/cli/install-cli-uninstall-mods.html)
*	<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands-deployment.html">建立或更新布署配置</a>
*	<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands-maint.html">开启或关闭维护模式</a>
*	[更新数据库表结构和数据]({{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands-db-upgr.html)
*	<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands-store.html">配置网店</a>
*	<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands-admin.html">创建或解锁Magento管理员</a>
*	[备份和还原文件系统，媒体文件和数据库]({{ page.baseurl }}/install-gde/install/cli/install-cli-backup.html)
*	[卸载主题]({{ page.baseurl }}/install-gde/install/cli/install-cli-theme-uninstall.html)
*	[卸载语言包]({{ page.baseurl }}/install-gde/install/cli/install-cli-uninstall-langpk.html)
*	<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-uninstall.html#instgde-install-uninstall">卸载Magento</a>
*	<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-uninstall.html#instgde-install-magento-update">更新Magento</a>
*	<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-uninstall.html#instgde-install-magento-reinstall">重装Magento</a>
