---
group: install_cli
subgroup: 05_Command-line installation
title: 建立或更新部署配置
menu_title: 建立或更新部署配置
menu_node:
menu_order: 9
version: 2.0
github_link: install-gde/install/cli/install-cli-subcommands-deployment.md
redirect_from:
  - /guides/v1.0/install-gde/install/install-cli-subcommands-deployment.html
  - /guides/v2.0/install-gde/install/install-cli-subcommands-deployment.html
functional_areas:
  - Install
  - System
  - Setup
  - Deploy
---

<h2 id="instgde-cli-before">第一步</h2>
{% include install/first-steps-cli.html %}
我们不止在这里讨论命令参数，更多请参考<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands.html#instgde-cli-subcommands-common">命令参数</a>.

<h2 id="instgde-cli-subcommands-configphp-prereq">先决条件</h2>
这个命令不需要任何前提条件

<h2 id="instgde-cli-subcommands-configphp">建立或更新Magento的部署配置</h2>
<a href="{{ page.baseurl }}/config-guide/config/config-php.html">Magento的布署配置</a> 提供了Magento必须的初始化和自引导的信息

你可以使用这个命令，如果：

*	你之前已经安装了Magento并且你想要修改部署配置
*	如果你仅想建立一个部署配置并且用一些其它的方法继续安装Magento
*	不想影响现有的东西，更新部署配置

命令参数：

	magento setup:config:set [--<parameter>=<value>, ...]

下面的表格讨论了安装的参数和值的含义

<table>
	<col width="25%">
	<col width="65%">
	<col width="10%">
	<tbody>
		<tr>
			<th>参数</th>
			<th>值</th>
			<th>是否必需?</th>
		</tr>

	<tr>
		<td><p>--backend-frontname</p></td>
		<td><p>统一资源定位(<a href="http://www.w3.org/Protocols/rfc2616/rfc2616-sec3.html#sec3.2" target="_blank">URI</a>) to access the Magento Admin.</p>
			<p>To prevent exploits, we recommend you <em>not</em> use a common word like <code>admin</code>, <code>backend</code>, and so on. The Admin URI can contain alphanumeric values and the underscore character (<code>_</code>) only. </p></td>
		<td><p>否</p></td>
	</tr>
	<tr>
		<td><p>--db-host</p></td>
		<td><p>使用下列值之一:</p>
		<ul><li>数据库服务器的完整的有效的主机名或IP地址.</li>
		<li><code>localhost</code> (默认) or <code>127.0.0.1</code>如果你的数据库服务器和你的web服务器在一台主机上.<br><code>localhost</code>表示Mysql客户端库使用了UNIX套接字来连接数据库。 <code>127.0.0.1</code> 是因为客户端库所用的是TCP协议,关于套接字的更多信息，see the <a href="http://php.net/manual/en/ref.pdo-mysql.php" target="_blank">PHP <code>PDO_MYSQL</code>文档</a>.</li></ul>
		<p><strong>注意</strong>: 你也可以在数据库的主机名后面加一个特定的端口，如<code>www.example.com:9000</code></p>
