---
group: install_cli
subgroup: 05_Command-line installation
title: 配置网店
menu_title: 配置网店
menu_node:
menu_order: 20
version: 2.0
github_link: install-gde/install/cli/install-cli-subcommands-store.md
redirect_from:
  - /guides/v1.0/install-gde/install/install-cli-subcommands-store.html
  - /guides/v2.0/install-gde/install/install-cli-subcommands-store.html
functional_areas:
  - Install
  - System
  - Setup
---


<h2 id="instgde-cli-before">第一步</h2>
{% include install/first-steps-cli.html %}
我们不止在这里讨论命令参数，更多请参考<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands.html#instgde-cli-subcommands-common">命令参数</a>.

## 先决条件 {#instgde-cli-subcommands-store-prereq}
在你执行这个命今之前，你必须完成以下步骤*或* 你必须<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-install.html">安装Magento</a>:

*	<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands-deployment.html">建立或更新布署配置</a>
*	<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands-db.html">创建Magento的数据库表结构</a>

{% include install/fully-secure.md %}

<h2 id="instgde-cli-storeconfig">配置网店</h2>
命令用法：

	magento setup:store-config:set [--<parameter_name>=<value>, ...]

下面的表格定义了一些可用的参数据和值。

<table>
	<col width="30%">
	<col width="50%">
	<col width="20%">
	<tbody>
		<tr>
			<th>名称</th>
			<th>值</th>
			<th>是否必需?</th>
		</tr>
		<tr>
		<td>--base-url</td>
		<td>Base URL to use to access your Magento Admin and storefront in any of the following formats:
		<ul><li><code>http[s]://&lt;host or ip>/&lt;你的Magento的安装目录>/</code>.
		<strong>注意</strong>: The scheme (<code>http://</code>或<code>https://</code>) and a trailing slash are <em>both</em> required.
		<code>&lt;你的Magento的安装目录></code> 是一个你把Magento安装到的相对docroot的路径，这个值依赖于你的web服务器和虚拟主机是如何配置的，这个路径可能是<code>magento2</code>或也有可能是空的.
		To access Magento on localhost, you can use <code>http://127.0.0.1/&lt;你的Magento的安装目录>/</code>.</li>
		<li><code>&#123;&#123;base_url&#125;&#125;</code>是一个被虚拟主机设置的或一个像Docker虚拟环境所定义的基本URL.例如, 如果你用一个主机名<code>magento.example.com</code>为Magento设置了一个虚拟主机, 这样你就可以使用<code>--base-url=&#123;&#123;base_url&#125;&#125;</code>来安装你的Magento和访问你的Magento的管理面板，使用URL:<code>http://magento.example.com/admin</code>.</li></ul>		</td>
		<td>否</td>
	</tr>
	<tr>
		<td>--language</td>
		<td><p>指定管理面板和网店使用的语言.</p>
			<p>(如果你不清楚有哪些，你可以通过在<code>bin</code>目录下执行<code>./magento info:language:list</code>来列出所有可用的语言)</p></td>
		<td>否</td>
	</tr>
	<tr>
		<td>--currency</td>
		<td><p>指定网店用于的默认货币</p> 
			<p>(如果你不清楚有哪些，可以在<code>bin</code>目录下执行<code>magento info:currency:list</code>来列出所有的可用货币)</p></td>
		<td>否</td>
	</tr>
	<tr>
		<td>--timezone</td>
		<td>默认时区用于管理面板和网店前台。(如果你还不清楚有哪些,你可以在 <code>bin</code>目录执行<code>./magento info:timezone:list</code>来列出所有的可选时区.)</td>
		<td>否</td>
	</tr>
	<tr>
		<td>--use-rewrites</td>
		<td><p><code>1</code>表示对所有网店前台和管理面板生成的链接使用服务器重写</p>
		<p><code>0</code>表示不允许服务器重写，默认是这个值。</p></td>
		<td>否</td>
	</tr>
	<tr>
		<td>--use-secure</td>
		<td><p><code>1</code> 表示在网让的URL中启用安全套接字层(SSL)，在选择这个选择之前，请确保您的服务器支持SSL</p>
		<p><code>0</code>表示不使用SSL,这种情况下，所有其它的关于安全url相关的选项都被假定为<code>0</code>. 默认是这个值。</p></td>
		<td>否</td>
	</tr>
	<tr>
		<td>--base-url-secure</td>
		<td>指定访问你的Magento管理面板和网店前台的安全的基础URL，格式如下：
		<code>http[s]://&lt;host or ip>/&lt;你的Magento的安装目录>/</code></td>
		<td>否</td>
	</tr>

	<tr>
		<td>--use-secure-admin</td>
		<td><p><code>1</code>表示在你的Magento管理面板的URL中使用SSL，在选择这个值之前，请确保您的服务器支持SSL</p>
		<p><code>0</code> 表示在管理面板的URL中不使用SSL，默认是这个值</p></td>
		<td>否</td>
	</tr>
	</tbody>
</table>

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
*	<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands-admin.html">创建或解锁Magento管理员</a>
*	[备份和还原文件系统，媒体文件和数据库]({{ page.baseurl }}/install-gde/install/cli/install-cli-backup.html)
*	[卸载主题]({{ page.baseurl }}/install-gde/install/cli/install-cli-theme-uninstall.html)
*	[卸载语言包]({{ page.baseurl }}/install-gde/install/cli/install-cli-uninstall-langpk.html)
*	<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-uninstall.html#instgde-install-uninstall">卸载Magento</a>
*	<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-uninstall.html#instgde-install-magento-update">更新Magento</a>
*	<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-uninstall.html#instgde-install-magento-reinstall">重装Magento</a>
