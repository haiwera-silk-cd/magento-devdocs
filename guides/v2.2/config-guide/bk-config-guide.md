---
group: config-guide
subgroup: 01_Introduction
title: 配置手册
landing-page: 配置手册
menu_title: 介绍
menu_order: 1
menu_node: parent
version: 2.2
github_link: config-guide/bk-config-guide.md
functional_areas:
  - Configuration
  - System
  - Setup
---

<h2 id="configuration">配置Magento应用</h2>
You can 配置Magento应用 in any of the following ways:

*	General configuration

	*  	Using a <a href="{{ page.baseurl }}/config-guide/cli/config-cli.html">command-line utility</a> (for example, enable or disable cache types, run indexers, set up translations, and so on)
	*  	Manually to set up <a href="{{ page.baseurl }}/config-guide/bootstrap/magento-bootstrap.html">bootstrap parameters</a>

*	Caching

	*	[Set up Varnish]({{ page.baseurl }}/config-guide/varnish/config-varnish.html)
	* [Set up caching]({{ page.baseurl }}/config-guide/cache.html)
	*	[使用Redis作为Magento页面缓存和默认缓存]({{ page.baseurl }}/config-guide/redis/redis-pg-cache.html)
	*	[使用Redis作为Session存储]({{ page.baseurl }}/config-guide/redis/redis-session.html)
	*	[Set up database caching]({{ page.baseurl }}/config-guide/cache/caching-database.html)

*	生产环境的Magento

	*	[pipeline deployment]({{ page.baseurl }}/config-guide/deployment/pipeline/)
	*	[Magento开发环境和生产环境的所有者和权限]({{ page.baseurl }}/config-guide/prod/prod_file-sys-perms.html)
	*	[单机部署]({{ page.baseurl }}/config-guide/deployment/single-machine.html)

*	Session storage
	*	[memcache]({{ page.baseurl }}/config-guide/memcache/memcache.html)
	*	[Redis]({{ page.baseurl }}/config-guide/redis/redis-session.html)
	*	[How to locate session files]({{ page.baseurl }}/config-guide/sessions.html)

*	{{site.data.var.ee}} only

	*	[安装和配置Elasticsearch]({{ page.baseurl }}/config-guide/elasticsearch/es-overview.html)
	*	<a href="{{ page.baseurl }}/config-guide/multi-master/multi-master.html">Split databases</a>
	*	<a href="{{ page.baseurl }}/config-guide/mq/rabbitmq-overview.html">消息队列</a>
