---
group: install_cli
subgroup: 99_contrib
title: 更新Magento
menu_title: 更新Magento
menu_order: 2
menu_node:
version: 2.1
github_link: install-gde/install/cli/dev_update-magento.md
redirect_from: /guides/v2.0/install-gde/install/cli/instgde-install-magento-update-db
functional_areas:
  - Install
  - System
  - Setup
---

这里讨论一个贡献开发者如何不用重装来更新Magento. 如果你不是贡献开发者，要执行升级，请参考<a href="{{ page.baseurl }}/comp-mgr/bk-compman-upgrade-guide.html">更新和升级Magento及其组件</a>.

如果你不是贡献开发者，要执行Magento更新

1.	用Magento文件所有者的身份登录或切换到<a href="{{ page.baseurl }}/install-gde/prereq/file-sys-perms-over.html">Magento文件所有者身份</a>.
3. 保存你对`composer.json`做的更改，因为下面的操作将会覆盖它:

		cd <your Magento install dir>
		cp composer.json composer.json.old

3.	获取最新的代码更新你本地的仓库:
		
		git pull origin develop

	<div class="bs-callout bs-callout-info" id="info">
		<span class="glyphicon-class">
  			<p>如果<code>git pull origin develop</code>失败,请参考<a href="{{ page.baseurl }}/install-gde/trouble/git/tshoot_git-pull-origin.html">问题排除</a>.</p> </span>
	</div>
				
3.	对比并合并`composer.json.old`和安装有Magento的`composer.json`
4.	执行下面的命令:

		composer update

5.	更新Magento的数据库:

		php <your Magento install dir>/bin/magento setup:upgrade

<!-- ABBREVIATIONS -->

*[贡献开发者]: 参与Magento 2 CE基础代码开发的开发者
