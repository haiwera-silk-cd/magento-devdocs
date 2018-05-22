---
group: install_cli
subgroup: 99_contrib
title: 新增或更新组件
menu_title: 新增或更新组件
menu_order: 5
menu_node:
version: 2.1
github_link: install-gde/install/cli/dev_add-update.md
functional_areas:
  - Install
  - System
  - Setup
---

贡献开发者通过在`composer.json`中指定组件和组件的版本来更新这个组件 

如果你不是一个贡献开发者，要更新你的组件请参考<a href="{{ page.baseurl }}/comp-mgr/bk-compman-upgrade-guide.html">更新Magento及其组件</a>.

你可以在`composer.json`添加一条`require`语句或直接通过执行`composer require`命令来更新，如下

1.	登录到你的Magento服务器, 切换到{% glossarytooltip 5e7de323-626b-4d1b-a7e5-c8d13a92c5d3 %}Magento文件所有者身份{% endglossarytooltip %}.
2.	去到你安装Magento的目录，例如,

		cd /var/www/magento2

你可以选择:

### 使用`composer require`命令
用法:

	composer require <vendor>/<name>:<version>

比如这样,

	composer require example/module:1.0.0

等待{% glossarytooltip d85e2d0a-221f-4d03-aa43-0cda9f50809e %}Composer{% endglossarytooltip %}更新依赖并安装这个组件

### 添加`require`语句到`composer.json`
用编辑器打开`composer.json`.

添加如下`require`语句:

```JSON
	"require": {
		"<vendor>/<name>": "<version>",
		"<vendor>/<name>": "<version>"
	}
```

保存更改`composer.json`, 退出编辑器, 键入`composer update`并执行

### 更多信息
如果你遇到什么问题，请参考<a href="https://getcomposer.org/doc/articles/troubleshooting.md" target="_blank">Composer故障排除</a>.

<!-- ABBREVIATIONS -->

*[贡献者]: 参与Magento 2基础代码开发的开发者
