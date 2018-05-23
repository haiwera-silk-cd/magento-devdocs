---
group: install_cli
title: 建立或更新部署配置
version: 2.1
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

    <li><code>files</code> to store session data in the file system. File-based session storage is appropriate unless the Magento file system access is slow oe you have a clustered database.</li>
    
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
		<td><p>Comma-separated list of HTTP cache gateway hosts to which to send purge requests. (For example, Varnish servers.) Use this parameter to specify the host or hosts to purge in the same request. (It doesn't matter if you have only one host or many hosts.)</p>
			<p>Format must be <code>&lt;hostname or ip>:&lt;listen port></code>, where you can omit <code>&lt;listen port></code> if it's port 80. For example, <code>--http-cache-hosts=192.0.2.100,192.0.2.155:6081</code>. Do not separate hosts with a space character.</p> </td>
		<td><p>否</p></td>
	</tr>
	</tbody>
</table>

{% include install/sens-data.md %}

If applicable, continue your Magento software installation:

*	<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-install.html">Command line installation</a>
*	<a href="{{ page.baseurl }}/install-gde/install/web/install-web.html">网页向导安装</a>

<!-- <h2 id="instgde-cli-subcommands-dep-config-enable-modules">关于启用和禁用模块</h2>
{% include install/enable-disable-modules.html %} -->