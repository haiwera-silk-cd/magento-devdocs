---
group: install_pre
subgroup: 01_resource
title: 快速安装参考（教程）
menu_title: 快速安装参考（教程）
menu_node:
menu_order: 2
version: 2.2
github_link: install-gde/install-quick-ref.md
functional_areas:
  - Install
  - System
  - Setup
---

我们知道安装Magento是一种挑战，我们尽可能的简化这个过程来帮助你

在这里我们假设:

*	你有你自己的Magento服务器(没有使用主机服务商提供的共享主机).
*	你正在使用`composer create-project`安装, 这种方法可以获取到最新的Magento版本，如果你想，这种方法也可以添加你自己的定制的功能到Magento.
*	单机部署 (数据库, web服务, 等等在同一台机器上).
*	你已经在机器上安装了Ubuntu或CentOS

	(你可以在其它的分布的UNIX主机上使用相同的指令安装，比如RedHat Linux企业版或Debian,但是这些命令并不适用于windows或mac)
*	你的主机ip是`192.0.2.5`.

	这个ip仅是一个示例，我们在这里会一直用这个ip进行演示,你可以用你自己服务器的本地局域网ip或静态ip代替它。

*	你正在安装到服务器的docroot下的`magento2`这个子目录(完整的路径是`/var/www/html/magento2`)

	你可以选择为其设置一个静态路由或一个虚拟主机来安装，而不是直接装在ip下面，但这超出了本节的内容

我们已经把安装过程分为了三个部分：起步，安装和后续操作，我们希望能帮到你，如果你有更好的建议，点击右上角的**在GitHub上编辑** 来告诉我们

## 前提: 你够专业吗?

你知道"终端"这个就用程序吗？你知道你的服务器用的操作系统吗？你知道什么是Apache吗？

如果你不知道，请参考<a href="{{ page.baseurl }}/install-gde/bk-install-guide.html">安装概览</a>.

## 第一部分: 起步
1.	参考[系统要求]({{ site.baseurl }}/magento-system-requirements.html).
2.	如果你的系统未满足下列条件之一，请参考我们的关于先决条件的文档:

	*	<a href="{{ page.baseurl }}/install-gde/prereq/apache.html">Apache</a>
	*	<a href="{{ page.baseurl }}/install-gde/prereq/php-ubuntu.html">PHP (Ubuntu)</a>
	*	<a href="{{ page.baseurl }}/install-gde/prereq/php-centos.html">PHP (CentOS)</a>
	*	<a href="{{ page.baseurl }}/install-gde/prereq/mysql.html">MySQL</a>
3.	强调一下, 设置在服务器上<a href="{{ page.baseurl }}/install-gde/prereq/file-sys-perms-over.html">Magento的文件所有者</a>是非常重要的.
4.	去看看{% glossarytooltip 5e7de323-626b-4d1b-a7e5-c8d13a92c5d3 %}Magento文件所有者{% endglossarytooltip %}.

### 获取Magento
当满足了所有的先决条件，使用composer{% glossarytooltip d85e2d0a-221f-4d03-aa43-0cda9f50809e %}Composer{% endglossarytooltip %}来获取Magento,如下:

	cd <web server docroot directory>
	composer create-project --repository-url=https://repo.magento.com/ magento/project-community-edition magento2

执行过程中会进行身份验证; 参考 <a href="{{ page.baseurl }}/install-gde/prereq/connect-auth.html">获取认证密钥</a>获取更多信息. 这一步仅仅只下载了Magento的代码; 并没有为你安装.

<div class="bs-callout bs-callout-tip">
	<p>这里，你也可以下载一个<a href="{{ page.baseurl }}/install-gde/install/get-software.html">Magento安装包</a>.</p>
</div>

{% include install/file-system-perms-before_22.md %}

## 第二部分: 启动安装
你可以选择使用<a href="{{ page.baseurl }}/install-gde/install/web/install-web.html">网页向导</a>或<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli.html">命令行</a>进行安装.

#### 命令行安装

