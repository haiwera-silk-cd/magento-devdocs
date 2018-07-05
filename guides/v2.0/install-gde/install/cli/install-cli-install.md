---
group: install_cli
subgroup: 05_Command-line installation
title: 安装Magento
menu_title: 安装Magento
menu_order: 4
version: 2.0
github_link: install-gde/install/cli/install-cli-install.md
redirect_from:
  - /guides/v1.0/install-gde/install/install-cli-install.html
  - /guides/v2.0/install-gde/install/install-cli-install.html
functional_areas:
  - Install
  - System
  - Setup
---

<div class="bs-callout bs-callout-tip">
  <p>总是不行? 需要援助? 尝试看看<a href="{{ page.baseurl }}/install-gde/install-quick-ref.html">快速安装参考(教程)</a>或<a href="{{ page.baseurl }}/install-gde/install-roadmap_part1.html">一步步安装(参考)</a>.</p>
</div>

<h2 id="instgde-install-cli-prereq">在你开始安装之前</h2>

在你开始之前，请确保：

1.	你的系统已经满足我们在<a href="{{ page.baseurl }}/install-gde/system-requirements.html">Magento系统要求</a>中所讨论的要求.
2.	你已经完成了我们在<a href="{{ page.baseurl }}/install-gde/prereq/prereq-overview.html">先决条件</a>讨论的所有必要的任务.
3.	You took your first installation steps as discussed in <a href="{{ page.baseurl }}/install-gde/bk-install-guide.html">你的安装或升级的路径</a>.
4.	在你登录到Magento服务器之后，<a href="{{ page.baseurl }}/install-gde/prereq/file-sys-perms-over.html">切换到Magento文件所有者身份</a>.
5.	Review the information discussed in <a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands.html">命令行安装起步</a>.

<div class="bs-callout bs-callout-info" id="info">
<span class="glyphicon-class">
  <p>You must install Magento from its <code>bin</code> subdirectory.</p></span>
</div>

安装器被设计成可以运行多次的，所以在你须要的时候，你可以:

*	提供不同的值

	例如, 在你配置好你的web服务器的安全套接字层(SSL)之后，你可以运行安装器来设置SSL的选项。
*	修正你之前安装的失误
*	安装Magento到不同的数据库实例中

<div class="bs-callout bs-callout-info" id="info">
<span class="glyphicon-class">
  <ul><li>默认情况下，安装器不会覆盖Magento的数据库，如果你安装Magento到相同的数据库，你可以使用<code>cleanup-database</code>选项来改变这个行为</li>
</div>

See also <a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-uninstall.html">更新, 重装, 卸载</a>.

{% include install/fully-secure.md %}

## 安装器的帮助命令 {#instgde-cli-help-cmds}
你可以使用下面的命令来找到一些必要的参数:

<table>
<tbody>
	<tr>
		<th>安装器参数</th>
		<th>命令</th>
	</tr>
<tr>
	<td>语言</td>
	<td><code>magento info:language:list</code></td>
</tr>
<tr>
	<td>货币</td>
	<td><code>magento info:currency:list</code></td>
</tr>
<tr>
	<td>时区</td>
	<td><code>php  magento info:timezone:list</code></td>
</tr>
</tbody>
</table>

<div class="bs-callout bs-callout-info" id="info">
<span class="glyphicon-class">
  <p>If an error displays when you run these commands, make sure you updated installation dependencies as discussed in <a href="{{ page.baseurl }}/install-gde/install/prepare-install.html">更新安装依赖</a>.</p></span>
</div>


<h2 id="instgde-install-cli-magento">从命令行安装Magento</h2>
安装命令的格式如下:

	magento setup:install --<option>=<value> ... --<option>=<value>

下面的表格讨论安装选项的各选项及其对应值的含义，我们在 <a href="#install-cli-example">简单本地安装</a>提供了示例.

<div class="bs-callout bs-callout-info" id="info">
<span class="glyphicon-class">
  <p>任何包含空格或特殊字符的选项必须用单引号或双引号引住.</p></span>
