---
group: install_cli
title: 备份和还原文件系统，媒体文件和数据库
version: 2.1
github_link: install-gde/install/cli/install-cli-backup.md
redirect_from:
  - /guides/v1.0/install-gde/install/install-cli-backup.html
  - /guides/v2.0/install-gde/install/install-cli-backup.html
functional_areas:
  - Install
  - System
  - Setup
---


<h2 id="instgde-cli-uninst-back-over">Overview of backup</h2>
This command enables you to back up:

*	The Magento file system (excluding <code>var</code>和<code>pub/static</code> directories)
*	The <code>pub/media</code> directory
*	The Magento 2 database

Backups are stored in the `var/backups` directory and can be restored at any time using the <a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-uninstall-mods.html#instgde-cli-uninst-mod-roll">magento setup:rollback</a> command.

After backing up, you can <a href="#instgde-cli-uninst-roll">roll back</a> at a later time.

<h2 id="instgde-cli-before">第一步</h2>
{% include install/first-steps-cli.html %}
我们不止在这里讨论命令参数，更多请参考<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands.html#instgde-cli-subcommands-common">命令参数</a>.

## Set ulimit for the web server user {#instgde-cli-ulimit}
{% include install/ulimit.md %}

<h2 id="instgde-cli-uninst-back">Backing up</h2>
命令用法：

	magento setup:backup [--code] [--media] [--db]

此命令执行以下任务：

1.	将网店设置为维护模式。
2.	执行以下命令选项之一。

	<table>
	<col width="25%">
	<col width="40%">
	<col width="35%">
	<tbody>
		<tr>
			<th>Option</th>
			<th>Meaning</th>
			<th>备份文件的名字和位置</th>
		</tr>
		
	<tr>
		<td><p>--code</p></td>
		<td><p>备份Magento文件系统(不包括 <code>var</code>和<code>pub/static</code>目录).</p></td>
		<td><p>var/backups/&lt;时间戳>_filesystem.tgz</p></td>
	</tr>
	<tr>
		<td><p>--media</p></td>
		<td><p>备份<code>pub/media</code>目录.</p></td>
		<td><p>var/backups/&lt;时间戳>_filesystem_media.tgz</p></td>
	</tr>
	<tr>
	<tr>
		<td><p>--db</p></td>
		<td><p>备份Magento2的数据库.</p></td>
		<td><p>var/backups/&lt;时间戳>_db.sql</p></td>
	</tr>
	<tr>
	</tbody>
	</table>

3.	离开维护模式。

例如，要同时备份文件系统和数据库

	magento setup:backup --code --db

命令行将有以下输出信息：

	Enabling maintenance mode
	Code backup is starting...
	Code backup filename: 1434133011_filesystem.tgz (The archive can be uncompressed with 7-Zip on Windows systems)
	Code backup path: /var/www/html/magento2/var/backups/1434133011_filesystem.tgz
	[SUCCESS]: Code backup completed successfully.
	DB backup is starting...
	DB backup filename: 1434133011_db.sql
	DB backup path: /var/www/html/magento2/var/backups/1434133011_db.sql
	[SUCCESS]: DB backup completed successfully.
	Disabling maintenance mode

<h2 id="instgde-cli-uninst-roll">Roll back</h2>
这一节讨论如何回滚还原到一个你之前的备份上，你必须知道你要恢复的备份文件的名称。

要想找到你备份文件的名称，可以执行：

	magento info:backups:list

备份文件的前缀是一个时间戳。

要还原到一个先前的备份，执行：

	magento setup:rollback [-c|--code-file="<name>"] [-m|--media-file="<name>"] [-d|--db-file="<name>"]

例如，要恢复到一个之前的备份文件，文件名是`1440611839_filesystem_media.tgz`, 执行

	magento setup:rollback -m 1440611839_filesystem_media.tgz

命令行将有以下输出信息：

	[SUCCESS]: Media rollback completed successfully.
	Please set file permission of bin/magento to executable
	Disabling maintenance mode

<div class="bs-callout bs-callout-info" id="info">
  <p>如果执行结果出现<code>一段故障</code>信息，请参考<a href="{{ page.baseurl }}/install-gde/trouble/tshoot_segfault.html">回滚还原故障</a>.</p>
</div>