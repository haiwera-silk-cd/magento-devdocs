---
group: config-guide
subgroup: 04_CLI
title: 命令行配置起步
menu_title: 命令行配置起步
menu_node:
menu_order: 2
version: 2.0
github_link: config-guide/cli/config-cli-subcommands.md
redirect_from: /guides/v1.0/config-guide/cli/config-cli-subcommands.html
functional_areas:
  - Configuration
  - System
  - Setup
---

## Before you 配置Magento应用 {#config-install-cli-prereq}
{% include install/before-you-begin-cli.html %}

## 第一步 {#config-cli-before}
1.  Log in to the Magento server as, or switch to, the <a href="{{ page.baseurl }}/install-gde/prereq/file-sys-perms-over.html">Magento文件系统所有者</a>.
2.  Change to the following directory:

        cd <your Magento install dir>/bin

    例如:

      - Ubuntu: `cd /var/www/magento2/bin`
      - CentOS: `cd /var/www/html/magento2/bin`

<div class="bs-callout bs-callout-tip" markdown="1">
You can run the commands in any of the following ways:

-   `php magento <command>`
-   `./magento <command>`
-   `magento <command>` (after [adding](http://unix.stackexchange.com/questions/117467/how-to-permanently-set-environmental-variables){:target="\_blank"} `<your Magento install dir>/bin` to your system `PATH`)
</div>

## Command summary {#config-cli-summary}
下面的表格总结了可用的命令，每个命令只引用了简要信息，关于命令的更多信息请点击对应列的链接。

<div class="bs-callout bs-callout-info" id="info" markdown="1">
Before you run any of these commands, you must either [install the Magento application]({{ page.baseurl }}/install-gde/install/cli/install-cli.html) or [enable some modules]({{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands-enable.html).
</div>

<table>
	<col width="40%">
  	<col width="30%">
  	<col width="30%">
	<tbody>
		<tr>
			<th>命令</th>
			<th>描述</th>
		</tr>

	<tr>
		<td><a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-cache.html">magento setup:cache:{enable|disable|clean|flush|status}</a></td>
		<td><p>Manages the cache</p></td>
	</tr>
	<tr>
		<td><a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-index.html">magento setup:indexer:{status|show-mode|set-mode|reindex|info}</a></td>
		<td><p>Manages the indexers</p></td>
	</tr>

	<tr>
		<td><a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-cron.html">magento cron:run</a></td>
		<td><p>Runs Magento cron jobs</p></td>
	</tr>
	<tr>
		<td><a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-compiler-multi.html">magento setup:di:compile-multi-tenant</a></td>
		<td><p>Use only if you have multiple independent Magento applications (in other words, one common Magento code base but more than one independent instance of the Magento application).</p>
		<p>Compiles all non-existent proxies and factories; and pre-compiles class definitions, inheritance information, and plugin definitions for multiple stores or websites.</p></td>
	</tr>
	<tr>
		<td><a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-compiler-single.html">magento setup:di:compile</a></td>
		<td><p>Use if you have one instance of the Magento application.</p>
			<p>Compiles all non-existent proxies and factories; and pre-compiles class definitions, inheritance information, and plugin definitions for one store and website.</p></td>
	</tr>
	<tr>
		<td><a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-depen.html">magento info:dependencies:{show-modules|show-modules-circular|show-framework}e</a></td>
		<td><p>模块依赖, circular dependencies, and Magento framework dependencies.</p></td>
	</tr>
	<tr>
		<td><a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-i18n.html">magento i18n:{collect-phrases|pack}</a></td>
		<td><p>Creates a translation dictionary or a translation package</p></td>
	</tr>
	<tr>
		<td><a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-static-view.html">magento setup:static-content:deploy</a></td>
		<td><p>Deploys static view files</p></td>
	</tr>
	<tr>
		<td><a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-less-sass.html">magento dev:source-theme:deploy</a></td>
		<td><p>Creates CSS from LESS</p></td>
	</tr>
	<tr>
		<td><a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-test.html">magento dev:tests:run</a></td>
		<td><p>Runs automated tests</p></td>
	</tr>
	<tr>
		<td><a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-layout-xml.html">magento dev:xml:convert</a></td>
		<td><p>Update your layout XML files to match the new Extensible Stylesheet Language Transformations (XSLT) stylesheet</p></td>
	</tr>
	<tr>
		<td><a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-perf-data.html">magento setup:perf:generate-fixtures</a></td>
		<td><p>Generate data to use for performance testing.</p></td>
	</tr>
	<tr>
		<td><a href="{{ page.baseurl }}/install-gde/install/sample-data.html#instgde-install-sample-enable-after">magento sampledata:install</a></td>
		<td><p>Installs optional Magento sample data after you install the Magento application.</p>
			<p>For more details about Magento sample data, see <a href="{{ page.baseurl }}/install-gde/install/sample-data.html">Optional Magento sample data</a>.</p></td>
	</tr>

	</tbody>
</table>

## Help commands {#config-cli-help}
{% include install/cli_help-commands.html %}

## Common arguments {#config-cli-subcommands-common}
{% include install/cli_common-commands.html %}

## Commands {#config-cli-subcommands}
下面的章节讨论了一些可用的命令。

-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-cache.html">管理缓存</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-index.html">管理索引</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-cron.html">配置和执行定时任务</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-compiler.html">代码编译器</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-mode.html">设置Magento的模式</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-urn.html">统一资源名称(URN)高亮</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-depen.html">依赖报告</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-i18n.html">翻译字典和语言包</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-static-view.html">部署静态视图文件</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-less-sass.html">创建软链接到LESS文件</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-test.html">运行单元测试</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-layout-xml.html">转换布局的XML文件</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-perf-data.html">为性能测试生成数据</a>
