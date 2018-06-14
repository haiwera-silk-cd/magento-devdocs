---
group: config-guide
subgroup: 04_CLI
title: 运行Magento支持工具
menu_title: 运行Magento支持工具 (仅企业版适用)
menu_node:
menu_order: 900
version: 2.1
ee_only: True
github_link: config-guide/cli/config-cli-subcommands-spt-util.md
functional_areas:
  - Configuration
  - System
  - Setup
---

{% include config/cli-intro.md %}

## 概述 of the support utilities {#config-cli-spt-utils-over}
The Magento support utilities (also referred to as the [*Data Collector*](http://docs.magento.com/m2/ee/user_guide/system/support-data-collector.html){:target="\_blank"}) enable {{site.data.var.ee}} users to gather troubleshooting information about your system that can be used by our Support team.

Magento Support uses these backups (also referred to as *dumps*) to analyze issues that require access to your code. A typical scenario follows:

1.  You're having an issue with your Magento store and you contact Magento Support.
2.  Support determines they need to see your code or database to reproduce the issue.
3.  You back up the code to a `.tar.gz` file.

	This backup *excludes* your media files to speed up the process and to result in a much smaller file.
4.  You back up the database to a `.tar.gz` file.

	By default, [sensitive data](#sens-data) is hashed when making the backup.
5.  You upload your backups to a file sharing service.
6.  Support analyzes your issues without affecting your development or production environment.

The utilities can take several minutes to complete.

## Create a code backup {#config-cli-spt-utils-code}
This command backs up code and compresses it in `tar.gz` format.

{% include config/code-backup.md %}

命令参数：

	bin/magento support:backup:code [--name=<file name>] [-o|--output=<path>] [-l|--logs]

Where:

-   **`--name`** specifies the dump file name (optional). If you omit this parameter, the dump file is time and date-stamped.
-   **`-o|--output=<path>`** is the absolute file system path to store the backup (required).
-   **`-l|--logs`** includes log files (optional).

For example, to create a code backup named `/var/www/html/magento2/var/log/mycodebackup.tar.gz`:

	bin/magento support:backup:code --name mycodebackup -o /var/www/html/magento2/var/log

After the command completes, provide the code backup to Magento Support.

## Create a database backup {#config-cli-spt-utils-db}
This command backs up the Magento database and compresses it in `tar.gz` format.

{% include config/code-backup.md %}

命令参数：

	bin/magento support:backup:db [--name=<name>] [-o|--output=<path>] [-l|--logs] [-i|--ignore-sanitize]

Where:

-   **`--name`** specifies the dump file name (optional). If you omit this parameter, the dump file is time and date-stamped.
-   **`-o|--output=<path>` is the absolute file system path to store the backup (required).
-   **`-l|--logs`** includes log files (optional).
-   **`-i|--ignore-sanitize`** means that data is preserved; omit the flag to hash [sensitive data](#sens-data) stored in the database when creating the backup (optional).

After the command completes, provide the database backup to Magento Support.

{% include install/sens-data.md %}

## 故障排除: display utilities and paths {#config-cli-spt-utils-trouble}
We provide commands that display paths to utilities required by the Data Collector and the command line. You can use these commands, for example, if errors like the following display in the {% glossarytooltip 29ddb393-ca22-4df9-a8d4-0024d75739b1 %}Admin{% endglossarytooltip %} or on the command line:

	Utility lsof not found

Run the following commands in the order shown to display the paths to the applications used by the support utilities and Data Collector:

1.  Change to your Magento installation directory.

  For example, `cd /var/www/magento2`

	<div class="bs-callout bs-callout-info" id="info" markdown="1">
  The commands run properly _only_ from your Magento installation directory.
	</div>
2.  `php bin/magento support:utility:paths` creates `<your Magento install dir>/var/support/Paths.php`, which lists the paths to all application used by the utility.
3.  `php bin/magento support:utility:check` displays the file system paths.

A sample follows:

	gzip => /bin/gzip
	lsof => /usr/sbin/lsof
	mysqldump => /usr/bin/mysqldump
	nice => /bin/nice
	php => /usr/bin/php
	tar => /bin/tar
	sed => /bin/sed
	bash => /bin/bash
	mysql => /usr/bin/mysql

To resolve issues with running the tools, make sure these applications are installed and are in the web server user's `$PATH` environment variable.

#### 相关主题

-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-cache.html">管理缓存</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-index.html">管理索引</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-cron.html">配置和执行定时任务</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-compiler.html">代码编译器</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-urn.html">统一资源名称(URN)高亮</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-depen.html">依赖报告</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-i18n.html">翻译字典和语言包</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-static-view.html">部署静态视图文件</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-less-sass.html">创建软链接到LESS文件</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-test.html">运行单元测试</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-layout-xml.html">转换布局的XML文件</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-perf-data.html">为性能测试生成数据</a>
