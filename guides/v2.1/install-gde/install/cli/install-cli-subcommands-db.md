---
group: install_cli
title: Create the Magento database schema
version: 2.1
github_link: install-gde/install/cli/install-cli-subcommands-db.md
redirect_from:
  - /guides/v1.0/install-gde/install/install-cli-subcommands-db.html
  - /guides/v2.0/install-gde/install/install-cli-subcommands-db.html
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

<h2 id="instgde-cli-dbconfig">配置数据库并添加数据</h2>
命令用法：

	magento setup:db-schema:upgrade
	magento setup:db-data:upgrade

要想知道数据库的状态，执行

	magento setup:db:status