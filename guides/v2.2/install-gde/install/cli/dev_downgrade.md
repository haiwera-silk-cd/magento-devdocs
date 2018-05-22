---
group: install_cli
subgroup: 99_contrib
title: 切换到一个发布版
menu_title: 切换到一个发布版
menu_order: 200
menu_node:
version: 2.2
github_link: install-gde/install/cli/dev_downgrade.md
functional_areas:
  - Install
  - System
  - Setup
---

这里讨论一个贡献开发者在克隆了`develop`分支之后如何切换到一个Magento的版本， 对于一些特定版本需要执行任务这可能是必要做的；

`develop`是默认分支，这意味着你从github上克隆下来的Magento2默认就在这个分支上，有些诸如从Magento 1.x迁移数据到Magento 2.x之类的任务，你必须切换到一个<a href="https://github.com/magento/magento2/tags" target="_blank">发布标签</a>上.

你可以选择：

*	*(更简单的方式)*. 如果你没有进行作何更改，你可以卸载Magento然后重装对应的发布版. 卸载不仅要删除所有数据表，还要清空`var`目录, 这样重头开始是不会有什么问题的.

	更多信息请参考[重新安装来改变Magento的版本](#downgrade-uninstall)
*	如果你已经完成了一些开发并不希望丢失它们，你要先备份当前的Magento, 然后切换到发布分支,然后安装到一个新的数据库.

	更多信息请参考[切换到发布版本并将Magento安装到新的数据库](#downgrade-db)

	你可以从备份中迁移你的修改(包括数据库和文件)或者直接使用数据库和文件系统工具。

### 使用重装的方法切换Magento的版本{#downgrade-uninstall}

要在克隆后切换版本:

1.	用Magento文件所有者身份登录到服务器或切换到<a href="{{ page.baseurl }}/install-gde/prereq/file-sys-perms-over.html">Magento文件所有者身份</a>.
2.	使用以下命令卸载Magento:

		php <your Magento clone dir>/bin/magento setup:uninstall
3.	删除老的克隆的Magento的目录或<a href="{{ page.baseurl }}/install-gde/install/cli/dev_update-magento.html">升级Magento</a>.
4.	如果你已经完成了上面的步骤，用下面的方法从GitHub重新克隆Magento 2，如下:

		git clone git@github.com:magento/magento2.git
5.	用下面的方法切换到<a href="https://github.com/magento/magento2/tags" target="_blank">发布标签</a>:

		git checkout tags/<tag name>  [-b <branch name>]

	例如, 要切换到2.2.0到一个新的`2.2.0`分支, 执行

		git checkout tags/2.2.0 -b 2.2.0

5.	使用<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-install.html">命令行</a>或<a href="{{ page.baseurl }}/install-gde/install/web/install-web.html">网页向导</a>安装Magento.

### 切换版本把Magento安装到一个新的数据库中{#downgrade-db}

要在克隆后切换版本:

1.	用Magento文件所有者身份或切换到<a href="{{ page.baseurl }}/install-gde/prereq/file-sys-perms-over.html">Magento文件所有者身份</a>登录到Magento服务器.
2.	为你的安装创建一个<a href="{{ page.baseurl }}/install-gde/prereq/mysql.html#instgde-prereq-mysql-config">新的数据库</a>.
2.	<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-backup.html#instgde-cli-uninst-back">备份</a>旧的Magento的文件、数据库和media里的文件:

		php <your Magento install dir>/bin/magento setup:backup --code --media --db
3.	用下面的方法切换到<a href="https://github.com/magento/magento2/tags" target="_blank">发布标签</a>:

		git checkout tags/<tag name>  [-b <branch name>]

	例如,要切换到2.2.0发布签到一个新的`2.2.0`分支, 执行

		git checkout tags/2.2.0 -b 2.2.0

4.	手动清空`var`目录:

		rm -rf <your Magento install dir>/var/cache/* <your Magento install dir>/var/page_cache/* <your Magento install dir>/generated/code/*

5.	安装Magento到你创建的新数据库中.

	你可以使用<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-install.html">命令行</a>或<a href="{{ page.baseurl }}/install-gde/install/web/install-web.html">网页向导</a>进行安装.

<!-- ABBREVIATIONS -->

*[贡献开发者]: 参与{{site.data.var.ce}}基础代码开发的开发者