{% collapsible Click to view the command-line installation %}

下面的例子演示了用命令行安装时如何使用这些命令行参数

*	Magento安装在`/var/www/html/magento2`目录下, 表示你的网店前台的地起是`http://192.0.2.5/magento2/`

*	数据库和web服务器在同一台主机上.

	数据库名称是`magento`, 用库名和密码都是`magento`

*	使用服务器重写

*	下面是Magento管理员的一些信息:

	*	姓名`Magento User`
	*	用户名是`admin` 密码是`admin123`
	*	电子邮箱是`user@example.com`

*	默认语言 `en_US` (U.S. English)
*	默认货币 U.S. dollars
*	默认时区 U.S. Central (America/Chicago)

		php /var/www/html/magento2/bin/magento setup:install --base-url=http://192.0.2.5/magento2/ \
		--db-host=localhost --db-name=magento --db-user=magento --db-password=magento \
		--admin-firstname=Magento --admin-lastname=User --admin-email=user@example.com \
		--admin-user=admin --admin-password=admin123 --language=en_US \
		--currency=USD --timezone=America/Chicago --use-rewrites=1

你可以选择切换到<a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-mode.html">开发模式</a>.

	cd <your Magento install dir>/bin
	php magento deploy:mode:set developer

{% endcollapsible %}

#### 网页向导安装

{% collapsible Click to view the Web Setup Wizard installation %}

下面展示了网页向导安装的一些选项和属性:

*	Magento目录放在关联到web服务的docroots下的`magento2`目录中, 对应的网店前端地址是`http://192.0.2.5/magento2/`

*	数据库和web服务在同一台主机.

	数据库名称是`magento`, 用户名和密码都是`magento`

*	下面是管理员的信息:

	*	用户名是 `admin` 密码是 `admin123`
	*	电子邮箱 `user@example.com`

*	默认语言 `en_US` (U.S. English)
*	默认货币 U.S. dollars
*	默认时区 is U.S. Central (America/Chicago)

执行网页向导:

1.	在浏览器地址栏输入下面的地址:

		http://192.0.2.5/magento2/setup
2.	在欢迎页点击 **同意并安装**.

	![你必须接受Magento的许可协议]({{ site.magentourl }}/common/images/install_qr_wizard-welcome.png){:width="200px"}
3.	第一步: 检查您的系统是否已经准备就绪安装Magento.

	点击 **开始就绪检查**

	![就绪检查确保了你的系统已经具备了安装Magento的条件]({{ site.magentourl }}/common/images/install_qr_readiness.png){:width="400px"}

	*	如果检查通过, 点击 **下一步** 继续.
	*	如果没有通过, 请参考[就绪检查]({{ page.baseurl }}/install-gde/trouble/readiness/tshoot_rc_main.html)
4.	第二步: 添加一个给Magento用的数据库.

	![设置Magento数据库]({{ site.magentourl }}/common/images/install_qr_database.png){:width="400px"}
5.	第三步: 站点配置页允许你为你的网店的前台和后台设置访问URL.

	![输入网页URL]({{ site.magentourl }}/common/images/install_qr_web.png){:width="400px"}
6.	第四步: 用户配置页允许你配置默认货币、时区和语言.

	![配置默认货币、时区和语言]({{ site.magentourl }}/common/images/install_qr_store.png){:width="400px"}
7.	第五步: 创页管理帐号页允许你创建Magento管理员. 这个管理员有Magento的所有权限.

	![创建Magento管理员]({{ site.magentourl }}/common/images/install_qr_admin.png){:width="400px"}
8.	第六步: 开始安装，点击**现在安装**开始安装.

	你可以展开**控制台输出**查看安装过程中输出的日志信息.

{% endcollapsible %}


## 第三部分: 后续操作
*	<a href="{{ page.baseurl }}/install-gde/install/verify.html">验证</a>安装是否成功.
*	了解<a href="{{ page.baseurl }}/comp-mgr/bk-compman-upgrade-guide.html">组件管理和系统升级</a>为将来更新做准备.
