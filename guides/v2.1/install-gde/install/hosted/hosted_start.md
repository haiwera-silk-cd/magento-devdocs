---
group: install_hosted
subgroup: 02_config-hosted
title: 配置你的主机系统
menu_title: 配置你的主机系统
menu_order: 1
menu_node: parent
version: 2.1
github_link: install-gde/install/hosted/hosted_start.md
functional_areas:
  - Install
  - System
  - Setup
---

## Hosted installation
Before you can install the Magento software, you must get your hosted system ready.  

If your hosted system is already set up, go to <a href="{{ page.baseurl }}/install-gde/install/hosted/hosted_get-ftp.html#get-archive">获取Magento packages</a>.

#### Contents
*	<a href="#newbie-verify">Verify the software on your system</a>
<!-- *	<a href="#newbie-cpanel">Start the cPanel configuration utility</a> -->
*	<a href="{{ page.baseurl }}/install-gde/install/hosted/hosted_start_db.html">配置数据库和数据库用户</a>
*	<a href="{{ page.baseurl }}/install-gde/install/hosted/hosted_start_php.html">配置PHP</a>
*	<a href="{{ page.baseurl }}/install-gde/install/hosted/hosted_get-ftp.html">将Magento上传到你的服务主机</a>
*	<a href="{{ page.baseurl }}/install-gde/install/hosted/hosted_install.html">安装Magento</a>

<h2 id="newbie-verify">Verify the software on your system</h2>
Magento requires the following software to run:

*	Web server: Apache 2.2 or 2.4
*	Programming language: {% glossarytooltip bf703ab1-ca4b-48f9-b2b7-16a81fd46e02 %}PHP{% endglossarytooltip %} 5.6.x or 5.5.x 
*	Database: MySQL 5.6.x

<div class="bs-callout bs-callout-info" id="info">
  <p>We recommend you contact your shared hosting provider's technical support to verify all of the preceding are installed and get their assistance if any of the software is not installed.</p>
</div>

For complete details, see <a href="{{ page.baseurl }}/install-gde/system-requirements.html">System requirements</a>.

#### 下一步
<a href="{{ page.baseurl }}/install-gde/install/hosted/hosted_start_db.html">配置数据库和数据库用户</a>

<!-- <h2 id="newbie-cpanel">Start the cPanel configuration utility</h2>
To start configuring your hosted system:

1.	Log in with your provided credentials.
2.	On the first page, in the Web Hosting row, click **Manage**.
3.	If necessary, log in to cPanel.
 -->

