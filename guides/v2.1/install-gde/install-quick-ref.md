---
group: install_pre
subgroup: 01_resource
title: 安装快速指引(教程)
menu_title: 安装快速指引(教程)
menu_node:
menu_order: 2
version: 2.1
github_link: install-gde/install-quick-ref.md
functional_areas:
  - Install
  - System
  - Setup
---

We know it's challenging to install the Magento software. We'd like to help you by simplifying the process as much as possible.

This topic assumes:

*	You have your own Magento server (you're not using a shared hosting provider).
*	You're starting the installation using `composer create-project`, which enables you to get the most recent Magento software and to add your own customizations to it, if desired.
*	Everything is installed on one host (database, web server, and so on).
*	The host you're installing on is either Ubuntu or CentOS.

	(You can use the same instructions to install on other UNIX distributions like RedHat Enterprise Linux (RHEL), or Debian, but these instructions aren't for Mac or Windows.)
*	Your host's IP address is `192.0.2.5`.

	This is just an example IP address that you'll see in detailed examples throughout this topic. You can substitute it with whatever internal/external IP address matches your server.

*	You're installing to the `magento2` subdirectory under your web server's docroot (full path is `/var/www/html/magento2`)

	You can optionally set up static routing or a virtual host to install to a host name instead of an IP but that's beyond the scope of this topic.

We've broken the installation process into three main parts: getting started, installing, and post-installation. We hope that what follows helps you; if you'd like to suggest improvements, click **Edit this page on GitHub** at the top of this page and let us know.

## 前提条件：你足够专业吗？
Do you know what a "terminal" application is? Do you know what operating system your server runs? Do you know what Apache is?

If not, see the <a href="{{ page.baseurl }}/install-gde/bk-install-guide.html">安装概述</a>.

## 安装第1部分: 起步
1.	See the [system requirements]({{ site.baseurl }}/magento-system-requirements.html).
2.	If your system lacks any requirements, see the prerequisites documentation:

	*	<a href="{{ page.baseurl }}/install-gde/prereq/apache.html">Apache</a>
	*	<a href="{{ page.baseurl }}/install-gde/prereq/php-ubuntu.html">PHP (Ubuntu)</a>
	*	<a href="{{ page.baseurl }}/install-gde/prereq/php-centos.html">PHP (CentOS)</a>
	*	<a href="{{ page.baseurl }}/install-gde/prereq/mysql.html">MySQL</a>
3.	Just as importantly, set up the <a href="{{ page.baseurl }}/install-gde/prereq/file-sys-perms-over.html">Magento文件系统所有者</a> on the server.
4.	Switch to the {% glossarytooltip 5e7de323-626b-4d1b-a7e5-c8d13a92c5d3 %}Magento文件系统所有者{% endglossarytooltip %}.

### 获取Magento
When all prerequisites have been met, 获取Magento using {% glossarytooltip d85e2d0a-221f-4d03-aa43-0cda9f50809e %}Composer{% endglossarytooltip %} as follows:

	cd <web server docroot directory>
	composer create-project --repository-url=https://repo.magento.com/ magento/project-community-edition magento2

You're required to authenticate; see <a href="{{ page.baseurl }}/install-gde/prereq/connect-auth.html">获取你的认证密钥</a> for details. This downloads Magento code only; it doesn't install the software for you.

<div class="bs-callout bs-callout-tip">
	<p>Alternatively, you can also download a <a href="{{ page.baseurl }}/install-gde/install/get-software.html">Magento software archive</a>.</p>
</div>

{% include install/file-system-perms-before.md %}

## 安装第2部分: Installing the Magento software
You can choose to install the Magento software using either a <a href="{{ page.baseurl }}/install-gde/install/web/install-web.html">web-based Setup Wizard</a> or using the <a href="{{ page.baseurl }}/install-gde/install/cli/install-cli.html">command line</a>.

#### 命令行安装

{% collapsible Click to view the command-line installation %}

The following example shows how to install using the command line with the following options:

*	The Magento software is installed in the `/var/www/html/magento2` directory, which means your storefront URL is `http://192.0.2.5/magento2/`

*	数据库服务器和web服务器在同一台主机.

	数据库名叫`magento`,数据库用户名和密码都是`magento`

*	使用服务器重写

*	Magento管理员有以下属性：

	*	First and last name are `Magento User`
	*	用户名是`admin` ，密码是`admin123`
	*	邮箱地址是`user@example.com`

*	默认语言是`en_US` (U.S. English)
*	默认货币是U.S. dollars
*	默认时区是U.S. Central (America/Chicago)

		php /var/www/html/magento2/bin/magento setup:install --base-url=http://192.0.2.5/magento2/ \
		--db-host=localhost --db-name=magento --db-user=magento --db-password=magento \
		--admin-firstname=Magento --admin-lastname=User --admin-email=user@example.com \
		--admin-user=admin --admin-password=admin123 --language=en_US \
		--currency=USD --timezone=America/Chicago --use-rewrites=1

Optionally switch to <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-mode.html">developer mode</a>.

	cd <your Magento install dir>/bin
	php magento deploy:mode:set developer

{% endcollapsible %}

#### 网页安装向导

{% collapsible Click to view the Web 网页向导安装 %}

The following example shows how to install using the 网页安装向导 with the following options:

*	The Magento software is installed in the `magento2` directory relative to the web server docroot, which means your storefront URL is `http://192.0.2.5/magento2/`

*	数据库服务器和web服务器在同一台主机.

	数据库名叫`magento`,数据库用户名和密码都是`magento`

*	Magento管理员有以下属性：

	*	用户名是`admin` ，密码是`admin123`
	*	邮箱地址是`user@example.com`

*	默认语言是`en_US` (U.S. English)
*	默认货币是U.S. dollars
*	默认时区是U.S. Central (America/Chicago)

To run the 网页安装向导:

1.	Enter the following URL in your browser's address or location field:

		http://192.0.2.5/magento2/setup
2.	At the welcome page, click **Agree and Setup Magento**.

	![You must accept the license agreement to install the Magento software]({{ site.magentourl }}/common/images/install_qr_wizard-welcome.png){:width="200px"}
3.	步骤1. Readiness Check verifies your system is ready to install the Magento software.

	Click **Start Readiness Check**

	![The Readiness Check makes sure your system is ready for the Magento software]({{ site.magentourl }}/common/images/install_qr_readiness.png){:width="400px"}

	*	If the readiness check passes, click **Next** and continue with the next step.
	*	If the readiness check fails, see [就绪检查的问题]({{ page.baseurl }}/install-gde/trouble/readiness/tshoot_rc_main.html)
4.	步骤2. Add a Database enables you to set up your Magento database.

	![Set up your Magento database]({{ site.magentourl }}/common/images/install_qr_database.png){:width="400px"}
5.	步骤3. Web Configuration enables you to enter the storefront and Magento Admin URLs.

	![Enter your storefront and Magento Admin URLs]({{ site.magentourl }}/common/images/install_qr_web.png){:width="400px"}
6.	步骤4. Customize Your Store enables you to enter a default store currency, time zone, and language.

	![Customize the store's language, time zone, currency]({{ site.magentourl }}/common/images/install_qr_store.png){:width="400px"}
7.	步骤5. Create Admin Account enables you to set up a Magento administrator. This user can perform all actions in the Magento Admin.

	![Create a Magento administrator account]({{ site.magentourl }}/common/images/install_qr_admin.png){:width="400px"}
8.	步骤6. Install starts the installation when you click **Install Now**.

	You can optionally expand **Console Log** to see installation messages while the installation is in progress.

{% endcollapsible %}


## 安装第3部分: 安装完成之后
*	<a href="{{ page.baseurl }}/install-gde/install/verify.html">验证你的安装</a> was successful.
*	Learn about the <a href="{{ page.baseurl }}/comp-mgr/bk-compman-upgrade-guide.html">Component Manager and System Upgrade</a> for future updates.
