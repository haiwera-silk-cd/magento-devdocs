---
group: install_cli
subgroup: 05_Command-line installation
title: Uninstall language packages
menu_title: Uninstall language packages
menu_node:
menu_order: 500
version: 2.0
github_link: install-gde/install/cli/install-cli-uninstall-langpk.md
redirect_from:
  - /guides/v1.0/install-gde/install/install-cli-uninstall-langpk.html
  - /guides/v2.0/install-gde/install/install-cli-uninstall-langpk.html
functional_areas:
  - Install
  - System
  - Setup
---

  
<h2 id="instgde-cli-uninst-lgpk-over">Overview of uninstalling language packages</h2>
This section discusses how to uninstall one or more language packages, optionally including the language packages' code from the file system. You can create backups first so you can restore the data at a later time.

This command uninstalls *only* language packages that are specified in `composer.json`; in other words, language packages that are provided as {% glossarytooltip d85e2d0a-221f-4d03-aa43-0cda9f50809e %}Composer{% endglossarytooltip %} packages. If your {% glossarytooltip 9c4c7b9b-43f0-4454-8e8c-fb62ad40c35f %}language package{% endglossarytooltip %} is not a Composer package, you must uninstall it manually by removing language package code from the file system.

You can restore backups at any time using the <a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-uninstall-mods.html#instgde-cli-uninst-mod-roll">magento setup:rollback</a> command.

<h2 id="instgde-cli-before">第一步</h2>
{% include install/first-steps-cli.html %}
我们不止在这里讨论命令参数，更多请参考<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands.html#instgde-cli-subcommands-common">命令参数</a>.

<h2 id="instgde-cli-uninst-lgpk-uninst">Uninstall language packages</h2>
命令用法：

	magento i18n:uninstall [-b|--backup-code] {language package name} ... {language package name}

The language package uninstall command performs the following tasks:

1.	Checks for dependencies; if so, the command terminates.

	To work around this, you can either uninstall all dependent language packages at the same time or you can uninstall the depending language packages first.
2.	If `--backup code` is specified, backs up the Magento file system (excluding <code>var</code>和<code>pub/static</code> directories) to `var/backups/<timestamp>_filesystem.tgz`
3.	Removes language packages files from the codebase using `composer remove`.
4.	Cleans the {% glossarytooltip 0bc9c8bc-de1a-4a06-9c99-a89a29c30645 %}cache{% endglossarytooltip %}.

For example, if you attempt to uninstall a language package that another language package depends on, the following message displays:

	Cannot uninstall vendorname/language-en_us because the following package(s) depend on it:
        vendorname/language-en_gb

One alternative is to uninstall both language packages after backing up the Magento codebase:

	magento i18n:uninstall vendorname/language-en_us vendorname/language-en_gb --backup-code

命令行将有以下输出信息：

	Code backup is starting...
	Code backup filename: 1435261098_filesystem_code.tgz (The archive can be uncompressed with 7-Zip on Windows systems)
	Code backup path: /var/www/html/magento2/var/backups/1435261098_filesystem_code.tgz
	[SUCCESS]: Code backup completed successfully.
	Loading composer repositories with package information
	Updating dependencies (including require-dev)
	  - Removing vendorname/language-en_us (dev-master)
	Removing Magento/LanguageEn_us
	  - Removing vendorname/language-en_br (dev-master)
		Removing vendorname/language-en_br (dev-master)
	Writing lock file
	Generating autoload files

#### 相关主题

*	<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-install.html">使用命令行安装Magento</a>
*	[移除样本数据模块或更新样本数据]({{ page.baseurl }}/install-gde/install/cli/install-cli-sample-data-other.html)
*	[启用或禁用模块]({{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands-enable.html)
*	[显示或更改管理面板的URI]({{ page.baseurl }}/install-gde/install/cli/install-cli-adminurl.html)
*	[卸载模块]({{ page.baseurl }}/install-gde/install/cli/install-cli-uninstall-mods.html)
*	<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands-deployment.html">建立或更新布署配置</a>
*	<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands-maint.html">开启或关闭维护模式</a>
*	<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands-db.html">创建Magento的数据库表结构</a>
*	[更新数据库表结构和数据]({{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands-db-upgr.html)
*	<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands-store.html">配置网店</a>
*	<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands-admin.html">创建或解锁Magento管理员</a>
*	[备份和还原文件系统，媒体文件和数据库]({{ page.baseurl }}/install-gde/install/cli/install-cli-backup.html)
*	[卸载主题]({{ page.baseurl }}/install-gde/install/cli/install-cli-theme-uninstall.html)
*	<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-uninstall.html#instgde-install-uninstall">卸载Magento</a>
*	<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-uninstall.html#instgde-install-magento-update">更新Magento</a>
*	<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-uninstall.html#instgde-install-magento-reinstall">重装Magento</a>
