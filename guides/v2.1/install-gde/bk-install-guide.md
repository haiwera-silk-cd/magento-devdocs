---
group: install2
subgroup: 起步
title: 如何获取Magento
landing-page: 安装向导
menu_title: 如何获取Magento
menu_node:
menu_order: 1
version: 2.1
github_link: install-gde/bk-install-guide.md
redirect_from:
  - /guides/v2.0/install-gde/continue.html
  - /guides/v2.1/install-gde/continue.html
  - /guides/v1.0/install-gde/bk-install-guide.html
  - /guides/v2.0/install-gde/install/install-merchbeta.html
functional_areas:
  - Install
  - System
  - Setup
---

## Magento安装

你好，非常荣幸作为24万店主之一的您选择了信任我们的电商软件，我们收集了帮助你初步了解和安装Magento的信息

这有一些帮助你入门的资料关于你将用到的电商平台 -- Magento 2

这正是我们做的.

## 获取Magento {#install-get-software}

要安装{{site.data.var.ce}}或{{site.data.var.ee}}.下面这张表格将告诉你如何开始。

<table>
	<tbody>
		<tr>
			<th>你需要</th>
			<th>描述</th>
			<th>应用级安装和升级步骤</th>
			<th>开始安装</th>
		</tr>
	<tr>
		<td><p>简单的安装（有命令行工具, 有自己的服务器）</p></td>
		<td><p>一点专业知识，能用命令行访问你要部署服务器.</p>
			<p>您可以使用<a href="{{ page.baseurl }}/install-gde/install/web/install-web.html">向导安装</a>或<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli.html">命令行</a>来安装Magento及其扩展.</p>
		<p>你<em>不能</em>使用向导页来升级它们. 必须使用<a href="{{ page.baseurl }}/install-gde/install/cli/dev_reinstall.html">Composer</a>和<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli.html">命令行</a>.</p></td>
		<td><ol><li>下载Magento的压缩包</li>
			<li>自己或让网管在服务器上解压</li>
			<li>使用命令行或网页向导安成安装步骤</li>
			<li>在命令行执行Composer升级和升级命令</li></ol>
		</td>
		<td><p><a href="{{ page.baseurl }}/install-gde/prereq/zip_install.html">安装包 (拥有服务器)</a></p></td>
	</tr>
	<tr>
		<td><p>集成, 组装</p></td>
		<td><p>想要完全控制所有组件的安装，有服务器权限和非常专业知识，可能要引入{{site.data.var.ce}}的其它的组件进行重新定制</p>
		<p>可以使用<a href="{{ page.baseurl }}/install-gde/install/web/install-web.html">网页向导</a>或<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli.html">命令行</a>安装Magento及其扩展.</p>
		<p>也能够使用<a href="{{ page.baseurl }}/comp-mgr/bk-compman-upgrade-guide.html">网页向导</a>或<a href="{{ page.baseurl }}/comp-mgr/cli/cli-upgrade.html">命令行</a>进行升级.</p></td>
		<td><ol><li>创建一个包含组件清单的Composer<em>项目</em></li>
			<li>使用Composer更新包依赖;使用<code>composer create-project</code>获取Magento工程包</li>
			<li>使用命令行或网页向导进行安装.</li>
		<li>通过命令行或网页向导更新Magento及其扩展.</li></ol>
		<td><p><a href="{{ page.baseurl }}/install-gde/prereq/integrator_install.html">获取工程包</a></p></td>
	</td>

	</tr>
	<tr>
		<td><p>参与贡献</p></td>
		<td><p>贡献Magento的基础代码，提Bug及参与定制Magento.有专业的技能，自己的开发服务器。熟悉Composert GitHub.</p>
			<p>允许使用<a href="{{ page.baseurl }}/install-gde/install/web/install-web.html">网页向导</a>或<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli.html">命令行</a>安装Magento及其扩展.</p>
			<p>但<em>不能</em>用到生产环境.</p>
      <p>也<em>不能</em>使用网页向导升级Magento及其扩展.必须使用<a href="{{ page.baseurl }}/install-gde/install/cli/dev_options.html">Composer和git命令</a>.</p></td>
		<td><ol><li>从github上Clones Magento 2的仓库.</li>
			<li>用composer安装依赖</li>
			<li>使用命令行或网页向导安装</li>
			<li>使用composer或git命令进行升级</li>
			<li>在<code>app/code</code>目录下编写你的代码.</li></ol></td>
		<td><p><a href="{{ page.baseurl }}/install-gde/prereq/dev_install.html">Clone Magento仓库</a></p></td>
	</tr>
	</tbody>
</table>

## 有用的信息

在你安装的过程中,take advantage of our [快速安装参考（教程）] or [一步步安装(参考)]. They're really easy to use; the tutorial walks you through a sample installation. The roadmap provides links to common tasks throughout the guide.

Use the links on the left side of the page to navigate topics in each part of the installation.

## 要求的服务器权限

UNIX systems require `root` privileges to install and configure software like a web server, PHP, and so on. If you need to install this software, make sure you have `root` access.

You should *not* install the Magento software in the web server docroot as the `root` user because the web server might not be able to interact with those files.

You'll also need `root` privileges to create the [Magento文件系统所有者] and add that owner to the web server's group. You'll use the {% glossarytooltip 5e7de323-626b-4d1b-a7e5-c8d13a92c5d3 %}Magento文件系统所有者{% endglossarytooltip %} to run any commands from the 命令行 and to set up the Magento cron job, which schedules tasks for you.

<!-- LINK DEFINITIONS -->

[快速安装参考（教程）]: {{ page.baseurl }}/install-gde/install-quick-ref.html
[一步步安装(参考)]: {{ page.baseurl }}/install-gde/install-roadmap_part1.html
[Magento文件系统所有者]: {{ page.baseurl }}/install-gde/prereq/file-sys-perms-over.html
