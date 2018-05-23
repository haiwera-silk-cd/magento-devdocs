---
group: install_pre
subgroup: 起步
title: Magento 2.2.x 技术栈要求
menu_title: Magento 2.2.x 技术栈要求
menu_node:
menu_order: 2
version: 2.2
github_link: install-gde/system-requirements-tech.md
functional_areas:
  - Install
  - System
  - Setup
---

### 操作系统(Linux x86-64)
Linux 分时系统，如 RedHat Enterprise Linux (RHEL), CentOS, Ubuntu, Debian等等.

### 内存要求
升级Magento和你从Magento Marketplaces和其他源上获取的扩展可能要求你的系统至少2G的内存，如果你使用的系统内存少于2G，我们建议您创建一个[交换文件]({{ page.baseurl }}/comp-mgr/trouble/cman/out-of-memory.html); 否则, 你的升级可能会失败.

### Composer (最新的稳定版)
{% glossarytooltip d85e2d0a-221f-4d03-aa43-0cda9f50809e %}Composer{% endglossarytooltip %}贡献Magento2基础代码和扩展的开发者将会用到

### Web服务器
*	<a href="http://httpd.apache.org/download.cgi" target="&#95;blank">Apache 2.2 or 2.4</a>

	In addition, 你必须启用Apache的`mod_rewrite`和`mod_version`模块. [`mod_rewrite`](https://httpd.apache.org/docs/2.4/mod/mod_rewrite.html)模块允许服务器进行路由重写。 [`mod_version`](https://httpd.apache.org/docs/2.4/mod/mod_version.html)模块为不同的httpd`版本`提供了一个灵活的版本检查.更多信息请参考<a href="{{ page.baseurl }}/install-gde/prereq/apache.html">我们的Apache文档</a>.

*	<a href="https://nginx.org/en/download.html" target="&#95;blank">nginx 1.x</a>

### 数据库
MySQL 5.6, 5.7

Magento同样支持MySQL NDB Cluster 7.4.&#42;, MariaDB 10.0, 10.1, 10.2, Percona 5.7以及其他的基于MySQL兼容的技术的数据库.

<div class="bs-callout bs-callout-info" id="info" markdown="1">
Magento仅支持MariaDB使用和MySQL兼容的特征，MariaDB并不完全兼容MySQL的所有特征，所以将你应用一个新的特征到Magento模块时，你应当先研究一下它们的兼容性,
</div>

### PHP
{% include install/php_2.2.md %}

#### 所需的PHP扩展

<div class="bs-callout bs-callout-info" id="info" markdown="1">
[CentOS]({{ page.baseurl }}/install-gde/prereq/php-centos.html)和[Ubuntu]({{ page.baseurl }}/install-gde/prereq/php-ubuntu.html)下php安装命令包含了安装他们扩展的步骤
</div>

*	<a href="http://php.net/manual/en/book.bc.php" target="&#95;blank">bc-math</a> ({{site.data.var.ee}} 仅2.2.0 - 2.2.3. {{site.data.var.ee}}及{{site.data.var.ce}}2.2.4以下.)
* <a href="http://php.net/manual/en/book.ctype.php" target="&#95;blank">ctype</a>
*	<a href="http://php.net/manual/en/book.curl.php" target="&#95;blank">curl</a>
* <a href="http://php.net/manual/en/book.dom.php" target="&#95;blank">dom</a>
*	<a href="http://php.net/manual/en/book.image.php" target="&#95;blank">gd</a>, <a href="http://php.net/manual/en/book.imagick.php" target="&#95;blank">ImageMagick 6.3.7</a>(或更新版本)或两个都装
*	<a href="http://php.net/manual/en/book.intl.php" target="&#95;blank">intl</a>
*	<a href="http://php.net/manual/en/book.mbstring.php" target="&#95;blank">mbstring</a>
*	<a href="http://php.net/manual/en/book.mcrypt.php" target="&#95;blank">mcrypt</a>
*	<a href="http://php.net/manual/en/book.hash.php" target="&#95;blank">hash</a>
*	<a href="http://php.net/manual/en/book.openssl.php" target="&#95;blank">openssl</a>
*	<a href="http://php.net/manual/en/ref.pdo-mysql.php" target="&#95;blank">PDO/MySQL</a>
*	<a href="http://php.net/manual/en/book.simplexml.php" target="&#95;blank">SimpleXML</a>
*	<a href="http://php.net/manual/en/book.soap.php" target="&#95;blank">soap</a>
* <a href="http://php.net/manual/en/book.spl.php" target="&#95;blank">spl</a>
*	<a href="http://php.net/manual/en/book.libxml.php" target="&#95;blank">libxml</a>
*	<a href="http://php.net/manual/en/book.xsl.php" target="&#95;blank">xsl</a>
*	<a href="http://php.net/manual/en/book.zip.php" target="&#95;blank">zip</a>
*	[json](http://php.net/manual/en/book.json.php){:target="&#95;blank"}
*	[iconv](http://php.net/manual/en/book.iconv.php){:target="&#95;blank"}

#### PHP OPcache
基于性能的原因，我们强烈建议你检查你的<a href="http://php.net/manual/en/intro.opcache.php" target="&#95;blank">PHP OPcache</a>是否开启. 在多数PHP中OPcache都是开启的. 要验证你是否已经正确安装, 请参考我们的<a href="{{ page.baseurl }}/install-gde/prereq/php-centos.html" target="&#95;blank">CentOS</a>或<a href="{{ page.baseurl }}/install-gde/prereq/php-ubuntu.html" target="&#95;blank">Ubuntu</a>的PHP文档.

如果你要单独地安装OPcache, 请参考<a href="http://php.net/manual/en/opcache.setup.php" target="&#95;blank">PHP OPcache安装文档</a>.

#### PHP配置
我们建议您修改PHP的一些配置, 诸如 `memory_limit`,这样可以避免在使用Magento的过程中的一些常见的问题

了解更多, 请参考[PHP配置要求]({{ page.baseurl }}/install-gde/prereq/php-settings.html).

### SSL
*	要使用Https你需要一个有效的{% glossarytooltip 363d6806-6a7d-4cb6-bc47-efc62bc26a1c %}安全证书{% endglossarytooltip %}
*	自己签发的证书是不支持的
*	传输层安全协议(TLS)要求 - PayPal和`repo.magento.com`都要求使用TLS 1.1或更新的版本:

	*	[关于PayPal的更多信息]({{ page.baseurl }}/install-gde/system-requirements_tls1-2.html)

	*	[`repo.magento.com`的更多信息](http://devdocs.magento.com/guides/v2.1/release-notes/tech_bull_tls-repo.html)

### 邮件服务server
邮件收发代理(MTA) 或一个简单邮件服务(SMTP)

### Magento能使用以下技术:
*	页面缓存及Session存储<a href="{{ page.baseurl }}/config-guide/redis/config-redis.html">Redis</a>版本3.2 (兼容2.4+ )
*	<a href="{{ page.baseurl }}/config-guide/varnish/config-varnish.html">Varnish</a>版本4.x或5.0
*	用于session存储的<a href="{{ page.baseurl }}/config-guide/memcache/memcache.html">memcached</a>(最新的稳定版)，您可以选择使用PHP的`memcache`或`memcached`扩展(最新的稳定版)连接它们

####	仅{{site.data.var.ee}}支持

*	Elasticsearch

    {{site.data.var.ee}}(版本2.2.x)支持以下的Elasticsearch版本:

    *	Elasticsearch [5.x](https://www.elastic.co/downloads/past-releases/elasticsearch-5-2-2){:target="&#95;blank"}
    *	Elasticsearch [2.x](https://www.elastic.co/downloads/past-releases/elasticsearch-2-4-5){:target="&#95;blank"}

    Magento 2.2.3 使用[Elasticsearch PHP客户端](https://github.com/elastic/elasticsearch-php){:target="&#95;blank"}(版本5.1).在2.2.3以前使用的PHP客户端是2.0.

*	RabbitMQ 3.5.x (兼容2.0及其以上)

    [RabbitMQ]({{ page.baseurl }}/config-guide/mq/rabbitmq-overview.html){:target="&#95;blank"}用于发布消息到队列，供用户订阅和导步地接收.

*	三个主数据库

    这些<a href="{{ page.baseurl }}/config-guide/multi-master/multi-master.html">主数据库</a>为Magento2应用程序的不同功能区提供了可伸缩的优势, 诸如checkout, 下单, 以及Magento2应用程序的所有数据表.

### 可选的建议:
*	<a href="http://xdebug.org/download.php" target="&#95;blank">php_xdebug2.2.0</a>或更高(仅安装在开发环境; 启用它是会影响性能的)

<div class="bs-callout bs-callout-info" id="info">
	<p>这是一个我们已知关于<code>xdebug</code影响Magento安装和安装后网站前台和后台访问的问题</p>
	<p>详情请参考<a href="{{ page.baseurl }}/install-gde/trouble/tshoot_install-issues.html">已知的影响</a>.</p>
</div>

*	PHPUnit (作为一个命令行工具安装) 6.2.0

### 文档
<a href="{{ page.baseurl }}/install-gde/prereq/prereq-overview.html">安装Magento所需的环境</a>
