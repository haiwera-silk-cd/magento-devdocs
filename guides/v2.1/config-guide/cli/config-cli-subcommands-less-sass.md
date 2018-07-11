---
group: config-guide
subgroup: 04_CLI
title: 创建软链接到LESS文件
menu_title: 创建软链接到LESS文件
menu_node:
menu_order: 350
version: 2.1
github_link: config-guide/cli/config-cli-subcommands-less-sass.md
redirect_from: /guides/v1.0/config-guide/cli/config-cli-subcommands-less-sass.html
functional_areas:
  - Configuration
  - System
  - Setup
---

{% include config/cli-intro.md %}

## Create LESS files {#config-cli-subcommands-less-sass}
Use this command to create symlinks to LESS files.

命令参数：

	bin/magento dev:source-theme:deploy [--type="..."] [--locale="..."] [--area="..."] [--theme="..."] [file1] ... [fileN]

The following table explains this command's parameters and values.

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
		<td><p>--type</p></td>
		<td><p>Type of source files: [less] (default: "less")</p>
			<p>Currently, LESS is the only file type supported.</p></td>
		<td><p>否</p></td>
	</tr>
	<tr>
		<td><p>--locale</p></td>
		<td><p>Locale code.</p>
			<p>To display the list of locale codes, enter <code>bin/magento info:language:list</code></p></td>
		<td><p>否</p></td>
	</tr>
	<tr>
		<td><p>--area</p></td>
		<td><p>Area (<code>adminhtml</code> for the administrative area, <code>frontend</code> for the storefront).</p></td>
		<td><p>否</p></td>
	</tr>
	<tr>
		<td><p>--theme</p></td>
		<td><p>Theme name in <code>&lt;VendorName>/&lt;theme name></code> format. 例如， <code>Magento/blank</code>或<code>Magento/backend</code>.</p></td>
		<td><p>否</p></td>
	</tr>
	<tr>
		<td><p>&lt;file></p></td>
		<td><p>Space-separated list of CSS files to convert to LESS without the <code>.css</code> extension. (Default is <code>css/styles-m css/styles-l</code>, for adminhtml type <code>css/styles css/styles-old</code>)</p></td>
		<td><p>否</p></td>
	</tr>
	</tbody>
</table>

例如， to create LESS files for the frontend theme named `VendorName/themeName` in the `en_US` locale using a CSS file named `<your Magento install dir>/pub/static/frontend/VendorName/themeName/en_US/css/styles-l.css`, enter the following command:

	bin/magento dev:source-theme:deploy --type="less" --locale="en_US" --area="frontend" --theme="VendorName/themeName" css/styles-l

The following messages display to confirm success:

	Processed Area: frontend, Locale: en_US, Theme: VendorName/themeName, File type: less.
	-> css/styles-l.less
	Successfully processed.

To create LESS files for the adminhtml, enter the following command:

	bin/magento dev:source-theme:deploy --locale="en_US" --area="adminhtml" --theme="Magento/backend" css/styles css/styles-old

#### 相关主题

-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-cache.html">管理缓存</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-index.html">管理索引</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-cron.html">配置和执行定时任务</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-compiler.html">代码编译器</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-mode.html">设置Magento的模式</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-urn.html">统一资源名称(URN)高亮</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-depen.html">依赖报告</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-i18n.html">翻译字典和语言包</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-static-view.html">部署静态视图文件</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-test.html">运行单元测试</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-layout-xml.html">转换布局的XML文件</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-perf-data.html">为性能测试生成数据</a>
