---
group: install_cli
subgroup: 99_contrib
title: 重新安装Magento
menu_title: 重新安装Magento
menu_order: 200
menu_node:
version: 2.1
github_link: install-gde/install/cli/dev_reinstall.md
functional_areas:
  - Install
  - System
  - Setup
---

作为一名贡献开发者，你可以通过修改`composer.json`指定你想要的Magento的及其组件的版本，然后执行`composer update`. 

贡献开发者重新安装:

2.	用一个拥有你magento文件权限的用户登录到你的Magento系统，(例如, <a href="{{ page.baseurl }}/install-gde/prereq/file-sys-perms-over.html">>切换到magento文件拥有者身份</a>.
3.	在你的Magento目录下备份 `composer.json`:

		cd <your Magento install dir>
		cp composer.json composer.json.bak

4.	用编辑器打开`composer.json`.
5.	找到下面的行:

		 "require": {
        	"magento/product-community-edition": "<version>"
    	},

5.	 用你要升级到的的版本号替换 `<version>`,`<version>`表示你的产品用到的Magento的版本. 
	
	(这版本号的格式类似于`2.0.x`)
<!-- is the `magento/product-community-edition` version from -->.
5.	保存并关闭`composer.json`.
6.	执行下面的命令:

		composer update

	等待依赖更新完成.

4.	<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli.html">安装Magento2</a>.

*[贡献开发者]: 参与Magento 2 CE基础代码开发的开发者