</div>
<table>
	<col width="35%">
	<col width="55%">
	<col width="10%">
	<tbody>
		<tr>
			<th>名称</th>
			<th>值</th>
			<th>是否必需?</th>
		</tr>
		<tr>
		<td><p>--admin-firstname</p></td>
		<td><p>Magento管理员的姓.</p></td>
		<td><p>是</p></td>
	</tr>
	<tr>
		<td><p>--admin-lastname</p></td>
		<td><p>Magento管理员的名.</p></td>
		<td><p>是</p></td>
	</tr>
	<tr>
		<td><p>--admin-email</p></td>
		<td><p>Magento管理员的电子邮箱</p></td>
		<td><p>是</p></td>
	</tr>
	<tr>
		<td><p>--admin-user</p></td>
		<td><p>Magento管理员的用户名</p></td>
		<td><p>是</p></td>
	</tr>
	<tr>
		<td><p>--admin-password</p></td>
		<td><p>Magento管理员的密码.</p>
			<p>密码至少7位，必须包含至少一个字母和数字.</p>
			<p我们推荐使用一个长的，更复杂的密码，用引号引住，例如, <code>--admin-password='A0b9%t_3`g'</code></p></td>
		<td><p>是</p></td>
	</tr>
		<tr>
		<td><p>--base-url</p></td>
		<td><p>Base URL用于访问你的网店的前台和后台，可以是以下格式:</p>
		<ul><li><code>http[s]://&lt;host or ip>/&lt;你的Magento的安装目录>/</code>.</p>
		<p><strong>注意</strong>: The scheme (<code>http://</code>或<code>https://</code>) and a trailing slash are <em>both</em> required.</p>
		<p><code>&lt;你的Magento的安装目录></code> 是一个你把Magento安装到的相对docroot的路径，这个值依赖于你的web服务器和虚拟主机是如何配置的，这个路径可能是<code>magento2</code>或也有可能是空的.</p>
		<p>To access Magento on localhost, you can use either <code>http://127.0.0.1/&lt;你的Magento的安装目录>/</code>或<code>http://127.0.0.1/&lt;你的Magento的安装目录>/</code>.</p></li>
		<li><code>&#123;&#123;base_url&#125;&#125;</code>是一个被虚拟主机设置的或一个像Docker虚拟环境所定义的基本URL.例如, 如果你用一个主机名<code>magento.example.com</code>为Magento设置了一个虚拟主机, 这样你就可以使用<code>--base-url=&#123;&#123;base_url&#125;&#125;</code>来安装你的Magento和访问你的Magento的管理面板，使用URL:<code>http://magento.example.com/admin</code>.</li></ul>

		</td>
		<td><p>否</p></td>
	</tr>
	<tr>
		<td><p>--backend-frontname</p></td>
		<td><p>统一资源定位(<a href="http://www.w3.org/Protocols/rfc2616/rfc2616-sec3.html#sec3.2" target="_blank">URI</a>)，用以访问Magento管理面板，你可以省略它来让Magento生成一个随机的URI.</p>
			<p>基于安全的考虑，我们强烈推荐使用一个随机的地址.黑客或恶意软件是很难破解一个随机的地址的</p>
			<p>这个URI会在安装结束时显示. 你可以在之后的任何时候使用<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-adminurl.html">magento info:adminuri</a>命令来查看这个URI </p>
			<p>如果你选择手动设置这个值, 我们推荐你不要使用一个像<code>admin</code>, <code>backend</code>等的常用词. 管理面板的URI仅可以包含数字、字母和(<code>_</code>). </p></td>
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
		<td><p>--language</p></td>
		<td><p>语言用于管理员面板和网店前台. (如果你不清楚有哪些，你可以在<code>bin</code>目录执行<code>./magento info:language:list</code>命令来列出所有可选的语言.)</p></td>
		<td><p>否</p></td>
	</tr>
	<tr>
		<td><p>--currency</p></td>
		<td><p>默认货币用于网店前台。(如果你还不清楚有哪些,你可以在 <code>bin</code>目录执行<code>./magento info:currency:list</code>来列出所有的可选货币.)</p></td>
		<td><p>否</p></td>
	</tr>
	<tr>
		<td><p>--timezone</p></td>
		<td><p>默认时区用于管理面板和网店前台。(如果你还不清楚有哪些,你可以在 <code>bin</code>目录执行<code>./magento info:timezone:list</code>来列出所有的可选时区.)</p></td>
		<td><p>否</p></td>
	</tr>
	<tr>
		<td><p>--use-rewrites</p></td>
		<td><p><code>1</code>表示对所有网店前台和管理面板生成的链接使用服务器重写</p>
		<p><code>0</code>表示不允许服务器重写，默认是这个值。</p></td>
		<td><p>否</p></td>
	</tr>
	<tr>
		<td><p>--use-secure</p></td>
		<td><p><code>1</code> 表示在网让的URL中启用安全套接字层(SSL)，在选择这个选择之前，请确保您的服务器支持SSL</p>
		<p><code>0</code>表示不使用SSL,这种情况下，所有其它的关于安全url相关的选项都被假定为<code>0</code>. 默认是这个值。</p>
		</td>
		<td><p>否</p></td>
	</tr>
	<tr>
		<td><p>--base-url-secure</p></td>
		<td>指定访问你的Magento管理面板和网店前台的安全的基础URL，格式如下：
		<code>http[s]://&lt;host or ip>/&lt;你的Magento的安装目录>/</code>
		</td>
		<td><p>否</p></td>
	</tr>

	<tr>
		<td><p>--use-secure-admin</p></td>
		<td><p><code>1</code>表示在你的Magento管理面板的URL中使用SSL，在选择这个值之前，请确保您的服务器支持SSL</p>
		<p><code>0</code> 表示在管理面板的URL中不使用SSL，默认是这个值</p></td>
		<td><p>否</p></td>
	</tr>
	<tr>
		<td><p>--admin-use-security-key</p></td>
		<td><p><code>1</code>使Magento在管理面板和在表单中使用一个随机生成的键值，这个键值能帮助防止<a href="https://www.owasp.org/index.php/Cross-Site_Request_Forgery_%28CSRF%29" target="_blank">跨站脚本攻击</a>. 默认是这个值.</p>
		<p><code>0</code> 不值用这个键值.</p></td>
		<td><p>否</p></td>
	</tr>
	<!-- <tr>
		<td>enable_modules=&lt;list>}</td>
		<td><p>Enable modules that are installed but disabled where <code>&lt;list></code> is a comma-separated list of modules (no spaces allowed). Use <code>php index.php help module-list</code> to list enabled and disabled modules.</p>
		<p>To enable and disable modules after installing Magento, see <a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands-enable.html">启用和禁用模块</a>.</p>
		<p>For important information about module dependencies, see <a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands-enable.html#instgde-cli-subcommands-enable-modules">关于启用和禁用模块</a>.</p></td>
		<td>否</td>
	</tr>
	<tr>
		<td>disable_modules=&lt;list>}</td>
		<td><p>Disable modules that are installed and enabled where <code>&lt;list></code> is a comma-separated list of modules (no spaces allowed). Use <code>php index.php help module-list</code> to list enabled and disabled modules.</p>
		<p>To enable and disable modules after installing Magento, see <a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands-enable.html">启用和禁用模块</a>.</p>
		<p>For important information about module dependencies, see <a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands-enable.html#instgde-cli-subcommands-enable-modules">关于启用和禁用模块</a>.</p></td>
		<td>否</td>
	</tr> -->
	<tr>
		<td><p>--session-save</p></td>
		<td><p>使用下列值之一:</p>
		<ul><li><code>db</code>将session数据存储到<a href="{{ page.baseurl }}/config-guide/cache/caching-database.html">数据库</a>. 如果你有一个数据库集群你可以选择数据库存储，否则，并不会比用文件来存储有更多好处</li>

			<li><code>files</code> to store session data in the file system. File-based session storage is appropriate unless the Magento file system access is slow or you have a clustered database.</li>
	</ul></td>
		<td><p>否</p></td>
	</tr>
	<tr>
		<td><p>--key</p></td>
		<td><p>如果你有，指定这个密钥来加密Magento数据库中<a href="#sens-data">敏感数据</a>,如果没有，Magento生成一个密钥来加密。</p></td>
		<td><p>否</p></td>
	</tr>
	<tr>
		<td><p>--cleanup-database</p></td>
		<td><p>在安装之前删除所有的数据库表，指定这个选项不须要参数.否则Magento数据库中的表将被完整保留。</p></td>
		<td><p>否</p></td>
	</tr>
	<tr>
		<td><p>--db-init-statements</p></td>
		<td><p>高级Mysql配置参数，当连接到Mysql数据库时执行数据库初始化语句。查阅类似的参考 <a href="http://dev.mysql.com/doc/refman/5.6/en/server-options.html" target="_blank">点击这里</a> 在你设置这个值之前.</p>
			<p>默认是<code>SET NAMES utf8;</code>.</p></td>
		<td><p>否</p></td>
	</tr>
	<tr>
		<td><p>--sales-order-increment-prefix</p></td>
		<td><p>为销售订单号指定一个前缀，通常，用于在支付处理中生成唯一的订单号。</p></td>
		<td><p>否</p></td>
	</tr>