</td>
		<td><p>否</p></td>
	</tr>
	<tr>
		<td><p>--db-name</p></td>
		<td><p>你想要把Magento数据表放入的数据库的名称</p>
			<p>默认是<code>magento2</code>.</p></td>
		<td><p>否</p></td>
	</tr>
	<tr>
		<td><p>--db-user</p></td>
		<td><p>Magento数据库的所有者的用户名</p>
			<p>默认是<code>root</code>.</p></td>
		<td><p>否</p></td>
	</tr>
	<tr>
		<td><p>--db-password</p></td>
		<td><p>Magento数据库所有者的密码.</p></td>
		<td><p>否</p></td>
	</tr>
	<tr>
		<td><p>--db-prefix</p></td>
		<td><p>仅用于安装数据库表到一个已经有Magento表的数据库时</p>
		<p>在这种情况下，用一个前缀来标识Magento是本次安装的，一些客户有一个或多个Magento实例运行在同一台服务器上，并将所有的数据表放到了同一个数据库中。</p>
		<p>这个前缀最长为5位，必须是以字母开头，只能包含数字、字母和下划线。</p>
		<p>这个选项允许客户为多个Magento安装共享数据库服务器</p></td>
		<td><p>否</p></td>
	</tr>
	<tr>
		<td><p>--session-save</p></td>
		<td><p>使用下列值之一:</p>
		<ul><li><code>db</code>将session数据存储到<a href="{{ page.baseurl }}/config-guide/cache/caching-database.html">数据库</a>. 如果你有一个数据库集群你可以选择数据库存储，否则，并不会比用文件来存储有更多好处</li>

    <li><code>files</code>将session数据存储到文件系统，基于文件的session存储是比较合适的，除非你的文件系统访问非常慢或你有一个数据库集群，或你想用redis来存储session数据</li>

    <li><code>redis</code>将session数据存储到<a href="{{ page.baseurl }}/config-guide/redis/config-redis.html">Redis</a>. 如果你将使用redis做为默认session存储或页面缓存，你必须已经安装好了redis See <a href="{{ page.baseurl }}/config-guide/redis/redis-session.html">使用redis存储session数据</a>来获取更多的关于配置支持redis的更多信息</li>
	</ul></td>
		<td><p>否</p></td>
	</tr>
	<tr>
		<td><p>--key</p></td>
		<td><p>如果你有，指定这个密钥来加密Magento数据库中<a href="#sens-data">敏感数据</a>,如果没有，Magento生成一个密钥来加密。</p></td>
		<td><p>否</p></td>
	</tr>
	<!-- <tr>
		<td>enable_modules=&lt;list></td>
		<td><p>Enable modules that are installed but disabled where <code>&lt;list></code> is a comma-separated list of modules (no spaces allowed). Use <code>php index.php help module-list</code> to list enabled and disabled modules.</p>
		<p>For important information about module dependencies, see <a href="#instgde-cli-subcommands-dep-config-enable-modules">关于启用和禁用模块</a>.</p></td>
		<td>否</td>
	</tr>
	<tr>
		<td>disable_modules=&lt;list></td>
		<td><p>Disable modules that are installed and enabled where <code>&lt;list></code> is a comma-separated list of modules (no spaces allowed). Use <code>php index.php help module-list</code> to list enabled and disabled modules.</p>
		<p>For important information about module dependencies, see <a href="#instgde-cli-subcommands-dep-config-enable-modules">关于启用和禁用模块</a>.</p></td>
		<td>否</td>
	</tr> -->
	<tr>
		<td><p>--db-init-statements</p></td>
		<td><p>Advanced MySQL configuration parameter. Uses database initialization statements to run when connecting to the MySQL database.</p>
			<p>默认是<code>SET NAMES utf8;</code>.</p>
			<p>Consult a reference similar to <a href="http://dev.mysql.com/doc/refman/5.6/en/server-options.html" target="_blank">点击这里</a> 在你设置这个值之前.</p></td>
		<td><p>否</p></td>
	</tr>
	<tr>
		<td><p>--http-cache-hosts</p></td>
		<td><p>Comma-separated list of HTTP cache gateway hosts to which to send purge requests. (例如， Varnish servers.) Use this parameter to specify the host or hosts to purge in the same request. (It doesn't matter if you have only one host or many hosts.)</p>
			<p>Format must be <code>&lt;hostname or ip>:&lt;listen port></code>, where you can omit <code>&lt;listen port></code> if it's port 80. 例如， <code>--http-cache-hosts=192.0.2.100,192.0.2.155:6081</code>. Do not separate hosts with a space character.</p> </td>
		<td><p>否</p></td>
	</tr>
	</tbody>
</table>

{% include install/sens-data.md %}

If applicable, continue your Magento安装:

*	<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-install.html">命令行安装</a>
*	<a href="{{ page.baseurl }}/install-gde/install/web/install-web.html">网页向导安装</a>

<!-- <h2 id="instgde-cli-subcommands-dep-config-enable-modules">关于启用和禁用模块</h2>
{% include install/enable-disable-modules.html %} -->

#### 相关主题

*	<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-install.html">使用命令行安装Magento</a>
*	[移除样本数据模块或更新样本数据]({{ page.baseurl }}/install-gde/install/cli/install-cli-sample-data-other.html)
*	[启用或禁用模块]({{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands-enable.html)
*	[显示或更改管理面板的URI]({{ page.baseurl }}/install-gde/install/cli/install-cli-adminurl.html)
*	[卸载模块]({{ page.baseurl }}/install-gde/install/cli/install-cli-uninstall-mods.html)
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
