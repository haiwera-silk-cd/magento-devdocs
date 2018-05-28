---
group: install2
subgroup: 起步
title: 如何获取Magento
landing-page: 安装向导
menu_title: 如何获取Magento
menu_node:
menu_order: 1
version: 2.0
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

Hi, we're glad you're among the 240,000 merchants worldwide who put their trust in our eCommerce software. We've gathered some information to help you get started with Magento and with your Magento installation.

We have some resources here to help get you started using the eCommerce platform of the future&mdash;Magento 2.

It’s what we do.

## 如何获取Magento {#install-get-software}

Consult the following table for how to get started installing {{site.data.var.ce}} or {{site.data.var.ee}}.

<table>
	<tbody>
		<tr>
			<th>用户需要</th>
			<th>描述</th>
			<th>高层的安装或升级步骤</th>
			<th>起步链接</th>
		</tr>
	<tr>
		<td><p>Easy installation, command line, have your own server</p></td>
		<td><p>Some technical expertise, command line access to the Magento server.</p>
			<p>Enables you to install the Magento software and extensions using either the <a href="{{ page.baseurl }}/install-gde/install/web/install-web.html">网页安装向导</a> or the <a href="{{ page.baseurl }}/install-gde/install/cli/install-cli.html">command line</a>.</p>
		<p>You <em>cannot</em> use the 网页安装向导 to upgrade the Magento software and extensions. You must upgrade using <a href="{{ page.baseurl }}/install-gde/install/cli/dev_reinstall.html">Composer</a> and the <a href="{{ page.baseurl }}/install-gde/install/cli/install-cli.html">command line</a>.</p></td>
		<td><ol><li>Downloads a compressed file that contains the Magento software.</li>
			<li>Extracts it on the Magento server or asks a network administrator to do so.</li>
			<li>Installs the Magento software using the 网页安装向导 or command line.</li>
			<li>Upgrades the Magento application and extensions using Composer and the command line.</li></ol>
		</td>
		<td><p><a href="{{ page.baseurl }}/install-gde/prereq/zip_install.html">Easy installation (own server)</a></p></td>
	</tr>
	<tr>
		<td><p>Integrator, packager</p></td>
		<td><p>Wants full control over all 组件 installed, has access to the Magento server, highly technical, might repackage {{site.data.var.ce}} with other 组件.</p>
		<p>Enables you to install the Magento software and extensions using either the <a href="{{ page.baseurl }}/install-gde/install/web/install-web.html">网页安装向导</a> or the <a href="{{ page.baseurl }}/install-gde/install/cli/install-cli.html">command line</a>.</p>
		<p>You can also upgrade the Magento application and extensions using the <a href="{{ page.baseurl }}/comp-mgr/bk-compman-upgrade-guide.html">网页安装向导</a>或<a href="{{ page.baseurl }}/comp-mgr/cli/cli-upgrade.html">command line</a>.</p></td>
		<td><ol><li>Creates a Composer <em>project</em> that contains the list of 组件 to use.</li>
			<li>Uses Composer to update package dependencies; uses <code>composer create-project</code> to get the Magento metapackage.</li>
			<li>Installs the Magento software using either a command line or the Setup Wizard.</li>
		<li>Upgrades the Magento application and extensions using the 网页安装向导 or command line.</li></ol>
		<td><p><a href="{{ page.baseurl }}/install-gde/prereq/integrator_install.html">Get the metapackage</a></p></td>
	</td>

	</tr>
	<tr>
		<td><p>Contributing developer</p></td>
		<td><p>Contributes to the Magento codebase, files bugs, and customizes the Magento software. Highly technical, has their own Magento development server, understands Composer and GitHub.</p>
			<p>Enables you to install the Magento software and extensions using either the <a href="{{ page.baseurl }}/install-gde/install/web/install-web.html">网页安装向导</a> or the <a href="{{ page.baseurl }}/install-gde/install/cli/install-cli.html">command line</a>.</p>
			<p>You <em>cannot</em> use Magento in a production environment.</p>
      <p>You <em>cannot</em> use the 网页安装向导 to upgrade the Magento software and extensions. You must upgrade using <a href="{{ page.baseurl }}/install-gde/install/cli/dev_options.html">Composer and git commands</a>.</p></td>
		<td><ol><li>Clones the Magento 2 GitHub repository.</li>
			<li>Uses Composer to update package dependencies.</li>
			<li>Installs the Magento software using either a command line or the Setup Wizard.</li>
			<li>Upgrades the Magento software using Composer and GitHub commands.</li>
			<li>Customizes code under the <code>app/code</code> directory.</li></ol></td>
		<td><p><a href="{{ page.baseurl }}/install-gde/prereq/dev_install.html">Clone the Magento repository</a></p></td>
	</tr>


	</tbody>
</table>

## 有用的信息

在你安装的过程中,take advantage of our [快速安装参考（教程）] or [一步步安装(参考)]. They're really easy to use; the tutorial walks you through a sample installation. The roadmap provides links to common tasks throughout the guide.

Use the links on the left side of the page to navigate topics in each part of the installation.

## 要求的服务器权限

UNIX systems require `root` privileges to install and configure software like a web server, PHP, and so on. If you need to install this software, make sure you have `root` access.

You should *not* install the Magento software in the web server docroot as the `root` user because the web server might not be able to interact with those files.

You'll also need `root` privileges to create the [Magento文件系统所有者] and add that owner to the web server's group. You'll use the {% glossarytooltip 5e7de323-626b-4d1b-a7e5-c8d13a92c5d3 %}Magento文件系统所有者{% endglossarytooltip %} to run any commands from the command line and to set up the Magento cron job, which schedules tasks for you.

<!-- LINK DEFINITIONS -->

[快速安装参考（教程）]: {{ page.baseurl }}/install-gde/install-quick-ref.html
[一步步安装(参考)]: {{ page.baseurl }}/install-gde/install-roadmap_part1.html
[Magento文件系统所有者]: {{ page.baseurl }}/install-gde/prereq/file-sys-perms-over.html