<tr>
<td><p>--amqp-host</p></td>
<td><p>仅适用{{site.data.var.ee}}. Do not use the `--amqp` options unless you have already set up an installation of RabbitMQ. See <a href="{{ page.baseurl }}/install-gde/prereq/install-rabbitmq.html">RabbitMQ安装</a> for more information about installing and configuring RabbitMQ.</p>
<p>RabbitMQ安装到的主机名</p></td>
<td><p>否</p></td>
</tr>
<tr>
<td><p>--amqp-port</p></td>
<td><p>仅适用{{site.data.var.ee}}. 连接到RabbitMQ的端口，默认值是 <code>5672</code>.</p></td>
<td><p>否</p></td>
</tr>
<tr>
<td><p>--amqp-user</p></td>
<td><p>仅适用{{site.data.var.ee}}. 连接到RabbitMQ的用户名，不要使用默认用户 <code>guest</code>.</p></td>
<td><p>否</p></td>
</tr>
<tr>
<td><p>--amqp-password</p></td>
<td><p>仅适用{{site.data.var.ee}}. 连接到RabbitMQ的密码，不要使用默认密码<code>guest</code>.</p></td>
<td><p>否</p></td>
</tr>
	</tbody>
</table>

<div class="bs-callout bs-callout-info" id="info">
<span class="glyphicon-class">
  <p>要在安装完之后启用或禁用模块，请参考<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands-enable.html">启用和禁用模块</a>.</p>
  	</span>
