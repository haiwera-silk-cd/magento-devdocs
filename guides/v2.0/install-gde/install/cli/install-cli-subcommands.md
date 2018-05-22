---
group: install_cli
subgroup: 05_Command-line installation
title: 命令行安装起步
menu_title: 命令行安装起步
menu_node:
menu_order: 2
version: 2.0
github_link: install-gde/install/cli/install-cli-subcommands.md
redirect_from:
  - /guides/v1.0/install-gde/install/install-cli-subcommands.html
  - /guides/v2.0/install-gde/install/install-cli-subcommands.html
functional_areas:
  - Install
  - System
  - Setup
---

<h2 id="instgde-install-cli-prereq">在你开始安装之前</h2>
{% include install/before-you-begin-cli.html %}

安装器被设计成可以运行多次的，所以在你须要的时候，你可以:

*	提供不同的值 

	例如, 在你配置好你的web服务器的安全套接字层(SSL)之后，你可以运行安装器来设置SSL的选项。

*	修正你之前安装的失误
*	安装Magento到不同的数据库实例中

<h2 id="instgde-cli-before">第一步</h2>
{% include install/first-steps-cli.html %}
我们不止在这里讨论命令参数，更多请参考<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands.html#instgde-cli-subcommands-common">命令参数</a>.

<h2 id="instgde-cli-summary">命令总结</h2>
下面的表格总结了可用的命令，每个命令只引用了简要信息，关于命令的更多信息请点击对应列的链接。

<table>
	<col width="40%">
  	<col width="30%">
  	<col width="30%">
	<tbody>
		<tr>
			<th>命令</th>
			<th>描述</th>
			<th>先决条件</th>
		</tr>
		
	<tr>
		<td><a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-install.html">magento setup:install</a></td>
		<td><p>安装Magento</p></td>
		<td><p>无</p></td>
	</tr>
	<tr>
		<td><a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-uninstall.html#instgde-install-uninstall">magento setup:uninstall</a></td>
		<td><p>移除Magento</p></td>
		<td><p>Magento已经安装</p></td>
	</tr>
	<tr>
		<td><a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-uninstall.html#instgde-install-magento-update">magento setup:upgrade</a></td>
		<td><p>更新Magento</p></td>
		<td><p>部署配置</p></td>
	</tr>
	<tr>
		<td><a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands-maint.html">magento maintenance:{enable|disable}</a></td>
		<td><p>启用或禁用维护模式(在维护模式中，只有在对应白名单中的ip可以访问Magento管理面板和网店前台).</p></td>
		<td><p>Magento已经安装</p></td>
	</tr>
	<tr>
		<td><a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands-deployment.html">magento setup:config:set</a></td>
		<td><p>建立或更新部署配置</p></td>
		<td><p>无</p></td>
	</tr>
	<tr>
		<td><a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands-enable.html">magento module:{enable|disable}</a></td>
		<td><p>启用或禁用模块.</p></td>
		<td><p>无</p></td>
	</tr>
	<tr>
		<td><a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands-store.html">magento setup:store-config:set</a></td>
		<td><p>设置网店相关的一些选项，比如基础URL,语言，时区等等。</p></td>
		<td><ul><li>部署配置</li>
			<li>数据库(最简单的方法是使用<code>magento setup:upgrade</code>)</li>
				</ul></td>
	</tr>
	<tr>
		<td><a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands-db.html">magento setup:db-schema:upgrade</a></td>
		<td><p>更新Magento数据库表结构。</p></td>
		<td><p>部署配置</p></td>
	</tr>
	<tr>
		<td><a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands-db.html">magento setup:db-data:upgrade</a></td>
		<td><p>更新Magento数据库数据。</p></td>
		<td><p>部署配置</p></td>
	</tr>
	<tr>
		<td><a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands-db.html#instgde-cli-dbconfig">magento setup:db:status</a></td>
		<td><p>检查数据库数据是否是对应当前代码的最新的版本。</p></td>
		<td><p>部署配置</p></td>
	</tr>
	<tr>
		<td><a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands-admin.html">magento admin:user:create</a></td>
		<td><p>创建Magento管理员。</p></td>
		<td><p>如下所示:</p>
			<ul><li>部署配置</li>
				<li>最小化启用<code>Magento_User</code>和<code>Magento_Authorization</code>模块</li>
				<li>数据库(最简单的方法是使用<code>magento setup:upgrade</code>)</li>
				</ul></td>
	</tr>
	<tr>
		<td><a href="#instgde-cli-help">magento list</a></td>
		<td><p>列出所有可用命令.</p></td>
		<td><p>无</p></td>
	</tr>
	<tr>
		<td><a href="#instgde-cli-help">magento help</a></td>
		<td><p>提供指定命令的帮助</p></td>
		<td><p>无</p></td>
	</tr>
	
	
	</tbody>
</table>

<h2 id="instgde-cli-help">命令帮助</h2>
{% include install/cli_help-commands.html %}


<h2 id="instgde-cli-subcommands-common">命令参数</h2>
{% include install/cli_common-commands.html %}


<h2 id="instgde-cli-subcommands">命令</h2>
下面的章节讨论了一些可用的命令。

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
*	[卸载语言包]({{ page.baseurl }}/install-gde/install/cli/install-cli-uninstall-langpk.html)
*	<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-uninstall.html#instgde-install-uninstall">卸载Magento</a>
*	<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-uninstall.html#instgde-install-magento-update">更新Magento</a>
*	<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-uninstall.html#instgde-install-magento-reinstall">重装Magento</a>