</div>

{% include install/sens-data.md %}

<h4 id="install-cli-example">简单的本地安装</h4>

**示例1**

下面的例子展示了用以下的选项安装Magento:

*	Magento安装在关联到web服务器的localhost的`magento2`目录，并且管理面板的路径是`admin`; 因此：

	你的网店的地址是`http://127.0.0.1`

*	数据库服务器和web服务器在同一台主机.

	数据库名叫`magento`,数据库用户名和密码都是`magento`

*	使用服务器重写

*	Magento管理员有以下属性：

	*	First and last name are `Magento User`
	*	用户名是`admin` ，密码是`admin123`
	*	邮箱地址是`user@example.com`

*	默认语言是`en_US` (U.S. English)
*	默认货币是U.S. dollars
*	默认时区是U.S. Central (America/Chicago)

		magento setup:install --base-url=http://127.0.0.1/magento2/ \
		--db-host=localhost --db-name=magento --db-user=magento --db-password=magento \
		--admin-firstname=Magento --admin-lastname=User --admin-email=user@example.com \
		--admin-user=admin --admin-password=admin123 --language=en_US \
		--currency=USD --timezone=America/Chicago --use-rewrites=1

如果成功你的控制台输出信息将和下面的类似

	Post installation file permissions check...
	For security, remove write permissions from these directories: '/var/www/html/magento2/app/etc'
	[Progress: 274 / 274]
	[SUCCESS]: Magento installation complete.
	[SUCCESS]: Admin Panel URI: /admin_puu71q


**Example 2** (with additional options)

下面的例子展示了用以下的选项安装Magento:

*	Magento安装在关联到web服务器的localhost的`magento2`目录，并且管理面板的路径是`admin`; 因此：

	你的网店的地址是`http://127.0.0.1`

*	数据库服务器和web服务器在同一台主机.

	数据库名叫`magento`,数据库用户名和密码都是`magento`

*	Magento管理员有以下属性：

	*	姓名是`Magento User`
	*	用户名是`admin` ，密码是`admin123`
	*	邮箱地址是`user@example.com`

*	默认语言是`en_US` (U.S. English)
*	默认货币是U.S. dollars
*	默认时区是U.S. Central (America/Chicago)
*	安装器在安装之前首先清除数据库中的表
*	你使用一个自增的前缀`ORD$`并且因为它包含一个特殊字符(`$`),所以必须使用引号引住
*	Session数据保存在数据库中
*	使用服务器重写

		magento setup:install --base-url=http://127.0.0.1/magento2/ \
		--db-host=localhost --db-name=magento \
		--db-user=magento --db-password=magento \
		--admin-firstname=Magento --admin-lastname=User --admin-email=user@example.com \
		--admin-user=admin --admin-password=admin123 --language=en_US \
		--currency=USD --timezone=America/Chicago --cleanup-database \
		--sales-order-increment-prefix="ORD$" --session-save=db --use-rewrites=1

如果成功你的控制台输出信息将和下面的类似

	Post installation file permissions check...
	For security, remove write permissions from these directories: '/var/www/html/magento2/app/etc'
	[Progress: 274 / 274]
	[SUCCESS]: Magento installation complete.
	[SUCCESS]: Admin Panel URI: /admin_puu71q


<div class="bs-callout bs-callout-info" id="info">
<span class="glyphicon-class">
  <p>命令必须在一行写完，或者像先前的例子一样，分行并在每行的末尾加上 <code>\</code></p></span>
</div>

#### 下一步
*	如果你有一个访问Magento服务器的账户, 请参考[可选地设置UMASK]({{ page.baseurl }}/install-gde/install/post-install-umask.html).

	这是一种在共享主机上安装的典型的类型
*	[验证安装]({{ page.baseurl }}/install-gde/install/verify.html).

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
